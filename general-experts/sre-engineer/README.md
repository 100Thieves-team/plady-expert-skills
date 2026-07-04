# SRE Engineer (Site Reliability Engineer) — 전문가 팩

> 이 팀/조직에 존재하지 않는 **SRE 역할**의 공백을 Agent + Skill 조합으로 메우기 위한 큐레이션·벤더링 팩입니다.
> 초점: **SLO/SLI, 에러 버짓, 장애 대응/포스트모템, 알림 정책, 용량 계획, 관측성(Observability)**.

---

## 1) 역할 개요 — 이 Agent에게 무엇을 위임하는가

전담 SRE/DevOps 인력이 없는 팀에서도, 이 팩의 에이전트는 "신뢰성 엔지니어링" 관점의 판단·문서·체크리스트를 대신 수행합니다. 구체적으로 다음을 위임합니다.

- **SLO/SLI 설계**: "핵심 요청 p99 지연 < 2s", "주요 API 가용성 99.9%" 같은 서비스 수준 목표를 정의하고, 그것을 측정할 SLI(성공률/지연/신선도)를 뽑아줍니다.
- **에러 버짓 정책**: 목표 대비 소진율(burn rate)을 기준으로 "기능 개발 vs 안정화" 의사결정 룰을 만들어 줍니다.
- **장애 대응 & 포스트모템**: 프로덕션 장애 발생 시 분류(SEV) → 초동 대응 → 근본원인 분석(RCA) → 재발방지 액션 아이템을 구조화합니다. 비난 없는(blameless) 포스트모템 템플릿을 생성합니다.
- **관측성 설계**: 어떤 메트릭/로그/트레이스를 남길지, RED(Rate·Errors·Duration)/USE 대시보드를 어떻게 구성할지 제안합니다.
- **용량 계획**: 트래픽 증가 시 리소스 모델링과 스케일링 전략을 제시합니다.
- **카오스/복원력 검증**: 장애 주입 실험(가설·블라스트 반경 제어)을 설계해 사고 전에 약점을 찾아냅니다.

| 위임 대상 에이전트 | 언제 부르나 |
| --- | --- |
| `sre-engineer` | SLO/SLI 정의, 에러 버짓 정책 수립, 토일 감소·자동화, 용량 계획 |
| `devops-incident-responder` | 프로덕션 장애가 "지금 발생 중"일 때 초동 진단·복구·포스트모템 |
| `chaos-engineer` | 장애 전에 복원력을 검증하고 싶을 때(게임데이, 장애 주입 실험) |

---

## 2) 추천 구성 표

### 벤더링한 Agent (이 팩에 실제 파일 포함)

| 구성요소 | 파일 | 소스(owner/repo) | ⭐ | 라이선스 | 런타임 |
| --- | --- | --- | --- | --- | --- |
| SRE Engineer | `agents/sre-engineer.md` | VoltAgent/awesome-claude-code-subagents | 22.8k | MIT | Claude Code (subagent) |
| DevOps Incident Responder | `agents/devops-incident-responder.md` | VoltAgent/awesome-claude-code-subagents | 22.8k | MIT | Claude Code (subagent) |
| Chaos Engineer | `agents/chaos-engineer.md` | VoltAgent/awesome-claude-code-subagents | 22.8k | MIT | Claude Code (subagent) |

> 세 파일 모두 순수 마크다운 프롬프트(YAML frontmatter + 지침)이며 실행 스크립트를 포함하지 않습니다. 원본 바이트를 변경 없이 벤더링했고, 각 파일 상단에 `SOURCE/REPO/LICENSE/RETRIEVED` 출처 헤더를 붙였습니다.

### 스킬(Skills) — 벤더링 없음, 디스커버리 허브 링크만

`sinzin91/awesome-sre-skills` (CC0-1.0)를 조회한 결과, 이 레포는 **실제 SKILL.md 파일을 담은 스킬 저장소가 아니라 "SRE 스킬 큐레이션 링크 목록(awesome-list)"** 입니다(53개 스킬을 외부 레포로 링크). 따라서 여기서 벤더링할 SKILL.md가 없어, 아래 4번·5번 카탈로그에 링크로만 소개합니다.

