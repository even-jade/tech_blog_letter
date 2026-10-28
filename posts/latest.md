<!-- 이 파일은 posts/2026-10-28.md의 사본입니다. 자동 생성됨. -->
# 2026-10-28 기술 블로그 모음

## [Amazon MSK Express Broker에서 Kafka 트랜잭션 워크로드를 최적화하는 방법](https://aws.amazon.com/ko/blogs/tech/optimizing-kafka-transactional-workloads-on-msk-express-broker/)
- 회사: AWS
- 본문 요약: MSK Express 브로커에서 Kafka 트랜잭션을 쓸 때 네트워크 기준선만으로 사이징하면 맞지 않는 이유를 분석했습니다. 3대 클러스터에서 10건 묶음 트랜잭션이 네트워크 기준선의 64%(120.5 MB/s)에서 멈췄고 이때 브로커 CPU는 44%였습니다. 병목은 네트워크, 코디네이터 커밋 처리량, 클라이언트 한도 중 하나입니다.
- 주목할 point: 프로듀서를 두 배로 늘려도 처리량이 같다면 코디네이터 한도가 원인입니다. 묶음 크기 확대 → 프로듀서 수 최적화 → 클러스터 확장 순으로 대응하고, 초기 용량은 세 한도 중 최소값의 약 80%로 잡으며 커밋 지연과 초당 커밋 수를 직접 계측하라고 권합니다.
- keyword: #AWS #Kafka #MSK #트랜잭션

## [채팅으로 디자인하는 AI, 실제로 쓸까? — A/B 테스트와 사용자 행동 분석기](https://medium.com/miridih/%EC%B1%84%ED%8C%85%EC%9C%BC%EB%A1%9C-%EB%94%94%EC%9E%90%EC%9D%B8%ED%95%98%EB%8A%94-ai-%EC%8B%A4%EC%A0%9C%EB%A1%9C-%EC%93%B8%EA%B9%8C-a-b-%ED%85%8C%EC%8A%A4%ED%8A%B8%EC%99%80-%EC%82%AC%EC%9A%A9%EC%9E%90-%ED%96%89%EB%8F%99-%EB%B6%84%EC%84%9D%EA%B8%B0-4eeac2fd985e?source=rss----79ed61a9dcb1---4)
- 회사: 미리디
- 본문 요약: AI 디자이너 MVP에 대해 A/B 테스트와 사용자 발화 분석을 진행해 이탈 원인을 기능 미지원과 응답 지연으로 구분했습니다. 도구별 우선순위와 캔버스 맥락 활용 가설을 도출했습니다.
- 주목할 point: 이탈 원인을 정성(발화) 분석으로 분류해 응답시간 개선과 제품 방향 논의에 직접 반영했습니다. 원문 본문은 직접 확인하지 못해 velopers.kr 요약 기준으로 정리했습니다.
- keyword: #LLM #AI에이전트 #A/B테스트 #사용자행동분석

## [팀이 신뢰할 수 있는 AI 분석 환경 만들기: 추천팀의 컨텍스트 설계](https://tech.kakao.com/posts/844)
- 회사: 카카오
- 본문 요약: 추천팀이 AI 에이전트가 지침 문서를 바탕으로 SQL을 작성하고 Hadoop에서 분석하도록 구성한 사례입니다. 로그 접근 방법과 분석 기준을 컨텍스트로 설계해 신뢰할 수 있는 분석 환경을 만들고자 했습니다.
- 주목할 point: 에이전트 성능보다 팀이 결과를 믿을 수 있게 하는 컨텍스트(지침·기준) 설계에 초점을 둡니다. 원문 본문이 페이지 조회에서 확인되지 않아 velopers.kr 요약 기준으로 정리했습니다.
- keyword: #AI에이전트 #SQL #Hadoop #컨텍스트설계

## [프론트엔드 시점에서 정리한 SSE 도입과 메시지 유실 해결 과정](https://www.nextree.io/peuronteuendeu-sijeomeseo-jeongrihan-sse-doibgwa-mesiji-yusil-haegyeol-gwajeong/)
- 회사: 넥스트리
- 본문 요약: AI 챗봇 SSE에서 완료 메시지가 오지 않아 5분 뒤 heartbeat 타임아웃으로 연결이 끊기던 문제를 다뤘습니다. 원인은 AI 처리가 SSE 연결보다 먼저 끝나면 채널이 없어 완료 메시지가 로그 없이 버려지는 경쟁 조건이었습니다. 작업 등록 시 채널을 미리 만들고 채널 삭제를 구독 완료 시점으로 옮겨 해결했습니다.
- 주목할 point: API 도구로 같은 요청을 직접 보내 프론트엔드 문제를 먼저 배제한 것이 원인 범위를 좁히는 데 효과적이었습니다.
- keyword: #SSE #React #경쟁조건 #챗봇

