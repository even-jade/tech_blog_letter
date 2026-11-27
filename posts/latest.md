<!-- 이 파일은 posts/2026-11-27.md의 사본입니다. 자동 생성됨. -->
# 2026-11-27 기술 블로그 모음

## [AWS 멀티 계정·리전 네트워크 토폴로지 시각화하기](https://aws.amazon.com/ko/blogs/tech/visualize-multi-account-multi-region-network-topology-aws/)
- 회사: AWS
- 본문 요약: 여러 계정·리전에 흩어진 VPC, Transit Gateway, 피어링, VPN, Direct Connect 구성을 읽기 전용으로 수집해 HTML 파일 하나짜리 다이어그램으로 만드는 오픈 소스 샘플(sample-network-topology-visualizer)을 소개합니다. CloudFormation으로 설치하며, EventBridge 예약 규칙이 한 시간마다 CodeBuild를 실행해 Describe/Get/List/Search 계열 조회 API로 구성을 모으고 결과를 S3에 저장합니다. 별도 서버·DB나 외부 API, AI 에이전트는 쓰지 않습니다.
- 주목할 point: 계정 > 리전 > VPC > AZ > 서브넷 순으로 중첩 배치하고 30종 넘는 리소스를 다룹니다. 권한이 없어 조회에 실패한 곳은 "확인하지 못했습니다"로 표시해 리소스가 없는 곳과 구분하고, 스냅샷을 비교해 최근 7일 변경 이력을 보여 줍니다. SVG/PNG 내보내기로 감사 자료에 바로 쓸 수 있습니다. Network Manager나 CloudWatch Application Map과 달리 네트워크 계층 전체를 한 장에 담는 데 초점을 둡니다.
- keyword: #AWS #네트워크토폴로지 #TransitGateway #CloudFormation #CodeBuild #시각화

## [LINE Games의 AX 여정: 개발자를 위한 게임 퍼블리싱 에이전트](https://aws.amazon.com/ko/blogs/tech/linegames-ax-game-publishing-agent-for-developer/)
- 회사: AWS (LINE Games, GS Neotek 공동 작성)
- 본문 요약: LINE Games가 NTSDK·플랫폼 코드 변경 시 GitLab MR 코드 리뷰, MR 요약, API 문서 수정안 작성을 하나로 잇는 에이전트를 만든 사례입니다. 요청은 웹이나 GitLab 웹훅→SQS 워커로 들어오고, Bedrock AgentCore Runtime의 에이전트가 Bedrock 모델로 검토합니다. DynamoDB 코드 지식 베이스로 변경 코드의 사용처·연결 관계를 찾고, AgentCore Memory로 저장소별 설계 의도와 호환성 결정을 참고합니다.
- 주목할 point: 변경된 줄뿐 아니라 연결된 함수 구현·호출부까지 탐색하고, "코드 수정 필요"와 "추가 확인 필요"를 구분해 리뷰합니다. 문서 쪽은 기존 Nexus AI의 Bedrock Knowledge Bases로 관련 문서를 고르고 S3 보관본으로 본문·버전을 확인해 수정안을 검증합니다. 담당자가 승인한 수정이 다시 Nexus AI 지식 베이스로 돌아가 개발사 문의 응답 근거가 되는 순환 구조입니다.
- keyword: #AmazonBedrock #AgentCore #코드리뷰 #API문서 #GitLab #DynamoDB

## [LLM 서비스를 위한 AI 레드티밍](https://blog.cslee.co.kr/llm-ai-red-teaming/)
- 회사: CSLEE
- 본문 요약: 회의록 속 숨은 지시가 요약 결과를 바꾸는 예처럼, 정상 기능을 거쳐 들어오는 공격을 출시 전에 찾아내는 AI 레드티밍을 정리했습니다. 기존 보안 레드티밍과 달리 침투 없이 입력·참조 문서만 조작해도 공격이 성립하고, 응답이 비결정적이어서 같은 공격을 반복해 성공률로 측정해야 합니다. 검증 대상은 데이터, 모델, 외부 연계, 애플리케이션, 제어 체계, 인프라로 나눕니다.
- 주목할 point: 전문가 중심, 자동화(PyRIT, garak, promptfoo), Agentic 방식을 블랙·그레이·화이트박스 접근 수준과 조합하는 전략 선정 흐름도를 제시하고, 외부 업체(RTaaS)를 쓰더라도 내부 담당자가 업무 맥락을 전달하고 재검증에 참여해야 한다고 강조합니다. 범위 협의 → 평가지표·시나리오 설계 → 환경 준비 → 공격 수행·평가 → 개선·재검증 단계별 역할과 산출물도 정리했습니다. KISA 에이전트 보안수칙의 최소 권한, 사람 승인 원칙을 반영합니다.
- keyword: #AI레드티밍 #LLM보안 #프롬프트인젝션 #PyRIT #garak #promptfoo

