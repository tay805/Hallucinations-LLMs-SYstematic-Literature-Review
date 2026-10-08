# Protocol: Systematic Review of Training Free and Model Preserving Hallucination Mitigation in LLMs
Window: 30 November 2022 to 30 September 2026. Fixed before screening. Changes after that point go in the amendments log, Section 10.

## 1. Research questions
Revised to match the broadened scope. Changed wording is in bold.

| RQ | Question | Answered from |
|---|---|---|
| RQ1 | What **training free and model preserving** strategies are used to mitigate hallucination in LLMs, and **at which stage of inference do they act**? | `intervention_layer`, `technique_family`, `adaptivity`, `verification_source` |
| RQ2 | Which benchmark datasets and knowledge domains are most frequently used to evaluate these frameworks? | `benchmarks_canonical`, `domain`, `task_setting` |
| RQ3 | What evaluation metrics are used to assess factual consistency and reliability of LLM outputs? | `metrics_canonical`, `metric_type`, `judge_validated` |
| RQ4 | How do **mitigation strategies across intervention layers** perform relative to one another in reducing hallucination? | Restricted synthesis, Section 8 |
| RQ5 | What are the primary methodological limitations and open research gaps in the **training free mitigation** literature? | Quality appraisal plus RQ1 to RQ4 |

## 2. Eligibility criteria
Written as yes or no tests so two screeners reach the same verdict.

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
| Ex4 | Detection only | No component changes the model output. See 2.2 |
| Ex5 | Non textual modality only | Vision, image generation or audio with no text only condition |
| Ex6 | No empirical evaluation | No experiment of the authors' own |
| Ex7 | Duplicate | Same study, different version. Keep the most complete |

### 2.1 The retrieval boundary
Retrieval augmented generation is in scope and it is a very large field. This test is binding from the first screened record:

> **Include** a retrieval paper only if reducing hallucination, factual error or unfaithfulness is stated as a goal in the title, abstract or introduction, **and** at least one reported outcome is a hallucination, factuality or faithfulness metric.

>

> **Exclude** retrieval papers whose outcomes are only answer accuracy, exact match, retrieval recall, MAP, NDCG or latency, even where hallucination is mentioned in passing.

This keeps retrieval methods that target hallucination and removes the general RAG literature that merely nods at it. Record the count excluded by this test separately, because reviewers will ask how you bounded the scope.

### 2.2 Detection only papers
Ex4 removes them from the corpus. Keep a separate **signal register** of detection papers that supply a risk or confidence signal computable without weight access. Screen those on I1, I2 and Ex1 only, record signal type and cost, and exclude them from all synthesis. Declare it in the paper as a deliberate secondary collection. The reason is practical: RQ3 asks which metrics are used and detection work defines most of them, and a risk signal is the input any adaptive method would need.

### 2.3 The hybrid case Ex6 leaves open
Your wording excludes papers focused "exclusively" on training or fine tuning, which does not say what to do with a paper that combines fine tuning and an inference time method. Operational test:

> Ask whether the headline result can be reproduced with no gradient update. If yes, include, and code the tuned variant as out of scope context. If no, exclude under Ex6.

This keeps a paper whose main claim is an inference time method with an optional tuned variant, and removes one whose main claim requires tuning.

### 2.4 Preprints (adopted decision)
A preprint is included only where no peer reviewed version of the same study exists. Where both exist, the peer reviewed version is kept and the preprint is removed under Ex8. Every included preprint is flagged in `venue_type`, and Section 8 runs a sensitivity analysis with preprints removed. Excluding preprints outright would remove foundational work on this topic, so a blanket exclusion is not used.

---

## 3. Information sources
Your eight, plus two.

Add **arXiv** through Semantic Scholar, subject to the preprint rule. Add **DBLP or Semantic Scholar** for proper coverage of ACL, EMNLP, NAACL, COLING and NeurIPS, since ACL Anthology search alone is weak and the conference literature carries most of the decoding and verification work now in scope.

Record for every source: platform, exact string, field tags, date limits, search date, hits, exported count.

---

## 4. Corrected search strings
Three blocks: Population AND Problem AND Intervention. The intervention block now covers all five layers.

**Scopus**

```

TITLE-ABS-KEY (

 ("large language model\*" OR "language model\*" OR "LLM" OR "LLMs" OR "ChatGPT" OR "GPT-4"

  OR "instruction-tuned model\*" OR "generative AI")

 AND ("hallucinat\*" OR "factual\*" OR "faithful\*" OR "fabricat\*" OR "confabulat\*"

      OR "groundedness" OR "semantic consistency")

 AND ("prompt\*" OR "training-free" OR "inference-time" OR "decoding-time" OR "test-time"

      OR "contrastive decoding" OR "constrained decoding" OR "decoding strateg\*"

      OR "retrieval-augmented" OR "retrieval augmented generation" OR "RAG"

      OR "knowledge graph" OR "grounding" OR "self-refine\*" OR "self-correct\*"

      OR "self-consistency" OR "self-check\*" OR "self-verification"

      OR "chain-of-verification" OR "chain of verification" OR "verification"

      OR "re-prompt\*" OR "critic" OR "abstention" OR "uncertainty-aware" OR "post-hoc correction")

) AND PUBYEAR > 2021 AND PUBYEAR < 2027

```

**Web of Science**

