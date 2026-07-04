# QA Engineer (Test Automation Engineer) — 전문가 팩

> **QA / 테스트 자동화 실행자** 역할을 Claude Code용 Agent + Skill 묶음으로 제공합니다.
> 핵심 초점: **Playwright/Selenium E2E · API 테스트 · flaky test 분석 · CI 테스트 파이프라인 · 접근성(a11y) 자동 검사**.

---

## 1) 역할 개요 — 이 Agent에게 무엇을 위임하는가

전담 QA가 없는 팀에서 테스트 자동화는 개발자가 곁다리로 떠안게 됩니다. 이 팩은 그 공백을 메우는
**"테스트 자동화 실행자"** 를 제공합니다. 다음을 위임하세요.

- **E2E 자동화 작성/실행** — 핵심 사용자 흐름(로그인 → 주요 기능 → 결과 확인 등)을 Playwright로 자동화
- **API 계약 테스트** — REST/GraphQL 엔드포인트에 대한 스키마 검증, 인증(JWT/OAuth2), 상태코드(4xx/5xx), 페이지네이션·정렬 경계값 테스트 (Playwright request fixture 또는 REST Assured)
- **flaky test 헌팅** — 비동기 큐·폴링·웹소켓처럼 타이밍에 취약한 테스트의 간헐적 실패를 근본 원인 분석하고 안정화
- **접근성 자동 검사** — WCAG 2.1 AA 기준 키보드 내비게이션/ARIA/대비 자동 점검
- **CI 통합** — 테스트를 CI 파이프라인에 배선하고 빠른 피드백/재시도 전략 구성

