# Alternative Protein Consumer Psychology

## Computational Discovery of Psychological Barriers in Alternative-Protein Discourse

This repository contains a proof-of-concept computational pipeline for identifying **psychological signals associated with consumer responses to alternative-protein products**.

The project is designed as an exploratory first-stage study within a broader **computational-to-experimental research programme**. It uses naturally occurring consumer discourse to identify candidate psychological barriers that can subsequently be examined through controlled behavioural experiments.

The conceptual framing is informed by research on novel-food differentiation, sustainability-related differentiation, and perceived naturalness in plant-based meat alternatives, including work by **Arnd Florack and colleagues**.

### Research motivation

Consumers do not necessarily evaluate novel food alternatives by considering all of their attributes equally. Research on the **Differentiation Principle** suggests that consumers may disproportionately attend to attributes that distinguish a novel food from a familiar alternative, which can affect taste expectations and purchase intentions.

Related work on the **sustainability liability** shows that sustainability attributes can become positive or negative differentiators depending on how a novel food is evaluated. More recent work on plant-based meat alternatives highlights the role of perceived processing and naturalness.

This repository asks a complementary exploratory question:

> **What psychological signals spontaneously appear in naturally occurring consumer discourse about alternative-protein products?**

The purpose is not to establish causal psychological mechanisms from text alone. Instead, the analysis is intended to generate **theoretically informed hypotheses for subsequent behavioural validation**.

---

## Research objectives

The pipeline is designed to:

1. Identify recurring psychological signals in alternative-protein consumer discourse.
2. Operationalise constructs relevant to novel-product evaluation and adoption.
3. Examine how these signals vary across consumer discussions and platforms.
4. Generate interpretable textual evidence associated with identified constructs.
5. Discover broader thematic patterns using topic modelling.
6. Translate exploratory findings into candidate hypotheses and communication interventions for subsequent experimental testing.

---

## Psychological construct taxonomy

The current exploratory taxonomy contains ten constructs:

| Construct | Operational focus |
|---|---|
| `differentiation_from_meat` | Comparisons between alternative proteins and conventional meat |
| `perceived_processing` | Concerns about ultra-processing, additives, or industrial production |
| `naturalness_perceptions` | Perceptions of products as artificial, synthetic, fake, or unnatural |
| `taste_expectations` | Expectations regarding taste, texture, and sensory quality |
| `sustainability_differentiation` | Evaluation or questioning of environmental and sustainability claims |
| `anchoring_to_meat` | Use of conventional meat as the default benchmark |
| `perceived_loss_switching` | Expected losses in enjoyment, satiety, nutrition, or other valued attributes |
| `trust_and_credibility` | Concerns about transparency, corporate motives, and credibility |
| `uncertainty_and_risk` | Uncertainty concerning health, safety, ingredients, or longer-term risks |
| `social_acceptance` | Concerns about social judgement, family acceptance, and cultural norms |

These constructs are **operational hypotheses**, not validated psychological scales.

---

## Methodology

### 1. Consumer discourse corpus

The supplied exploratory corpus contains:

- **123 consumer discussions**
- Sources labelled **X/Twitter and Reddit**
- Alternative-protein topics including plant-based and cultivated/lab-grown meat
- Text-level metadata including source, topic, and approximate date

The corpus is used as a proof-of-concept dataset rather than as a representative sample of the population.

### 2. Zero-shot construct classification

The pipeline uses:

- `facebook/bart-large-mnli`
- Multi-label zero-shot classification
- Ten theoretically specified construct descriptions

Each text receives a model score for each construct.

The resulting scores should be interpreted as **model-assigned construct probabilities/scores**, not as observed prevalence or validated psychological measurements.

### 3. Dominant construct analysis

For each text, the construct with the highest model score is assigned as the dominant construct.

This provides an exploratory description of which construct the model considers most salient within individual texts.

### 4. Cross-platform comparison

Where both platform groups are available, the pipeline uses the **Mann–Whitney U test** to compare construct scores across platforms.

These comparisons are exploratory and should not be interpreted as population-level causal or representative estimates.

### 5. Interpretable text analysis

`KeyBERT` is used to extract semantically relevant keyphrases from selected texts and from groups of texts dominated by particular constructs.

This provides qualitative evidence that can be inspected alongside model scores.

### 6. Topic modelling

`BERTopic` with sentence-transformer embeddings is used to identify broader thematic clusters independently of the predefined psychological taxonomy.

This provides a complementary, less theory-constrained view of recurring discourse themes.

---

## Exploratory results

The current run produced the following **mean model scores across the 123 texts**:

| Construct | Mean model score |
|---|---:|
| Uncertainty and risk | **53.1%** |
| Differentiation from meat | **41.4%** |
| Naturalness perceptions | 30.7% |
| Perceived processing | 29.3% |
| Sustainability differentiation | 27.5% |
| Perceived loss from switching | 23.8% |
| Trust and credibility | 15.1% |
| Taste expectations | 11.8% |
| Social acceptance | 11.2% |
| Anchoring to meat | 1.1% |

The dominant-construct distribution was:

- Uncertainty and risk: **64/123 (52.0%)**
- Differentiation from meat: **27/123 (22.0%)**
- Sustainability differentiation: **18/123 (14.6%)**
- Naturalness perceptions: **8/123 (6.5%)**
- Perceived loss from switching: **4/123 (3.3%)**
- Perceived processing: **2/123 (1.6%)**

An exploratory cross-platform Mann–Whitney comparison also identified a statistically significant difference in the model score for **sustainability differentiation (p = 0.0029)**.

### Important interpretation

The values above are **zero-shot model scores**, not prevalence estimates. In particular, a mean score of 53.1% does **not** mean that 53.1% of consumers have a validated uncertainty/risk barrier.

