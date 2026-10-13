<!-- 이 파일은 posts/2026-10-13.md의 사본입니다. 자동 생성됨. -->
# 2026-10-13 기술 블로그 모음

## [코딩 에이전트가 Spring을 못 짠다면, component scan부터 걷어내 보세요](https://flex.team/blog/2026/10/13/backend46)
- 회사: flex
- 본문 요약: 라이브러리 버전 업그레이드 후 컨트롤러 테스트에서 반복된 BeanDefinitionOverrideException을 분석했습니다. 원인은 @SpringBootApplication의 하위 패키지 component scan에 테스트용 @Configuration이 포함되어 다른 테스트 컨텍스트로 유입된 것이었습니다. component scan 대신 @AutoConfiguration, @Import, AutoConfiguration.imports 기반 명시 등록과 @TestConfiguration 전환, @ConfigurationProperties 활용으로 해결했습니다.
- 주목할 point: 파일 위치에 따라 빈 등록 범위가 달라지는 암묵적 구조는 코딩 에이전트가 추적하기 어렵기 때문에, 명시 등록으로 바꿔 작업의 예측 가능성을 높였습니다. 다만 @Import 누락 시 404·미등록 빈이 생길 수 있어 실제 컨텍스트 검증과 테스트 diff 검토(테스트 비활성화·skip 여부)가 필요합니다.
- keyword: #SpringBoot #Kotlin #ComponentScan #코딩에이전트

## [우리 아이가 달라졌어요: 텍스트에 워터마크를 어떻게 넣을까](http://devocean.sk.com/blog/techBoardDetail.do?id=168550&boardType=techBlog&isShared=Y)
- 회사: 데보션
- 본문 요약: LLM 텍스트 워터마크가 문맥과 비밀키로 다음 토큰 샘플링에 통계적 패턴을 남기고 같은 키로 검출하는 원리를 설명하고, KGW(Green 토큰 logit 보너스), SynthID-Text(후보 토너먼트 점수), textGrain(블록·최적수송 기반 샘플링) 방식을 비교했습니다. 신호 강화와 원래 토큰 분포·응답 다양성 사이의 트레이드오프, 짧거나 편집된 텍스트에서 약해지는 검출력을 짚었습니다.
- 주목할 point: PRD 에이전트에 워터마크를 적용한 뒤 단어 선택이 어색해 PM이 이탈한 사례처럼, 검출력뿐 아니라 요구사항의 강도·책임·기간 같은 의미 보존과 실제 수정 부담을 함께 평가해야 합니다. 어색한 표현, 용어 일관성, 수정 시간, PM 선호도, 응답 다양성을 분리 측정하는 기준이 제안됩니다.
- keyword: #LLM #텍스트워터마크 #SynthID #PRD에이전트

## [여러 번의 연산으로 필요한 지표 만들기](https://on.com2us.com/tech/chart-secondary-operation-analysis/)
- 회사: 게임빌컴투스플랫폼
- 본문 요약: Hive 애널리틱스 차트에서 이벤트·속성에 1차 연산으로 측정값을 만들고, 2차 연산으로 일정 간격별 결과의 최대·최소·평균·최신 값을 다시 계산하는 방법을 소개합니다. 예를 들어 2분마다 접속자를 COUNT DISTINCT로 구한 뒤 MAX를 적용하면 하루 최대 동시 접속자 수를 얻을 수 있습니다.
- 주목할 point: 월간 일평균 AU, 오늘의 최대 동시 접속자 수처럼 한 번의 집계로 얻기 어려운 지표를 별도 쿼리 없이 차트 설정만으로 구성할 수 있습니다.
- keyword: #애널리틱스 #연산 #차트 #하이브

## [차원값을 원하는 기준으로 묶어 비교하기](https://on.com2us.com/tech/chart-dimension-bucket-analysis/)
- 회사: 게임빌컴투스플랫폼
- 본문 요약: Hive 애널리틱스 차트의 구간 설정으로 국가 코드 같은 문자형 값은 그룹으로, 가격·레벨 같은 숫자형 값은 직접 입력하거나 등간격 구간으로 나눠 새로운 차원값처럼 비교하는 방법을 설명합니다. 설정하지 않은 나머지 값도 하나의 이름으로 묶어 볼 수 있습니다.
- 주목할 point: 원본 로그를 바꾸지 않고 화면에서 분류 기준을 바꿔 가며 볼 수 있어, 별도 쿼리나 가공 데이터를 반복해 만들지 않고 분석 준비 시간을 줄일 수 있습니다.
- keyword: #애널리틱스 #구간설정 #차원 #하이브

