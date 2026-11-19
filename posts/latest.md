<!-- 이 파일은 posts/2026-11-19.md의 사본입니다. 자동 생성됨. -->
# 2026-11-19 기술 블로그 모음

## [백엔드 개발자 한 명이 팀처럼 일하는 법](https://tech.channel.io/kr/articles/d87a6773)
- 회사: 채널톡
- 본문 요약: 채널톡 커머스 백엔드 개발자가 넉 달간 600개 넘는 PR을 머지한 AI 다중 세션 운영 구조를 소개합니다. Linear 이슈 → 계획 확정 → 구현 → 빌드·테스트 → 관점별(스펙·백엔드·보안·도메인·설계) 병렬 리뷰 → PR → CI·리뷰 대응 → 회고로 이어지는 '하네스'를 만들고, 머지 뒤 검증 환경 E2E 실패 시 후속 PR을 자동으로 여는 단계를 추가했습니다. 이후 세션을 워커(이슈 1건)·PM(프로젝트별, "바로 머지/리뷰 요청/보류" 판정만 보고)·오케스트레이터(최상위)로 나누고, 결정할 것을 모으는 웹 보고판을 두었습니다.
- 주목할 point: 사람 개입 횟수·턴 비용·단계별 방어를 지표로 삼아, 대기 턴을 큰 세션에서 분리하고 감시를 합쳐 런당 턴을 39→24로, 회고 턴을 12→4로 줄였습니다. 모든 테스트를 통과한 카페24 주문 메모가 실제로는 바이트 기준 글자 수 제한에 걸린 사례, 런당 비용 절감의 대부분은 하네스가 아니라 모델 단가 변화 덕이었다는 점, PM 층 도입 후 개입 횟수가 오히려 2배 넘게 늘었다는 점까지 솔직하게 공유합니다.
- keyword: #AI에이전트 #하네스 #Claude #Codex #오케스트레이터 #개발생산성

## [온톨로지, 구축에서 활용까지. 질문이 답을 설계한다.](https://d2.naver.com/helloworld/5037527)
- 회사: 네이버 D2
- 본문 요약: NAVER Engineering Day 10th 발표 공개 세션입니다. 가상의 물류회사가 받는 "S-15262 화물은 지금 어디 있고, 예외가 있었나?"(조회)와 "예외 난 소포, 다시 배송 보낼 수 있나?"(조작) 두 질문을 축으로, 스키마가 아닌 고객 Pain Point 질문에서 출발해 Object·Property·Link·Action을 도출하는 온톨로지 구축 과정과 RDB·RDF/OWL·Foundry 구현 방식을 다룹니다. 데모 모델은 Object Type 60개, Link 63개, Action 31개 규모입니다.
- 주목할 point: 같은 질문을 LLM 단독(환각), RAG(최신 상태 보장 어려움), 온톨로지+에이전트(정확한 상태 조회와 쓰기 Action, 대신 비용 최대)에 던져 비교하고, 사람 승인이 필요한 Action은 에이전트가 승인 대기 상태로 멈추는 흐름과 FDE의 요구 분해 6항목(도메인·데이터 위치·용어 차이·제약·정확도 기준·우선순위)을 소개합니다. (본문은 발표 소개·목차 중심이며 상세 내용은 영상)
- keyword: #온톨로지 #AI에이전트 #RAG #FDE #Foundry #EngineeringDay

## [Devops Agent 리포트 오이데~ 평가 야호~](https://d2.naver.com/helloworld/0118355)
- 회사: 네이버 D2
- 본문 요약: NAVER Engineering Day 10th 발표 공개 세션으로, 네이버 통합검색 알람이 발생하면 1분 안에 장애 1차 진단 리포트를 이슈로 남기는 Devops Agent와, 그 리포트를 평가해 시스템 정확도를 도출한 경험을 다룹니다. 목차는 에이전트 소개, 에이전트라서 생기는 문제, 평가 기준 정하기, 평가 시스템 구성·구축, 향후 방향입니다.
- 주목할 point: LLM 기반 이상 신호 분석 시스템을 "만드는 것"보다 결과를 어떻게 평가해 정확도를 수치화할지에 초점을 맞춘 발표입니다. (본문은 발표 소개·목차 중심이며 상세 내용은 영상)
- keyword: #DevOps #AI에이전트 #장애진단 #LLM평가 #EngineeringDay

## [부족한 건 모델이 아니라 팀 문서였다: 팀 공유 지식층 Third Brain 구축기](https://d2.naver.com/helloworld/2622882)
- 회사: 네이버 D2
- 본문 요약: NAVER Engineering Day 10th 발표 공개 세션으로, 네이버 Observability 담당 팀이 AI가 팀 업무 질문에 답하지 못하는 원인이 모델이 아니라 팀 문서의 부재임을 확인하고, 팀 위키를 AI가 읽고 쓰는 공유 지식층 'Third Brain'으로 만들어 운영한 경험을 공유합니다.
- 주목할 point: "어디에 적나요? 문서는 누가 업데이트하나요? AI가 쓴 걸 믿을 수 있나요?"라는 실무 질문을 중심으로 목차가 구성되어, 팀 지식 관리와 AI 활용을 함께 고민하는 개발자에게 참고가 됩니다. (본문은 발표 소개·목차 중심이며 상세 내용은 영상)
- keyword: #지식관리 #ThirdBrain #팀위키 #AI에이전트 #EngineeringDay