Likewise, the original analysis used a >40% rule to flag high-scoring constructs. This repository treats that as an **exploratory reporting threshold**, not a statistical significance test.

The results therefore support **hypothesis generation**, not causal inference.

---

## Connection to the proposed research programme

The computational stage is designed as a first step in a larger research sequence:

```text
Naturally occurring consumer discourse
                ↓
Computational discovery
                ↓
Theoretically grounded hypotheses
                ↓
Controlled behavioural experiments
                ↓
Causal validation of psychological pathways
                ↓
Psychologically tailored communication interventions
```

The exploratory findings suggest candidate mechanisms for later testing, particularly:

- differentiation from conventional meat;
- uncertainty and perceived risk;
- naturalness and processing perceptions;
- sustainability-related differentiation.

For example, a subsequent experiment could manipulate how an alternative-protein product is described relative to conventional meat and test effects on perceived differentiation, naturalness, expected taste, product evaluation, and adoption intention.

The computational results **do not establish these causal pathways**. Their purpose is to help identify and prioritise mechanisms for experimental testing.

---

## Relevance to consumer-psychological research

The project is particularly connected to research on:

- **novel-product differentiation**;
- **taste expectations and purchase intentions**;
- **sustainability as a differentiating attribute**;
- **naturalness and perceived processing**;
- consumer responses to **plant-based and other alternative proteins**.

Key conceptual references include:

- Florack et al. (2021), *The Differentiation Principle: Why Consumers Often Neglect Positive Attributes of Novel Food Products*, Journal of Consumer Psychology. DOI: `10.1002/jcpy.1222`
- Kunz et al. (2021), *The sustainability liability revisited: Positive versus negative differentiation of novel products by sustainability attributes*, Appetite. DOI: `10.1016/j.appet.2021.105637`
- Steiner, Kunz & Florack, *Less is more: How package color saturation influences naturalness perceptions of plant-based meat alternatives*, University of Vienna research record.

---

## Repository structure

```text
alternative-protein-consumer-psychology/
│
├── data/
│   └── alt_protein_discussions.csv
│
├── output/
│   ├── alt_protein_results.csv
│   └── alt_protein_summary.csv
│
├── notebook/
│   └── alternative_protein_psychology_pipeline.ipynb
│
├── requirements.txt
├── README.md
└── .gitignore
```

---

## Reproducibility

The analysis is implemented in Python.

Main components:

- Python
- pandas
- NumPy
- SciPy
- Hugging Face Transformers
- PyTorch
- Sentence Transformers
- BERTopic
- KeyBERT
- scikit-learn

The notebook automatically detects whether CUDA is available and otherwise falls back to CPU.

### Installation

```bash
git clone <your-repository-url>
cd alternative-protein-consumer-psychology

python -m venv .venv
```

Windows:

```bash
.venv\Scripts\activate
```

macOS/Linux:

```bash
source .venv/bin/activate
```

Install dependencies:

```bash
pip install -r requirements.txt
```

Launch Jupyter:

```bash
jupyter notebook
```

Then open:

```text
notebook/alternative_protein_psychology_pipeline.ipynb
```

---

## Data and ethical considerations

The repository is intended for research and methodological demonstration.

The included corpus contains user-generated text and source metadata. Researchers reproducing or extending the project should comply with the terms of the relevant platforms, applicable privacy/data-protection requirements, and institutional research-ethics procedures.

For a public repository, personally identifying fields such as usernames/handles should be removed or anonymised unless their publication is clearly justified and permitted.

The present analysis should not be interpreted as representative of all consumers or all alternative-protein markets.

---

## Limitations

This proof-of-concept has several important limitations:

1. **Small exploratory corpus:** 123 texts are insufficient for population-level inference.
2. **Non-probability sampling:** platform users are not representative of consumers generally.
3. **Zero-shot classification:** model scores are not validated psychological measurements.
4. **Construct overlap:** concepts such as naturalness, processing, uncertainty, and differentiation can co-occur.
5. **No causal identification:** text analysis cannot establish whether a construct causes adoption or rejection.
6. **Human validation is still required:** future work should use expert/human annotation and reliability assessment.
7. **Platform effects:** discourse characteristics may differ systematically across platforms.
8. **Topic modelling instability:** the small corpus limits the stability and generalisability of discovered topics.

These limitations motivate the proposed transition from computational discovery to controlled behavioural experimentation.

---

## Future development

The next methodological stage should:

- expand the corpus substantially;
- add systematic human annotation;
- assess inter-rater reliability;
- refine construct definitions;
- compare alternative classification models;
- examine construct co-occurrence;
- test robustness across platforms and product categories;
- pre-register key hypotheses before experimental validation;
- experimentally test whether identified psychological barriers influence product evaluation, adoption intention, and choice.

The ultimate objective is to use computational analysis as a **hypothesis-generation and measurement-support tool**, rather than as a substitute for behavioural experimentation.

---

## Citation

If you use this repository or its methodology, please cite the relevant underlying research and acknowledge the exploratory nature of the computational analysis.

### Core conceptual references

Florack, A., Koch, T., Haasova, S., Kunz, S., & Alves, H. (2021). The Differentiation Principle: Why Consumers Often Neglect Positive Attributes of Novel Food Products. *Journal of Consumer Psychology, 31*(4), 684–705. https://doi.org/10.1002/jcpy.1222

Kunz, S., Florack, A., Campuzano, I., & Alves, H. (2021). The sustainability liability revisited: Positive versus negative differentiation of novel products by sustainability attributes. *Appetite, 167*, 105637. https://doi.org/10.1016/j.appet.2021.105637
