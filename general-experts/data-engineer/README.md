# Data Engineer 전문가 팩 (general-experts/data-engineer)

> 팀에 아직 없는 **Data Engineer** 역할의 공백을, 공개 Claude Code 서브에이전트/스킬을 큐레이션·벤더링해서 메우는 팩입니다.
> **데이터 파이프라인·모델링·품질을 실무로 끌고 가는 관점**으로 구성했습니다.

---

## 1) 역할 개요 — 이 Agent에게 무엇을 위임하는가

제품이 운영되면 사용자 행동·트랜잭션·시스템 이벤트가 계속 쌓입니다. 이 원천 데이터를 "분석 가능한 자산"으로 바꾸는 일이 Data Engineer의 몫입니다. 이 팩의 Agent/Skill에게 다음을 위임합니다.

- **데이터 파이프라인 설계 / ETL·ELT**: 원천 이벤트·로그를 수집→정제→적재하는 배치/스트림 파이프라인 설계, 오케스트레이션, SLA·데이터 신선도·무손실 보장.
- **웨어하우스 / 데이터 모델링**: 운영 RDB와 분리된 분석용 스키마(팩트/디멘전, 집계 테이블) 설계, 정규화/비정규화 판단, 파티셔닝.
- **데이터 품질 / 거버넌스**: 스키마 검증, NULL·중복·지연 데이터 처리, 품질 체크, 문서화.
- **배치 / 스트림 처리**: 대용량 로그의 분산 처리(Spark), 스트리밍 집계, 스큐/셔플 최적화.
- **분석 지원(BI)**: 이해관계자가 볼 수 있는 지표·대시보드 정의, 프로덕트 인사이트 도출.
- **(선택) MLOps**: 예측/추천 모델을 붙일 때의 학습 파이프라인·모델 버저닝·모니터링.

> 협업 경계: 제품/데이터 오너는 "무엇을 측정할지 / 어떤 인사이트가 필요한지"를 정하고, 이 팩의 Agent는 "그걸 어떤 파이프라인·모델·쿼리로 구현할지"를 담당하는 그림입니다. DBA/DevOps 역할과는 인접 팩(general-experts의 DBA/SRE)과 나눠 봅니다.

---

## 2) 추천 구성 표

### Agents (VoltAgent/awesome-claude-code-subagents, ⭐ 약 22.8k, MIT)

| Agent | 무엇을 하나 | 소스 (owner/repo) | 라이선스 | 런타임 |
|---|---|---|---|---|
| `data-engineer` | 데이터 플랫폼·ETL/ELT·파이프라인 아키텍처·데이터 레이크/웨어하우스·스트림 처리 (핵심) | VoltAgent/awesome-claude-code-subagents | MIT | Claude Code / 서브에이전트 호환 |
| `data-analyst` | BI·통계 분석·SQL·대시보드·KPI 정의 | VoltAgent/awesome-claude-code-subagents | MIT | Claude Code / 서브에이전트 호환 |
| `mlops-engineer` | ML 인프라·학습 파이프라인·모델 버저닝·실험 추적·모니터링 (ML 모델 확장 시) | VoltAgent/awesome-claude-code-subagents | MIT | Claude Code / 서브에이전트 호환 |

### Skills (Jeffallan/claude-skills, ⭐ 약 10.4k, MIT)

| Skill | 무엇을 하나 | 소스 (owner/repo) | 라이선스 | 런타임 |
|---|---|---|---|---|
| `spark-engineer` | Apache Spark/PySpark 분산 처리, ETL 최적화, 파티셔닝·브로드캐스트 조인·스큐 처리·구조적 스트리밍 | Jeffallan/claude-skills | MIT | Claude Code (Skill) |
| `sql-pro` | SQL 쿼리 최적화, 스키마 설계, 인덱싱, 윈도우 함수/CTE, EXPLAIN ANALYZE, 여러 RDB 방언 차이 대응 | Jeffallan/claude-skills | MIT | Claude Code (Skill) |

