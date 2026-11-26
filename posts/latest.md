<!-- 이 파일은 posts/2026-11-26.md의 사본입니다. 자동 생성됨. -->
# 2026-11-26 기술 블로그 모음

## [Agentic AI, 멀티 에이전트로 신뢰와 비용 효율을 설계하다](https://tech.kakaopay.com/post/multi-agent-ai-code-reviewer-jorgit/)
- 회사: 카카오페이
- 본문 요약: 카카오페이손해보험 전사 개발자가 쓰는 AI 코드 리뷰어 jorgit의 설계 회고입니다. PR 자동 리뷰(CRITICAL/MAJOR/MINOR), 코멘트 질의응답, 재리뷰, 자동 승인, 제3자 합의(슬랙 알림) 기능을 제공하며, 오탐·환각을 줄이려고 Analyst(분석)와 Verifier(검증) 에이전트가 반박이 없을 때까지 상호 검증해 confidence 80 이상인 이슈만 게시하는 구조로 바꿨습니다. 기본 리뷰·컨벤션 검토 팀이 병렬로 돌고 Leader가 결과를 통합합니다.
- 주목할 point: Pre Checker와 읽기 계층(PR Content Reader, Custom Rule Loader)이 변경 파일·메타데이터·컨벤션을 미리 읽어 커밋 단위로 캐싱·주입하고(순차 조회 대비 누적 입력 토큰 20개 파일 기준 약 11.9배 차이), Leader는 저가 모델·최소 도구, Verifier는 고성능 모델·tool call 횟수 제한으로 모델 티어링을 적용해 PR당 평균 토큰 비용을 약 60% 줄였습니다. 하루 리뷰 PR 수는 6월 대비 약 6배, 10월 리뷰의 41.8%가 자동 승인으로 마무리됐습니다.
- keyword: #AgenticAI #멀티에이전트 #코드리뷰 #모델티어링 #비용최적화

## [웅진씽크빅의 AI-Ready Data 기반 콘텐츠 추천 에이전트 구축기 Part 2 – Amazon Bedrock AgentCore로 그래프 에이전트 만들기](https://aws.amazon.com/ko/blogs/tech/woongjin-ai-ready-data-graph-agent-part-2/)
- 회사: AWS
- 본문 요약: 스마트올 학습 데이터를 연결한 Neptune 지식그래프를 기획자·교사가 자연어로 탐색하도록 Strands Agents 기반 그래프 에이전트를 만든 과정입니다. 요약·개수를 먼저 주고 ID로 깊이 들어가는 Progressive Disclosure 방식의 도구 6개(lookup_topic, navigate, get_prerequisites, run_readonly_cypher 등)와 쓰기 절 차단·행 수 상한 가드를 두고, 6개 역할 56건 골든셋(개발 29/홀드아웃 27)을 Strands Evals의 여러 평가자로 채점하며 반복 개선했습니다. 이후 EKS 직접 서빙에서 AgentCore Runtime·Gateway·Identity·Memory로 옮기고 CloudWatch Omni로 관측성을 구성했습니다.
- 주목할 point: 비용 추적용 추론 프로파일 ARN에는 모델 이름이 없어 Strands의 Claude 자동 캐싱이 꺼져 있던 문제를 찾아 캐싱 전략을 직접 지정한 결과, 케이스당 비캐시 입력 토큰이 59,366개에서 8개로 줄고 입력 토큰 실효 비용이 약 70% 낮아졌습니다. 저장된 안내 속성 질문은 규칙으로 판별해 LLM 없이 바로 답하는 직답 경로도 효과가 컸습니다.
- keyword: #AmazonBedrockAgentCore #AmazonNeptune #StrandsAgents #그래프에이전트 #프롬프트캐싱

