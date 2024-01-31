---
summary: "It is a naive search engine built from scratch with document preprocesssing, indexing, retrieving, and relevance evaluation based on the wikipedia pages. It is embedded with BasicInvertedIndex, BM25, Learn-to-Rank, Doc2Query, Bi-Encoder, CrossEncoder, and NDCG."
authors:
  - admin
lastMod: 2023-11-07T00:00:00.000Z
title: Naive Search Engine
subtitle: ""
date: 2023-11-07T00:00:00.000Z
tags: []
categories: []
projects: []
image:
  caption: ""
  focal_point: top
  filename: ""
---
- Designed and implemented a Naive Search Engine with a focus on efficiency and relevance, achieving
notable results in indexing and ranking tasks.
- Engineered basic inverted, positional, and on-disk inverted indexes while incorporating the idea of
SPIMI to accelerate indexing processes by at least 30 times, effectively optimizing memory usage.
- Successfully processed and tokenized a substantial dataset of 1 million Wikipedia pages (7GB) within
20 minutes, demonstrating efficient and scalable data handling capabilities.
- Enhanced search result relevance by implementing L2Ranker with LightGBM Ranker, Doc2Query, Bi-Encder, and CrossEncoder with huggingface.

Basic Setup:
- Number of documents: 200k
- Indexer: `BasicInvertedIndex`
- Doc2Query: `doc2query/msmarco-t5-base-v1`
- Learn-to-Rank: `lightgbm.LGBMRanker`
- Bi-Encoder: `sentence-transformers/msmarco-MiniLM-L12-cos-v5`
- CrossEncoder: `cross-encoder/msmarco-MiniLM-L6-en-de-v1`

Comment: select related models based on number of downloads on huggingface.

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: left;">
      <th></th>
      <th>MAP@10</th>
      <th>NDCG@10</th>
      <th>CONFIG</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>base</td>
      <td>0.043913</td>
      <td>0.332071</td>
      <td> index + BM25</td>
    </tr>
    <tr>
      <td>BM25</td>
      <td>0.039091</td>
      <td>0.331340</td>
      <td> index_aug + BM25</td>
    </tr>
    <tr>
      <td>VectorRanker</td>
      <td>0.059544</td>
      <td>0.314000</td>
      <td> index_aug + vec_rank</td>
    </tr>
    <tr>
      <td>l2r</td>
      <td>0.070226</td>
      <td>0.343751</td>
      <td> index + BM25 + l2r </td>
    </tr>
    <tr>
      <td>pipeline_1</td>
      <td>0.052045</td>
      <td>0.330412</td>
      <td> index_aug + BM25 + l2r (cross_enc) </td>
    </tr>
    <tr>
      <td>pipeline_2</td>
      <td>0.059102</td>
      <td>0.333798</td>
      <td> index_aug + vec_rank + l2r (cross_enc) </td>
    </tr>
    <tr>
      <td>pipeline_3</td>
      <td>0.046063</td>
      <td>0.328585</td>
      <td> index + vec_rank + l2r </td>
    </tr>
    <tr>
      <td>pipeline_4</td>
      <td>0.056367</td>
      <td>0.331492</td>
      <td> index_aug + vec_rank + l2r </td>
    </tr>
  </tbody>
</table>
</div>

**Discussion**
- Document augmentation might help the re-rank, but a further experiment shows that pure BM25 with document augmentation gets lower MAP in the first matching part than that without augmentations.
- VectorRanker outperforms BM25, which shows that bi-encoder are providing important information.
- Cross encoders will increase NDCG score without lowering MAP too much. It shows the effectiveness to use CrossEncoder in the reranking part.
- HW2 pipeline performs better than others, which shows that the added new features in hw2 plays a quite critical role in prediction.