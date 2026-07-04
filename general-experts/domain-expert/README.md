# 도메인 전문가 (Domain Expert) — general-experts 팩

> 팀에 아직 없는 **도메인 전문가** 역할을 Agent + Skill 로 메우는 큐레이션 팩입니다.
> DDD 기반 도메인 발굴/모델링에 초점을 둡니다: 요구사항 → 도메인 개념 추출 → 유비쿼터스 언어 →
> 서브도메인 → 바운디드 컨텍스트 → 애그리거트 → 도메인 모델 리뷰.

---

## 1) 역할 개요 — 이 Agent에게 무엇을 위임하는가

많은 팀에 **도메인 전문가 역할이 비어 있습니다.** 이 팩은 그 공백을 대행합니다.

이 Agent에게 위임하는 일:

- **도메인 발굴**: 요구사항/기획 초안에서 도메인 이벤트·커맨드·개념을 추출 (이벤트 스토밍)
- **유비쿼터스 언어 정립**: 핵심 도메인 용어의 정의·동의어·반의어(anti-term)·충돌 해소
- **전략적 설계**: 서브도메인 분류(Core/Supporting/Generic), 바운디드 컨텍스트 경계, 경계 ADR
- **전술적 설계**: 불변식 기반 애그리거트 경계, 애그리거트 루트/엔티티/VO, 트랜잭션 경계, 리포지토리 초안
- **도메인 모델 리뷰**: 용어 일관성·경계 정합성·불변식 표현률·이벤트 완전성·결합도 스코어링 + 되돌리기 트리거

> 경계 구분: `algo-experts/`는 (앞으로 정해질) 도메인 특화 커스텀 공간으로, **제품-도메인 아키텍트**가
> "무엇을 만들 것인가"(제품 뼈대·MVP·범위)를 다룹니다.
> 이 도메인 전문가는 그 산출물을 입력으로 받아 **"이 도메인을 어떻게 모델링할 것인가"**(경계·불변식·애그리거트)를 책임집니다. 상보 관계입니다.

무엇을 **위임하지 않는가**: 영속성 엔티티/테이블/ERD 작성, API 설계, 코드 생성. 이 Agent는 도메인 형태가
명확해진 **뒤** 구현 담당 개발자·개발 에이전트에게 구현을 넘깁니다.

---

## 2) 추천 구성 표

| 종류 | 이름 | 소스 (owner/repo) | ⭐ | 라이선스 | 런타임 | 벤더링 |
|---|---|---|---:|---|---|---|
| Skill | `ddd-discover` | ForceInjection/domain-driven-design-skills | 21 | Apache-2.0 | Claude Code | ✅ `skills/ddd-discover/SKILL.md` |
| Skill | `ddd-subdomains` | ForceInjection/domain-driven-design-skills | 21 | Apache-2.0 | Claude Code | ✅ `skills/ddd-subdomains/SKILL.md` |
| Skill | `ddd-contexts` | ForceInjection/domain-driven-design-skills | 21 | Apache-2.0 | Claude Code | ✅ `skills/ddd-contexts/SKILL.md` |
| Skill | `ddd-aggregates` | ForceInjection/domain-driven-design-skills | 21 | Apache-2.0 | Claude Code | ✅ `skills/ddd-aggregates/SKILL.md` |
| Skill | `ddd-model-review` | ForceInjection/domain-driven-design-skills | 21 | Apache-2.0 | Claude Code | ✅ `skills/ddd-model-review/SKILL.md` |
| Agent | `business-analyst` | VoltAgent/awesome-claude-code-subagents | 22.8k | MIT | Claude Code (subagent) | ✅ `agents/business-analyst.md` |
| Agent | `domain-expert` (맞춤 합성) | — (직접 합성) | — | — | Claude Code (subagent) | 🧩 `agents/domain-expert.agent.md` (SYNTHESIZED) |

> 벤더링한 스킬은 원본 저장소의 **영문판(`SKILL.en.md`)** 바이트를 그대로 가져와 `SKILL.md`로 저장했습니다
> (원본 저장소는 `SKILL.md`=중국어, `SKILL.en.md`=영어 병행. 한국어 팀에는 영어판이 더 범용적이라 판단).
> 각 파일 최상단 출처 헤더(HTML 주석)의 `SOURCE` URL이 실제 fetch 원본입니다.

### 카탈로그 전용 (링크만 — 벤더링 안 함)