## [데모는 완벽했는데, 왜 실제 서비스만 되면 흔들릴까?](https://blog.cslee.co.kr/llmops-core-elements/)
- 회사: CSLEE
- 본문 요약: LLM 서비스 운영에 필요한 LLMOps의 7가지 핵심 요소(프롬프트 버전 관리, 모델 서빙·라우팅, 평가·품질 모니터링, 옵저버빌리티·트레이싱, 데이터 파이프라인(RAG), 안전성·거버넌스, 환각 탐지·완화)를 정리하고, "품질이 들쑥날쑥하다", "비용이 늘고 느리다" 같은 운영 문제별로 먼저 손볼 요소를 짝지었습니다. MLOps와의 차이는 관리 중심이 "모델"에서 "서비스 운영"으로 옮겨 가는 점으로 설명합니다.
- 주목할 point: Langfuse는 불변 버전과 production/staging 레이블로 배포·롤백하지만, SDK 캐시 기본 TTL이 60초라 즉시 반영은 아니라는 점을 짚었습니다. LiteLLM Router의 재시도(같은 모델 그룹), 폴백(다른 그룹, max_fallbacks 기본 5), 쿨다운(기본 5초)의 범위 차이를 설명하고, 라우팅 규칙을 바꿀 때도 promptfoo 회귀 테스트셋으로 품질을 확인하라고 권합니다.
- keyword: #LLMOps #프롬프트관리 #모델라우팅 #LLMasJudge #Langfuse #LiteLLM

## [vLLM 아키텍처 이해와 동시 추론량 극대화: 동작 원리와 12B 실측 튜닝](https://blog.cslee.co.kr/vllm-concurrent-inference-optimization-gemma4-12b/)
- 회사: CSLEE
- 본문 요약: vLLM 0.33 V1 엔진의 API 서버·엔진 코어·GPU 워커 구조, 연속 배칭, 청크 프리필, PagedAttention, 자동 접두사 캐시를 설명합니다. 공유 H200에서 61GiB만 할당받아 Gemma 4 12B 서빙을 실측했고, 동시 처리량은 KV 메모리, SLO, 프리필 연산량, max_num_seqs 중 가장 낮은 한계에서 멈춘다고 정리했습니다.
- 주목할 point: BF16 채팅 기준 최대 92건이 동시에 실행됐고 처리량은 초당 약 1,970토큰에서 포화됐습니다. FP8 가중치로 동시 실행 +32%, 처리량 +25%를 얻었고 GSM8K 차이는 1,319문항 중 최대 10문항이었습니다. 32K 공유 시스템 프롬프트는 접두사 캐시로 첫 토큰이 21.8초에서 1.4초로 줄었고, 스텝 예산을 8,192에서 2,048로 낮추면 긴 문서 프리필 중 채팅의 최대 멈춤이 0.64초에서 0.19초로 줄었습니다. 요청마다 바뀌는 값은 프롬프트 맨 뒤에 둬야 캐시가 깨지지 않습니다.
- keyword: #vLLM #LLM서빙 #KV캐시 #FP8 #PrefixCaching #Gemma4

