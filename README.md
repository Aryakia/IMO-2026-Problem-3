# IMO 2026 Problem 3 — Stick-Cutting Game

A self-contained technical companion note for **Problem 3 of the 2026 International Mathematical Olympiad**, focused on the mathematical structure behind the game: pairing, exploitable symmetry, the optimal powers-of-two construction, and the guaranteed value of Player 1.

- Official problem page: https://www.imo-official.org/problems/
- Problem: IMO 2026, Problem 3
- Proposed by: Russian Federation

## Problem

Let $n$ be a positive integer. Player 1 first marks at most $n$ points on a stick of length $1$. Player 2 sees those marks and then marks at most $n$ additional points, all distinct from the earlier marks. The stick is cut at every marked point. The players then alternate claiming unclaimed pieces, with Player 1 choosing first. Each player wants to maximize the total length obtained.

For each $n$, determine the largest value $c_n$ that Player 1 can guarantee regardless of Player 2's play.

## Main result

The exact value is

```math
\boxed{c_n=\frac{2^n}{2^{n+1}-1}}.
```

Set

```math
\delta=\frac{1}{2^{n+1}-1}.
```

Then

```math
c_n=\frac{1+\delta}{2}.
```

Thus, under optimal play, the smallest advantage in total length that Player 1 can guarantee over Player 2 is exactly $\delta$.

## 1. The claiming stage

Suppose the final piece lengths, in non-increasing order, are

```math
x_1\ge x_2\ge\cdots\ge x_m>0.
```

The value of the claiming stage is exactly

```math
O=x_1+x_3+x_5+\cdots.
```

To see this, if Player 1 always takes a longest remaining piece, then before Player 1's $j$-th turn at most $2j-2$ pieces have been removed. Therefore at least one of the largest $2j-1$ original pieces is still available, so Player 1 receives a piece of length at least $x_{2j-1}$. Hence Player 1 can guarantee at least $O$.

Conversely, if Player 2 always takes a longest remaining piece, then before Player 2's $j$-th turn at most $2j-1$ pieces have been removed. Therefore Player 2 receives a piece of length at least $x_{2j}$. Player 2 can consequently guarantee at least

```math
E=x_2+x_4+x_6+\cdots,
```

leaving Player 1 at most $1-E=O$. Thus the value is exactly $O$.

Define the alternating gap

```math
A=x_1-x_2+x_3-x_4+\cdots,
```

where a missing final even-indexed term is interpreted as zero. Since $O+E=1$ and $O-E=A$,

```math
O=\frac{1+A}{2}.
```

The marking stage can therefore be viewed as a minimax problem over the final alternating gap $A$.

## 2. Player 2's basic idea: create counterparts

Player 2 benefits from symmetry. If the final pieces can be organized into equal pairs, Player 2 can answer each selection by Player 1 with its identical counterpart.

That produces an exact tie:

```math
\boxed{\frac12:\frac12}.
```

This immediately gives two simple failure modes for Player 1.

### Failure case 1: Player 1 creates too few pieces

If Player 1 creates at most $n$ initial pieces, Player 2 can bisect every one of them. For a piece of length $x$,

```math
x\longrightarrow \frac{x}{2}+\frac{x}{2}.
```

Every piece now has an identical counterpart, so Player 2 can force a tie.

### Failure case 2: Player 1 creates two equal pieces

Even if Player 1 uses all $n$ marks and creates $n+1$ pieces, two equal pieces are already enough to give Player 2 a complete pairing strategy.

Suppose two initial pieces have length

```math
x,\qquad x.
```

They already form one pair. At most $n-1$ other pieces remain. Player 2 can bisect each of those using at most $n-1$ cuts, producing equal pairs everywhere else.

Again Player 2 forces

```math
\boxed{\frac12:\frac12}.
```

The lesson is that Player 1 must avoid exploitable symmetry from the beginning.

## 3. Player 1's optimal construction

Player 1 chooses $n+1$ initial pieces proportional to successive powers of two:

```math
1,2,4,\ldots,2^n.
```

Let

```math
D=2^{n+1}-1.
```

The normalized piece lengths are

```math
\frac1D,\quad \frac2D,\quad \frac4D,\quad\ldots,\quad\frac{2^n}{D}.
```

They sum to one because

```math
1+2+4+\cdots+2^n=2^{n+1}-1=D.
```

This construction guarantees Player 1 at least

```math
\boxed{\frac{2^n}{2^{n+1}-1}}.
```

![Optimal initial cuts for n=1 and n=2](figures/optimal-initial-cuts.svg)

### Worked example: $n=1$

Player 1 begins with

```math
\frac13,\qquad\frac23.
```

If Player 2 does not cut, Player 1 simply takes $2/3$. If Player 2 bisects the larger piece,

