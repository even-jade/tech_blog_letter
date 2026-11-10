<!-- 이 파일은 posts/2026-11-10.md의 사본입니다. 자동 생성됨. -->
# 2026-11-10 기술 블로그 모음

## [AI 스킬 만들기 10계명: Figma→Code 자동화 실전기](https://d2.naver.com/helloworld/8562180)
- 회사: 네이버
- 본문 요약: Claude Agent Skills(SKILL.md·references·scripts)로 Figma 디자인을 Android UI 코드로 변환하는 맞춤 스킬을 만들며 얻은 설계 원칙을 정리했습니다. Node ID 추출, 디자인 컨텍스트·스크린샷 확보, 에셋 분류·처리, 코드 변환, 검증으로 이어지는 7단계 워크플로를 구성하고, 에셋을 정적 에셋·동적 비주얼·기존 리소스(A/B/C)로 분류해 VectorDrawable·WebP·Canvas 처리 방식을 결정합니다. (원문 사이트가 이번 수집 환경에서 접근 제한되어 velopers.kr 요약 정보를 바탕으로 정리했습니다.)
- 주목할 point: 결과가 고정된 변환·검증은 스크립트로, 판단이 필요한 분류·스타일은 기준표로 분리하고, 모델이 이미 아는 일반 지식은 SKILL.md에서 빼 토큰 낭비와 규칙 희석을 막습니다. 작성 세션의 대화 맥락·메모리·Git 히스토리로 테스트 결과가 오염되지 않도록 검증 환경을 분리하라는 조언이 인상적입니다.
- keyword: #Claude #AgentSkills #Figma #Android #자동화

## [유진그룹의 온톨로지 여정: Amazon Neptune과 Amazon Bedrock으로 건자재 유통 데이터를 지식 그래프로 전환하기](https://aws.amazon.com/ko/blogs/tech/eugene-ontology/)
- 회사: AWS
- 본문 요약: 온라인몰·POS·WMS·ERP에 분산되고 코드 체계가 제각각인 건자재 유통 데이터를 R2G·GRAD 방법론과 GoodRelations·schema.org·GS1 표준으로 모델링해 Amazon Neptune 지식 그래프로 전환한 PoC입니다. Bedrock(Claude Sonnet 4.5) 기반 Rule-grounded Text-to-Cypher 에이전트가 자연어 질의를 규칙·스키마 컨텍스트와 함께 openCypher로 변환해 재고·납기·대체품을 탐색합니다.
- 주목할 point: 7개 업무 질의(CQ)의 그래프 질의 성립을 검증했고, 키워드 규칙 매칭·최대 3회 자기교정·별칭 탐색으로 신뢰성을 보완했습니다. 운영 확장의 선결 과제로 데이터 표준화, 용어집, 정답 검증 계층, 도메인 전문가 협업을 꼽았습니다.
- keyword: #AmazonNeptune #AmazonBedrock #지식그래프 #온톨로지 #TextToCypher

## [[데이터센터 입문 시리즈] 6가지 조건이 정하는 입지 선택](https://library.gabia.com/contents/infrahosting/16132/)
- 회사: 가비아
- 본문 요약: 데이터센터 입지를 결정하는 조건을 시설 구축·운영 조건(전력·부지·물·지반)과 고객 도달 조건(통신망·고객 거리)으로 나눠 설명합니다. 송전망 여유가 부족하면 계통 접속 대기, 공급 전력 축소, 개소 지연이 생길 수 있어 전력 확보를 최우선 기준으로 둡니다.
- 주목할 point: 대도시 입지(낮은 지연·우수한 연결성 vs 높은 토지 비용·전력 제약)와 외곽 입지(전력·증설 부지 확보 vs 고객·인력 확보 어려움)의 트레이드오프, 물 절약 냉각과 추가 전력 소비의 교환 관계, AI 학습·추론처럼 지연 민감도가 다른 워크로드별 입지 판단을 정리했습니다.
- keyword: #데이터센터 #전력 #입지 #인프라

