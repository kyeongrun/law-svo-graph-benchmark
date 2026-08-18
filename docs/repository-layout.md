# 저장소 구조

```text
data/             원문 스냅샷과 공통 전처리 산출물
contracts/        두 방식이 반드시 지켜야 하는 데이터 계약
extractors/       KoNLPy 규칙형 / LLM 직접 추출형 구현 경계
common/           문장 분할·정규화·검증·적재의 공통 계층
infrastructure/   그래프 DB와 DDL·컨테이너 설정
benchmarks/       정답 SVO와 대표 질의 평가셋
runs/             방식별 실행 메타데이터와 생성 산출물
tests/            공통 계약 및 방식별 회귀 테스트
docs/             비교 목적과 설계 결정 기록
```

## 데이터 흐름(예정)

```text
data/raw
  → common/segmentation
  → data/source_units
  → extractors/konlpy_rule 또는 extractors/llm_svo
  → common/normalization + common/validation
  → common/loading
  → 서로 분리된 그래프 DB / 실행 결과
```

이 구조에서는 `common/`이 추출 방식 간 공정성을 지키는 경계입니다. 각 추출기는 공통 문장 단위를 받아 공통 관계 계약에 맞는 후보만 반환합니다.