## [웅진씽크빅의 AI-Ready Data 기반 콘텐츠 추천 에이전트 구축기 Part 1 – Amazon Neptune으로 콘텐츠용 시맨틱 레이어 만들기](https://aws.amazon.com/ko/blogs/tech/woongjin-ai-ready-data-semantic-layer-part-1/)
- 회사: AWS
- 본문 요약: 약 500억 건 학습 데이터를 가진 웅진스마트올의 콘텐츠 메타데이터가 여러 RDB 테이블에 흩어져 선수학습·콘텐츠 간 연결 추천이 어려웠던 문제를, AWS AI Ready Data 프로그램으로 Neptune 지식그래프 시맨틱 레이어를 만들어 푼 과정입니다. "테이블은 마지막에 본다"는 원칙으로 서비스가 던질 질문(Competency Question)에서 출발해 사전 시뮬레이션과 Domain Storytelling 워크샵으로 스키마(엔티티 14개·관계 17개)를 그리고, 설계 워크샵에서 T-Box를 확정한 뒤 EMR·Airflow·Neptune 벌크 로더로 적재했습니다.
- 주목할 point: 사전 시뮬레이션에서 추천의 핵심인 선후관계(PREREQUISITE_OF)·연관관계(RELATED_TO) 데이터가 명시돼 있지 않음을 미리 발견해 보강했고, 최종 적재본은 노드 라벨 11종·관계 타입 11종입니다. 경로 탐색이 핵심이라 RDF 대신 속성 그래프와 openCypher를 1차 모델로 택했고, 적재 후에는 원천 파일과 개수를 대조해 누락을 검증했습니다.
- keyword: #AIReadyData #AmazonNeptune #지식그래프 #시맨틱레이어 #openCypher

## [Product Engineer 파일럿 회고: 7일 만에 만든 기능을 다섯 달 뒤에 내리기까지](https://techblog.yogiyo.co.kr/product-engineer-%ED%8C%8C%EC%9D%BC%EB%9F%BF-%ED%9A%8C%EA%B3%A0-7%EC%9D%BC-%EB%A7%8C%EC%97%90-%EB%A7%8C%EB%93%A0-%EA%B8%B0%EB%8A%A5%EC%9D%84-%EB%8B%A4%EC%84%AF-%EB%8B%AC-%EB%92%A4%EC%97%90-%EB%82%B4%EB%A6%AC%EA%B8%B0%EA%B9%8C%EC%A7%80-91a3af71a2a4)
- 회사: 요기요
- 본문 요약: 요기요 Checkout팀 백엔드 개발자가 Product Engineer 파일럿으로 12개 질문에 답하면 16가지 음식 유형과 추천 음식을 보여 주는 '오늘의 음식궁합'을 혼자 기획·출시한 회고입니다. AI 도구 덕에 처음 다룬 웹뷰로도 7일 만에 동작하는 버전을 만들었지만, 고정 영역으로 방향을 잡으며 서버·iOS·Android·로그까지 얽혀 전체 노출까지 39일이 걸렸고, 성공 지표와 중단 기준 없이 시작한 탓에 다섯 달 동안 약 2.3만 명이 열어봤어도 주문 증가 근거를 얻지 못해 10월 2일 직접 내렸습니다.
- 주목할 point: 추천 음식을 눌러 검색으로 간 사람의 31%가 1시간 안에 주문했지만 결과만 보고 나간 사람도 28%가 주문했고, 전체 노출이라 대조군이 없어 효과를 증명할 수 없었습니다. 7명이 8주 걸리던 일을 혼자 끝낸 장점은 컸지만 기다리는 시간이 만드는 시간의 4배를 넘었다며, "어떤 숫자가 움직이나"를 착수 전에 묻고 키울/내릴 기준을 먼저 적으며 대기 시간 자동화를 우선하라고 제안합니다.
- keyword: #ProductEngineer #제품실험 #성공지표 #대조군 #회고

