<!-- 이 파일은 posts/2026-11-16.md의 사본입니다. 자동 생성됨. -->
# 2026-11-16 기술 블로그 모음

## [AWS에서 Laya를 통한 Decision Model 학습 및 배포 환경 구성하기](https://aws.amazon.com/ko/blogs/tech/aws-laya/)
- 회사: AWS
- 본문 요약: 텍스트를 생성하지 않고 선택지별 확률을 돌려주는 Decision Model을 LLM 대신 판단 작업에 쓰는 구성 가이드입니다. Apache-2.0 오픈소스 Laya(mmBERT-base 인코더 약 3.2억 파라미터 + 결정 헤드, 입력 1,024토큰)를 SageMaker 자체 컨테이너로 추가 학습하고 실시간 엔드포인트로 배포해, 한국어 텍스트에 개인정보보호법상 개인정보가 있는지와 종류·등급을 판정하고 ALLOW/BLOCK/REVIEW 규칙으로 처리합니다. 제로샷 Laya는 거의 모든 문장을 개인정보로 판정해 쓸 수 없었고, 추가 학습 후에는 Jev(관리형 API)·Strands Decider·SGLang으로 띄운 LLM(Qwen3-235B 등)과 같은 문장으로 비교해 비슷한 수준의 오류를 보이면서 T4 1장(ml.g4dn.xlarge)에서 건당 35~39ms로 처리했습니다.
- 주목할 point: 처음 보는 398건에서 오류가 53건→5건으로 줄어든 것은 판단 기준과 합성 데이터를 두 차례 보강한 재학습 루프의 결과이며, 운영 전 실제 샘플 1~2천 건으로 재측정을 권합니다. 비용은 인스턴스 시간 고정(2대 월 약 1,323달러)이라 월 330만 건 아래에서는 LLM 호출이 더 싸다는 손익분기 계산, 1,024토큰을 넘어 잘린(truncated) 응답은 ALLOW로 쓰지 말라는 규칙, 소량 PII 필터는 Bedrock Guardrails가 낫다는 기준도 제시합니다.
- keyword: #DecisionModel #Laya #AmazonSageMaker #개인정보필터 #LLM대체 #재학습

## [노트북을 닫아도 개발은 계속된다: 자율 그래프 주도 개발](https://d2.naver.com/helloworld/5976687)
- 회사: 네이버
- 본문 요약: NAVER Engineering Day 10th 발표 공개글로, 사람의 직접 지시 없이 '그래프'가 프로젝트를 주도하는 Autonomous Graph-Driven Development를 소개합니다. 스펙 문서와 코드는 AI Agent 루프가 작성하고 결정론적 코드가 기계적으로 검사하며, 결함은 피드백 루프로 자동 수정합니다. 그래프는 Upstream(기획서 변경→요구사항), Spec-drive(스펙 확정), Dev(구현), Verify(E2E 테스트 검증), Audit(스펙 논리 결함 탐색) 노드와 진행 현황 대시보드로 구성됩니다.
- 주목할 point: "Don't call us, we'll call you" — 사람이 AI를 부르던 주도권을 뒤집어 AI가 필요할 때만 사람을 호출하는 구조입니다. 발표 목차 기준 백엔드 개발 공수 86% 절감, 사람+AI 합산 전체 비용 71% 절감, 프런티어 모델이 아니어도 루프는 충분하다는 토큰 비용 관점을 다루며, 루프 안정화와 애매한 기획 문장 같은 어려움도 함께 공유합니다. (원문은 영상 발표 소개글로, 세부 내용은 영상에 있습니다.)
- keyword: #AIAgent #자율개발 #그래프주도개발 #E2E테스트 #HumanInTheLoop

