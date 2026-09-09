# HCD_S

HCD_S is a Chinese semantic textual similarity dataset designed for fine-grained semantic similarity measurement in short-video subtitle scenarios. It contains subtitle pairs with different degrees of semantic overlap, including paraphrased, rewritten, partially related, and semantically unrelated content.

## Dataset Statistics

HCD_S contains 5,000 Chinese subtitle pairs.

| Split | Number of pairs |
| --- | ---: |
| Train | 4,000 |
| Validation | 500 |
| Test | 500 |
| Total | 5,000 |

## Annotation Protocol

During dataset construction, overly short, incomplete, noisy, and extremely long subtitles were removed. Candidate subtitle pairs were curated to cover different similarity levels and common rewriting patterns, including synonym substitution, entity replacement, word-order adjustment, paraphrastic rewriting, and semantic-structure reuse.

Annotation was performed independently by two trained annotators. Each subtitle pair was assigned a semantic similarity score from 0 to 5 using an annotation scheme adapted from the STS-B framework to the short-video homogenization setting.

Annotators were instructed to prioritize the preservation or reuse of key entities, factual claims, and narrative structure, while treating surface lexical overlap as a secondary factor.

Pairs with an absolute annotation difference of two points or more were discussed by the two annotators. A consensus score was assigned when agreement was reached, and pairs for which no consensus could be reached were removed. For pairs not requiring discussion, the final score was obtained by averaging the two independent annotations.

## Score Definition

The annotation scale ranges from 0 to 5.

| Score | Description |
| --- | --- |
| 0 | Semantically unrelated |
| 1 | Weak or indirect semantic relation |
| 2 | Partially related, with major differences in key semantic content |
| 3 | Moderately related, but with clear differences in information content or focus |
| 4 | Highly related, with the core meaning largely preserved but some differences in scope or details |
| 5 | Essentially semantically equivalent, with differences mainly in wording or sentence structure |

Because independent annotations are averaged for pairs not requiring discussion, final dataset scores may contain non-integer values.

## Inter-Annotator Agreement

Inter-annotator agreement was calculated from the initial independent annotations before disagreement resolution.

- Number of annotators: 2
- Agreement metric: quadratic-weighted Cohen's kappa
- Cohen's kappa: 0.72

## Data Split and Leakage Control

The dataset was split before knowledge graph construction and LLM-based augmentation. The training, validation, and test splits do not share original video IDs, and cross-split near-duplicate checking found no confirmed near-duplicate subtitles.

Only training-split subtitles were used for knowledge graph construction, LLM-based augmentation, and parameter optimization. Validation data were used for model selection, and test data were reserved for final evaluation.

## Data Format

Each instance contains two Chinese subtitle texts and a semantic similarity score.

```csv
id,sentence1,sentence2,score
1,"Chinese text A","Chinese text B",4.0
2,"Chinese text A","Chinese text B",1.0

Data Availability

The HCD_S dataset will be available from the corresponding author upon reasonable request. This repository is anonymized during double-blind review.