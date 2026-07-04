# DevOps Engineer — general-experts 팩

> 이 팀/프로젝트에 아직 없는 **DevOps Engineer** 역할을 Agent + Skill 조합으로 메우기 위한 큐레이션 팩입니다.
> 원칙: **읽기전용 리뷰 → 변경 계획 제시 → 사람 승인 → 적용(apply)**. 에이전트가 인프라를 임의로 바꾸지 않고, 항상 계획을 먼저 보여주고 사람의 승인을 받은 뒤에만 적용하도록 운용합니다.

---

## 1) 역할 개요 — 이 Agent에게 무엇을 위임하는가

전담 DevOps/인프라 엔지니어를 두기 어려운 팀이 많습니다. 이 팩은 그 공백을 메꿔 다음을 위임할 수 있게 합니다.

- **컨테이너화**: 애플리케이션을 위한 멀티스테이지 Dockerfile 작성/리뷰, 이미지 슬림화·보안 하드닝.
- **CI/CD 파이프라인**: GitHub Actions 워크플로 스캐폴딩(빌드·테스트·이미지 push·배포), 시크릿/권한 최소화 리뷰.
- **IaC(Infrastructure as Code)**: Terraform으로 데이터베이스·네트워크·런타임 인프라를 코드화, `plan` 승인 게이트 강제.
- **Kubernetes(선택/도입 검토)**: Deployment/Service/Ingress/ConfigMap/HPA 매니페스트 생성 및 검증.
- **배포 자동화 & 롤백 전략**: blue-green / canary / rolling 전략 설계, 실패 시 자동 롤백·MTTR 단축.
- **인프라 변경 리뷰**: PR 단위의 Dockerfile/워크플로/`.tf`/`k8s.yaml` 변경을 사람 대신 1차 검토하고 위험 지점을 지적.

핵심 운용 방식은 **read-only 리뷰 우선**입니다. 에이전트는 먼저 현재 상태를 분석하고, 변경안을 텍스트/디프로 제시하며, `terraform apply`·`kubectl apply`·프로덕션 배포 같은 파괴적 동작은 사람이 승인한 뒤에만 실행합니다.

---

## 2) 추천 구성 표

### Agents (`agents/`)

| Agent | 초점 | 소스 (owner/repo) | ⭐ | 라이선스 | 런타임 |
|---|---|---|---|---|---|
| `devops-engineer` | 인프라 자동화·CI/CD·컨테이너 전반의 제너럴리스트 | VoltAgent/awesome-claude-code-subagents | 22.8k | MIT | Claude Code (subagent) |
| `deployment-engineer` | 배포 파이프라인·릴리스 오케스트레이션·**롤백/GitOps** | VoltAgent/awesome-claude-code-subagents | 22.8k | MIT | Claude Code (subagent) |
| `terraform-engineer` | IaC·모듈 설계·**state 관리·plan 승인 게이트** | VoltAgent/awesome-claude-code-subagents | 22.8k | MIT | Claude Code (subagent) |

### Skills (`skills/`)

| Skill | 초점 | 소스 (owner/repo) | ⭐ | 라이선스 | 런타임 |
|---|---|---|---|---|---|
| `dockerfile-generator` | 멀티스테이지·보안 하드닝 Dockerfile 생성 | akin-ozer/cc-devops-skills | 260 | Apache-2.0 | Claude Code / Codex (skill) |
| `github-actions-generator` | GitHub Actions 워크플로·custom action 스캐폴딩 | akin-ozer/cc-devops-skills | 260 | Apache-2.0 | Claude Code / Codex (skill) |
| `terraform-generator` | 프로덕션급 Terraform HCL 생성 | akin-ozer/cc-devops-skills | 260 | Apache-2.0 | Claude Code / Codex (skill) |
| `k8s-yaml-generator` | Kubernetes 매니페스트 생성·검증 | akin-ozer/cc-devops-skills | 260 | Apache-2.0 | Claude Code / Codex (skill) |

> ⭐ 수치는 2026-07-04 기준 레포 스타 수(전체 레포 기준)이며, 개별 파일이 아닌 저장소의 규모 지표입니다.

### 이 팩에서 벤더링한 것 vs. 링크만 한 것

- **벤더링(실제 파일 포함)**: 위 표의 Agent 3개 + Skill 4개 (원본 바이트 그대로, 출처 헤더 부착).
- **벤더링한 skill의 실행 스크립트(`scripts/*.sh` 등)는 포함하지 않았습니다** — SKILL.md 텍스트만 가져왔습니다. (아래 5절 보안 주의 참고)
- **카탈로그 전용(링크만)**: Jeffallan/claude-skills, gstack 슬래시 명령 (아래 참고).

---

## 3) 설치 · 사용

### 3-1. 저장소 클론 후 바로 사용

