# general-experts

## 1. 소개

`general-experts`는 **`awesome-xxx-skills`처럼 GitHub에 공개된 유명 Agent/Skill을 역할별로 모아 벤더링(vendoring)하고 카탈로그화한 공간**입니다. 팀에 없는 역할(도메인 전문가 · 기획자 · UI/UX 디자이너 · QA · DBA · SRE · DevOps · Data Engineer)의 공백을, 검증된 오픈소스 Agent/Skill을 원본 그대로 가져와(무변경 + 최상단 SOURCE 헤더 주석만 추가) 메웁니다. **특정 제품·도메인·기술 스택에 종속되지 않은 범용 팩**을 지향합니다.

> **`algo-experts`와의 차이** — `general-experts`는 제품과 무관한 범용 소프트웨어 역할을 커버합니다. `algo-experts`는 (앞으로 구체화될) 특정 제품/도메인에 특화해 커스텀한 experts를 모으는 공간으로, 도메인 색이 짙은 커스터마이징은 그쪽에 둡니다.

벤더링 원칙: 원본 바이트 무변경 보존, 파일 최상단에만 `SOURCE / REPO / LICENSE / RETRIEVED` 주석 헤더 추가, 실행 스크립트(`*.sh`/`*.py`)는 원칙적으로 미포함(텍스트 `SKILL.md`/에이전트 프로필/`references/*.md`만), 라이선스가 벤더링을 허용하지 않는 소스는 카탈로그 링크로만 소개.

현재 규모: **9개 역할 · Agent 25개 · Skill 22개** 벤더링.

---

## 2. 역할별 요약

| 역할 | 디렉터리 | 핵심 Agent | 핵심 Skills | 주요 소스 (owner/repo · 라이선스) | 검증 |
|---|---|---|---|---|---|
| 도메인 전문가 (DDD 발굴/모델링) | [`domain-expert`](./domain-expert) | domain-expert(합성), business-analyst | ddd-discover, ddd-subdomains, ddd-contexts, ddd-aggregates, ddd-model-review | ForceInjection/domain-driven-design-skills (Apache-2.0) · VoltAgent/awesome-claude-code-subagents (MIT) | ✅ PASS |
| 기획자 (Product Planner/PM) | [`product-planner`](./product-planner) | product-manager, scrum-master, backlog-grooming, assumption-mapping | (없음 · 카탈로그로 커버) | VoltAgent/awesome-claude-code-subagents (MIT) | ✅ PASS |
| UI/UX 디자이너 | [`uiux-designer`](./uiux-designer) | ux-researcher, accessibility-tester | accessibility-audit, design-token, component-spec, form-design | Owl-Listener/designer-skills (MIT) · VoltAgent (MIT) | ✅ PASS |
| QA 전략가 (Quality Strategist) | [`qa-strategist`](./qa-strategist) | qa-expert | test-strategy, risk-based-testing, release-readiness, ai-bug-triage | petrkindlmann/qa-skills (MIT) · VoltAgent (MIT) | ✅ PASS |
| DBA | [`dba`](./dba) | database-administrator, sql-pro, postgres-pro, database-optimizer | (없음 · Agent가 스킬 겸함) | VoltAgent/awesome-claude-code-subagents (MIT) | ✅ PASS |
| SRE 엔지니어 | [`sre-engineer`](./sre-engineer) | sre-engineer, devops-incident-responder, chaos-engineer | (없음 · 카탈로그로 커버) | VoltAgent/awesome-claude-code-subagents (MIT) | ✅ PASS |
| QA 엔지니어 (자동화 실행) | [`qa-engineer`](./qa-engineer) | test-automator, flaky-test-hunter, accessibility-tester | api-testing, playwright-e2e-testing, a11y-playwright-testing | fugazi/test-automation-skills-agents (MIT) · VoltAgent (MIT) | ✅ PASS |
| DevOps 엔지니어 | [`devops-engineer`](./devops-engineer) | devops-engineer, deployment-engineer, terraform-engineer | dockerfile-generator, github-actions-generator, terraform-generator, k8s-yaml-generator | akin-ozer/cc-devops-skills (Apache-2.0) · VoltAgent (MIT) | ✅ PASS |
| 데이터 엔지니어 | [`data-engineer`](./data-engineer) | data-engineer, data-analyst, mlops-engineer | spark-engineer, sql-pro | Jeffallan/claude-skills (MIT) · VoltAgent (MIT) | ✅ PASS |

> 검증 열은 각 역할 큐레이션의 `verify.overall` 값입니다. **9개 역할 전부 PASS, 환각 의심(fabricationSuspected) 0건**이라 ⚠️ 표기 대상이 없습니다. 자세한 근거는 6절 참조.
>
> ⭐ 스타 수·라이선스·벤더 여부는 아래 **소스 저장소 일람** 참조(2026-07-04 직접 조회).

