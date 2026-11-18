<!-- 이 파일은 posts/2026-11-18.md의 사본입니다. 자동 생성됨. -->
# 2026-11-18 기술 블로그 모음

## [컨테이너처럼 쓰고, VM처럼 격리하기 1편 - 컨테이너와 VM의 차이, Kata Containers의 Pod 실행 구조](https://d2.naver.com/helloworld/8055238)
- 회사: 네이버 D2
- 본문 요약: 불특정 다수가 B200 8-GPU 서버를 공유하는 Kubernetes 환경에서 사용자별 격리를 위해 Kata Containers(4.1.0)를 도입한 4부작의 첫 편입니다. 컨테이너는 호스트 커널을 공유하므로 runc·NVIDIA Container Toolkit 취약점(CVE-2024-21626, CVE-2024-0132, NVIDIAScape CVE-2025-23266, 2025년 11월 runc CVE 3건)이 곧바로 호스트 침해로 이어질 수 있다는 점을 짚고, VT-x/KVM·QEMU·VM exit·virtio의 동작과 kata shim → QEMU → kata-agent(vsock)로 Pod가 VM 안에서 실행되는 구조를 설명합니다. Cilium이 만든 veth(eth0)는 게스트 커널에 보이지 않으므로 kata가 tap을 만들고 tc 리다이렉트(tcfilter)로 eth0↔tap을 잇고, vhost-net으로 왕복을 줄여 Pod IP·Service·DNS를 그대로 쓰게 합니다.
- 주목할 point: "알려지지 않은 취약점까지 한 사용자 안에 가두려면 커널을 공유하지 않아야 한다"는 요구에서 출발해, VM 격리와 Pod 운영 편의를 동시에 얻는 선택지로 kata를 고른 근거가 명확합니다. `ip netns`, `tc filter show`, `ethtool -i eth0`로 연결을 직접 확인하는 방법을 제시하고, 이후 편에서 다룰 4가지 이슈(GPU 8장 VM 부팅·크기·NUMA, NVLink 조합, IB·NVMe, vCPU 배치)를 표로 정리했습니다.
- keyword: #KataContainers #Kubernetes #컨테이너탈출 #KVM #QEMU #Cilium #GPU격리

