# 기획자 (Product Planner / PM) 전문가 팩

> 이 팩은 PRD 작성, 문제 정의, 사용자 스토리, 수용 기준(AC), 로드맵/우선순위, 지표 설계를 담당하는 "기획자" 역할을 **Claude Code 서브에이전트**로 메운다. 아직 무엇을 만들지 정해지지 않은 팀에서도 바로 쓸 수 있도록 특정 제품·도메인·스택을 가정하지 않는다.

- **메우려는 공백**: 제품 기획(PM/PO) — 요구사항을 정의하고, 무엇을 왜 언제 만들지 결정하고, 성공을 지표로 검증하는 사람

---

## 1) 역할 개요 — 이 Agent에게 무엇을 위임하는가

이 팩의 에이전트들에게는 "코드"가 아니라 **"무엇을 만들지에 대한 결정과 문서"**를 위임한다.

| 위임 업무 | 담당 에이전트 | 산출물 예시 |
|---|---|---|
| 제품 전략·로드맵·기능 우선순위 | `product-manager` | 분기 로드맵, RICE 우선순위표, North Star 지표 |
| 백로그 정리·리파인먼트·스토리 준비 | `backlog-grooming` | 스프린트 준비된(Ready) 스토리, 추정치, DoR 체크리스트 |
| 리스크 가정 발굴·검증 우선순위 | `assumption-mapping` | VUBF 가정표, 최우선 검증 실험 3~5개 |
| 애자일 진행·회고·임피디먼트 제거 | `scrum-master` | 스프린트 계획, 회고 액션, 번다운 진단 |

이 네 에이전트는 서로 물려 있다: `assumption-mapping`으로 리스크를 걸러내고 → `product-manager`가 우선순위/로드맵을 정하고 → `backlog-grooming`이 스프린트 준비 스토리로 다듬고 → `scrum-master`가 실행 사이클을 돌린다.

---

## 2) 추천 구성 표

| 구성요소 | 종류 | 소스 (owner/repo) | ⭐ | 라이선스 | 런타임 | 벤더링 |
|---|---|---|---|---|---|---|
| `product-manager` | Agent | VoltAgent/awesome-claude-code-subagents | ~22.8k | MIT | Claude Code | ✅ `agents/` |
| `backlog-grooming` | Agent | VoltAgent/awesome-claude-code-subagents | ~22.8k | MIT | Claude Code | ✅ `agents/` |
| `assumption-mapping` | Agent | VoltAgent/awesome-claude-code-subagents | ~22.8k | MIT | Claude Code | ✅ `agents/` |
| `scrum-master` | Agent | VoltAgent/awesome-claude-code-subagents | ~22.8k | MIT | Claude Code | ✅ `agents/` |

### 카탈로그 전용 (링크만 — 벤더링 금지)

