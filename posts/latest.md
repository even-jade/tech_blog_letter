<!-- 이 파일은 posts/2026-10-15.md의 사본입니다. 자동 생성됨. -->
# 2026-10-15 기술 블로그 모음

## [ParallelCluster 잘 쓰고 있는데, 왜 AWS PCS인가(1부) — 관리형 Slurm의 가치와 비용 구조](https://aws.amazon.com/ko/blogs/tech/pcs-1/)
- 회사: AWS
- 본문 요약: AWS PCS는 Slurm 컨트롤러 운영(패치·장애 복구·in-place 업그레이드)을 AWS에 맡겨 HPC 클러스터 운영 부담을 줄이는 관리형 서비스입니다. 컨트롤러·큐·accounting DB는 AWS 관리 VPC에, 컴퓨트 노드·AMI·스토리지·네트워크는 고객 VPC에 두며 월 99.9% SLA를 제공합니다. 대신 EC2·스토리지 외에 컨트롤러·노드 관리·선택형 Slurm Accounting 요금이 추가됩니다.
- 주목할 point: 추가 관리 요금은 가동률, 커스터마이징 요구, 중단 손실까지 포함한 TCO로 판단해야 합니다. 상시 가동 환경은 노드 관리비, 저가동 환경은 컨트롤러 고정비 비중이 커지며, 비용 민감도와 세밀한 커스터마이징 요구가 크면 ParallelCluster가 여전히 선택지가 될 수 있습니다.
- keyword: #AWS #PCS #Slurm #HPC #ParallelCluster

## [코드를 모르는 기획자의 Product Engineer 도전 : 준비와 소통으로 서버부터 앱까지](https://techblog.yogiyo.co.kr/%EC%BD%94%EB%93%9C%EB%A5%BC-%EB%AA%A8%EB%A5%B4%EB%8A%94-%EA%B8%B0%ED%9A%8D%EC%9E%90%EC%9D%98-product-engineer-%EB%8F%84%EC%A0%84-%EC%A4%80%EB%B9%84%EC%99%80-%EC%86%8C%ED%86%B5%EC%9C%BC%EB%A1%9C-%EC%84%9C%EB%B2%84%EB%B6%80%ED%84%B0-%EC%95%B1%EA%B9%8C%EC%A7%80-f6c1db423de9)
- 회사: 요기요
- 본문 요약: 코드를 읽지 못하는 기획자가 Claude Code와 마크다운 설계 계획서를 활용해 주문추적화면 지도 마커를 광고 지면으로 쓰는 기능을 서버·API·어드민·Android·iOS까지 직접 출시한 경험을 공유합니다. 영향 범위와 기존 마커 동작을 AI로 분석해 계획서에 담고, 영역별 담당자의 설계 리뷰와 코드 리뷰, QA를 병행했습니다. 첫 외부 광고에서 목표 대비 노출수·클릭수 200% 이상을 달성했습니다.
- 주목할 point: 사소한 스펙 변경도 계획서에 즉시 반영해 AI와 협업자의 공통 맥락을 유지하고, AI 응답은 재질문과 기능 단위 테스트로 검증하는 것이 핵심입니다. 비개발자 PE는 도메인 정책을 잘 아는 작은 서비스부터 시작하고, 오류 로그를 해석할 수 있는 환경(Datadog 등)을 갖추는 것이 중요합니다.
- keyword: #ProductEngineer #ClaudeCode #AI협업 #기획자 #설계계획서

## [AI 코딩 시대, DDD가 더 필요해진 이유](https://blog.banksalad.com/tech/banksalad-ddd-in-ai-era/)
- 회사: 뱅크샐러드
- 본문 요약: Go 마이크로서비스가 커지며 핸들러에 로직이 몰려 사실상 모놀리식화된 신용점수 서비스를 DDD-lite와 Clean Architecture로 리팩토링한 과정을 소개합니다. KCB 데이터 출처 기준 폴더 분리가 잘못된 바운디드 컨텍스트를 만든 문제를 인식하고, 신용점수·신용변동·신용유저 등 비즈니스 개념 단위 컨텍스트와 handler·application·domain·infrastructure 4계층(포트/어댑터 분리)으로 재구성했습니다. 435개 PR로 전체를 정비했습니다.
- 주목할 point: 명확한 경계와 계층 컨벤션은 사람뿐 아니라 AI 코딩 에이전트의 탐색·리뷰 범위와 읽는 코드량을 줄여 결과물의 일관성을 높입니다. AGENTS.md 규칙으로 컨벤션을 AI에게 명시하는 점도 참고할 만합니다.
- keyword: #DDD #CleanArchitecture #Go #AI코딩 #리팩토링