## [실행은 격리하고, 세션은 이어간다: 망분리 환경의 Agent Platform 설계기](https://toss.tech/article/agent-platform-foundation)
- 회사: 토스
- 본문 요약: 망분리 환경에서 내부 데이터 분석 자동화용 에이전트 코드를 실행하기 위해, 사용자별 Kubernetes Pod를 Workspace로 재사용하고 OpenSandbox로 수명주기를 관리하는 플랫폼을 설계했습니다. Runtime은 bubblewrap 기반 Linux namespace 안에서 하네스와 도구를 실행하고, 작업 파일·하네스 세션 상태는 PV에, 공통 실행 기록은 OpenResponses 형식으로 보관해 Pod 교체 후에도 대화를 이어갑니다.
- 주목할 point: 인증 프록시로 API 키를 노출하지 않고 Gateway로 모델·도구 호출 경로를 통제합니다. namespace 격리는 VM 운영 부담을 줄이지만 호스트 커널을 공유하는 한계가 있고, 세션 재개는 중단 지점 재실행·외부 작업 롤백을 지원하지 않는다는 트레이드오프를 명시했습니다.
- keyword: #Kubernetes #OpenSandbox #AIAgent #망분리 #샌드박스

## [비가 오면 사장님이 먼저 압니다: SSE로 만든 실시간 기상악화 알림](https://techblog.woowahan.com/28139/)
- 회사: 우아한형제들
- 본문 요약: 기상악화로 라이더가 부족해 주문 취소가 늘어나는 상황을 파트너(사장님)에게 즉시 알리기 위해 SSE 기반 실시간 알림을 설계했습니다. 외부 기상악화 이벤트를 SNS·SQS로 받아 Kafka로 재발행하고, 파드별 고유 groupId로 전체 파드에 fan-out한 뒤 연결된 파트너에게만 선별 전송하며, SSE는 신호만 보내고 최신 상태는 REST API로 재조회하는 zero-payload 방식을 택했습니다.
- 주목할 point: 폴링·롱 폴링·WebSocket 대비 단방향 요구에 맞는 SSE를 선택한 이유와, Reactor Sink 멀티캐스트·느린 구독자 이벤트 폐기, Nginx 버퍼 비활성화·연결 상한, heartbeat와 재연결 지터·백오프 등 운영 전략을 함께 다룹니다.
- keyword: #SSE #Kafka #Reactor #실시간알림 #백엔드

## [데이터로 돌아보는 6번의 Channel Dev Meetup](https://tech.channel.io/kr/articles/eda834e2)
- 회사: 채널톡
- 본문 요약: 6회 개발자 밋업을 관심도(Demand)·현장 경험(Experience)·행사 후 관계(Engagement) 세 지표로 회고했습니다. 누적 신청 1,303건, 참석 386명, 평균 참석률 74.2%, 세션·네트워킹 만족도 4.42점, 운영 만족도 4.60점을 기록했습니다.
- 주목할 point: 넓은 주제보다 DynamoDB 운영처럼 실무 문제를 깊게 다룬 회차의 만족도가 높았고, 회차당 2~3주 준비·약 160만 원 예산으로 피드백을 다음 회차에 반영했습니다. 재신청·커피챗 의향을 관계 형성 지표로 활용한 점이 참고할 만합니다.
- keyword: #밋업 #개발문화 #컨퍼런스 #데이터회고

## [게임듀오가 Amazon EC2 기반 ClickStack으로 게임 서버 관측성 비용을 절반 이하로 줄인 방법](https://aws.amazon.com/ko/blogs/tech/gameduo-clickstack-on-amazon-ec2/)
- 회사: AWS
- 본문 요약: 250대 이상 게임 서버에서 일일 로그 1~2억 건, 스팬 4~6억 건을 수집하던 게임듀오가 SaaS 과금·15일 보존 제한·Loki 검색 타임아웃 문제를 EC2 기반 ClickStack(ClickHouse)으로 해결했습니다. OpenTelemetry Collector를 거쳐 S3에 원문을 먼저 적재하고 SQS 이벤트로 ClickHouse에 비동기 INSERT하며, EBS 핫 티어·S3 콜드 티어·TTL로 보존 정책을 구성했습니다.
- 주목할 point: S3·SQS 버퍼와 DLQ로 ClickHouse 중단이나 Fargate Spot 회수 시에도 재처리가 가능하고, 카나리·CloudWatch 데드맨으로 유실을 감시합니다. Grafana SQL 알람을 16개에서 170여 개로 늘리며 관측 비용은 절반 이하로 줄였습니다.
- keyword: #ClickHouse #ClickStack #OpenTelemetry #관측성 #AWS

