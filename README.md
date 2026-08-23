# Responsive Facade Visual–Semantic Data

## Can Visual Clusters Support Semantic Steering? A Cross-Scale Study of Responsive-Façade Images

This repository provides the **derived research data and generated experimental outputs** associated with the paper titled above.

The study investigates façade imagery in active responsive architecture and develops an interpretable visual–semantic workflow connecting architectural image features, unsupervised clustering, cross-scale analysis, researcher-reviewed semantic mapping, and controlled generative-AI validation.

The repository contains case metadata, ResNet-50 image embeddings, 43-dimensional interpretable visual features, Set A and Set B cluster memberships, image-level CLIP evaluation records from two independent controlled-generation batches, the 144 generated images used in the formal generative experiment, the complete generation prompts and recorded parameters, six-prototype similarity scores and predicted prototype labels, and the confusion-matrix data used for the class-specificity analysis.

> **Note on scope.** The results released here are **conditional on a specific analytical configuration**. Cluster memberships, the cross-scale relationship, and the semantic prototypes all change under alternative feature weightings (Sections 7 and 8). They are exploratory research outputs, not a fixed façade taxonomy.

---

# 1. Research Overview

Architectural visual research has progressively expanded from conventional stylistic and typological classification toward computer-vision-based image analysis. More recently, generative artificial intelligence has extended architectural visual research from recognition and classification toward semantic modeling and design generation.

Active responsive architecture provides a particularly challenging visual domain because façade states may be influenced by mechanical components, smart materials, sensors, environmental conditions, control systems, and user interaction. Its visible characteristics therefore involve not only static formal composition but also component configuration, material articulation, geometric organization, environmental context, and visible indications of potential responsive behavior.

Conventional typological labels or designer-authored natural-language descriptions may not consistently represent these heterogeneous visual characteristics. Rather than defining fixed architectural categories in advance, this study extracts computable visual features from architectural images, identifies visual organization through unsupervised clustering, and subsequently interprets the resulting clusters using within-cluster samples, representative images, standardized feature profiles, and project-level contextual information.

The core methodological pathway is:

**Visual Features → Cluster Structure → Architectural Interpretation → Researcher-Reviewed Semantic Labels → Controlled Generative Validation**

The objective is not to establish a universal taxonomy of active responsive architecture. Instead, the study develops an interpretable **visual–semantic interface** through which architectural visual differences can be organized into structured semantic information for image analysis, prompt construction, and generative-AI design-variable organization.

---

# 2. Data at a Glance

| Item | Count |
| --- | --- |
| Architectural cases | 75 |
| Paired analytical images | 150 |
| Set A close-up observations | 75 |
| Set B full-façade observations | 75 |
| Observation scales | 2 |
| Interpretable visual features per image | 43 |
| ResNet-50 embedding dimensions per image | 2,048 |
| Working granularity per observation scale | K = 6 |
| Exploratory visual–semantic prototypes | 12 |
| Independent controlled-generation batches | 2 |
| Generated images in the formal experiment | 144 |
| Image-level CLIP evaluation records | 144 |
| Generation-prompt and parameter records | 144 |
| Six-prototype similarity and prediction records | 144 |
| Confusion-matrix cells (Set × Condition × Target × Prediction) | 144 |

The released materials consist of case-level metadata, derived numerical image representations, interpretable visual-feature matrices, clustering outputs, generative evaluation records, the 144 AI-generated experimental images, complete generation prompts and recorded parameters, same-scale six-prototype similarities and predicted labels, and the confusion-matrix data used in the class-specificity analysis.

---

# 3. Dual-Scale Dataset Structure

Each of the 75 architectural cases is represented at two observation scales.

### Set A — Close-Up Images

Set A contains 75 close-up observations emphasizing local façade components, material textures, connections, open or closed states, repetitive modules, and local geometric organization.

### Set B — Full-Façade Images

Set B contains 75 full-façade observations emphasizing overall building massing, façade composition, proportional organization, lighting conditions, environmental background, and building–site relationships.

The analytical dataset therefore follows a paired structure:

**75 cases × 2 observation scales = 150 architectural images**

Corresponding case identifiers are retained across Set A and Set B, enabling case-level comparison between local component-scale and overall façade-scale visual organization.

