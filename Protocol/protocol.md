# Protocol: Systematic Review of Training Free and Model Preserving Hallucination Mitigation in LLMs
Window: 30 November 2022 to 30 September 2026.

## 1. Research questions

| RQ | Question | Answered from |
|---|---|---|
| RQ1 | What **training free and model preserving** strategies are used to mitigate hallucination in LLMs, and **at which stage of inference do they act**? | `intervention_layer`, `technique_family`, `adaptivity`, `verification_source` |
| RQ2 | Which benchmark datasets and knowledge domains are most frequently used to evaluate these frameworks? | `benchmarks_canonical`, `domain`, `task_setting` |
| RQ3 | What evaluation metrics are used to assess factual consistency and reliability of LLM outputs? | `metrics_canonical`, `metric_type`, `judge_validated` |
| RQ4 | How do **mitigation strategies across intervention layers** perform relative to one another in reducing hallucination? | Restricted synthesis, Section 8 |
| RQ5 | What are the primary methodological limitations and open research gaps in the **training free mitigation** literature? | Quality appraisal plus RQ1 to RQ4 |

## 2. Eligibility criteria

### Include if all are true
| ID | Criterion | Operational test |
|---|---|---|
| I1 | Population is an LLM | A transformer language model used generatively is the object of study |
| I2 | Hallucination is the target | Reduction of hallucination, factual error or unfaithfulness is a stated goal |
| I3 | Model preserving | Base model weights unchanged. No SFT, LoRA, adapters, DPO, RLHF or continued pretraining |
| I4 | Intervention at inference | The contribution acts at prompt, sampling, decoding, retrieval, verification or abstention stage, or orchestrates these |
| I5 | Measurable outcome | At least one quantitative result on a hallucination, factuality or faithfulness metric |
| I6 | Primary study | Reports its own experiments |

### Exclude if any is true
| ID | Criterion | Operational test |
|---|---|---|
| Ex1 | Outside window | First public version before 30 Nov 2022 or after 30 Sep 2026 |
| Ex2 | Secondary source | Review, survey, editorial, letter, opinion, tutorial |
| Ex3 | Clinical hallucination | Hallucination in human psychology, medicine or psychiatry rather than in a model |
| Ex4 | Detection only | The study focuses on detection only. |
| Ex5 | Non textual modality only | Vision, image generation or audio with no text only condition |
| Ex6 | No empirical evaluation | No experiment of the authors' own |
| Ex7 | Duplicate | Same study, different version. Keep the most complete |

### 2.1 The retrieval boundary

**Include** a retrieval paper only if reducing hallucination, factual error or unfaithfulness is stated as a goal in the title, abstract or introduction, **and** at least one reported outcome is a hallucination, factuality or faithfulness metric.

**Exclude** retrieval papers whose outcomes are only answer accuracy, exact match, retrieval recall, MAP, NDCG or latency, even where hallucination is mentioned in passing.

### 2.2 Detection only papers
Ex4 removes papers that only focuses on the detection of hallacinations in LLMs from the corpus.

### 2.3 Preprints
A preprint is included only where no peer reviewed version of the same study exists. Where both exist, the peer reviewed version is kept and the preprint is removed under Ex7. Every included preprint is flagged in `venue_type`, and Section 8 runs a sensitivity analysis with preprints removed.

---

## 3. Information sources

IEEE Xplore
ACM DL
Lens.org
Springer
ACL Anthology
DBLP or Semantic Scholar
arXiv

---

## 4. Search Strategy: Strings and Execution Plan

Seven sources will be searched for studies published between 30 November 2022 and 30 September 2026. Each string below translates the same three concept blocks, Population AND Problem AND Intervention, into the syntax accepted by the platform in question. For every source, the exact string, the date of the search, the settings applied, the hit count and the number exported will be recorded in the log at the end.

---

## 1. IEEE Xplore

Command Search will be used from the Advanced Search page. Because IEEE rejects grouped terms inside a field, three searches will be run and combined in Search History rather than submitting a single string.

**Search #1, Population AND Problem**

```
("Abstract":"large language model" OR "Abstract":"language model" OR "Abstract":LLM OR "Abstract":ChatGPT OR "Document Title":"large language model" OR "Document Title":LLM) AND ("Abstract":hallucinat* OR "Abstract":factual* OR "Abstract":faithful* OR "Abstract":groundedness OR "Document Title":hallucinat*)
```

**Search #2, Intervention at prompt, sampling and verification layers**

