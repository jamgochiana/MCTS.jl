# MCTS

[![Documentation](https://img.shields.io/badge/docs-latest-blue.svg)](https://juliapomdp.github.io/MCTS.jl/latest)
[![Build Status](https://travis-ci.org/JuliaPOMDP/MCTS.jl.svg?branch=master)](https://travis-ci.org/JuliaPOMDP/MCTS.jl)
[![Coverage Status](https://coveralls.io/repos/github/JuliaPOMDP/MCTS.jl/badge.svg?branch=master)](https://coveralls.io/github/JuliaPOMDP/MCTS.jl?branch=master)

[![MCTS Tree for Grid World, visualized](https://github.com/JuliaPOMDP/MCTS.jl/raw/master/img/tree.png)](https://nbviewer.jupyter.org/github/JuliaPOMDP/MCTS.jl/blob/master/notebooks/Test_Visualization.ipynb)

This package implements the Monte-Carlo Tree Search algorithm in Julia for solving Markov decision processes (MDPs).
The user should define the problem according to the [generative interface](https://github.com/JuliaPOMDP/POMDPs.jl/blob/master/src/generative.jl) in [POMDPs.jl](https://github.com/JuliaPOMDP/POMDPs.jl). Examples of problem definitions can be found in [POMDPModels.jl](https://github.com/JuliaPOMDP/POMDPModels.jl). 

There is also a BeliefMCTSSolver that solves a POMDP by converting it to an MDP in the belief space.

Special thanks to Jon Cox for writing the original version of this code.

For reference, see the UCT algorithm in this paper:
Kocsis, Levente, and Csaba Szepesvári. "Bandit Based Monte-Carlo planning." European Conference on Machine Learning. Springer, Berlin, Heidelberg, 2006.

## Installation

In Julia, type, `]add MCTS`

## Documentation

Documentation can be found on the following site: [juliapomdp.github.io/MCTS.jl/latest/](http://juliapomdp.github.io/MCTS.jl/latest/)

## Usage

If `mdp` is an MDP defined with the [POMDPs.jl](https://github.com/sisl/POMDPs.jl) interface, the MCTS solver can be used to find an optimized action, `a`, for the MDP in state `s` as follows:

```julia
using POMDPs
using POMDPModels # for the SimpleGridWorld problem
using MCTS
using StaticArrays
mdp = SimpleGridWorld()
solver = MCTSSolver(n_iterations=50, depth=20, exploration_constant=5.0)
planner = solve(solver, mdp)
a = action(planner, SA[1,2])
```

See [this notebook](https://nbviewer.jupyter.org/github/JuliaPOMDP/MCTS.jl/blob/master/notebooks/Test_Visualization.ipynb) for an example of how to visualize the search tree.

See [this notebook](https://github.com/JuliaPOMDP/MCTS.jl/blob/master/notebooks/Domain_Knowledge_Example.ipynb) for examples of customizing solver behavior, specifically [the Rollouts section](https://github.com/JuliaPOMDP/MCTS.jl/blob/master/notebooks/Domain_Knowledge_Example.ipynb#Rollouts) for using heuristic rollout policies.