| 스킬 소스 | 소스(owner/repo) | ⭐ | 라이선스 | 런타임 | 처리 |
| --- | --- | --- | --- | --- | --- |
| Awesome SRE Skills (디스커버리 허브) | sinzin91/awesome-sre-skills | 5 | CC0-1.0 | Claude Code / OpenClaw / SkillMD | 링크(허브) |
| Elastic Agent Skills (관측성) | elastic/agent-skills | 525 | Apache-2.0 | Claude Code | **카탈로그 전용(벤더 금지)** |
| gstack `/health` `/investigate` `/retro` | garrytan/gstack | 119k | MIT | Claude Code (슬래시 명령) | 링크/명령만 |

---

## 3) 설치 · 사용

### A. 벤더링된 에이전트 사용 (이 레포에 이미 포함)

Claude Code 프로젝트에서 subagent로 쓰려면 `.claude/agents/` 로 복사합니다.

```bash
# 이 레포 루트 기준
mkdir -p .claude/agents
cp general-experts/sre-engineer/agents/*.md .claude/agents/
```

복사 후 Claude Code에서 자연어로 호출하면 됩니다.

```
> sre-engineer 를 써서 "핵심 API"의 SLO/SLI 초안을 잡아줘
> devops-incident-responder 로 방금 발생한 지연 장애의 초동 진단 절차를 진행해줘
> chaos-engineer 로 워커 프로세스가 죽는 상황의 게임데이 실험을 설계해줘
```

> 각 파일의 YAML frontmatter `name:` 값(`sre-engineer`, `devops-incident-responder`, `chaos-engineer`)이 호출 이름입니다. `tools: Read, Write, Edit, Bash, Glob, Grep`, `model: sonnet` 으로 지정되어 있으니, 조직 정책에 맞게 조정하세요.

### B. 원본에서 직접 가져오기 (업스트림 갱신 시)

```bash
gh api "repos/VoltAgent/awesome-claude-code-subagents/contents/categories/03-infrastructure/sre-engineer.md" --jq '.content' | base64 -d > sre-engineer.md
# 또는
curl -sL "https://raw.githubusercontent.com/VoltAgent/awesome-claude-code-subagents/main/categories/03-infrastructure/sre-engineer.md" -o sre-engineer.md
```

### C. 외부 스킬 설치 (선택 — 4번 카탈로그에서 고른 것)

`awesome-sre-skills` 가 안내하는 방식(레포별 상이):

```bash
# Claude Code 스킬 설치(레포가 SKILL.md/commands 를 제공하는 경우)
claude mcp add-skill https://github.com/OWNER/SKILL-REPO
# 로컬 디렉터리에서
claude mcp add-skill /path/to/skill-directory
```

> 외부 스킬은 **머신에서 코드를 실행**할 수 있습니다. 설치 전 반드시 `SKILL.md`와 동봉 스크립트를 감사하세요(5번 참고).

---

## 4) 활용 시나리오

- **SLO/SLI 초안 잡기 (`sre-engineer`)**: 핵심 사용자 여정을 입력으로 주면 측정 가능한 SLI(성공률/지연/신선도)와 SLO 목표, 다중 창(window) 번레이트 알림 정책 초안을 만들어 줍니다.
- **용량 계획 (`sre-engineer`)**: 현재 리소스 구성(스레드풀·커넥션풀·워커 동시성 등)을 입력으로 주면 피크 트래픽 N배 시 병목과 스케일링 전략을 모델링합니다.
- **장애 초동 대응 & 포스트모템 (`devops-incident-responder`)**: 장애 발생 시 SEV 분류 → 영향 범위 파악 → 최근 배포/변경과의 상관관계 확인 → 롤백/우회 결정 → 복구 후 비난 없는 포스트모템(타임라인 + 5-whys RCA + 액션 아이템) 작성.
- **게임데이로 복원력 검증 (`chaos-engineer`)**: 프로세스 종료·커넥션 고갈·외부 의존성 타임아웃 같은 시나리오를 가설·블라스트 반경 제어와 함께 설계해, 서킷 브레이커/타임아웃/재시도/우아한 성능저하가 실제로 동작하는지 검증.

### gstack 연계 슬래시 명령 (garrytan/gstack, MIT)
팀이 gstack 셋업을 도입했다면, 아래 명령을 SRE 루틴에 그대로 연결할 수 있습니다(이 팩은 링크/명령만 소개, 벤더링하지 않음).
- **`/health`** — 시스템/코드베이스 헬스 점검 루틴(주기 점검에 사용).
- **`/investigate`** — 이슈·장애 조사 워크플로우(장애 초동 조사에 `devops-incident-responder`와 병행).
- **`/retro`** — 회고/포스트모템 루틴(사고 후 액션 아이템 정리에 사용).
- 소스: https://github.com/garrytan/gstack