The cases were selected through purposive sampling across the open web, architectural media, design-firm websites, and project platforms. Built, competition, conceptual, and research cases with clear active response characteristics were included. After excluding images of nontarget buildings, corrupted files, severe defocus, and samples in which the primary subject could not be identified, 75 cases remained.

Accordingly, the dataset should be interpreted as a **purpose-built exploratory research sample**, rather than a statistically representative sample of active responsive architecture as a whole.

---

# 4. Research Pipeline

The study follows the analytical sequence:

**Dataset Construction → Benchmark Representation → Visual-Feature Clustering → Robustness Validation → Semantic Mapping → Generative Validation**

## 4.1 Preprocessing

Image preprocessing comprised six steps: exposure and color-cast correction, size standardization, geometric correction, manual cropping, edge-preserving denoising, and format unification.

One researcher performed the procedure and another reviewed it independently. Color and exposure corrections addressed only evident deviations; no cross-sample homogenization was applied. Perspective correction preserved building proportions and component relationships, while cropping removed only nonarchitectural and temporary distractions. No geometry, material, or texture was added, removed, or redrawn, and color outliers were retained.

Complete clustering of the raw and preprocessed images produced identical memberships, indicating that preprocessing did not alter sample assignment.

## 4.2 Benchmark Representation

An ImageNet-1K-pretrained **ResNet-50** implemented in PyTorch was used as a reference for general deep representation, rather than as an algorithmic-performance competitor to the handcrafted visual features. From the 75 raw images in each of Sets A and B, 2,048-dimensional embeddings were extracted after global average pooling of `layer4` and normalized with the L2 norm.

The two sets of 2,048-dimensional vectors were concatenated case by case with equal weighting to form a **75 × 4,096 joint matrix**. K-means solutions for K = 2–10 were compared in the full space, and **K = 2** was retained as a coarse-grained working baseline.

## 4.3 Interpretable Feature Space and Clustering

Sets A and B each produced a **75 × 43 feature matrix**. To calibrate a common value of K, the two sets were concatenated case by case into a **75 × 86 joint matrix**.

Principal component analysis (PCA) was performed after **variable-wise Z-score standardization**. Two-, three-, five-, and ten-dimensional PCA spaces were compared with the complete standardized feature space. The working value of K and clustering performance changed with the analysis space.

K-means used k-means++ initialization and Lloyd's algorithm; clustering and evaluation were implemented in scikit-learn. Solutions for K = 2–10 were compared without prior labels, using the silhouette coefficient, the Calinski–Harabasz (CH) index, and the Davies–Bouldin (DB) index.

In the two-dimensional PCA space at K = 6, the joint solution reached a mean silhouette coefficient of **0.4357** and a CH index of **73.8157**, with joint cluster sizes of **20, 14, 11, 11, 10, and 9** cases.

Two-dimensional PCA and K = 6 are used **only as an exploratory working space and granularity** for cross-scale semantic comparison. They do not represent the intrinsic structure of the complete feature space, and K = 6 does not imply that active responsive architecture inherently consists of six natural façade categories.

Set A and Set B were then clustered independently under the shared K value. Their paired cross-scale relationships were examined, followed by feature-group equal weighting, feature-group ablation, K-sensitivity analysis, ResNet-50 same-pipeline comparison, independent architectural-attribute validation, researcher-reviewed semantic mapping, and controlled generative evaluation.

---

# 5. Repository Contents

The repository contains twelve research-data and experimental-output files.

```
responsive-facade-visual-semantic-data/
│
├── README.md
├── LICENSE
├── 01_case_metadata.csv
├── 02_Original_images_resnet50_embeddings.csv
├── 03_Set A_visual_features_43D.csv
├── 04_Set B_visual_features_43D.csv
├── 05_Set A_cluster_membership.csv
├── 06_Set B_cluster_membership.csv
├── 07_Batch 1 CLIP_Scores.csv
├── 08_Batch 2 CLIP_Scores.csv
├── 09_Generated_experiment_images.xlsx
├── 10_Generation_Prompts_and_Parameters.csv
├── 11_Six_Prototype_Similarity_and_Predictions.csv
└── 12_Figure_22_Confusion_Matrix.csv
```

A recommended inspection order is `01 → 02 → 03/04 → 05/06 → 07/08 → 09 → 10 → 11 → 12`, which follows the analytical sequence of the study.

---

