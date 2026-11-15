<!-- 이 파일은 posts/2026-11-15.md의 사본입니다. 자동 생성됨. -->
# 2026-11-15 기술 블로그 모음

## [AWS Emulator 시작하기 – 계정 없이 AWS 애플리케이션을 로컬에서 테스트하는 방법과 활용 사례](https://aws.amazon.com/ko/blogs/tech/getting-started-with-aws-emulator-local-testing-without-an-aws-account/)
- 회사: AWS
- 본문 요약: 2026년 11월 11일 공개된 AWS Emulator는 AWS API를 로컬 프로세스 하나(기본 127.0.0.1:9297, HTTPS 단일 엔드포인트)로 흉내 내는 빌드·테스트 전용 도구입니다. 실행마다 전용 액세스 키·인증서와 독립 계정(000000000000)을 만들고, 모든 리소스를 메모리에 두며, 미구현 작업은 HTTP 501을 돌려줍니다. 글은 Linux 패키지 설치(서명 검증 포함)와 Docker·AI 코딩 에이전트 skill 경로, 환경 변수 8개로 CLI/SDK를 연결하는 방법, AWS CLI 첫 호출, pytest fixture로 테스트 세션마다 에뮬레이터를 띄우는 통합 테스트 예제를 다룹니다. v1.0.322 기준 서비스 355개 충실도 테스트 통과율은 56.5%였고, 실습에서 오류 응답 7건 중 6건이 실제 AWS와 같았습니다.
- 주목할 point: 연결 변수를 일부만 설정한 채 에뮬레이터가 꺼지면 EC2 인스턴스 프로필 자격 증명으로 실제 계정에 요청이 갈 수 있어, 변수 8개+unset을 모두 지정하고 계정 ID 가드를 두라고 권고합니다. 버킷당 1,000개 초과 객체 거부, Terraform S3 Control 요청 실패, Bedrock Converse 고정 응답 등 문서에 없는 제약을 실측으로 보여 주며, IAM/KMS 정책 검증·복잡한 IaC·부하 테스트는 실제 AWS 스테이징에 남기고 앱 통합 테스트·오류 경로·자격 증명 없는 CI·코딩 에이전트 반복에 쓰라는 기준을 제시합니다.
- keyword: #AWSEmulator #로컬테스트 #통합테스트 #CI #pytest #코딩에이전트