## [Image AI 서빙 최적화: CPU와 GPU의 빈 시간을 줄여 H100 67장을 절감하기까지](https://d2.naver.com/helloworld/9994827)
- 회사: 네이버
- 본문 요약: NAVER Engineering Day 10th 발표 공개글로, SNOW의 16개 Image AI 서비스에서 응답 속도와 안정성을 높이면서 H100 환산 약 67장(67.37장)의 GPU를 절감한 경험을 다룹니다. LitServe로 전환해 반복되는 이미지 인코딩·디코딩을 없애고 CPU 전처리와 GPU 계산의 대기 시간을 줄였으며, 워커·스레드 수, CPU 한도와 코어 고정, Autoscaling 로직을 실제 트래픽에 맞춰 조정했습니다.
- 주목할 point: 가벼운 작업을 CPU로 분리하고 여러 서비스를 하나의 GPU에 함께 배치하는 GPU 공유, 에이전트 실험·검토를 통한 반복 최적화가 핵심입니다. 응답 속도·처리량·첫 요청 예열·오류율·취소율·GPU 활용도 개선을 함께 다루고, 향후 과제로 Image Harness와 트래픽 기반 자동 최적화를 제시합니다. (원문은 영상 발표 소개글입니다.)
- keyword: #LitServe #GPU최적화 #모델서빙 #ImageAI #오토스케일링

## [TV 앱 실행 시간 측정 자동화 개발기](https://techblog.samsung.com/blog/article/108)
- 회사: 삼성전자
- 본문 요약: TV 앱 실행 시간은 실물 TV에 리모컨 신호를 보내고 화면을 지켜봐야 잴 수 있어 그동안 사람이 TV 앞에서 직접 측정해 왔습니다. 이를 PC, USB IR 송신기, 웹캠만으로 자동화하는 도구를 Claude Code와 함께 7주 만에 만들어 측정자가 TV 앞을 지키는 시간을 95% 줄였다고 합니다.
- 주목할 point: 결과 판정에 일부러 LLM을 쓰지 않은 이유와, 여러 세션에 걸친 AI 협업 개발에서 맥락을 유지한 방법을 공유합니다. (원문 페이지가 520 오류로 열리지 않아 공식 RSS 요약과 velopers 요약을 바탕으로 작성했으며, 본문 직접 확인은 하지 못했습니다.)
- keyword: #테스트자동화 #TV앱 #IR송신기 #ClaudeCode #성능측정

## [카페 관리도구 개편기: 문서는 낡았고, 사람은 떠났고, 코드만 남았다.](https://d2.naver.com/helloworld/4049909)
- 회사: 네이버
- 본문 요약: NAVER Engineering Day 10th 발표 공개글로, 코드만 남아 있던 14년 된 카페 관리도구를 AI와 함께 분석하고 Storybook과 MSW로 화면과 동작을 재현하며 새로운 카페 스튜디오를 개발한 과정을 다룹니다. 구 관리도구 분석, 신규 스튜디오 개발, 일하는 방식 순으로 구성됩니다.
- 주목할 point: 문서와 담당자가 사라진 레거시를 코드 기반으로 복원·재현하는 접근과, 이 과정에서 기획·디자인·백엔드와의 협업 방식이 어떻게 달라졌는지가 핵심입니다. 레거시 개편을 준비하는 개발자나 화면·정책을 함께 검증하려는 기획자·디자이너를 대상으로 합니다. (원문은 영상 발표 소개글입니다.)
- keyword: #레거시개편 #Storybook #MSW #AI코드분석 #프론트엔드

## [흩어진 행동을 연결하다: 네이버 전 지면의 사용자 행동을 학습하는 추천 모델 개발기](https://d2.naver.com/helloworld/1599966)
- 회사: 네이버
- 본문 요약: NAVER Engineering Day 10th 발표 공개글로, 검색·피드·광고 등 여러 도메인의 데이터와 추천 기술을 연결하는 버티컬 추천 모델(VMs)의 개발 및 서비스 적용 경험을 소개합니다. 시스템 구조, 리트리버와 통합 랭커, 지면별 적용 현황과 성과를 다룹니다.
- 주목할 point: 대규모 추천 모델의 실시간 추론·GPU 서빙 최적화와, Foundation Model의 지식을 경량 모델로 옮기는 지식 증류(Knowledge Distillation) 기반 도메인 간 지식 전이 방향을 공유합니다. 크로스 도메인·시퀀스 기반·생성형 추천에 관심 있는 분들을 대상으로 합니다. (원문은 영상 발표 소개글입니다.)
- keyword: #추천시스템 #크로스도메인 #GPU서빙 #지식증류 #FoundationModel