## [컨테이너처럼 쓰고, VM처럼 격리하기 2편 - GPU 패스스루 계층과 GPU 8장 VM의 부팅·메모리 구성](https://d2.naver.com/helloworld/1376800)
- 회사: 네이버 D2
- 본문 요약: GPU가 IOMMU(DMA 주소 변환·격리) → VFIO(vfio-pci로 호스트 드라이버에서 분리해 QEMU에 전달) → CDI(컨테이너 장치 주입) 계층을 거쳐 VM 안 컨테이너에 도달하는 과정과, ACS로 IOMMU 그룹을 245개로 나눠 GPU 한 장씩 할당하는 원리를 설명합니다. GPU 8장 VM은 kubelet 샌드박스 대기 한도(4분) 안에 부팅하지 못했는데, 256GiB BAR를 4KiB 페이지로 매핑하는 비용은 `transparent_hugepage=always`(커널 6.12+ vfio-pci가 BAR도 큰 페이지로 매핑)로, 게스트 메모리 2,688GiB 사전 할당 비용은 1GiB hugepage 2,688개 예약으로 줄여 141~151초에 Ready가 되었습니다.
- 주목할 point: 업스트림 kata가 `hugepages-1Gi` 요청량을 VM 크기 계산에서 빼 14GiB를 요청해도 10GiB VM이 만들어지던 문제를 KubeVirt 방식을 참고해 수정(업스트림 PR #13853 제안)했고, `enable_numa`·`numa_mapping`으로 게스트를 호스트와 같은 2-NUMA 구성으로 맞추자 GPU→호스트 복사 합산 대역폭이 약 410GB/s에서 459.0GB/s로 올랐습니다.
- keyword: #GPU패스스루 #IOMMU #VFIO #CDI #Hugepage #THP #NUMA #KataContainers

## [컨테이너처럼 쓰고, VM처럼 격리하기 3편 - Fabric Manager 파티션과 DRA를 이용한 GPU 할당](https://d2.naver.com/helloworld/6180316)
- 회사: 네이버 D2
- 본문 요약: B200 서버의 NVSwitch는 Fabric Manager가 정한 파티션(8장 1개, 4장 2개, 2장 4개, 1장 8개 등 15개) 단위로만 NVLink를 연결하기 때문에 "GPU 2장"을 아무 조합으로나 줄 수 없습니다. 개수만 요청하는 장치 플러그인으로는 이 제약을 보장하지 못해 DRA(동적 리소스 할당) 드라이버를 직접 만들어 파티션 디바이스를 발행하고 SharedCounters로 겹치는 파티션의 동시 할당을 막았습니다. 업스트림 kata shim은 PodResources API에서 DRA 디바이스를 읽지 않아 VM이 GPU 없이 부팅되었기에, 클레임 단위로 GPU·NIC를 읽어 정해진 순서로 루트 포트에 콜드 플러그하도록 수정했습니다(PR #13323, #13420).
- 주목할 point: 서버 한 대를 GPU 1+1+2+4장 VM 4개로 나눠 동시에 돌린 상태에서 NCCL all_reduce 버스 대역폭이 2장 623.5GB/s, 4장 680.7GB/s, 8장 단독 835.9GB/s로 베어메탈 대비 1% 이내였습니다. `kubectl get resourceslices`/`resourceclaims`와 게스트 안 `all_reduce_perf`로 할당 결과를 검증하는 절차도 함께 보여줍니다.
- keyword: #DRA #NVLink #FabricManager #NVSwitch #NCCL #Kubernetes #GPU할당

## [컨테이너처럼 쓰고, VM처럼 격리하기 4편 - IB 네트워크와 로컬 NVMe, vCPU 배치, 베어메탈 대비 성능](https://d2.naver.com/helloworld/5896967)
- 회사: 네이버 D2
- 본문 요약: VM 안 분산 학습을 위해 GPU와 같은 PCIe 스위치의 컴퓨트 IB NIC(PF·레일셋)와 스토리지 VF를 연결하고, NCCL 토폴로지 파일과 ACS DT 비트로 GPUDirect RDMA 경로를 확보했으며, 로컬 NVMe는 SPDK vhost-user-blk와 논리 볼륨으로 여러 VM에 나눠 줬습니다. vCPU 배치 오류로 생긴 성능 저하·게스트 멈춤은 kubelet static CPU 정책과 strict-cpu-reservation, vCPU 1:1 고정, 예약 CPU 제외로 해결해 CPU steal을 0으로 만들었습니다. 사용자는 runtimeClassName·resourceClaims·`hugepages-1Gi`만 더한 Pod YAML 하나로 VM을 씁니다.
- 주목할 point: 베어메탈 대비 성능 비교가 솔직합니다 — vLLM 추론 출력 처리량은 0.4~7% 낮고 TPOT는 차이가 없었지만, TTFT 142.1→181.4ms, 스텝당 16k 토큰 학습 514→716ms(131k 토큰은 956→998ms), 콜드 스타트 537→980초로 차이가 컸고, 원인은 CUDA 커널 제출 경로(3.96µs→5.83µs)와 VM 부팅·워밍업이었습니다. 격리 경계가 하이퍼바이저로 옮겨간 만큼 하이퍼바이저 취약점 패치가 새 숙제라는 점도 짚습니다.
- keyword: #InfiniBand #GPUDirectRDMA #SPDK #NVMe #vCPU #CPU고정 #KataContainers #성능비교

## [[현장 스케치] AI 인프라의 경쟁력, 이제는 '통합'이다! - 2026 OCP Global Summit](https://tech.ktcloud.com/entry/2026-11-ktcloud-ocp-2026-ai-infrastructure-integration)
- 회사: KT 클라우드
- 본문 요약: 2026년 10월 12~15일 산호세에서 열린 OCP Global Summit(참가 약 1만 5천 명, 578개 세션) 참관기입니다. AMD의 랙 스케일 플랫폼 Helios와 에이전틱 AI용 개방형 랙 설계 Helion, NVIDIA의 Vera Rubin 랙·컴퓨트 트레이 설계 OCP 기여와 MGX 1.2, SK하이닉스의 CXL 메모리 풀링·KV 캐시 공유(MARS), ABB·Eaton의 800V DC 배전과 SST, Delta의 사이드카 기반 단계적 800V DC 전환과 2.5MW급 In-row CDU, NPO·CPO 광통신과 Lumentum의 레이저 광원(ILS/ELS), Meta의 ESUN·OSPA 개방형 네트워킹을 소개합니다.
- 주목할 point: 경쟁의 축이 개별 GPU 성능에서 전력·냉각·메모리·네트워크를 랙 단위로 통합하는 쪽으로 옮겨갔다는 관찰이 핵심입니다. 800V DC의 아크 차단(SSCB)·상호운용성 과제, CDU 펌프·필터·센서 이중화와 핫스왑, 광원 배치에 따른 유지보수성처럼 "운영 안정성"을 함께 다룬 점이 데이터센터 운영사 관점에서 의미 있습니다.
- keyword: #OCPGlobalSummit #랙스케일 #800VDC #액체냉각 #CXL #CPO #AI데이터센터

## [[사례연구] Harbor와 Gitea를 멀티 AZ Active-Active로 바꾸기](https://tech.ktcloud.com/entry/2026-11-ktcloud-harbor-gitea-multi-az-active-active)
- 회사: KT 클라우드
- 본문 요약: 단일 AZ에 기대던 레지스트리(Harbor)와 git(Gitea)을 두 AZ를 묶은 단일(Federated) 클러스터 위 Active-Active로 전환한 사례입니다. 진입점을 공통 externalURL과 두 AZ 파드를 묶는 스패닝 Service로 합치고, Harbor A·B 인스턴스가 토큰 서명 키를 공유하게 해(core.secretName) AZ를 넘나들 때 생기던 간헐적 401을 없앴습니다. 트래픽은 zone-aware(preferLocal) + 헬스체크 failover로 평소엔 로컬 AZ를, 장애 시엔 다른 AZ를 쓰게 했고, 운영 라우트 backendRef를 2단계로 옮겨 무중단 컷오버했습니다.
- 주목할 point: "상태의 종류가 처방을 정한다"는 정리가 핵심입니다 — 토큰 서명 키는 공유(PKCS#8이 아닌 PKCS#1 PEM이어야 했던 함정 포함), Gitea OIDC 로그인 세션은 sticky 또는 세션 저장소 공유, 파일 볼륨은 Multi-Attach를 피하려 인스턴스별로 분리. 반면 Raft로 스스로 복제하는 Vault와 상태 없는 ArgoCD는 replica를 AZ에 분산하는 것만으로 충분했다는 대비가 실무적입니다.
- keyword: #Harbor #Gitea #멀티AZ #ActiveActive #EnvoyGateway #고가용성 #OIDC

## [[기술 트렌드] 2026 아태지역 데이터센터 지형도: AI 수요 폭발과 전력망의 한계](https://tech.ktcloud.com/entry/2026-11-ktcloud-apac-ai-data-centers-power-grid)
- 회사: KT 클라우드
- 본문 요약: 아태 데이터센터 수요의 동력이 클라우드 마이그레이션에서 AI 연산으로 바뀌고, GPUaaS에 특화된 네오클라우드가 수십 MW 단위 블록 딜로 초기 물량을 선점하고 있다고 분석합니다. 랙당 100kW 이상 고밀도 가속기로 100MW~GW급 캠퍼스가 필요해졌지만 전력망 확충이 따라가지 못해 건설 단가가 치솟았고(도쿄·싱가포르 최고 수준), 수요는 싱가포르 모라토리엄의 스필오버를 흡수한 말레이시아 조호르(2025년 가동 용량 50% 이상 증가)와 인도·태국·인도네시아로 남하하고 있습니다.
- 주목할 point: 한국(수도권)은 공실률 5% 미만으로 사실상 완전 임대 상태이고 수전 제약 때문에 100MW 이상 캠퍼스가 어려워 부산 등 남부권 메가 캠퍼스로 수요가 이동 중이라는 진단과, 도심형은 저지연 엣지로·대규모 학습 클러스터는 지방 100MW급 캠퍼스로 나누는 '투 트랙' 전략 제안이 눈에 띕니다. 투자 측면에서도 토지·용도 변경 등 밸류애드와 플랫폼 M&A가 늘었다는 흐름을 짚습니다.
- keyword: #APAC데이터센터 #네오클라우드 #GPUaaS #전력망 #하이퍼스케일 #조호르 #AI데이터센터

## [[기술 분석] 고조파가 역률개선용 커패시터에 미치는 영향과 대책](https://tech.ktcloud.com/entry/2026-11-ktcloud-harmonics-capacitor-resonance)
- 회사: KT 클라우드
- 본문 요약: 역률개선용 콘덴서는 용량성 리액턴스가 주파수에 반비례해 고조파 전류가 집중 유입되고, 계통 인덕턴스와 병렬공진 조건(nX₀ = nXL − Xc/n)이 맞으면 특정 차수 고조파가 수십 배 증폭된다는 원리를 등가회로와 수식으로 설명합니다. 계통 측 대책으로 6% 직렬리액터를 넣어 5차(300Hz) 이상에서 회로를 유도성으로 만들어 공진을 막고, 콘덴서 자체의 과전류·단자전압 상승·실효용량 증가에 따른 소손·열화에는 KS/IEC 허용전류·과전압 기준에 맞춘 정격 여유 설계로 대응합니다.
- 주목할 point: 리액터 비율별(4%·6%·13%) 유도성 전환 차수 비교와, AIDC 수전설비 콘덴서 선정 시 "6% 리액터 병용, 정격전류 기본파 × 1.3 이상, THD가 높으면 능동필터(APF) 병용"이라는 실무 체크리스트가 유용합니다. 국내 계통에서 5차 고조파가 지배적이기 때문에 6%가 표준이라는 근거도 함께 제시합니다.
- keyword: #고조파 #역률개선 #병렬공진 #직렬리액터 #전력품질 #AI데이터센터

## [Claude에서 사내 데이터를 안전하게: 한국일보의 Amazon Bedrock AgentCore Gateway 기반 사내 MCP 게이트웨이 구축기](https://aws.amazon.com/ko/blogs/tech/hankookilbo-agentcore-gateway-rbac/)
- 회사: AWS
- 본문 요약: 한국일보가 2026년 10월 27일부터 운영 중인 사내 MCP 게이트웨이 HAI Connector를 소개합니다. Amazon Bedrock AgentCore Gateway 위에 타깃 9개(기사 검색, 행동 로그, 클라우드 비용, GA·Search Console 등)를 하나의 MCP 엔드포인트로 묶고, 구성원이 Microsoft 365(Entra ID) 계정으로 claude.ai·Claude Code에서 로그인하게 했습니다. 인바운드 JWT 인증 위에 요청 인터셉터(tools/call 거부)와 응답 인터셉터(tools/list에서 권한 밖 도구 제거)가 같은 권한표(S3의 permissions.json)를 공유하고, 행동 로그 조회는 역할별 IAM role을 수임해 Athena에서 테이블 단위로 한 번 더 제한합니다.
- 주목할 point: 권한별로 도구를 복제하거나 권한 조합마다(2ⁿ−1) DB 계정을 만드는 대신, 도구는 시스템 단위로 하나만 두고 "보이는 목록"을 역할로 바꾸는 설계가 깔끔합니다. 클라이언트가 보낸 신원·role 인자를 인터셉터가 항상 덮어쓰도록 단위 테스트로 고정했고, 권한표는 60초 ETag 폴링으로 재배포 없이 반영되며, AgentCore Policy(Cedar)는 배열 클레임을 정확히 비교하지 못해(like만 동작) 채택하지 않았다는 검토 결과도 공유합니다. 도메인 지식은 RAG 대신 목차를 먼저 주고 모델이 필요한 문서를 고르게 했습니다.
- keyword: #AmazonBedrock #AgentCoreGateway #MCP #Claude #RBAC #EntraID #Athena #인터셉터

## [AI Infra Summit 2026: 늘어나는 AI 추론 비용, LPU가 제시하는 새로운 해법](https://hyper-accel.github.io/posts/ai-infra-summit-review/)
- 회사: 하이퍼엑셀
- 본문 요약: 2026년 9월 15~17일 산타클라라에서 열린 AI Infra Summit(등록 9,200명, 파트너사 250여 곳) 참관기입니다. 현장에서 본 4가지 흐름으로 병목이 모델이 아니라 용량·전력·토큰당 비용으로 이동(FuriosaAI: 1년 새 토큰 수요 20배), 칩을 넘어선 랙 스케일 경쟁과 Sovereign AI(리벨리온의 RebelServer·Rack·POD), NVIDIA DSX MaxLPS 등 전력 최적화와 Extreme Co-design, Prefill/Decode 분리와 저지연 표준화(d-Matrix)를 꼽습니다. 하이퍼엑셀은 골드 스폰서로 첫 단독 부스를 운영하며 LPU BERTHA 실시간 데모를 선보였습니다.
- 주목할 point: 김주영 대표 발표의 문제의식 — 토큰 단가는 내려가는데 추론·에이전틱 토큰과 긴 컨텍스트로 작업 1건당 토큰 수가 폭증해 총비용은 늘어난다 — 이 핵심이며, LPU가 LLM 추론에서 메모리 대역폭 활용률 평균 83%(최대 90% 이상)를 달성했다는 수치를 제시합니다. 와트·달러당 성능 최대 3~5배 향상은 워크로드와 비교 대상에 따라 다르다는 단서가 붙어 있고, 행사 리뷰 겸 자사 홍보 성격의 글입니다.
- keyword: #AIInfraSummit #LPU #AI추론 #토큰효율 #PD분리 #랙스케일 #AI반도체

## [Claude Code Skills, MCP, Hooks를 팀 표준으로 묶어보기](https://blog.bespinglobal.com/post/bundling-claude-code-skills-mcp-hooks-into-team-standards/)
- 회사: 베스핀글로벌
- 본문 요약: AI플랫폼엔지니어링팀이 Claude Code를 개인 생산성 도구가 아니라 팀 표준 워크플로우로 쓰기 위해 기능별 역할을 정리한 글입니다. 상시 규칙은 CLAUDE.md, 반복 절차는 Skills(`.claude/skills/`, 사용할 때만 로드), 이슈·PR·모니터링·문서 같은 외부 컨텍스트는 MCP, 포맷·린트·위험 명령 차단 같은 자동 검증은 Hooks(PreToolUse·PostToolUse·Stop 등)로 나누고, 설정 범위(Managed/User/Project/Local)로 공유 범위를 정하자고 제안합니다.
- 주목할 point: skill 이름 충돌 시 Enterprise > Personal > Project 우선순위라 개인 skill이 팀 skill을 덮어쓸 수 있다는 점, MCP로 가져온 로그·이슈·댓글이 프롬프트 인젝션 경로가 될 수 있어 읽기 전용·마스킹 기준이 필요하다는 점, 팀 공통은 project에 두되 개인 토큰은 절대 project 설정에 넣지 말라는 점 등 운영상 함정을 짚습니다. 데이터 플랫폼의 pipeline 변경 검토 워크플로우 하나부터 작게 시작하는 예시를 듭니다.
- keyword: #ClaudeCode #Skills #MCP #Hooks #CLAUDEmd #팀표준 #AI코딩

## [Anthropic Prompt Engineering을 Claude 업무 활용 기준으로 정리](https://blog.bespinglobal.com/post/anthropic-prompt-engineering-for-claude-work-guidelines/)
- 회사: 베스핀글로벌
- 본문 요약: Anthropic의 Prompt Engineering 인터랙티브 튜토리얼과 공식 문서를 데이터 플랫폼 업무 관점에서 다시 정리한 글입니다. 프롬프트를 고치기 전에 성공 기준과 테스트 방법부터 세우라는 원칙, Claude를 "맥락 없는 똑똑한 신입"처럼 보고 목적·입력·처리 기준·출력 형식·금지 사항을 명확히 쓰기, 긴 문서는 위에 두고 질문은 뒤에 두기, XML 태그로 지시·컨텍스트·예시 구분하기, 몇 개의 실제 예시로 결과 형식 고정하기, 역할 설정을 말투가 아닌 판단 기준으로 쓰기를 다룹니다.
- 주목할 point: "하지 말라"보다 "이렇게 하라"(예: "장황하게 쓰지 마" 대신 "5문장 이내")가 낫다는 점, 확실하지 않으면 추정으로 표시하고 문서에 없는 내용은 쓰지 않게 하는 제약으로 환각을 줄이는 방법 등을 장애 메모·기술 검토 프롬프트 예시와 함께 보여줍니다. Console의 평가 도구로 테스트 세트 기반 비교를 하자는 제안도 담았습니다.
- keyword: #PromptEngineering #Claude #XML태그 #FewShot #프롬프트평가 #LLM활용

## [Codex GitHub Actions로 PR 리뷰 자동화를 보는 관점](https://blog.bespinglobal.com/post/a-perspective-on-automating-pr-reviews-with-codex-github-actions-2/)
- 회사: 베스핀글로벌
- 본문 요약: OpenAI Codex로 PR 리뷰를 자동화하는 두 흐름 — PR에서 `@codex review`나 자동 리뷰로 리뷰어처럼 호출하는 방식과, `openai/codex-action@v1`을 GitHub Actions에 넣어 CI 작업으로 `codex exec`를 실행하는 방식 — 을 구분하고 운영 기준을 정리합니다. Action 방식은 PR 이벤트 → checkout(base/head ref 준비) → prompt-file 기반 리뷰 → final-message를 PR 코멘트로 게시하는 구조이며, 리뷰 기준을 `.github/codex/prompts/` 파일로 코드처럼 관리할 수 있습니다.
- 주목할 point: Codex 실행 job은 `contents: read`, 코멘트 게시 job만 `pull-requests: write`로 권한을 분리하고 `persist-credentials: false`를 쓰는 최소 권한 원칙과, P0/P1 수준 이슈만 짚고 스타일 지적은 빼도록 범위를 좁혀야 리뷰 피로가 줄어든다는 조언이 핵심입니다. AGENTS.md(지속 규칙)와 prompt-file(이번 작업 지시)의 역할 구분, comment-only부터 도입하자는 단계적 접근도 제안합니다.
- keyword: #Codex #GitHubActions #PR리뷰 #코드리뷰자동화 #최소권한 #AGENTSmd

## [Databricks Lakehouse 아키텍처를 다시 정리하며 배운 점(손재홍_AI플랫폼엔지니어링)](https://blog.bespinglobal.com/post/lessons-learned-from-revisiting-databricks-lakehouse-architecture/)
- 회사: 베스핀글로벌
- 본문 요약: Lakehouse를 단순히 Data Lake와 Warehouse를 합친 개념이 아니라 "데이터를 저장하는 방식과 믿고 운영하는 방식을 잇는 구조"로 다시 이해한 학습 정리입니다. Data Lake의 저비용·다양성과 Warehouse의 안정성·거버넌스를 오브젝트 스토리지 위에서 함께 가져가는 핵심이 Delta Lake의 트랜잭션 로그와 메타데이터(ACID, 스키마 강제, Time Travel)이며, 이 덕분에 배치 실패 시 버전·커밋 단위로 상태를 추적할 수 있다고 설명합니다.
- 주목할 point: 운영 관점의 체크포인트로 테이블 변경 이력 확인, 배치 실패 시점 추적, 데이터 품질·스키마 변경 사전 감지를 꼽고, Lakehouse를 써도 파티션·권한·비용·Job 모니터링 기준은 오히려 더 명확해야 한다고 강조합니다. 개념 정리 위주의 짧은 글로, 후속으로 Unity Catalog·Lakeflow·DLT를 다룰 예정입니다.
- keyword: #Databricks #Lakehouse #DeltaLake #데이터플랫폼 #TimeTravel #데이터거버넌스

## [하루 187건의 테스트 실패, 사람이 보는 건수는 10건 — LLM이 로그를 읽고 담당까지 정하는 파이프라인 구축기](https://techblog.samsung.com/blog/article/109)
- 회사: 삼성전자
- 본문 요약: (원문 사이트가 응답 오류(HTTP 520)를 반환해 원문 확인 불가 — velopers 요약 기반) TV 소프트웨어 자동 테스트에서 하루 187건씩 쌓이는 실패 로그를 LLM이 분석하는 파이프라인을 소개한 글입니다. 실제 이슈인지 선별하고 담당자 지정까지 자동화해 사람이 직접 검토하는 건수를 약 10건으로 줄였습니다.
- 주목할 point: 원문 확인 불가로 세부 구현(모델, 분류 기준, 정확도 등)은 확인하지 못했습니다. 제목 기준으로 일일 실패 187건 중 사람 검토를 10건 수준으로 줄였다는 점이 핵심 성과입니다.
- keyword: #LLM #테스트자동화 #로그분석 #트리아지 #파이프라인