```
"Abstract":prompt* OR "Abstract":"training-free" OR "Abstract":"inference-time" OR "Abstract":"self-refine" OR "Abstract":"self-correction" OR "Abstract":"self-consistency" OR "Abstract":"self-verification" OR "Abstract":"chain-of-verification" OR "Abstract":verification
```

**Search #3, Intervention at decoding, retrieval and abstention layers**

```
"Abstract":decoding OR "Abstract":"contrastive decoding" OR "Abstract":"retrieval-augmented" OR "Abstract":RAG OR "Abstract":"knowledge graph" OR "Abstract":grounding OR "Abstract":abstention OR "Abstract":"uncertainty-aware"
```

These will be combined as `#1 AND (#2 OR #3)`, with the year range set to 2022 through 2026. Since IEEE filters by publication year only, records falling outside the exact window will be removed during screening.

---

## 2. ACM Digital Library

An initial search will be run, after which Edit Search and View Query Syntax will be opened so that the following can be pasted into Edit Query.

```
(Title:("large language model" OR "language model" OR LLM OR ChatGPT) OR Abstract:("large language model" OR "language model" OR LLM OR ChatGPT)) AND (Title:(hallucinat* OR factual* OR faithful*) OR Abstract:(hallucinat* OR factual* OR faithful* OR groundedness)) AND Abstract:(prompt* OR "training-free" OR "inference-time" OR decoding OR "contrastive decoding" OR "retrieval-augmented" OR RAG OR "knowledge graph" OR grounding OR "self-refine" OR "self-correction" OR "self-consistency" OR "self-verification" OR "chain-of-verification" OR verification OR abstention)
```

The Publication Date range will be set to November 2022 through September 2026. The ACM Guide to Computing Literature will be searched rather than the ACM full text collection, so that non ACM publishers are included, and the collection used will be recorded.

---

## 3. Lens.org

Stemming will be turned off under Query Tools before the search is run, because Lens does not stem wildcard terms and leaving stemming on would produce inconsistent matching. This setting will be reported.

```
(title:("large language model" OR "large language models" OR LLM OR ChatGPT) OR abstract:("large language model" OR "large language models" OR LLM OR ChatGPT)) AND (title:(hallucinat* OR factual* OR faithful*) OR abstract:(hallucinat* OR factual* OR faithful* OR fabricat* OR groundedness)) AND abstract:(prompt* OR "training-free" OR "inference-time" OR decoding OR "contrastive decoding" OR "retrieval-augmented" OR RAG OR "knowledge graph" OR grounding OR "self-refine" OR "self-correction" OR "self-consistency" OR "self-verification" OR "chain-of-verification" OR verification OR abstention) AND date_published:[2022-11-30 TO 2026-09-30]
```

Export will be performed from a signed in account, since anonymous accounts are capped at 1,000 records.

---

## 4. Springer Nature Link

Springer offers no abstract only field, and its Keywords field searches full text. Two searches will therefore be run, the first of which will be reported as primary.

**Run A, pasted into the Title box**

```
("large language model" OR "large language models" OR "LLM" OR "ChatGPT") AND ("hallucination" OR "hallucinations" OR "factual consistency" OR "faithfulness")
```

**Run B, pasted into the Keywords box**

```
("large language model" OR "LLM") AND ("hallucination" OR "hallucinations") AND ("prompting" OR "training-free" OR "decoding" OR "retrieval-augmented" OR "self-consistency" OR "verification" OR "abstention")
```

Date Published will be set to 30 November 2022 through 30 September 2026. Run B is expected to be noisy because it reaches body text, and Springer will accordingly be reported as a title level search with a supplementary full text pass. Where a result set exceeds 1,000 it will be split by year, since the CSV export is capped at that figure and no batch RIS export exists.

---

## 5. ACL Anthology

The Anthology's site search is a Google Programmable Search Engine, so it returns a ranked and capped list rather than a Boolean result set, and it offers no export. It will be used only for orientation, with the following terms.

```
hallucination mitigation large language model prompting decoding retrieval verification
```

For the reportable search, `anthology+abstracts.bib.gz` will be downloaded, the download date and file hash recorded, and the file filtered locally with a scripted equivalent of the Boolean string. The script will be archived as supplementary material. This source will be reported in PRISMA under other methods and registers.

---

## 6. DBLP

DBLP indexes titles, authors and venues only, uses prefix matching by default, and has phrase search and NOT disabled. It will be treated as a supplementary source for computer science venue coverage, searched with three short queries.

```
hallucinat llm|language
```

```
hallucinat mitigat|detect
```

```
faithful|factual llm|language
```

