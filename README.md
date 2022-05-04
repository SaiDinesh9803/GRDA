# Graph-Relational Domain Adaptation (GRDA)
This repo contains the code for our ICLR 2022 paper: "[Graph-Relational Domain Adaptation](wanghao.in/paper/ICLR22_GRDA.pdf)". We are still re-organizing the code for the camera-ready version.

## Beyond Domain Adaptation: Brief Introduction for GRDA
Essentially GRDA goes beyond current (categorical) domain adaptation regime and proposes the first approach to **adapt across graph-relational domains**. We introduce a new notion, dubbed "**domain graph**", that to encode domain adjacency, e.g., a graph of states in the US with each state as a domain and each edge indicating adjacency. Theoretical analysis shows that *at equilibrium, GRDA recovers classic domain adaptation when the graph is a clique, and achieves non-trivial alignment for other types of graphs*. See the following example (black nodes as source domains and white nodes as target domains).

<p align="center">
<img src="fig/GRDA-domain-graph-US.png" alt="" data-canonical-src="fig/GRDA-domain-graph-US.png" width="95%"/>
</p>

## Sample Results
In a DA problem with 15 domains connected by a domain graph (see the figure below), if we use domains 0, 3, 4, 8, 12, 14 as source domains (left of the following figure) and the rest as target domains, below are some sample results from previous domain adaptation methods and GRDA (right of the figure), where GRDA successfully generalizes across different domains in the graph.

<p align="center">
<img src="fig/GRDA-DG-15-results.png" alt="" data-canonical-src="fig/GRDA-DG-15-results.png" width="91%"/>
</p>

## Method Overview
We provide a simple yet effective learning framework with **theoretical guarantees** (see the [Theory section](https://github.com/Wang-ML-Lab/GRDA/edit/main/README.md#theory-informal) at the end of this README). Below is a quick comparison between previous domain adaptation methods and GRDA (differences marked in red). 
* Previous domain adaptation methods use a discriminator is classifify different domains (as categorical values), while GRDA's discriminator directly reconstructs the domain graph (as a adjacency matrix).
* Previous domain adaptation methods' encoders ignore domain IDs, while GRDA takes the domain IDs with the domain graph as input.
<p align="center">
<img src="fig/blog-method-DA-vs-GRDA.png" alt="" data-canonical-src="fig/blog-method-DA-vs-GRDA.png" width="95%"/>
</p>


## Installation
    pip install -r requirements.txt

## How to train
    python main.py

## Visualization
We use visdom to visualize. We assume the code is run on a remote gpu machine.

### Change config
Find the config in "config" folder. Choose the config you need and Set "opt.use_visdom" to "True".

### Start visdom server on gpu machine
    python -m visdom.server -p 2000
Now connect your computer with the gpu server and forward the port 2000 to your local computer. You can now go to:
    http://localhost:2000 (Your local address)
to see the visualization during training.

## Theory (Informal)
- Traditional DA is equivalent to using our GRDA with a fully-connected graph (i.e., a clique).
- D and E converge if and only if <img src="https://latex.codecogs.com/svg.image?E_{i,j}[A_{i,j}|e_i,e_j]&space;=&space;E_{i,j}[A_{i,j}]" />.
- The global optimum of the two-player game between E and D matches the three-player game between E, D, and F.

<!-- <img src="https://latex.codecogs.com/svg.image?E_{i,j}[A_{i,j}|e_i,e_j]&space;=&space;E_{i,j}[A_{i,j}]" /> -->

## Reference
If you find our work useful in your research, please consider citing:
```
@inproceedings{GRDA,
  title={Graph-Relational Domain Adaptation},
  author={Xu, Zihao and He, Hao and Lee, Guang-He and Wang, Yuyang and Wang, Hao},
  booktitle={International Conference on Learning Representations},
  year={2022}
}
```