## [Docker 컨테이너 기반 수집 워커 구축: 키워드 크롤러 구조 개선하기](https://blog.cslee.co.kr/building-docker-container-based-crawling-workers/)
- 회사: CSLEE
- 본문 요약: 포털마다 하나씩 만들어 크론탭으로 하루 한 번 돌리던 키워드 크롤러를, 포털별 어댑터를 둔 URL 발견 워커와 포털에 상관없이 같은 코드로 도는 본문 추출 워커로 나눴습니다. 두 워커를 Docker 컨테이너로 병렬 실행하는 구조입니다. 두 워커는 MariaDB의 t_crawl_url 테이블을 할 일 목록 삼아 서로 직접 호출하지 않고, 추출 결과는 개인정보를 마스킹해 Solr에 색인합니다.
- 주목할 point: discovered → extracting → stored/failed_transient/failed_permanent/dead 상태값만 보면 각 URL이 어느 단계인지 알 수 있습니다. 일시적 실패는 30초에서 시작해 최대 1시간까지 늘어나는 백오프로 자동 재시도하고, 5회를 넘기면 dead로 빼 운영자가 확인합니다. 덕분에 실패한 URL만 부분 재처리할 수 있게 됐습니다. 포털 API가 본문을 주지 않아 스크래핑을 택했고, 도메인별 요청 간격과 헤드리스 브라우저 처리도 다룹니다.
- keyword: #Docker #크롤링 #워커분리 #재시도정책 #Solr #MariaDB

## [AWS 기본 서비스를 데이터플랫폼 구조로 다시 묶어보기](https://blog.bespinglobal.com/post/reorganizing-core-aws-services-into-a-data-platform-architecture/)
- 회사: 베스핀글로벌
- 본문 요약: EC2, S3, RDS, VPC를 서비스별 정의로 외우는 대신, 데이터가 들어오고 저장·처리·조회되는 흐름 안에서 다시 묶어 본 글입니다. Region/AZ는 장애 범위를, VPC/Subnet은 접근 경로를 나누는 기준으로 보고, S3는 저장소이자 이벤트 시작점, EC2는 작업 실행 환경, RDS는 관리형 DB와 운영 책임 기준으로 해석합니다.
- 주목할 point: 장애가 나면 인스턴스, Subnet/AZ, Region, 네트워크 경로·권한 중 어느 범위인지부터 묻는 질문 목록을 제시합니다. EC2가 어느 Subnet에 있는지, S3 접근이 인터넷을 타는지 VPC Endpoint를 쓰는지, RDS가 Multi-AZ인지와 백업 정책은 어떤지 같은 운영 체크리스트도 담았습니다. 입문 수준의 AWS 지식을 실제 인프라 문서 독해로 잇는 관점이 실용적입니다.
- keyword: #AWS #데이터플랫폼 #VPC #S3 #RDS #장애분석

## [Claude Code를 처음 프로젝트에 적용하며 느낀 점](https://blog.bespinglobal.com/post/thoughts-from-first-applying-claude-code-to-a-project/)
- 회사: 베스핀글로벌
- 본문 요약: 데이터 엔지니어가 Claude Code를 처음 프로젝트에 적용하며 공식 문서(Overview, Quickstart, Best practices)를 기준으로 정리한 글입니다. Claude Code를 자동완성 도구나 챗봇이 아니라, 코드베이스를 읽고 파일을 수정하고 명령을 실행·검증하는 터미널 기반 agentic coding 도구로 이해해야 한다고 설명합니다.
- 주목할 point: 탐색 → 계획 → 수정 → 검증 흐름을 반복하고, 처음에는 작은 변경부터 맡기며 pytest 같은 검증 명령을 함께 주라고 권합니다. 운영 환경 접근이나 파괴적 작업은 바로 맡기지 말고 권한을 제한해야 한다는 점, 데이터 엔지니어 업무에 맞춘 사용 예시와 첫 적용 후 세운 기준을 정리했습니다.
- keyword: #ClaudeCode #AgenticCoding #AI코딩 #검증 #권한관리