## [토스뱅크가 패키지를 관리하는 방식 #1: 패키지를 ESM으로만 제공하기로 했어요](https://toss.tech/article/package-management-1)
- 회사: 토스
- 본문 요약: ESM·CJS 이중 배포 시 import와 require()가 서로 다른 구현 파일을 로드해 React 컨텍스트·캐시 같은 공유 상태가 이중화되고, TypeScript 설정에 따라 CJS 경로를 선택하면 타입 파일이 없어 외부 타입이 any로 전파될 수 있는 문제를 분석했습니다. Node.js 22.12.0의 require(esm) 지원을 근거로 사내 패키지를 ESM-only로 전환했습니다.
- 주목할 point: ESM-only 전환으로 이중 실행 코드와 타입 연결 관리 부담이 줄고 디버깅 복잡도가 감소합니다. 단, require(esm)을 쓰려면 해당 ESM과 의존 모듈에 최상위 await가 없어야 합니다.
- keyword: #ESM #CJS #Nodejs #TypeScript #패키지관리

## [채널톡의 FDE는 어떤 일을 할까?](https://tech.channel.io/kr/articles/850fcc83)
- 회사: 채널톡
- 본문 요약: FDE(Forward Deployed Engineer)가 고객 요구를 PoC로 빠르게 검증하고 제품화 근거로 전환하는 과정을 소개합니다. 웹 이탈 방문자의 상담 전환, 수천~수만 건의 전화 발신·결과 분석 같은 콜 캠페인 요구에서 응답이 불확실한 요청의 자동 재시도 대신 중복 발신 방지를 우선하고, SQS 대신 PostgreSQL 작업 상태와 주기적 실행기로 초기 운영 복잡도를 줄였습니다.
- 주목할 point: CPS뿐 아니라 최대 통화 시간에 따른 회선 점유를 고려해 발신 속도와 예약 물량을 산정하고, 원본 발신 대상과 통화 기록을 대조해 미확인 대상을 점검합니다. 고객별 PoC → 반복 사용 검증 → 제품팀의 공통 기능 제품화로 이어지는 흐름이 참고할 만합니다.
- keyword: #FDE #PoC #콜캠페인 #PostgreSQL #제품화

## [모던 백엔드- 문법 & 성능 개선(1)](https://www.nextree.io/modeon-baegendeu-munbeob-seongneung-gaeseon-1/)
- 회사: 넥스트리
- 본문 요약: Java 25의 유연한 생성자 본문(super()/this() 호출 전 유효성 검사와 필드 사전 초기화), 모듈 임포트 선언, switch·instanceof의 기본형 패턴 매칭 확장을 소개하고, Compact Object Headers 기반 HotSpot JVM 메모리 최적화를 살펴봅니다.
- 주목할 point: Compact Object Headers는 64비트 객체 헤더를 압축해 힙 사용량을 줄이고 캐시 지역성을 높여, 대규모 트래픽 환경의 JVM 메모리 최적화에 이점이 있습니다. 최신 Java 문법으로 백엔드 코드 생산성 개선을 검토해볼 만합니다.
- keyword: #Java25 #CompactObjectHeaders #HotSpot #패턴매칭 #백엔드

