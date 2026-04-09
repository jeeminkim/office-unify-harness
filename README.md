# office-unify-harness
기존 Cursor 프로젝트 통합을 위한 하네스 엔지니어링 적용

# office-unify-harness

`office-unify-harness`는  
`ai_office`와 `dev_support`를 하나의 통합 웹 서비스로 재구성하기 위해 만든  
**하네스 엔지니어링용 방법론 저장소**다.

이 저장소는 실제 앱 코드 저장소가 아니라,  
아래를 표준화하기 위한 **운영 기준 저장소**다.

- 프로젝트 원칙
- 아키텍처 경계
- 마이그레이션 워크플로
- 완료 기준
- Cursor 작업 규칙
- 계획 템플릿
- 프롬프트 템플릿
- 문서/보고 형식

---

# 1. 이 저장소의 목적

현재 목표는 아래 두 프로젝트를 별도 서비스가 아니라  
하나의 서비스로 통합하는 것이다.

- `ai_office`
- `dev_support`

통합의 최종 방향은 다음과 같다.

- `dev_support`를 최종 제품 본체로 삼는다.
- `ai_office`는 기능 원천 및 참조 소스로 본다.
- Discord 중심 구조는 웹 구조로 치환한다.
- 순수 로직은 최대한 재사용한다.
- 민감정보와 외부 연동은 서버 계층으로 이동한다.
- 기존 `dev_support` 기능은 깨지지 않게 유지한다.

이 저장소는 위 작업을  
단순 프롬프트 의존이 아니라 **하네스 엔지니어링 방식**으로 진행하기 위해 존재한다.

---

# 2. 하네스 엔지니어링이란 무엇인가

이 프로젝트에서 하네스 엔지니어링은  
“AI에게 한 번 좋은 프롬프트를 주는 것”이 아니라,  
**AI가 흔들리지 않도록 작업 레일을 먼저 깔아두는 방식**을 뜻한다.

즉, 아래를 함께 관리한다.

- 프로젝트 헌장
- 아키텍처 경계
- 작업 순서
- 검증 기준
- 결과 보고 형식
- 계획 문서
- 체크리스트
- 리스크 기록

이 저장소는 위 기준의 원본 저장소다.

---

# 3. 이 저장소와 실제 코드 저장소의 관계

이 저장소는 방법론 원본이고,  
실제 구현은 별도의 작업 루트에서 진행한다.

예시:

```text
D:\workspace\office-unify\
  ai_office\
  dev_support\
  .cursor\
    rules\
    plans\
```

또는 별도 하네스 저장소를 포함해 아래처럼 운영할 수 있다.

```text
D:\workspace\
  office-unify-harness\
  office-unify\
    ai_office\
    dev_support\
    .cursor\
      rules\
      plans\
```

핵심은 다음과 같다.

- `office-unify-harness`는 방법론의 원본 저장소다.
- 실제 Cursor 작업 시에는 이 저장소의 핵심 파일을  
  **실제 작업 루트 안의 `.cursor/rules/`, `.cursor/plans/`, `docs/` 등으로 반영해야 한다.**
- Cursor는 현재 열려 있는 작업 루트 안의 규칙과 계획을 기준으로 동작한다.

즉, 이 저장소만 따로 존재한다고 자동 적용되는 것은 아니고,  
실제 작업할 프로젝트 루트에도 필요한 파일이 들어 있어야 한다.

---

# 4. 현재 디렉토리 구성

예상 구조 예시:

```text
office-unify-harness/
├─ README.md
├─ .cursor/
│  ├─ rules/
│  │  ├─ 00-project-charter.md
│  │  ├─ 10-architecture-boundaries.md
│  │  ├─ 20-migration-workflow.md
│  │  └─ 30-validation-and-done.md
│  └─ plans/
│     └─ office-unify-master-plan.template.md
├─ docs/
├─ prompts/
└─ templates/
```

현재 핵심 파일의 역할은 아래와 같다.

## `.cursor/rules/00-project-charter.md`
통합 프로젝트의 최상위 원칙을 고정한다.

## `.cursor/rules/10-architecture-boundaries.md`
클라이언트/서버, 순수 로직/Discord 결합 로직, 보안 경계를 정의한다.

## `.cursor/rules/20-migration-workflow.md`
분석 → 설계 → 구현 → 검증 → 문서화 순서를 강제한다.

## `.cursor/rules/30-validation-and-done.md`
검증 없는 완료 선언을 막고, 완료 기준을 고정한다.

## `.cursor/plans/office-unify-master-plan.template.md`
실제 통합 작업 전에 채워야 하는 마스터 계획 템플릿이다.