## [Jetpack Compose 기반 커스텀 3D 캐러셀 개발기](https://d2.naver.com/helloworld/7426315)
- 회사: 네이버 D2
- 본문 요약: 네이버의 북미 SNS ThingsBook '모아보기' 화면의 카드형 3D 캐러셀을 LazyRow 없이 직접 만든 경험입니다. 카드마다 간격이 다르고(90dp/30dp) 넘기는 동안 간격이 옮겨 가며, 같은 드래그에도 카드별 이동 거리·기울기가 달라 LazyRow의 세 약속(배치·스크롤·보이는 것만 컴포즈)을 모두 어기기 때문에, Float 하나(ratio)가 화면 전체를 움직이고 각 카드는 그 값의 순수 함수가 되도록 설계했습니다.
- 주목할 point: 값을 그대로 넘기면 120Hz·카드 10장 기준 초당 1,200번 리컴포지션이 생겨 ratio를 람다로 넘겨 graphicsLayer 안에서만 읽게 했고, Compose 1.7.0에서 레이어 구현이 RenderNodeLayer→GraphicsLayerOwnerLayer로 바뀌며 cos θ로 나눠야 할 값을 곱해 3D 회전 카드의 터치 영역이 2배로 잡히는 버그를 찾아 컨테이너가 렌더와 같은 수식으로 직접 판정하게 했습니다. Paging 3는 get(뷰포트 안)·peek(밖)을 구분해 로드 신호를 직접 챙깁니다.
- keyword: #Android #JetpackCompose #3D캐러셀 #리컴포지션 #Paging3

## [실리콘투의 바이브코딩 에셋을 위한 AWS 기반 표준 배포 파이프라인 구축기](https://aws.amazon.com/ko/blogs/tech/silicon2-vibe-coding-assets-aws-deployment-pipeline/)
- 회사: AWS
- 본문 요약: 업무별 MCP 서버로 사내 데이터에 접근하게 되자 현업이 바이브코딩으로 대시보드('에셋')를 직접 만들기 시작한 실리콘투가, 이를 사내 서비스로 안전하게 공유하기 위해 만든 표준 배포 체계입니다. 에셋을 대시보드형(Type 1)과 서비스형(Type 2)으로 나눠 Type 1부터 표준화했고, 접수→분석·분류→정제·리뷰→배포→검증·운영 5단계와 현업·개발팀·인프라보안팀의 역할을 정했습니다. 인프라(CDK)·백엔드(Lambda 코드)·화면(정적 파일)을 독립 배포하는 GitHub Actions 워크플로를 OIDC 임시 자격 증명으로 구성했습니다.
- 주목할 point: 로컬 코딩 에이전트가 매번 MCP에서 전체 데이터를 가져와 토큰이 많이 들고 결과도 대화마다 달랐던 수집·정제를 Step Functions·EventBridge Scheduler 기반 공통 백엔드로 옮기고(대시보드별 호출 시각 20분씩 분산, 증분 수집+재조회 기간), 배포 역할 신뢰 정책에 저장소 이름뿐 아니라 고유 ID·main 브랜치까지 명시했습니다. 조회는 CloudFront + Lambda@Edge가 사내 통합 SSO(OIDC, MFA)의 ID 토큰을 검증하고 OAC로 비공개 S3에서 읽습니다.
- keyword: #바이브코딩 #MCP #GitHubActions #OIDC #LambdaEdge

## [AWS Physical AI Toolchain 소개](https://aws.amazon.com/ko/blogs/tech/introducing-aws-physical-ai-toolchain/)
- 회사: AWS
- 본문 요약: AWS Physical AI 블로그(2026년 10월 7일) 글의 번역으로, 로봇·자율주행 등 Physical AI 정책을 데이터 수집부터 합성 데이터 생성, 학습, 시뮬레이션 검증, 엣지 배포까지 AWS에서 실행하는 레퍼런스 아키텍처·IaC·배포 자동화 모음 'Physical AI Toolchain on AWS'를 소개합니다. 컴퓨팅 이질성, 아티팩트 난립, 검증 깊이, 데이터 경제성, 제어 경로 배치라는 다섯 문제 때문에 일반 ML-Ops와 다른 전용 툴체인이 필요하다고 설명하고, NVIDIA GR00T·Isaac Sim·Isaac Lab·Cosmos·OSMO를 S3·EKS·Batch·SageMaker·EC2·IoT Greengrass(Jetson 배포) 위에 묶었습니다.
- 주목할 point: 개발 주기를 선형 파이프라인이 아닌 플라이휠(배포 로봇의 엣지 케이스 → 시뮬레이션 시나리오 → 합성 데이터 → 학습 → 검증)로 보고, 각 구성요소를 독립 Terraform 모듈로 만들어 단계별로 채택할 수 있게 했습니다. Zarr→LeRobot, PyTorch·Hugging Face, Gymnasium, URDF, ONNX, ROS 2 같은 공개 표준을 쓰며, Strands Agents SDK 기반 에이전트 계층이 자연어 의도로 구성요소 호출·컴퓨팅 프로비저닝·데이터 인수인계를 조율합니다.
- keyword: #PhysicalAI #NVIDIAIsaac #GR00T #로보틱스 #StrandsAgents