## [RAG 시스템의 재순위화(Reranking): 구조와 발전부터 리랭커 선정까지](https://blog.cslee.co.kr/rag-%ec%8b%9c%ec%8a%a4%ed%85%9c%ec%9d%98-%ec%9e%ac%ec%88%9c%ec%9c%84%ed%99%94reranking-%ea%b5%ac%ec%a1%b0%ec%99%80-%eb%b0%9c%ec%a0%84%eb%b6%80%ed%84%b0-%eb%a6%ac%eb%9e%ad%ec%bb%a4-%ec%84%a0/)
- 회사: CSLEE
- 본문 요약: RAG에서 1차 검색 후보 10~20건의 관련도를 크로스 인코더·LLM 기반 모델로 다시 평가하는 재순위화의 구조와 발전(규칙 기반 → 크로스 인코더 → LLM → 추론형·한국어 특화·경량 모델)을 정리하고, 한국어 기업 문서로 여러 리랭커를 비교했습니다. 모든 모델이 미적용 대비 nDCG@10과 1위 정답률을 높였고, Nemotron-3.5-Rerank-8B가 nDCG@10 0.711, KURE-Reranker-base가 1위 정답률 87.8%로 최고였습니다.
- 주목할 point: 저지연·소형 GPU 환경엔 bge-reranker-v2-m3-ko나 KURE-Reranker-nano, 균형형으로 KURE-Reranker-base, 정확도 우선이면 Nemotron을 권합니다. 후보 20건 이후엔 정확도 이득이 작고, 1차 검색에서 빠진 정답은 복구할 수 없다는 한계도 짚었습니다.
- keyword: #RAG #Reranking #리랭커 #LLM #한국어검색

## [우리 팀만의 스펙 주도 개발 정착기](https://d2.naver.com/helloworld/8644274)
- 회사: 네이버
- 본문 요약: 팀 개발 정책으로 스펙 주도 개발(SDD)을 채택하고 정착시킨 배경과 시행착오, 팀이 채택한 SDD 구조와 정책 수립 과정의 고민, 남은 과제를 공유하는 NAVER Engineering Day 10th 발표 세션 공개 글입니다. (원문 사이트가 이번 수집 환경에서 접근 제한되어 velopers.kr 요약 정보를 바탕으로 정리했습니다.)
- 주목할 point: SDD 도입을 검토하는 팀이 정책화 과정에서 겪을 고민과 시행착오를 미리 확인할 수 있는 사례입니다.
- keyword: #SDD #스펙주도개발 #개발프로세스 #NAVEREngineeringDay

## [프로덕트 디자이너와 개발자를 연결하는 AX 프로젝트, AXPD스쿼드](https://medium.com/miridih/%ED%94%84%EB%A1%9C%EB%8D%95%ED%8A%B8-%EB%94%94%EC%9E%90%EC%9D%B4%EB%84%88%EC%99%80-%EA%B0%9C%EB%B0%9C%EC%9E%90%EB%A5%BC-%EC%97%B0%EA%B2%B0%ED%95%98%EB%8A%94-ax-%ED%94%84%EB%A1%9C%EC%A0%9D%ED%8A%B8-axpd%EC%8A%A4%EC%BF%BC%EB%93%9C-bac79dfe09a3?source=rss----79ed61a9dcb1---4)
- 회사: 미리디
- 본문 요약: AI로 빠르게 만든 프로토타입이 개발 단계에서 결국 재작성되고, 화면 동작·상태·예외를 담은 디스크립션과 따로 관리되며 생기는 디자인·개발 협업 병목을 분석했습니다. 도구를 통일하는 대신 디자인 규칙·상태·예외·동작을 확인하는 공통 검증 루트와, 피그마 요소와 코드 컴포넌트를 잇는 AI-Readable Design System, 피그마·Claude Design·Open Design 결과물을 Storybook으로 연결하는 경로별 하네스를 마련했습니다.
- 주목할 point: 스쿼드가 결과물을 대행하지 않고 각 팀이 하네스를 직접 만들고 고치게 하며, 자립적 적용을 전제로 스쿼드 해체를 목표로 삼았다는 운영 방식이 특징입니다.
- keyword: #Storybook #디자인시스템 #AX #프로토타입 #하네스