```

TS=(

 ("large language model\*" OR "language model\*" OR "LLM" OR "LLMs" OR "ChatGPT")

 AND ("hallucinat\*" OR "factual\*" OR "faithful\*" OR "fabricat\*" OR "confabulat\*" OR "groundedness")

 AND ("prompt\*" OR "training-free" OR "inference-time" OR "decoding-time" OR "contrastive decoding"

      OR "constrained decoding" OR "retrieval-augmented" OR "RAG" OR "knowledge graph" OR "grounding"

      OR "self-refine\*" OR "self-correct\*" OR "self-consistency" OR "self-check\*"

      OR "chain-of-verification" OR "self-verification" OR "abstention" OR "uncertainty-aware")

)

```

Apply the 2022 to 2026 limit in the interface, and refine out clinical categories if the platform offers it.

**PubMed**

```

("large language model\*"[tiab] OR "LLM"[tiab] OR "ChatGPT"[tiab] OR "GPT-4"[tiab]

 OR "generative artificial intelligence"[tiab])

AND ("hallucinat\*"[tiab] OR "factual\*"[tiab] OR "faithful\*"[tiab] OR "fabricat\*"[tiab]

     OR "confabulat\*"[tiab])

AND ("prompt\*"[tiab] OR "training-free"[tiab] OR "inference-time"[tiab] OR "decoding"[tiab]

     OR "retrieval-augmented"[tiab] OR "RAG"[tiab] OR "grounding"[tiab] OR "self-refine\*"[tiab]

     OR "self-correct\*"[tiab] OR "self-consistency"[tiab] OR "chain-of-verification"[tiab]

     OR "verification"[tiab] OR "abstention"[tiab])

AND ("2022/11/30"[Date - Publication] : "2026/09/30"[Date - Publication])

```

The population block no longer accepts a bare hallucination term. That single change is what stops the psychiatry flood at source, and it makes Ex3 a safety net rather than your main defence.

**IEEE Xplore**

```

("Abstract":"large language model\*" OR "Abstract":"LLM" OR "Abstract":"ChatGPT")

AND ("Abstract":"hallucinat\*" OR "Abstract":"factual\*" OR "Abstract":"faithful\*"

     OR "Abstract":"groundedness")

AND ("Abstract":"prompt\*" OR "Abstract":"training-free" OR "Abstract":"inference-time"

     OR "Abstract":"decoding" OR "Abstract":"retrieval-augmented" OR "Abstract":"RAG"

     OR "Abstract":"grounding" OR "Abstract":"self-refine\*" OR "Abstract":"self-correct\*"

     OR "Abstract":"self-consistency" OR "Abstract":"chain-of-verification"

     OR "Abstract":"verification" OR "Abstract":"abstention")

```

Abstract rather than All Metadata, so precision is comparable with the other sources. If recall looks low, rerun on All Metadata and report both counts.

**ACM Digital Library** — the same three blocks with `Abstract:` prefixes.

**ACL Anthology, DBLP or Semantic Scholar**

```

("large language model" OR LLM) AND (hallucination OR factuality OR faithfulness OR groundedness)

AND (prompting OR "training-free" OR "inference-time" OR decoding OR "contrastive decoding"

     OR "retrieval-augmented" OR grounding OR "self-refinement" OR "self-correction"

     OR "self-consistency" OR "chain-of-verification" OR "self-verification" OR abstention)

```

**Lens.org and Springer** — the Scopus form, with straight quotation marks only. Your Lens string currently has curly quotation marks around `"hallucination\*"` and will be rejected as written.

### 4.1 Validate before running at scale
Choose six papers you already know belong, one per intervention layer: a prompting method, a sampling or consistency method, a contrastive decoding method, a retrieval grounding method, a chain of verification method, and an abstention method. Every corrected string must return all six. A string that misses one is wrong, not the paper. Record the test in the search log, since reviewers increasingly ask for it.

---

## 5. Screening
**Stage 1, title and abstract.** Apply I1, I2, I4 and Ex1, Ex2, Ex3, Ex5, Ex8 only. When in doubt, advance the record. Over inclusion here is cheap; over exclusion is permanent and invisible.

**Stage 2, full text.** Apply everything, including the retrieval boundary test in 2.1 and the hybrid test in 2.3. Record exactly one exclusion reason per excluded paper, using the criterion ID rather than free text, because PRISMA needs the counts tabulated.

**Agreement.** Both screeners independently screen a random 20 percent at each stage. Compute Cohen kappa and report it. Below 0.70, stop, rewrite the criterion that caused the disagreement, and rescreen. Resolve conflicts by discussion, with a third party only for deadlock.

**Snowballing.** After Stage 2, backward snowball the reference lists of all included papers and of the surveys excluded under Ex2, which is the one good use for that material. Forward snowball the five most cited included papers. Run new candidates through both stages and report them separately in the flow diagram.

---

## 6. Quality appraisal
Scored for every included study. Used for sensitivity analysis and for RQ5. Never an eligibility filter.

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

Q2, Q8, Q11 and Q12 are the ones that usually fail. Report the per item satisfaction rate across the corpus, not just totals. That table is the direct answer to RQ5. Q12 matters particularly now that decoding methods are in scope, because a method needing logit access cannot run against a commercial endpoint, and papers seldom say so.

---

## 7. Extraction codebook
One record per study. Every value traced to a section, table or page. Absent values recorded as `not_reported`, never inferred. Record names verbatim at extraction; canonicalise once, globally, afterwards.

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

`access_level` carries real weight now that decoding is in scope. Model preserving is not the same as black box: contrastive decoding changes no weights but needs logits, so it cannot run against a commercial endpoint. Code it on every study.

`adaptivity` is the field carrying your third objective. Code it everywhere, including when the answer is `none`, because the count of `none` is the evidence for the gap.

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
Narrative synthesis with structured tabulation. No meta-analysis: the outcome measures are not commensurable and pooling them would misrepresent the evidence.

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