## [AI에게 API를 그대로 열어 주지 마세요 — 원격 TV 팜을 AI 에이전트용 인터페이스로 다시 설계하며 얻은 6가지 원칙](https://techblog.samsung.com/blog/article/111)
- 회사: 삼성전자
- 본문 요약: 원격 TV 팜의 기기 관리 기능을 AI 에이전트가 쓸 수 있도록 MCP 서버와 OpenAPI로 다시 설계한 사례입니다. IDE의 AI 에이전트에게 자연어로 지시하면 원격 TV 팜에서 실기기를 찾아 할당받고, SDB 접속·전원 제어·반납까지 처리하도록 구성했으며, 그 과정에서 얻은 6가지 설계 원칙을 정리했습니다. (원문 사이트가 응답 오류(HTTP 520)로 열리지 않아 본문을 직접 확인하지 못했으며, velopers.kr 요약을 바탕으로 작성했습니다.)
- 주목할 point: 사람이 쓰던 API를 그대로 노출하는 대신 에이전트 작업 흐름(찾기→할당→접속→제어→반납)에 맞춘 인터페이스로 재설계했다는 점이 핵심입니다. 세부 원칙 6가지는 원문에서 확인이 필요합니다.
- keyword: #AI에이전트 #MCP #OpenAPI #SDB #TV팜

## [행사 순간을 함께 나누는 한마디, if(kakao)26 네트워킹 스크린 제작기](https://tech.kakao.com/posts/850)
- 회사: 카카오
- 본문 요약: if(kakao)26 참가자가 현장 QR로 접속해 짧은 메시지를 남기면 운영자 확인을 거쳐 행사장 스크린에 띄우는 '네트워킹 스크린'을 DevRel 담당자가 기획·화면 디자인·웹사이트 제작까지 맡아 만든 이야기입니다. 메시지 입력→색상·이름 선택→미리보기→전송으로 참여 흐름을 단순화했고, 전시 화면에서는 메시지가 독립적으로 움직이며 등장해 살아 있는 공간처럼 보이도록 했습니다.
- 주목할 point: 공개 화면인 만큼 자동 검사를 통과한 메시지를 운영자가 최종 승인해야만 노출되고, 메시지가 쌓이면 먼저 들어온 것부터 사라지도록 설계했습니다. 이틀간 총 103건(첫날 56건, 둘째 날 47건)이 남았으며, AI로 아이디어를 빠르게 구현하면서 구현보다 '어떤 경험을 만들지'에 더 집중하게 됐다고 회고합니다.
- keyword: #ifkakao #DevRel #네트워킹스크린 #참여경험 #콘텐츠모더레이션

## [데이터센터 보안 | ISMS 인증이 지키는 것과 인증 범위](https://library.gabia.com/contents/infrahosting/16186/)
- 회사: 가비아
- 본문 요약: 정보통신망법 제47조에 따라 집적정보통신시설 사업자에게 의무인 데이터센터 ISMS 인증이 무엇을 보호하고 어디까지 적용되는지 설명합니다. 인증서 유효기간은 3년이며 매년 사후심사를 받고, ISMS-P는 ISMS 기준에 개인정보 처리 심사를 더한 인증이라 ISMS 의무를 이행한 것으로 봅니다. 보호 대상은 시설·장비(보호구역 출입 통제, 온습도·화재·누수 감지, UPS·비상발전기), 계정·접속 경로, 장애·재해(복구 체계와 시험), 보안 사고(이상행위 모니터링, 연 1회 이상 대응 훈련)입니다.
- 주목할 point: 인증으로 관리 수준을 확인할 수 있는 곳은 인증서 범위 문구에 적힌 센터와 서비스뿐이고, 같은 사업자라도 범위 밖 센터는 인증서로 확인되지 않으며, 코로케이션 랙 안의 서버·계정·데이터는 이용 기업이 직접 관리해야 합니다. 계약 전 인증 범위와 고객 책임 영역을 확인하라는 실무 조언이 핵심입니다.
- keyword: #ISMS #ISMS-P #데이터센터 #코로케이션 #정보보호

