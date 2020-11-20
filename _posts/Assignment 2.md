Auto-balanced Force-Directed Visualization
------------------------------------------

Haoning Wu, Jingcheng Zhang, as an **Report of Assignment 2 of VisClass**



### Methodology: Push and Pull like Magnetics?

To first solve with the auto-balance force-directed algorithm, we need to understand the pseudo code of it. However, most of the existing publications has shown too complicated pseudo code which on the contrary becomes a burden for implementing this mechanism.



We categorize the **kernel mechanism** of the method as follows:

```pseudocode
define Force-Directed (Nodes, Edges):
	1. GENRERATE A RANDOM DISTRIBUTION on the position of the Nodes.
	2. RUN iterations below:
		2.1. CALCULATE the REPULSION between the points, get the accumulated Repulsive Force given by all other points.
		2.2. CALCULATE the REPULSION between the points, get the accumulated Repulsive Force given by all CONNECTED points.
	
```



This mechanism seems like a differential process in physics: every iteration looked like a fairly small time interval when both **repulsive** and **traction** forces are applied to each nodes lying in their current 'unstable' position. When the repulsive and traction forces get stable for each nodes, the iterative method converges.



This method is easy discribed than formally implemented because the balance point we need does not have a **simple criterion** because it is a visualization problem rather than a fixed-goal optimization problem. We will then propose two ways in realizing for our specified problem after analyzing the characteristics of the data source.



### What does the data contain?

The data contains the following two lists:

A. Nodes: a list of objects representing colleges from the class **Nodes**, which includes the following attributes:

1. ID: Name of the colleges, a string.
2. Weight: The rank index of a college, a float, indicating how brilliant the college is.
3. \[X, Y\]: position of the college on our visualized graph.

B. Lists: a list of objecgs representing college connections from the class **Lists**, which includes the following attributes:

1. Source, Target: Name of the colleges that are included in the connection, each is a string.
2. Weight: How much the connection weighs, a float, indicating the total Ph.D. to faculty flow between colleges.



We will need to build a force-directed map, diversing the two forces and the final distance within the float number shown above (also we could make some tricks on point colors and point scale, but they are minor practices).



The algorithms with the Plus edition of both of them are shown **together with the visualized results and analysis.**



Before seeing the well-organized Force-Directed Versions, let's first see some failures on the unoptimized editions of the Force-Directed Versions:

![截圖 2020-11-17 上午1.25.43](/Users/realtimothyhwu/Library/Application Support/typora-user-images/截圖 2020-11-17 上午1.25.43.png)

1: Too large balance distance......without careful consideration on how to organize the gravity...

![截圖 2020-11-17 上午1.31.08](/Users/realtimothyhwu/Library/Application Support/typora-user-images/截圖 2020-11-17 上午1.31.08.png)

2. More severely, distance overflow can lead to the thing shown above.

### Algorithm: the Spring algorithm

`NotImplemented`

The Spring algorithm shows the following principle and assumptions: *suppose the points are all connected with springs, so the balance distance between points should be fixed and only relevant to the data point's characteristics.* If the points are deviated from the `balance distance', then the **punishment term ($P_s$)** is defined as follows.

$$ P_s = K (d - d^*) $$

And the $d^*$ is defined with the following hyper-parameters:

$$ d^*_{i,j} = k_s * w_iw_j/w_{ij}^2 $$, for the basic idea that large weight circle should be kept further unless strongly connected.

The $k_s$ is a hyperparamter, normalized in the following way:

$k_s = \text{dist_lim} * i * j /（\sum_{i,j} w_iw_j/w_{ij}^2)$.

The realization result is as follows:



### Algorithm 2: Spring-Column algorithm

In the Spring-Column algorithm, the traction is still punished by the deviation from the 'balanced distance', but the repulsion force is defined by the column repulsion (or gravitional force, in reverse way), which is defined as follows:

$$ F_{r} = k_r w_iw_j / d^2$$

$$ F_t = k_t (d - d^*) $$

And the definition of $d^*$ is the same as algorithm 1.

The realization result is as follows:



We will use the second algorithm.

### Algorithm^+^: Force as second derivative of distance

`NotImplemented`







### 