## [코딩만 시키기엔 아까운 AI 활용기: Jira 일감부터 PR 검토까지](https://on.com2us.com/tech/ai-agent-developer-workflow-beyond-coding/)
- 회사: 게임빌컴투스플랫폼
- 본문 요약: 코드 작성 밖의 개발 업무에 AI를 연결한 경험담입니다. 직접 만든 로컬 웹 도구 jira-auto-agent는 Jira 일감을 고르면 설명·댓글·관련 코드로 작업 명세를 만들고, 빠진 조건은 구현 전에 확인한 뒤 Codex/Claude Code로 구현·테스트하고 변경 내용·실제 검사 결과·남은 확인 사항·화면 전후 비교를 모아 초안 PR·MR과 Jenkins 테스트 배포까지 잇습니다(실무 10여 회 적용). 업무 문의에는 FocusDesk와 Aside(MCP로 로그인된 업무 화면을 읽는 통로)를 연결해 답변 후보·원문 근거·추가 확인 사항을 모으고(약 2주, 채팅 50건 이상 시험), 낯선 코드는 REA(Reverse Engineer Anything)로 궁금한 동작 하나부터 추적합니다.
- 주목할 point: 실패 사례를 솔직하게 기록한 점이 유용합니다. 잘린 맥락 때문에 코드를 전혀 못 고친 경우, 'Git 변경 내역 미확인' 보고가 '코딩 규칙 위반'으로 잘못 표시돼 검증이 멈춘 경우, '일부라도 미확인이면 보류' 지시 때문에 확인된 답까지 막힌 경우, 같은 대화방 최신 메시지만 처리해 질문이 누락된 경우 등입니다. AI 완료 설명과 실제 테스트 결과를 따로 기록하고, '권한이 없어 못 읽음'과 '읽었지만 내용 없음'을 구분하라는 교훈을 남깁니다.
- keyword: #AI에이전트 #Jira자동화 #ClaudeCode #Codex #MCP #개발생산성

## [AI의 답에 동료 AI가 질문을 던졌다― weave-agents로 엮은 멀티 벤더 AI 협업](https://techblog.samsung.com/blog/article/107)
- 회사: 삼성전자
- 본문 요약: 서로 다른 벤더의 AI에 구현과 검토를 나누어 맡기고, 의견이 갈리면 코드와 테스트로 확인하는 weave-agents를 만든 이야기입니다. 기존 협업 아이디어를 바탕으로 모델의 남은 사용량과 역할별 평가를 고려해 담당 모델을 고르도록 설계했습니다.
- 주목할 point: 다른 벤더 AI의 추가 검토로 검사 누락을 메우고 잘못된 오류 지적을 걸러낸 실제 사례를 소개합니다. (원문 페이지가 520 오류로 열리지 않아 공식 RSS 요약과 velopers 요약을 바탕으로 작성했으며, 본문 직접 확인은 하지 못했습니다.)
- keyword: #weave-agents #멀티에이전트 #멀티벤더AI #코드리뷰 #테스트

## [베지어 다시 짓기 (1) : 사람과 AI를 위한 디자인 시스템](https://tech.channel.io/kr/articles/8029b017)
- 회사: 채널톡
- 본문 요약: 채널팀 디자인 시스템 '베지어(Bezier)' 리디자인의 원칙과 정책을 정리한 1편입니다. 언제 어떤 컴포넌트를 써야 하는지 불명확하고, 디자이너가 피그마 컴포넌트를 자주 detach해 AI가 디자인 소스를 읽는 비용도 컸던 문제에서 출발해, 'Readable by Humans, Runnable by AI', 'Extensible for Every Need', 'Clear by Default' 세 원칙을 디자이너·웹·iOS·안드로이드 개발자가 함께 확정했습니다.
- 주목할 point: 모든 컴포넌트에 사용 목적·베리언트 선택·금지 기준을 담은 기준 문서(spec.md)를 두고 피그마 컴포넌트 설정에 깃헙 링크를 연결했습니다. 피그마 슬롯은 '스펙은 자유롭게, 정책은 엄격하게' 원칙으로, 구현은 자유 영역으로 두되 BaseItem.md 같은 공통 규격 문서와 부모별 전용 자식 컴포넌트로 통제해 detach와 파일 무게, figma-to-code 비효율을 줄였습니다.
- keyword: #디자인시스템 #Figma #슬롯 #컴포넌트가이드 #AI네이티브

