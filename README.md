# Search Ranking Optimization (BM25 → ML Ranking)

## 1. Problem
기존 키워드 기반 검색은 단어 매칭 중심이라 사용자 의도를 충분히 반영하지 못해,
관련 문서가 상위에 노출되지 않는 문제가 발생할 수 있습니다.
본 프로젝트는 전통적인 IR baseline(BM25) 대비 머신러닝 기반 랭킹 모델이
검색 품질을 얼마나 개선하는지 검증하는 것을 목표로 합니다.

## 2. Approach
- Baseline: BM25로 검색 랭킹 생성
- Feature Engineering:
  - BM25 score
  - Query length / Document length
  - Term overlap ratio
  - TF-IDF cosine similarity
- Model: LightGBM (regression 또는 ranking)
- Evaluation: Precision@K, NDCG@K로 비교

## 3. Dataset
- 예정: MS MARCO (Passage Ranking) subset 또는 샘플 데이터

## 4. Project Structure
search-ranking-project/
├─ README.md
├─ data/
├─ notebooks/
├─ src/
└─ results/

## 5. Milestones
- [ ] BM25 baseline 구현 및 지표 계산
- [ ] feature 생성
- [ ] ML 모델 학습/평가
- [ ] 결과 분석 및 정리