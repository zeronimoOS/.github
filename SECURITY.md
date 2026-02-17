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
