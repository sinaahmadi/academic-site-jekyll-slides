---
title: Modified Adsorption Analysis for Translation Inference
description: 
theme: white
---

<script type="text/javascript"
    src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML">
</script>

### Adsorption algorithm
#### Preliminaries
#### Random-walk view
#### Averaging view 
### Modified Adsorption algorithm
#### References
---


## Adsorption algorithm

Adsorption is a general algorithm framework for transductive learning where the learner is given a small set of labelled examples and large set of unlablled examples. 

**Goal**: Label all the unlabelled examples and also, relabel the labelled examples. 

---
## Preliminaries 

<!-- <section>
	\[\begin{aligned}
	 \\
	\\
	\\
	
	\end{aligned} \]
</section> -->

$$G = (V, E, W)$$  
$$v \in V, e = (a, b) \in V \times V $$  
$$W_{ab} \in \mathbb{R}_+ $$  
$$n = |V|$$  
$$n_l$$: number of examples for which we have prior knowledge.
$$n_u$$: number of examples to be labelled. 
$$n = n_l + n_u$$  
$$\mathcal{L} = \{1...m\}$$: set of the possible labels  
$$m = |\mathcal{L}|$$

~~


Each instance $$v \in V$$ is associated with $$Y_v, \hat{Y}_v \in \mathbb{R}_+^m$$:

$$
Y_v=
  \begin{bmatrix}
    Y_{v0} & ... & Y_{vl} & ... & Y_{vm}
  \end{bmatrix}
$$ prior knowledge

$$
\hat{Y}_v=
  \begin{bmatrix}
    \hat{Y}_{v0} & ... & \hat{Y}_{vl} & ... & \hat{Y}_{vm}
  \end{bmatrix}
$$ output of the algorithm


$$Y, \hat{Y} \in \mathbb{R}_+^{n \times m}$$: the matrices whose rows are $$Y_v, \hat{Y}_v$$ respectively.

$$0_d$$: all-zeros row vector of dimension $$d$$.


--- 

## Random-walk view

The adsorption algorithm can be viewed as a *controlled* random walk (RW) over $$G$$ formalized via three actions:

- *inject* ($$inj$$) with predefined probability $$p_v^{inj}$$ 
- *continue* ($$cont$$): with predefined probability $$p_v^{cont}$$
- *abandon* ($$abnd$$): with predefined probability $$p_v^{abnd}$$

$$p_v^{inj}, p_v^{cont}, p_v^{abnd} \geq 0$$ per vertex $$v \in V$$.
$$p_v^{inj} + p_v^{cont} + p_v^{abnd} = 1$$ 

~~

To label any vertex $$v \in V$$, we initiate a random-walk starting at $$v$$ facing three options:

- with $$p_v^{inj}$$, RW stops and return $$Y_v$$(i.e. *inject*)
- with $$p_v^{cont}$$, RW *abandons* the labelling process and return $$0_d$$
- with $$p_v^{abnd}$$, RW *continues* to one of $$v$$'s neighbours $$v'$$ with probability proportional to $$W_{v'v} \geq 0$$

For unlabelled examples, $$p_v^{inj} = 0$$.

By definition, $$W_{v'v} = 0$$ if $$(v, v')  \notin  E$$.

~~

### In summary:

<section>
$$
Pr[v' | v] = \left\{\begin{matrix}
\frac{W_{v'v}}{\sum_{u : (u, v) \in E}W_{uv}} & (v', v) \in E\\ 
0 & \text{otherwise}
\end{matrix}\right.
$$
</section>

$$\hat{Y}_v$$ for node $$v \in V$$ is given by:

<section>
$$\hat{Y}_v = p_v^{inj} \times Y_v + p_v^{cont} \times \sum_{v' : (v', v) \in E} Pr[v' | v] \hat{Y}_{v'} + p_v^{abnd} \times 0_m $$
</section>

<!-- <script type="math/tex; mode=display">
	\left( \sum_{k=1}^n a_k b_k \right)^2 \leq \left( \sum_{k=1}^n a_k^2 \right) \left( \sum_{k=1}^n b_k^2 \right)
</script> -->

~~

## Averaging view 

Encoding ignorance about the correct label by using a dummy variable $$\mathtt{v} \notin \mathcal{L}$$, so $$Y_v, \hat{Y}_v \in \mathbb{R}_+^{m + 1}$$

If the RW is abandoned, then the corresponding labelling vector is zero for all true labels in $$\mathcal{L}$$, and an arbitrary value of unit for $$\mathtt{v}$$
- A-priori no vertex is associated with $$\mathtt{v}$$, so $$Y_{\mathtt{v}v} = 0 $$
- Replace $$0_m$$ with $$r \in \mathbb{R}_+^{m + 1}$$ where $$r_l = 0$$ for $$l \neq \mathtt{v}$$ and $$r_\mathtt{v} = 1$$.

~~

### Initialization (based on <a href="#ref1">[1]</a>)

<p align="center">
$$p_v^{cont} \propto c_v$$ $$p_v^{inj} \propto d_v$$
</p>

- $$c_v \in [0, 1]$$ is monotonically decreasing with the number of neighbours for node $$v$$ in $$G$$
- $$d_v \geq 0$$ is monotonically increasing with the entropy

~~

$$p_v^{cont} = \frac{c_v}{z_v}$$ ; $$p_v^{inj} = \frac{d_v}{z_v}$$ ; $$p_v^{abnd} = 1 - p_v^{cont} - p_v^{inj}$$

<div style="border:1px solid #000;">

<!-- We first compute the entropy of the transition probabilities for each node: -->

$$ H[v] = - \sum_u \text{Pr}[u|v]\text{log Pr}[u|v]$$
$$f(x) = \frac{\text{log} \beta}{\text{log}(\beta + e^x)}$$
$$c_v = f(H[v])$$
$$
d_v = \left\{\begin{matrix}
(1-c_v) \times \sqrt{H[v]} & \text{the vertex v is labelled}\\ 
0 & \text{the vertex v is unlabelled}
\end{matrix}\right.
$$
$$z_v = \text{max}(c_v + d_v, 1)$$
$$\beta = 2$$

</div>

~~
## Objective function

![adsorption algorithm](../../imgs/adsorption_algorithm.png)

~~

The adsorption algorithm minimizes some objective function <i>Q</i>. Talukdar et al. <a href="#ref1">[1]</a> prove that:

<blockquote>
  <p>There does not exist a function <i>Q</i> with continuous second partial derivatives such that the Adsorption algorithm converges when gradient of <i>Q</i> is equal to 1. </p>
</blockquote>


<font color="green"><b>There is no <i>Q</i> such that its local optimal would be the output of the adsorption algorithm.</b></font>

---

## Modified Adsorption algorithm (MAD)

An objective requiring:

1. $$Y_u \approx \hat{Y}_v$$
2. $$\hat{Y}_u \approx \hat{Y}_v$$, if $$W_{uv}$$ is large
3. $$\hat{Y}_v \approx r$$

~~

### Redefining matrices

$$W'_{vu} = p_v^{cont} \times W_{vu}$$


~~

![adsorption algorithm](../../imgs/modified_adsorption_algorithm.png)

~~

$$
\mathop{\text{arg min}}_{\hat{Y}} \sum_{l=1}^{m+1} 
\begin{bmatrix}
|| S\hat{Y}_l - SY_l||^2 + \mu_1 \sum_{u, v} M_{uv} (\hat{Y}_{ul} - \hat{Y}_{vl})^2 \\ 
+ \mu_2|| \hat{Y}_l - R_l||^2
\end{bmatrix}
$$

- $$m$$ labels, +1 dummy label
- $$M= W'^T + W'$$ is the symmetrized weight matrix
- $$\hat{Y}_{vl}$$: weight of label $$l$$ on node $$v$$
- $$Y_{vl}$$: seed weight of label $$l$$ on node $$v$$
- $$S$$: diagonal matrix, non-zero for seed nodes
- $$R_{vl}$$: regularization target for label $$l$$ on node $$v$$



---
## References

<p id="ref1">Talukdar, Partha Pratim, and Koby Crammer. "New regularized algorithms for transductive learning." Joint European Conference on Machine Learning and Knowledge Discovery in Databases. Springer, Berlin, Heidelberg, 2009.</p>










