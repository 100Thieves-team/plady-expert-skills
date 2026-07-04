# UI/UX 디자이너 (UI/UX Designer) — general-experts 팩

> 전담 UI/UX 디자이너가 없는 팀을 위한 팩이다. **사용자 흐름 · 와이어프레임 · 디자인 시스템 · 컴포넌트 규칙 · 접근성(WCAG) · UX 리뷰**의 공백을 Agent + Skill 조합으로 메운다. 화면을 만들 때, 그리고 UX 의사결정을 검토할 때 "옆자리 디자이너"처럼 호출해서 쓴다.

---

## 1) 역할 개요 — 이 Agent에게 무엇을 위임하는가

이 팩의 Agent와 Skill에 다음을 위임한다. 특정 제품/도메인을 가정하지 않고, 어떤 화면 흐름에도 붙여 쓸 수 있는 범용 자산이다.

- **사용자 흐름 & 리서치**: 사용자 여정(journey) 설계, 사용성 테스트 계획, 이탈 지점 분석, 페르소나 정의 → `ux-researcher` 에이전트
- **접근성(WCAG) 검증**: 폼·결과 표시·에디터 등 주요 영역의 키보드 내비게이션, 스크린리더, 색 대비 감사 → `accessibility-tester` 에이전트 + `accessibility-audit` 스킬
- **디자인 시스템 토대**: 색/간격/타이포/모션 토큰 정의, 다크모드/테마 대응 → `design-token` 스킬
- **컴포넌트 규칙**: 버튼·뱃지·카드·패널 등 컴포넌트 명세(props/state/variant/접근성) 작성 → `component-spec` 스킬
- **폼 UX**: 입력 폼·회원가입·설정 등 폼의 마찰 최소화, 인라인 검증, 멀티스텝 설계 → `form-design` 스킬

> 요약: **"만들기 전 결정(리서치·토큰·명세)"과 "만든 후 검증(접근성·UX 리뷰)"** 두 축을 모두 커버한다.

---

## 2) 추천 구성 표

| 유형 | 이름 | 무엇을 하나 | 소스 (owner/repo) | ⭐ | 라이선스 | 런타임 |
|---|---|---|---|---|---|---|
| Agent | `ux-researcher` | 사용자 리서치·사용성 테스트·저니맵·페르소나 | VoltAgent/awesome-claude-code-subagents | MIT | Claude Code (subagent) |
| Agent | `accessibility-tester` | WCAG 2.1 AA 감사, 스크린리더/키보드 검증 | VoltAgent/awesome-claude-code-subagents | MIT | Claude Code (subagent) |
| Skill | `accessibility-audit` | WCAG POUR 기반 감사 + 심각도/조치 | Owl-Listener/designer-skills | MIT | Claude Code / Codex (SKILL.md) |
| Skill | `design-token` | 디자인 토큰 아키텍처(global/alias/component) | Owl-Listener/designer-skills | MIT | Claude Code / Codex (SKILL.md) |
| Skill | `component-spec` | 컴포넌트 명세(anatomy/변형/상태/접근성) | Owl-Listener/designer-skills | MIT | Claude Code / Codex (SKILL.md) |
| Skill | `form-design` | 폼 마찰 최소화·검증·멀티스텝 UX | Owl-Listener/designer-skills | MIT | Claude Code / Codex (SKILL.md) |

> ⭐(star) 수치는 레포가 시점에 따라 변하므로 의도적으로 비워 두었다. 최신 값은 각 GitHub 레포에서 직접 확인한다. 두 레포 모두 MIT.

### 카탈로그 전용 (벤더링 금지 — 링크만)