이 팩은 이미 레포에 벤더링되어 있으므로 별도 다운로드 없이 파일을 참조하면 됩니다.

```bash
# 레포 루트 기준 경로
general-experts/devops-engineer/
├── README.md
├── agents/
│   ├── devops-engineer.md
│   ├── deployment-engineer.md
│   └── terraform-engineer.md
└── skills/
    ├── dockerfile-generator/SKILL.md
    ├── github-actions-generator/SKILL.md
    ├── terraform-generator/SKILL.md
    └── k8s-yaml-generator/SKILL.md
```

### 3-2. Claude Code 프로젝트에 Agent/Skill로 설치

```bash
# 프로젝트 단위 서브에이전트로 설치 (해당 리포지토리에서 작업 시)
mkdir -p .claude/agents .claude/skills
cp general-experts/devops-engineer/agents/*.md .claude/agents/

# skill은 폴더 단위로 복사 (SKILL.md의 name 프론트매터가 skill 식별자)
cp -R general-experts/devops-engineer/skills/dockerfile-generator .claude/skills/
cp -R general-experts/devops-engineer/skills/github-actions-generator .claude/skills/
cp -R general-experts/devops-engineer/skills/terraform-generator .claude/skills/
cp -R general-experts/devops-engineer/skills/k8s-yaml-generator .claude/skills/
```

- **Agent 호출**: Claude Code에서 "use the deployment-engineer subagent to design a canary rollout for our service"처럼 에이전트 이름으로 위임하거나, 서브에이전트 자동 라우팅에 맡깁니다.
- **Skill 호출**: skill의 `description` 트리거에 맞는 요청(예: "write a multi-stage Dockerfile for our service")을 하면 자동 발동됩니다.

### 3-3. 원본 저장소에서 최신본 받기 (업스트림 갱신 시)

```bash
# 개별 스킬 SKILL.md 최신본
gh api "repos/akin-ozer/cc-devops-skills/contents/devops-skills-plugin/skills/dockerfile-generator/SKILL.md" --jq '.content' | base64 -d

# 서브에이전트 최신본
curl -sL "https://raw.githubusercontent.com/VoltAgent/awesome-claude-code-subagents/main/categories/03-infrastructure/deployment-engineer.md"
```

---

## 4) 활용 시나리오

특정 도메인/스택을 가정하지 않는 일반적인 위임 예시입니다.

- **애플리케이션 컨테이너화** (`dockerfile-generator` + `devops-engineer`): 멀티스테이지 Dockerfile 생성·리뷰. 이미지 크기, non-root 유저, 헬스체크, `.dockerignore`, 시크릿 하드코딩 여부를 점검.
- **CI/CD 파이프라인** (`github-actions-generator` + `deployment-engineer`): PR마다 빌드·테스트, 기본 브랜치 머지 시 이미지 빌드·레지스트리 push·스테이징 배포 워크플로 스캐폴딩. 배포는 canary → 헬스체크 통과 시 승격, 실패 시 자동 롤백 전략으로 설계.
- **인프라 IaC** (`terraform-generator` + `terraform-engineer`): 데이터베이스·네트워크·런타임 리소스를 변수화된 Terraform 모듈로 코드화. **반드시 `terraform plan`을 먼저 출력·리뷰**한 뒤 사람 승인 후에만 `apply`. state는 원격 백엔드 + 잠금(lock) 사용.
- **배포·오토스케일·PR 리뷰 게이트** (`k8s-yaml-generator` + `deployment-engineer` / `devops-engineer`): HPA를 건 Deployment/Service 매니페스트 생성·검증, rolling update maxSurge/maxUnavailable·readiness/liveness probe·PodDisruptionBudget 리뷰. 인프라 변경 PR(Dockerfile/`.yml`/`.tf`/`k8s.yaml`)은 읽기전용 1차 리뷰로 위험 지점(권한 과다, 시크릿 노출, 롤백 불가 구조)을 코멘트하고 사람이 최종 승인.

### gstack 슬래시 명령 연계 (garrytan/gstack, MIT, ⭐ 119k — 링크/명령만, 벤더링 없음)
Garry Tan의 Claude Code 셋업. 릴리스/배포 워크플로를 슬래시 명령으로 표준화하고 싶을 때 참고합니다. 이 팀의 배포 리듬을 다음 명령들과 연계할 수 있습니다.

| 명령 | 용도 | 소스 파일 |
|---|---|---|
| `/ship` | 변경을 검토·정리해 출하(ship)하는 릴리스 흐름 | `ship/SKILL.md` |
| `/land-and-deploy` | 머지(land) 후 배포까지 이어지는 오케스트레이션 | `land-and-deploy/SKILL.md` |
| `/setup-deploy` | 배포 파이프라인 초기 셋업 | `setup-deploy/SKILL.md` |
| `/guard` | 배포/변경 전 가드레일(안전 점검) | `guard/SKILL.md` |