> 참고: 두 Skill은 원본 폴더에 `references/*.md`(각 8~20KB, 순수 텍스트) 5개씩을 더 갖고 있습니다. 벤더링은 "역할당 핵심 파일만" 원칙에 따라 **SKILL.md 본체만** 가져왔습니다. 상세 레퍼런스는 아래 카탈로그 링크에서 원본을 참고하세요.

### 카탈로그 전용 (링크만 — 벤더링 안 함)

| 항목 | 용도 | 소스 | 라이선스 | 비고 |
|---|---|---|---|---|
| awesome-agent-skills | dbt/airflow/warehouse/DuckDB 계열 스킬 탐색 카탈로그 | [VoltAgent/awesome-agent-skills](https://github.com/VoltAgent/awesome-agent-skills) | MIT | 벤더링 금지, 탐색용 링크만 |
| DuckDB 공식 스킬 | 로컬/원격 파일(CSV·Parquet·JSON) 쿼리, 스키마 탐색 | [awesome-agent-skills > DuckDB](https://github.com/VoltAgent/awesome-agent-skills#skills-by-duckdb) | (각 스킬 라이선스 확인 필요) | 데이터 애드혹 분석에 유용 |
| gstack (Garry Tan) | Claude Code를 가상 엔지니어링 팀으로 만드는 워크플로 슬래시 명령 모음 | [garrytan/gstack](https://github.com/garrytan/gstack) · [카탈로그](https://github.com/VoltAgent/awesome-agent-skills#skills-by-garry-tan-gstack) | MIT | 이 역할 전용 슬래시 명령은 없음 — 연계 소개만 |

---

## 3) 설치 · 사용

### A. 이 팩을 그대로 쓰기 (이미 벤더링됨)

이 디렉터리(`general-experts/data-engineer/`)에 실제 파일이 들어 있습니다.

```
general-experts/data-engineer/
├── README.md
├── agents/
│   ├── data-engineer.md
│   ├── data-analyst.md
│   └── mlops-engineer.md
└── skills/
    ├── spark-engineer/SKILL.md
    └── sql-pro/SKILL.md
```

- **Agent로 사용**: `agents/*.md`를 프로젝트의 `.claude/agents/` (또는 팀 규칙에 맞는 서브에이전트 디렉터리)로 복사하면, 해당 프로파일이 서브에이전트로 로드됩니다.
- **Skill로 사용**: `skills/<name>/`를 `.claude/skills/<name>/`로 복사하면 Claude Code가 SKILL.md의 `description` 트리거로 자동 로딩합니다.

```bash
# 예시: 이 팩의 스킬을 프로젝트 스킬 디렉터리로 복사
mkdir -p .claude/skills
cp -R general-experts/data-engineer/skills/sql-pro       .claude/skills/
cp -R general-experts/data-engineer/skills/spark-engineer .claude/skills/

# 예시: 에이전트 프로파일 복사
mkdir -p .claude/agents
cp general-experts/data-engineer/agents/data-engineer.md .claude/agents/
```

### B. 원본에서 최신본 받기 (레퍼런스 포함 전체가 필요할 때)

```bash
# 서브에이전트 원본
gh repo clone VoltAgent/awesome-claude-code-subagents
#  → categories/05-data-ai/{data-engineer,data-analyst,mlops-engineer}.md

# 스킬 원본 (references/*.md 포함)
gh repo clone Jeffallan/claude-skills
#  → skills/spark-engineer/  (SKILL.md + references/*.md)
#  → skills/sql-pro/         (SKILL.md + references/*.md)
```

### C. 호출 방법

- Agent: 서브에이전트가 로드된 상태에서 "이벤트 로그 ETL 파이프라인 설계해줘" 같은 요청을 하면 `data-engineer` 프로파일이 개입합니다. 각 파일의 `description`(예: 파이프라인/ETL/데이터 인프라)이 라우팅 트리거입니다.
- Skill: `sql-pro`는 "이 쿼리 왜 느려?", "EXPLAIN ANALYZE 봐줘", "스키마 마이그레이션" 등에, `spark-engineer`는 "Spark 잡 최적화", "셔플 파티션 튜닝", "스트리밍 집계" 등에 자동 트리거됩니다.

---

## 4) 활용 시나리오 (범용)

특정 도메인·스택을 가정하지 않은, 이 역할의 일반적인 업무 예시입니다.

1. **이벤트/로그 ETL·ELT 파이프라인 (`data-engineer`)**
   운영 저장소에 쌓이는 원천 이벤트를 분석 저장소로 흘려보내는 파이프라인 설계. CDC vs 배치 추출, 스키마 진화, 무손실·신선도 SLA, 오케스트레이션 방식, 그리고 운영 DB에 분석 부하가 가지 않도록 읽기 분리·집계 테이블 전략까지.

2. **분석용 스키마 모델링 + 쿼리 튜닝 (`sql-pro` + `data-engineer`)**
   핵심 지표를 위한 팩트/디멘전 스키마 설계, 윈도우 함수·CTE 기반 집계, 커버링 인덱스, `EXPLAIN ANALYZE`로 느린 리포트 쿼리 최적화. 여러 RDB 방언 차이도 함께 커버.

3. **대용량 로그 배치·스트림 처리 (`spark-engineer`)**
   로그가 커지면 PySpark로 집계·백필. broadcast join, salting(데이터 스큐 완화), 캐싱 패턴을 응용하고, 구조적 스트리밍으로 실시간 대시보드용 집계까지.

4. **지표·대시보드 정의 (`data-analyst`)**
   이해관계자가 원하는 KPI를 실제 SQL/집계 스펙으로 번역하고, 임베드할 분석 뷰의 쿼리 성능까지 챙깁니다.

---

## 5) 라이선스 · 보안 주의

- **벤더링한 파일 (모두 MIT, 출처 헤더 포함):**
  - `agents/*.md` — VoltAgent/awesome-claude-code-subagents (MIT)
  - `skills/*/SKILL.md` — Jeffallan/claude-skills (MIT)
  - 각 파일 최상단 HTML 주석에 원본 URL·레포·라이선스·취득일(2026-07-04)을 명시했으며, 그 아래 본문은 **원본 바이트 그대로** 붙였습니다(내용 무변경).

- **벤더링하지 않은 것 (링크만):**
  - `awesome-agent-skills`(카탈로그 전용) — 절대 복사하지 않고 탐색 링크로만 사용.
  - 각 Skill 원본의 `references/*.md` — 순수 텍스트지만 "핵심 파일만" 원칙에 따라 미벤더링. 필요 시 원본 레포에서 참조.
  - DuckDB / 기타 카탈로그 스킬 — 개별 스킬 라이선스는 사용 전 반드시 확인.

- **스크립트 감사 주의:**
  - 이번에 벤더링한 5개 파일은 **전부 Markdown 텍스트**이며 실행 스크립트(`*.sh`/`*.py`)를 포함하지 않습니다(감사 후 벤더링).
  - 단, `Jeffallan/claude-skills` **레포 전체**에는 `scripts/` 등 실행 코드가 존재합니다. 원본에서 스킬 폴더 전체(레퍼런스 포함)를 clone 해 쓸 경우, 포함된 스크립트/도구는 **실행 전 반드시 코드 감사**하세요. 이 팩은 스크립트를 일절 가져오지 않았습니다.
  - 벤더링한 SKILL.md의 코드 예제(PySpark/SQL)는 **참고용 스니펫**입니다. 운영 DB/클러스터에 적용하기 전 데이터량·인덱스·권한을 검증하세요.

- **라이선스 준수:** MIT 조건상 출처·라이선스 표기를 유지해야 하며(헤더로 충족), 재배포 시에도 이 표기를 제거하지 마세요.