## [베지어 다시 짓기 (2) : 클로드 코드로 컴포넌트 만들기](https://tech.channel.io/kr/articles/92cd237e)
- 회사: 채널톡
- 본문 요약: 디자이너 한 명이 Claude Code와 63일 동안 웹 컴포넌트 38종, 모바일 컴포넌트 32종을 만든 과정입니다(3~4개 병렬 세션, 3개월간 총 754개 세션). 리디자인 병행으로 SSOT 경로가 뒤섞이고, 세션 간 기억이 공유되지 않아 이전 결정을 뒤집거나 같은 실수를 되풀이하는 문제가 있었습니다.
- 주목할 point: 결정 이력(decision-log.md), 피그마 Plugin API 우회 노하우 60여 개(plugin-api-workaround.md), 컴포넌트 세트 삭제를 막는 훅(figma-safety-gate.sh), Spec.md와 피그마 값을 대조하는 검수 에이전트(bezier-figma-auditor)를 갖추자 한 번 교정한 문제가 재발하는 세션이 100번당 약 27번에서 1번 수준으로 줄었습니다. 다시 한다면 문서·맥락부터 채우고, AI가 잘 못 알아들을 땐 직접 샘플을 만들어 보여 주겠다는 회고도 담겼습니다.
- keyword: #ClaudeCode #Figma #디자인시스템 #FigmaMCP #AI협업 #훅

## [누구나 디자인할 수 있는 환경 만들기](https://tech.remember.co.kr/%EB%88%84%EA%B5%AC%EB%82%98-%EB%94%94%EC%9E%90%EC%9D%B8%ED%95%A0-%EC%88%98-%EC%9E%88%EB%8A%94-%ED%99%98%EA%B2%BD-%EB%A7%8C%EB%93%A4%EA%B8%B0-ea8d232614f9)
- 회사: 리멤버
- 본문 요약: 리멤버 채용솔루션 디자이너가 Figma 대신 실제 제품 코드 위에서 Claude로 디자인하고 결과를 PR로 개발에 넘기는 방식으로 바꾼 이야기입니다. 최신 화면을 찾아 맞추는 비용, 정적 화면의 맥락 전달 한계, Figma Make가 매번 화면을 새로 그리고 디자인 시스템을 반영하기 어려운 문제의 근본 원인을 '분산된 작업 환경'으로 보고, 로컬 서버 위 실제 코드로 통합했습니다.
- 주목할 point: 프로토타입 스킬, UX 원칙·페르소나·문구 규칙·서비스 정책서·디자인 시스템을 담아 자동 발동되는 design guide 스킬, "PR 올려줘" 한마디로 화면 코드와 가짜 데이터를 커밋 분리해 디자인 브랜치에 PR을 올리고 QA 배포 확인·정책 문서까지 만드는 스킬을 팀 플러그인으로 배포했습니다. PM이 직접 시안 PR을 만들고 디자이너는 초안 검수 한 번만 개입한 사례를 공유합니다. (Medium 원문 페이지는 403으로 막혀 같은 글의 공식 RSS 전문으로 확인했습니다.)
- keyword: #Claude #프로토타입 #디자인핸드오프 #ClaudeSkills #팀플러그인

## [카페 아르바이트를 뽑는데, AI 대학원생이 지원을 했다.](https://blog.cslee.co.kr/a-graduate-ai-applied-for-a-cafe-part-time-job/)
- 회사: CSLEE
- 본문 요약: 카페 주문을 도구 호출로 바꾸는 작업에 MoE 모델 Gemma 4 26B(층당 전문가 128명 중 8명 활성)에서 카페 일에 덜 쓰이는 전문가를 가지치기해 노트북(32GB, 인텔 내장 GPU)에 올린 실험입니다. 카페 주문 600문장으로 전문가 기여도를 매겨 층당 98/64/48명만 남겼고, 전문가 절반을 지운 64e(11GB)는 일반 지식이 72.7%→47.3%로 떨어졌지만 카페 시험 93.3%, 사람이 쓴 실전 시험 70%(원본 75%)를 유지했습니다. 같은 내장 GPU에서 12B보다 빠르고(응답 중앙값 2.55초 vs 3.33초) 실전 점수도 높았습니다.
- 주목할 point: 논문의 REAP 점수를 그대로 쓰면 빈도를 보지 않아 토큰의 32~70%를 처리하는 '바쁜 전문가'가 해고될 뻔해, 전체 토큰 합 기준과 30% 이상 처리 전문가 보존 규칙으로 바꿨습니다. 48e는 AI가 만든 시험에선 93.3%였지만 사람이 쓴 실전 20문항에서 50%로 무너져, 가지치기 평가에는 사람이 쓴 데이터가 꼭 필요하다는 교훈을 줍니다. 속도를 가장 크게 바꾼 건 모델이 아니라 프롬프트 순서(매번 바뀌는 주문 내역 위치)였다는 점도 흥미롭습니다. 실전 시험이 20문항뿐이라 통계적으로 유의하지 않다는 한계를 스스로 밝힙니다.
- keyword: #LLM #MoE #ExpertPruning #Gemma4 #온디바이스AI #REAP

