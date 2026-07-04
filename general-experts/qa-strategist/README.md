# QA 전문가 (QA Lead / Strategist) — general-experts 팩

> 이 팀에는 전담 QA 인력이 없을 수 있다. 이 팩은 **품질 전략가(Quality Strategist)** 역할을
> Agent + Skill 조합으로 대체한다. 자동화 테스트 코드를 대신 짜주는 "자동화 코더"가 아니라,
> **무엇을·왜·언제 테스트할지**를 설계하고 릴리즈 품질을 판정하는 역할이다.

- **역할 슬러그:** `qa-strategist`
- **초점:** 테스트 전략 / 리스크 기반 테스트 / 수용 기준 검증 / 릴리즈 품질 게이트 / 회귀 범위 설계 / 버그 트리아지
- **명시적 비(非)범위:** Playwright/Cypress 스크립트 작성·실행, CI 파이프라인 구현 → 이는 `qa-engineer`(자동화 실행) 역할의 몫. 아래 5) 카탈로그의 `fugazi/test-automation-skills-agents` 참조.

---

## 1) 역할 개요 — 이 Agent에게 무엇을 위임하는가

작은 팀에는 QA·기획·디자인 등 여러 역할 공백이 생기기 쉽다.
그중 **품질 판단(quality judgment)** 을 이 팩이 메운다. 다음을 위임한다.

| 위임 항목 | 구체 산출물 |
| --- | --- |
| **테스트 전략 수립** | 스코프, 테스트 피라미드(단위/통합/E2E) 배분, 진입·종료 기준, 품질 KPI, 도구 선택 근거를 담은 실행형 전략 문서 |
| **리스크 기반 우선순위** | 비즈니스 영향 × 발생확률 리스크 매트릭스/히트맵, 상위 항목 실패 모드 분석, 리스크 존 ↔ 테스트 커버리지 매핑 |
| **수용 기준(AC) 검증** | 스토리별 Given/When/Then 수용 기준, "완료의 정의(DoD)" 체크 |
| **릴리즈 품질 게이트** | 근거 기반 Go/No-Go 체크리스트, 스모크 스위트 설계, 단계적 롤아웃·롤백 기준, 배포 후 검증 |
| **버그 트리아지** | 심각도/우선순위 매트릭스, 결함 분류 taxonomy, 중복 제거, 표준 버그 리포트 템플릿 |

> 이 Agent는 **판단과 문서를 만든다.** 실제 테스트 실행/자동화는 개발자 또는 `qa-engineer` 역할에 넘긴다.

---

## 2) 추천 구성 표

### 벤더링(이 팩에 실제 포함된 파일)

| 종류 | 이름 | 소스 (owner/repo) | ⭐ | 라이선스 | 런타임 |
| --- | --- | --- | ---: | --- | --- |
| Agent | `qa-expert` | VoltAgent/awesome-claude-code-subagents | 22.8k | MIT | Claude Code (subagent) |
| Skill | `test-strategy` | petrkindlmann/qa-skills | 28 | MIT | Claude Code / Codex / Cursor / Gemini CLI (Agent Skills Standard) |
| Skill | `risk-based-testing` | petrkindlmann/qa-skills | 28 | MIT | 〃 |
| Skill | `release-readiness` | petrkindlmann/qa-skills | 28 | MIT | 〃 |
| Skill | `ai-bug-triage` | petrkindlmann/qa-skills | 28 | MIT | 〃 |