## [[기술 소개] 서버의 열기를 밖으로 실어 나르는 최종 열 교환기, 냉각탑(Cooling Tower)](https://tech.ktcloud.com/entry/2026-11-ktcloud-data-center-cooling-tower-operation)
- 회사: KT 클라우드
- 본문 요약: 데이터센터 냉방에서 서버 열을 대기로 버리는 냉각탑의 종류와 원리를 소개합니다. 효율이 높고 초기 비용이 낮아 대형 데이터센터에 널리 쓰이지만 수질 관리가 필수인 개방형과, 코일 안 냉각수를 간접 냉각해 오염을 막는 밀폐형을 비교하고, 약 1%의 물이 증발하며 나머지 99%의 열을 빼앗는 증발 잠열 원리와 성능 지표인 Cooling Range·Cooling Approach(출구 수온과 습구 온도의 차이)를 설명합니다.
- 주목할 point: 옥상 구조 안전성·크레인 양중·배관 용접 등 시공 요소, 도심 민원을 줄이는 백연 저감형 냉각탑, 팬 모터 VFD 제어와 겨울철 냉동기를 멈추는 프리쿨링으로 전력을 아끼는 방법, 스케일·슬라임을 막기 위한 수질 검사와 블로우다운 같은 운용자 역할까지 현장 관점으로 정리했습니다.
- keyword: #데이터센터 #냉각탑 #프리쿨링 #VFD #수질관리

## [[인사이트] 엔비디아의 무료 LLM API 공개, 인프라 엔지니어 관점에서 바라본 NIM의 활용 가치](https://tech.ktcloud.com/entry/2026-11-ktcloud-nvidia-nim-llm-deployment)
- 회사: KT 클라우드
- 본문 요약: 엔비디아가 build.nvidia.com으로 주요 오픈소스 LLM 추론 API를 무료 공개한 배경을 NIM(NVIDIA Inference Microservices) 관점에서 분석합니다. NIM은 모델 가중치, 모델·GPU 조합에 따라 자동 선택되는 추론 엔진(TensorRT-LLM, vLLM, SGLang 등), OpenAI 호환 API 서버를 컨테이너 하나로 묶어 GPU 드라이버·CUDA·프레임워크 버전 정합성 문제를 없애 줍니다.
- 주목할 point: PoC는 엔비디아 퍼블릭 API로, 운영은 NGC에서 받은 NIM 컨테이너를 사내 프라이빗 인프라에 올려 엔드포인트만 바꾸면 되는 전환 흐름이 장점입니다. 반면 NVIDIA 하드웨어·CUDA 생태계 종속이 커지고, 개발·테스트용은 최대 16 GPU까지 무료지만 프로덕션에는 GPU당 연 약 $4,500의 NVAIE 라이선스가 필요하다는 점을 함께 짚었습니다.
- keyword: #NVIDIANIM #LLM #모델서빙 #AI인프라 #VendorLockin

## [[인사이트] AI가 작업복을 입었다: 1.4조 원 피지컬AI 프로젝트와 클라우드 인프라](https://tech.ktcloud.com/entry/2026-11-ktcloud-physical-ai-manufacturing-cloud-infrastructure)
- 회사: KT 클라우드
- 본문 요약: 2026~2030년 총 1조 4,131억 원(전북 7,368억·경남 6,763억) 규모, 150여 기관·연구진 약 3,500명이 참여하는 피지컬AI 연구개발사업을 클라우드·인프라 관점에서 정리했습니다. 전북은 AI 공장 설계·3D 디지털트윈 사전 검증·VLM 상황 인식·강화학습 통합 제어로 이기종 설비를 묶는 '공장 오케스트레이션' 플랫폼을, 경남은 작업자·로봇 행동 데이터와 물리법칙·공간정보를 학습하는 제조 특화 거대행동모델(LAM)을 맡습니다.
- 주목할 point: 2030년 목표 중 '현장 결과의 재학습 반영 24시간 이내'는 데이터 수집·정제·재학습·검증·재배포 전체를 하루에 끝내야 하는 인프라 과제라고 짚고, Real→Sim→Real 순환 루프와 KT의 조선소 용접로봇 실증(5G SA, 네트워크 슬라이싱, AI-RAN), 미국(Omniverse)·중국(구현지능 정책)의 동향을 비교합니다. 참여 기관의 약 68%가 중소·중견기업이라는 점도 눈에 띕니다.
- keyword: #피지컬AI #거대행동모델 #디지털트윈 #공장오케스트레이션 #엣지클라우드