### `01_case_metadata.csv`

Metadata for the 75 architectural cases. It records the correspondence between Set A and Set B and provides project-level information used for contextual interpretation and independent architectural-attribute validation.

The metadata include basic building information (name, year of completion, floor area, number of stories, building type), designer information (architect name and nationality), response-mechanism attributes, and geographical and climate information (country, city, latitude, longitude, minimum temperature, maximum temperature, annual mean temperature, annual precipitation, mean daily precipitation, humidity).

The four response-mechanism attributes are **response target**, **actuation mechanism**, **construction type**, and **material type**. Their coded categories are defined in the file; latitude and longitude fields follow their conventional geographic definitions.

**Two notes for users of the association analyses.** Cases carrying more than one label on a categorical attribute were combined into a `multiple` category, and missing values were not imputed. Climate variables are available for **73 of the 75 cases**; the categorical attributes are complete at n = 75.

The file does **not** contain the original architectural images.

---

### `02_Original_images_resnet50_embeddings.csv`

ResNet-50 embeddings derived from the 150 architectural source images. Each record contains observation set, case identifier, image identifier, and 2,048 embedding dimensions extracted after global average pooling of `layer4`.

The file contains **150 image records**: 75 Set A observations and 75 Set B observations. The embeddings are L2-normalized and provide the general deep visual representation baseline used in the study.

Despite the filename, this file contains **numerical embeddings only and does not contain the original architectural images**.

---

### `03_Set A_visual_features_43D.csv`

Interpretable visual features extracted from the 75 Set A close-up observations. Each record includes image-identification fields and the 43 visual-feature variables used for the principal clustering analysis.

The data support variable-wise standardization, PCA, K-means clustering, cluster-level visual-feature profiling, robustness analysis, and subsequent semantic interpretation at the close-up scale.

---

### `04_Set B_visual_features_43D.csv`

The corresponding interpretable visual features extracted from the 75 Set B full-façade observations. The same 43-dimensional feature structure is used for both sets, enabling independent clustering and paired cross-scale comparison.

---

### `05_Set A_cluster_membership.csv`

K = 6 working cluster memberships of the 75 Set A observations. Cluster sizes for Clusters 0–5 are **13, 17, 18, 12, 8, and 7** observations.

The file supports cluster-member inspection, representative-image identification, cluster-level feature profiling, and Set A–Set B cross-scale association analysis.

---

### `06_Set B_cluster_membership.csv`

K = 6 working cluster memberships of the 75 Set B observations. Cluster sizes for Clusters 0–5 are **20, 12, 8, 17, 10, and 8** observations.

Together with the Set A membership file, it supports paired case-level comparison between close-up and full-façade visual organization.

---

### `07_Batch 1 CLIP_Scores.csv`

**72 image-level evaluation records** from the first controlled-generation batch. The formal Batch 1 analysis uses replicates **R4–R6**; earlier replicate identifiers correspond to preparatory generations that are not part of the formal experiment and are not released.

Each record contains identifiers for observation scale, cluster, prompt condition, and replicate, together with CLIP-derived evaluation measures:

- target–text similarity;
- target–text margin relative to the strongest competing target;
- target–text Top-1 indicator;
- visual–prototype similarity;
- visual–prototype margin relative to the strongest competing prototype;
- visual–prototype Top-1 indicator.

---

### `08_Batch 2 CLIP_Scores.csv`

**72 image-level evaluation records** from the second independent controlled-generation batch, using replicates **R7–R9**. Files 07 and 08 together provide the **144 image-level CLIP evaluation records** used in the formal controlled-generation analysis.

---

### `09_Generated_experiment_images.xlsx`

The **144 generated images used in the formal controlled-generation experiment**: 72 Batch 1 images (R4–R6) and 72 Batch 2 images (R7–R9).

Each image is an independent experimental output rather than a duplicated preview or summary illustration. The 144 images correspond to the evaluation records in Files 07 and 08 and to the generation records in File 10.

---

### `10_Generation_Prompts_and_Parameters.csv`

The complete generation record for the 144 formal experimental images. Each row corresponds to one generated image and includes sample identifier, experimental batch, observation set, target cluster, prompt condition, replicate identifier, the complete English generation prompt, prompt-record status, recorded generation system information, image width and height, aspect ratio, fixed experimental generation conditions, other recorded generation-parameter information, the corresponding image filename, an SHA-256 image hash, and evidence-record information.

