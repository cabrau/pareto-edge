# Pareto-Edge

**Pareto-Aware Adaptive Model Selection for Energy-Efficient Edge AI**

Pareto-Edge is a research project investigating **runtime model selection for energy-efficient inference on edge devices**.

Instead of deploying a single model and using it for every input, the system maintains a portfolio of models with different trade-offs between predictive quality, energy consumption, latency, and computational resources. At runtime, it selects an appropriate model according to the characteristics of the input and the current operating conditions of the device.

## Motivation

Edge AI systems operate under constrained and dynamic environments. Computational resources, energy availability, thermal conditions, latency requirements, and input difficulty can vary over time.

A highly accurate model is not necessarily the most appropriate model for every inference.

For an easy input, running a computationally expensive model may provide little additional predictive value while consuming substantially more energy. Conversely, difficult inputs may justify the additional cost of a more capable model.

This motivates a shift from:

> **Which model should be deployed?**

to:

> **Which model should be executed for this input, under the current resource constraints?**

## Research Direction

The project investigates **Pareto-aware adaptive model selection**, treating inference as a multi-objective decision problem.

Given a portfolio of models:

[
\mathcal{M} = {M_1, M_2, \ldots, M_K}
]

each model can be characterized by several objectives, such as:

* Predictive quality
* Energy consumption
* Inference latency
* Computational cost
* Memory/resource usage

These objectives generally conflict with one another. Rather than reducing them to a single weighted score, Pareto-Edge explores the use of **Pareto optimality** to represent the available trade-offs between competing objectives.

At runtime, a selection policy can then choose an appropriate model according to:

* Input characteristics and difficulty
* Current device state
* Resource constraints
* Application requirements
* The estimated trade-offs between candidate models

Conceptually:

```text
                  Input
                    │
                    ▼
            ┌───────────────┐
            │ Input Analysis │
            └───────┬───────┘
                    │
                    ▼
         ┌──────────────────────┐
         │ Runtime Context      │
         │                      │
         │ • Battery            │
         │ • Temperature        │
         │ • Resource usage     │
         │ • Latency budget     │
         └──────────┬───────────┘
                    │
                    ▼
          ┌────────────────────┐
          │ Model Selection    │
          │                    │
          │ Pareto-aware       │
          │ decision policy    │
          └─────────┬──────────┘
                    │
          ┌─────────┼─────────┐
          ▼         ▼         ▼
       Model A   Model B   Model C
       cheap     medium    accurate
          │         │         │
          └─────────┼─────────┘
                    ▼
                 Output
```

## Research Questions

The project is intended to investigate questions such as:

1. **Can runtime model selection reduce energy consumption while maintaining a target level of predictive quality?**

2. **How should model selection incorporate both input-dependent characteristics and dynamic device conditions?**

3. **Can Pareto-based selection provide advantages over fixed model deployment or scalarized objective functions?**

4. **How accurately can the energy, latency, and quality trade-offs of candidate models be estimated at runtime?**

5. **How should the system adapt when the operating conditions of the edge device change?**

6. **What is the computational overhead of the selection mechanism itself, and when does adaptive selection become beneficial?**

## Potential Methodological Directions

The research is intentionally open to several possible approaches, including:

* Pareto-front modeling
* Context-aware model selection
* Bayesian optimization
* Multi-objective Bayesian optimization
* Online learning
* Uncertainty-aware decision making
* Model cascades
* Adaptive computation
* Resource-aware inference

The specific methodology is still under investigation.

## Core Hypothesis

The working hypothesis is that **a portfolio of complementary models combined with an adaptive selection mechanism can achieve a better accuracy–energy trade-off than consistently executing a single model**.

In particular, the potential benefit comes from recognizing that the marginal value of additional computation is not constant across inputs or runtime conditions.

For an input (x), the additional predictive value of a more expensive model can be considered alongside its additional energy cost:

$Q(x,M_{\text{cheap}})$


$E(M_{\text{cheap}})$


The selection problem can therefore be viewed as determining whether the expected improvement in predictive quality justifies the additional computational and energy cost.

## Project Status

**Research / Experimental**

This repository currently serves as a research workspace. The problem formulation, experimental methodology, and model-selection strategy are expected to evolve as the research progresses.

## Repository Structure

```text
pareto-edge/
├── models/          # Candidate models and model configurations
├── datasets/        # Dataset definitions and preprocessing
├── profiling/       # Energy, latency, and resource profiling
├── pareto/          # Pareto-front computation and analysis
├── selection/       # Model-selection strategies
├── runtime/         # Runtime inference and adaptation
├── experiments/     # Experimental configurations and scripts
├── evaluation/      # Metrics and evaluation utilities
└── README.md
```

## Long-Term Goal

The long-term goal of Pareto-Edge is to develop and experimentally evaluate **adaptive inference strategies that treat energy and computational resources as first-class objectives of intelligent decision making at the edge**.

The project is motivated by the broader Green AI principle that efficient AI should not only rely on making individual models cheaper, but also on **avoiding unnecessary computation altogether**.

---


## Citation

*To be added when the research is published.*
