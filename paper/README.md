# Research Manuscript

**국문 제목:** 기술문서의 수치 변조 위치 식별을 위한 경량 VLM 기반 OCR 후보 선택 기법  
**영문 설명:** VLM-Guided OCR Candidate Selection for Numeric Change Localization in Technical Documents  
**저자(원고):** 김동규, 김병욱 · 국립창원대학교 정보통신공학과

## Abstract

본 연구는 동일하거나 유사한 수치가 반복되는 기술문서에서 변경된 수치의 정확한 위치를 식별하는 문제를 다룹니다. ORB/RANSAC 기반 문서 정합과 24개 중첩 타일 비교를 수행하고, 경량 VLM을 사용해 변경 전후 수치와 주변 문맥 단서를 추출합니다. PaddleOCR가 제공하는 문자 영역의 위치를 후보로 구성한 뒤 같은 VLM이 후보 ID를 선택해 최종 Bounding Box를 결정합니다. 연구 원고는 통제된 합성 문서 6쌍의 수치 변경 19개를 대상으로 Precision 90.5%, Recall 100.0%를 보고합니다.

## Research Materials

이 저장소에는 연구 초록, 아키텍처, 보고된 평가 결과 및 관련 데스크톱 GUI 구성도를 공개합니다.

- [Project overview](../README.md)
- [Architecture](../docs/ARCHITECTURE.md)
- [Evaluation](../docs/EVALUATION.md)
