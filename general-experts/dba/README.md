# DBA (Database Administrator) — general-experts 팩

> 이 팀/프로젝트에 **전담 DBA 역할이 없을 때**, 그 공백을 Agent로 메우기 위한 큐레이션 팩입니다.
> 특정 제품·도메인·기술 스택을 가정하지 않습니다. 관계형 데이터베이스를 쓰는 프로젝트라면 어디에나 적용할 수 있는 범용 역할 팩입니다.

---

## 1) 역할 개요 — 이 Agent에게 무엇을 위임하는가

많은 팀에는 전담 DBA가 없어, 애플리케이션/백엔드 개발자가 스키마 설계·쿼리 작성까지 겸하게 됩니다. 그 결과 **일상적인 DB 리뷰/튜닝 루프**를 돌려 줄 사람이 비어 있기 쉽습니다. 이 팩의 Agent들은 그 공백을 다음 영역에서 메웁니다.

- **스키마 / DDL 리뷰** — 정규화 수준, 데이터 타입 선택, 제약조건, 파티셔닝 전략 검토
- **인덱스 전략** — 복합 인덱스 컬럼 순서, 커버링/부분/표현식 인덱스, 불필요 인덱스 제거
- **슬로우 쿼리 분석** — `EXPLAIN (ANALYZE, BUFFERS)` 실행계획 해석, 병목 진단, 쿼리 리라이팅
- **ORM / 쿼리 빌더 성능 리뷰** — N+1, 페이지네이션, 조인 페치, 배치 사이즈, 생성되는 SQL 점검
- **마이그레이션 위험 분석** — 무중단(zero-downtime) 스키마 변경, 락 영향, 롤백 계획
- **백업 / 복구** — RTO/RPO 목표 설정, PITR(Point-in-Time Recovery), 백업 검증
- **모니터링** — 슬로우 쿼리 추적, 락/블로트 모니터링, 복제 지연 알림, 용량 예측

### 어떤 요청을 어느 Agent에게?

| 상황 | 우선 호출 Agent |
|---|---|
| "이 마이그레이션이 프로덕션에 안전한가?" / HA·백업·복구·RTO/RPO | `database-administrator` |
| "이 SQL/네이티브 쿼리를 어떻게 다시 쓰지?" / 스키마 설계·인덱스·CTE·윈도우 함수 | `sql-pro` |
| "이 슬로우 쿼리 P95를 낮춰줘" / 실행계획·인덱스 처방·캐시 히트율 | `database-optimizer` |
| PostgreSQL 고유 기능(JSONB, VACUUM/autovacuum, 스트리밍 복제, `pg_stat_statements`) | `postgres-pro` |

> 4개 Agent는 초점이 겹치되 서로 다른 각도를 봅니다. 실무에서는 `database-optimizer`(진단) → `sql-pro`(재작성) → `database-administrator`(배포/마이그레이션 안전성) 순으로 물려서 쓰면 리뷰 루프가 완성됩니다.

---

## 2) 추천 구성 표

모두 **VoltAgent/awesome-claude-code-subagents** (⭐ 22.8k, MIT) 레포에서 **실제 바이트 그대로 벤더링**했습니다. 런타임은 Claude Code 서브에이전트 포맷(YAML frontmatter + 시스템 프롬프트)이며, Codex 등 다른 러너에서도 프롬프트 본문을 그대로 재사용할 수 있습니다.

| Agent | 초점 | 소스(owner/repo) | ⭐ | 라이선스 | 런타임 |
|---|---|---|---|---|---|
| `database-administrator` | HA·백업/복구(RTO<1h, RPO<5m)·모니터링·마이그레이션 | VoltAgent/awesome-claude-code-subagents | 22.8k | MIT | Claude Code / Codex |
| `sql-pro` | 스키마 설계·인덱스·복잡 쿼리 최적화·ORM 연동 | VoltAgent/awesome-claude-code-subagents | 22.8k | MIT | Claude Code / Codex |
| `database-optimizer` | 슬로우 쿼리 진단·실행계획·인덱스 처방·캐시 | VoltAgent/awesome-claude-code-subagents | 22.8k | MIT | Claude Code / Codex |
| `postgres-pro` | PostgreSQL 전용 튜닝·복제·PITR·JSONB·VACUUM | VoltAgent/awesome-claude-code-subagents | 22.8k | MIT | Claude Code / Codex |

**Skills**: 이 역할에 대해 별도로 벤더링한 스킬 폴더는 없습니다(위 4개 Agent 프로필이 실질 스킬 역할을 겸함). 절차적 스킬이 필요하면 아래 5번의 "감사 필요" 주의를 참고하세요.

파일 위치:
- `agents/database-administrator.md`
- `agents/sql-pro.md`
- `agents/database-optimizer.md`
- `agents/postgres-pro.md`

---

## 3) 설치 · 사용

### A. Claude Code 프로젝트 서브에이전트로 사용

Claude Code는 `.claude/agents/`(프로젝트 범위) 또는 `~/.claude/agents/`(사용자 범위)의 `*.md` 파일을 서브에이전트로 로드합니다. 이 팩을 그대로 복사하세요.

```bash
# 저장소 루트에서
mkdir -p .claude/agents
cp general-experts/dba/agents/*.md .claude/agents/

# 확인
ls .claude/agents/
# database-administrator.md  database-optimizer.md  postgres-pro.md  sql-pro.md
```

Claude Code 세션에서 호출:

```
> use the database-optimizer subagent to analyze this slow query plan
> @sql-pro  이 ORM 쿼리로 만들어지는 SQL을 리뷰하고 인덱스를 제안해줘
```

각 파일 상단의 `name:` frontmatter(`database-administrator`, `sql-pro`, `database-optimizer`, `postgres-pro`)가 호출 이름입니다. `description`에 트리거 조건이 있어 적절한 상황에서 자동 위임되기도 합니다.

### B. 원본 레포에서 직접 받기 (breadth 확장용)

이 팩은 DBA 초점 4개만 벤더링했습니다. DB 인접 역할(예: `data-engineer`, `sre-engineer`, `backend-developer`)까지 넓히려면 원본을 클론하세요.

```bash
git clone https://github.com/VoltAgent/awesome-claude-code-subagents.git
ls awesome-claude-code-subagents/categories/
# 03-infrastructure/ , 02-language-specialists/ , 05-data-ai/ 등
```

### C. gstack 연계

garrytan/gstack(MIT)에는 **DBA 역할에 직접 대응하는 슬래시 명령이 없습니다**(해당 없음). DB 스키마/마이그레이션을 코드 레벨에서 다룰 때 gstack의 프로젝트 스캐폴딩 명령을 참고 링크로만 소개합니다.
- 링크: https://github.com/garrytan/gstack — 벤더링하지 않으며, 필요 시 명령만 참조하세요.

---

## 4) 활용 시나리오

특정 도메인·스택을 가정하지 않은 일반적인 DBA 업무 흐름 예시입니다.

- **인덱스 설계 리뷰** (`sql-pro` + `database-optimizer`) — 자주 쓰는 조회 패턴에 맞춰 복합 인덱스 컬럼 순서·부분 인덱스를 리뷰받고, `EXPLAIN ANALYZE`로 seq scan → index scan 전환을 확인합니다.
- **N+1 / ORM 쿼리 점검** (`sql-pro`) — 목록 화면에서 반복 발생하는 N+1을 조인 페치·배치 사이즈·페이지네이션(카운트 쿼리 분리, keyset pagination) 관점에서 진단하고 생성 SQL을 점검합니다.
- **무중단 마이그레이션 리뷰** (`database-administrator`) — 컬럼 추가·백필 마이그레이션의 락 영향(ACCESS EXCLUSIVE 회피, `CREATE INDEX CONCURRENTLY`), 배치 백필, 롤백 절차, 스테이징 선검증을 배포 전에 리뷰합니다.
- **백업/복구·모니터링 부트스트랩** (`database-administrator` + `postgres-pro`) — RTO/RPO 목표를 수립하고, WAL 아카이빙 + PITR 셋업과 복구 리허설을 문서화하며, 상위 지연 쿼리 Top-N 추적 루틴으로 최소 모니터링을 갖춥니다.

---

## 5) 라이선스 · 보안 주의

- **벤더링 라이선스**: 4개 Agent 파일 모두 `VoltAgent/awesome-claude-code-subagents` (MIT) 에서 가져왔습니다. 각 파일 최상단에 `SOURCE / REPO / LICENSE / RETRIEVED` 출처 헤더(HTML 주석)를 붙였고, 그 아래는 원본을 **변경 없이** 그대로 보존했습니다. 재배포 시 MIT 저작권 고지를 유지하세요.
- **catalogOnly / 벤더 불가 항목**: 이 역할에는 catalogOnly로 지정된 레포가 없습니다. gstack은 링크로만 소개하며 벤더링하지 않았습니다.
- **스크립트 감사 경고**: 벤더링한 4개 파일은 **프롬프트 텍스트(.md)뿐**이며 실행 스크립트(`*.sh`, `*.py`)를 포함하지 않습니다. 다만 각 Agent는 프롬프트 내부에서 `Bash` 툴 사용과 "backup automation / failover procedures / recovery testing" 같은 **자동화 스크립트 생성**을 전제로 합니다. Agent가 생성하는 DDL·마이그레이션·백업/failover 스크립트는 **프로덕션 적용 전 반드시 사람이 감사**하고 스테이징에서 검증하세요. 특히:
  - `ALTER TABLE` / 인덱스 생성은 락·소요 시간·복제 지연을 검토(가능하면 `CREATE INDEX CONCURRENTLY`).
  - 백필/삭제 쿼리는 트랜잭션 경계와 롤백 계획을 먼저 확인.
  - 실 데이터 접속 정보/자격증명은 Agent 프롬프트에 넣지 말 것.
- **모델 주의**: 원본 frontmatter는 `model: sonnet`으로 지정되어 있습니다. 런타임/조직 정책에 맞게 조정하세요.

---

### 부록 — 벤더 파일 원본 URL

| 파일 | 원본 URL |
|---|---|
| `agents/database-administrator.md` | https://github.com/VoltAgent/awesome-claude-code-subagents/blob/main/categories/03-infrastructure/database-administrator.md |
| `agents/sql-pro.md` | https://github.com/VoltAgent/awesome-claude-code-subagents/blob/main/categories/02-language-specialists/sql-pro.md |
| `agents/database-optimizer.md` | https://github.com/VoltAgent/awesome-claude-code-subagents/blob/main/categories/05-data-ai/database-optimizer.md |
| `agents/postgres-pro.md` | https://github.com/VoltAgent/awesome-claude-code-subagents/blob/main/categories/05-data-ai/postgres-pro.md |