## [OA-RAG: 온톨로지 reasoner를 도구로 쓰는 Agentic RAG](https://blog.cslee.co.kr/oa-rag-ontology-based-agentic-rag-paper-review/)
- 회사: CSLEE
- 본문 요약: 맨체스터 대학교·SNOMED International의 논문 「OA-RAG」 리뷰입니다. 지식원을 문서에서 OWL 온톨로지로 바꾸고, axiom 기반 논리 추론은 reasoner에, annotation의 자연어는 LLM에 맡기는 ReAct agent(pre-tool reasoning → SPARQL DESCRIBE/ASK/SELECT 최대 10회 → answering) 구조입니다. 온톨로지에서 만든 문제(Test 1·2)에서는 가장 강한 baseline보다 평균 10~15%p 높았고, 의료 QA(Test 3)에서는 Qwen 기준 262k context i-MedRAG와 정확도가 비슷하면서(84.9% vs 85.2%) 문항당 token은 약 1/10(9.7k vs 96.7k)만 썼습니다.
- 주목할 point: 리뷰어는 Test 1·2 정답이 OA-RAG가 조회하는 바로 그 온톨로지로 정해졌고, Test 3에서는 tool 단계를 모두 빼도 정확도가 1%p도 안 떨어진다는 점(정확도 대부분이 모델 자체 지식)을 짚습니다. LLM이 스스로 매긴 grounding level은 Llama에서 정답·오답을 거의 가르지 못해, 등급은 tool 결과를 보고 규칙으로 정하자고 제안합니다. 사내 코드 체계·제품 분류처럼 관계가 분명한 데이터를 임베딩 대신 조회·검증 API tool로 여는 방식은 옮겨 올 만하다고 봅니다.
- keyword: #RAG #AgenticRAG #온톨로지 #OWL #SPARQL #논문리뷰

## [[Arm Create 2026] Arm AI Model Optimizer 핸즈온 현장 스케치](https://blog.nota.ai/kr/insights/arm-create-2026-model-optimization)
- 회사: 노타
- 본문 요약: PyTorch Conference 주간 산호세에서 열린 Arm Create 2026에서 Arm과 노타가 진행한 90분 핸즈온 후기입니다. Arm AI Model Optimizer는 노타 넷츠프레소(NetsPresso) 기반으로 그래프 최적화·양자화·혼합 정밀도를 적용하고 전후 성능·정확도·메모리를 비교하는 도구(얼리 액세스)입니다. 참가자들은 WideResNet-50을 Alif Ensemble E8(Cortex-M55 + Ethos-U85 NPU)용으로 CLI 10단계에 걸쳐 최적화해, 지연 시간 26.6% 단축(477→350ms, MLIA 추정)과 Top-1 정확도 0.5%p 차이를 확인하고 .pte 파일로 추출했습니다.
- 주목할 point: 설정 파일에서 가중치 granularity를 CHANNEL→TENSOR, 활성화 보정을 PERCENTILE→HISTOGRAM으로 두 곳만 바꿔 속도와 정확도를 함께 챙긴 점, ExecuTorch 내보내기·캘리브레이션·Vela 컴파일·평가를 따로 하던 과정을 명령어 몇 개로 줄인 점이 핵심입니다. 마지막에는 Qwen2.5-0.5B를 AWS Graviton4용으로 AWQ+최적화해 파일 크기 39% 감소, XNNPACK 위임 비율 38.0%→54.5%, 정확도 차이 0.2%p, 첫 토큰 1.8배·전체 응답 2.3배 빠른 데모 결과를 공개했습니다.
- keyword: #Arm #NetsPresso #모델최적화 #양자화 #ExecuTorch #엣지AI
