This explains how the actual code is going to be roughly structure - this is only provisional as it could change depending on how the project evolves.

As of 20 Oct 2026 this is the structure:
- **The [[DSL]]:** syntax, types and interpreter. It defines which programs are possible, and its types fix which edges the graph can have.
- **The [[Learning Graph]]:** the learned beliefs about which combinations of operators work.
- **The [[Search Loop]]:** builds candidate programs from the graph, applies crossover and mutation, evaluates them, and updates the graph.
- **The problem domain:** primitives plus a fitness function. This is easy to forget, but it’s what candidate programs are scored against, and keeping it separate is what lets you swap problems later.

So it should sit into a nice flow similar to:
```
  ┌────────────────────▶ graph
  │                        │ sample
  │                        ▼
  │               candidate programs ◀───┐
  │                        │ run via DSL │
  │                        ▼             │
  │                     problem          │
  │                        │             │
  │                        ▼             │
  │                     fitness          │
  │                        │             │
  │                        ▼             │
  └─ update beliefs ◀─ selection         │
                           │             │
                           ▼             │
                       survivors         │
                           │             │
                           ▼             │
                   genetic operators ────┘
```
For any given step the program should follow the following flow:
1. [[Population Initialisation]] - Generate an initial population of syntax trees representing potential heuristics
2. [[Genetic Operators]] - Apply some genetic operators to the candidate population of syntax trees
3. Use [[Compiler]] - convert each candidate syntax tree into a runnable program (some defined type)
4. [[Candidate Evaluation]] - use a given fitness function to evaluate each compiled candidate
5. [[Survivor Selection]] - From the evaluated candidates select survivors
6. [[Graph Update]] - update the graph for generating fresh candidate syntax trees
7. [[Population Regeneration]] - Generate a new initial