## [디자이너의 아이디어가 금융상품이 되기까지](https://toss.tech/article/rpg-savings)
- 회사: 토스
- 본문 요약: 자동이체 후 앱을 다시 열 이유가 적었던 기존 ‘키워봐요 적금’의 한계를 넘기 위해, 저금과 캐릭터 성장을 연결한 ‘키우기’ 콘셉트를 재정립했습니다. 일일 스토리와 선택·능력치 기반 멀티엔딩을 갖춘 31일 적금(매일 5,000원 저금 시 연 10% 보상)으로 구체화한 과정을 소개합니다.
- 주목할 point: 사용자 테스트로 예적금 경험이 적은 사용자의 소액 저축 수요를 확인했고, PO와 비용 구조를, DA와 데이터 분석을 협의하며 입문형 상품의 가치를 도출했습니다. 방치된 제품의 재방문 단계와 이탈 지점을 점검하는 데 참고할 만합니다.
- keyword: #UI/UX #사용자테스트 #금융상품 #협업

## [서비스 개발에 집중할 수 있는 AI 플랫폼 만들기](https://toss.tech/article/ai-platform-foundation)
- 회사: 토스
- 본문 요약: GenAI Portal의 모델 사용 신청·프로젝트 설정과 GenAI Gateway의 실제 모델 호출, MCP Gateway의 사내 도구 실행 권한 검증을 연결한 토스 AI 플랫폼 구조를 소개합니다. 프로젝트 단위로 모델 권한·예산·사용량·변경 이력을 통합 관리하고 개인정보·프롬프트 공격 가드레일과 Langfuse 트레이스를 연계했습니다.
- 주목할 point: 누적 예산과 TPM 한도를 분리하고, 진행 중 요청의 예상 출력 토큰을 예약했다가 완료 후 보정하며, 약정 용량(PTU) 우선 라우팅 후 부족 시 PAYG로 전환하는 운영 방식이 눈에 띕니다. 호출 형식 통일과 별개로 모델별 도구 호출·구조화 출력 지원 여부는 따로 확인해야 합니다.
- keyword: #AI플랫폼 #LLMGateway #MCP #토스

## [[데이터주권 시리즈] 주권 확보를 위한 다섯 가지 요건](https://library.gabia.com/contents/infrahosting/15814/)
- 회사: 가비아
- 본문 요약: 데이터 주권을 법인 지배 구조, 운영 접근 권한, 암호화 키, 공급망, 네트워크 경로의 다섯 요건으로 나눠 판정하는 틀을 정리했습니다. CSF는 사업자 비교용 평가 틀, SecNumCloud는 준수 조항을 둔 국가 자격으로 구분하고, 소재지만 역내이고 실질 통제권은 역외에 있는 상태를 CSF의 SEAL-1 사례로 제시합니다.
- 주목할 point: 소재지와 인증만으로는 부족하며, 역외 법 집행 명령이 법인·운영 인력·사업자 보관 키를 통해 데이터에 닿는 위험과 하위 수탁자·펌웨어 업데이트·데이터 이동 경로까지 계약·접근권·키 통제권과 함께 점검해야 합니다.
- keyword: #데이터주권 #cloud #클라우드보안 #SecNumCloud

## [Naver Cloud에서 IaC 기반 Managed Platform 구축하기](https://www.nextree.io/naver-cloudeseo-iac-giban-managed-platform-gucughagi/)
- 회사: 넥스트리
- 본문 요약: VM 기반 Kubernetes·PostgreSQL 직접 운영의 패치·장애 대응·백업·복구 부담을 줄이기 위해 Naver Cloud의 Managed NKS와 Cloud DB for PostgreSQL 중심의 IaC 운영 플랫폼을 구축한 경험을 정리했습니다. Terraform stack으로 네트워크·보안·NKS·DB 등을 분리 관리하고, Ansible로 VM 내부 구성을, GitOps로 애플리케이션 desired state를 관리합니다.
- 주목할 point: 도구별 책임을 분리하고 recovery stack 기반 ‘new DB + cutover’ 복구 흐름으로 복구 리허설과 검증 원칙을 세운 점이 핵심입니다.
- keyword: #Terraform #Ansible #GitOps #NaverCloud