## [[🎤인터뷰] 월 천만 명 방문 페이지, AI와 알잘딱하게 마이그레이션하기](https://techblog.woowahan.com/28589/)
- 회사: 우아한형제들
- 본문 요약: (원문 사이트가 접근을 거부(HTTP 403)해 원문 확인 불가 — velopers 요약 기반) AI 에이전트와 공통 스킬을 활용해 월 천만 명이 방문하는 7만 줄 규모 웹뷰 코드를 무중단 방식으로 마이그레이션한 경험을 인터뷰 형식으로 소개한 글입니다.
- 주목할 point: 자동 검증으로 잡지 못하는 부분은 사람의 정책 판단과 베타 테스트로 보완했다고 합니다. 세부 수치와 과정은 원문을 직접 확인하시길 권합니다.
- keyword: #마이그레이션 #AI에이전트 #웹뷰 #디자인시스템 #테스트

## [CSM(Customer Service Management)와 AI Agent의 활용 — 문서를 지식으로, 지식을 답변으로](https://tech.osci.kr/csm-ai-agent-knowledge-base/)
- 회사: 오픈소스컨설팅
- 본문 요약: 매뉴얼·정책 문서가 PDF·Excel·Word 첨부파일로 흩어져 있어 Rovo 같은 AI Agent가 답변 근거로 쓰기 어렵다는 문제에서 출발했습니다. Forge 커스텀 앱으로 Confluence에 올린 원본 파일을 본문으로 변환해 주제별 지식문서로 정리하고, CSM으로 들어온 문의는 Rovo Agent가 분류한 뒤 지식문서를 근거로 응답 초안을 만듭니다.
- 주목할 point: AI 도입의 병목은 모델이 아니라 AI가 읽을 수 없는 형태로 흩어진 사내 지식이라고 진단합니다. 원본은 첨부로 남기고 AI가 읽을 본문은 따로 만들며, 업로드 이후 지식 정리는 자동화하되 고객에게 나가는 최종 답은 상담원이 근거를 검토해 보내는 세 가지 원칙을 세웠습니다.
- keyword: #Atlassian #CSM #RovoAgent #Forge #Confluence #지식베이스

## [실행형 AI 피클(Pickle)은 어떻게 '대신 실행'하는가](https://blog.cslee.co.kr/ai-assistant-pickle-action-agent-review/)
- 회사: CSLEE
- 본문 요약: 브라우저를 직접 열어 로그인, 날짜 선택, 폼 제출까지 대신하는 실행형 AI 비서 피클의 공개 기술 문서를 바탕으로 보안·격리 구조를 분석하고, 4박 5일 삿포로 여행 준비로 실제 활용 범위를 시험한 글입니다. 피클은 모델 판단이 틀릴 수 있다는 전제에서 Virtual browser, File workspace, Sealed vault 세 공간을 분리합니다.
- 주목할 point: 자격 증명은 AWS Nitro Enclaves 기반 Sealed vault에서만 쓰여 모델이나 서버 운영자도 원문을 볼 수 없습니다. 원본 암호화 키는 사용자 기기(iCloud Keychain 등)에 두고 원격 증명(Remote Attestation)으로 신뢰할 수 있는 enclave에서만 토큰을 복호화해, 프롬프트 인젝션이 일어나도 피해 범위를 공간 안으로 묶습니다. 남은 보안·제도 과제도 함께 정리했습니다.
- keyword: #실행형AI #AI에이전트보안 #NitroEnclaves #프롬프트인젝션 #격리

## [롯데GRS의 캠페인 AI 에이전트 CamBot: Amazon Bedrock과 Strands Agents로 설계부터 운영, 모델 전환까지](https://aws.amazon.com/ko/blogs/tech/lotte-grs-cambot-campaign-ai-agent-bedrock-strands-agents/)
- 회사: AWS (롯데GRS 사례)
- 본문 요약: 가맹점주·점장이 캠페인 한 건을 만드는 데 1~4시간 걸리던 문제를 풀기 위해, 롯데GRS가 CRM 솔루션 STORE360에 대화형 멀티 에이전트 CamBot을 붙여 7월 1일 정식 오픈한 과정입니다. 7회 약 18시간의 Working Backwards 워크숍과 현장 인터뷰로 진짜 문제가 "UI 사용성"이 아니라 "기준 부재로 시작조차 못 하는 구조적 공백"임을 찾았고, 목표를 "5분 이내 캠페인 설계"로 정의했습니다.
- 주목할 point: Strands Agents 오케스트레이터가 전문 Sub-Agent를 부르는 구조입니다. Lambda Web Adapter 스트리밍, DynamoDB 대화 상태, Parameter Store 모델 ID 관리, Glue·Athena 일자 마트를 씁니다. 품목·혜택 금액은 모델이 지어내지 않고 조회한 후보에서 고르며, 쿠폰 시작일은 요일별 매출로 코드가 계산합니다. 디지털에 익숙하지 않은 중·장년층을 위한 UX Writing 원칙과 Sonnet 4에서 Sonnet 5로 모델을 전환한 과정도 다룹니다.
- keyword: #AmazonBedrock #StrandsAgents #멀티에이전트 #CRM #UXWriting #모델전환

