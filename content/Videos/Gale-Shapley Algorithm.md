
## Stable Marriage/Matching Problem

#### Objective
Identify a **perfect** and **stable** matching between two equally sized sets. 

> [!NOTE] Perfect
> Everyone in each group has exactly one partner in the opposite group.
> 

> [!NOTE] Stable
> No pair of individuals mutually prefers one another over the person they are paired with.

#### Algorithmic Solution (Gale-Shapley Algorithm)
The most popular solution, proposed by Gale and Shapley in 1962 (and which won a Nobel prize in 2012 for its applications), goes as follows:

There are $n$ members of group $A$ (men) and that same number $n$ in group $B$ (women). Each member has a list ranking their preferences for each member of the other group. Group $A$ will serve as the **proposers** and group $B$ as **acceptors**. 

In the first round, the members of group $A$ send out a proposal to their top choice in group $B$ and the members in group $B$ who received proposals have the choice to either:
- Reject the proposal
- Provisionally accept the proposal
Then, in the second round, the still unpaired members of group $A$ send out proposals to their second ranked choice among members of group $B$. Once again, members of group $B$ have the choice to either reject or provisionally accept the proposal, but now they have the additional option to leave their previously provisionally accepted proposal in favor of the new one. 

This continues until the unpaired individuals in group $A$ have sent out proposals to everyone, by order of decreasing preference.

##### The End Result
A perfect and stable matching is achieved in $O(n^2)$. Everyone has a partner and nobody mutually prefers to be with another member of the opposite group than their partner. But there is a catch. This algorithm guarantees the *best possible* outcome for members of group $A$ (proposers) and the *worst possible* outcome for members of group $B$ (acceptors).

So now the pertinent question is *"how do we make this algorithm fair?"* Which leaves us with a new problem:
## The Equitable Stable Marriage Problem (ESMP)