Because DBLP offers no date parameter and caps results at 1,000, the year field will be filtered after export.

---

## 7. Semantic Scholar

The website search box ignores Boolean operators, so the bulk endpoint will be queried directly by pasting the following into the browser address bar.

```
https://api.semanticscholar.org/graph/v1/paper/search/bulk?query=%28%22large+language+model%22+%7C+%22large+language+models%22+%7C+LLM+%7C+ChatGPT%29+%2B+%28hallucination+%7C+hallucinations+%7C+faithfulness+%7C+%22factual+consistency%22+%7C+groundedness%29+%2B+%28prompting+%7C+%22training-free%22+%7C+%22inference-time%22+%7C+decoding+%7C+%22retrieval-augmented%22+%7C+grounding+%7C+%22self-refine%22+%7C+%22self-correction%22+%7C+%22self-consistency%22+%7C+%22chain-of-verification%22+%7C+verification+%7C+abstention%29&publicationDateOrYear=2022-11-30:2026-09-30&fields=title,abstract,year,venue,externalIds
```

The response carries a continuation `token`, which will be appended as `&token=<value>` to retrieve each further batch of 1,000. The returned JSON will be converted to RIS for screening, and the raw JSON archived.

---

## 8. arXiv

The arXiv API will be queried directly, since the web interface offers no bulk export. The API supports no wildcards, so every variant has been spelled out.

```
http://export.arxiv.org/api/query?search_query=%28cat:cs.CL+OR+cat:cs.AI+OR+cat:cs.LG%29+AND+%28abs:%22large+language+model%22+OR+abs:%22large+language+models%22+OR+abs:LLM+OR+abs:ChatGPT%29+AND+%28abs:hallucination+OR+abs:hallucinations+OR+abs:faithfulness+OR+abs:%22factual+consistency%22+OR+abs:factuality%29+AND+%28abs:prompting+OR+abs:%22training-free%22+OR+abs:%22inference-time%22+OR+abs:decoding+OR+abs:%22retrieval-augmented%22+OR+abs:grounding+OR+abs:%22self-correction%22+OR+abs:%22self-consistency%22+OR+abs:%22chain-of-verification%22+OR+abs:verification+OR+abs:abstention%29+AND+submittedDate:%5B202211300000+TO+202609302359%5D&start=0&max_results=200
```

Paging will proceed by increasing `start` in steps of 200, with three seconds between requests as arXiv's terms require. An arXiv record will be retained only where no peer reviewed version of the same study exists, and every retained preprint will be flagged so that it can be removed in the sensitivity analysis.

## 5. Screening
**Stage 1, title and abstract.** Two reviewers will independently review each article and inlcude it only when both reach the consensus. In case of a disagreement, third reviewer will make the final decision.

**Stage 2, full text.** Expert Reviewer will inlude or excludes a study. Record exactly one exclusion reason per excluded paper, using the criterion ID.

**Agreement.** Both screeners independently screen a random 20 percent at each stage. Compute Cohen kappa and report it. Below 0.70, stop, rewrite the criterion that caused the disagreement, and rescreen. Resolve conflicts by discussion, with a third party only for deadlock.

---

## 6. Quality appraisal
Scored for every included study. Used for sensitivity analysis and for RQ5.

Each item scores 0 absent, 1 partial, 2 complete. Maximum 24.

| ID | Item |
|---|---|
| Q1 | Objective and hallucination type targeted stated explicitly |
| Q2 | Method described in enough detail to reimplement, including prompt templates or decoding parameters as applicable |
| Q3 | Base models named with version or snapshot date |
| Q4 | Decoding configuration reported: temperature, sampling, max tokens, seeds |
| Q5 | Benchmarks named, public, with split identified |
| Q6 | A no mitigation condition is included as a baseline |
| Q7 | At least one competing mitigation method is included as a baseline |
| Q8 | Baseline provenance stated, rerun or copied |
| Q9 | Metrics defined and appropriate; an LLM judge validated against human labels where used |
| Q10 | Variability addressed: repeated runs, confidence intervals, or a statistical test |
| Q11 | Inference cost reported: model calls, tokens, or latency per query |
| Q12 | Access requirement stated: whether the method needs logits or internals |

Bands: high 18 to 24, moderate 11 to 17, low 0 to 10.

Report the per item satisfaction rate across the corpus. That table is the direct answer to RQ5.

---

## 7. Extraction codebook

### Identification
`study_id`, `citation`, `year`, `venue`, `venue_type` {journal, conference, workshop, preprint}, `doi_or_url`