---

## 5) 라이선스 · 보안 주의

### 벤더링 가능 여부
| 소스 | 라이선스 | 이 팩에서의 처리 |
| --- | --- | --- |
| VoltAgent/awesome-claude-code-subagents | MIT | ✅ 3개 에이전트 벤더링(출처 헤더 부착) |
| sinzin91/awesome-sre-skills | CC0-1.0 | ⛔ 벤더링할 SKILL.md 없음(링크 목록 레포) → 링크만 |
| **elastic/agent-skills** | Apache-2.0 | ⛔ **카탈로그 전용 — 벤더링 금지**(팀 스택 불확실). 링크만 |
| garrytan/gstack | MIT | ⛔ 벤더링 불필요 — 슬래시 명령 링크만 |

### 스크립트 감사 경고 (중요)
- **이 팩에 벤더링된 파일은 안전**: `agents/*.md` 3종은 순수 프롬프트 마크다운으로 실행 스크립트가 없습니다.
- **외부 스킬 설치 시 감사 필수**: 4번 카탈로그의 스킬들(예: `ahmedasmar/devops-claude-skills`는 SLO 계산·로그 분석 등 **스크립트 6종 포함**, `PagerDuty/claude-code-plugins`, `julianobarbosa/claude-code-skills` 등)은 **머신에서 코드를 실행**합니다. 설치 전 반드시 `SKILL.md`/`CLAUDE.md`와 동봉된 `*.sh`/`*.py` 스크립트를 직접 감사하세요. 업스트림 소스는 언제든 변경될 수 있습니다(공급망 리스크).
- 원문 경고(awesome-sre-skills): "Skills execute code on your machine. Source code can change at any time. Always audit the SKILL.md or CLAUDE.md and any scripts before installing."
- **비상업/상업 확인**: 카탈로그 스킬 각각의 라이선스를 도입 전 확인하세요(이 목록의 ⭐/🎖️ 표기는 인기/공식 여부일 뿐 라이선스 보증이 아닙니다).

### 관측성 스킬 카탈로그 (awesome-sre-skills에서 발췌한 실제 링크 — 벤더링 아님, 참고용)
- 디스커버리 허브: https://github.com/sinzin91/awesome-sre-skills (CC0-1.0)
- Incident Response (Anthropic 공식): https://github.com/anthropics/knowledge-work-plugins/tree/main/engineering/skills/incident-response
- Incident Commander (SEV 스코어링·RCA·포스트모템): https://github.com/borghei/Claude-Skills/blob/main/engineering/incident-commander/SKILL.md
- Incident Response / Observability 플러그인(wshobson): https://github.com/wshobson/agents/tree/main/plugins/incident-response · https://github.com/wshobson/agents/tree/main/plugins/observability-monitoring
- PagerDuty 공식 플러그인: https://github.com/PagerDuty/claude-code-plugins
- Chaos Engineering (fault-injection): https://github.com/borghei/Claude-Skills/blob/main/engineering/chaos-engineering/SKILL.md
- AWS Resilience Skills(FIS 카오스): https://github.com/aws-samples/sample-aws-resilience-skill
- SLO 계산·대시보드 스크립트(ahmedasmar, ⚠️스크립트 감사): https://github.com/ahmedasmar/devops-claude-skills
- Grafana 공식 스킬(PromQL/Loki/Tempo/OnCall): https://github.com/grafana/skills
- Prometheus/Grafana/Loki 스킬(julianobarbosa): https://github.com/julianobarbosa/claude-code-skills
- Neon Postgres 신뢰성 스킬(RDB 운영 튜닝): https://github.com/neondatabase/postgres-skills
- Elastic 공식 관측성 스킬(카탈로그 전용): https://github.com/elastic/agent-skills

---

### 부록 — 이 팩의 파일 트리
```
general-experts/sre-engineer/
├── README.md                              # 이 문서(한국어 큐레이션 카탈로그)
└── agents/
    ├── sre-engineer.md                    # 벤더링 (MIT, VoltAgent)
    ├── devops-incident-responder.md       # 벤더링 (MIT, VoltAgent)
    └── chaos-engineer.md                  # 벤더링 (MIT, VoltAgent)
```