#### Objective
- A **perfect** and **stable** matching like in the Stable Marriage Problem.
- Members from both groups now must be **equally satisfied**, which results in this problem now being strongly **NP-hard**[^1]. See [[Gale-Shapley Algorithm#^cae7ac|aside on complexity classes]] for more information on this. 

As a measure of equity, we may employ the *sex equality cost* (see [[Gale-Shapley Algorithm#^eed6f6|[2]]]), which measures the gap between the two sides' average obtained preference:
$$
d(M)=\left|\sum_{(m,w)\in M} pr_{m}(w) - \sum_{(m,w)\in M} pr_{w}(m)\right|
$$
where $pr_{m}(w)$ denotes the position of the woman $w$ in a man $m$'s preference list (and vice versa).

There are several algorithms that can solve this problem, but they each have different trade offs. Many enter cyclical loops and have no guarantee of termination. I will describe one of the more promising ones below.
%%

|                            | SML2         | SWING    | ESMA  | DACC     | GS       | LDS      | EDS      | PDB      |
| -------------------------- | ------------ | -------- | ----- | -------- | -------- | -------- | -------- | -------- |
| Guaranteed <br>Termination | Yes          | No       | No    | Yes      | Yes      | -        | -        | -        |
| Complexity                 | $O(n\log n)$ | $O(n^2)$ | -     | $O(n^4)$ | $O(n^2)$ | $O(n^3)$ | $O(n^3)$ | $O(n^3)$ |
| Fair                       | Yes          | Yes      | Yes   | Yes      | No       |          |          |          |
| Endless <br>Cycles         | Maybe        |          | Maybe | No       |          |          |          |          |
%%
%%%#### Algorithmic Solution Attempt I: ESMA



%> [!NOTE] Stability Theorem
%> If the algorithm terminates, it finds a stable matching.%

##### The End Result
The groups are now equally satisfied, however, because the groups alternate in their roles, monotonicity is lost, which introduces issues with termination and stability. 

##### Properties
- Complex indexing needed for preference list
- Not monotonic
- Termination condition from gale shapley (everyone married) does not guarantee stability
#### SML2

Iteratively eliminates selected blocking pairs%%%
#### Algorithmic Solution Best Attempt: DACC
In 2016, Dworczak proposed an algorithm: **Deferred Acceptance with Compensation Chains (DACC)**, which is, so far, the only *fair* procedure proven to terminate. It does so in $O(n^4)$, by following an arbitrary sequence of proposals from both sides of the market, so like ESMA, it is not monotonic.

Funny enough, if only one side of the market makes offers, this algorithm reduces to Gale-Shapley! This algorithm can also be used to solve the "Stable Roommate Problem".

It works as follows:
Both men and women make offers in some pre-specified order which we will call $\Phi$.
###### But what is a compensation chain?
I say that $i$ **deceived** $j$ if $i$ divorced $j$,(who $i$ proposed to in the past themselves). We now introduce a rule that when someone is deceived, they will be **compensated**. That is, they are now able to make an offer in the current round regardless of the order $\Phi$. Now if $j$ is accepted by $k$, who by doing so deceives $k$'s current match $\mu(k)$, then $\mu(k)$ is compensated (allowed to propose next). This chain of compensation ends when the last person in the chain exhausts his or her **budget set**, or is accepted by agent $l$ who does not deceive $\mu(l)$ (for example, he/she is single). Only then does the algorithm proceed to the next round, and the proposer is determined by the original order $\Phi$. 

> [!NOTE] Budget Set
> Defined by Dworczak as follows:
> 
> *Whenever $i$ proposes to $j$, we add $i$ to $j$'s budget set $B_j$. Whenever $i$ is rejected or divorced by $j$, we remove $j$ from $i$'s budget set $B_i$.*

Every compensation chain is proven to stop in finite time. This differs from McVitie and Wilson's algorithm as only deceptions trigger compensation chains in DACC, as opposed to every rejection and divorce, so this algorithm generates all stable matchings (unlike McVitie and Wilson's)!
##### The End Result
For *any* pre-specified order of proposal turns $\Phi$, DACC stops in finite time (1) and its outcome is stable (2). Furthermore, for any stable outcome, there is an initial ordering $\Phi$ such that this outcome can be achieved without compensation chains. Every stable matching can be achieved by an algorithm from the DACC class (3), in fact. 

The two obvious simplifications of this algorithm (one of which being the Gale-Shapley Algorithm) in Dworczak's paper lack all three of these important properties at once. 
### Aside on complexity classes (optional)

^cae7ac

A complexity class (such as "NP-hard") is a set of computational problems (ie. decision problems, function problems, counting problems, optimization problems, etc.) of "related resource-based complexity". In general, a computational problem is simply a question that can be solved by an algorithm.

The following classes are listed in increasing order of complexity. The first, and least complex is $P$, which can be defined as such:

> [!NOTE] P (complexity class)
> The set of all decision problems that can be **solved** in polynomial time.

Note that a decision problem a problem with a "yes" or "no" answer. 

> [!NOTE] NP (complexity class)
> The set of all decision problems for which the instances where the answer is "yes" have proofs that can be **verified** in polynomial time.

There is a distinction drawn here between *solving* a decision problem and *verifying* the solution. 

> [!NOTE] NP-complete (complexity class)
> The set of all problems $X$ in NP for which it is possible to reduce any other NP problem $Y$ (as described above) to $X$ in polynomial time.

> [!NOTE] NP-Hard (complexity class)
> If a problem $X$ is NP-hard, there exists an NP-complete problem $Y$ s.t. $Y$ is reducible to $X$ in polynomial time (ex. the Halting Problem). 
> 
> **Intuitively, you can think of these as being at least as hard as the hardest problems in NP, and at least as hard as the NP-complete problems.**

*Note: NP-hard problems do not have to be in NP (that is, we may or may not be able to verify the solution to these problems in polynomial time), and they do not have to be decision problems. The Halting Problem, for example, is an NP-hard decision problem that is not in NP.*

In our case, it is important to note that the decision problem for **the classical Stable Matching Problem "does a stable matching exist" is trivially in $P$, as the Gale-Shapley algorithm solves it in $O(n^2)$**. The "Stable Roommate Problem" (where all participants now belong to the same pool) is also in $P$, when the same question is asked. Spoiler: a stable matching does not always exist!


[^1]: NP-hardness is a complicated enough thing that it warrants a video on its own. To read more about this for now, I suggest this paper: https://ocw.mit.edu/courses/6-046j-design-and-analysis-of-algorithms-spring-2012/f53967be74f440c4855f9472dff28a63_MIT6.046J_S12_rec10.pdf

***
### Resources

**\[1\]** [Stable Allocations And The Practice Of Market Design]( https://www.nobelprize.org/uploads/2018/06/advanced-economicsciences2012.pdf) *compiled by the Economic Sciences Prize Committee of the Royal Swedish Academy of Sciences*
**\[2\]** [Fair Procedures for Fair Stable Marriage Outcomes](https://ojs.aaai.org/index.php/AAAI/article/download/6218/6074) *Northeastern University, National Technical University of Athens*
**\[3\]** [Hard Variants of Stable Marriage](https://www.dcs.gla.ac.uk/~davidm/pubs/TR-1999-43.pdf) *Computing Science Department, University of Glasgow; School of Informatics, Kyoto University*
**\[4\]** [An Equitable Solution to the Stable Marriage Problem](https://www.cslab.ece.ntua.gr/~ggian/files/presentations/ictai15_presentation.pdf) *Computing Systems Laboratory, National Technical University of Athens, Greece*
\[5\] [The Stable Marriage Problem](https://dl.acm.org/doi/10.1145/362619.362631) *McVitie and Wilson* ^eed6f6
\[6\] [Deferred Acceptance with Compensation Chains](https://bpb-us-e1.wpmucdn.com/sites.northwestern.edu/dist/1/2465/files/2018/07/DACC-EC-169707u.pdf) *Stanford University, Graduate School of Business*
**\[7\]** [Local Search Approaches in Stable Matching Problems](https://www.mdpi.com/1999-4893/6/4/591) *Mirco Gelain, University of Padova*