### Intervention, two levels
`intervention_layer` — the stage at which the method acts:

`prompt`, `sampling`, `decoding`, `retrieval`, `verification`, `abstention`, `orchestration`

`technique_family` — within that layer:

| Layer | Families |
|---|---|
| prompt | instruction or constraint prompting; few shot exemplar grounding; guided chain of thought; re prompting or re ask; structured output constraint |
| sampling | self consistency sampling; zero resource consistency check |
| decoding | contrastive decoding; constrained decoding; confidence or entropy guided decoding; lookahead decoding |
| retrieval | retrieval grounding; knowledge graph grounding; post hoc retrieval correction; adaptive or selective retrieval |
| verification | chain of verification; self refinement or self correction; decompose and verify; multi agent debate or critic; external tool verification |
| abstention | abstention or uncertainty expression |
| orchestration | pipeline combining two or more of the above |

Other fields: `technique_name_verbatim`, `combines_with`, `adaptivity` {none, fixed threshold, input conditioned, iterate until convergence, learned router}, `iteration_policy` {single pass, fixed N, until convergence, not_reported}, `iterations_n`, `verification_source` {self, second LLM, retrieval, external tool, none}, `access_level` {black box, grey box, white box}

`access_level` carries real weight that decoding is in scope. Model preserving is not the same as black box: contrastive decoding changes no weights but needs logits, so it cannot run against a commercial endpoint. Code it on every study.

`adaptivity` is the field carrying the third objective. Code it everywhere, including when the answer is `none`, because the count of `none` is the evidence for the gap.

### Evaluation
`task_setting`, `domain`, `hallucination_type` {factuality, faithfulness, both}, `benchmarks_verbatim`, `benchmark_split`, `base_models_verbatim`, `metrics_verbatim`, `metric_type` {reference based, reference free, LLM as judge, human, mixed}, `judge_validated` {yes, no, not applicable}, `baseline_none_included`, `baseline_competing_methods`, `baseline_source`

### Cost and availability
`calls_per_query`, `tokens_reported`, `latency_reported`, `code_available`, `prompts_published`, `data_available`

### Outcomes
Long table, one row per reported comparison: `result_id`, `study_id`, `benchmark`, `split`, `base_model`, `metric`, `baseline_name`, `baseline_value`, `proposed_value`, `direction`, `relative_change`, `calls_per_query`, `protocol_notes`, `provenance`

### Author statements
`claimed_novelty`, `claimed_limitation`

---

## 8. Synthesis and comparison plan

**RQ1.** Frequency of `intervention_layer` crossed with `adaptivity` and with `access_level`. The layer by access cross tabulation is the single most informative table you will produce, because it shows which layers are actually available to deployments without weight or logit access.

**RQ2.** Frequency of canonical benchmarks and domains. Report how many studies use a bespoke dataset and how many evaluate on more than one benchmark.

**RQ3.** Frequency of canonical metrics by `metric_type`. Report how many use an LLM as judge without validating it against human labels.

**RQ4, restricted comparison.** In order:

1. Build comparability groups keyed on benchmark, split, base model and metric.

2. Report head to head results only within groups containing two or more studies. State how many such groups exist and how many studies they cover.

3. Where a no mitigation baseline exists, express each result as relative change over that baseline. Relative change is comparable in direction across studies even when absolute values are not, provided you present direction and magnitude rather than a ranking.

4. Cross layer view: within comparable groups, compare layers rather than individual methods. This is where RQ4 earns its place, because whether decoding beats prompting is answerable at a coarser grain than whether method A beats method B.

For results outside those groups, use **vote counting by direction of effect**, reporting per layer how many studies improve, show no change, or worsen. Label it vote counting explicitly. It is an accepted method for heterogeneous evidence and it is honest, unlike an invented cross benchmark table.

**Cost adjusted view.** Where both an outcome delta and `calls_per_query` exist, report delta per additional call. Expect few studies to support it, and report that scarcity as part of RQ5.

**Sensitivity analyses.** Repeat RQ4 with low quality studies removed, and again with preprints removed. Report whether conclusions change.

---

## 9. Reporting
PRISMA 2020. Flow diagram with counts at identification, deduplication, title and abstract screening, full text assessment with reasons by criterion ID, and inclusion. Report Cohen kappa for both stages, the search validation test from 4.1, and the number excluded by the retrieval boundary test in 2.1. State that the protocol was fixed before screening began.

---

## 10. Amendments log
| Date | Section | Change | Reason |
|---|---|---|---|
| | | | |