| 이름 | 소스 | ⭐ | 라이선스 | 비고 |
|---|---|---:|---|---|
| `agent-business-analyst` | [majiayu000/claude-skill-registry](https://github.com/majiayu000/claude-skill-registry/tree/main/skills/business/agent-business-analyst) | 469 | MIT | 비즈니스 분석 스킬 레지스트리. 필요 시 선택적으로 참고 (직접 벤더링하지 않음) |

### 관련 gstack 슬래시 명령 (벤더링 불필요 — 명령/링크만)

[garrytan/gstack](https://github.com/garrytan/gstack) (MIT, ⭐ 119k) 의 슬래시 명령을 도메인 워크플로에 연계할 수 있습니다:

- `/investigate` — 개념 발굴 보조 → `ddd-discover` 입력 준비
- `/spec` — 도메인 스펙 도출 → `ddd-contexts` / `ddd-aggregates` 산출물을 스펙 문서로 정리
- `/learn` — 도메인 학습/정리

---

## 3) 설치 · 사용

### A. 이 팩을 그대로 사용 (이미 벤더링됨)

이 디렉터리(`general-experts/domain-expert/`)에 스킬·에이전트가 이미 포함되어 있습니다.
Claude Code 프로젝트에서 스킬로 인식시키려면 각 `skills/<name>/SKILL.md`를
프로젝트의 `.claude/skills/`(또는 팀 규칙 경로)로 복사하거나 심볼릭 링크합니다.

```bash
# 예: 프로젝트 .claude/skills 로 링크
mkdir -p .claude/skills .claude/agents
ln -s "$(pwd)/general-experts/domain-expert/skills/"* .claude/skills/
cp general-experts/domain-expert/agents/*.md .claude/agents/
```

### B. 원본 저장소에서 최신본 다시 받기 (선택)

```bash
# DDD 스킬 (Apache-2.0)
gh api "repos/ForceInjection/domain-driven-design-skills/contents/skills/ddd-discover/SKILL.en.md" --jq '.content' | base64 -d
# 또는
curl -sL "https://raw.githubusercontent.com/ForceInjection/domain-driven-design-skills/main/skills/ddd-contexts/SKILL.en.md"

# business-analyst 에이전트 (MIT)
curl -sL "https://raw.githubusercontent.com/VoltAgent/awesome-claude-code-subagents/main/categories/08-business-product/business-analyst.md"
```

### C. 호출 방법

- **스킬 직접 호출**: 대화에서 `@ddd-discover`, `@ddd-contexts` 처럼 언급하고 요구사항/산출물을 붙여넣습니다.
  각 `SKILL.md`의 `## Example` 블록이 호출 템플릿입니다.
- **파이프라인 오케스트레이션**: `agents/domain-expert.agent.md` 서브에이전트를 호출하면
  발굴 → 서브도메인 → 컨텍스트 → 애그리거트 → 리뷰 단계를 대상 도메인 시드와 함께 자동 조율합니다.
- **보조 에이전트**: `agents/business-analyst.md`는 이해관계자 요구사항 정리·프로세스 분석이 필요할 때 도메인 전문가를 보조합니다.

---

## 4) 활용 시나리오

특정 도메인/스택을 가정하지 않는 일반 업무 예시입니다.

- **킥오프 발굴**: 요구사항/기획 초안을 `@ddd-discover`에 넣어 도메인 이벤트·커맨드 흐름을 뽑고, 메인 경로 1개 + 예외 경로 몇 개를 과거형 이벤트로 명명합니다.
- **유비쿼터스 언어 정리**: 사람마다 다르게 쓰는 핵심 용어를 `@ddd-contexts`로 정의하고, 동의어·반의어(anti-term)까지 확정해 경계 ADR로 남깁니다.
- **애그리거트/서브도메인 설계**: `@ddd-subdomains`로 Core/Supporting/Generic을 분류해 투자 우선순위를, `@ddd-aggregates`로 불변식 기반 애그리거트 경계와 트랜잭션 경계를 도출합니다.
- **구현 직전 품질 게이트**: 데이터 모델을 짜기 전에 `@ddd-model-review`로 용어 일관성·경계 정합·불변식 표현률·이벤트 완전성·결합도를 스코어링하고 되돌리기 트리거를 확인합니다.

---

## 5) 라이선스 · 보안 주의

### 벤더링한 항목의 라이선스 (출처 표기 필수 — 각 파일 상단 헤더 참조)

- `skills/ddd-*/SKILL.md` → **ForceInjection/domain-driven-design-skills, Apache-2.0**
  (원본 `SKILL.en.md` 바이트 무변경 + 출처 헤더). Apache-2.0은 저작권 고지·라이선스 사본 유지 의무.
- `agents/business-analyst.md` → **VoltAgent/awesome-claude-code-subagents, MIT** (원본 무변경 + 출처 헤더).
- `agents/domain-expert.agent.md` → **직접 합성(SYNTHESIZED)**. 벤더링 아님. 대상 도메인에 맞춰 작성.

### 벤더 불가 / 링크만

- **majiayu000/claude-skill-registry** (MIT) 는 카탈로그 전용으로 지정되어 **벤더링하지 않았습니다**.
  필요 시 위 링크에서 직접 확인하세요.
- **garrytan/gstack** (MIT) 는 슬래시 명령/링크만 소개합니다(벤더링 불필요).

### 스크립트 감사 경고

- 벤더링한 DDD 스킬들은 **SKILL.md(순수 텍스트) 뿐**이며 실행 스크립트(`*.sh`, `*.py`)를 포함하지 않습니다 —
  원본 각 스킬 폴더에도 `SKILL.md` / `SKILL.en.md` 두 텍스트 파일만 존재함을 확인했습니다.
- 다만 원본 저장소 **루트/다른 디렉터리**에는 별도 도구 스크립트가 있을 수 있습니다. 이 팩은 그 스크립트를
  **가져오지도 실행하지도 않았습니다.** 상류 저장소에서 스크립트를 추가로 채택할 경우 **실행 전 반드시 감사**하세요.
- 벤더링 스킬의 영문 콘텐츠는 무변경 원본입니다. 내부 상호 참조 링크(예: `> 🌐 中文版本: [Chinese](SKILL.md)`)는
  원문 그대로 보존한 것이며, 이 팩에는 중국어판을 함께 벤더링하지 않았습니다(깨진 링크가 아니라 원문 보존 결과).