The file contains **144 rows = 72 Free Prompt outputs + 72 Semantic Prompt outputs**, across Set A, Set B, Batch 1, and Batch 2. Generated images have recorded dimensions of **1254 × 1254 pixels** (1:1 aspect ratio).

Only generation parameters that were **actually recorded during the experiment** are reported. Where an exact model version, random seed, quality setting, or style setting was not recorded, the file explicitly identifies the parameter as **not recorded** rather than retrospectively reconstructing or inferring unavailable settings.

---

### `11_Six_Prototype_Similarity_and_Predictions.csv`

Complete same-scale six-prototype similarity results for all 144 formally evaluated generated images. Each generated image is compared with all six visual prototypes from its corresponding observation scale.

Each record includes image identifier, observation set, target cluster, prompt condition, batch, replicate, `Similarity_C0` through `Similarity_C5`, predicted cluster, own-prototype similarity, strongest competing-prototype similarity, prototype margin, and Top-1 correctness indicator.

Definitions:

- **Predicted cluster** — the prototype with the highest CLIP similarity among the six prototypes of the corresponding observation scale.
- **Own-prototype similarity** — CLIP similarity between the generated image and its intended target-cluster prototype.
- **Strongest competing-prototype similarity** — the maximum similarity among the five non-target prototypes.
- **Prototype margin** — own-prototype similarity minus strongest competing-prototype similarity. A positive margin indicates that the intended prototype is more similar to the generated image than every competing prototype.
- **`Top1_Correct`** — 1 when the predicted cluster equals the target cluster, 0 otherwise.

This file provides the complete underlying data required to independently inspect the class-specificity analysis.

---

### `12_Figure_22_Confusion_Matrix.csv`

Complete confusion-matrix data for the same-scale nearest-prototype class-specificity analysis presented in Figure 22 of the associated paper.

The file covers all combinations of Set A / Set B, Free / Semantic condition, Target Clusters 0–5, and Predicted Clusters 0–5:

**2 Sets × 2 Conditions × 6 Target Clusters × 6 Predicted Clusters = 144 matrix cells**

Counts are derived directly from the `Predicted_Cluster` values in File 11. The four corresponding confusion matrices each cover 36 generated images: Set A Free, Set A Semantic, Set B Free, and Set B Semantic.

---

# 6. The 43-Dimensional Interpretable Visual Feature Space

Each Set A and Set B observation is represented by a **43-dimensional visual feature vector** consisting of four feature groups.

| Feature group | Dimensions | Description |
| --- | ---: | --- |
| SSIM | 1 | Grayscale structural similarity between each image and the within-scale pixel-wise mean template |
| Mean RGB | 3 | Mean red, green, and blue channel values |
| Gradient-orientation histogram | 32 | L1-normalized 32-bin distribution of major edge directions |
| Hu moments | 7 | Signed-log Hu moments representing global shape and contour distributions |
| **Total** | **43** | |

**SSIM** functions as a proxy for image-level structural and compositional similarity rather than an architectural performance measure.

**Mean RGB** values describe image-level color characteristics and do not directly identify construction materials.

**Gradient-orientation** features characterize directional structure, geometric organization, repetitive façade patterns, and compositional order.

**Hu moments** provide shape-related visual information but are not interpreted as direct measurements of architectural symmetry, formal complexity, material behavior, or responsive mechanisms.

Because the four groups contain unequal numbers of variables, variable-wise standardization does not give them equal influence on the Euclidean distance. This is examined directly in Section 8.

All 43 variables are treated as **computational proxies for visual organization**, rather than direct indicators of structural performance, responsive performance, environmental performance, material properties, buildability, or overall architectural quality.

---

# 7. K = 6 and the Cross-Scale Relationship

In the two-dimensional PCA exploratory space, K = 6 was retained as the common working granularity for Set A and Set B. The two observation scales share the same K value but were clustered independently.

**Under the original weighting specification**, the paired case-level cross-scale comparison produced:

**ARI = 0.033  ·  NMI = 0.194  ·  Permutation test: p = 0.0065**

The low ARI and NMI indicate that Set A and Set B do **not** form a stable one-to-one cluster correspondence, although the permutation test places the observed relationship above chance under random case pairing.

