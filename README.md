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

```
## Annotation Example

### Score 3

Text A:
夜景人像糊成鬼？三脚架不是唯一选择！教你手持拍出清晰夜景：开大光圈到F1.8，ISO调到1600，快门速度控制在1/50秒以上，再让模特稍微靠墙借力，成片率直接翻倍！

Text B:
晚上拍照总是一团黑？试试手机夜景模式的黑科技！打开专业模式，手动拉高阴影，降低高光，再用夜景算法合成，瞬间提亮暗部细节。记得让人物站在有光源的地方，皮肤都会发光哦！

Rationale: Both texts discuss night portrait photography but focus on different technical approaches, corresponding to a moderate similarity level.

### Score 5

Text A:
眼霜是不是智商税？我觉得真不是！尤其是过了25岁，眼部细纹、黑眼圈都来了，用对眼霜能明显改善。选的时候看成分，像胜肽、维A醇这些，坚持用才有效果，别指望涂一两天就见效啊。
Text B:
眼霜到底是不是智商税？我个人认为不是的。特别是25岁以后，眼部问题像细纹、黑眼圈会出现，合适的眼霜很有帮助。关键要选含有效成分如胜肽或维A醇的产品，并且需要持续使用才能看到效果，不能急于求成。
Rationale: Both texts express nearly identical claims about eye cream, age-related concerns, key ingredients, and the need for continued use, with differences mainly in wording.

## Data Availability

The HCD_S dataset will be available from the corresponding author upon reasonable request. This repository is anonymized during double-blind review.