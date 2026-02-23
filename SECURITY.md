# Security Policy

## Reporting a Vulnerability

**중요한 보안 취약점은 공개 이슈로 보고하지 마세요.**

민감한 취약점은 GitHub의 **Private Vulnerability Reporting** 기능을 사용해주세요:

1. 해당 리포의 Security 탭으로 이동
2. "Report a vulnerability" 클릭
3. 취약점 내용을 비공개로 제출

또는 org 차원 보고:
- [ZeronimoOS Security Advisories](https://github.com/zeronimoOS/.github/security/advisories/new)

응답 시간: 영업일 기준 3일 이내

## Supported Versions

| 버전 | 지원 여부 |
|------|----------|
| latest | ✅ 지원 |
| 이전 버전 | ❌ 미지원 |

## Scope

보안 리포트 대상:
- 인증/인가 취약점
- API 보안 이슈
- 의존성 취약점 (CVE)
- 하드코딩된 시크릿/키 노출
- 네트워크 경로 보안 이슈

범위 외 (버그 리포트로 제출):
- 기능 버그, UI 오류, 성능 문제

## Disclosure Policy

- 취약점 확인 후 패치 개발
- 패치 배포 후 90일 이내 공개 공시 (조율 가능)
- 기여자는 CHANGELOG의 Security 섹션에 크레딧 표기

---

## Bitcoin Node 특화 보안 가이드

### 개발자 필수 규칙

- Bitcoin RPC 자격증명(`rpcuser`, `rpcpassword`)을 코드에 하드코딩 금지
- `.env` 파일은 절대 커밋 금지 (`.gitignore` 확인)
- 개인키/시드 처리 코드에 AI 직접 관여 금지
- API 엔드포인트에 Bitcoin RPC를 직접 노출 금지 (반드시 Salon API를 통해서만)

### 의존성 취약점 처리

1. CVE 발견 시: **Private Vulnerability Report** 제출 (GitHub Security 탭)
2. 의존성 업그레이드 PR 제출 시 커밋 타입 `security` 사용
3. `bandit` MEDIUM 이상 경고는 `# nosec B###` + 사유 주석 필수

### 보안 심각도 기준

| 심각도 | 대응 시간 | 예시 |
|--------|---------|------|
| CRITICAL | 24시간 이내 | RPC 자격증명 노출, 인증 우회 |
| HIGH | 72시간 이내 | CSRF 미검증, 헤더 스푸핑 |
| MEDIUM | 7일 이내 | 정보 노출, 입력 미검증 |
| LOW | 다음 릴리스 | 코드 품질, 로깅 개선 |