```math
\frac23\longrightarrow\frac13+\frac13,
```

the three pieces are all $1/3$, and Player 1 still receives two of them. Hence

```math
\boxed{c_1=\frac23}.
```

This is the simplest example of a legal response that changes the board but gives Player 2 no improvement at all.

### Worked example: $n=2$

Player 1 begins with

```math
\frac47,\qquad\frac27,\qquad\frac17.
```

A natural response is to bisect the largest piece:

```math
\frac47\longrightarrow\frac27+\frac27.
```

If Player 2 stops there, the pieces are

```math
\frac27,\quad\frac27,\quad\frac27,\quad\frac17,
```

and Player 1 can secure $4/7$.

Player 2 still has another permitted cut. For example,

```math
\frac27\longrightarrow\frac17+\frac17.
```

The configuration changes again, but Player 1 can still secure

```math
\boxed{\frac47}.
```

The theorem below shows that no legal response can push Player 1 below this value.

## 4. Proof that Player 1 can guarantee the lower bound

Set

```math
\delta=\frac{1}{2^{n+1}-1}.
```

Player 1 creates the pieces

```math
\delta,2\delta,4\delta,\ldots,2^n\delta.
```

It is convenient to scale all lengths by $1/\delta$. We therefore work with the initial lengths

```math
1,2,4,\ldots,2^n.
```

Player 2 makes at most $n$ cuts, so there are at most $2n+1$ final pieces. Write their lengths in non-increasing order as

```math
x_1\ge x_2\ge\cdots\ge x_m>0.
```

Pair consecutive pieces:

```math
(x_1,x_2),(x_3,x_4),\ldots.
```

If $m$ is odd, append a single dummy piece of length $0$ and pair it with $x_m$.

Now construct a multigraph. There is one vertex for each of the $n+1$ original pieces $1,2,4,\ldots,2^n$. If a dummy zero was added, include one additional dummy vertex. Each adjacent pair of final pieces gives an edge joining the vertices corresponding to the original pieces from which those two final pieces came; in the odd case the final edge may join an original vertex to the dummy vertex.

If $m$ is even, the graph has $n+1$ vertices and $m/2\le n$ edges. If $m$ is odd, it has $n+2$ vertices and $(m+1)/2\le n+1$ edges. In either case the number of edges is strictly smaller than the number of vertices. Therefore at least one connected component is a tree.

Choose such a tree component and two-color it. Assign a coefficient $\lambda_i\in\{-1,+1\}$ to each original vertex in this tree according to its color, and set $\lambda_i=0$ for all original vertices outside the tree. If the dummy vertex lies in the tree, color it as well but give it numerical weight $0$.

Consider

```math
S=\sum_{i=0}^{n}\lambda_i2^i.
```

This integer is nonzero. If $j$ is the largest index for which $\lambda_j\ne0$, then

```math
|S|\ge 2^j-\sum_{i=0}^{j-1}2^i=1.
```

On the other hand, all final pieces originating from the original piece $2^i$ have total length $2^i$. Hence $S$ is also the signed sum of all final pieces, using the coefficient of their original vertex.

For every paired edge inside the chosen tree, the two endpoint coefficients are opposite, so that pair contributes either

```math
+(x_{2r-1}-x_{2r})
```

or

```math
-(x_{2r-1}-x_{2r}).
```

Pairs outside the chosen component contribute zero because both coefficients are zero. The same statement holds for the last pair $(x_m,0)$ if the dummy vertex is used. Therefore

```math
|S|\le (x_1-x_2)+(x_3-x_4)+\cdots=A.
```

Since $|S|\ge1$, we obtain

```math
A\ge1
```

at the scaled level. Returning to the original scale multiplies every length, and therefore $A$, by $\delta$. Thus

```math
A\ge\delta.
```

By the claiming-stage formula, Player 1 receives at least

```math
\frac{1+A}{2}\ge\frac{1+\delta}{2}=\frac{2^n}{2^{n+1}-1}.
```

This proves the lower bound.

## 5. Proof that Player 2 can hold Player 1 to the upper bound

Let Player 1 choose any initial partition.

If there are at most $n$ initial pieces, Player 2 bisects every piece and forces a tie. So only the case of exactly $n+1$ initial pieces remains.

Let their lengths be

```math
a_1,a_2,\ldots,a_{n+1},\qquad \sum_{i=1}^{n+1}a_i=1.
```

Consider all $2^{n+1}$ subset sums

```math
\sum_{i\in I}a_i,\qquad I\subseteq\{1,2,\ldots,n+1\}.
```

They all lie in $[0,1]$. Arrange these subset sums in non-decreasing order. Among the $2^{n+1}-1$ consecutive gaps, at least one has size at most

```math
\delta=\frac{1}{2^{n+1}-1}.
```