### This above-chance association is not robust

After group-level equal weighting of the four feature groups (Section 8), the cross-scale association was **no longer significant (p = 0.829)**.

The cross-scale relationship reported above is therefore **conditional on the original weighting specification**. It should not be read as evidence of a representation-independent correspondence between the two observation scales.

Qualitatively, under the original specification Set A clusters separate mainly by component form, material texture, connection methods, and modular order, whereas Set B clusters additionally integrate building massing, façade composition, lighting conditions, and environmental relationships.

The two scales are not interchangeable. However, the present data do **not** support a stable, weighting-independent complementarity between them.

---

# 8. Robustness and Representation Dependence

Because the four visual-feature groups contain different numbers of variables, additional analyses were conducted to examine feature-weighting effects. After variable-wise Z-score standardization, the SSIM, RGB, orientation-histogram, and Hu-moment variables were divided by **√1, √3, √32, and √7** respectively, giving equal weight to the four feature groups. PCA–K-means was then rerun.

Agreement between the original and equal-weight clusterings was low:

**Set A: ARI = 0.022  ·  Set B: ARI = 0.083**

Jaccard overlap between matched clusters from the original and revised solutions was **0.125–0.333**.

Under equal weighting, the cross-scale association reported in Section 7 was **no longer significant (p = 0.829)**.

Both cluster membership and the cross-scale relationship are therefore sensitive to feature-group weighting. The equal-weight solutions nevertheless retained measurable initialization and subsampling stability, so the finding is one of **representation and configuration dependence**, not of general instability.

Feature-group ablation showed that RGB had the greatest influence on the partitions at both scales, whereas Hu moments had the smallest overall influence. K-sensitivity analysis likewise did not identify K = 6 as a representation-independent unique optimum.

Accordingly, the K = 6 memberships released in this repository should be interpreted as:

**exploratory partitions obtained under a specific dataset, visual-feature representation, weighting configuration, PCA space, and K-means analysis pipeline.**

They should **not** be interpreted as universal, immutable, or naturally occurring categories of active responsive architecture.

---

# 9. ResNet-50 Same-Pipeline Validation and Independent Architectural Attributes

## 9.1 ResNet-50 Same-Pipeline Comparison

To examine whether the clustering conclusions depended on the handcrafted visual representation, ResNet-50 features were also evaluated using the same analytical pipeline.

The complete paired ResNet-50 representation again supported **K = 2** as a coarse-grained working baseline; in the two-dimensional PCA space the two clusters contained 72 and 3 cases. When K was fixed at 6 for same-pipeline comparison, ResNet-50 produced single-sample clusters in both the joint data and Set A, while the smallest Set B cluster contained three samples.

The general deep representation can therefore produce repeatable coarse visual partitions, but the fixed K = 6 ResNet-50 solution was substantially more unbalanced than the principal 43-dimensional feature solution. ResNet-50 was consequently retained as a **representation baseline and sensitivity reference**, rather than being adopted as the principal space for the 12-prototype visual–semantic interpretation.

## 9.2 Independent Architectural Attributes

The study additionally examined associations between the K = 6 visual partitions and independently recorded architectural attributes: **response target**, **actuation mechanism**, **construction type**, **material type**, and **climate conditions**.

Categorical attributes were tested with Monte Carlo permutation chi-square tests; climate variables were tested with permutation Kruskal–Wallis tests. Cramér's V and ε² were reported as effect sizes. Cases with more than one label were combined into a `multiple` category, and missing values were not imputed. P values were adjusted with the Benjamini–Hochberg false-discovery-rate procedure, with q < .05 treated as significant. Categorical variables were tested at n = 75 and climate variables at n = 73.

After adjustment, only **construction type** was significantly associated with both partitions:

**Set A: q = .002, Cramér's V = .426**

**Set B: q = .018, Cramér's V = .390**

Response target, actuation mechanism, material type, and climate variables showed no significant associations (**q ≥ .387**).

These results indicate that the visual partitions reflect constructional differences in part, but they should **not** be interpreted as categories directly determined by response mechanism, material type, or climatic conditions.

---

# 10. Visual–Semantic Mapping

Set A and Set B each contain six visual clusters under the working K = 6 configuration, resulting in **12 exploratory visual–semantic prototypes**.