각 Skill 폴더에는 `SKILL.md` 와 함께 원본의 소형 텍스트 리소스(`references/*.md`: 템플릿·워크시트·분류표·예시)를 함께 벤더링했다. **실행 스크립트(*.sh/*.py)는 포함하지 않았다.**

### 카탈로그 전용(링크만 — 이 팩에 벤더링하지 않음)

| 이름 | 소스 | ⭐ | 라이선스 | 왜 링크만인가 |
| --- | --- | ---: | --- | --- |
| test-automation-skills-agents | [fugazi/test-automation-skills-agents](https://github.com/fugazi/test-automation-skills-agents) | 185 | MIT | 자동화 **실행**은 `qa-engineer` 역할 담당. 전략가 팩은 상호 참조만. |
| gstack 슬래시 명령 `/qa` `/qa-only` `/retro` | [garrytan/gstack](https://github.com/garrytan/gstack) | 119k | MIT | Garry Tan의 Claude Code 셋업. 벤더링 불필요, 명령/링크로 연계. |

> gstack 연계 명령 실제 경로(확인 완료):
> [`qa/SKILL.md`](https://github.com/garrytan/gstack/blob/main/qa/SKILL.md) ·
> [`qa-only/SKILL.md`](https://github.com/garrytan/gstack/blob/main/qa-only/SKILL.md) ·
> [`retro/SKILL.md`](https://github.com/garrytan/gstack/blob/main/retro/SKILL.md)

---

## 3) 설치·사용

### A. 이 팩을 그대로 쓰기 (권장)

이 저장소를 클론했다면 파일은 이미 아래 위치에 있다.

```
general-experts/qa-strategist/
├─ README.md
├─ agents/
│  └─ qa-expert.md
└─ skills/
   ├─ test-strategy/       (SKILL.md + references/)
   ├─ risk-based-testing/  (SKILL.md + references/)
   ├─ release-readiness/   (SKILL.md + references/)
   └─ ai-bug-triage/       (SKILL.md + references/)
```

**Claude Code 프로젝트 스킬로 등록** — 스킬 폴더를 프로젝트 `.claude/skills/` 로 심볼릭 링크하거나 복사한다.

```bash
mkdir -p .claude/skills
cp -R general-experts/qa-strategist/skills/* .claude/skills/
# 서브에이전트 등록
mkdir -p .claude/agents
cp general-experts/qa-strategist/agents/qa-expert.md .claude/agents/
```

등록 후 Claude Code 세션에서 자연어로 호출한다.

```
> 이번 스프린트의 핵심 기능에 대해 test-strategy 스킬로 테스트 전략을 잡아줘
> risk-based-testing 으로 핵심 처리 흐름의 리스크 히트맵을 만들어줘
> release-readiness 체크리스트로 v0.3 배포 Go/No-Go 판정해줘
> qa-expert 서브에이전트에게 현재 테스트 커버리지 갭 분석을 맡겨줘
```

### B. 원본에서 최신 스킬 받기 (Agent Skills Standard)

```bash
# 특정 스킬만
npx skills add petrkindlmann/qa-skills test-strategy risk-based-testing
# 또는 전체 클론
git clone https://github.com/petrkindlmann/qa-skills.git .skills/qa-skills
```

### C. gstack 슬래시 명령 연계(선택)

gstack를 설치한 팀이라면 이 팩의 전략 산출물을 gstack의 릴리즈/회고 루프와 연결할 수 있다.

- `/qa`, `/qa-only` — 릴리즈 매니저/QA 관점의 검수 실행
- `/retro` — 스프린트 회고. `quality-postmortem` 과 궁합이 좋다.

---

## 4) 활용 시나리오

특정 도메인이나 기술 스택을 가정하지 않는, 이 역할의 일반 업무 예시다.

- **테스트 전략 정렬 (test-strategy)** — 스프린트/기능 단위로 테스트 피라미드(단위·통합·E2E) 배분, 진입·종료 기준, 품질 KPI를 담은 실행형 전략 문서를 만든다.
- **리스크 히트맵 (risk-based-testing)** — 비즈니스 영향 × 발생확률로 핵심 기능의 리스크를 매트릭스화하고, 상위 리스크에 테스트 커버리지를 집중 배치한다.
- **릴리즈 게이트 (release-readiness)** — 근거 기반 Go/No-Go 체크리스트, 스모크 스위트, 롤백 기준, 배포 후 검증 창(watch window)을 설계한다. `references/communication-templates.md` 로 배포 공지/롤백 알림 문안을 준비한다.
- **버그 트리아지 표준화 (ai-bug-triage)** — `references/classification-taxonomy.md` 의 심각도/우선순위 매트릭스로 버그를 일관되게 등급화하고, 중복 결함은 fingerprint로 묶어 조사 중복을 방지한다.

> `release-readiness` 의 품질 KPI와 `ai-bug-triage` 의 심각도 분포는 제품 책임자(PO)의 릴리즈 판단·백로그 우선순위에 그대로 입력된다. 회고는 gstack `/retro` 로 연결할 수 있다.

---

## 5) 라이선스·보안 주의

### 라이선스
- 벤더링된 모든 파일은 **MIT** 이며, 각 파일 최상단에 다음 형식의 출처 헤더를 붙였다.
  ```
  <!-- SOURCE: <원본 웹 URL> | REPO: <owner/repo> | LICENSE: MIT | RETRIEVED: 2026-07-04 -->
  ```
  헤더 아래 본문은 원본 바이트를 **변경 없이** 그대로 보존했다(MIT 저작권 고지 유지).
- 원본 저작권: `qa-skills` © 2026 Petr Kindlmann / `awesome-claude-code-subagents` © 2025 VoltAgent.
- 재배포·수정 시 각 레포 루트의 `LICENSE`(MIT 전문)를 함께 유지할 것.

### 벤더 불가 / 벤더 안 함
- **fugazi/test-automation-skills-agents** — MIT 이지만 이 전략가 팩의 범위 밖(자동화 실행). 링크만 제공, 벤더링하지 않음. 자동화 실행이 필요하면 `qa-engineer` 역할 팩에서 다룬다.
- **garrytan/gstack** — MIT. 슬래시 명령 연계 소개용 링크만. 벤더링하지 않음.

### 스크립트 감사 경고 (중요)
- 벤더링한 것은 **`SKILL.md` 와 `references/*.md`(순수 텍스트)뿐**이다. 원본 `qa-skills` 레포에는 자동화/CI용 실행 스크립트가 포함될 수 있으나, 이 팩에는 **어떤 `*.sh` / `*.py` / 도구 스크립트도 포함하지 않았다.**
- `ai-bug-triage` 등 일부 스킬은 본문에서 **LLM 파이프라인·CI 로그 파싱·외부 티켓 연동**을 전제로 한다. 이런 통합을 실제 실행할 경우 **반드시 코드 감사 후** 최소 권한으로 도입할 것(로그에 PII/시크릿 유입 여부, 아웃바운드 네트워크 호출 확인).
- gstack `ios-qa` 등은 데몬/CLI 실행 코드를 포함한다. **본 팩은 이를 참조/실행하지 않는다.** 사용 시 별도 감사 필요.
- 원칙: 이 팩의 스킬은 **의사결정·문서 생성용**으로 안전하게 쓰고, 실행형 자동화는 반드시 사람이 검토한 뒤 별도 역할로 분리해 도입한다.
