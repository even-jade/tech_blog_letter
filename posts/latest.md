<!-- 이 파일은 posts/2026-10-10.md의 사본입니다. 자동 생성됨. -->
# 2026-10-10 기술 블로그 모음

## [사내 지식으로 Agentic RAG 만들기 (3/3) : 관측 가능한 RAG, 운영되는 도구로](https://techblog.gccompany.co.kr/%EC%82%AC%EB%82%B4-%EC%A7%80%EC%8B%9D%EC%9C%BC%EB%A1%9C-agentic-rag-%EB%A7%8C%EB%93%A4%EA%B8%B0-3-3-%EA%B4%80%EC%B8%A1-%EA%B0%80%EB%8A%A5%ED%95%9C-rag-%EC%9A%B4%EC%98%81%EB%90%98%EB%8A%94-%EB%8F%84%EA%B5%AC%EB%A1%9C-dbac813832db)
- 회사: 여기어때
- 본문 요약: Langfuse trace로 검색·프롬프트 조립·생성 단계의 입력·출력·토큰·비용을 추적하고, Recall@5·Hit Rate·MRR 검색 지표와 LLM-as-a-judge 정확도 평가를 결합한 이중 평가 파이프라인을 구축했습니다. FastMCP 기반 원격 MCP 서버와 서버 instructions를 다듬어 도구 활용 정확도를 높이고 운영 환경에 제공했습니다.
- 주목할 point: 검색 오류와 생성 오류를 분리해 관측하고, 모든 변경 전 3회 이상 실험으로 정확도·지연시간·토큰·비용을 비교하는 운영 방식.
- keyword: #AI #RAG #Langfuse #MCP #FastMCP

## [사내 지식으로 Agentic RAG 만들기 (2/3) : 검색을 얹기, LightRAG와 Navigator](https://techblog.gccompany.co.kr/%EC%82%AC%EB%82%B4-%EC%A7%80%EC%8B%9D%EC%9C%BC%EB%A1%9C-agentic-rag-%EB%A7%8C%EB%93%A4%EA%B8%B0-2-3-%EA%B2%80%EC%83%89%EC%9D%84-%EC%96%B9%EA%B8%B0-lightrag%EC%99%80-navigator-9f3119060242)
- 회사: 여기어때
- 본문 요약: 벡터 검색만으로는 분산된 문서 조각 간 관계와 문서의 계층적 위치를 판별하기 어려워, LightRAG의 Entity·Relation 지식 그래프와 Neo4j 기반 Navigator(Confluence 트리·Jira 계층 보존)를 결합했습니다. 갱신은 삭제·완료 확인·재업로드로 처리하고, 사내 문서용 Entity type·한영 인물 표기 규칙·도메인 few-shot, 헤딩·문단 기반 청킹으로 정확도와 운영 효율을 높였습니다.
- 주목할 point: 의미 기반 후보 축소 후 계층 탐색으로 문서 위치와 주변 맥락을 확인하는 리트리버 분업, 실패 인덱싱 알림·재처리 자동화.
- keyword: #AI #RAG #LightRAG #Neo4j #GraphRAG

## [쉐도잉 검증 개선기](https://techblog.gccompany.co.kr/%EC%89%90%EB%8F%84%EC%9E%89-%EA%B2%80%EC%A6%9D-%EA%B0%9C%EC%84%A0%EA%B8%B0-cef1ddc8318d)
- 회사: 여기어때
- 본문 요약: 레거시 MongoDB 기반 응답을 원천 API 직접 호출로 전환하며 가격·재고 응답 동등성을 검증하기 위해, 비동기 실행·샘플링·키 기반 비교·MATCH/DIFF/ERROR 보고를 공통 ShadowRunner 라이브러리로 통합했습니다. 실제 URI·쿼리·선별 헤더를 기록해 불일치 요청을 재현하고, Prometheus 메트릭과 Loki 로그를 Grafana 대시보드로 연결했습니다.
- 주목할 point: 메트릭 라벨 카디널리티 방지(필드 경로 정규화·상한·overflow 집계), 리포터 실패가 사용자 응답에 영향 없는 구조, 비교 불가 요청은 일치율 분모에서 제외하고 ERROR는 별도 관찰.
- keyword: #백엔드 #쉐도잉 #Grafana #Prometheus #Loki

