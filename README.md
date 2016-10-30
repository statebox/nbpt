# NANO BIPARTITE

> minimalist encoding of bipartite graphs

Say we have a bipartite graph with partitions *N* and *J*.

Let the *J-boundary* of a J-vertex be its (directly) adjacent N-vertices.

Suppose we label our nodes in the N partition starting from the number 1.

The boundary is now a list of numbers bigger than zero.

To encode the graph now, join all J-boundary lists with 0's interspersed
to denote the next J-vertex.

We now encoded a bipartite graph as a sequence of numbers.

### size of encoding

size = k * (edges + vertices)

## directed vs undirected

In the directed case we split the adjectent vertices into two lists

- lowercase, the incoming arcs
- and uppercase, the outgoing arcs.

We alternate by listing the incoming and then the outgoing arc
of each J-vertex.

> a0 a1 split A0 A1 A2 split b0 split B0 B1 split split C0

The directed case **Always** has an uneven nr of splits.

#### Undirected

We ensure **Always** even nr of splits.

This works out as above if the N-partition has an
*uneven nr of vertices*:

> a0 a1 split b0 split c0 c1

Is this not the case, we add an extra split at the end.

> a0 a1 split b0 split c0 c1 split d0 split

Voila.

## integer weighted arcs

by simply repeating the identifier of a vertex in N the weight
is increased. For low weights this is efficient.

An edge with a very high weight would be expensive.

run length encoding can be applied to resolve this

## sequentiality

we have further information in this encoding, namely, the
ordering of `a0 a1 a2`.
