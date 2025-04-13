---
layout: post
disqus_comments: true
related_posts: false
toc:
  sidebar: left
title: LLM Learning Roadmap
date: 2025-04-13
description: important llm models since 2017
tags: CS ML NLP LLM
categories: Code
thumbnail: assets/img/2025Q2/1.png
---


<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/2025Q2/1.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>


[66個大型語言模型LLM經典論文](https://tomohiroliu22.medium.com/66個大型語言模型llm經典論文-0fcdab74e822)



# Encoder

## Transformer

**《Attention Is All You Need》**（2017）

 https://arxiv.org/pdf/1706.03762.pdf

- **贡献**：提出Transformer架构，取代传统RNN/CNN，奠定了所有现代LLM的基础。核心创新是自注意力机制，支持并行计算和长距离依赖建模610。
- **研读重点**：多头注意力机制、位置编码、编码器-解码器结构。

**《Transformer-XL: Attentive Language Models Beyond a Fixed-Length Context》**（2019）

https://arxiv.org/pdf/1901.02860

- **Abstract**：讓Transformer可以吃更長的句子

**《Reformer: The Efficient** **Transformer****》**（2020）

https://arxiv.org/pdf/2001.04451.pdf

- **Abstract**：讓Transformer運算更快、使用記憶體更有效



## BERT族

**《****BERT****: Pre-training of Deep Bidirectional** **Transformers****》**（2018）

 https://arxiv.org/pdf/1810.04805

- **贡献**：引入双向Transformer编码器，通过掩码语言模型（MLM）和下一句预测（NSP）任务，显著提升文本理解能力610。
- **研读重点**：双向上下文建模与预训练任务设计。

**《****ALBERT****:** **A Lite BERT** **for Self-supervised Learning of Language Representations》**（2019）

https://arxiv.org/pdf/1909.11942.pdf

- **Abstract**：我把BERT參數減少，然後加上了一個酷酷的自監督式學習

**《RoBERTa: A Robustly Optimized** **BERT** **Pretraining Approach》**（2019）

https://arxiv.org/pdf/1907.11692.pdf

- **Abstract**：我用了更多資源、更猛的方法訓練一個更猛的BERT

**《DistilBERT, a distilled version of** **BERT****: smaller, faster, cheaper and lighter》**（2019）

- **Abstract**：利用知識蒸餾訓練更小的BERT。

## ERNIE

**《ERNIE: Enhanced Language Representation with Informative Entities》**（2019）

 https://arxiv.org/pdf/1905.07129

- **贡献**：将知识图谱融入BERT，提升模型对结构化知识的理解能力，开辟知识增强型LLM方向610。
- **研读重点**：知识注入方法、异构信息融合。

# Decoder

## GPT-1

**《Improving Language Understanding by Generative Pre-Training》（GPT-1）**（2018）

 https://cdn.openai.com/research-covers/language-unsupervised/language_understanding_paper.pdf

- **贡献**：首次将Transformer解码器用于生成式预训练，提出“预训练+微调”范式，验证了无监督预训练在NLP任务中的有效性610。
- **研读重点**：自回归语言模型、任务适配微调方法。

## **GPT-2**

**《Language Models are Unsupervised Multitask Learners》（GPT-2）**（2019）

- **贡献**：证明大规模模型可通过无监督预训练实现多任务Zero-Shot学习，推动模型参数向百亿级扩展610。
- **研读重点**：Zero-Shot推理能力与模型规模的关系。

## GPT-3

**《Language Models are Few-Shot Learners》（****GPT-3****）**（2020）

 https://arxiv.org/pdf/2005.14165

- **贡献**：千亿参数模型展示出强大的上下文学习（In-Context Learning）能力，推动了对“涌现能力”的研究210。
- **研读重点**：Few-Shot提示工程、模型规模与泛化性能的关系。

**《Scaling Laws for Neural Language Models》**（2020）

- **Abstract**：最早的LLM規模定律全面分析

https://arxiv.org/pdf/2001.08361.pdf

## GPT-4

GPT-4 Technical Report (2023)

https://arxiv.org/pdf/2303.08774.pdf

- **Abstract**：目前世界上最強的LLM之一

## InstructGPT

**Training language models to follow instructions with human feedback**  （2022）

https://arxiv.org/pdf/2203.02155.pdf

- **Abstract**：ChatGPT的前身，讓人類來教GPT-3社會化

## LLaMA

LLaMA: Open and Efficient Foundation Language Models （2023）

- **Abstract**：最有名的開源LLM第一代

https://arxiv.org/pdf/2302.13971.pdf

Llama 2: Open Foundation and Fine-Tuned Chat Models  （2023）

https://arxiv.org/pdf/2307.09288.pdf

- **Abstract**：開源LLM第二代，可以和人對話了

# Decoder-Encoder

## UniLM

**《Unified Language Model Pre-training for Natural Language Understanding and Generation》**（2019）

https://arxiv.org/pdf/1905.03197.pdf

- **Abstract**：讓我們把NLU和NLG預訓練統一吧

## T-5

**《Exploring the Limits of** **Transfer Learning** **with a Unified Text-to-Text** **Transformer****》（T5）**（2020）

 https://arxiv.org/pdf/1910.10683

- **贡献**：将各类NLP任务统一为文本到文本的框架，验证了模型泛化能力的极限611。
- **研读重点**：任务统一化设计、模型容量与数据量的平衡。

## BART

**《****BART****: Denoising Sequence-to-Sequence Pre-training》**（2019）

 https://arxiv.org/pdf/1910.13461

- **贡献**：结合双向编码器与自回归解码器，支持文本生成与重构任务，成为多任务适配的经典架构1012。
- **研读重点**：去噪自编码预训练、多任务适应性。

**《Multimodal Chain-of-Thought》**（2023，参考多模态LLM综述）

- **贡献**：扩展思维链（CoT）至多模态推理，推动LLM在视觉-语言任务中的复杂推理能力。
- **研读重点**：多模态信息整合、跨模态推理框架。

**《LoRA: Low-Rank Adaptation of Large Language Models》**（2021）

- **贡献**：提出低秩适配微调方法，显著降低大模型微调成本，成为轻量化部署的核心技术。
- **研读重点**：参数高效微调、适配器设计原理。