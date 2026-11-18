# Experimental Evaluation

## Task

**Numeric change localization**: 단순히 변경된 값의 존재를 예측하는 것이 아니라, 기준 문서와 검사 문서에서 **어느 문자 영역이 변경되었는지** 위치를 식별하는 작업입니다.

## Benchmark Design

논문에 사용된 평가 세트는 동일·유사 수치가 반복되는 문서 조건을 통제하기 위해 구성한 **paired synthetic raster-document benchmark**입니다.

| Attribute | Configuration |
|---|---|
| Paired documents | 6 |
| Modified document pairs | 4 |
| Unchanged document pairs | 2 |
| Ground-truth numeric changes | 19 |
| Layout coverage | Tables, multiple regions, prose+tables, numeric fields near figures |
| Focus | Repeated values and contextual disambiguation of numeric changes |

변경 정답 위치를 알고 있으므로 수치 변경 여부와 실제 문서 내 위치 식별을 분리해서 평가할 수 있습니다.

## Methods

1. **OCR Only** — OCR 기반 변경 위치 후보를 최종 예측으로 사용.
2. **VLM Only** — OCR 위치 후보 없이 VLM이 변경 문자 영역의 위치를 직접 지정.
3. **Proposed OCR + VLM** — 1차 VLM이 변경 정보를 추출하고, 2차 VLM이 OCR 후보 ID를 선택.

## Manuscript-Reported Results

| Method | Precision ↑ | Recall ↑ |
|---|---:|---:|
| OCR Only | 24.3% | 89.5% |
| VLM Only | 0.0% | 0.0% |
| **Proposed OCR + VLM** | **90.5%** | **100.0%** |

Precision = 올바르게 식별된 위치 / 전체 예측 위치.  
Recall = 올바르게 식별된 위치 / 전체 정답 변경 위치.

**Reading the results:** OCR 후보는 상대적으로 넓은 위치 탐색 공간을 제공하고, VLM의 문맥적 후보 선택은 그중 실제 변경된 문자 영역의 식별에 활용됩니다. VLM Only의 `0.0%`는 **위치 식별 기준**의 결과이며, 수치 변경 자체를 전혀 검출하지 못했다는 뜻이 아닙니다.

> **Evaluation scope:** 제공된 연구 자료에 보고된 합성 문서 6쌍·수치 변경 19개의 위치 식별 결과입니다. 본 저장소는 해당 연구 결과를 소개합니다.

## Improvement over OCR Only

- Precision: **+66.2%p** (90.5% − 24.3%).
- Recall: **+10.5%p** (100.0% − 89.5%).

두 값은 표에 보고된 지표의 차이로 계산했습니다.

## Research Takeaway

OCR과 VLM을 단순히 직렬 결합하는 대신, **OCR을 후보 좌표 제공자**, **VLM을 변경값·문맥 추출 및 후보 선택자**로 역할 분리하면 반복 수치 환경에서 위치 식별의 정확성을 높일 수 있다는 연구적 가능성을 보여줍니다.