---

# 5. 실제 작업 방식

이 저장소는 아래 순서로 활용한다.

## 1단계. 방법론 정리
이 저장소에서 규칙, 템플릿, 체크리스트를 정리한다.

## 2단계. 실제 작업 루트 준비
작업 PC에 아래처럼 통합 작업 루트를 만든다.

```text
D:\workspace\office-unify\
  ai_office\
  dev_support\
```

## 3단계. 하네스 반영
이 저장소의 핵심 파일을 실제 작업 루트에 반영한다.

예시:

```text
D:\workspace\office-unify\
  .cursor\
    rules\
    00-project-charter.md
    10-architecture-boundaries.md
    20-migration-workflow.md
    30-validation-and-done.md
  .cursor\
    plans\
    office-unify-master-plan.md
```

## 4단계. Cursor 작업 시작
Cursor에서는 실제 작업 루트 하나를 열고,
먼저 분석/설계부터 진행한다.

## 5단계. Plan 기반 구현
바로 큰 구현으로 가지 말고,
계획 문서를 먼저 채운 뒤 작은 단위로 구현한다.

---

# 6. 권장 작업 원칙

이 프로젝트의 기본 원칙은 아래와 같다.

1. 최종 제품 본체는 `dev_support`다.
2. `ai_office`는 기능 원천이자 참조 소스다.
3. 기존 `dev_support` 핵심 기능은 깨지면 안 된다.
4. Discord 결합 로직은 직접 이식하지 않는다.
5. 순수 로직은 가능한 한 재사용한다.
6. 민감정보는 항상 서버 전용으로 둔다.
7. 큰 작업은 반드시 분석 → 설계 → 구현 → 검증 → 문서화 순서로 간다.
8. 모든 주요 작업은 결과 보고 형식을 따른다.

---

# 7. Cursor에서의 사용 방식

Cursor는 아래 요소를 함께 활용할 때 가장 안정적으로 동작한다.

- 현재 열린 작업 루트의 코드베이스
- `.cursor/rules/` 안의 규칙 파일
- `.cursor/plans/` 안의 계획 파일
- 명확한 작업 프롬프트
- 검증 명령
- 문서 업데이트 요구사항

따라서 이 저장소의 목적은  
Cursor에게 “좋은 말을 한 번 해주는 것”이 아니라,  
**항상 같은 기준으로 판단하도록 작업 문맥을 구조화하는 것**이다.

---

# 8. 권장 프롬프트 운영 방식

실제 Cursor 작업 시에는 한 번에 너무 많은 것을 시키지 않는다.

권장 순서:

1. 분석 전용 프롬프트
2. 설계 전용 프롬프트
3. 소규모 구현 프롬프트
4. 검증/문서화 프롬프트

즉, 아래처럼 나눠서 진행하는 것이 좋다.

- “지금은 코드 수정하지 말고 분석만 하라.”
- “현재 구조를 바탕으로 통합 설계를 제안하라.”
- “가장 안전한 1차 변경만 구현하라.”
- “변경 파일, 검증 방법, 남은 리스크를 정리하라.”

---

# 9. 이 저장소가 다루는 범위

이 저장소는 아래를 다룬다.

- 통합 프로젝트 운영 원칙
- Cursor용 하네스 파일
- 설계/구현 템플릿
- 문서화 기준
- 체크리스트
- 리스크 관리 방식
- GPT Builder로 확장 가능한 요약 지침의 원본

이 저장소는 아래를 직접 다루지 않는다.

- 실제 앱 소스 코드 구현
- 환경변수 값 자체
- 실데이터 운영
- 배포 비밀정보

---

# 10. 향후 확장 방향

향후 아래 파일들을 추가해 확장할 수 있다.

- `docs/overview/project-vision.md`
- `docs/overview/terminology.md`
- `docs/workflow/cursor-operating-guide.md`
- `docs/workflow/harness-engineering-guide.md`
- `prompts/cursor/01-analysis-only.md`
- `prompts/cursor/02-implementation.md`
- `prompts/cursor/03-debugging.md`
- `templates/report-template.md`
- `templates/migration-plan-template.md`
- `templates/risk-log-template.md`

---

# 11. 운영 결론

이 저장소의 핵심 목적은 하나다.

**통합 프로젝트를 프롬프트 의존형이 아니라,  
규칙·계획·검증·문서화를 포함한 하네스 엔지니어링 방식으로 운영하는 것.**

즉,
- 프롬프트는 작업 지시이고
- 컨텍스트는 배경 지식이며
- 하네스는 작업 전체를 안정시키는 레일이다

이 저장소는 그 레일의 원본이다.