## [시킬 때마다 다른 결과를 내는 AI에게 도구를 쥐여 주었습니다 — AI가 쓰는 ERD 도구 제작기](https://techblog.gccompany.co.kr/%EC%8B%9C%ED%82%AC-%EB%95%8C%EB%A7%88%EB%8B%A4-%EB%8B%A4%EB%A5%B8-%EA%B2%B0%EA%B3%BC%EB%A5%BC-%EB%82%B4%EB%8A%94-ai%EC%97%90%EA%B2%8C-%EB%8F%84%EA%B5%AC%EB%A5%BC-%EC%A5%90%EC%97%AC-%EC%A3%BC%EC%97%88%EC%8A%B5%EB%8B%88%EB%8B%A4-ai%EA%B0%80-%EC%93%B0%EB%8A%94-erd-%EB%8F%84%EA%B5%AC-%EC%A0%9C%EC%9E%91%EA%B8%B0-f97eefa26354)
- 회사: 여기어때
- 본문 요약: 비결정적인 AI가 Mermaid·HTML로 ERD를 만들 때의 배치 불안정 문제를 해결하기 위해, AI는 테이블·관계 설계를, MCP 기반 도구는 영문명·타입·배치 결정을 맡도록 역할을 분리했습니다. 13개 MCP 도구(조회·수정·정렬·내보내기·되돌리기)로 자동 정렬, 직각 관계선, 용어사전·도메인 규칙 기반의 결정적 렌더링을 구현했습니다.
- 주목할 point: 도구 설명에 사용·미사용 조건과 재질문·거절 기준을 명시하고 변경 전후 값을 응답에 포함해, Haiku·Sonnet·Opus 반복 측정으로 실패 호출을 61회에서 3회로 줄임.
- keyword: #AI #MCP #ERD #도구설계

## [새로운 팀에 기여하기, 그리고 기여의 확장 (feat. 전시개발팀 옵저버빌리티 향상 시키기)](https://techblog.gccompany.co.kr/%EC%83%88%EB%A1%9C%EC%9A%B4-%ED%8C%80%EC%97%90-%EA%B8%B0%EC%97%AC%ED%95%98%EA%B8%B0-%EA%B7%B8%EB%A6%AC%EA%B3%A0-%EA%B8%B0%EC%97%AC%EC%9D%98-%ED%99%95%EC%9E%A5-feat-%EC%A0%84%EC%8B%9C%EA%B0%9C%EB%B0%9C%ED%8C%80-%EC%98%B5%EC%A0%80%EB%B2%84%EB%B9%8C%EB%A6%AC%ED%8B%B0-%ED%96%A5%EC%83%81-%EC%8B%9C%ED%82%A4%EA%B8%B0-c39614694661)
- 회사: 여기어때
- 본문 요약: 게이트웨이 이후 대량 트래픽을 처리하는 전시 서비스의 장애 대응 흐름에 맞춰 OpenTelemetry·Grafana 기반으로 Metrics·Traces·Logs를 연계한 관측 가능성 대시보드를 구축했습니다. 기존 파이프라인을 활용하고 AI 에이전트로 반복 작업을 줄이며 팀 단위 개선으로 확장했습니다.
- 주목할 point: 기존 Pinpoint 중심 환경에서 요청·성공·실패·TPS, Incoming/Outgoing, 레이턴시·에러별 지표로 문제 요점을 직관적으로 확인하게 한 점.
- keyword: #데브옵스 #OpenTelemetry #Grafana #옵저버빌리티

## [AI 시대 당신의 팀은 안녕하신가요](https://techblog.gccompany.co.kr/ai-%EC%8B%9C%EB%8C%80-%EB%8B%B9%EC%8B%A0%EC%9D%98-%ED%8C%80-%EC%A1%B0%EC%A7%81%EC%9D%80-%EC%95%88%EB%85%95%ED%95%98%EC%8B%A0%EA%B0%80%EC%9A%94-c59f982d5add)
- 회사: 여기어때
- 본문 요약: AI 생성 코드가 늘면서 결과물만으로는 의도·전제·선택 근거를 알기 어렵다는 문제를 짚고, 스킬·서브에이전트·가이드·히스토리를 공유 저장소에 모은 AI 워크스페이스를 소개했습니다. 작업 중 판단을 즉시 히스토리에 잠정 기록하고 팀 리뷰를 거쳐 검증된 내용만 가이드로 승격합니다.
- 주목할 point: 기계 검증과 사람 중심의 맥락 리뷰를 분리해 인지 부채·의도 부채를 줄이고 AI 협업의 주도권을 유지하려는 접근.
- keyword: #AI #팀협업 #에이전트 #코드리뷰