For each cluster, the real sample with the shortest Euclidean distance to the K-means centroid was selected as the primary representative image. A representative image cannot independently reveal the full architectural semantics and is used only for visual presentation.

Semantic mapping was **researcher-led**. Candidate descriptions first combined visible characteristics, cluster-level feature profiles, and documented information about mechanisms or context. ChatGPT was used only to suggest and refine candidate wording; labels were not generated automatically from the features. The researchers then verified, consolidated, and condensed those descriptions.

The resulting labels should therefore be understood as **researcher-reviewed exploratory visual–semantic labels**, rather than automatically generated architectural labels or objectively fixed architectural classes.

The semantic mapping functions as an interpretive middle layer connecting computational visual organization with architectural language and the subsequent generative experiments, while avoiding a direct equation of static visual cues with material performance or response mechanisms.

---

# 11. Controlled Generation and CLIP Evaluation

Two prompting conditions were compared.

**Free Prompt** — common constraints on building type, observation scale, composition, style, lighting, and negative constraints.

**Semantic Prompt** — the same base constraints, plus a structured cluster-level semantic description.

The only systematic difference between the two conditions was therefore **whether cluster-level structured semantic information was included**.

The experiment covered 12 semantic targets across Sets A and B and generated 144 images in two independent batches:

**12 targets × 2 conditions × 3 images × 2 batches = 144 generated images**

The **12 semantic clusters served as the units of inference**. Cluster-level Semantic–Free paired differences were pooled with equal weighting, evaluated with a two-sided exact sign-flipping test, and accompanied by cluster-level bootstrap confidence intervals.

Generated images are provided in `09_Generated_experiment_images.xlsx`; prompts and recorded conditions in `10_Generation_Prompts_and_Parameters.csv`; image-level CLIP records in `07_Batch 1 CLIP_Scores.csv` and `08_Batch 2 CLIP_Scores.csv`.

### Target–Text Similarity

Alignment between each generated image and its target semantic text. Equal-weight pooled results:

| Condition | Value |
| --- | --- |
| Free | 0.2865 |
| Semantic | 0.3220 |
| Difference | **+0.0355** |
| 95% CI | [0.0266, 0.0447] |
| p | 0.0005 |
| Positive clusters | 12/12 |

Because the target text and the Semantic Prompt share core semantic content, this endpoint should be read as a manipulation check rather than as independent evidence of generative control.

### Visual–Prototype Similarity

Similarity between each generated image and the corresponding visual prototype, defined as the mean of the normalized CLIP image embeddings of the original architectural images belonging to that cluster. Equal-weight pooled results:

| Condition | Value |
| --- | --- |
| Free | 0.8066 |
| Semantic | 0.8404 |
| Difference | **+0.0339** |
| 95% CI | [0.0097, 0.0569] |
| p | 0.0215 |
| Positive clusters | 10/12 |

The two independent batches showed effects in the same direction and of similar magnitude, providing preliminary evidence of reproducibility.

These CLIP measures are **visual–semantic alignment proxies**. They do not imply gains in constructability, responsive performance, environmental performance, or overall design quality.

---

# 12. Same-Scale Six-Prototype Class-Specificity Analysis

Each of the 144 generated images was additionally compared with all six visual prototypes at the same observation scale. Complete similarity vectors and predicted labels are in `11_Six_Prototype_Similarity_and_Predictions.csv`; confusion-matrix counts in `12_Figure_22_Confusion_Matrix.csv`.

| Measure | Free | Semantic | Difference | 95% CI | p |
| --- | --- | --- | --- | --- | --- |
| Own-prototype similarity | 0.8066 | 0.8404 | +0.0339 | [0.0097, 0.0569] | 0.0215 |
| Own-prototype–strongest-competitor margin | −0.0425 | −0.0119 | +0.0306 | [0.0137, 0.0484] | 0.0093 |
| Top-1 prototype identification rate | 13.9% | 44.4% | +30.6 pp | — | 0.0586 |

Top-1 identification exceeded the chance level obtained by permuting labels. Semantic Prompt conditioning therefore improved prototype consistency and category discrimination in the generated outputs. However:

- the strict own-prototype–strongest-competitor margin **remained negative**, meaning that on average a competing prototype was still closer than the intended one;
- the Top-1 rate **remained below 50%**;
- the between-condition Top-1 difference was **only marginally significant (p = 0.0586)**.

