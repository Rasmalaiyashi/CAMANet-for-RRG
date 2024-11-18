# CAMANet with Fuzzy Alignment for Radiology Report Generation
This repository implements an enhanced version of CAMANet (Class Activation Map Guided Attention Network) for radiology report generation. The architecture is tailored for better visual-textual alignment by integrating a fuzzy algorithm in place of the standard cross-attention mechanism.

# Overview
CAMANet is designed to leverage Class Activation Maps (CAMs) for guiding attention in radiology report generation. It utilizes a Visual-Textual Attention Consistency Module (VTACM) to align visual and textual features effectively. In this modified version, the cross-attention mechanism has been replaced with a fuzzy logic-based algorithm to improve the alignment between visual regions and textual descriptions.

Key Contributions

* Visual Extractor:

Processes input chest X-rays to generate patch-level features.
Uses a Feature Extractor to derive visual embeddings.

* VDMAE:

Integrates a masked autoencoder approach to learn richer visual embeddings.

* Fuzzy Logic for Alignment:

Replaces the cross-attention module for aligning visual and textual representations.
Improves interpretability and alignment accuracy by leveraging fuzzy sets and membership functions.

* Decoder:

Generates human-readable radiology reports based on aligned embeddings.

* Features
Visual-Textual Alignment: Enhances the alignment using fuzzy logic principles.
Report Generation: Outputs detailed radiology reports based on input chest X-ray images.
Robust Supervision: Employs MSE and BCE loss to ensure reliable training.

* Architecture
The modified CAMANet architecture incorporates a Fuzzy Logic-based Alignment Module (FLAM) in the Visual-Textual Attention Consistency Module (VTACM). The fuzzy algorithm replaces matrix multiplication-based cross-attention scoring with membership-based alignment, ensuring smoother alignment of features.

# What is Fuzzy Alignment Module (FLAM)?

* Motivation
The Fuzzy Alignment Module (FLAM) is designed to enhance the alignment of visual features extracted from medical images (e.g., chest X-rays) with the corresponding textual features generated during report creation. Traditional cross-attention mechanisms rely on matrix multiplication to compute alignment scores between visual and textual embeddings. However, these methods may lack interpretability and fail to capture nuanced relationships in complex medical data.

Fuzzy alignment introduces a fuzzy logic-based approach that leverages the principles of fuzzy sets and membership functions to compute alignment scores. This ensures smoother and more interpretable alignment, crucial for generating accurate and meaningful radiology reports.

* Overview of Fuzzy Logic
Fuzzy logic extends classical binary logic by allowing partial truth values between 0 and 1. It works on the concept of membership functions, which define the degree of belonging of an element to a fuzzy set. This property is particularly useful in handling uncertain or imprecise data, such as the relationship between image patches and report words.

* Implementation in CAMANet
Inputs:

Visual Features (
𝑣
𝑠
v 
s
 ): Patch-level features extracted from the chest X-ray image by the visual extractor.
Textual Features (
𝑡
t): Word embeddings from the textual report decoder.
Cross Scores (
𝐴
A): Preliminary attention scores indicating correlations between visual and textual embeddings.
Fuzzification:

Convert raw attention scores (
𝐴
A) into fuzzy sets using membership functions. For instance:
𝜇
𝑙
𝑜
𝑤
(
𝑥
)
=
{
1
𝑥
≤
𝑎
𝑏
−
𝑥
𝑏
−
𝑎
𝑎
<
𝑥
<
𝑏
0
𝑥
≥
𝑏
μ 
low
​
 (x)= 
⎩
⎨
⎧
​
  
1
b−a
b−x
​
 
0
​
  
x≤a
a<x<b
x≥b
​
 
𝜇
ℎ
𝑖
𝑔
ℎ
(
𝑥
)
=
1
−
𝜇
𝑙
𝑜
𝑤
(
𝑥
)
μ 
high
​
 (x)=1−μ 
low
​
 (x)
Each visual-textual pair is assigned membership values in categories such as low alignment, medium alignment, and high alignment.

* Fuzzy Rules:

Define rules to model the alignment process. For example:
If visual feature has high intensity and textual feature has high relevance, then alignment is strong.
If visual feature has medium intensity and textual feature is moderately relevant, then alignment is moderate.
These rules are based on domain knowledge, such as common patterns in medical imaging and report descriptions.
Inference:

Combine fuzzy rules to compute alignment scores using an aggregation method like the max-min composition.
Output a fuzzy alignment matrix that indicates the strength of association between visual and textual elements.
Defuzzification:

Convert the fuzzy alignment matrix into crisp alignment scores using defuzzification techniques, such as:
𝐴
𝑓
𝑖
𝑛
𝑎
𝑙
=
∑
(
𝜇
𝑖
⋅
𝑥
𝑖
)
∑
𝜇
𝑖
A 
final
​
 = 
∑μ 
i
​
 
∑(μ 
i
​
 ⋅x 
i
​
 )
​
 
These scores replace the cross-attention scores in the Visual-Textual Attention Consistency Module.
Advantages of Fuzzy Alignment
Interpretability:

The alignment process is explainable, as each step (membership, rules, and defuzzification) is based on logical principles.
Robustness:

Handles noisy and uncertain relationships between visual and textual data more effectively than traditional cross-attention mechanisms.
Domain Adaptation:

Easily adaptable to new datasets by modifying fuzzy rules based on specific medical contexts.
Workflow in CAMANet
The Visual Extractor generates patch features (
𝑣
𝑠
v 
s
 ).
The Decoder generates textual embeddings (
𝑡
t).
FLAM computes the alignment between 
𝑣
𝑠
v 
s
  and 
𝑡
t using fuzzy logic principles, producing an enhanced alignment matrix (
𝐴
𝑓
𝑢
𝑧
𝑧
𝑦
A 
fuzzy
​
 ).
The alignment matrix guides the decoder in generating more accurate and relevant radiology reports.

# Acknowledgments
CAMANet Paper: Class Activation Map Guided Attention Network for Radiology Report Generation.
Dataset contributions from MIMIC-CXR and IU-Xray.

# Future Work
Explore additional fuzzy rules for further enhancement.
Test on other medical imaging datasets.