## [성능 테스트 결과를 보고 N+1을 걷어내다](https://www.nextree.io/seongneung-teseuteu-gyeolgwareul-bogo-n-1eul-geodeonaeda/)
- 회사: 넥스트리
- 본문 요약: 약 270만 건·110 req/s 부하 테스트에서 평균 80ms, p95 331ms였고 공통으로 쓰이는 '내 지원 목록 조회'가 평균 345ms로 가장 느렸습니다. 반복되던 건수·지원서 조회를 group by와 IN 쿼리로 묶고, 응답에 필요한 정보를 포함해 추가 호출을 없앴으며, 큰 JSON 컬럼을 제외한 요약 조회와 limit+1 페이지 판단을 도입했습니다.
- 주목할 point: 재측정이 로컬 환경·다른 시나리오라 직접 비교가 어렵고 개선 배수를 단정할 수 없다고 스스로 밝힌 점이 솔직합니다.
- keyword: #JPA #N+1 #성능테스트 #쿼리최적화

## [엔지니어 1명이 레포 170여 개를 pnpm 11로](https://tech.channel.io/kr/articles/db0bc143)
- 회사: 채널톡
- 본문 요약: 2026년 8월 npm 웜 사태 이후 설치 스크립트를 기본 차단하는 pnpm 11로 JS·TS 레포 171개를 전환했습니다. 반복 작업은 검증 하네스를 붙인 AI가 맡았고, 설치 버전·실행 스크립트·빌드 산출물 해시·lint/test 결과를 층별로 비교했습니다.
- 주목할 point: 실행 AI와 채점 AI를 분리하고 사람은 방향 결정과 리뷰에 집중했습니다. 7주간 234개 PR 중 10월 20일 기준 130개가 머지됐습니다.
- keyword: #pnpm #npm #보안 #AI자동화

## [Amazon Quick으로 내 업무와 관련된 Slack 이슈만 모아보기](https://library.gabia.com/contents/15917/)
- 회사: 가비아
- 본문 요약: Slack 세 채널의 최근 24시간 글과 스레드 댓글을 읽기 전용으로 수집하고, 담당 고객사·지원 범위·작업 이력 문서를 기준으로 판단하는 Agent를 만들었습니다. 이를 매일 오전 7시(KST) Routine으로 등록해 Feed에 우선순위·근거·조치를 게시합니다.
- 주목할 point: 스레드 댓글까지 수집해야 진행 상황을 놓치지 않고, 업무 관련도와 우선순위를 별도 항목으로 판단해야 한다는 점이 핵심입니다.
- keyword: #AmazonQuick #Slack #AI에이전트 #업무자동화

## [AI가 97% 확신한다면, 서버를 격리해도 될까?](https://blog.kyobodts.co.kr/2026/10/28/ai%ea%b0%80-97-%ed%99%95%ec%8b%a0%ed%95%9c%eb%8b%a4%eb%a9%b4-%ec%84%9c%eb%b2%84%eb%a5%bc-%ea%b2%a9%eb%a6%ac%ed%95%b4%eb%8f%84-%eb%90%a0%ea%b9%8c/)
- 회사: 교보DTS
- 본문 요약: AI가 내놓는 확률은 실행 권한이 아니라 판단 신호로 다뤄야 한다고 설명합니다. AWS 환경에서 검증, 정책 게이트, 사람 승인, 감사 기록을 분리하는 설계를 제안합니다. (원문 본문은 직접 확인하지 못하고 velopers.kr 요약 기준으로 정리했습니다.)
- 주목할 point: 자동 대응에서 AI 판단과 실행 권한을 분리하는 거버넌스 구조가 포인트입니다.
- keyword: #AWS #SecurityHub #AI보안 #자동대응

