# A Survey of Recent Development and Trends of Graph Embedding for Biomedical Data
## Introduction
## Preliminaries
## Taxonomy of Graph Embedding Models
### Homogeneous Graph Embedding Models
#### Matrix factorization based methods
#### Random walk based methods
#### Deep learning based methods
### Heterogeneous Graph Embedding Models
#### Translational distance methods
#### Semantic matching methods
### Dynamic Graph Embedding Models
#### Probabilistic models
#### Dynamic graph embedding methods
## Applications and Tasks in Biomedical Domain
### Biomedical datasets
#### Survey about Drug Repurposing Knowledge Graph (DRKG) database



##### Introduction

DRKG is a comprehensive biological knowledge graph which have  97,238 entities( genes, compounds, diseases, biological processes, side effects and symptoms etc) belonging to 13 entity-types, and 5,874,261 triplets belonging to 107 edge-types, as depicted in the figure below. ([github of DRKG](https://github.com/gnn4dr/DRKG))

![DRKG schema](https://github.com/gnn4dr/DRKG/raw/master/connectivity.png)







DRKG consist of six existing databases including DrugBank, Hetionet, GNBR, String, IntAct and DGIdb, and data collected from recent publications particularly related to Covid-19. 



**The type-wise distribution of the entities in DRKG and their original data-source(s)**

| Entity type         | Drugbank |   GNBR | Hetionet | STRING | IntAct | DGIdb | Bibliography | Total Entities |
| :------------------ | -------: | -----: | -------: | -----: | -----: | ----: | -----------: | -------------: |
| Anatomy             |       \- |     \- |      400 |     \- |     \- |    \- |           \- |            400 |
| Atc                 |    4,048 |     \- |       \- |     \- |     \- |    \- |           \- |          4,048 |
| Biological Process  |       \- |     \- |   11,381 |     \- |     \- |    \- |           \- |         11,381 |
| Cellular Component  |       \- |     \- |    1,391 |     \- |     \- |    \- |           \- |          1,391 |
| Compound            |    9,708 | 11,961 |    1,538 |     \- |    153 | 6,348 |        6,250 |         24,313 |
| Disease             |    1,182 |  4,746 |      257 |     \- |     \- |    \- |           33 |          5,103 |
| Gene                |    4,973 | 27,111 |   19,145 | 18,316 | 16,321 | 2,551 |        3,181 |         39,220 |
| Molecular Function  |       \- |     \- |    2,884 |     \- |     \- |    \- |           \- |          2,884 |
| Pathway             |       \- |     \- |    1,822 |     \- |     \- |    \- |           \- |          1,822 |
| Pharmacologic Class |       \- |     \- |      345 |     \- |     \- |    \- |           \- |            345 |
| Side Effect         |       \- |     \- |    5,701 |     \- |     \- |    \- |           \- |          5,701 |
| Symptom             |       \- |     \- |      415 |     \- |     \- |    \- |           \- |            415 |
| Tax                 |       \- |    215 |       \- |     \- |     \- |    \- |           \- |            215 |
| Total               |   19,911 | 44,033 |   45,279 | 18,316 | 16,474 | 8,899 |        9,464 |         97,238 |



**the number of triplets between different entity-type pairs in DRKG for DRKG and various datasources**

| Entity\-type pair                 |  Drugbank |    GNBR |  Hetionet |    STRING |  IntAct |  DGIdb | Bibliography | Total interactions |
| :-------------------------------- | --------: | ------: | --------: | --------: | ------: | -----: | -----------: | -----------------: |
| \(Gene, Gene\)                    |        \- |  66,722 |   474,526 | 1,496,708 | 254,346 |     \- |       58,629 |          2,350,931 |
| \(Compound, Gene\)                |    24,801 |  80,803 |    51,429 |        \- |   1,805 | 26,290 |       25,666 |            210,794 |
| \(Disease, Gene\)                 |        \- |  95,399 |    27,977 |        \- |      \- |     \- |          461 |            123,837 |
| \(Atc, Compound\)                 |    15,750 |      \- |        \- |        \- |      \- |     \- |           \- |             15,750 |
| \(Compound, Compound\)            | 1,379,271 |      \- |     6,486 |        \- |      \- |     \- |           \- |          1,385,757 |
| \(Compound, Disease\)             |     4,968 |  77,782 |     1,145 |        \- |      \- |     \- |           \- |             83,895 |
| \(Gene, Tax\)                     |        \- |  14,663 |        \- |        \- |      \- |     \- |           \- |             14,663 |
| \(Biological Process, Gene\)      |        \- |      \- |   559,504 |        \- |      \- |     \- |           \- |            559,504 |
| \(Disease, Symptom\)              |        \- |      \- |     3,357 |        \- |      \- |     \- |           \- |              3,357 |
| \(Anatomy, Disease\)              |        \- |      \- |     3,602 |        \- |      \- |     \- |           \- |              3,602 |
| \(Disease, Disease\)              |        \- |      \- |       543 |        \- |      \- |     \- |           \- |                543 |
| \(Anatomy, Gene\)                 |        \- |      \- |   726,495 |        \- |      \- |     \- |           \- |            726,495 |
| \(Gene, Molecular Function\)      |        \- |      \- |    97,222 |        \- |      \- |     \- |           \- |             97,222 |
| \(Compound, Pharmacologic Class\) |        \- |      \- |     1,029 |        \- |      \- |     \- |           \- |              1,029 |
| \(Cellular Component, Gene\)      |        \- |      \- |    73,566 |        \- |      \- |     \- |           \- |             73,566 |
| \(Gene, Pathway\)                 |        \- |      \- |    84,372 |        \- |      \- |     \- |           \- |             84,372 |
| \(Compound, Side Effect\)         |        \- |      \- |   138,944 |        \- |      \- |     \- |           \- |            138,944 |
| Total                             | 1,424,790 | 335,369 | 2,250,197 | 1,496,708 | 256,151 | 26,290 |       84,756 |          5,874,261 |

### Applications and Tasks
#### Pharmaceutical data analysis
#### Multi-omics data analysis
#### Clinical data analysis
