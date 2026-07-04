# algo-experts skills

알고리즘 문제 풀이 **제품**을 설계하기 위한 커스텀 Claude Agent Skill 모음입니다.
각 스킬은 `<slug>/SKILL.md`(YAML frontmatter + 본문) 형식이며, 원본 전문가 문서
(`../Algorithm-Problem-Solving-Product-Domain-Architect.md`, `../Activity-Area-Experts/*.skill.md`)의
**본문을 바이트 단위로 보존**하고 그 위에 `name` / `description` frontmatter만 부여해 생성했습니다.

> 이 스킬들은 알고리즘 문제를 **푸는** 도구가 아니라, 알고리즘 문제 풀이 제품의
> 도메인 프레이밍·요구사항·범위(MVP)·리스크를 정의하기 위한 **제품 도메인 전문가**입니다.

## 계층

`aps-domain-architect`(parent) 아래에 12개 subdomain 전문가(child)가 있습니다.
제품 방향이 모호하면 parent를 먼저, 질문이 특정 subdomain에 명확하면 child를 사용합니다.

| Skill (slug) | Specialist | 사용 시점 |
|---|---|---|
| `aps-domain-architect` | Algorithm Problem Solving Domain Architect | **(parent)** 제품 도메인 프레임·skeleton·subdomain 관계·MVP 경계를 잡아야 할 때 |
| `aps-problem-solving-lifecycle` | Problem Solving Lifecycle Expert | 실제 사람의 풀이 흐름과 막히는 단계를 매핑해야 할 때 |
| `aps-learning-retention` | Learning & Retention Expert | AC·이해·숙달(mastery)·파지(retention)·전이(transfer)를 구분해야 할 때 |
| `aps-practice-recommendation` | Practice & Recommendation Expert | 다음에 어떤 문제를 풀지와 그 이유를 정해야 할 때 |
| `aps-judge-submission` | Judge & Submission Expert | submission·verdict·judge 동기화·검증 신호를 다뤄야 할 때 |
| `aps-explanation-editorial` | Explanation & Editorial Expert | hint·설명·editorial·walkthrough·리뷰 프롬프트를 설계해야 할 때 |
| `aps-ai-assistance-integrity` | AI Assistance & Integrity Expert | 학습·integrity를 지키며 AI hint/디버깅/리뷰를 설계해야 할 때 |
| `aps-assessment-contest` | Assessment & Contest Expert | practice vs mock/contest/interview/assignment 모드 규칙을 정의해야 할 때 |
| `aps-study-group-social` | Study Group & Social Expert | 그룹 과제·accountability·peer review·소셜 러닝을 설계해야 할 때 |
| `aps-product-metrics-operations` | Product Metrics & Operations Expert | 성공 지표·event taxonomy·검증 신호·운영 건전성이 필요할 때 |
| `aps-legal-policy-content-rights` | Legal / Policy / Content Rights Expert | 콘텐츠·플랫폼·프라이버시·contest·assignment 정책 risk를 식별해야 할 때 |
| `aps-engineering-integration` | Engineering Integration Expert | 제품 도메인 선택을 integration/reliability 함의로 옮겨야 할 때 |
| `aps-algorithm-concept-taxonomy` | Algorithm Concept & Pattern Taxonomy Expert | 개념 taxonomy·prerequisite·tag·pattern·난이도 차원이 필요할 때 |

## 활성화(설치)

이 스킬들은 레포 루트의 `.claude/skills/<slug>/` 에도 동일하게 설치되어 있어,
이 프로젝트에서 Claude Code가 바로 인식·자동 로딩합니다. 원본 문서
(`../Activity-Area-Experts/*.skill.md`, 번들, `README_subdomain_experts.md`)는 카탈로그로 그대로 보존됩니다.
