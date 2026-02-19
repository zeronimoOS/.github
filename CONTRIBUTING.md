# Contributing to ZeronimoOS

ZeronimoOS 프로젝트에 기여해주셔서 감사합니다.
이 문서는 개발 워크플로우와 기여 규칙을 설명합니다.

---

## 1. Guidelines

### 브랜치 전략

- `main` 브랜치에 직접 푸시 금지
- 모든 변경은 feature 브랜치 → PR → merge 흐름
- 브랜치 프리픽스:

| 프리픽스 | 용도 |
|----------|------|
| `feat/` | 새 기능 |
| `fix/` | 버그 수정 |
| `refactor/` | 리팩토링 |
| `docs/` | 문서 수정 |
| `chore/` | 설정/빌드/의존성 |
| `security/` | 보안 수정 |
| `infra/` | 인프라 변경 |

```bash
git checkout -b feat/my-feature
```

### PR 규칙

- 모든 변경은 PR 필수
- PR 템플릿 작성 완료 후 merge
- CI 검사 통과 필수

---

## 2. Commits

[Conventional Commits](https://www.conventionalcommits.org/) 형식 준수:

```
<type>(<scope>): <subject>
```

### 타입

| 타입 | 용도 |
|------|------|
| `feat` | 새 기능 추가 |
| `fix` | 버그 수정 |
| `style` | 코드 포맷/스타일 (기능 변경 없음) |
| `refactor` | 리팩토링 (기능/버그 수정 없음) |
| `chore` | 빌드/설정/의존성 변경 |
| `docs` | 문서 추가/수정 |
| `test` | 테스트 추가/수정 |

### 예시

```bash
feat(api): add OTA rollback endpoint
fix(web): correct sync percentage calculation
chore(infra): update nginx configuration
docs: update README with setup instructions
```

---

## 3. Development Workflow

```bash
# 1. 브랜치 생성
git checkout -b feat/my-feature

# 2. 개발 및 테스트
# (각 리포의 README.md 참조)

# 3. PR 생성
# PR 템플릿에 따라 작성
```

---

## 4. Releases

### 버전 체계

[Semantic Versioning](https://semver.org/) 준수: `MAJOR.MINOR.PATCH`

| 변경 유형 | 버전 올리기 |
|----------|-------------|
| 하위 호환 버그 수정 | PATCH |
| 새 기능 (하위 호환) | MINOR |
| 하위 비호환 변경 | MAJOR |

### 릴리스 노트 형식

```markdown
## v1.2.3 (YYYY-MM-DD)

### Added
- feat: 새 기능 설명

### Fixed
- fix: 버그 수정 설명

### Changed
- refactor: 변경 사항

### Security
- security: 보안 패치
```

---

## 5. Testing

각 리포의 README.md 또는 `CONTRIBUTING.md`에서 테스트 방법을 확인하세요.

공통 원칙:
- 새 기능/버그 수정에는 테스트 추가
- PR merge 전 모든 테스트 통과 필수
- 커버리지 유지

---

## Questions?

- **Issues**: [GitHub Issues](https://github.com/zeronimoOS)
- **Security**: [SECURITY.md](SECURITY.md) 참조

---

## 6. AI-Assisted Development

이 프로젝트는 AI 도구(Claude, Codex 등)를 적극 활용합니다.

### 표기 규칙
- AI 협업 커밋: `Co-Authored-By: Claude <model> <noreply@anthropic.com>` 트레일러 필수
- AI 관련 이슈: `🤖 ai-assisted` 라벨 부여
- 자동 생성 이슈: `📋 automated` 라벨 부여

### AI 사용 범위
- ✅ 코드 생성, 리팩토링, 테스트 작성, 문서화
- ✅ 아키텍처 분석, 디버깅 보조
- ⚠️ 보안 관련 코드는 AI 초안 + 인간 검증 필수
- ❌ 비밀키/시드/인증정보 처리에 AI 직접 관여 금지

### 참고
- [ADR-008: AI-Native Development](https://github.com/zeronimoOS/zeronimo-os/blob/main/docs/architecture/decisions/adr-008-ai-native-development.md)