## [Jetpack Compose 기반 커스텀 3D 캐러셀 개발기](https://d2.naver.com/helloworld/2957037)
- 회사: 네이버 D2
- 본문 요약: NAVER Engineering Day 10th 발표 공개 세션으로, ThingsBook 서비스의 비스듬히 겹쳐 쌓이고 넘길 때마다 간격·기울기가 바뀌는 3D 카드 덱을 LazyRow 없이 Jetpack Compose로 직접 구현한 과정을 다룹니다. Float 하나로 모든 카드를 움직이는 구조를 바탕으로 세 가지 이슈를 해결했습니다.
- 주목할 point: ① 매 프레임 바뀌는 값을 리컴포지션 0으로 반영하기, ② 3D로 기울인 UI의 터치 영역이 어긋나는 버그를 직접 판정으로 해결하기, ③ LazyRow 없이 Paging3의 다음 페이지 로드 제어하기, 그리고 AI와 함께 만들며 빨라진 점과 안 됐던 점을 다룹니다. (본문은 발표 소개·목차 중심이며 상세 내용은 영상)
- keyword: #JetpackCompose #Android #캐러셀 #리컴포지션 #Paging3 #EngineeringDay

## [자연어로 세그먼트의 구매 리텐션 확인하기: Hive Axyl Plugin 활용 4편](https://on.com2us.com/tech/hive-axyl-plugin-segment-retention/)
- 회사: 게임빌컴투스플랫폼
- 본문 요약: ChatGPT에 Hive Axyl Plugin을 설치해 이용자 조건을 자연어로 지정하면 Hive 애널리틱스 세그먼트를 만들고, 그 세그먼트를 대상으로 기준·복귀 이벤트, 기간, 표시 단위를 대화로 정해 리텐션을 구성할 수 있습니다. 3편에서 매출·ARPPU 변화가 컸던 미국·GO 마켓 결제 이용자(PU) 세그먼트를 만들고 구매 리텐션을 생성해 변화가 일시적인지 확인하는 예시를 보여 줍니다.
- 주목할 point: 세그먼트·리텐션 저장 전 적용 조건, 대상, 예상 이용자 수, 저장 위치, 중복 여부를 먼저 보여 주고 사용자가 승인한 뒤 생성하는 'human-in-the-loop' 흐름이 MCP 기반 분석 도구 설계 측면에서 눈여겨볼 만합니다.
- keyword: #HiveAxyl #MCP #애널리틱스 #세그먼트 #리텐션 #자연어분석

## [자연어로 대시보드 핵심 변화 요약하기: Hive Axyl Plugin 활용 3편](https://on.com2us.com/tech/hive-axyl-plugin-dashboard-summary/)
- 회사: 게임빌컴투스플랫폼
- 본문 요약: Hive Axyl Plugin으로 Hive 애널리틱스에 저장된 대시보드를 자연어로 요약해 여러 차트의 핵심 변화와 주요 기여 대상을 한 번에 파악하는 방법을 소개합니다. 화면 이미지가 아니라 각 차트의 지표·차원·기간·필터와 조회 결과를 기준으로 비교하며, 예시에서는 전주 같은 요일 대비 매출 27.5%, 결제 이용자 7.8%, ARPPU 18.2% 증가와 미국·GO의 특정 상품 고액 결제가 주요 기여 요인으로 요약됐습니다.
- 주목할 point: 요약 후 국가·마켓·상품을 지정한 후속 질문으로 범위를 좁히고, 특정 날짜에 몰린 고액 결제는 기간을 넓혀 반복 패턴인지 다시 확인하는 등 요약을 그대로 믿지 않고 검증하는 분석 절차를 함께 제시합니다.
- keyword: #HiveAxyl #MCP #대시보드 #ARPPU #자연어분석 #애널리틱스

## [AI와 Playwright로 구축한 E2E 테스트 자동화: 적용 경험과 확장 방향](https://on.com2us.com/tech/hive-playwright-e2e-test-automation/)
- 회사: 게임빌컴투스플랫폼
- 본문 요약: Hive 콘솔에서 AI로 Playwright 테스트 스펙 파일과 실행·관리 도구(React·TypeScript UI + 로컬 Node.js 서버)를 만들어 E2E 테스트를 자동화한 경험입니다. 스펙 원본은 QA 저장소에서 공용 관리하고 프론트엔드 저장소도 참조하며, 셸 안에 제품 화면을 iframe으로 띄우는 콘솔 구조에 맞춰 셸 메뉴로 진입하는 흐름을 기본으로 삼았습니다. 로그인 상태는 storageState로 재사용하고, 데이터는 실데이터와 MSW Mock 모드로 나누며, 운영 환경에서는 데이터 변경 실행을 차단했습니다.
- 주목할 point: 탐색은 Playwright MCP, 반복 검증은 저장된 스펙으로 나눠 매 실행마다의 AI 호출을 줄인 설계가 핵심입니다. 요소는 나타났지만 애니메이션 진행 중이라 패널이 덜 열린 스크린샷 문제를 보완했고, 607건 중 484건 통과·123건 건너뜀 기록을 들어 "건너뛴 항목과 이유도 함께 봐야 한다"고 강조합니다.
- keyword: #Playwright #E2E테스트 #테스트자동화 #MSW #TraceViewer #AI활용

