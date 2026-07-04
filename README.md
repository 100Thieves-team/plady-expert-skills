# plady-expert-skills

------------

## Purpose
우리 팀에는 백엔드 개발자 2명, 프론트엔드 개발자 1명이 존재한다. 그리고 백엔드 멘토 1명, 프론트엔드 멘토 1명, 데이터엔지니어(PO) 멘토 1명이 멘토링해주고 있다.
우리 팀에 존재하지 않는 도메인 전문가, 기획자, UI/UX 디자이너, QA 전문가, DBA, SRE Engineer, Devops, Data Engineer의 공백을 채우기 위해, 각 역할을 Agent와 Skill로 구성한다.

## List
- 도메인 전문가
- 기획자
- UI/UX 디자이너
- QA 전문가
- DBA
- SRE Engineer
- QA Engineer
- Devops Engineer
- Data Enginer

## general-experts
awesome-xxx-skills 같이 github 상에 유명한 skill들을 모아두는 공간입니다.

검증된 오픈소스 Agent/Skill을 원본 무변경으로 벤더링(+ 최상단 `SOURCE` 헤더)하고, 라이선스상 벤더 불가한 소스는 카탈로그 링크로만 소개합니다. 현재 **9개 역할 · Agent 25 · Skill 22** (전 항목 출처 대조 통과, 환각 0건). 자세한 역할별 구성·gstack 연계·라이선스/보안 주의는 [`general-experts/README.md`](./general-experts/README.md) 참조.

| 역할 | 디렉터리 | 주요 소스 |
|---|---|---|
| 도메인 전문가 | [`domain-expert`](./general-experts/domain-expert) | ForceInjection/domain-driven-design-skills, VoltAgent |
| 기획자 | [`product-planner`](./general-experts/product-planner) | VoltAgent (deanpeters/Digidai는 카탈로그) |
| UI/UX 디자이너 | [`uiux-designer`](./general-experts/uiux-designer) | Owl-Listener/designer-skills, VoltAgent |
| QA 전략가 | [`qa-strategist`](./general-experts/qa-strategist) | petrkindlmann/qa-skills, VoltAgent |
| DBA | [`dba`](./general-experts/dba) | VoltAgent (database-administrator, sql-pro, postgres-pro) |
| SRE Engineer | [`sre-engineer`](./general-experts/sre-engineer) | VoltAgent (sinzin91은 카탈로그) |
| QA Engineer | [`qa-engineer`](./general-experts/qa-engineer) | fugazi/test-automation-skills-agents, VoltAgent |
| DevOps Engineer | [`devops-engineer`](./general-experts/devops-engineer) | akin-ozer/cc-devops-skills, VoltAgent |
| Data Engineer | [`data-engineer`](./general-experts/data-engineer) | VoltAgent (05-data-ai), Jeffallan/claude-skills |

> 전 역할을 가로지르는 [garrytan/gstack](https://github.com/garrytan/gstack)(MIT)은 슬래시 명령으로 연계 소개(미벤더).

## algo-experts
우리가 해결하려고 하는 알고리즘 문제 풀이 영역에 최적화된 experts skill들을 커스텀해서 모아두는 공간입니다.

전문가 문서(`Algorithm-Problem-Solving-Product-Domain-Architect.md`, `Activity-Area-Experts/*.skill.md`)를 실제 Claude Agent Skill(`skills/<slug>/SKILL.md`, YAML frontmatter + 본문)로 변환했습니다. 원본 **본문은 바이트 단위로 보존**하고 스킬 자동 로딩을 결정하는 `description` frontmatter만 각 문서로부터 새로 작성했습니다. 현재 **Skill 13** (parent architect 1 + subdomain 전문가 12). 목록·계층·사용 시점은 [`algo-experts/skills/README.md`](./algo-experts/skills/README.md) 참조.

> 이 스킬들은 알고리즘 문제를 **푸는** 도구가 아니라, 알고리즘 문제 풀이 제품의 도메인 프레이밍·요구사항·범위·리스크를 정의하는 **제품 도메인 전문가**입니다. 원본 `.skill.md`·번들·`README_subdomain_experts.md`는 카탈로그로 그대로 보존됩니다.

## Skill vs Agent 분류 기준
새 전문가를 추가할 때 **Skill**로 둘지 **Agent(서브에이전트)** 로 둘지는 아래 기준으로 판단한다.

**한 줄 기준** — 결과물을 *지금 이 대화에서 직접 만들어 적용*하면 **Skill**, *통째로 위임하고 결과만* 받으면 **Agent**.

**하드 룰 — 하나라도 해당하면 Agent**
1. 자기만의 도구 허용목록(`tools:`)이나 모델(`model:`)을 지정해야 한다
2. 독립 context에서 자율 실행하고 최종 결과만 반환받고 싶다 (중간 과정 격리)
3. 여러 개를 병렬로 돌리고 싶다
4. 파일을 쓰고 명령을 돌리는 실행(execution) 역할이다

**Skill 조건** — 위가 전부 아니고, 핵심이 지식·절차·규칙·포맷이라 현재 에이전트가 읽어 인라인 적용하면 되는 자문형(분석·요구사항·spec·design)이면 Skill.

| | Skill | Agent |
|---|---|---|
| frontmatter | `name`, `description` (+metadata) | `name`, `description`, **`tools`**, **`model`** |
| 실행 | 현재 대화에 로드, 같은 context | 별도 context, 결과만 반환 |
| 설치 위치 | `.claude/skills/<name>/SKILL.md` | `.claude/agents/<name>.md` |
| 예시 | `sql-pro`(구현 플레이북), `ddd-*`, `aps-*` | `data-engineer`, `postgres-pro`, `sre-engineer` |

> `sql-pro`처럼 같은 전문성을 **Skill(인라인 적용)** 과 **Agent(위임)** 두 모드로 동시에 두는 것도 정상이다 — 폴더가 달라 충돌하지 않는다.

## 활성화 (.claude/)
Claude Code가 이 프로젝트에서 실제로 인식하려면 스킬은 `.claude/skills/<name>/`, 에이전트는 `.claude/agents/<name>.md`에 있어야 하므로 위 기준대로 모두 설치했다.

- **`.claude/skills/` — 35개** (algo-experts 13 + general-experts 22)
- **`.claude/agents/` — 24개** (general-experts 25개 중 `accessibility-tester` 중복 1건 통합)

정규화·보존 규칙:
- general-experts **카탈로그 원본**은 `SOURCE` 헤더를 최상단에 두는 벤더링 규칙 그대로 보존한다(무변경).
- **설치본**은 frontmatter가 1번째 줄에 오도록 `SOURCE` 주석을 frontmatter 아래로 옮긴다(출처 보존, 로딩 가능화).
- 업스트림 결함은 설치본에서만 최소 교정(내용 불변): `assumption-mapping`·`backlog-grooming`은 `description`이 따옴표 없이 `: `를 포함해 YAML이 깨져 재인용, `flaky-test-hunter`는 `name: 'Flaky Test Hunter'`(공백·대문자)를 호출 가능한 슬러그로 변경. → 카탈로그 원본에도 반영하려면 별도 요청.
