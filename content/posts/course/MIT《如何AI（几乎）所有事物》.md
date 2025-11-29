---
title: "MIT《如何AI（几乎）所有事物》"
date: 2025-11-29T18:34:25+08:00
lastmod: 2025-11-29T21:54:22+08:00
math: true
categories:
- 在线课程
tags:
- MIT
- AI
# description->需要自己编写的文章描述，是搜索引擎呈现在搜索结果链接下方的网页简介，建议设置
description: ""
weight: # 输入1可以顶置文章，用来给文章展示排序，不填就默认按时间排序
slug: ""
draft: false # 是否为草稿
comments: true
showToc: true # 显示目录
TocOpen: true # 自动展开目录
hidemeta: false # 是否隐藏文章的元信息，如发布日期、作者等
disableShare: true # 底部不显示分享栏
---

# MIT _How to AI(Almost) Everything_


## 前言

本门课程主要讲的是多模态大模型，而不是AI应用方式。

[课程资料链接](https://mit-mi.github.io/how2ai-course/spring2025/schedule/)


## Course Description

Artificial Intelligence (AI) holds great promise as a technology to enhance digital productivity, physical interactions, overall well-being, and the human experience. To enable the true impact of AI, these systems will need to be grounded in real-world data modalities, from language-only systems to vision, audio, sensors, medical data, music, art, smell, and taste. This course will introduce the basic principles of AI (focusing on modern deep learning and foundation models) and how we can apply AI to novel real-world data modalities. In addition, we will introduce the principles of multimodal AI that can process many modalities at once, such as connecting language and multimedia, music and art, sensing and actuation, and more.

Through lectures, readings, discussions, and a significant research component, this course will develop critical thinking skills and intuitions when applying AI to new data modalities, knowledge of recent technical achievements in AI, and a deeper understanding of the AI research process.

## Course Info

##### Instructor

- [Prof. Paul Liang](https://ocw.mit.edu/search/?q=Prof.+Paul+Liang)

##### Departments

- [Media Arts and Sciences](https://ocw.mit.edu/search/?d=Media+Arts+and+Sciences)

# Content

## Introduction

Multisensory intelligence: Creating human-AI symbiosis across scales and sensory mediums to enhance productivity, creativity, and wellbeing.

![](https://setsailtowardstianhan.ip-ddns.com/blog/6efcb9a36aa9717f5385c1ae0f9d7441.png)

### Course Overview

1. AI for new modalities: data, modeling, evaluation, deployment
2. Multimodal AI: connecting multiple different data sources

### Learning Objectives 

1. Study recent technical achievements in AI research 
2. Improve critical and creative thinking skills 
3. Understand future research challenges in AI 
4. Explore and implement new research ideas in AI

### Preferred Pre-requisites

1. Some knowledge of programming (ideally in Python) 
2. Some basic understanding of modern AI capabilities & limitations 
3. Bring external (non-AI) domain knowledge about your problem 
4. Bonus: worked on AI for some modality

### Research Projects on New Modalities

Motivation: Many tasks of real-world impact go beyond image and text.

Challenges:
- AI with non-deep-learning effective modalities (e.g., tabular, time-series)
- Multimodal deep learning + time-series analysis + tabular models
- AI for physiological sensing, IoT sensing in cities, climate and environment sensing
- Smell, taste, art, music, tangible and embodied systems

Potential models and dataset to start with
- Brain EEG Signal: https://arxiv.org/abs/2306.16934
- Speech: https://arxiv.org/pdf/2310.02050.pdf
- Facial Motion: https://arxiv.org/abs/2308.10897
- Tactile: https://arxiv.org/pdf/2204.00117.pdf

### Research Projects on AI Reasoning

Motivation: Robust, reliable, interpretable reasoning in (multimodal) LLMs.

Challenges:
- Fine-grained and compositional reasoning
- Neuro-symbolic reasoning
- Emergent reasoning in foundation models

Potential models and dataset to start with
- Can LLMs actually reason and plan?
- Code for VQA: CodeVQA: https://arxiv.org/pdf/2306.05392.pdf, VisProg:
https://prior.allenai.org/projects/visprog, Viper: https://viper.cs.columbia.edu/
- Cola: https://openreview.net/pdf?id=kdHpWogtX6Y
- NLVR2: https://arxiv.org/abs/1811.00491
- Reference games: https://mcgill-nlp.github.io/imagecode/, https://github.com/AlabNII/onecommon, https://dmg-photobook.github.io/

### Research Projects on Interactive Agents

Motivation: Grounding AI models in the web, computer, or other virtual worlds to help humans with digital tasks.

Challenges:
- Web visual understanding is quite different from natural image understanding
- Instructions and language grounded in web images, tools, APIs
- Asking for human clarification, human-in-the-loop
- Search over environment and planning

Potential models and dataset to start with
- WebArena: https://arxiv.org/pdf/2307.13854.pdf
- AgentBench: https://arxiv.org/pdf/2308.03688.pdf
- ToolFormer: https://arxiv.org/abs/2302.04761
- SeeAct: https://osu-nlp-group.github.io/SeeAct/

### Research Projects on Embodied and Tangible AI

Motivation: Building tangible and embodied AI systems that help humans in physical tasks.

Challenges:
- Perception, reasoning, and interaction
- Connecting sensing and actuation
- Efficient models that can run on hardware
- Understanding influence of actions on the world (world model)

Potential models and dataset to start with
- Virtual Home: http://virtual-home.org/paper/virtualhome.pdf
- Habitat 3.0 https://ai.meta.com/static-resource/habitat3
- RoboThor: https://ai2thor.allenai.org/robothor
- LangSuite-E: https://github.com/bigai-nlco/langsuite
- Language models and world models: https://arxiv.org/pdf/2305.10626.pdf

### Research Projects on Socially Intelligent AI

Motivation: Building AI that can understand and interact with humans in social situations.

Challenges:
- Social interaction, reasoning, and commonsense.
- Building social relationships over months and years.
- Theory-of-Mind and multi-party social interactions.

Potential models and dataset to start with
- Multimodal WereWolf: https://persuasion-deductiongame.socialai-data.org/
- Ego4D: https://arxiv.org/abs/2110.07058
- MMToM-QA: https://openreview.net/pdf?id=jbLM1yvxaL
- 11866 Artificial Social Intelligence: https://cmu-multicomp-lab.github.io/asi-course/spring2023/

### Research Projects on Human-AI Interaction

Motivation: What is the right medium for human-AI interaction? How can we really trust AI? How do we enable collaboration and synergy?

Challenges:
- Modeling and conveying model uncertainty – text input uncertainty, visual uncertainty,
multimodal uncertainty? cross-modal interaction uncertainty?
- Asking for human clarification, human-in-the-loop, types of human feedback and ways to learn from human feedback through all modalities.
- New mediums to interact with AI. New tasks beyond imitating humans, leading to collaboration.

Potential models and dataset to start with
- MMHal-Bench: https://arxiv.org/pdf/2309.14525.pdf aligning multimodal LLMs
- HACL: https://arxiv.org/pdf/2312.06968.pdf hallucination + LLM

### Research Projects on Ethics and Safety

Motivation: Large AI models are can emit unsafe text content, generate or retrieve biased images.

Challenges:
- Taxonomizing types of biases: text, vision, audio, generation, etc.
- Tracing biases to pretraining data, seeing how bias can be amplified during training, fine-tuning.
- New ways of mitigating biases and aligning to human preferences.

Potential models and dataset to start with
- Many works on fairness in LLMs -> how to extend to multimodal?
- Mitigating bias in text generation, image-captioning, image generation

### Introduction to AI and AI research 

- Introduction to AI and AI research  
- Generating ideas, reading and writing papers, AI experimentation

![](https://setsailtowardstianhan.ip-ddns.com/blog/83653b7e2311d55d157814aea71a24bc.png)

How Do We Get Research Ideas?

Turn a concrete understanding of existing research's failings to a higher-level experimental question.
• Bottom-up discovery of research ideas
• Great tool for incremental progress, but may preclude larger leaps

Move from a higher-level question to a lower-level concrete testing of that question.

• Top-down design of research ideas
• Favors bigger ideas, but can be disconnected from reality

Beware "Does X Make Y Better?" "Yes"

The above question/hypothesis is natural, but indirect

- If the answer is "no" after your experiments, how do you tell what's going wrong?

Usually you have an intuition about why X will make Y better (not just random)

Can you think of other research questions/ hypotheses that confirm/falsify these assumptions

How to do Literature Review and Read a Paper?

1. Google scholar
2. Papers with code, Github, Huggingface
3. Recent conference proceedings
4. Blog posts
5. Survey papers, tutorials, courses

Testing Research Ideas

1. Gather and process dataset, visualize data, gather labels, do data splits.
2. Implement the most simple pipeline and get it working. -> Pipeline = data loading + basic model + eval function + loss/visualization/deployment
3. Change one component of the model at a time, repeat x10 (top-down or bottom-up).
4. Find what works best, and exploit.
5. Scale up experiments, repeat across multiple datasets.
6. Careful ablation studies.
7. Qualitative comparisons and visualizations.
8. Repeat until successful.

How to Write a Paper

1. Prepare a 15min talk (with figures, examples, tables, etc.)
2. Convert the talk into a paper.

More resources

- https://github.com/pliang279/awesome-phd-advice
- https://github.com/jbhuang0604/awesome-tips
- https://www.cs197.seas.harvard.edu/
- https://medium.com/spotprobe/the-hexagon-of-ideas-02e5b770d75e

## Module 1: Foundations of AI 
### Data, structure, and information

Lecture Outline:

1. Vision, language, audio, sensing, set, graph modalities
2. Modality profile
3. Types of data and labels
4. Common learning objectives and generalization

Most of AI is about learning abstractions, or representations, from data.

Modality Profile:

1. Element representations: Discrete, continuous, granularity
2. Element distributions: Density, frequency
3. Structure: Temporal, spatial, latent, explicit
4. Information: Abstraction, entropy
5. Noise: Uncertainty, noise, missing data
6. Relevance: Task, context dependence

![](https://setsailtowardstianhan.ip-ddns.com/blog/c7fd5d109e0541537796199d9b51db7b.png)

Summary: How To Data

1. Decide how much data to collect, and how much to label (costs and time)
2. Clean data: normalize/standardize, find noisy data, anomaly/outlier detection
3. Visualize data: plot, dimensionality reduction (PCA, t-sne), cluster analysis
4. Decide on evaluation metric (proxy + real, quantitative and qualitative)
5. Choose model class and learning algorithm (more next lecture)

#### Huggingface Tutorial

- “Huggingface” is a set of multiple packages
	- transformers: Provides API to initialize large pretrained models
	- datasets: Provides easy way to download datasets
- Not from Huggingface but often used together
	- bitsandbytes: Provides functions to quantize large models
	- flash-attn: Allows the model to run faster with less memory
- Some terms to keep in mind
	- LoRA: Adapter to train large models with less memory
	- Bfloat16: Robust half precision representation often used to save memory


#### The Recipe

- Become one with the Data
- Set up end-to-end skeleton and get dumb baselines
- Overfit to diagnose errors
- Regularize for better generalization
	● Add more real data – the best way to reduce overfitting  
	● Use data augmentation and pretraining  
	● Reduce input dimensions and model size  
	● Techniques: Dropout, weight decay, early stopping  
- Tune hyperparameters
	● Prefer random search over grid search  
	● Use Bayesian optimization tools when available   
	● Don’t overcomplicate – start with simple models  
- Squeeze out final improvements

#### How to Design ML Models for New Data

- Look at the data first
- For simple, low dimensional data, start with simple models (SVM, Random Forest, Shallow MLP/CNN)
- For vision/language data, try pretrained model
- Start simple, then add complexity. Simple ones can be used as baselines.

#### How to Debug Your Model
- Look at the data first. Is the input data & label correct?
	- Ensure no data leakage;
- Look at the outputs. Is model only predicting one label?
	- Label imbalance: Data Augmentation; loss scaling
- Look at the training loss
	- Loss is nan: Inspect weights and inputs for NaN values. Make sure weights are initialized. LLM: Use bfloat16 instead of float16.
	- Loss not changing: Model underfitting. Increase learning rate; decrease weight decay; Add more complexity; Use better optimizer*.
- Look at Loss (Continued)
	- Loss highly varied/increasing: Decrease learning rate; Gradient Clipping; Use better Optimizers
- Look at train vs val accuracy (or any other metrics)
	- Train >> Val: Model overfitting. More weight decay, reduce model complexity, data augmentation, get more data
	- Train ≈ Val ≈ 100%: Check for data leakage

Personal tip: I recommend trying second order optimizers from packages like Heavyball

### Common model architectures

Lecture Outline

1.  A unifying paradigm of model architectures
2. Temporal sequence models
3. Spatial convolution models
4. Models for sets and graphs

Summary: How To Model

1. Decide how much data to collect, and how much to label (costs and time)
2. Clean data: normalize/standardize, find noisy data, anomaly/outlier detection
3. Visualize data: plot, dimensionality reduction (PCA, t-sne), cluster analysis
4. Decide on evaluation metric (proxy + real, quantitative and qualitative)
5. Choose modeling paradigm - domain-specific vs general-purpose
6. Figure out base elements and their representation
7. Figure out data invariances & equivariances (+other parts of modality profile)
8. Iterate between data collection, model design, model training, hyperparameter tuning etc. until satisfied.
### **Discussion 1: Learning and generalization**

- [Learning the Bitter Lesson](https://arxiv.org/pdf/2410.09649)  
- [Unifying Grokking and Double Descent](https://arxiv.org/pdf/2303.06173)  
- [Generalization in Neural Networks](https://arxiv.org/pdf/2209.01610)  
- [Textbooks are all you Need](https://arxiv.org/pdf/2306.11644)  
- [A Conceptual Pipeline for Machine Learning](https://arxiv.org/pdf/2207.07528)

## Module 2: Foundations of multimodal AI 

### Multimodal connections and alignment

![](https://setsailtowardstianhan.ip-ddns.com/blog/5b5cd7675f62426f70dfe7985f9155ff.png)

![](https://setsailtowardstianhan.ip-ddns.com/blog/ac168ca938d2cdf2ea8590f72482cb39.png)

Modality refers to the way in which something expressed or perceived.

A research-oriented definition… Multimodal is the science of heterogeneous and interconnected(Connected + Interacting) data.

Heterogeneous Modalities: Information in different modalities shows diverse qualities, structures, & representations.

![](https://setsailtowardstianhan.ip-ddns.com/blog/5b27d830a96c3a294f9b2e139e53f893.png)

Challenge 1: Representation 

Definition: Learning representations that reflect cross-modal interactions between individual elements, across different modalities This is a core building block for most multimodal modeling problems!

Challenge 2: Alignment 

Definition: Identifying and modeling cross-modal connections between all elements of multiple modalities, building from the data structure.

Sub-challenges: 
- Discrete connections: Explicit alignment (e.g., grounding) 
- Contextualized representation: Implicit alignment + representation
- Continuous alignment: Granularity of individual elements 

Challenge 2a: Discrete Alignment 

Definition: Identify and model connections between elements of multiple modalities

![](https://setsailtowardstianhan.ip-ddns.com/blog/207230008dd6a8c59c35717e86cea6bd.png)

Challenge 2b: Continuous Alignment 

Definition: Model alignment between modalities with continuous signals and no explicit elements

Challenge 3: Reasoning 

Definition: Combining knowledge, usually through multiple inferential steps, exploiting multimodal alignment and problem structure.

Challenge 4: Generation 

Definition: Learning a generative process to produce raw modalities that reflects cross-m

Challenge 5: Transference 

Definition: Transfer knowledge between modalities, usually to help the target modality which may be noisy or with limited resources.

Challenge 6: Quantification 

Definition: Empirical and theoretical study to better understand heterogeneity, cross-modal interactions, and the multimodal learning process.

### **Discussion 2: Modern AI architectures**

- [Scaling Laws for Generative Mixed-Modal Models](https://arxiv.org/abs/2301.03728)  
- [Not All Tokens Are What You Need for Pretraining](https://arxiv.org/abs/2404.07965)  
- [PaLI: A Jointly-Scaled Multilingual Language-Image Model](https://arxiv.org/abs/2209.06794)  
- [The Evolution of Multimodal Model Architectures](https://arxiv.org/abs/2405.17927)  
- [An Image is Worth 16x16 Words: Transformers for Image Recognition at Scale](https://arxiv.org/abs/2010.11929)  
- [A ConvNet for the 2020s](https://arxiv.org/abs/2201.03545)  
- [Inductive Representation Learning on Large Graphs](https://arxiv.org/abs/1706.02216)  
- [Janossy Pooling: Learning Deep Permutation-Invariant Functions for Variable-Size Inputs](https://arxiv.org/abs/1811.01900)
### Multimodal interactions and fusion

Visual-and-Language Transformer (ViLT) (≈ BERT + ViT)

ALBEF: Align Before Fusion 32 (≈ BERT + ViT + CLIP-ish)

![](https://setsailtowardstianhan.ip-ddns.com/blog/6e48bfc64f296152fa3f7439320bf0be.png)

### **Discussion 3: Multimodal alignment**

- [The Platonic Representation Hypothesis](https://arxiv.org/pdf/2405.07987)  
- [What Makes for Good Views for Contrastive Learning?](https://arxiv.org/abs/2005.10243)  
- [Understanding the Emergence of Multimodal Representation Alignment](https://arxiv.org/pdf/2502.16282)  
- [Does equivariance matter at scale?](https://arxiv.org/abs/2410.23179)  
- [Learning Transferable Visual Models From Natural Language Supervision?](https://arxiv.org/pdf/2103.00020)  
- [Emerging Properties in Self-Supervised Vision Transformers](https://arxiv.org/pdf/2104.14294)  
- [Foundations & trends in multimodal machine learning - Principles, challenges, and open questions](https://arxiv.org/abs/2209.03430)
### Cross-modal transfer

Transference

Definition: Transfer knowledge between modalities, usually to help the primary modality which may be noisy or with limited resources

Part 1: Transfer via Pretrained Models

Definition: Transferring knowledge from large-scale pretrained models to downstream tasks involving

Part 2: Co-learning

Definition: Transferring information from secondary to primary modality by sharing representation spaces between both modalities.

Co-learning via Alignment

Definition: Transferring information from secondary to primary modality by sharing representation spaces between modalities

Representation alignment: word embedding space for zero-shot visual classification

Co-learning via Translation

Definition: Transferring information from secondary to primary modality by using the secondary modality as a generation target.

Part 3: Model Induction

Model Induction 𝑦1 𝑦2 Definition: Keeping individual unimodal models separate but inducing common behavior across separate models.

![](https://setsailtowardstianhan.ip-ddns.com/blog/a93c027b0a8f19412a197d2f0249652c.png)

### **Discussion 4: Multimodal interactions**

- [Multimodal interaction: A review](https://www.sciencedirect.com/science/article/pii/S0167865513002584)  
- [Quantifying & Modeling Multimodal Interactions: An Information Decomposition Framework](https://arxiv.org/abs/2302.12247)  
- [Does my multimodal model learn cross-modal interactions? It’s harder to tell than you might think!](https://aclanthology.org/2020.emnlp-main.62/)  
- [Kosmos-2: Grounding Multimodal Large Language Models to the World](https://arxiv.org/abs/2306.14824)  
- [Chameleon: Mixed-modal early-fusion foundation models](https://arxiv.org/abs/2405.09818)  
- [MM1: Methods, Analysis and Insights from Multimodal LLM Pre-training](https://link.springer.com/chapter/10.1007/978-3-031-73397-0_18)  
- [MoMa: Efficient Early-Fusion Pre-training with Mixture of Modality-Aware Experts](https://arxiv.org/pdf/2407.21770)
## Module 3: Large models and modern AI 

### Pre-training, scaling, fine-tuning LLMs

Today’s Agenda
- History of LLMs, RNNs vs Transformer 
- Pretraining of LLMs
- Types of Architecture 
- Instruction Finetuning & Preference Tuning 
- Efficient Training 
- Practical Tips

![](https://setsailtowardstianhan.ip-ddns.com/blog/125d02839e5bf7ef07a5d4f36b2b0ac5.png)

Scaling Laws:
- Bigger model allows models to reach a better performance given sufficient compute 
- Over training models getting popular nowadays

Limitations of RL + Reward Modeling

- Human preferences are unreliable 
	- Chatbots are rewarded to produce responses that seem authoritative and helpful, regardless of truth 
	- This can result in making up facts + hallucinations
- Reward Model doesn’t always reflect humans’ preferences & may have unintended behaviors

Efficient Training: LoRA / Efficient low rank adaptation

- Training the whole model takes a lot of compute and GPU memory 
- Solution: Freeze the model, train a small adapter that updates with a low-rank decomposition

Efficient Training: Mixture of Experts

- Train multiple parallel networks (experts) simultaneously
- During each forward pass, only activate k experts 
- Saves compute & GPU memory 
- Deepseek R1: 671B, only 37B activated, performance on par with OpenAI o1-mini

Efficient Inference: Quantization

- Range Clipping 
- Scale & Shift 
- Convert to lower bits 
- Calibration

Practical Tips: How to Instruction Finetune an LLM

1. Data Preparation: Convert your data to conversation format
2. Choosing a good starting point
3. Secure compute & Finetune the model
4. Evaluation & Deployment

### Large multimodal models

Today’s lecture

1. Multimodal foundation models and pre-training
2. Adapting LLMs into multimodal LLMs
3. From text to multimodal generation
4. Latest directions: natively multimodal, multimodal MoE, real-world modalities

Part 1: Multimodal foundation model representations of text, video, audio

Part 2: Adapting large language models for multimodal text generation

Part 3: Enabling text and image generation

Visual-and-Language Transformer (ViLT)

Pre-training datasets
- Largest dataset is DataComp. It has 12.8 billion image-text pairs.
- Recent efforts shifted more towards filtering for high quality multimodal data.

Examples include DFN (2B), COYO (600M), and Obelics (141M)

Native Multimodal Models

- Background
	- Non-native VLMs: Image encoder paired with frozen trained LLM. The image encoder can either be frozen or trained. Most VLMs now use this structure.
	- Native Multimodal Modals: LLMs Trained from scratch with multimodal input
		- Late fusion: Image patches -> Image Encoder -> Linear -> LLM.
		- Early fusion: Image patches -> Linear -> LLM (No image encoder!)

Scaling Laws for Native Multimodal Models

- Early fusion models hold small advantage on small scales.
- On larger scales, both architectures perform similarly. (We don’t actually need image encoders!)
- NMMs scale similarly to unimodal LLMs, with slightly varying scaling exponents depending on the target data type and training mixture
- Sparse structure like MOE significantly benefits NMMs at the same inference cost 
- In an MOE structure, Modality-aware design (having separate image/text experts) performs worse than modality-agnostic design (unified experts for both image/text tokens)

### **Discussion 5: Large language models**

- [LoRA: Low-Rank Adaptation of Large Language Models](https://arxiv.org/abs/2106.09685)  
- [Gated Linear Attention Transformers with Hardware-Efficient Training](https://arxiv.org/abs/2312.06635)  
- [Unintended Impacts of LLM Alignment on Global Representation](https://arxiv.org/abs/2402.15018)  
- [A Visual Guide to Quantization](https://newsletter.maartengrootendorst.com/p/a-visual-guide-to-quantization)  
- [Scaling Instruction-Finetuned Language Models](https://arxiv.org/abs/2106.09685)

### Modern generative AI

Todays Lecture

1. What are Generative Models?
2. Current State of the Art (Flow Matching)
3. Conditional Generation
4. Architectures
5. Tips to Train these Models

 ### **Discussion 6: Large multimodal models**

- [LLaMA-Adapter: Efficient Fine-tuning of Language Models with Zero-init Attention](https://arxiv.org/pdf/2303.16199)  
- [Cobra: Extending Mamba to Multi-Modal Large Language Model for Efficient Inference](https://arxiv.org/pdf/2403.14520)
- [ModaVerse: Efficiently Transforming Modalities with LLMs](https://arxiv.org/abs/2401.06395)  
- [Spider: Any-to-Many Multimodal LLM](https://arxiv.org/pdf/2411.09439)  
- [SPHINX-X: Scaling Data and Parameters for a Family of Multi-modal Large Language Models](https://arxiv.org/pdf/2402.05935)  
- [How Far Are We to GPT-4V? Closing the Gap to Commercial Multimodal Models with Open-Source Suites](https://arxiv.org/pdf/2404.16821)  
- [NExT-GPT: Any-to-Any Multimodal LLM](https://arxiv.org/pdf/2309.05519)  
- [Learning to rebalance multi-modal optimization by adaptively masking subnetworks](https://arxiv.org/pdf/2404.08347)

## Module 4: Interactive AI

### **Discussion 7: Generative AI**

- [Large Language Diffusion Models](https://arxiv.org/pdf/2502.09992)  
- [Compositional Generative Modeling: A Single Model is Not All You Need](https://arxiv.org/pdf/2402.01103)  
- [Flow Matching for Generative Modeling](https://arxiv.org/abs/2210.02747)  
- [Flow Matching Guide and Code](https://arxiv.org/abs/2412.06264)  
- [FlowMotion: Target-Predictive Conditional Flow Matching for Jitter-Reduced Text-to-Motion Generation](https://arxiv.org/abs/2504.01338)  
- [MusFlow: Multimodal Music Generation via Conditional Flow Matching](https://arxiv.org/abs/2504.13535)  
- [Unraveling the Connections Between Flow Matching and Diffusion Probabilistic Models](https://arxiv.org/abs/2311.07625)
- [Exploring Diffusion and Flow Matching Under Generator Matching](https://arxiv.org/abs/2412.11024)

### Multi-step reasoning

Today’s lecture
1. Multimodal reasoning: Solving hard problems by breaking them down into step-by-step reasoning steps in multiple modalities
2. AI agents
3. Human-AI interaction
4. Ethics and safety

Models: Multimodal fusion and generation  
Data: Hard challenges + human reasoning steps  
Training: Reinforcement learning for emergent reasoning  
Human: Trustworthy, safe, controllable  

Multimodal Reasoning 

Part 1: Multimodal foundation model representations of text, video, audio

Part 2: Adapting large language models for multimodal text generation

Part 3: Enabling text and image generation

Part 4: Human-AI interaction

### Interactive and embodied AI

Today’s lecture
1.  Basics of reinforcement learning
2.  Modern RL for LLM alignment and reasoning
3.  Interactive LLM agents

![](https://setsailtowardstianhan.ip-ddns.com/blog/c7e007c0be2df306bfa71746afbfdd2b.png)

Tips and Training for Reinforcement Learning
1. Sanity Check with Fixed Policy
2. Monitor KL Divergence (in PPO-like algorithms)
3. Plot Entropy Over Time
4. Use Greedy Rollouts for Evaluation
5. Debug Value Function Separately: Visualize predicted vs. actual return
6. Gradient Norm Clipping is Crucial
7. Check Advantage Distribution
8. Train on a Frozen Replay Buffer
9. Use Curriculum Learning: Gradually increase task difficulty or reward sparsity
10. Watch for Mode Collapse in MoE or Multi-Head Policies

### Human-AI interaction and safety

Interactive Agents

Multisensory agents for the web and digital automation

Example task: Purchase a set of earphones with at least 4.5 stars in rating and ship it to me.

![](https://setsailtowardstianhan.ip-ddns.com/blog/964f2f63b3842e0b7084a8a55bea5e84.png)

Embodied Agents 

Generate precise robotics control directly via trained vision language models.

Human-AI interaction

1. What medium(s) is most intuitive for human-AI interaction?
	- especially beyond language prompting 1
2. What new technical challenges in AI have to be solved for human-AI interaction?
	- quantification
3. What new opportunities arise when integrating AI with the human experience?
	- productivity, creativity, wellbeing

Quantification

Definition: Empirical and theoretical studies to better understand model
shortcomings and predict and control model behavior.

Quantification - Safety 

Easy to generate biased and dangerous content with language models!

But there exist ways to ‘jailbreak’ the safety measures in aligned LLMs

![](https://setsailtowardstianhan.ip-ddns.com/blog/86da7377b1b2cb82abeb80edaa652400.png)




## Readings

- [Foundations and Trends in Multimodal Machine Learning: Principles, Challenges, and Open Questions](https://arxiv.org/abs/2209.03430)  
    
- [Multimodal Machine Learning: A Survey and Taxonomy](https://arxiv.org/abs/1705.09406)  
    
- [Representation Learning: A Review and New Perspectives](https://arxiv.org/abs/1206.5538)

- [Machine learning: Trends, Perspectives, and Prospects](https://www.science.org/doi/abs/10.1126/science.aaa8415)  
    
- [Representation Learning: A Review and New Perspectives](https://arxiv.org/abs/1206.5538)  
    
- [Foundations and Trends in Multimodal Machine Learning: Principles, Challenges, and Open Questions](https://arxiv.org/abs/2209.03430)  
    
- [Geometric Deep Learning: Grids, Groups, Graphs, Geodesics, and Gauges](https://arxiv.org/abs/2104.13478)

- [A Recipe for Training Neural Networks](https://karpathy.github.io/2019/04/25/recipe/)  
    
- [Fine-tuning a Code LLM on Custom Code on a single GPU](https://colab.research.google.com/drive/1EDsjYRrAiujUew0GRJ_hyVoNMsSDnlnx?usp=sharing)  
    
- [MAS.S60 Pytorch Introduction](https://colab.research.google.com/drive/1SoTu6gvYcLNDqPwNPTWmsSYF-l-UfHPx?usp=sharing)

- [Geometric Deep Learning: Grids, Groups, Graphs, Geodesics, and Gauges](https://arxiv.org/abs/2104.13478)  
    
- [An Image is Worth 16x16 Words: Transformers for Image Recognition at Scale](https://arxiv.org/abs/2010.11929)  
    
- [Attention Is All You Need](https://arxiv.org/abs/1706.03762)  
    
- [Neural Machine Translation by Jointly Learning to Align and Translate](https://arxiv.org/abs/1409.0473)  
    
- [Deep Sets](https://arxiv.org/abs/1703.06114)  
    
- [Graph Attention Networks](https://arxiv.org/abs/1710.10903)

- [Learning the Bitter Lesson](https://arxiv.org/pdf/2410.09649)  
    
- [Unifying Grokking and Double Descent](https://arxiv.org/pdf/2303.06173)  
    
- [Generalization in Neural Networks](https://arxiv.org/pdf/2209.01610)  
    
- [Textbooks are all you Need](https://arxiv.org/pdf/2306.11644)  
    
- [A Conceptual Pipeline for Machine Learning](https://arxiv.org/pdf/2207.07528)

- [Foundations and Trends in Multimodal Machine Learning: Principles, Challenges, and Open Questions](https://arxiv.org/abs/2209.03430)  
    
- [What Makes for Good Views for Contrastive Learning?](https://arxiv.org/abs/2005.10243)  
    
- [Characterization and classification of semantic image-text relations](https://link.springer.com/article/10.1007/s13735-019-00187-6)  
    
- [When and why vision-language models behave like bags-of-words, and what to do about it?](https://arxiv.org/abs/2210.01936)

- [Scaling Laws for Generative Mixed-Modal Models](https://arxiv.org/abs/2301.03728)  
    
- [Not All Tokens Are What You Need for Pretraining](https://arxiv.org/abs/2404.07965)  
    
- [PaLI: A Jointly-Scaled Multilingual Language-Image Model](https://arxiv.org/abs/2209.06794)  
    
- [The Evolution of Multimodal Model Architectures](https://arxiv.org/abs/2405.17927)  
    
- [An Image is Worth 16x16 Words: Transformers for Image Recognition at Scale](https://arxiv.org/abs/2010.11929)  
    
- [A ConvNet for the 2020s](https://arxiv.org/abs/2201.03545)  
    
- [Inductive Representation Learning on Large Graphs](https://arxiv.org/abs/1706.02216)  
    
- [Janossy Pooling: Learning Deep Permutation-Invariant Functions for Variable-Size Inputs](https://arxiv.org/abs/1811.01900)

- [Ten Myths of Multimodal Interaction](https://dl.acm.org/doi/pdf/10.1145/319382.319398)  
    
- [Multimodal interaction: A review](https://www.sciencedirect.com/science/article/pii/S0167865513002584)  
    
- [Quantifying & Modeling Multimodal Interactions: An Information Decomposition Framework](https://arxiv.org/abs/2302.12247)  
    
- [Does my multimodal model learn cross-modal interactions? It’s harder to tell than you might think!](https://aclanthology.org/2020.emnlp-main.62/)

- [The Platonic Representation Hypothesis](https://arxiv.org/pdf/2405.07987)  
    
- [What Makes for Good Views for Contrastive Learning?](https://arxiv.org/abs/2005.10243)  
    
- [Understanding the Emergence of Multimodal Representation Alignment](https://arxiv.org/pdf/2502.16282)  
    
- [Does equivariance matter at scale?](https://arxiv.org/abs/2410.23179)  
    
- [Learning Transferable Visual Models From Natural Language Supervision?](https://arxiv.org/pdf/2103.00020)  
    
- [Emerging Properties in Self-Supervised Vision Transformers](https://arxiv.org/pdf/2104.14294)  
    
- [Foundations & trends in multimodal machine learning - Principles, challenges, and open questions](https://arxiv.org/abs/2209.03430)


- [LLaVA-Med: Training a Large Language-and-Vision Assistant for Biomedicine in One Day](https://arxiv.org/abs/2303.00915v3)  
    
- [DreamLLM: Synergistic Multimodal Comprehension and Creation](https://arxiv.org/abs/2309.11499)  
    
- [PaLM-E: An Embodied Multimodal Language Model](https://arxiv.org/abs/2303.03378)

- [Multimodal interaction: A review](https://www.sciencedirect.com/science/article/pii/S0167865513002584)  
    
- [Quantifying & Modeling Multimodal Interactions: An Information Decomposition Framework](https://arxiv.org/abs/2302.12247)  
    
- [Does my multimodal model learn cross-modal interactions? It’s harder to tell than you might think!](https://aclanthology.org/2020.emnlp-main.62/)  
    
- [Kosmos-2: Grounding Multimodal Large Language Models to the World](https://arxiv.org/abs/2306.14824)  

- [Chameleon: Mixed-modal early-fusion foundation models](https://arxiv.org/abs/2405.09818)  
    
- [MM1: Methods, Analysis and Insights from Multimodal LLM Pre-training](https://link.springer.com/chapter/10.1007/978-3-031-73397-0_18)  
    
- [MoMa: Efficient Early-Fusion Pre-training with Mixture of Modality-Aware Experts](https://arxiv.org/pdf/2407.21770)

- [Training Compute-Optimal Large Language Models](https://arxiv.org/abs/2203.15556)  
    
- [Super-NaturalInstructions: Generalization via Declarative Instructions on 1600+ NLP Tasks](https://arxiv.org/abs/2204.07705)  
    
- [LoRA: Low-Rank Adaptation of Large Language Models](https://arxiv.org/abs/2106.09685)  
    
- [A Visual Guide to Mixture of Experts (MoE)](https://newsletter.maartengrootendorst.com/p/a-visual-guide-to-mixture-of-experts)  
    
- [A Visual Guide to Quantization](https://newsletter.maartengrootendorst.com/p/a-visual-guide-to-quantization)  
    
- [Improved Baselines with Visual Instruction Tuning](https://arxiv.org/abs/2310.03744)

- [Quantifying & Modeling Multimodal Interactions: An Information Decomposition Framework](https://arxiv.org/abs/2302.12247)  
    
- [Multimodal Transformer for Unaligned Multimodal Language Sequences](https://arxiv.org/abs/1906.00295)  
    
- [Masked Autoencoders Are Scalable Vision Learners](https://arxiv.org/abs/2111.06377)  
    
- [Scaling Laws for Native Multimodal Models Scaling Laws for Native Multimodal Models](https://arxiv.org/abs/2504.07951)  
    
- [Transfer between Modalities with MetaQueries](https://arxiv.org/abs/2504.06256)

- [LoRA: Low-Rank Adaptation of Large Language Models](https://arxiv.org/abs/2106.09685)  
    
- [Gated Linear Attention Transformers with Hardware-Efficient Training](https://arxiv.org/abs/2312.06635)  
    
- [Unintended Impacts of LLM Alignment on Global Representation](https://arxiv.org/abs/2402.15018)  

- [A Visual Guide to Quantization](https://newsletter.maartengrootendorst.com/p/a-visual-guide-to-quantization)  
    
- [Scaling Instruction-Finetuned Language Models](https://arxiv.org/abs/2106.09685)

- [Scalable Diffusion Models with Transformers](https://arxiv.org/abs/2212.09748)  
    
- [Flow Matching in Latent Space](https://arxiv.org/abs/2307.08698)  
    
- [Scaling Rectified Flow Transformers for High-Resolution Image Synthesis](https://arxiv.org/abs/2403.03206)  
    
- [Movie Gen: A Cast of Media Foundation Models](https://arxiv.org/abs/2410.13720)

- [LLaMA-Adapter: Efficient Fine-tuning of Language Models with Zero-init Attention](https://arxiv.org/pdf/2303.16199)  
    
- [Cobra: Extending Mamba to Multi-Modal Large Language Model for Efficient Inference](https://arxiv.org/pdf/2403.14520)  
    
- [ModaVerse: Efficiently Transforming Modalities with LLMs](https://arxiv.org/abs/2401.06395)  
    
- [Spider: Any-to-Many Multimodal LLM](https://arxiv.org/pdf/2411.09439)  
    
- [SPHINX-X: Scaling Data and Parameters for a Family of Multi-modal Large Language Models](https://arxiv.org/pdf/2402.05935)  
    
- [How Far Are We to GPT-4V? Closing the Gap to Commercial Multimodal Models with Open-Source Suites](https://arxiv.org/pdf/2404.16821)  
    
- [NExT-GPT: Any-to-Any Multimodal LLM](https://arxiv.org/pdf/2309.05519)  
    
- [Learning to rebalance multi-modal optimization by adaptively masking subnetworks](https://arxiv.org/pdf/2404.08347)

- [Large Language Diffusion Models](https://arxiv.org/pdf/2502.09992)  
    
- [Compositional Generative Modeling: A Single Model is Not All You Need](https://arxiv.org/pdf/2402.01103)  
    
- [Flow Matching for Generative Modeling](https://arxiv.org/abs/2210.02747)  
    
- [Flow Matching Guide and Code](https://arxiv.org/abs/2412.06264)  
    
- [FlowMotion: Target-Predictive Conditional Flow Matching for Jitter-Reduced Text-to-Motion Generation](https://arxiv.org/abs/2504.01338)  
    
- [MusFlow: Multimodal Music Generation via Conditional Flow Matching](https://arxiv.org/abs/2504.13535)  
    
- [Unraveling the Connections Between Flow Matching and Diffusion Probabilistic Models](https://arxiv.org/abs/2311.07625)  
    
- [Exploring Diffusion and Flow Matching Under Generator Matching](https://arxiv.org/abs/2412.11024)

- [Deep reinforcement learning from human preferences](https://arxiv.org/abs/1706.03741)  
    
- [Deepseek-r1: Incentivizing reasoning capability in LLMs via reinforcement learning](https://arxiv.org/abs/2501.12948)  
    
- [Faulty reward functions in the wild](https://openai.com/index/faulty-reward-functions/)  
    
- [Direct preference optimization: Your language model is secretly a reward model](https://arxiv.org/abs/2305.18290)



- [Interactive Sketchpad: A Multimodal Tutoring System for Collaborative, Visual Problem-Solving](https://arxiv.org/abs/2503.16434)  
    
- [VideoWebArena: Evaluating Multimodal Agents on Video Understanding Web Tasks](https://arxiv.org/abs/2410.19100)  
    
- [OpenVLA: An Open-Source Vision-Language-Action Model](https://arxiv.org/abs/2406.09246)  
    
- [ArtPrompt: ASCII Art-based Jailbreak Attacks against Aligned LLMs](https://arxiv.org/abs/2402.11753)  
    
- [Guidelines for Human-AI Interaction](https://dl.acm.org/doi/abs/10.1145/3290605.3300233)










