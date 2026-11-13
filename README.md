# Probabilistically Guided Genetic Programming for Automated Heuristic Design

Undergraduate dissertation project investigating whether genetic programming that learns which search operators combine well can discover higher-quality heuristics than an equivalent approach without learning.

## Overview

Heuristics are represented as programs in a strongly typed domain-specific language (DSL) of search operators—ensuring every evolved candidate is type-correct by construction. Rather than relying on blind crossover and mutation, the system maintains a probabilistic model over operator combinations and adapts how new candidates are generated.

## Architecture

1. **Typed DSL** — Primitive search operators whose types constrain which operators can legally be composed.
2. **Probabilistic Learning Graph** — A graph where nodes are DSL operators and weighted edges represent how well pairs of operators combine; weights are updated from search outcomes.
3. **Adaptive Search Loop** — Evaluates candidate programs, selects survivors, updates edge beliefs, and learns whether to graft survivors, mutate, or sample fresh programs from the graph.
4. **Decoupled Problem Domain** — Provides problem-specific operators and fitness evaluation independently of the DSL, graph, and search loop.