## [LLM 최적화의 핵심 KV cache 기술](https://blog.cslee.co.kr/llm-optimization-kv-cache-and-prefix-caching/)
- 회사: CSLEE
- 본문 요약: LLM 추론을 연산이 병목인 프리필(compute-bound, TTFT)과 메모리 대역폭이 병목인 디코딩(memory-bound, TPOT)으로 나눠 설명하고, KV cache가 계산 병목을 메모리 병목으로 옮긴다는 점(Llama-3-8B FP16 기준 토큰당 약 128KB, 8K 대화 하나에 약 1GB)과 FlashAttention·PagedAttention·prefix caching의 역할을 정리합니다. 이어 정해진 선택지와 확률만 돌려주는 'System-1' 결정 모델(Jev, Kev)이 LM head만 바뀌고 디코딩 루프가 없을 뿐 백본은 일반 트랜스포머와 같다고 해부합니다.
- 주목할 point: L40S 1장에서 Kev-4B와 Qwen3.5-4B-Base(1토큰 출력)를 실측한 결과, 8K·동시 1에서 캐시 off는 516ms/485ms로 거의 같고 prefix caching을 켜면 89ms/95ms로 둘 다 5배 이상 빨라졌습니다. '수백 배 빠르다'는 수치는 큰 모델·긴 출력과의 비교일 뿐이며, prefix caching은 서버 설정이 아니라 고정 부분을 앞에 두는 프롬프트 설계의 문제라는 결론입니다(단, vLLM이 528토큰 블록 단위로 재사용해 512토큰 prefix는 캐시 효과가 없었음).
- keyword: #LLM #KVcache #PrefixCaching #vLLM #System1모델

## [Hybrid RAG는 어떻게 검색 정확도를 높일까?](https://blog.cslee.co.kr/hybrid-rag-search-optimization/)
- 회사: CSLEE
- 본문 요약: 공공AX 프로젝트인 조세심판원 AI 검색 서비스의 Hybrid RAG 검색 구조를 설명합니다. 단어는 달라도 쟁점이 같은 문서를 찾는 Dense Search와 법률 용어가 일치하는 문서를 찾는 BM25를 Qdrant에서 함께 돌리고, 점수 체계가 달라 원점수 대신 순위 기반 RRF로 결합한 뒤, LLM이 질문과 후보 요약을 비교해 실제 쟁점에 가까운 문서를 재랭킹합니다.
- 주목할 point: "2021년 이후 부가가치세 심판례"처럼 질문에서 핵심 쟁점(검색 대상)과 문서 유형·세목·기간(필터 조건)을 분리해 사전 필터링해야 '2021년'이라는 단어만 들어간 문서가 올라오는 문제를 막을 수 있다고 강조합니다. 품질은 Recall@K(누락)과 nDCG@K(순위)로 단계별로 비교하고, 후보 수·재랭킹 대상 수·응답 시간의 균형도 함께 측정해야 한다고 정리합니다.
- keyword: #HybridRAG #BM25 #RRF #Qdrant #재랭킹