## [LLM의 다음 변곡점: 루프 트랜스포머](https://tech.channel.io/kr/articles/978765a4)
- 회사: 채널톡
- 본문 요약: 일부 레이어를 같은 가중치로 여러 번 반복 통과시켜, 파라미터를 늘리지 않고 계산 깊이를 키우는 루프 트랜스포머(Looped Transformer)를 설명합니다. 모델을 Prelude(1회) – Recurrent(r회) – Coda(1회)로 나누고, 유효 깊이는 prelude + r × recurrent + coda 층 수로 정해집니다. RNN이 토큰 순서 방향으로 반복하는 것과 달리 한 토큰 안에서 깊이 방향으로 반복합니다.
- 주목할 point: 학습 때 반복 횟수를 무작위로 뽑는 가변 횟수 학습으로 추론 시 "얼마나 생각할지"를 난이도에 맞춰 조절할 수 있고, 반복에 따른 입력 망각·발산은 입력 재주입과 학습 안정화로 막습니다. 루프 구조 기반 Inkling-2-mini가 채널톡 사내 벤치마크에서 동급 최고 성능을 보이고 파라미터가 몇 배 큰 모델과 비슷한 결과를 냈다는 점이 계기였습니다.
- keyword: #LLM #루프트랜스포머 #LoopedTransformer #가중치공유 #추론효율

## [새로운 Amazon Bedrock AgentCore Runtime(플랫폼 버전 V2) 소개 – 스냅샷 기반 cold start와 탄력 메모리](https://aws.amazon.com/ko/blogs/tech/agentcore-runtime-v2/)
- 회사: AWS
- 본문 요약: AgentCore Runtime V2는 런타임 생성 시 헬스 체크가 통과한 실행 환경 전체를 스냅샷으로 만들고, 새 세션마다 이를 복원해 이미지 크기·동시성과 무관하게 cold start를 일정하게 유지합니다. 쓰지 않는 메모리는 120초 뒤 회수해 과금에서 빼는 탄력 메모리도 도입했습니다. 같은 에이전트를 서울 리전 V1·V2에 나란히 배포해 측정했으며, 11월 12일부터 서울 포함 19개 리전에서 신규 런타임 기본값이 V2입니다.
- 주목할 point: 서울 리전에서 2GB 이미지 cold start가 27.51초에서 1.81초(p75)로 줄었고 세션 50개 동시 유입에도 같았습니다. 해제한 메모리 1.5GB 중 과금에 남은 양은 0.08GB였습니다. vCPU 단가는 42.6%, 메모리 단가는 78.8% 올랐지만 2GB 이미지의 총비용은 약 9.8배 낮아졌습니다. 최적화 대상이 이미지 크기·엔드포인트 수에서 "시작 시 무엇을 미리 준비할지"로 옮겨 가며, 배포 시간 증가와 스냅샷 안전성 점검은 따로 챙겨야 합니다.
- keyword: #AmazonBedrock #AgentCore #ColdStart #스냅샷 #탄력메모리 #서버리스