| 이름 | 소스 | 라이선스 | 왜 링크만인가 |
|---|---|---|---|
| ux-ui-agent-skills | [plugin87/ux-ui-agent-skills](https://github.com/plugin87/ux-ui-agent-skills) | **NO LICENSE** | 라이선스 표기가 없어 재배포/벤더링 불가. Senior Design Architect 페르소나, **DTCG 디자인 토큰**, **WCAG 2.2 감사** 등 참고 가치는 높으니 아이디어 참조용으로만 열람. |

### gstack 연계 슬래시 명령 (벤더링 불필요)

[garrytan/gstack](https://github.com/garrytan/gstack) (MIT)는 디자인 워크플로 슬래시 명령을 제공한다. 프론트엔드 작업 시 gstack을 함께 설치하면 아래 명령을 바로 쓸 수 있다.

| 명령 | 용도 |
|---|---|
| `/design` | 화면/기능 디자인 초안 생성 |
| `/design-review` | 구현된 UI를 디자인 관점에서 리뷰 |
| `/design-consultation` | 디자인 방향 상담(옵션 비교) |
| `/design-html` | HTML 프로토타입 산출 |
| `/design-shotgun` | 여러 디자인 시안 병렬 생성 |

> gstack 명령은 이 팩에 복사하지 않는다. gstack 저장소를 별도로 설치해 사용한다(아래 3절 참고).

---

## 3) 설치 · 사용

### 3-1. 이 팩(벤더링된 Skill/Agent) 사용

이 디렉터리는 이미 실제 파일이 벤더링되어 있다. 별도 설치 없이 바로 쓸 수 있다.

```
general-experts/uiux-designer/
├── README.md                       # 이 문서
├── agents/
│   ├── ux-researcher.md            # 서브에이전트 프로필
│   └── accessibility-tester.md     # 서브에이전트 프로필
└── skills/
    ├── accessibility-audit/SKILL.md
    ├── design-token/SKILL.md
    ├── component-spec/SKILL.md
    └── form-design/SKILL.md
```

**Claude Code에서 Skill 로드** — SKILL.md를 프로젝트/개인 스킬 경로에 심볼릭 링크하거나 복사한다.

```bash
# 예: 프로젝트 스킬로 연결
mkdir -p .claude/skills
cp -r general-experts/uiux-designer/skills/* .claude/skills/
```

**Claude Code에서 Agent 등록** — 각 `agents/*.md`는 YAML frontmatter(`name`, `description`, `tools`, `model`)를 가진 서브에이전트 정의다. `.claude/agents/`에 두면 자동 인식된다.

```bash
mkdir -p .claude/agents
cp general-experts/uiux-designer/agents/*.md .claude/agents/
```

호출 예:
- `> ux-researcher 서브에이전트로 주요 화면의 사용성 테스트 계획을 세워줘`
- `> accessibility-tester 서브에이전트로 입력 폼의 WCAG AA 위반을 감사해줘`
- 스킬은 대화 중 관련 작업을 요청하면 자동 트리거되거나 이름으로 명시 호출한다: `design-token 스킬로 이 프로젝트의 색/간격 토큰 초안을 만들어줘`

### 3-2. 원본 레포에서 직접 가져오기(업데이트/확장 시)

```bash
# 디자인 스킬 원본 (11개 플러그인, 다수 SKILL.md)
git clone https://github.com/Owl-Listener/designer-skills

# 서브에이전트 컬렉션 원본
git clone https://github.com/VoltAgent/awesome-claude-code-subagents
```

특정 파일만 최신본으로 갱신:

```bash
gh api "repos/Owl-Listener/designer-skills/contents/ui-design/skills/responsive-design/SKILL.md" \
  --jq '.content' | base64 -d
```

### 3-3. gstack 슬래시 명령 설치

```bash
git clone https://github.com/garrytan/gstack
# gstack README의 설치 절차에 따라 슬래시 명령을 Claude Code에 등록
```

---

## 4) 활용 시나리오

특정 도메인/스택을 가정하지 않은 일반 업무 예시다.

- **만들기 전**: `ux-researcher`로 사용자 여정·페르소나·사용성 테스트 계획을 세우고, `design-token`으로 색/간격/타이포 토큰의 3계층(global → alias → component)과 다크모드 대응 토대를 잡는다.
- **구현 직전**: `component-spec`으로 컴포넌트의 props·상태·변형·접근성을 문서화하고, `form-design`으로 입력 폼의 마찰(라벨 노출, blur 시점 인라인 검증, 멀티스텝, 로딩 상태)을 줄인다.
- **구현 후 검증**: `accessibility-audit` 스킬과 `accessibility-tester` 에이전트로 WCAG(색 대비 4.5:1, 색 단독 상태 표시 금지, 키보드 포커스 순서, 스크린리더 낭독)를 감사하고 심각도별 개선 리스트를 백로그로 전환한다.
- **기준 ↔ 실행 분리**: 이 팩의 `component-spec`/`design-token`이 "기준"이 되고, gstack `/design-review`·`/design` 같은 명령이 "리뷰/생성 실행기" 역할을 한다.

---

## 5) 라이선스 · 보안 주의

### 벤더링된 자산 (모두 MIT — 출처 헤더 포함)
- `skills/*` 4종 ← **Owl-Listener/designer-skills** (MIT)
- `agents/*` 2종 ← **VoltAgent/awesome-claude-code-subagents** (MIT)

각 파일 맨 위 HTML 주석에 `SOURCE / REPO / LICENSE / RETRIEVED` 출처 헤더가 붙어 있고, 그 아래는 원본을 **변경 없이** 그대로 담았다. MIT 재배포 조건(저작권·라이선스 고지 유지)을 이 헤더로 충족한다.

### 벤더링 금지 항목
- **plugin87/ux-ui-agent-skills**: 라이선스 파일이 없다(NO LICENSE). 저작권 기본 보호가 적용되므로 **복사/재배포 불가**. 아이디어 참조는 가능하나 코드/텍스트를 이 레포로 가져오지 말 것. README 링크로만 유지.

### 스크립트 감사 경고
- 벤더링한 6개 파일은 모두 **순수 텍스트(SKILL.md / 에이전트 프로필)**이며 실행 스크립트를 포함하지 않는다. 별도 실행 위험 없음.
- 단, 원본 **Owl-Listener/designer-skills** 레포 루트에는 `scripts/` 디렉터리와 각 플러그인의 `commands/`가 존재한다. 이들은 **의도적으로 벤더링하지 않았다**. 만약 향후 원본 레포에서 `*.sh`/`*.py`/툴 스크립트를 추가로 가져올 경우, 실행 전 반드시 **코드 감사(audit)** 후 사용할 것.
- **accessibility-tester** 에이전트는 frontmatter에서 `tools: Read, Grep, Glob, Bash`를 선언한다(Bash 실행 권한). 자동화 스캐너 실행을 유도할 수 있으니, 권한이 민감한 환경에서는 `Bash` 도구 허용 여부를 검토하고 필요 시 tools 목록을 축소해 사용할 것.
- **ux-researcher** 에이전트는 `tools: Read, Grep, Glob, WebFetch, WebSearch`로 외부 네트워크 접근(WebFetch/WebSearch)을 사용한다. 사내 폐쇄망/보안 정책에 맞춰 도구 허용을 조정할 것.

---

*RETRIEVED: 2026-07-04 · 큐레이터: general-experts 워크플로 (UI/UX 디자이너 역할)*