## [모던 백엔드 - 문법 & 성능 개선(2)](https://www.nextree.io/modeon-baegendeu-munbeob-seongneung-gaeseon-2/)
- 회사: 넥스트리
- 본문 요약: Java 25 유연한 생성자 본문의 프롤로그 영역 규칙과 상속 구조에서의 초기화 순서 함정, 컴팩트 객체 헤더 활성화 플래그(-XX:+UseCompactObjectHeaders)와 적용 여부 검증 방법을 다룹니다.
- 주목할 point: 프롤로그에서는 파라미터 검증·예외 발생·로컬 연산은 가능하지만 인스턴스 필드 읽기, 인스턴스 메서드 호출, this 유출은 금지됩니다. 성능 진단 시 기동 시간·웜업과 힙 메모리·GC 부하를 구분하고, 메모리 절감에 따른 GC 빈도·STW 감소를 장기 처리량 관점에서 봐야 합니다.
- keyword: #Java25 #생성자 #JVM #GC #성능개선

## [데이터 쿼리 AI 에이전트 — SQL 몰라도 돼! 사내 데이터 직접 꺼내 쓰는 방법](https://medium.com/@fasoo.marcom/%EB%8D%B0%EC%9D%B4%ED%84%B0-%EC%BF%BC%EB%A6%AC-ai-%EC%97%90%EC%9D%B4%EC%A0%84%ED%8A%B8-sql-%EB%AA%B0%EB%9D%BC%EB%8F%84-%EB%8F%BC-%EC%82%AC%EB%82%B4-%EB%8D%B0%EC%9D%B4%ED%84%B0-%EC%A7%81%EC%A0%91-%EA%BA%BC%EB%82%B4-%EC%93%B0%EB%8A%94-%EB%B0%A9%EB%B2%95-dd5531881acd)
- 회사: 파수 AI
- 본문 요약: 조직의 테이블 구조, 컬럼 의미, 지표 정의서, 쿼리 이력 같은 데이터 맥락을 반영해 자연어 질문을 SQL로 바꿔주는 Data Query ACE를 소개합니다. 현업의 반복 조회 요청으로 인한 데이터팀 병목과 일반적 Text to SQL의 실무 신뢰성 한계를 해결 대상으로 삼습니다.
- 주목할 point: 민감한 스키마와 데이터를 외부 AI 서비스에 올리기 어려운 보안 제약을 Private 환경과 접근 권한 통제로 풀었다는 점이 포인트입니다.
- keyword: #TextToSQL #AI에이전트 #데이터쿼리 #보안 #Private

## [[보안] 달라지는 공공 클라우드 보안 기준｜꼭 확인해야 할 3가지 변화](https://blog.naver.com/n_cloudplatform/224442401297)
- 회사: 네이버 클라우드 플랫폼
- 본문 요약: 국가·공공기관의 클라우드 구축과 민간 서비스 이용에 적용되는 국가 클라우드컴퓨팅 보안 가이드라인 개정안을 소개하며, 정보 등급 분류 기준, 등급별 민간 클라우드 이용 범위, 보안 요건·검증 체계의 변화를 예고합니다.
- 주목할 point: 보유 정보의 등급과 처리 가능한 클라우드 범위를 우선 확인하고, 개정되는 보안 기준과 절차를 바탕으로 공공 클라우드 도입을 검토해야 합니다.
- keyword: #공공클라우드 #클라우드보안 #보안가이드라인 #정보등급 #NCP

## [PaaS란? 서비스형 플랫폼의 개념·구조·과금 방식 정리](https://library.gabia.com/contents/infrahosting/15825/)
- 회사: 가비아
- 본문 요약: PaaS의 책임 경계(제공자는 네트워크·서버·OS·런타임, 사용자는 애플리케이션·데이터 관리)와 코드 저장소/CLI 배포 → CI/CD → 런타임·미들웨어·관리형 DB → 모니터링으로 이어지는 구성, 사용량 기반·플랜 정액제 과금 방식을 정리했습니다.
- 주목할 point: 도입 시 지원 런타임 범위와 버전 종료 정책, 벤더 종속, 보안 책임, 사용량 증가에 따른 확장 비용을 확인해야 합니다. 오토스케일링 최소·최대 인스턴스, 월 예산, 유휴 시간 과금 여부와 데이터 내보내기 가능성도 점검하세요.
- keyword: #PaaS #클라우드 #배포 #과금 #벤더종속