- 저장소: <https://github.com/garrytan/gstack> — 필요한 명령만 골라 참고하거나 자신의 워크플로에 이식. (이 팩에는 벤더링하지 않음)

---

## 5) 라이선스 · 보안 주의

### 라이선스 요약

| 항목 | 라이선스 | 벤더링 | 비고 |
|---|---|---|---|
| akin-ozer/cc-devops-skills | Apache-2.0 | ✅ SKILL.md만 | 출처 헤더 부착, 원본 바이트 보존 |
| VoltAgent/awesome-claude-code-subagents | MIT | ✅ 에이전트 3개 | 출처 헤더 부착, 원본 바이트 보존 |
| Jeffallan/claude-skills | MIT | ❌ 링크만 | 아래 카탈로그 참고 |
| garrytan/gstack | MIT | ❌ 링크/명령만 | 4절 gstack 표 참고 |

모든 벤더링 파일 맨 위에는 다음 형식의 출처 헤더가 있습니다:
`<!-- SOURCE: <URL> | REPO: <owner/repo> | LICENSE: <SPDX> | RETRIEVED: 2026-07-04 -->`

### ⚠️ 스크립트 감사 필요 (실행 스크립트는 벤더링하지 않음)

벤더링한 SKILL.md들은 원본 저장소에서 **실행 스크립트를 함께 제공**하며, 본문에서 이를 호출합니다. **이 팩에는 스크립트를 포함하지 않았고, 사용 전 반드시 감사(audit)해야 합니다.**

- `dockerfile-generator` → `scripts/dockerfile-validate.sh` (미포함)
- `terraform-generator` → `scripts/run_ci_checks.sh` (미포함)
- `k8s-yaml-generator` → `scripts/setup_tools.sh` (미포함, 도구 설치 스크립트 — 특히 주의)
- (그 외 각 skill 폴더의 `scripts/`, `tests/` 는 벤더링 대상에서 제외)

이 스크립트들이 필요하면 원본 저장소(`akin-ozer/cc-devops-skills`)에서 직접 받아 **코드 리뷰 후** 신뢰 경계 안에서만 실행하세요. SKILL.md가 스크립트 경로를 참조하더라도, 미포함 상태에서는 해당 자동 검증 단계가 동작하지 않으니 수동 검증으로 대체합니다.

### 운영 안전 수칙 (read-only 우선)

- `terraform apply`, `kubectl apply`, 프로덕션 배포 등 **파괴적/비가역 동작은 항상 사람 승인 후**에만.
- 에이전트가 생성한 Dockerfile/워크플로/HCL/매니페스트는 **시크릿 하드코딩·과도한 권한(IAM/RBAC)·롤백 불가 구조**를 사람이 최종 확인.
- CI 시크릿은 최소 권한 원칙, OIDC 기반 단기 크리덴셜 우선.

### 카탈로그 전용 (링크만, 벤더링 금지)

- **Jeffallan/claude-skills** [MIT, ⭐ 10.4k] — DevOps skill 모음 (Dockerfile / CI / K8s / Terraform / GitOps / rollback 등 폭넓은 주제).
  <https://github.com/Jeffallan/claude-skills>
  이 팩의 4개 skill로 부족한 breadth(GitOps, rollback 전용 패턴 등)를 보완할 때 참고하세요. 벤더링하지 않았으므로 사용 시 라이선스·스크립트 감사를 직접 수행하세요.

---

### 부록 — 벤더링 출처 원본 URL

- dockerfile-generator: <https://github.com/akin-ozer/cc-devops-skills/blob/main/devops-skills-plugin/skills/dockerfile-generator/SKILL.md>
- github-actions-generator: <https://github.com/akin-ozer/cc-devops-skills/blob/main/devops-skills-plugin/skills/github-actions-generator/SKILL.md>
- terraform-generator: <https://github.com/akin-ozer/cc-devops-skills/blob/main/devops-skills-plugin/skills/terraform-generator/SKILL.md>
- k8s-yaml-generator: <https://github.com/akin-ozer/cc-devops-skills/blob/main/devops-skills-plugin/skills/k8s-yaml-generator/SKILL.md>
- devops-engineer (agent): <https://github.com/VoltAgent/awesome-claude-code-subagents/blob/main/categories/03-infrastructure/devops-engineer.md>
- deployment-engineer (agent): <https://github.com/VoltAgent/awesome-claude-code-subagents/blob/main/categories/03-infrastructure/deployment-engineer.md>
- terraform-engineer (agent): <https://github.com/VoltAgent/awesome-claude-code-subagents/blob/main/categories/03-infrastructure/terraform-engineer.md>
