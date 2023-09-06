---
layout: distill
title: Artificial Intelligence and the Computational Power of Neural Networks
description: Understanding the capabilities and limitations of neural networks in the pursuit of artificial intelligence.
tags: artificial-intelligence neural-networks theory-of-computation
date: 2023-09-06
featured: false

authors:
  - name: Gabriel Faria
    url: "/"
    affiliations:
      name: "-"

bibliography: 2023-09-06-neural-network-computational-power.bib

# Optionally, you can add a table of contents to your post.
# NOTES:
#   - make sure that TOC names match the actual section names
#     for hyperlinks within the post to work correctly.
#   - we may want to automate TOC generation in the future using
#     jekyll-toc plugin (https://github.com/toshimaru/jekyll-toc).
toc:
  - name: Introduction
    # if a section has subsections, you can add them as follows:
    # subsections:
    #   - name: Example Child Subsection 1
    #   - name: Example Child Subsection 2
  - name: Theory of computation
  - name: "Neural networks and their computational power: the beginnings"
  - name: The computational power of modern sequence models
  - name: The computational power of Transformers
  - name: Are there more powerful models?
  - name: What now?
  - name: A path forward?

---

## Introduction

Artificial intelligence has been a longstanding pursuit in the field of computer science, driven by the ultimate goal of creating machines capable of human-like intelligence.
At its core, this endeavor aims to empower computers with the ability to solve a wide range of problems, from answering general questions to proving theorems, writing code, creating art, and playing games.
This ability to solve a large variety of arbitrary problems may be referred to as *general intelligence*.

The field of artificial intelligence has come a long way.
Today, it is spearheaded by neural networks and machine learning techniques, which have been responsible for realizing many of the goals envisioned over the last century.
We now have models capable of unprecedent super-human performance in complex game environments, such as AlphaGo <d-cite key="silver2016go,silver2017gozero" />.
We also have models capable of creating a images and illustrations from textual descriptions alone, such as DALL-E <d-cite key="ramesh2021zeroshot,ramesh2022hierarchical" /> and Stable Diffusion <d-cite key="rombach2021highresolution" />.
Most notably, we have models that are able to interact with humans using natural language and solve an impressive number of tasks, as exemplified by ChatGPT <d-cite key="openai2022chatgpt,ouyang2022training,openai2023gpt4" />.

Indeed, large language models (LLMs) like ChatGPT are prime examples of what modern neural networks are capable of.
Through extensive self-supervised pretraining and instruction-following fine-tuning, these models are able to achieve remarkable feats of intelligence.
These include not only holding conversations in natural language, but also generating code, solving mathematical problems, composing and editing text, and providing translations between languages.
Arguably, this is the closest we have ever been to having a system capable of general intelligence.

But can these models ever reason like a human? Despite their impressive abilities, these models are not infallible; they fall short of consistent generalization in many tasks.
In fact, they occasionally make simple reasoning mistakes that a human would easily avoid.
This raises some questions about what these models are ultimately capable of doing.
Let's disregard the question of learning for the moment and focus strictly on their theoretical capabilities.
Could these models solve any problem that a human could solve? Exactly how powerful are they? And, perhaps most importantly, is there a systematic way to go about such questions?

In this article, we will attempt to answer these questions, unraveling the capabilities and limitations of contemporary neural network models.
In doing so, we will hopefully shed light onto some of the challenges and potential solutions in the pursuit of general intelligence using neural networks.

## Theory of computation