## [Cursor MCP를 AI 코딩 워크플로우 관점에서 정리하기](https://blog.bespinglobal.com/post/cursor-mcp-in-ai-coding-workflow/)
- 회사: 베스핀글로벌
- 본문 요약: Cursor에서 MCP를 IDE 내 AI와 문서·스키마·이슈·운영 도구를 연결하는 표준 구조로 보고, `mcp.json`(command·args·env·envFile) 설정, tool approval, 서버 실패 시 격리 동작, MCP의 tools(행동)·resources(근거)·prompts(절차) 구분을 정리합니다. 데이터 엔지니어링 관점에서 문서 검색, 스키마 조회(Unity Catalog·Glue 등), Job 상태 조회, Issue/PR 조회, 내부 API 명세 서버를 후보로 제시합니다.
- 주목할 point: read-only 서버부터 시작, 최소 권한 API key, secret은 env로 분리, 개인정보 포함 resource 제외, write tool은 별도 승인·로깅이 있을 때만 허용하는 기준과, 조회/외부 호출/데이터 변경·배포를 3단계 승인 수준으로 나누는 방식을 제안합니다. 민감 데이터는 local stdio 서버로 제한하라는 권고도 담았습니다.
- keyword: #Cursor #MCP #AI코딩 #ToolApproval #보안 #데이터엔지니어링

## [오픈소스 통합 보안 솔루션 Wazuh](https://tech.osci.kr/wazuh-open-source-edr-guide/)
- 회사: 오픈소스컨설팅
- 본문 요약: 상용 EDR을 오픈소스로 대체할 수 있는지에 대한 문의에서 출발해, OSSEC에서 갈라져 나온 XDR·SIEM 통합 플랫폼 Wazuh를 소개합니다. Agent(로그 수집·FIM·SCA·인벤토리, Windows/Linux/macOS), Manager(디코더·룰 기반 분석과 대응 총괄), Indexer(OpenSearch 기반 저장), Dashboard 구조와 로그 상관 분석, 파일 무결성 감시, 악성코드 탐지(rootcheck·VirusTotal·YARA·CDB), CIS 기반 SCA, 취약점 탐지 기능을 정리했습니다.
- 주목할 point: OSSEC가 탐지에서 끝났던 한계를 Active Response(firewall-drop으로 iptables/Windows 방화벽 IP 차단, VirusTotal 판정 파일 자동 삭제 등)로 보완한 점, 대시보드가 Endpoint Security·Threat Intelligence(MITRE ATT&CK 매핑)·Security Operations(PCI DSS·GDPR 등 컴플라이언스)·Cloud Security(Docker·AWS·GCP·Azure·GitHub·Office 365) 네 영역으로 구성된다는 점을 설명합니다.
- keyword: #Wazuh #EDR #XDR #SIEM #OSSEC #오픈소스보안

## [[데이터센터 입문 시리즈] 데이터센터 전력은 어떻게 끌어올까? 발전소에서 서버까지](https://library.gabia.com/contents/infrahosting/16140/)
- 회사: 가비아
- 본문 요약: 데이터센터 전력이 송전망 → 변전소 → 수전 → 변전 설비 → 배전의 다섯 곳을 거쳐 서버에 닿는 과정을 도로에 빗대 설명합니다. 한전 기본공급약관상 계약전력 1만kW 이하는 22.9kV 이하 배전선, 1만~40만kW는 154kV 송전선 공급이 기본이며(4만kW 이하는 조건부 22.9kV 가능), 154kV로 받는 데이터센터는 전압을 낮추는 수변전 설비를 부지 안에 직접 갖춰야 합니다.
- 주목할 point: 예비 선을 같은 변전소에서 받느냐 다른 변전소에서 받느냐(이중 수전)에 따라 평소 비용과 정전 대비 수준이 달라지고, 154kV 이상 수전 사업자에게는 예비 선 공급이 원칙이며, 배전 단에서는 Uptime Institute 기준에 따라 이중 전기 경로와 UPS·발전기를 둔다는 점을 약관 조항 출처와 함께 정리했습니다. 'OO MW급' 뉴스로 연결 전압을 가늠하는 법도 제시합니다.
- keyword: #데이터센터 #전력 #수변전 #이중수전 #154kV #인프라
