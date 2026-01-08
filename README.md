# Search Ranking Optimization (BM25 → Learning to Rank)

## 1. Problem
키워드 기반 검색 시스템은 주로 단어 매칭에 의존하기 때문에,
사용자 질의(Query)와 의미적으로 관련 있는 문서라도
상위 검색 결과에 노출되지 않는 문제가 발생할 수 있습니다.

본 프로젝트는 검색을 **랭킹(Ranking) 문제**로 정의하고,
전통적인 정보 검색(IR) 기법인 **BM25**와
머신러닝 기반 **Learning-to-Rank 모델**을 비교하여,
상위 검색 결과 품질이 얼마나 개선되는지를
**랭킹 지표(NDCG@K, Precision@K)** 기준으로 정량적으로 검증하는 것을 목표로 합니다.

---

## 2. Approach
본 프로젝트는 검색 랭킹 파이프라인을 단계적으로 확장하며,
각 단계에서의 성능을 **BM25 baseline과 비교**합니다.

1. **Baseline (Lexical Ranking)**
   - BM25를 사용해 query-document 랭킹 생성

2. **Feature Engineering**
   - BM25 score
   - Query length / Document length
   - Term overlap ratio
   - TF-IDF cosine similarity

3. **Learning to Rank**
   - LightGBM 기반 모델
     - Regression 방식
     - Ranking (LambdaRank) 방식

4. **Evaluation**
   - Precision@K, NDCG@K 기준 성능 비교
   - 각 단계별 성능 변화 분석

---

## 3. Dataset
- **BEIR Benchmark**
  - SciFact (primary dataset)
- 각 데이터셋은 다음 요소로 구성됩니다:
  - Queries
  - Corpus (documents)
  - Relevance judgments (qrels)

※ 파이프라인 검증 후 MS MARCO Passage Ranking 데이터셋으로 확장 예정

---

## 4. Project Structure
search-ranking-project/
├─ README.md # project overview and results
├─ data/ # datasets and preprocessed files
├─ notebooks/ # experiments (BM25, features, LTR)
├─ src/ # feature generation, models, evaluation
└─ results/ # metrics, runs, and plots

---

## 5. Experiments
### 5.1 BM25 Baseline
- BM25를 사용해 각 query에 대해 Top-K 문서를 검색
- 랭킹 성능은 NDCG@10, Precision@10 기준으로 평가

### 5.2 Feature-based Ranking
- Lexical feature들을 사용해 문서 relevance 예측
- 단일 feature 및 feature 조합의 효과 분석

### 5.3 Learning to Rank
- LightGBM 기반 모델 학습
- Regression vs LambdaRank 성능 비교

---

## 6. Results
### 6.1 BM25 Baseline (BEIR / SciFact)

| Model | NDCG@10 | Precision@10 |
|------|---------|---------------|
| BM25 | 0.xxx   | 0.xxx         |

※ 이후 실험 결과는 동일한 지표 기준으로 비교

---

## 7. Learnings
- BM25는 term overlap이 높은 query에서 강점을 보이지만,
  의미적 유사성이 중요한 query에서는 한계를 보임
- 간단한 lexical feature 추가만으로도
  상위 검색 결과 품질 개선 가능성을 확인

---

## 8. Next Steps
- Feature importance 및 ablation study
- LambdaRank 기반 모델 고도화
- MS MARCO 데이터셋 확장 실험
- Error analysis를 통한 실패 케이스 분석