## [Cline을 이용한 AI Agent 개발워크플로우의 신뢰성을 위한 설계](https://blog.cslee.co.kr/designing-reliable-ai-agent-development-workflows-with-cline/)
- 회사: CSLEE
- 본문 요약: VS Code의 코드 어시스턴트 Cline으로 에이전트 애플리케이션을 개발할 때 작업이 허용된 범위 안에서 목표에 일관되게 도달하도록 하는 '하네스 엔지니어링' 설계를 설명합니다. 설정 오류 수정이 의존성 교체·인증 코드 변경으로 번지거나 일부 입력만 확인하고 완료를 보고하는 문제를 막기 위해, 컨텍스트·도구·실행 제약·검증·피드백을 Observe→Plan→Act→Verify→Feedback 단계로 연결하고 각 단계의 입력·허용 작업·통과 조건·실패 시 조치를 명시합니다.
- 주목할 point: 작업 명세에 목표와 완료 조건을 먼저 적고, 정확해야 하는 데이터 처리는 LLM 대신 검증된 함수(Pydantic strict 등)에 맡기며, 위험도에 따라 권한과 개인정보 접근을 통제합니다. Cline의 Plan/Act, Rules·Workflows·Skills, MCP 도구(run_validation), Hooks, Checkpoints를 검토 가능한 실행 흐름으로 엮고, 필수 검사와 실행 기록으로 완료를 판정하며 반복 평가로 목표 달성·범위 준수·비용을 확인한 작업부터 자율성을 넓히라고 제안합니다.
- keyword: #Cline #하네스엔지니어링 #AI에이전트 #MCP #코드어시스턴트

## [IdP 프로비저닝을 써도 남는 Atlassian 로컬 그룹, 반복 요청을 툴 하나로 처리하기까지](https://tech.osci.kr/atlassian-local-group-automation/)
- 회사: 오픈소스컨설팅
- 본문 요약: 회사 IdP와 SCIM 프로비저닝·SAML SSO로 연결된 Atlassian Jira·Confluence에서도 협력사·기간제 프로젝트·권한 분리용처럼 조직도에 없는 그룹은 로컬 그룹으로 남아 생성·추가·제거를 사람이 해야 했던 문제를 API 기반 단일 툴로 해결한 운영 사례입니다. 그룹 생성·인원 추가, 인원 제거, 그룹 삭제, 명단 조회(엑셀 추출), 여러 Jira 스페이스에 같은 역할 일괄 배정의 5가지 요청 유형별로 처리 순서를 정해 묶었습니다.
- 주목할 point: 인원수만큼 늘어나는 '처리'와 '반영 확인'만 툴로 옮기고, 동기화/로컬 그룹 구분이나 못 찾은 계정 확인처럼 판단이 필요한 일은 사람이 맡았습니다. 추가 후 실제 멤버를 다시 조회해 신청서와 차이만 확인하고, 되돌리기 어려운 제거·삭제는 명단 사전 확인·삭제 전 엑셀 백업·확인 문구 직접 입력을 거치게 해 3명이든 20명이든 같은 순서로 바로 처리할 수 있게 됐습니다.
- keyword: #Atlassian #SCIM #SAMLSSO #운영자동화 #Jira

## [업무 메신저 유출 대응: 크리덴셜 점검 3단계와 Mattermost 자체 호스팅](https://insight.infograb.net/blog/2026/11/26/mattermost-check/)
- 회사: 인포그랩
- 본문 요약: 2026년 11월 9일 카카오워크 서비스 제공자 시스템 침해로 메일 본문·첨부파일·암호화된 메시지가 유출된 사고를 서드파티 위험 사례로 들어, 업무 메신저 유출 시 크리덴셜 점검 3단계를 정리합니다. ① 메시지·첨부파일·DM에서 토큰 접두사(glpat-, AKIA 등)와 키워드 검색, 내보낸 대화의 gitleaks 검사로 크리덴셜 목록화 ② 봇·웹훅 토큰까지 교체(교체 직전 마지막 사용 시각·IP 기록) ③ 침해 시점이 아닌 '공유한 날'부터 사용 기록을 확인하고 공격자가 남긴 SSH 키·토큰·설정 변경을 제거하는 순서입니다.
- 주목할 point: Slack·Mattermost는 AKIA*처럼 별표로 접두사 검색이 되지만 Mattermost는 하이픈을 무시해 glpat- 검색이 부정확하다는 실전 팁이 있습니다. 사전 조치로 시크릿 관리 도구(Vault, Secrets Manager)나 1회 열람 링크로 공유, 토큰 수명 단축과 임시 크리덴셜(IAM Identity Center, CI_JOB_TOKEN), 대화 보존 기간 단축을 권하고, Mattermost 자체 호스팅으로 데이터를 조직 인프라에 두고 저장 전 크리덴셜 패턴을 차단하는 방법을 소개합니다.
- keyword: #보안 #크리덴셜관리 #Mattermost #서드파티위험 #시크릿관리