Choose two distinct subsets realizing such a gap. Remove all indices common to both subsets. This leaves disjoint subsets $P$ and $Q$ satisfying, after interchanging them if necessary,

```math
0\le \sum_{i\in P}a_i-\sum_{j\in Q}a_j\le\delta.
```

Write

```math
p=\sum_{i\in P}a_i,\qquad q=\sum_{j\in Q}a_j,
```

so that $0\le p-q\le\delta$.

If $Q$ is empty, then $p\le\delta$. Player 2 leaves the pieces in $P$ as the residual part and bisects every piece outside $P$. Since $P$ is nonempty, this uses at most $n$ cuts. All non-residual pieces are now paired, while the total residual length is at most $\delta$.

Now suppose both $P$ and $Q$ are nonempty. Player 2 refines the pieces from these two families into matched equal segments. Repeatedly compare one currently unpaired piece from each family:

- if their lengths are equal, pair them and remove both from the comparison;
- if one is longer, cut the longer one so that one new part equals the shorter piece, pair those equal parts, and return only the leftover remainder to its family.

If $r=|P|+|Q|$, this procedure requires at most $r-1$ cuts: each cut completely exhausts at least one currently active original piece from the matching process. When the shorter-total family is exhausted, the total unmatched remainder is exactly

```math
R=p-q\le\delta.
```

Player 2 then bisects every original piece outside $P\cup Q$. There are $n+1-r$ such pieces, so the total number of cuts is at most

```math
(r-1)+(n+1-r)=n.
```

Thus, in all cases, every final piece can be placed into an equal pair except for residual pieces whose total length is some $R\le\delta$.

During the claiming stage, Player 2 can secure one member of every equal pair: whenever Player 1 takes one member of an untouched pair, Player 2 takes its mate; if Player 1 instead takes a residual piece, Player 2 can take one member of any untouched pair. Therefore Player 1 receives at most one half of the paired mass plus all of the residual mass:

```math
\frac{1-R}{2}+R=\frac{1+R}{2}\le\frac{1+\delta}{2}=\frac{2^n}{2^{n+1}-1}.
```

This proves the upper bound. Since the lower and upper bounds coincide,

```math
\boxed{c_n=\frac{2^n}{2^{n+1}-1}}.
```

## 6. A small but useful corollary: one permitted cut has no additional value

The $n=1$ example already shows the idea clearly. Player 2 may use the available cut or leave it unused; either way Player 1 receives $2/3$. The cut is legal, but it provides no improvement.

There is also a general version of this observation. Against Player 1's optimal powers-of-two construction, Player 2 can already attain the minimax upper bound using at most $n-1$ cuts.

For $n\ge2$, Player 2 bisects each original piece

```math
2^k\delta\qquad (k=2,3,\ldots,n).
```

This uses exactly $n-1$ cuts. The resulting multiset contains equal pairs at every level from $2^{n-1}\delta$ down to $4\delta$, followed by the tail

```math
2\delta,\quad2\delta,\quad2\delta,\quad\delta.
```

All equal pairs cancel in the alternating gap, and the tail contributes

```math
2\delta-2\delta+2\delta-\delta=\delta.
```

Hence Player 1's share is exactly

```math
\frac{1+\delta}{2}=\frac{2^n}{2^{n+1}-1}.
```

For $n=1$, the same conclusion is reached with zero cuts.

So Player 2 does not need the full cut budget to achieve the best possible response against Player 1's optimal construction. In that precise minimax sense, **at least one of Player 2's permitted cuts has no additional strategic value**.

## 7. Strategic interpretation

The game contains two complementary mechanisms:

1. **Player 2 seeks counterparts.** Symmetry allows Player 2 to answer one move with an equivalent move and push the allocation toward parity.
2. **Player 1 anticipates the response.** The powers-of-two construction is chosen so that Player 2's best refinement cannot erase Player 1's guaranteed advantage.

The final corollary sharpens the second point. A robust opening does not necessarily eliminate the opponent's legal options. It can instead make part of the opponent's available action space strategically redundant.

This is why the problem is useful as a simple model of robust strategic design: the quality of an opening move depends not only on its immediate effect, but on how well it survives the opponent's strongest response.

## References

- International Mathematical Olympiad, official problems: https://www.imo-official.org/problems/
- Art of Problem Solving, IMO 2026 Problem 3: https://artofproblemsolving.com/wiki/index.php?title=2026_IMO_Problems/Problem_3
- Dragomir Grozev, *IMO 2026, Problem 3, and Beyond*: https://dgrozev.wordpress.com/2026/08/13/imo-2026-problem-3-and-beyond/

## Notes

This repository is intended as a transparent mathematical companion to a broader essay on asymmetric strategy. The political interpretation is separate from the proof above; the mathematical claims stand independently of that interpretation.
