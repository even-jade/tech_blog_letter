<!-- 이 파일은 posts/2026-11-09.md의 사본입니다. 자동 생성됨. -->
# 2026-11-09 기술 블로그 모음

## [스마일게이트의 MS SQL 데이터베이스 현대화 – AWS Transform for SQL Server와 Claude Code의 하이브리드 전략](https://aws.amazon.com/ko/blogs/tech/smilegate-sql-server-modernization-aws-transform/)
- 회사: AWS (스마일게이트 사례)
- 본문 요약: AWS Transform과 Claude Code를 조합해 SQL Server 기반 .NET 시스템 두 개를 Aurora PostgreSQL로 전환한 사례입니다. AWS Transform이 스키마·프로시저와 데이터 접근 계층의 대량 변환 초안을 만들고, 원본·타깃에 동일 입력을 넣는 동등성 검증으로 수정 DDL을 동결한 뒤 Claude Code가 동결 스키마의 프로시저 시그니처를 계약 삼아 코드를 교차 검증·일괄 수정했습니다. DapperHelper 공통 래퍼를 재작성해 256개 호출부의 개별 수정을 최소화했습니다.
- 주목할 point: 빌드가 성공해도 OUTER APPLY, SELECT INTO, 시간 함수, XML 처리 등은 경고 없이 오변환될 수 있어 원본 비교 검증이 필수입니다. DB 트랙 약 87%, 애플리케이션 트랙 약 69%의 공수 절감을 보고했습니다.
- keyword: #AWSTransform #ClaudeCode #SQLServer #AuroraPostgreSQL #마이그레이션

## [로그인 화면, 이제 만들지 마세요 - n3r OIDC](https://d2.naver.com/helloworld/4293206)
- 회사: 네이버 D2
- 본문 요약: 사내 계정 시스템 n3r.iam을 OIDC Provider로 확장해 서비스마다 로그인 화면을 만들지 않고 'n3r 계정으로 로그인' 방식으로 연동하는 구조를 소개합니다. 클라이언트 등록, 연동 설정, 토큰 내 n3r 정보 확인 순으로 이어지며, 토큰에 project·role·group 정보를 담아 Access Token으로 n3r API 호출과 role 기반 인가에 활용합니다.
- 주목할 point: 표준 OIDC 위에 자체 권한 체계를 결합한 설계이며, role이 바뀌면 Access Token을 재발급해 권한을 반영합니다. 적용 범위는 n3r app의 로그인·권한 연동 대상에 한정됩니다.
- keyword: #OIDC #Kubernetes #AccessToken #인가 #SSO

## [PennyLane을 활용한 Amazon Braket에서의 Max-Cut 문제의 해결 (2부) – 세 가지 실행 방식 비교](https://aws.amazon.com/ko/blogs/tech/amazon-braket-pennylane-maxcut-qaoa-part2/)
- 회사: AWS
- 본문 요약: PennyLane QAOA Max-Cut 코드를 로컬, Braket Hybrid Jobs 임베디드 시뮬레이터, SV1 온디맨드 시뮬레이터의 세 방식으로 실행해 비교했습니다. 디바이스 ARN만 바꿔 lightning.qubit, SV1, 실제 QPU로 전환할 수 있고, 실행 위치에 따라 콘솔 추적, 네트워크 왕복, 과금 방식이 달라집니다.
- 주목할 point: 임베디드 시뮬레이터는 네트워크 왕복이 없고 인스턴스 시간으로 과금되는 반면 SV1은 반복마다 태스크를 제출해 왕복과 시뮬레이터 사용량 비용이 붙습니다. QAOA의 확률적 특성상 최고 확률 비트열이 항상 최대 컷은 아니므로 상위 후보의 컷 크기를 고전적으로 계산해 최종 해를 고르라고 권합니다.
- keyword: #AmazonBraket #PennyLane #QAOA #MaxCut #양자컴퓨팅

## [매일 아침 AI가 알려주는 앱 크래시 리포트 자동화 개발 기록](https://medium.com/cj-onstyle/ai-%ED%81%AC%EB%9E%98%EC%8B%9C%EB%A6%AC%ED%8F%AC%ED%8A%B8-%EC%9E%90%EB%8F%99%ED%99%94-%EA%B0%9C%EB%B0%9C-%EA%B8%B0%EB%A1%9D-2ab7ba12d606?source=rss----c2837295b0fd---4)
- 회사: CJ온스타일
- 본문 요약: Firebase Crashlytics API로 이슈 ID, 스택 트레이스, 발생 횟수, 영향 사용자 수, 앱 버전을 추출하고, Jenkins에서 수집한 데이터를 Claude CLI가 develop 브랜치 소스와 함께 분석해 원인과 수정 방향을 Confluence 리포트로 만든 뒤 Slack·Teams로 알리는 자동화 흐름을 구축했습니다.
- 주목할 point: BigQuery에서 Crashlytics 데이터를 확인할 수 없어 API로 전환했고, 토큰 비용과 특정 AI 종속 우려로 Firebase MCP는 채택하지 않았습니다. crashed == true 이슈와 신규 크래시를 우선 처리하며, ANR·OOM은 제외해 분석 가능한 이슈를 우선화하고, 공통 코드를 재사용해 iOS에도 적용했습니다.
- keyword: #Crashlytics #ClaudeCLI #Jenkins #자동화 #Android

