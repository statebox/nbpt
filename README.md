# NANO BIPARTITE

> minimalist encoding of various graph-like structures

Central idea: use a list of numbers and denote `0` as
a separator symbol.

Depending on the number of zeros in
a list of numbers, we encode a different structure.

| Number of zeros  | Encoded Structure          |
|------------------|----------------------------|
| 0                | Multiset                   |
| 1                | Pair of multisets          |
| 2 (at the start) | Directed graph             |
| 3 + 2k           | Undirected bipartite graph |
| 4 + 2k           | Directed bipartite graph   |

#### Multisets

Multisets over some finite set (1...n).

> e0 e0 e1 e2 e2 e2 e4

This describes a multiset with four elements (e0, e1, e2, e4)
and the multiplicity of an element is the number of times
it occurs in the set.

#### Transition

This is just two multisets separated by a zero

> e0 e1 e1 `0` f3 f4 f4

#### Directed graph

A directed graph is given as an arc list,
alternating between the source and target of the arc.

> `00` s0 d0 s1 d1 s2 d2

It starts with two zeros.

#### Undirected bipartite graph

We define one partition `A` by pointing to the other partition `B`. Every partition-element in `A` is a multiset over `B` and
they are separated by a zeros.

> p0 p1 p2 p2 `0` q0 q1 `0` r0 r0 (`0`)

The last zero is only added if this makes the number of zeros uneven `3 + 2k`. If there is only on or two elements in the `A`
parition, zeros are added to the end until there are at least three zeros.

> p0 p1 `000`

> p0 `0` q0 `00`

#### Direct bipartite graph

The same idea as in the undirected case, except now every partition element is a pair of multisets, separated by a zero.

> s0 s1 s1 `0` S2 S3 `0`

Again if the number of zeros are less than `4` the list should
be have zeros postfixed to it.

> s0 `0000`

> `0` S0 `000`

> s0 `0` S0 `000`

> s0 `0` S0 `0` t1 t1 t2 `0` T4 `0`


## Notes

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
