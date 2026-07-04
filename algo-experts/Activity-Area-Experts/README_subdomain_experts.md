# Algorithm Problem Solving Subdomain Expert Skills

이 폴더는 **Algorithm Problem Solving Domain Architect**의 하위 전문가(child specialist) 스킬을 담고 있다.

parent architect는 제품 도메인 프레이밍, 제품 skeleton, subdomain 관계, MVP 경계, 기획자 커뮤니케이션을 계속 책임져야 한다.

이 child expert들은 알고리즘 문제 풀이 제품의 특정 영역에 대해 더 깊은 렌즈를 제공한다.

## 권장 계층 구조

```text
Algorithm Problem Solving Domain Architect
├─ Problem Solving Lifecycle Expert
├─ Learning & Retention Expert
├─ Practice & Recommendation Expert
├─ Judge & Submission Expert
├─ Explanation & Editorial Expert
├─ AI Assistance & Integrity Expert
├─ Assessment & Contest Expert
├─ Study Group & Social Expert
├─ Product Metrics & Operations Expert
├─ Legal / Policy / Content Rights Expert
├─ Engineering Integration Expert
└─ Algorithm Concept & Pattern Taxonomy Expert
```

## 파일 목록

| File | Specialist | 사용 시점 |
|---|---|---|
| `aps_problem_solving_lifecycle_expert.skill.md` | Problem Solving Lifecycle Expert | 실제 사람의 풀이 흐름과 막히는 단계를 매핑해야 할 때 |
| `aps_learning_retention_expert.skill.md` | Learning & Retention Expert | AC, 이해, 숙달(mastery), 파지(retention), 전이(transfer)를 구분해야 할 때 |
| `aps_practice_recommendation_expert.skill.md` | Practice & Recommendation Expert | 사용자가 다음에 어떤 문제를 풀어야 하는지와 그 이유를 정해야 할 때 |
| `aps_judge_submission_expert.skill.md` | Judge & Submission Expert | submission, verdict, judge 동기화, 검증 신호를 다뤄야 할 때 |
| `aps_explanation_editorial_expert.skill.md` | Explanation & Editorial Expert | hint, 설명, editorial, walkthrough, 리뷰 프롬프트를 설계해야 할 때 |
| `aps_ai_assistance_integrity_expert.skill.md` | AI Assistance & Integrity Expert | 학습과 integrity를 지키면서 AI hint/디버깅/리뷰를 설계해야 할 때 |
| `aps_assessment_contest_expert.skill.md` | Assessment & Contest Expert | practice vs mock/contest/interview/assignment 모드 규칙을 정의해야 할 때 |
| `aps_study_group_social_expert.skill.md` | Study Group & Social Expert | 그룹 과제, accountability, peer review, 소셜 러닝을 설계해야 할 때 |
| `aps_product_metrics_operations_expert.skill.md` | Product Metrics & Operations Expert | 성공 지표, event taxonomy, 검증 신호, 운영 건전성이 필요할 때 |
| `aps_legal_policy_content_rights_expert.skill.md` | Legal / Policy / Content Rights Expert | 콘텐츠·플랫폼·프라이버시·contest·assignment 정책 risk를 식별해야 할 때 |
| `aps_engineering_integration_expert.skill.md` | Engineering Integration Expert | 제품 도메인 선택을 integration/reliability 함의로 옮겨야 할 때 |
| `aps_algorithm_concept_taxonomy_expert.skill.md` | Algorithm Concept & Pattern Taxonomy Expert | 개념 taxonomy, prerequisite, tag, pattern, 난이도 차원이 필요할 때 |

## 설계 원칙

이 스킬들은 제품을 **DDD 연습**으로 만들기 위한 것이 **아니다**.

이 스킬들은 제품 팀이 다음을 하도록 돕기 위한 것이다:

1. 알고리즘 문제 풀이 도메인을 이해하고,
2. 요구사항을 명확히 하고,
3. 기획자·엔지니어와 소통하고,
4. 범위(scope) 결정을 내리고,
5. risk를 조기에 식별하고,
6. 일관된 제품 skeleton을 구축하도록.

DDD 개념은 유용할 때 사용할 수 있지만, 기본 산출물은 아니다.

## 로딩 규칙 권장

제품 방향이 모호할 때는 먼저 parent architect를 사용한다.

질문이 특정 subdomain에 명확히 관한 것일 때는 child expert를 사용한다.

여러 child expert가 관련될 때는 parent architect가 관계와 trade-off를 조율해야 한다.
