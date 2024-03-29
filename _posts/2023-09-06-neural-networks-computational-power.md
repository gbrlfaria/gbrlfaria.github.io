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

bibliography: 2023-09-06-neural-networks-computational-power.bib

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

There are many different models of computation within this theory, each with their own set of capabilities and some stronger than others.
A particularly important one is the [Turing machine](https://en.wikipedia.org/wiki/Turing_machine), which is capable of performing any algorithmic computation.
According to the [Church-Turing thesis](https://en.wikipedia.org/wiki/Church%E2%80%93Turing_thesis), any function that is computable can be computed by a Turing machine.
Thus, any model that can simulate a Turing machine is equally capable of general computation.
Such models are said to be Turing-complete.

Knowing this, it would be natural to expect that a computational model that can perform arbitrary reasoning and solve arbitrary problems must be capable of performing arbitrary computation.
In other words for a model to be capable of general intelligence, it must be capable of general computation (Turing-complete).

But what does all of this have to do with neural networks?
Much like any computational model, neural networks transform an input into an output, and are therefore a subject of the theory of computation.
Accordingly, we are able to determine the computational power of different neural network architectures based on this theory.
In fact, this treatment of neural networks is not a new idea.
Let's explore this further.

## Neural networks and their computational power: the beginnings

The study of neural networks has a perhaps surprising relationship with the field of theoretical computer science, with each discipline influencing the other over the course of their development <d-cite key="forcada2002flann" />.
This relationship can be traced back to the pioneering work of McCulloch and Pitts <d-cite key="mcculloch1943nn" />, which introduced the first artificial neural network model and demonstrated its ability to express logical propositions, and to Kleene <d-cite key="kleene1956automata" /> and Minsky <d-cite key="minsky1967computation" />, who established the computational model of finite automata and its connection to artificial neural networks.

<div class="row justify-content-center">
  <div>
    {% include figure.liquid path="assets/img/mcculloch_pitts_network.jpg" class="img-fluid" %}
  </div>
</div>
<div class="caption">
  Representation of a logical proposition by a McCulloch-Pitts network <d-cite key="logicalneuron"></d-cite>.
  In the diagram, painted-dot ends indicate excitatory inputs, while looping ends indicate inhibitory inputs.
</div>

In 1943, McCulloch and Pitts introduced the first computational model of biological neural networks.
In this model, neurons are represented by threshold logical units (TLUs).
Each unit exhibits an "all-or-nothing" behavior, where it can be considered either active or inactive based on the number of excitatory inputs and the presence of inhibitory inputs. Due to the binary nature of this model, McCulloch and Pitts argued that neural activity can be treated by means of propositional logic.
Essentially, the output of each neuron in a network can be interpreted as the truth value of a logical proposition.
By combining multiple neurons, we can therefore construct propositions of increasing complexity (see image above).
Based on this, McCulloch and Pitts characterized the set of propositions that can be expressed by neural networks.

Later, in 1956, Kleene published a mathematical reworking of McCulloch's paper which also included significant developments in the theory of finite automata.
In his paper, titled *Representation of Events in Nerve Nets and Finite Automata*, Kleene characterized the set of "regular events" (which we today refer to as regular expressions), and showed that this is exactly what finite automata and McCulloch-Pitts networks with circles<d-footnote>Feedback; recurrent connections. Interestingly, the idea of a recurrent network was present since the very inception of artificial neural networks in McCulloch and Pitts's paper, although the modern recurrent neural networks that we know today would not be developed until the late 80s.</d-footnote> can represent.
Therefore, Kleene established the equivalence between finite automata and McCulloch-Pitts networks.
The simulation of finite automata using McCulloch-Pitts neurons was later explicitly shown by Minsky in 1967, in his book *Computation: Infinite and Finite Machines*.

Since then, neural networks have evolved significantly, incorporating continuous values, multiple layers, differentiable activations, and learning through backpropagation.
This process has led to the development of the modern neural networks that we know today.
Concurrently, the theory of computation has also advanced, influencing the study of the computational power of these neural networks.

## The computational power of modern sequence models

<div class="row justify-content-center">
  <div>
    {% include figure.liquid path="assets/img/rnn.svg" class="img-fluid" %}
  </div>
</div>
<div class="caption">
  Illustration of a recurrent neural network (RNN).
</div>

With the development of modern RNNs <d-cite key="elman1990rnn" />, researchers became increasingly interested in understanding the computational and learning abilities of sequence-processing neural networks.
This has led to multiple research efforts into determining the capabilities and limitations of RNNs and their extensions, such as the LSTM and memory-augmented neural networks <d-cite key="steijvers1996csrnn,gers2001lstm,das1992stack,siegelmann1996farnn" />.
Using tools from the theory of computation, including automata and formal languages, researchers have conducted empirical and theoretical analyses in order to establish what kinds of strings such networks can process and what problems they can effectively solve.

Around this time, an important line of research emerged, focusing on the theoretical investigation of the Turing completeness of neural networks.
In their classical paper, Siegelmann and Sontag <d-cite key="siegelmann1992turing" /> established the Turing completeness of RNNs with arbitrary precision, saturated linear activations, and unlimited computational steps.
They demonstrated this by simulating a two-stack machine, where the RNN's (arbitrarily precise) hidden state encoded the machine's internal state at each step.
This result would influence research decades later.

However, there are limitations associated with the assumptions in Siegelmann's work.
Several authors have argued that these are unrealistic, leaving a significant gap between theory and practice <d-cite key="chen2018recurrent,weiss2018practical,merrill2019sequential" />.
Notably, the Turing machine simulation proposed in her proof would be difficult to realize in a practical learning setting and substantially differs from the typical supervised sequence modeling setup.
Thus, a more recent line of research attempts to study the computational power of neural networks under more realistic assumptions, such as finite precision and a number of computation steps bounded by the input length.

<div class="l-page row justify-content-center">
  <table>
    <tr>
      <th>Level</th>
      <th>Task</th>
      <th>RNN</th>
      <th>LSTM</th>
      <th>Stack-RNN</th>
      <th>Tape-RNN</th>
      <th>Transformer (encoder)</th>
      <th>Transformer (autoregressive)</th>
    </tr>
    <tr>
      <td>R</td>
      <td>Even Pairs</td>
      <td>100.0</td>
      <td>100.0</td>
      <td>100.0</td>
      <td>100.0</td>
      <td>96.4</td>
      <td>-</td>
    </tr>
    <tr>
      <td>R</td>
      <td>Modular Arithmetic (Simple)</td>
      <td>100.0</td>
      <td>100.0</td>
      <td>100.0</td>
      <td>100.0</td>
      <td>24.2</td>
      <td>-</td>
    </tr>
    <tr>
      <td>R</td>
      <td>Parity Check</td>
      <td>100.0</td>
      <td>100.0</td>
      <td>100.0</td>
      <td>100.0</td>
      <td>52.0</td>
      <td>-</td>
    </tr>
    <tr>
      <td>R</td>
      <td>Cycle Navigation</td>
      <td>100.0</td>
      <td>100.0</td>
      <td>100.0</td>
      <td>100.0</td>
      <td>61.9</td>
      <td>-</td>
    </tr>
    <tr>
      <td>DCF</td>
      <td>Stack Manipulation</td>
      <td>56.0</td>
      <td>59.1</td>
      <td>100.0</td>
      <td>100.0</td>
      <td>57.5</td>
      <td>53.2</td>
    </tr>
    <tr>
      <td>DCF</td>
      <td>Reverse String</td>
      <td>62.0</td>
      <td>60.9</td>
      <td>100.0</td>
      <td>100.0</td>
      <td>62.3</td>
      <td>53.5</td>
    </tr>
    <tr>
      <td>DCF</td>
      <td>Modular Arithmetic</td>
      <td>41.3</td>
      <td>59.2</td>
      <td>96.1</td>
      <td>95.4</td>
      <td>32.5</td>
      <td>-</td>
    </tr>
    <tr>
      <td>DCF</td>
      <td>Solve Equation</td>
      <td>51.0</td>
      <td>67.8</td>
      <td>56.2</td>
      <td>64.4</td>
      <td>25.7</td>
      <td>-</td>
    </tr>
    <tr>
      <td>CS</td>
      <td>Duplicate String</td>
      <td>50.3</td>
      <td>57.6</td>
      <td>52.8</td>
      <td>100.0</td>
      <td>52.8</td>
      <td>100.0</td>
    </tr>
    <tr>
      <td>CS</td>
      <td>Missing Duplicate</td>
      <td>52.3</td>
      <td>54.3</td>
      <td>55.2</td>
      <td>100.0</td>
      <td>56.4</td>
      <td>-</td>
    </tr>
    <tr>
      <td>CS</td>
      <td>Odds First</td>
      <td>51.0</td>
      <td>55.6</td>
      <td>51.9</td>
      <td>100.0</td>
      <td>52.8</td>
      <td>54.7</td>
    </tr>
    <tr>
      <td>CS</td>
      <td>Binary Addition</td>
      <td>50.3</td>
      <td>55.5</td>
      <td>52.7</td>
      <td>100.0</td>
      <td>54.3</td>
      <td>69.0</td>
    </tr>
    <tr>
      <td>CS</td>
      <td>Binary Multiplication</td>
      <td>50.0</td>
      <td>53.1</td>
      <td>52.7</td>
      <td>58.5</td>
      <td>52.2</td>
      <td>52.2</td>
    </tr>
    <tr>
      <td>CS</td>
      <td>Compute Sqrt</td>
      <td>54.3</td>
      <td>57.5</td>
      <td>56.5</td>
      <td>57.8</td>
      <td>52.4</td>
      <td>52.4</td>
    </tr>
    <tr>
      <td>CS</td>
      <td>Bucket Sort</td>
      <td>27.9</td>
      <td>99.3</td>
      <td>78.1</td>
      <td>70.7</td>
      <td>91.9</td>
      <td>40.4</td>
    </tr>
  </table>
</div>
<div class="caption">
  Maximum accuracy in recognizing different formal languages across the Chomsky hierarchy (R = Regular, DCF = deterministic context-free, CS = context-sensitive) <d-cite key="deletang2023chomsky"></d-cite>. <d-footnote>Notice how the autoregressive Transformer is able to perfectly solve the string duplication task. This might help explain one of the most important abilities of LLMs such as ChatGPT, which is to transform text while reliably maintaining information (think of formatting some data into a table or a JSON string).</d-footnote>
</div>

<div class="row justify-content-center">
  <div>
    {% include figure.liquid path="assets/img/chomsky.svg" class="img-fluid" %}
  </div>
</div>
<div class="caption">
  Correspondence between formal languages, automatons, and different neural network architectures for sequence processing <d-cite key="deletang2023chomsky"></d-cite>.
</div>

This trend has been followed by many recent works, both empirical and theoretical, which investigate the computational power of sequence models in practical settings <d-cite key="weiss2018practical,merrill2019sequential,tran2018hierarchy,korsky2019computational,suzgun2019lstm,ebrahimi2020dyck" />.
Some of these works not only explore the models' expressive capacity, but also their ability to learn to recognize languages in practice.
One particularly relevant example is the recent work by Delétang et al. <d-cite key="deletang2023chomsky" />, which empirically examines the ability of various neural network architectures, including RNNs, LSTMs, Transformers, and memory-augmented neural networks, to learn how to recognize different formal languages (see table above).
To accomplish this, the researchers trained each model using a variety of short strings from each formal language.
Then, they evaluated the generalization ability of the models by measuring their accuracy on a diverse range of test strings, many considerably longer than those seen during training.
Based on these results, the authors classified each architecture according to the [Chomsky hierarchy](https://en.wikipedia.org/wiki/Chomsky_hierarchy) (see image above).
Notice how memory-augmented neural networks exhibit a stronger capacity compared to the other architectures, and how Transformers seemingly do not correspond to any level of the Chomsky hierarchy.

| Neural Network Architecture  | Recognizable Languages                | References                             |
| :--------------------------- | :------------------------------------ | :------------------------------------- |
| Sigmoid / Tanh RNN           | Regular languages                     | <d-cite key="siegelmann1996farnn,merrill2019sequential" />      |
| LSTM                         | Regular languages + Counter languages | <d-cite key="weiss2018practical,merrill2019sequential" /> |
| GRU                          | Regular languages                     | <d-cite key="merrill2019sequential" /> |
| CNN (finite receptive field) | Strictly local languages              | <d-cite key="merrill2019sequential" /> |

<div class="caption">
  Common neural network architectures and the formal language classes they can theoretically recognize.
</div>

Within this context, Merrill <d-cite key="merrill2019sequential,merrill2020formal" /> made an important theoretical advance by formalizing the concept of saturated neural networks.
In these networks, activation values are discretized by increasing the parameter norm to an asymptotic limit in the presence of squashing activation functions, similarly to the idea described in <d-cite key="siegelmann1996farnn" />.
The concept of saturated neural networks enabled a principled analysis of neural sequence models that led to a more realistic classification of their computational capabilities.
The table above presents some of the most relevant theoretical results related to this line of research.

## The computational power of Transformers

<div class="row justify-content-center">
  <div>
    {% include figure.liquid path="assets/img/transformer.svg" class="img-fluid" %}
  </div>
</div>
<div class="caption">
  The Transformer architecture <d-cite key="zhang2023dive"></d-cite>.
</div>

So far, much of the results we have seen focused on recurrent neural networks.
But the most prominent architecture in today's sequence processing landscape is the Transformer, which is the basis of models like ChatGPT and other LLMs.
Due to the relatively recent emergence of this architecture <d-cite key="vaswani2017transformer" />, research into the theory of Transformers and their attention mechanism is comparably new in relation to that of RNNs.
Nonetheless, many recent studies have aimed at theoretically analyzing them.

Inspired by Siegelmann's work <d-cite key="siegelmann1992turing" />, Pérez et al. <d-cite key="perez2019turing,perez2021turing" /> proved the Turing completeness of Transformers.
The proof consisted in directly simulating a Turing machine, step by step, using an encoder-decoder Transformer.
In the proposed simulation, the output tokens are responsible for keeping track of the machine's state and current symbol at each time step.
In each forward pass, the decoder calculates the current position of the Turing machine's head by summing the directions of all previous head movements (i.e., $$\{+1,-1\}$$), which are in turn calculated from the previous output tokens.
Then, it retrieves the symbol corresponding to the calculated position and proceeds to output the next state and the next symbol under the head.
This process is repeated until halting.
Similarly to Siegelmann and Sontag <d-cite key="siegelmann1992turing" />, the authors assumed arbitrary precision and an unlimited number of computation steps.

Contrasting with Pérez's approach, another line of research analyzed Transformers from a different perspective.
In particular, this line of research focuses on the ability of Transformer encoders to process strings in a single step, as opposed to solving tasks using multiple decoder steps.
In this context, the first theoretical results on the limitations of Transformers were shown by Hahn <d-cite key="hahn2020limitations" />.
He demonstrated that hard-attention Transformers---in which each layer can only attend to a single token at a time---cannot recognize the Parity<d-footnote>The Parity language is the language of binary strings whose number of $1$s is even.</d-footnote> and Dyck-$$k$$<d-footnote>The Dyck-$k$ language is the language of well-balanced parentheses, where $k$ indicates the number of types of parentheses. For instance, "({()})" is a valid string in the Dyck-2 language, while "({" and "({))" are not.
Due to its nature, this language is often used as a proxy for hierarchy understanding, which is considered essential for effective natural language processing.</d-footnote> languages, suggesting limitations on the ability of Transformers to model hierarchy.
Moreover, Hahn showed that soft-attention Transformers cannot robustly model the Parity and Dyck-$$k$$ languages, being unable to attain perfect cross-entropy on these tasks.
Particularly, this proof assumed that all layers of the Transformer are [Lipschitz-continuous](https://en.wikipedia.org/wiki/Lipschitz_continuity).

Hahn's work laid the ground for subsequent studies.
Chiang and Cholak <d-cite key="chiang2022overcoming" /> followed up by observing that the Lipschitz-continuity assumption disregarded the impact of layer normalization on the Transformer.
Based on this observation, the authors constructed a soft-attention Transformer with layer normalization that can robustly recognize the Parity language.
Yao et al. <d-cite key="yao2021bounded" /> also followed up, demonstrating that Transformers can recognize Dyck languages with bounded nesting depth.
According to the authors, this setup could better represent the hierarchical structure of natural language, which could help explain the success of Transformers in natural language processing (NLP).
Meanwhile, Bhattamishra et al. <d-cite key="bhattamishra2020ability" /> demonstrated that uniform-attention Transformers---in which each layer can attend to multiple tokens with uniform intensity---can recognize the Shuffle-Dyck-$$k$$<d-footnote>The Shuffle-Dyck-$k$ language is a Dyck-$k$ language where each type of bracket must be well-balanced while their relative order is unconstrained. For instance, "({)}" is a valid string in the Shuffle-Dyck-2 language.</d-footnote> language.
Furthermore, they showed that Transformers can simulate a less powerful kind of counter automaton called Simplified Stateless Counter Machine (SSCM), establishing a first lower bound on the computational power of these models.
They supported this observation by empirically demonstrating that Transformers can learn several regular and counter languages.

In parallel, Weiss et al. <d-cite key="weiss2021rasp" /> introduced RASP, a programming language that closely emulates the computational constraints of the Transformer architecture, providing a first computational model of Transformers that could be useful in understanding their inner workings and learning abilities.
In their work, the authors manually construct RASP programs to solve different tasks and show that these can be realized by actual models.

<div class="row justify-content-center">
  <div>
    {% include figure.liquid path="assets/img/example_circuit.svg" class="img-fluid" %}
  </div>
</div>
<div class="caption">
  A Boolean circuit that takes a string in $\{0, 1\}^5$ and returns whether it contains the bigram $11$ <d-cite key="merrill2022saturated"></d-cite>.
  By constructing families of circuits (i.e., sets of related circuits parameterized by input size), we can use circuit complexity theory to analyze the computational capabilities of parallel models in processing arbitrary strings.
</div>

A more robust understanding of the computational model of Transformers emerged after Hao et al. <d-cite key="hao2022circuit" /> analyzed the architecture using circuit complexity theory.
Simplifying and unifying prior results, the authors proved that hard-attention Transformers can only recognize formal languages in the complexity class $$\text{AC}^0$$, which comprises the languages recognizable by families of Boolean circuits with polynomial size constant depth.
The computational power of uniform and soft-attention Transformers, however, remained an open question.
Through additional developments <d-cite key="merrill2022saturated" />, Merrill and Sabharwal <d-cite key="merrill2023parallelism" /> finally published the paper titled *The Parallelism Tradeoff: Limitations of Log-Precision Transformers*.
In this paper, they established that log-precision Transformers can be simulated by uniform polynomial-size constant-depth threshold circuits and, as a result, are limited to recognizing languages in $$\text{TC}^0$$, suggesting fundamental limitations on the expressive capacity of Transformers.
Later, researchers further improved on these results by proving tighter bounds on the expressivity of Transformers in terms of generalizations of first-order logic <d-cite key="chiang2023tighter,merrill2023logic" />.

In summary, research suggests that the Transformer does not align with any of the major classes of the Chomsky hierarchy.
Rather, results indicate that Transformers correspond to a limited parallel computational model, echoing the early idea that the attention mechanism has limited sequential processing abilities <d-cite key="tran2018hierarchy,dehghani2019ut" />.
In particular, Merrill and Sabharwal's findings indicate that, under reasonable assumptions<d-footnote>For example, logspace-uniform $\text{TC}^0 \neq \text{NP}$. See Section 2 of Merrill and Sabharwal's paper.</d-footnote>, there are many problems for which Transformers cannot generalize.
For instance, it would be impossible for an encoder-only Transformer such as BERT <d-cite key="devlin2019bert" /> to achieve perfect generalization on the [Boolean satisfiability problem](https://en.wikipedia.org/wiki/Boolean_satisfiability_problem) (SAT).
Likewise, a similar statement can be made about decoder-only Transformers like GPT <d-cite key="brown2020gpt" />.
Specifically, no such an LLM would be able to correctly answer the question "Is the Boolean formula $$X$$ satisfiable?" for arbitrary $$X$$ with a simple yes-or-no answer, since that would imply a computational budget of a single step.
Importantly, this limitation is not confined to the SAT problem; rather, it extends to *any problem of equivalent complexity*.

## Are there more powerful models?

Several approaches have been adopted to overcome the limitations of conventional architectures and create more powerful models.
One of them, which we have already mentioned, is memory-augmented neural networks <d-cite key="das1992stack,grefenstette2015transduce,hao2018context,joulin2015inferring,suzgun2019memory,dusell2023nstack,graves2014ntm,rae2016scaling" />.
In general, these networks are constructed by equipping a recurrent neural network with some kind of differentiable memory, typically with the goal of emulating a stronger kind of automaton.
Another approach is based on the very observation that, while the computational budget of a neural network is often constant, some problem instances are harder than others and may thus require more computation.
With this in mind, researchers have proposed several dynamic computation schemes for neural networks <d-cite key="graves2017act,dehghani2019ut,banino2021pondernet" />, which allow them to adapt the amount of computation according to the input.
However, these approaches often result in models that are complex, difficult to scale, or that do not beat Transformers on practical tasks.
This raises a question: is there a simple model that is both powerful and efficient, encompassing both parallel and sequential computation? This query motivated me to start my own investigation during my undergraduate studies.
Let's briefly explore it.

One interesting line of research investigates the use of differentiable optimizers as neural network layers.
The main idea is to use a parameterized optimization procedure as a part of the forward pass of a neural network and then differentiate through it such that its parameters can be learned.
Examples of this kind of model include OptNet <d-cite key="amos2017optnet" />, a differentiable convex optimization solver, SATNet <d-cite key="wang2019satnet" />, a differentiable MAXSAT solver based on semidefinte programming, and CombOptNet <d-cite key="paulus2021comboptnet" />, an integer programming solver that uses gradient approximations for differentiability.
Similarly, IREM <d-cite key="du2022irem" /> is a differentiable energy-based model that solves problems by minimizing an energy function using gradient descent.
By formulating the forward pass as an optimization problem, these models have a real potential for greater expressive power, often promising superior performance in reasoning problems.
However, they can be difficult to use practice.
In general, the optimization procedures associated with these models incur in elevated computational costs, which can quickly become prohibitive.
Moreover, these models are not adapted to sequence data, which precludes their immediate use in applications such as language modeling.

In this context, a different yet related class of models captures our attention: the class of deep equilibrium models (DEQs) <d-cite key="bai2019deq" />.
In essence, these models revolve around solving an equilibrium equation expressed as $$\mathbf z^\star=f(\mathbf z^\star,\mathbf x)$$.
Their output is calculated by repeatedly applying a neural network layer $$f(\cdot)$$ until a fixed point is reached, making DEQs equivalent to infinitely deep weight-tied neural networks.
As for backpropagation, these models exploit implicit differentiation in order to compute gradients by solving another equilibrium equation, without the need to store intermediate activations.
Notably, in contrast to the previously discussed models, DEQs can be readily applied to sequence data by employing convolutional and Transformer layers.
In fact, they have shown positive results in several NLP benchmarks, with some studies suggesting that DEQs have superior generalization capabilities compared to standard architectures <d-cite key="liang2021deqood" />.

However, it is crucial to understand the abilities of these models from a theoretical perspective.
Are DEQs any more expressive than regular CNNs and Transformers? Does their infinite depth lend them more computational power?
The short answer is yes.
I will not go into much detail, but we can show that DEQs can simulate formalisms ranging from finite automata to Turing machines, depending on the assumptions made.
For the Turing machine simulation, the key is to imagine that the vector $$\mathbf z$$ represents the tape, where each position encodes a symbol, a state, and the presence of the head.
Then, at each step, we only need to update the current symbol and state and then move the head to one of the neighboring positions, which can be easily done with convolution operations.
Unfortunately, these results do not necessarily translate well to practice.
For instance, running the experiments from Delétang's work <d-cite key="deletang2023chomsky" /> will show that DEQ-CNNs fail to learn even the most basic regular languages.
Moreover, DEQs are quite inefficient compared to regular sequence models, which can render them unusable on longer sequences.

The bottom line is that computational efficiency seems to be a major issue among all these approaches.
It appears that there exists, in fact, a parallelism tradeoff, and that it is key to the efficiency and success of Transformers; and it seems that any attempt at a more powerful neural network architecture inevitably leads to complications.

## What now?

We started this article on a quest to understand the reasoning and general computation abilities of neural networks.
Particularly, we have focused on the computational power of Transformers, the architecture that powers most current LLMs.
Research on the subject, however, reveals that the computations that these models can perform in a single step are quite limited, and that there are many problems that they cannot solve.
Unfortunately, alternative architectures that might offer greater computational capabilities often come with a variety of drawbacks such as elevated computational costs, making them impractical choices for creating models capable of general intelligence.

But what if we give up on the idea of having a model with an "all-powerful" step and fully embrace the idea of solving problems through multiple explicit "weak" steps?
After all, this is the approach used in Pérez's paper in order to prove the Turing completeness of Transformers.
This is also what the "step-by-step thinking" strategy <d-cite key="kojima2022zeroshot,wei2022cot" />, widely used by LLMs, looks like.
Is this ultimately the right approach to problem-solving?
If so, are Transformer-based LLMs already capable of general computation, meaning that they are all we need to achieve general intelligence?
Let's discuss this further.

Let's start by going back to Pérez's work.
In order to see if his Turing completeness proof holds in practice, we must go over its assumptions.
The two main ones are unbounded computation and arbitrary precision.
Let's ignore the assumption of an unlimited number of computation steps, since that is precisely what we're aiming for---taking as many steps as necessary in order to solve a problem.
Let's also ignore the arbitrary precision assumption, this time on the basis that the floating-point numbers on the computer are precise enough to carry Turing-complete computation for all practical problems (in fact, some believe that log-precision Transformers have enough capacity to compute a Turing machine step).
Given this context, does Pérez's proof apply in practice?
Not necessarily.
This is because the construction proposed by Pérez relies on a non-standard attention score function and an unconventional positional encoding scheme.
Meanwhile, practical Transformers use dot-product attention and standard positional encoding schemes, which would likely render the attention patterns needed for the Turing machine simulation impossible.
In the end, I believe that the practical computational power of autoregressive Transformer decoders is still not entirely clear.

However, even if such Transformers were proven to be Turing-complete in practice, a critical problem would remain: these models have linear space complexity and quadratic time complexity.
Because of this, processing excessively long sequences becomes impractical.
Certainly, such models are not able to naively reason for an indefinite amount of time, nor are they able to solve problems with very long descriptions.
As an example, fixing a bug in a program with 10K lines of code can be unfeasible even for the largest commercial LLMs of today.
Furthermore, while the attention operation is "dense" (i.e., the computation is performed over all input elements), the memory access pattern required to simulate a Turing machine should be mostly sparse.
In Pérez's simulation, after computing the current head position, we should only need to retrieve the current and the next element under the head.
Similarly, in a practical setting, we can imagine that the sparsity of an LLM's attention increases as its context gets longer through interaction.
This phenomenon arises as a simple result of the increasing amount of irrelevant information in its history over time.
From this, we can conclude that there is an inherent inefficiency in the way attention works, although this is the price we pay for the parallelism of Transformers.

In contrast, an ideal model should have a constant computation cost per step and sparse-access memory at inference time.
This is akin to the construction proposed in a recent paper by Chung and Siegelmann <d-cite key="chung2021rnnbounded" />, in which they construct a Turing-complete finite-precision RNN that is augmented with two external growing memory modules so as to simulate a two-stack machine.
However, the RNN in this construction interacts with the memory modules in a discrete, non-differentiable manner, meaning that alternative learning strategies are necessary in order to train the model in practice (e.g., reinforcement learning).
Moreover, since the model is RNN-based, it cannot be parallelized during training like Transformers.

Yet, efficiency during training is just as important as efficiency during inference.
After all, large-scale self-supervised pretraining is the cornerstone of building LLMs.
Fortunately, a recent yet rapidly evolving line of research aims to develop efficient alternatives to Transformers while matching their performance levels <d-cite key="gu2020hippo,gu2021lssl,gu2022efficiently,smith2023simplified,orvieto2023resurrecting,poli2023hyena,sun2023retnet" />.
Particularly, this line of research has produced several state-space models that can be both trained in parallel and run recurrently at inference time.
With remarkable constant complexity both in space and time during inference, these models have exhibited promising results across a multitude of sequence processing tasks, both real and artificial.
Notably, there have been good results on both language modeling and downstream NLP tasks.
However, it should be noted that these models are based on linear recurrences, in contrast to the nonlinear recurrences of traditional RNNs.
Consequently, the expressive power of such networks remains unknown, although it is likely weaker than that of Transformers.

## A path forward?

Using these recent architectures, it might be possible to create a model that is both Turing-complete and capable of efficient parallel and sequential computation.
The key is to equip the model with an external memory module and use the right training setup.
Specifically, this training setup would consist of two distinct phases.
In the first phase, the model goes through parallel self-supervised pretraining, during which it learns from a substantial amount of text.
In the second, the model is subjected to sequential reinforcement learning fine-tuning, where the model is equipped with the external memory module and tasked with solving various reasoning problems.
The idea is that, in the self-supervised pretraining phase, the model would learn to compress and approximate language information.
Then, in the reinforcement learning fine-tuning phase, the model would learn to use language to carry reasoning and computation in a precise and generalizable manner.
In other words, it is as though the first phase consisted in learning the "machine" of intelligence, whereas the second phase consisted in operating it by learning the "program" of intelligence.
In a way, this aligns with the notion presented by Mahowald et al. <d-cite key="mahowald2023dissociating" /> that language and thought are distinct abilities that require different approaches.
Thus, we could maybe say that in the first phase the model learns language, whereas in the second the model learns thought.

But this is just a rough idea and, naturally, it has its own set of challenges.
What is the best way to implement the external memory module?
Would it ever be practical to sequentially fine-tune something like a large language model with reinforcement learning, even with constant generation cost?
What datasets and training objectives should be used in the fine-tuning phase?
Would learning from text data alone using current machine learning methods be enough?
And how could a model like this be used within a broader text-based agent framework, being able to use external tools in order to accomplish its goals (e.g., [LangChain](https://www.langchain.com/))?

At the end of the day, it only seems certain that efficiency and Turing completeness are important properties of models capable of general intelligence.
This is a very complex and broad subject and no single article would be able to address all the related problems and possibilities.
The approach presented here is thus mere speculation; only time will tell what such models will look like.