## [하나의 플랫폼으로 두 가지 에이전트 런타임 운영하기: 웅진씽크빅의 Amazon Bedrock AgentCore 및 Amazon EKS 기반 플랫폼 구축기](https://aws.amazon.com/ko/blogs/tech/woongjin-thinkbig-agent-platform/)
- 회사: AWS (웅진씽크빅 사례)
- 본문 요약: Bedrock AgentCore와 EKS를 함께 지원하는 사내 AI 에이전트 플랫폼 구축 과정을 소개합니다. 모델·지시문·MCP·지식 기반 설정을 Strands Agents 코드와 컨테이너 이미지로 자동 생성하고, CodeBuild·ECR 파이프라인과 AgentCore Control Plane API로 Runtime 배포와 버전 엔드포인트를 관리합니다. EKS 배포 유형은 Helm values·ArgoCD로 기존 GitOps 흐름에 연동했습니다.
- 주목할 point: ARM64 전용 베이스 이미지를 분리해 exec format error를 해소했고, 설정 저장부터 호출 가능 상태까지 중앙값 약 2분 10초를 달성했습니다. GitOps 상태 판정, outbox 기반 등록 일관성, SQS FIFO 기반 동시 배포 직렬화를 개선 방향으로 검토합니다.
- keyword: #BedrockAgentCore #EKS #MCP #GitOps #AI에이전트

## [경력 없이 시작해 정규직 2개월 만에 연봉 8천만원, "다음 목표는 1억"](https://corp.banksalad.com/blog/culture/bfs-interview-1/)
- 회사: 뱅크샐러드
- 본문 요약: 뱅크샐러드 컬처 블로그의 구성원 인터뷰 글로, 제목 기준으로 경력 없이 입사해 정규직 전환 2개월 만에 연봉 8천만 원을 달성한 사례를 다룹니다. 원문 본문은 직접 확인하지 못해 제목·회사 등 확인 가능한 정보만 기록합니다.
- 주목할 point: 기술 내용보다 조직문화·보상 체계 중심의 글입니다.
- keyword: #뱅크샐러드 #인터뷰 #조직문화

## [망분리 환경에서도 한 달 만에 AX로 생산성을 높인 방법](https://corp.banksalad.com/blog/tech/banksalad-ax-workflow-automation/)
- 회사: 뱅크샐러드
- 본문 요약: 개인정보·민감 데이터를 다루는 망분리 환경에서 AX 적용 범위를 '개인정보 제외·사내 용도·연구개발망 한정'으로 제한하고, 사내 호스팅이 가능한 오픈소스 n8n 중심으로 재무·CR팀의 반복 업무를 자동화했습니다. 스크래핑, LLM 판정·요약, Slack 알림을 조합해 정부지원과제 후보 선별, 법인카드 잔액 알림, 신규 회사 뉴스 탐지·논조 분석 등을 구현했습니다.
- 주목할 point: 비개발 직군이 직접 수정할 수 있는 시각적 워크플로 도구를 우선했고, 재무팀 인당 일일 30분~1시간 절감과 CR팀 즉시 대응 체계를 확보했습니다.
- keyword: #n8n #LLM #AX #자동화 #망분리

## [TASTE, 토스의 추천 파운데이션 플랫폼](https://toss.tech/article/taste)
- 회사: 토스
- 본문 요약: TASTE는 앱이벤트 공동학습(DCN-V2 인코더, Causal Transformer 시퀀스 모듈, PLE 기반 과제별 예측)으로 사용자 표현을 만들고, 예측 확률과 임베딩을 여러 추천·타기팅 모델에 제공하는 플랫폼입니다. 앱이벤트와 소비는 특성과 정답 시점이 달라 목적별로 모델을 분리했고, 서비스 과제를 재현한 TASTE Bench로 임베딩 후보의 전이 성능을 사전 비교합니다.
- 주목할 point: 공통 앱이벤트 Macro Recall@5k가 상대 35.1% 개선됐고, 임베딩 추가로 CRM·쇼핑·광고 모델의 AUROC와 미니앱 추천 온라인 CTR이 개선됐습니다. 모든 행동을 단일 모델로 학습하면 성능이 상충하고, 모델 갱신에 따른 벡터 분포 변화 대응이 과제로 남습니다.
- keyword: #추천시스템 #임베딩 #Transformer #ML #A/B테스트

