# office-unify-harness

`office-unify-harness`는 `ai_office`와 `dev_support`를 하나의 통합 웹 서비스로 재구성하기 위한 **하네스 엔지니어링 방법론 저장소**입니다.

이 저장소는 실제 앱 소스가 아니라, 통합 작업을 안정적으로 진행하기 위한 기준을 담습니다.

- 프로젝트 원칙
- 아키텍처 경계
- 마이그레이션 워크플로
- 완료 기준
- Cursor 작업 규칙
- 계획 템플릿
- 프롬프트 템플릿
- 체크리스트
- 문서/보고 형식

---

## 목적

현재 목표는 아래 두 프로젝트를 **하나의 웹 서비스**로 통합하는 것입니다.

- `ai_office`
- `dev_support`

통합 원칙은 다음과 같습니다.

- 최종 제품 본체는 `dev_support` 기준으로 간다.
- `ai_office`는 기능 원천과 참조 구현으로 활용한다.
- Discord 중심 UX는 웹 UX로 재구성한다.
- 순수 로직은 최대한 재사용한다.
- 민감정보와 외부 연동은 서버 계층으로 이동한다.
- 기존 `dev_support` 핵심 기능은 깨지지 않게 유지한다.
- 모든 큰 작업은 분석 → 설계 → 구현 → 검증 → 문서화 순서로 진행한다.

즉, 이 저장소는 단순 프롬프트 모음이 아니라, **AI 작업의 기준 레일**을 제공하는 저장소입니다.

---

## 하네스 엔지니어링이란

이 프로젝트에서 하네스 엔지니어링은 AI에게 즉흥적으로 구현을 맡기는 방식이 아니라, 아래를 먼저 고정한 뒤 작업하는 방식입니다.

- 프로젝트 헌장
- 아키텍처 경계
- 작업 순서
- 검증 기준
- 결과 보고 형식
- 계획 문서
- 체크리스트
- 리스크 관리 방식

프롬프트가 작업 지시라면, 하네스는 작업 전체를 안정시키는 운영 틀입니다.

---

## 저장소 역할

이 저장소는 **방법론 원본 저장소**입니다.  
실제 구현은 별도의 통합 작업 루트에서 진행하는 것을 권장합니다.

예시:

    C:\work\office-unify\
      .cursor\
        rules\
        plans\
      apps\
      packages\
      docs\

핵심 원칙:

- `office-unify-harness`는 기준 저장소다.
- 실제 Cursor 작업은 통합 작업 루트에서 수행한다.
- 이 저장소의 규칙/계획/문서를 실제 작업 루트에 반영한 뒤 개발한다.

---

## 현재 구성

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
    │  ├─ checklists/
    │  ├─ overview/
    │  └─ workflow/
    ├─ prompts/
    │  ├─ cursor/
    │  └─ gpt-builder/
    └─ templates/

---

## 핵심 디렉터리 설명

### `.cursor/rules/`
통합 프로젝트에서 Cursor가 흔들리지 않도록 하는 핵심 규칙입니다.

- `00-project-charter.md`  
  프로젝트의 최상위 목표와 불변 원칙 정의

- `10-architecture-boundaries.md`  
  클라이언트/서버, 순수 로직/플랫폼 결합 로직, 보안 경계 정의

- `20-migration-workflow.md`  
  분석 → 설계 → 구현 → 검증 → 문서화 순서 정의

- `30-validation-and-done.md`  
  완료 기준과 검증 항목 정의

### `.cursor/plans/`
- `office-unify-master-plan.template.md`  
  실제 통합 작업 전 작성할 마스터 계획 템플릿

### `docs/`
- `checklists/`: 설계/구현/릴리즈 점검표
- `overview/`: 프로젝트 상위 개념 문서
- `workflow/`: 작업 운영 방식 문서

### `prompts/`
- `cursor/`: 단계별 Cursor 실행 프롬프트
- `gpt-builder/`: GPT Builder 확장용 지침 원본

### `templates/`
- 계획서, 리스크 로그, 보고서 템플릿

---

## 권장 통합 방향

최종 통합 방향은 다음과 같습니다.

- 웹 서비스 본체는 `dev_support` 중심으로 간다.
- `ai_office`의 분석/포트폴리오/토론/트렌드 로직은 서버 엔진으로 흡수한다.
- Discord 전용 인터랙션은 그대로 이식하지 않고 웹 흐름으로 재설계한다.
- UI는 `dev_support`, 도메인 로직은 `ai_office` 기반으로 통합한다.
- 환경변수, API 키, DB 접근은 서버 전용으로 둔다.

---

## 권장 로컬 작업 구조

현재 로컬 경로가 아래와 같다면:

- `C:\ai-office`
- `C:\work\dev_support`

기존 소스를 직접 섞지 말고, 새 통합 작업 루트를 만드는 것을 권장합니다.

예시:

    C:\work\office-unify\
    ├─ .cursor\
    │  ├─ rules\
    │  └─ plans\
    ├─ apps\
    │  └─ web\
    ├─ packages\
    │  ├─ ai-office-engine\
    │  ├─ shared-types\
    │  ├─ shared-utils\
    │  └─ supabase-access\
    ├─ docs\
    └─ legacy-sources\
       ├─ ai-office\
       └─ dev_support\

운영 원칙:

- `apps/web`는 `dev_support` 기반 웹 앱으로 사용
- `packages/ai-office-engine`에는 `ai_office`의 재사용 가능한 순수 로직 이관
- `legacy-sources/`는 원본 비교 및 참조용으로 유지
- 실제 개발은 통합 루트 기준으로 진행

---

## 작업 순서

권장 작업 순서는 다음과 같습니다.

1. 하네스 반영  
   - `.cursor/rules`
   - `.cursor/plans`
   - `docs`
   - `prompts`

2. 통합 작업 루트 준비  
   - 새 폴더 생성
   - 하네스 파일 복사
   - Cursor는 통합 루트 하나만 열기

3. 웹 셸 확보  
   - `dev_support`를 `apps/web` 기준으로 정리
   - 기존 기능 정상 동작 확인

4. 엔진 추출  
   - `ai_office`에서 순수 로직을 패키지화
   - Discord 결합 로직은 분리 또는 제외

5. API/웹 통합  
   - Next.js API 또는 서버 계층으로 기능 연결
   - 포트폴리오/토론/트렌드/운영 기능을 웹 메뉴로 재구성

6. 검증 및 문서화  
   - 기능 검증
   - 리스크 정리
   - 문서 업데이트

---

## 완료 기준

다음 조건을 만족해야 완료로 봅니다.

- 기존 `dev_support` 기능이 유지된다.
- `ai_office`의 핵심 로직이 웹 구조로 안전하게 통합된다.
- Discord 전용 결합이 웹 구조로 치환된다.
- 환경변수와 민감정보가 클라이언트에 노출되지 않는다.
- 주요 변경 사항이 문서화된다.
- 검증 결과와 남은 리스크가 정리된다.

---

## 한 줄 요약

`office-unify-harness`는  
`dev_support`를 웹 본체로, `ai_office`를 도메인 엔진으로 삼아  
두 프로젝트를 하나의 통합 서비스로 만들기 위한 **작업 기준 저장소**입니다.