| 소스 | ⭐ | 라이선스 | 이유 / 내용 |
|---|---|---|---|
| [deanpeters/Product-Manager-Skills](https://github.com/deanpeters/Product-Manager-Skills) | ~5.5k | CC BY-NC-SA 4.0 (NOASSERTION) | **비상업 라이선스 → 벤더링 금지.** 52개 PM 스킬(페르소나, JTBD, PRD, 실험 설계 등). 학습·참조용으로만 열람 |
| [Digidai/product-manager-skills](https://github.com/Digidai/product-manager-skills) | ~117 | NOASSERTION (불명확) | **라이선스 불명확 → 벤더링 금지.** PRD 비판, SaaS 지표, 로드맵 관련 프롬프트. 링크 참조만 |
| [github/awesome-copilot](https://github.com/github/awesome-copilot) | ~36k | MIT | Producer/PRD 계열 chatmode·agent 링크 모음. 필요 시 개별 파일을 별도 검토 후 벤더링 가능 |

### 연계 도구: gstack 슬래시 명령 (garrytan/gstack, MIT)

벤더링하지 않고 **명령/링크로만** 연계한다. [garrytan/gstack](https://github.com/garrytan/gstack)

| 명령 | 용도 |
|---|---|
| `/office-hours` | CEO식 제품 리뷰 — 결정 사항을 날카롭게 압박 검증 |
| `/plan-ceo-review` | 계획을 경영자 관점에서 사전 리뷰 |
| `/spec` | 기능 명세 초안 생성 |
| `/retro` | 스프린트 회고 진행 |

---

## 3) 설치·사용

### 이 팩(로컬 벤더링본) 사용
이 저장소에 이미 4개 에이전트가 `agents/` 아래에 벤더링되어 있다. Claude Code 프로젝트에서 서브에이전트로 인식시키려면 프로젝트의 `.claude/agents/`로 복사하거나 심볼릭 링크한다.

```bash
# 프로젝트 루트에서
mkdir -p .claude/agents
cp general-experts/product-planner/agents/*.md .claude/agents/
```

그런 다음 Claude Code 세션에서 역할을 지목해 호출한다:

```
> product-manager 에이전트로 이번 분기 로드맵과 North Star 지표를 잡아줘
> assumption-mapping 으로 새 기능의 리스크 가정을 뽑아줘
> backlog-grooming 으로 이번 스프린트 백로그를 Ready 상태로 다듬어줘
```

### 원본에서 직접 가져오기 (선택)

```bash
# 특정 파일만
gh api "repos/VoltAgent/awesome-claude-code-subagents/contents/categories/08-business-product/product-manager.md" \
  --jq '.content' | base64 -d > product-manager.md

# 또는 raw
curl -sL "https://raw.githubusercontent.com/VoltAgent/awesome-claude-code-subagents/main/categories/08-business-product/product-manager.md"
```

### gstack 연계 (선택)
gstack의 슬래시 명령은 별도 설치가 필요하다. [garrytan/gstack](https://github.com/garrytan/gstack) README를 따라 설치한 뒤 `/spec`, `/office-hours`, `/retro` 등을 제품 리뷰 루틴에 편입한다.

---

## 4) 활용 시나리오

특정 도메인·스택을 가정하지 않는 일반 업무 예시:

- **새 기능 PRD 만들기**: `assumption-mapping`으로 가장 약한 근거를 가진 가정부터 검증 실험을 설계 → `product-manager`로 사용자 스토리와 수용 기준(AC) 작성 → `backlog-grooming`으로 스프린트 크기(≤1 스프린트)로 쪼개고 추정.
- **기능 우선순위 결정**: `product-manager`의 **RICE / Kano** 프레임으로 후보 기능을 점수화하고 이해관계자 정렬 문서로 사용.
- **지표 설계**: `product-manager`의 analytics 섹션으로 North Star와 그 하위 **funnel/cohort** 지표를 정의하고, 로그·이벤트에서 뽑을 수 있는 형태로 명세.
- **스프린트 운영**: `scrum-master`로 계획·회고·임피디먼트 추적을 구조화하고, `backlog-grooming`의 **Definition of Ready 체크리스트**로 스토리의 착수 가능 여부를 게이트. 필요 시 gstack `/office-hours`로 스프린트 종료 결정을 압박 검증.

---

## 5) 라이선스·보안 주의

### 벤더링 가능 여부
- ✅ **벤더링됨 (MIT)**: `product-manager`, `backlog-grooming`, `assumption-mapping`, `scrum-master` — 전부 [VoltAgent/awesome-claude-code-subagents](https://github.com/VoltAgent/awesome-claude-code-subagents) `categories/08-business-product/` 원본 바이트. 각 파일 상단에 `SOURCE / REPO / LICENSE / RETRIEVED` 출처 헤더 부착.
- 🚫 **벤더링 금지**: `deanpeters/Product-Manager-Skills` (CC BY-NC-SA 4.0, **비상업** 조항). 상업/제품 배포 맥락에서 복제·재배포 불가. 링크 참조만.
- 🚫 **벤더링 금지**: `Digidai/product-manager-skills` (라이선스 명시 없음 = NOASSERTION). 라이선스가 명확해지기 전까지 복제 금지. 링크 참조만.
- ⚠️ `github/awesome-copilot` (MIT)는 개별 파일 단위로만 검토 후 벤더링. 이번 팩에서는 링크만 등록.

### 스크립트 감사 경고
- 이번에 벤더링한 4개 파일은 **전부 순수 마크다운(프롬프트) 텍스트**이며 실행 스크립트(`*.sh`, `*.py`, 툴 스크립트)를 포함하지 않는다 → 실행 감사 불필요.
- gstack 슬래시 명령은 **원본 저장소에서 별도 설치**해야 하며, 설치 전 스크립트/훅을 직접 감사할 것. 이 팩은 gstack 코드를 벤더링하지 않는다(명령 이름/링크만 소개).
- 원본 에이전트 프론트매터의 `tools:`에 `WebFetch`, `WebSearch`가 포함되어 있다. 네트워크 접근을 원치 않으면 프로젝트 정책에서 해당 툴 권한을 제한하라.

---

### 출처 요약
- 벤더 원본: https://github.com/VoltAgent/awesome-claude-code-subagents/tree/main/categories/08-business-product (MIT)
- 조회일(RETRIEVED): 2026-07-04