### 소스 저장소 일람 (⭐ · 라이선스 · 상태, 2026-07-04 기준)

| 저장소 | ⭐ | 라이선스 | 상태 |
|---|---|---|---|
| [garrytan/gstack](https://github.com/garrytan/gstack) | 119k | MIT | 연계(메타 팩, 미벤더) |
| [VoltAgent/awesome-agent-skills](https://github.com/VoltAgent/awesome-agent-skills) | 27.2k | MIT | 카탈로그 |
| [VoltAgent/awesome-claude-code-subagents](https://github.com/VoltAgent/awesome-claude-code-subagents) | 22.8k | MIT | **벤더** |
| [Jeffallan/claude-skills](https://github.com/Jeffallan/claude-skills) | 10.4k | MIT | **벤더** |
| [deanpeters/Product-Manager-Skills](https://github.com/deanpeters/Product-Manager-Skills) | 5.5k | CC BY-NC-SA | ⛔ 카탈로그(비상업) |
| [Owl-Listener/designer-skills](https://github.com/Owl-Listener/designer-skills) | 1.7k | MIT | **벤더** |
| [elastic/agent-skills](https://github.com/elastic/agent-skills) | 525 | Apache-2.0 | 카탈로그 |
| [majiayu000/claude-skill-registry](https://github.com/majiayu000/claude-skill-registry) | 469 | MIT | 카탈로그 |
| [plugin87/ux-ui-agent-skills](https://github.com/plugin87/ux-ui-agent-skills) | 438 | 없음 | ⛔ 카탈로그(무라이선스) |
| [akin-ozer/cc-devops-skills](https://github.com/akin-ozer/cc-devops-skills) | 260 | Apache-2.0 | **벤더** |
| [fugazi/test-automation-skills-agents](https://github.com/fugazi/test-automation-skills-agents) | 185 | MIT | **벤더** |
| [Digidai/product-manager-skills](https://github.com/Digidai/product-manager-skills) | 117 | NOASSERTION | ⛔ 카탈로그(불명확) |
| [petrkindlmann/qa-skills](https://github.com/petrkindlmann/qa-skills) | 28 | MIT | **벤더** |
| [ForceInjection/domain-driven-design-skills](https://github.com/ForceInjection/domain-driven-design-skills) | 21 | Apache-2.0 | **벤더** |
| [sinzin91/awesome-sre-skills](https://github.com/sinzin91/awesome-sre-skills) | 5 | CC0-1.0 | 카탈로그(awesome-list) |

> ⭐는 조회 시점(2026-07-04) 값이라 변동됩니다. `github/awesome-copilot`(MIT, ⭐36k)도 기획자 카탈로그로 링크만 유지합니다.

---

## 3. gstack 연계

[garrytan/gstack](https://github.com/garrytan/gstack) (MIT · ⭐119k)는 Claude Code를 "가상 소프트웨어 팀"으로 만드는 **메타 팩으로, 특정 역할이 아니라 전 역할을 가로질러 씁니다.** 이 저장소는 gstack 코드를 벤더링하지 않고, 슬래시 명령 이름/링크로만 각 역할에 연계 소개합니다(사용하려면 gstack을 별도 설치해야 하며, 설치 전 스크립트/훅 감사 필요 — 5절 참조).

| 슬래시 명령 | 매핑 역할 | 용도 |
|---|---|---|
| `/investigate` | domain-expert, sre-engineer | 코드/장애 원인 조사 |
| `/spec` | domain-expert, product-planner | 명세(스펙) 작성 |
| `/learn` | domain-expert | 학습/온보딩 |
| `/office-hours` | product-planner | CEO/PM 리뷰·브레인스토밍 |
| `/plan-ceo-review` | product-planner | 기획 상위 리뷰 |
| `/retro` | product-planner, qa-strategist, sre-engineer | 회고 |
| `/design`, `/design-review`, `/design-consultation`, `/design-html`, `/design-shotgun` | uiux-designer | 디자인 컨설팅·리뷰·HTML 시안 |
| `/qa`, `/qa-only` | qa-strategist, qa-engineer | QA 실행·품질 게이트 |
| `/health` | sre-engineer | 시스템 헬스체크 |
| `/ship`, `/land-and-deploy`, `/setup-deploy`, `/guard` | devops-engineer | 배포 리듬(배포·셋업·가드) |

> **dba**, **data-engineer**는 gstack에 직접 대응하는 슬래시 명령이 없어 매핑에서 제외했습니다(해당 역할 README에서도 gstack은 링크만).

gstack에는 이 표 외에도 `/plan`, `/brainstorm`, `/document-release`, `/careful`, `/freeze`·`/unfreeze`, `/diagram`, `/make-pdf`, `/skillify`, `/review`, `/pair-agent`, `/cso` 등 다수의 명령이 존재합니다. 필요 시 원본 저장소에서 확인하세요.

---

## 4. 설치 · 사용 가이드

### 4-1. 벤더링된 Skill/Agent를 프로젝트에 적용

각 역할 디렉터리의 `agents/*.md`, `skills/<name>/SKILL.md`를 Claude Code가 인식하는 위치로 복사합니다.

```bash
# 저장소 루트 기준
GE=general-experts

# 프로젝트 스코프(.claude/…)에 특정 역할의 스킬/에이전트 반영 (예: devops-engineer)
mkdir -p .claude/skills .claude/agents
cp -R "$GE/devops-engineer/skills/"* .claude/skills/
cp    "$GE/devops-engineer/agents/"*.md .claude/agents/

# 사용자 전역 스코프(~/.claude/…)로 쓰려면 대상 경로만 교체
cp -R "$GE/qa-engineer/skills/"* ~/.claude/skills/
cp    "$GE/qa-engineer/agents/"*.md ~/.claude/agents/
```

- **Skill**: `skills/<name>/SKILL.md`가 스킬 1개 단위입니다. `<name>` 폴더째 `.claude/skills/`로 옮기세요(폴더명 = 스킬명 유지).
- **Agent**: `agents/<name>.md`(또는 `<name>.agent.md`)를 `.claude/agents/`로 옮기면 서브에이전트로 인식됩니다.
- 각 파일 최상단 `SOURCE` 헤더 주석은 출처 추적용이며 지워도 동작에는 영향 없습니다(추적성 위해 유지 권장).
- 일부 스킬 본문은 `references/*.md`를 참조합니다. 상세 가이드까지 필요하면 원본 스킬 폴더 전체(references 포함)를 함께 받으세요(아래 4-2).

### 4-2. 원본 레포에서 최신본 받기

벤더링본은 특정 시점 스냅샷입니다. 최신본이 필요하면 원본에서 직접 받으세요.

```bash
# 단일 파일만 최신화 (gh CLI, raw 경로 = default branch main)
gh api repos/petrkindlmann/qa-skills/contents/skills/test-strategy/SKILL.md \
  --jq '.content' | base64 -d > SKILL.md

# 스킬 폴더 전체(스크립트/references 포함)가 필요할 때는 sparse clone
git clone --filter=blob:none --sparse https://github.com/akin-ozer/cc-devops-skills
cd cc-devops-skills
git sparse-checkout set devops-skills-plugin/skills/dockerfile-generator
```

주요 원본 저장소:

- VoltAgent/awesome-claude-code-subagents — https://github.com/VoltAgent/awesome-claude-code-subagents (MIT)
- ForceInjection/domain-driven-design-skills — https://github.com/ForceInjection/domain-driven-design-skills (Apache-2.0)
- Owl-Listener/designer-skills — https://github.com/Owl-Listener/designer-skills (MIT)
- petrkindlmann/qa-skills — https://github.com/petrkindlmann/qa-skills (MIT)
- fugazi/test-automation-skills-agents — https://github.com/fugazi/test-automation-skills-agents (MIT)
- akin-ozer/cc-devops-skills — https://github.com/akin-ozer/cc-devops-skills (Apache-2.0)
- Jeffallan/claude-skills — https://github.com/Jeffallan/claude-skills (MIT)
- garrytan/gstack — https://github.com/garrytan/gstack (MIT) — 메타 팩/슬래시 명령은 플러그인으로 설치

---

## 5. 라이선스 · 보안 주의 (전역)

### 5-1. 벤더링 불가 (라이선스 사유 — 카탈로그 링크로만 소개)

| 저장소 | 라이선스 | 사유 |
|---|---|---|
| deanpeters/Product-Manager-Skills | CC BY-NC-SA 4.0 (NOASSERTION) | **비상업 라이선스** — 재배포/벤더링 금지 |
| Digidai/product-manager-skills | NOASSERTION | 라이선스 불명확 — 벤더링 금지 |
| plugin87/ux-ui-agent-skills | 라이선스 파일 없음 | **NO LICENSE** — 재배포/벤더링 금지 |

> 그 외 `majiayu000/claude-skill-registry`(MIT), `github/awesome-copilot`(MIT), `elastic/agent-skills`(Apache-2.0), `VoltAgent/awesome-agent-skills`(MIT), `sinzin91/awesome-sre-skills`(CC0-1.0) 등은 라이선스상 벤더 가능하나, 큐레이션 지시에 따라 **카탈로그 전용**으로 두어 링크만 유지합니다. `sinzin91/awesome-sre-skills`는 스킬 저장소가 아니라 외부 스킬을 링크만 모은 awesome-list라 벤더링할 `SKILL.md` 자체가 없습니다.

### 5-2. 스크립트 감사 (필수)

- 벤더링본은 **텍스트만** 포함하고 실행 스크립트는 가져오지 않았습니다. 그러나 일부 `SKILL.md` 본문은 원본 저장소의 스크립트 호출을 전제로 합니다. 원본에서 스크립트까지 받아 쓸 경우 **실행 전 반드시 코드 감사**하세요.
- 특히 주의(원본에 존재, 본 저장소 미포함): `devops-engineer/dockerfile-generator → scripts/dockerfile-validate.sh`, `terraform-generator → scripts/run_ci_checks.sh`, `k8s-yaml-generator → scripts/setup_tools.sh`(도구 설치 스크립트). `qa-engineer/api-testing`의 `scripts/*.sh`·`templates/*` 및 gstack 슬래시 명령 설치본도 동일하게 감사 대상입니다.
- 네트워크 툴 주의: 일부 에이전트 프론트매터에 `WebFetch`/`WebSearch`(외부 네트워크) 또는 `Bash` 실행 권한이 선언돼 있습니다(예: ux-researcher, accessibility-tester, qa-expert 등). 폐쇄망/민감 환경에서는 프로젝트 권한에서 도구 허용을 제한하세요.

### 5-3. 인프라 역할 운영 원칙 — DBA · SRE · DevOps

이들 역할의 Agent는 DDL/마이그레이션/백업/`terraform apply`/`kubectl apply`/프로덕션 배포 등 **비가역 동작을 생성**할 수 있습니다. 반드시 다음 순서를 지키세요.

> **읽기전용 리뷰 → 변경 계획 → 사람 승인 → 적용**

- 인덱스/DDL 변경은 락 영향 검토(예: `CREATE INDEX CONCURRENTLY`), 백필/삭제는 트랜잭션 경계·롤백 계획 선확인.
- 실 자격증명을 프롬프트에 넣지 말 것. 스테이징 검증 후 프로덕션 적용.

---

## 6. 검증 노트

큐레이션 시 각 역할별로 벤더링 파일을 원본(raw.githubusercontent.com)과 독립 재대조했습니다.

**결과: 전 항목 출처 대조 통과.** 9개 역할 모두 `verify.overall = PASS`, `MISMATCH`·`SOURCE_404`·환각 의심(fabricationSuspected) **0건**입니다.

투명성을 위한 참고 사항:

- **샘플링 상한(SKIPPED)**: 동일 레포에서 온 형제 파일이 여럿일 때 대조는 3파일 상한으로 표본 검사했습니다. 아래 파일은 "미대조"일 뿐 불일치가 아니며, 같은 레포·구조의 형제 파일이 모두 MATCH로 확인됐습니다.
  - domain-expert: `ddd-subdomains`, `ddd-contexts`, `ddd-aggregates` (SKILL.md)
  - uiux-designer: `component-spec` (SKILL.md)
  - qa-strategist: `ai-bug-triage` (SKILL.md)
  - devops-engineer: `k8s-yaml-generator` (SKILL.md)
- **합성 파일(SYNTHESIZED, 벤더 아님)**: `domain-expert/agents/domain-expert.agent.md`는 직접 작성한 **제품 무관(product-agnostic) DDD 오케스트레이터** 프로필이며 대조 원본이 없습니다. 파일 헤더에 `SYNTHESIZED` 표기가 있습니다. 유비쿼터스 언어/서브도메인/바운디드 컨텍스트/애그리거트 표는 특정 도메인을 가정하지 않는 **빈 플레이스홀더 템플릿**이므로, 실제 프로젝트가 정해지면 그 도메인 개념으로 채워 사용하세요(도메인 특화 커스터마이징은 `algo-experts`에서).
- **벤더링 못한 스킬(소스 성격 문제, 환각 아님)**: `sre-engineer`는 지정 소스(sinzin91/awesome-sre-skills, CC0)가 링크 큐레이션 목록이라 벤더 가능한 `SKILL.md`가 없어 스킬을 만들지 않고 카탈로그로만 커버했습니다(`skills/` 미생성). `dba`·`product-planner`도 소스가 에이전트 프로필 중심이라 벤더 스킬 0개이며, 에이전트가 스킬을 겸하거나 카탈로그로 breadth를 보완합니다.