## [Amazon Bedrock과 AWS Device Farm을 활용한 자연어 테스트케이스 자동 실행 시스템 구축 과정](https://aws.amazon.com/ko/blogs/tech/automating-natural-language-test-cases-amazon-bedrock-aws-device-farm/)
- 회사: AWS (우아한형제들)
- 본문 요약: 우아한형제들이 자연어로 쓴 테스트케이스를 AI 에이전트가 웹·실기기 앱·API에서 자동 실행하는 시스템을 만든 과정입니다. FastAPI 백엔드가 Strands Agents의 BedrockModel로 Claude를 호출하고, 웹은 playwright-mcp, 앱은 Device Farm 원격 접속 세션의 관리형 Appium에 연결한 devicefarm-mcp, API는 전용 도구로 조작합니다. 결과 JSON은 S3와 Bedrock Knowledge Bases로 이어져 다음 실행의 RAG 근거가 됩니다.
- 주목할 point: 앱 사전 설치·자동 온보딩·다중 세션 병렬화로 온보딩이 120초에서 36초로 줄었습니다. 페이지 소스 87% 압축, 대기 시간 완화, 도구 융합, 프롬프트 캐싱 같은 실측 기반 튜닝으로 대표 케이스 실행 시간을 웹 795초→약 255초, 앱 482초→약 270초로 단축했습니다. 타깃별 워커 큐, 전역 세마포어(동시 10개), 시작 시차(1,500ms)로 부하를 분산하고, 과거 실패 행동은 벡터 검색으로 피합니다.
- keyword: #AmazonBedrock #AWSDeviceFarm #테스트자동화 #MCP #StrandsAgents #QA

## [미국 패서디나점 오픈런 고객의 첫 결제부터 막힘없도록, 글로벌 오프라인 시스템 개발자의 과제와 설계 결정](https://oliveyoung.tech/2026-11-27/global-offline-system-open/)
- 회사: 올리브영
- 본문 요약: 2026년 5월 미국 첫 오프라인 매장(패서디나점) 시스템을 6개월 안에 처음부터 만든 기록입니다. 상품 등록부터 POS·ESL·POG·결제·재고·정산까지 E2E 데이터 흐름, 매장 위치와 상품마다 다른 미국 판매세, 직접 개발 POS 대신 현지 SaaS POS 도입, 매장과 다른 시간대에서 운영해야 하는 문제를 풀어야 했습니다.
- 주목할 point: 흐름을 구간으로 나눠 다음 구간으로 값이 그대로 넘어갔는지 확인하도록 설계하고, 이를 위해 Aggregation Service를 새로 만들었습니다. 기준 시간은 매장 현지 시간(PST/PDT)으로 통일했습니다. 확정된 약 4,000개 상품을 참고 데이터로 근거와 함께 Tax Code를 추천하는 AI는 확신이 없으면 추천하지 않도록 했고, 상용 솔루션 대신 직접 만든 이유(분류 자산화, 표준 카테고리 유지, SKU 비례 비용)도 설명합니다.
- keyword: #글로벌커머스 #POS #판매세 #SaaS #데이터정합성 #TaxCodeAI

## [공격이 4배 늘어도 버티는 서비스 만들기](https://tech.imweb.me/posts/infra-security-ai-response/)
- 회사: 아임웹
- 본문 요약: 웹 방화벽이 막은 공격이 1년 새 하루 평균 약 4.3배가 됐지만, 서비스 정상 처리 비율은 99.971%에서 99.9985%로 올라간 보안 대응 사례입니다. "조사와 초안은 AI, 판단·변경·발송은 사람" 원칙으로 자동 차단, 탐지와 경보(P1~P4, 보안 봇 4단계 판정), 취약점 조치 등을 정리했고, 인프라 엔지니어뿐 아니라 개발자도 보안 대응에 직접 참여합니다.
- 주목할 point: DDoS v2는 오리진까지 들어온 요청을 세다가 이상 IP를 0.6초 만에 웹 방화벽 차단 명단에 올립니다. 초당 약 8만 건, 약 123만 건이 몰린 공격에도 웹 서버 대기 줄이 쌓이지 않았습니다. PHP 최상급 취약점은 공개 1시간 만에 완화 설정, 2시간 30분 만에 직접 만든 패치로 운영 웹 서버를 교체했습니다. Java 취약점 때 보안 봇이 "영향 없음" 승인 카드를 만들었지만 사람이 걸러내 승인하지 않은 사례도 공유합니다.
- keyword: #DDoS #웹방화벽 #취약점대응 #보안자동화 #AI운영 #PHP
