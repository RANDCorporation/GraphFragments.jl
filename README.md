# GraphFragments.jl

## Introduction

`GraphFragments.jl` implements the fragmentation metric introduced by [Borgatti](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=1149843). The package includes standard implementation, distance-based fragmentation, and serial and distributed approaches.


### Installation Notes

`GraphFragments.jl` depends on the following packages from the RAND repository, which must be added in the following order:

```
Pkg.add(url = "https://github.com/RANDCorporation/IterativeHeaps.jl")
Pkg.add(url = "https://github.com/RANDCorporation/GraphDistanceAlgorithms.jl")
```



## Use

The fragmentation of the graph can be calculated using the `fragmentation` function. This function will automatically try to run in parallel if the keyword argument `parallel_approach = true` (default) is set; this can be fixed to run serially if desired or in parallel (if a script is setup to automatically run in parallel). 

Fragmentation relies on the calculation of shortest paths across the graph from each starting node; if parallelized, the calculation will use synchronous data parallelization to distribute each source node on an available compute node. A dictionary of `DistributedArrays.DArray` objects for use by the distance algorithm can be passed using the `dict_arrays` argument, though the user should ensure these arrays match those necessary for the algorithm specificed by `distance_algorithm`. These arrays can include intermediate algorithmic vectors as well as any applicable heap cache arrays.

The user can access information about these arguments using the docstrings for `fragmentation` in Julia. 

```
fragmentation(
    graph::Union{AbstractGraph, Nothing}, 
    dict_arrays::Union{Dict{Symbol, Vector}, Dict{Symbol, DArray}, Nothing} = nothing;
    D_invs::Union{Matrix{Int64}, Matrix{Float64}, Nothing} = nothing,
    distance_algorithm::Symbol = :auto,
    parallel_approach::Symbol = :auto,
    use_distance_weighting::Bool = true,
    kwargs...
)
```

```
fragmentation(
    adj::Union{SparseMatrixCSC{Float64, Int64}, Matrix{Float64}};
    kwargs...
)
```



## Data

The code only needs a Graph to work off of. This can be loaded in a Julia session using `Graphs.jl`. If using `DiscreteGraphAlgorithms.jl`, then the `graph` property of a `GraphWrapper` can be used.



## Project information

This package is [one of five](https://github.com/RANDCorporation/black-knights-and-dark-network) created during the research phase of a RAND project.

In their report [_North Korea's Black Knights and Dark Network: Towards the Disruption and Typology of DPRK Sanctions Evasion Networks_ (RAND, RR-A3413-1)](https://www.rand.org/pubs/research_reports/RRA3413-1.html) researchers describe how they created a network representation of the DPRK sanctions-evasion system, comprising over 4,100 nodes and 6,500 links derived from UN Panel of Experts reports and the Center for Advanced Defense Studies (C4ADS) dataset. Together, the five code packages supported the team's ability to rank nodes and links, calculate priority scores, and compare the results to sanctioned entities, thus offering a rigorous, computationally driven approach to network disruption and target prioritization.

See the [parent repository](https://github.com/RANDCorporation/black-knights-and-dark-network) for a full list and additional details.


## References/Bibliography

Borgatti, Steve, The Key Player Problem (September 21, 2002). Available at SSRN: https://ssrn.com/abstract=1149843 or http://dx.doi.org/10.2139/ssrn.1149843

 

## Copyright and License

Copyright (C) <2025> RAND Corporation. This code is made available under the MIT license.

 

## Authors and Reference

James Syme, 2025.

```
@misc{GF2025,
  author       = {Syme, James},
  title        = {GraphFragments.jl: Distributed implementation of Key-Player Problem negative (KPP-Negative) metric.},
  year         = 2025,
  url          = {https://github.com/RANDCorporation/GraphFragments.jl}
}