## [MongoDB 클러스터 연결 장애와 설정 개선](https://www.nextree.io/mongodb-keulreoseuteo-yeongyeol-jangaewa-seoljeong-gaeseon/)
- 회사: 넥스트리
- 본문 요약: AWS EKS 배포와 MongoDB Atlas 버전 업그레이드가 겹치며 신규 WAS의 최초 연결이 지연되고, 초기화 대기 중 Kubernetes Health Check와 배포가 진행되어 기존 인스턴스가 종료되는 장애를 분석했습니다. Primary 전환 시 토폴로지 확인·서버 선택 지연과 기본 Timeout 의존이 원인이었고, JVM DNS 캐시 TTL 5초, connectTimeout 3초·readTimeout 5초·serverSelectionTimeout 5초 명시, WriteConcern.MAJORITY와 primaryPreferred 읽기 정책으로 대응했습니다.
- 주목할 point: Timeout 값은 환경별 기동 허용 시간과 쿼리 특성에 맞춰 조정해야 하고, primaryPreferred는 Secondary 조회에 따른 일관성 요구사항 검토가 필요하며, 재발이 없다는 것만으로 설정 효과를 단정할 수 없습니다.
- keyword: #MongoDB #EKS #Timeout #장애분석

## [Forge 앱 하나가 Rovo 에이전트가 되고, MCP 도구가 되기까지](https://tech.osci.kr/forge-app-rovo-agent-mcp-tool/)
- 회사: 오픈소스컨설팅
- 본문 요약: Confluence 문서의 적절한 폴더 위치를 추천·이동하는 Forge 앱을 Rovo 에이전트와 MCP 도구로 확장한 과정을 소개합니다. Forge 앱이 CQL로 스페이스 계층을 조회해 추천 위치와 사유를 제공하고, get-space-tree-action과 move-page-action을 UI·rovo:agent·rovo:mcp에서 재사용하며 Rovo Studio에서 팀별 지시문과 도구 조합을 구성합니다.
- 주목할 point: 권한·확인 절차에 유의해야 하며, rovo:mcp는 미리보기 상태이고 Atlassian 외부 MCP 호출은 지원되지 않으며 로그 내 인증 토큰 마스킹이 필요합니다.
- keyword: #Forge #Rovo #MCP #Confluence

## [“고객의 목소리를 서비스 개선으로 잇는 사람들, 고객만족 CX팀”](https://medium.com/miridih/%EA%B3%A0%EA%B0%9D%EC%9D%98-%EB%AA%A9%EC%86%8C%EB%A6%AC%EB%A5%BC-%EC%84%9C%EB%B9%84%EC%8A%A4-%EA%B0%9C%EC%84%A0%EC%9C%BC%EB%A1%9C-%EC%9E%87%EB%8A%94-%EC%82%AC%EB%9E%8C%EB%93%A4-%EA%B3%A0%EA%B0%9D%EB%A7%8C%EC%A1%B1-cx%ED%8C%80-82ae42e8a6c8)
- 회사: 미리디
- 본문 요약: 고객 문의를 해결하는 데 그치지 않고 반복 문의·클레임 원인을 분석해 안내 문구·서비스 흐름·내부 프로세스 개선으로 연결하는 CX팀을 소개합니다. 디자인·파일 변환·인쇄·배송 단계별 복합 원인이 생기는 PoD 인쇄 커머스 특성을 이해한 서비스 운영자 역할을 강조합니다.
- 주목할 point: 약 두 달간 이론 교육, 선배 상담 관찰, 단순 문의 실습, 클레임·품질 이슈 판단으로 이어지는 온보딩과 AI 상담·자동화 프로세스 병행 운영이 특징입니다.
- keyword: #CX #고객만족 #PoD #온보딩

## [[웨비나 후기] AI 시대, 데이터센터 운영의 기준을 높이다](https://tech.ktcloud.com/entry/2026-10-ktcloud-webinar-review)
- 회사: KT 클라우드
- 본문 요약: 운영자가 바이브 코딩으로 현장 분석·예측 도구를 직접 개발하는 AI 기반 AIDC Ops Studio 사례를 소개합니다. BIM과 운영 데이터를 연결해 간섭 검토, LiDAR 3D 스캐닝 기반 시공 검증, AR 기반 사전 현장 검토를 수행하고 Digital Twin 확장 전략을 제시합니다.
- 주목할 point: FastAPI·Next.js·Google Gemini 계열 모델을 활용하되 민감 데이터는 망 분리하고 API 키를 중앙 관리하는 구성이 언급됩니다.
- keyword: #AIDC #DigitalTwin #BIM #웨비나