## [캠페인 메타엔진 — 무진장 많은 콘텐츠를 하나의 캠페인 구조로 통합하다](https://techblog.musinsa.com/%EC%BA%A0%ED%8E%98%EC%9D%B8-%EB%A9%94%ED%83%80%EC%97%94%EC%A7%84-%EB%AC%B4%EC%A7%84%EC%9E%A5-%EB%A7%8E%EC%9D%80-%EC%BD%98%ED%85%90%EC%B8%A0%EB%A5%BC-%ED%95%98%EB%82%98%EC%9D%98-%EC%BA%A0%ED%8E%98%EC%9D%B8-%EA%B5%AC%EC%A1%B0%EB%A1%9C-%ED%86%B5%ED%95%A9%ED%95%98%EB%8B%A4-a29ece6ae6d9?source=rss----f107b03c406e---4)
- 회사: 무신사
- 본문 요약: 월 1,000건 이상의 CRM 캠페인 수작업 설정과 라이브·기획전·매거진 등 이질적 콘텐츠를 통합하기 위해 5W1H 기반 공통 캠페인 모델과 어댑터 구조를 도입했습니다. Campaign Content·Content Snapshot·Campaign Asset·Campaign Execution Record로 책임을 나누고, 원천 데이터를 어댑터로 변환한 뒤 오디언스 평가·발송·성과 수집 파이프라인을 재사용합니다.
- 주목할 point: 메타데이터 변경분만 스냅샷으로 축적해 실행 시점 콘텐츠 상태를 복원하고, ML 적합도 계산 전 하드 제약(수신 동의·유효 기간·소재 완결성)으로 필터링합니다. 월 수억 건 메시지 중 절반 이상을 최적화하고 캠페인 세팅 시간을 절반 이하로 줄였으며, 정규화된 메타데이터로 LLM 푸시 문구의 브랜드명 오역도 줄였습니다.
- keyword: #CRM #캠페인 #메타데이터 #개인화 #아키텍처

## [AI가 바꾼 보험 영업의 방식, AI-Native Sales](https://corp.banksalad.com/blog/culture/bfs-ai-native-sales/)
- 회사: 뱅크샐러드
- 본문 요약: 뱅크샐러드금융서비스의 '금융 솔루션 전문가'의 하루를 따라가며 AI 중심으로 재설계한 보험 영업 방식을 소개합니다. AI 상담 시스템이 고객을 상태별로 정리해 두고, 마이데이터로 고객의 보험 계약 전체를 확인해 몇 분 만에 보장 진단을 준비하며, 채팅 상담에서 AI가 지난 대화 요약·다음 메시지 초안·약관 및 특약 페이지 검색, 응답이 끊긴 고객 재접촉을 맡습니다.
- 주목할 point: 현장 아이디어를 사내 메신저로 공유하면 다음 날 시스템에 반영되고, 실적 대시보드로 당일 계약과 예상 인센티브를 바로 확인합니다. 기술 심층 분석보다는 조직·채용 소개 성격의 컬처 글입니다.
- keyword: #AINative #보험영업 #마이데이터 #뱅크샐러드 #컬처

## [꿈꾸던 AI가 되었어요 - Anthropic 꿈꾸기(dreaming) 글을 우리 개발 환경에 적용하기](http://devocean.sk.com/blog/techBoardDetail.do?id=168600&boardType=techBlog&isShared=Y)
- 회사: 데보션(SK)
- 본문 요약: 에이전트 메모리를 원본 기록과 대조해 정제하는 Anthropic의 '꿈꾸기(dreaming)' 개념을 원본 기록·메모 노트·링크형 메모리·주입 컨텍스트의 4계층으로 정리하고, Claude Code 프로젝트 메모리에 적용하는 방법을 제안합니다. MEMORY.md는 작은 인덱스로 유지하고 세부 규칙은 주제별 메모 파일로 분리하며, Claude Code 스킬과 cron 등 스케줄러로 원본 확인·메모 통합·변경 보고를 주기적으로 수행합니다.
- 주목할 point: 상위에 주입되는 메모리의 오류는 이후 모든 세션의 반복 실수로 전파되므로, 원본으로 확인한 사실만 반영하고 비밀값·개인정보는 기록하지 않으며 자동 정리 결과는 사람이 검토해야 한다고 강조합니다.
- keyword: #ClaudeCode #AgentMemory #Anthropic #LLM #메모리관리