> 참고: **테스트 "전략/계획" 수립**(무엇을 어느 수준으로 테스트할지, 리스크 기반 우선순위, 커버리지 정책)은 별도 **qa-strategist** 역할의 몫입니다. 이 팩은 **실행·자동화**에 집중합니다. 전략 레이어는 아래 [카탈로그](#5-라이선스보안-주의)의 `petrkindlmann/qa-skills`를 참조하세요.

---

## 2) 추천 구성 표

### 벤더링된 Skills (이 저장소에 실제 파일 포함)

| Skill | 용도 | 소스(owner/repo) | ⭐ | 라이선스 | 런타임 |
|---|---|---|---|---|---|
| `skills/api-testing` | REST/GraphQL API 테스트 — 스키마 검증, 인증, 에러/경계값 (Playwright request + REST Assured) | fugazi/test-automation-skills-agents | 185 | MIT | Claude Code (Skill) |
| `skills/playwright-e2e-testing` | 웹 E2E 자동화 — Page Object Model, 로케이터 전략 | fugazi/test-automation-skills-agents | 185 | MIT | Claude Code (Skill) |
| `skills/a11y-playwright-testing` | 접근성 자동 검사 — WCAG 2.1 AA 체크리스트, ARIA 패턴 | fugazi/test-automation-skills-agents | 185 | MIT | Claude Code (Skill) |

### 벤더링된 Agents (에이전트 프로필)

| Agent | 용도 | 소스(owner/repo) | ⭐ | 라이선스 | 런타임 |
|---|---|---|---|---|---|
| `agents/flaky-test-hunter` | 간헐적 실패(flaky) 테스트 식별·근본원인 분석·안정화 (대표 agent) | fugazi/test-automation-skills-agents | 185 | MIT | Claude Code (subagent) |
| `agents/test-automator` | 테스트 프레임워크 설계·스크립트 작성·CI/CD 통합 총괄 | VoltAgent/awesome-claude-code-subagents | 22.8k | MIT | Claude Code (subagent) |
| `agents/accessibility-tester` | WCAG 준수 검증·보조기술 지원 평가 | VoltAgent/awesome-claude-code-subagents | 22.8k | MIT | Claude Code (subagent) |

### 카탈로그 전용(링크만 — 벤더링하지 않음)

| 항목 | 용도 | 소스 | ⭐ | 라이선스 |
|---|---|---|---|---|
| qa-skills | 테스트 **전략** 레이어 (qa-strategist 역할이 사용) | petrkindlmann/qa-skills | 28 | MIT |
| gstack `/qa` | gstack 워크플로우와의 QA 슬래시 명령 연계 | garrytan/gstack | 119k | MIT |

---

## 3) 설치 · 사용

### 3-1. 이 저장소를 그대로 사용
이 팩은 `general-experts/qa-engineer/` 아래에 이미 벤더링되어 있습니다.

```
general-experts/qa-engineer/
├── README.md
├── skills/
│   ├── api-testing/
│   │   ├── SKILL.md
│   │   └── references/{rest-assured-testing.md, schema-validation.md}
│   ├── playwright-e2e-testing/
│   │   ├── SKILL.md
│   │   └── references/page_object_model.md
│   └── a11y-playwright-testing/
│       ├── SKILL.md
│       └── references/wcag21aa-checklist.md
└── agents/
    ├── flaky-test-hunter.md
    ├── test-automator.md
    └── accessibility-tester.md
```

### 3-2. Skill 설치 (Claude Code)
Skill은 폴더 단위입니다. 프로젝트 또는 개인 스킬 경로로 복사하세요.

```bash
# 프로젝트 스킬로 사용
mkdir -p .claude/skills
cp -R general-experts/qa-engineer/skills/api-testing            .claude/skills/
cp -R general-experts/qa-engineer/skills/playwright-e2e-testing .claude/skills/
cp -R general-experts/qa-engineer/skills/a11y-playwright-testing .claude/skills/
```

각 `SKILL.md`의 `description` 트리거에 맞는 요청(예: "이 API 테스트 만들어줘", "핵심 사용자 흐름 E2E 짜줘")을 하면 Claude Code가 해당 스킬을 자동 로드합니다.

### 3-3. Agent(subagent) 설치 (Claude Code)

```bash
mkdir -p .claude/agents
cp general-experts/qa-engineer/agents/flaky-test-hunter.md   .claude/agents/
cp general-experts/qa-engineer/agents/test-automator.md      .claude/agents/
cp general-experts/qa-engineer/agents/accessibility-tester.md .claude/agents/
```

호출 예: `@test-automator 핵심 API에 대한 회귀 테스트 스위트를 만들어줘`, `@flaky-test-hunter 폴링 테스트가 CI에서 5%쯤 실패해 — 원인 잡아줘`.

> 원본 그대로 벤더링했으므로, 팀의 프론트엔드 프레임워크/CI에 맞춰 `tools`·경로·명령어는 조정하세요. `flaky-test-hunter`는 Playwright MCP 도구 이름을 참조하므로 실제 도구 세팅에 맞게 정리가 필요합니다.

### 3-4. 최신본 다시 가져오기 (원저장소)

```bash
gh api "repos/fugazi/test-automation-skills-agents/contents/skills" --jq '.[].name'
gh api "repos/VoltAgent/awesome-claude-code-subagents/contents/categories/04-quality-security" --jq '.[].name'
```

---

## 4) 활용 시나리오

1. **E2E 자동화 (playwright-e2e-testing)** — 핵심 사용자 흐름을 Page Object Model로 구조화하고, 상태 전이를 명시적 wait로 검증(임의 sleep 금지).
2. **API 계약 테스트 (api-testing + REST Assured)** — 주요 엔드포인트의 상태코드·JSON 스키마·인증(JWT)을 계약으로 고정해 회귀를 방지. `references/rest-assured-testing.md`·`references/schema-validation.md`가 그대로 참고자료.
3. **flaky test 안정화 (flaky-test-hunter)** — 타이밍 의존 테스트의 간헐 실패를 근본원인(레이스 컨디션/암묵적 대기/테스트 간 상태 공유) 분석 후 명시적 대기·격리로 교정. (테스트를 임의로 비활성화하지 않고 사유를 문서화하는 원칙 내장.)
4. **접근성 자동 검사 + CI 배선 (a11y-playwright-testing + accessibility-tester + test-automator)** — WCAG 2.1 AA 체크리스트로 키보드/ARIA/대비를 점검하고, API·E2E·a11y 테스트를 CI에 스모크 → 회귀 순으로 게이팅. 실패 시 아티팩트(스크린샷/trace) 수집을 표준화.

---

## 5) 라이선스 · 보안 주의

### 라이선스
- 벤더링된 모든 파일은 **MIT** 라이선스이며, 각 파일 최상단에 `SOURCE | REPO | LICENSE | RETRIEVED` 출처 헤더(HTML 주석)를 부착했습니다. 본문은 원본 바이트를 **변경 없이** 보존했습니다.
  - `fugazi/test-automation-skills-agents` — MIT (© 2026 Douglas Urrea Ocampo)
  - `VoltAgent/awesome-claude-code-subagents` — MIT (© 2025 VoltAgent)

### 카탈로그 전용 — 벤더링 금지
- **petrkindlmann/qa-skills** (MIT) — 테스트 **전략** 스킬. 본 팩(실행/자동화)과 역할이 다르며 **qa-strategist** 역할에서 다룹니다. 여기서는 링크로만 상호 참조:
  https://github.com/petrkindlmann/qa-skills
- **garrytan/gstack** (MIT) — `/qa` 슬래시 명령 등 QA 워크플로우 연계용. 대형 모노레포이므로 **벤더링하지 않고** 링크/명령만 소개합니다. gstack을 함께 쓰는 팀이라면 gstack의 QA 명령과 본 팩 스킬을 조합할 수 있습니다:
  https://github.com/garrytan/gstack

### 스크립트 감사 경고 (중요)
- 원본 `api-testing` 스킬에는 **실행 스크립트/템플릿**이 포함되어 있으나, 정책에 따라 **벤더링하지 않았습니다.** 필요 시 원본에서 직접 가져오되 **실행 전 반드시 코드 감사**하세요.
  - `skills/api-testing/scripts/api-health-check.sh` — **미벤더링(감사 필요)**
  - `skills/api-testing/templates/playwright-api-spec.ts`, `skills/api-testing/templates/rest-assured-test.java` — 미벤더링(예시 템플릿, 필요 시 원본 확인)
- 벤더링한 것은 **SKILL.md와 텍스트 references(.md)뿐**입니다. 실행 가능한 `.sh`/`.py`/툴 스크립트는 포함하지 않았습니다.
- `agents/flaky-test-hunter.md`는 `bash` 및 Playwright MCP 도구 사용을 전제로 합니다. 실제 도구 권한/명령을 팀 환경에 맞게 검토·제한한 뒤 사용하세요.

---

### 원본 파일 출처 (fetch URL)

| 벤더 파일 | 원본 URL |
|---|---|
| `skills/api-testing/SKILL.md` | https://github.com/fugazi/test-automation-skills-agents/blob/main/skills/api-testing/SKILL.md |
| `skills/api-testing/references/rest-assured-testing.md` | https://github.com/fugazi/test-automation-skills-agents/blob/main/skills/api-testing/references/rest-assured-testing.md |
| `skills/api-testing/references/schema-validation.md` | https://github.com/fugazi/test-automation-skills-agents/blob/main/skills/api-testing/references/schema-validation.md |
| `skills/playwright-e2e-testing/SKILL.md` | https://github.com/fugazi/test-automation-skills-agents/blob/main/skills/playwright-e2e-testing/SKILL.md |
| `skills/playwright-e2e-testing/references/page_object_model.md` | https://github.com/fugazi/test-automation-skills-agents/blob/main/skills/playwright-e2e-testing/references/page_object_model.md |
| `skills/a11y-playwright-testing/SKILL.md` | https://github.com/fugazi/test-automation-skills-agents/blob/main/skills/a11y-playwright-testing/SKILL.md |
| `skills/a11y-playwright-testing/references/wcag21aa-checklist.md` | https://github.com/fugazi/test-automation-skills-agents/blob/main/skills/a11y-playwright-testing/references/wcag21aa-checklist.md |
| `agents/flaky-test-hunter.md` | https://github.com/fugazi/test-automation-skills-agents/blob/main/agents/flaky-test-hunter.agent.md |
| `agents/test-automator.md` | https://github.com/VoltAgent/awesome-claude-code-subagents/blob/main/categories/04-quality-security/test-automator.md |
| `agents/accessibility-tester.md` | https://github.com/VoltAgent/awesome-claude-code-subagents/blob/main/categories/04-quality-security/accessibility-tester.md |