## [RFP 작성 에이전트 — 아직도 작년 RFP 복사해서 고쳐 쓰고 계신가요?](https://medium.com/@fasoo.marcom/rfp-%EC%9E%91%EC%84%B1-%EC%97%90%EC%9D%B4%EC%A0%84%ED%8A%B8-%EC%95%84%EC%A7%81%EB%8F%84-%EC%9E%91%EB%85%84-rfp-%EB%B3%B5%EC%82%AC%ED%95%B4%EC%84%9C-%EA%B3%A0%EC%B3%90-%EC%93%B0%EA%B3%A0-%EA%B3%84%EC%8B%A0%EA%B0%80%EC%9A%94-96efdbb298c3?source=rss-faeb0df33c15------2)
- 회사: 파수 AI
- 본문 요약: AI 기반 제안서 평가에서는 명확하고 빠짐없는 RFP가 공정한 평가의 기준이 된다는 관점에서, 조직 내부 발주 자산을 활용해 초안을 만들고 누락·모호성을 점검하는 RFP 작성 에이전트를 소개합니다. (원문 본문은 직접 확인하지 못하고 velopers.kr 요약 기준입니다.)
- 주목할 point: 과거 RFP 복사·수정 관행 대신 사내 자산 기반 생성과 누락·모호성 점검을 결합했습니다.
- keyword: #RFP #AI에이전트 #문서자동화

## [[보안] AI 해킹의 현실화 | 기업이 점검해야 할 5가지 보안 과제](https://blog.naver.com/n_cloudplatform/224456639136?fromRss=true&trackingCode=rss)
- 회사: 네이버 클라우드 플랫폼
- 본문 요약: AI 기반 자동화 공격과 침투 테스트 도구 악용 가능성에 따른 보안 위협을 짚고, 기업이 Zero Trust 관점에서 클라우드 보안 과제 5가지를 점검하도록 안내합니다. (원문 본문은 직접 확인하지 못하고 velopers.kr 요약 기준입니다.)
- 주목할 point: 공격 자동화 시대에 Zero Trust 기반 점검 체크리스트로 활용할 수 있습니다.
- keyword: #보안 #cloud #ZeroTrust #AI해킹

## [[데모데이] 2026 네이버클라우드 그린하우스: MARKET CONNECT](https://blog.naver.com/n_cloudplatform/224456509803?fromRss=true&trackingCode=rss)
- 회사: 네이버 클라우드 플랫폼
- 본문 요약: 그린하우스 시장 검증 캠페인에 참여한 6개 스타트업의 데모데이를 소개합니다. 시장 반응, 시행착오, 리스크와 향후 사업 전략을 공유합니다. (원문 본문은 직접 확인하지 못하고 velopers.kr 요약 기준입니다.)
- 주목할 point: 기술 글이라기보다 스타트업 시장 검증 사례 소개 성격입니다.
- keyword: #데모데이 #스타트업 #시장검증 #네이버클라우드

## [케클s피드 10월호｜기술 경쟁력, 보이지 않는 곳에서 결정된다](https://tech.ktcloud.com/entry/202610-ktcloud-newsletter)
- 회사: KT 클라우드
- 본문 요약: AI 데이터센터의 GPU·네트워크·전력·냉각 인프라와 운영 기술을 소개하고, DR, AIOps, BIM 기반으로 서비스 연속성과 구축·운영 효율을 높이는 방안을 다룹니다. (원문 본문은 직접 확인하지 못하고 velopers.kr 요약 기준입니다.)
- 주목할 point: AI 데이터센터 운영에서 인프라와 운영 자동화가 경쟁력이 된다는 뉴스레터입니다.
- keyword: #데이터센터 #GPU #AIOps #DR

## [[케클러 인터뷰 시리즈] #6 - 백업만으로는 부족하다, 공공 DR의 새로운 기준](https://tech.ktcloud.com/entry/2026-10-ktcloud-gov-DR)
- 회사: KT 클라우드
- 본문 요약: 공공 DR을 데이터 백업이 아닌 서비스 전체의 복구 역량으로 설명하고, 등급별 아키텍처와 훈련, AI 워크로드 복구 전략을 다룹니다. (원문 본문은 직접 확인하지 못하고 velopers.kr 요약 기준입니다.)
- 주목할 point: DR을 백업이 아닌 서비스 단위 복구 역량으로 정의하는 관점이 핵심입니다.
- keyword: #DR #공공클라우드 #재해복구 #AI워크로드