The current evidence therefore supports **improved visual–semantic alignment and an improved prototype-discrimination tendency**, but does **not** demonstrate stable class-specific generative control.

The 12 visual–semantic prototypes should be interpreted as candidate semantic mediators and structured prompt resources, rather than as generative controllers with fixed class boundaries.

---

# 13. Verification and Reproducibility Scope

This repository is intended to improve the **transparency, traceability, and verifiability** of the reported analysis.

### What can be inspected

Case-level metadata; ResNet-50 baseline embeddings; the 43-dimensional interpretable visual-feature matrices; Set A and Set B K = 6 working cluster memberships; image-level CLIP scores from two independent generation batches; the 144 generated images used in the formal experiment; the complete English prompts for those images; the generation parameters that were actually recorded; image-level SHA-256 integrity identifiers; complete same-scale six-prototype CLIP similarity vectors; predicted prototype labels; own-prototype and strongest-competitor similarities; prototype margins; Top-1 correctness indicators; and the complete confusion-matrix counts.

### What cannot be reproduced from this repository alone

The repository does **not** redistribute the 150 third-party architectural source images. Independent users therefore cannot reconstruct the workflow beginning from architectural-image acquisition and preprocessing using only these materials.

The repository does **not** release the complete analysis source code. It is intended to support **inspection, traceability, and verification of the released derived data and reported outputs**, rather than end-to-end computational reproduction.

No unrecorded generation settings have been retrospectively inferred or reconstructed. Parameters not retained during the experiment are explicitly identified as **not recorded** in File 10.

### Conditionality

The reported clusters and semantic labels are conditional on the present sample composition, image sources, visual representation, feature weighting, PCA space, clustering algorithm, semantic interpretation procedure, and generative experimental configuration.

The principal transferable contribution is the analytical pathway:

**Visual Features → Cluster Structure → Semantic Mapping → Generative Feedback**

rather than direct reuse of the present K = 6 memberships or the 12 semantic labels as fixed categories for other architectural datasets.

---

# 14. Data Copyright and Usage Boundary

The original architectural images analyzed in the visual-clustering stage were obtained from publicly accessible architectural platforms, media sources, design-practice websites, and project websites. Copyright and related rights in those source images remain with the respective photographers, architectural practices, publishers, project owners, or other original rights holders.

For this reason, **the 150 original architectural source images are not redistributed through this repository.**

The repository instead releases derived research data: case metadata, ResNet-50 numerical embeddings, 43-dimensional visual features, Set A and Set B cluster memberships, image-level CLIP evaluation scores, generation prompts and recorded parameters, six-prototype similarity and prediction data, and confusion-matrix data.

The AI-generated experimental images produced specifically for the controlled generative validation are provided separately in `09_Generated_experiment_images.xlsx`, to support research transparency, visual inspection, and correspondence with the released CLIP evaluation records.

The release of derived research data does not transfer or grant rights to reuse any third-party architectural source image. This repository is therefore more accurately described as an **open derived research-data repository** rather than an **open architectural image dataset**.

Users are responsible for ensuring that any independent reuse of third-party source materials complies with applicable copyright, licensing, and attribution requirements.

---

# 15. License

The derived research data and the AI-generated experimental images in this repository are released under **CC BY 4.0** (see `LICENSE`).

This license covers **only** the derived data and the images generated by the authors. It does **not** extend to the 150 third-party architectural source images, which are not redistributed here and remain subject to the terms of their original rights holders (see Section 14).

---

# 16. Citation

If you use the released research data, derived representations, or experimental outputs in this repository, please cite the associated paper:

> Liu, R. Can Visual Clusters Support Semantic Steering? A Cross-Scale Study of Responsive-Façade Images. *Buildings* **2026**, *16*, xxxx.

Journal volume, article number, and DOI will be added upon publication.

---

# 17. Data Availability

This repository provides the derived numerical data, clustering outputs, CLIP evaluation records, generated experimental images, complete generation prompts and recorded parameters, six-prototype similarity and prediction data, and confusion-matrix data associated with the study.

The third-party architectural source images used to construct the original 150-image analytical dataset are not redistributed because of copyright restrictions.

The repository is intended to support transparent inspection and verification of the released research outputs while explicitly documenting the boundaries of full end-to-end reproducibility.