## [왓챠가 사용자의 취향에 다가가는 방법 (feat. CIKM)](https://medium.com/watcha/%EC%99%93%EC%B1%A0%EA%B0%80-%EC%82%AC%EC%9A%A9%EC%9E%90%EC%9D%98-%EC%B7%A8%ED%96%A5%EC%97%90-%EB%8B%A4%EA%B0%80%EA%B0%80%EB%8A%94-%EB%B0%A9%EB%B2%95-feat-cikm-ba3ce5c7d787?source=rss----bd1678892a27---4)
- 회사: 왓챠
- 본문 요약: 코사인 유사도 기반 Sampled Softmax 학습에서도 인기 편향이 남는 원인을 분석했습니다. 학습 중 원본 임베딩 길이가 커지며 인기도별 그래디언트 크기가 달라지고, 인기작이 positive로 자주 등장해 업데이트가 누적 집중되기 때문입니다. 매 업데이트 후 임베딩을 정규화하는 L2 Projection과 시청 수를 로그 스케일로 반영하는 Degree Prior를 결합한 GD-SSM을 제안했습니다.
- 주목할 point: SSM 대비 전체 Recall@20 7.2%, NDCG@20 9.9% 개선, 롱테일 Recall@20 39.0%, NDCG@20 61.4% 개선과 커버리지 확대를 보였고, 추가 학습 파라미터나 튜닝 하이퍼파라미터가 필요 없습니다.
- keyword: #추천시스템 #협업필터링 #인기편향 #LightGCN #CIKM

## [[행사스케치] 국방 AI를 위한 풀스택 기술 파트너 : IAMSEC 2026 국제 육군 M&S 전시회](https://blog.naver.com/n_cloudplatform/224470078838)
- 회사: 네이버 클라우드 플랫폼
- 본문 요약: 대전컨벤션센터에서 열린 IAMSEC 2026 국제 육군 M&S(모델링·시뮬레이션) 학술 컨퍼런스 및 전시회 참가 현장을 소개합니다. '국방 AI를 위한 풀스택 기술 파트너'를 주제로 한 기조연설과 전시 부스 운영 내용을 다룹니다.
- 주목할 point: 기술 심층 분석보다는 행사 참가 스케치 성격의 글입니다.
- keyword: #네이버클라우드 #국방AI #M&S #행사스케치

## [RAG 검색 알고리즘을 바꾸지 않고 검색 품질을 개선한 방법_AIOps](https://blog.cslee.co.kr/improving-rag-search-quality-with-query-centric-data/)
- 회사: CSLEE
- 본문 요약: 질문과 상세 답변을 함께 인덱싱한 Q&A RAG에서 부가 설명이 많은 문서가 정답보다 상위에 노출되는 문제를 분석했습니다. BM25와 KNN 양쪽의 잘못된 상위 순위가 RRF 결합에서도 이어지는 구조였고, 검색 알고리즘은 유지한 채 검색 대상을 질문 의도 중심의 Query-Centric 텍스트로 재설계하고 Answer ID로 별도 Answer DB에서 상세 답변을 조회하도록 역할을 분리했습니다.
- 주목할 point: Top-1 Accuracy, Hit@K, Retrieval Failure Rate@K로 효과를 검증하며, 검색 표현의 과도한 확장 방지, 한국어 토큰화 설정 점검, 중복 Answer ID 처리, 인덱스-답변 DB 정합성 관리가 필요합니다.
- keyword: #RAG #BM25 #KNN #RRF #AIOps

## [코드에서 화면 지도를 그리고, AI와 함께 회귀 테스트의 빈 곳을 채우다](https://helloworld.kurly.com/blog/web-e2e-coverage-map/)
- 회사: 마켓컬리
- 본문 요약: 3개 프론트 레포의 라우트 467개를 코드 기준으로 수집하고 Playwright 크롤러 실측과 기존 E2E 분석을 결합해 화면 지도를 만들었습니다. 담당자 검토로 제외·제약·기구현·구현 대상을 분류하고, Claude Code와 서브에이전트로 시나리오 제안과 Jira·Kase 등록을 자동화해 모바일웹 35개·PC 34개 화면에 신규 테스트 114개를 3.5일 만에 추가했습니다.
- 주목할 point: 고장 주입과 다중 에이전트 리뷰로 항상 통과하는 판정, 잘못된 선택자, 플랫폼 간 누락을 보완했고, 12개 러너 병렬 실행으로 568개 테스트를 13분 44초에 수행합니다. 분기별 라우트 변화 점검으로 지도를 최신화할 계획입니다.
- keyword: #ClaudeCode #Playwright #E2E #회귀테스트 #QA
