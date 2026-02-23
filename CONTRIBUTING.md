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

---

## 7. 로컬 개발 환경 설정

### 사전 요구사항
- Python 3.11+
- [uv](https://docs.astral.sh/uv/) 패키지 매니저 (`curl -LsSf https://astral.sh/uv/install.sh | sh`)
- Docker (컨테이너 테스트용)

### 코드 품질 체크 (PR 전 필수)

```bash
uvx ruff check .           # 린트
uvx ruff format --check .  # 포맷
uv run mypy .              # 타입 체크
uvx bandit -r . -ll        # 보안 스캔 (MEDIUM 이상)
uv run pytest tests/ -m "not integration and not slow"  # 단위 테스트
```

---

## 8. 아키텍처 규칙

### DI 패턴 (Salon FastAPI 라우터 필수)

모든 Salon FastAPI 라우터는 전역 인스턴스 직접 접근 금지. 반드시 `Depends()`로 주입:

```python
# ❌ 금지 — 전역 인스턴스 직접 접근
bitcoin_client = BitcoinClient()  # 전역 생성 금지

@router.get("/info")
async def get_info():
    return bitcoin_client.get_info()  # 직접 접근 금지


# ✅ 올바른 패턴 — Depends() 의존성 주입
@router.get("/info")
async def get_info(bitcoin: BitcoinClient = Depends(get_bitcoin_client)):
    return bitcoin.get_info()
```

### 네이밍 규칙

| 컨텍스트 | 규칙 | 예시 |
|---------|------|------|
| 소프트웨어/서비스 | Zeronimo | zeronimo-os, zeronimo-ui |
| 하드웨어/기기 | Nodin | nodin.local, Nodin Pro |
| 금지 식별자 | `bitcoin-core-app` | ❌ 절대 사용 금지 |
| 금지 하드코딩 경로 | `/opt/zeronimo/` | ❌ 환경변수로 대체 |

### PyQt5 ARM64 주의사항 (zeronimo-ui)

ODROID ARM64에서 `pyqtSignal` 3개 이상 파라미터 조합이 QML 연동 시 SEGV 유발:

```python
# ❌ SEGV 유발 — 3개 이상 파라미터
status_changed = pyqtSignal(str, int, str)

# ✅ 올바른 패턴 — QVariant + dict
from PyQt5.QtCore import QVariant
status_changed = pyqtSignal(QVariant)
# 호출: self.status_changed.emit({"status": s, "code": n, "msg": m})
```

---

## 9. PR 체크리스트

PR 생성 전 반드시 확인:

- [ ] `uvx ruff check .` 통과
- [ ] `uvx ruff format --check .` 통과
- [ ] `uv run mypy .` 통과 (또는 `# type: ignore` 사유 주석 명시)
- [ ] 새 기능: 테스트 파일 추가 (`tests/test_*.py`)
- [ ] FastAPI 라우터: DI 패턴 준수 (`Depends()` 사용)
- [ ] 네이밍 규칙 준수 (Nodin/Zeronimo 구분, 금지 식별자 없음)
- [ ] CI 전체 통과 확인 (GitHub Actions 탭)
- [ ] `bandit` MEDIUM 이상 경고 시 `# nosec B###` + 사유 주석 필수