The [theory of computation](https://en.wikipedia.org/wiki/Theory_of_computation) is a branch of theoretical computer science that explores the fundamental principles of computation, encompassing the study of algorithms, computational problems, and formal computational models.
Using this theory, we are able to analyze the capabilities of different models of computation, establish the computational complexity of different problems in terms of space and time, and even determine whether a problem is computable at all.
To enable this, the theory of computation offers a wide range of formal tools, including [automata](https://en.wikipedia.org/wiki/Automata_theory), [formal languages](https://en.wikipedia.org/wiki/Formal_language), [grammars](https://en.wikipedia.org/wiki/Formal_grammar), logics, and [circuits](https://en.wikipedia.org/wiki/Circuit_(computer_science)).

There are many different models of computation within this theory, each with their own set of capabilities.
The strongest of them is the [Turing machine](https://en.wikipedia.org/wiki/Turing_machine), which is capable of performing any algorithmic computation.
According to the [Church-Turing thesis](https://en.wikipedia.org/wiki/Church%E2%80%93Turing_thesis), any function that is computable can be computed by a Turing machine.
Thus, any model that can simulate a Turing machine is equally capable of general computation.
Such models are said to be Turing-complete.

But what does all of this have to do with neural networks?
Much like any computational model, neural networks transform an input into an output, and are therefore a subject of the theory of computation.
Accordingly, we are able to determine the computational power of different neural network architectures based on this theory.
In fact, this treatment of neural networks is not a new idea.
Let’s explore this further.

## Neural networks and their computational power: the beginnings

The study of neural networks has a perhaps surprising relationship with the field of theoretical computer science, with each discipline influencing the other over the course of their development <d-cite key="forcada2002flann" />.
This relationship can be traced back to the pioneering work of McCulloch and Pitts <d-cite key="mcculloch1943nn" />, which introduced the first artificial neural network model and demonstrated its ability to express logical propositions, and to Kleene <d-cite key="kleene1956automata" /> and Minsky <d-cite key="minsky1967computation" />, who established the computational model of finite automata and its connection to artificial neural networks.

<div class="row justify-content-center">
  <div>
    {% include figure.html path="assets/img/mcculloch_pitts_network.jpg" class="img-fluid" %}
  </div>
</div>
<div class="caption">
  Representation of a logical proposition by a McCulloch-Pitts network <d-cite key="logicalneuron"></d-cite>.
  In the diagram, painted dot ends indicate excitatory inputs, while looping ends indicate inhibitory inputs.
</div>

In 1943, McCulloch and Pitts introduced the first computational model of biological neural networks.
In this model, neurons are represented by threshold logical units (TLUs).
Each unit exhibits an "all-or-nothing" behavior, where it can be considered either active or inactive based on the number of excitatory inputs and the presence of inhibitory inputs. Due to the binary nature of this model, McCulloch and Pitts argued that neural activity can be treated by means of propositional logic.
Essentially, the output of each neuron in a network can be interpreted as the truth value of a logical proposition.
By combining multiple neurons, we can therefore construct propositions of increasing complexity (see image above).
Based on this, McCulloch and Pitts characterized the set of propositions that can be expressed by neural networks.

Later, in 1956, Kleene published a mathematical reworking of McCulloch's paper which also included significant developments in the theory of finite automata.
In his paper, titled *Representation of Events in Nerve Nets and Finite Automata* Kleene characterized the set of "regular events" (which we today refer to as regular expressions), and showed that this is exactly what finite automata and McCulloch-Pitts networks with circles<d-footnote>Feedback; recurrent connections. Interestingly, the idea of a recurrent network was present since the very inception of artificial neural networks in McCulloch and Pitts's paper, although the modern recurrent neural networks that we know today would not be developed until the late 80s.</d-footnote> can represent.
Therefore, Kleene established the equivalence between finite automata and McCulloch-Pitts networks.
The simulation of finite automata using McCulloch-Pitts neurons was later explicitly shown by Minsky in 1967, in his book *Computation: Infinite and Finite Machines*.

Since then, neural networks have evolved significantly, incorporating continuous values, multiple layers, differentiable activations, and learning through backpropagation.
This process has led to the development of the modern neural networks that we know today.
Concurrently, the theory of computation has also advanced, influencing the study of the computational power of these neural networks.

## The computational power of modern sequence models

