
What does Hinge's "most compatible" feature, organ donation networks and doctor-residency matching have in common?

They all essentially use the same algorithm. 

It's called the Gale-Shapley algorithm, and it won the economics Nobel prize in 2012 for its applications. 

It was originally introduced as a solution to the "stable marriage problem" in 1962, where you have a group of men and a group of women, and you want to create a perfect and stable matching between them. 

Perfect meaning that everyone in each group has exactly one partner in the opposite group, and stable meaning that no pair of individuals mutually prefers one another over the person they're paired with.

Their algorithm goes as follows:

Each person has a list ranking their preferences for each member of the other group. Group $A$ (the men) will serve as the **proposers** and group $B$ as **acceptors** (the women_. 

In the first round, the members of group $A$ send out a proposal to their top choice in group $B$ and the members in group $B$ who received proposals have the choice to either:
- Reject the proposal
- Provisionally accept the proposal

Then, in the second round, the still unpaired members of group $A$ send out proposals to their second ranked choice among members of group $B$. Once again, members of group $B$ have the choice to either reject or provisionally accept the proposal, but now they have the additional option to leave their previously provisionally accepted proposal in favor of the new one. 

This continues until the unpaired individuals in group $A$ have sent out proposals to everyone, by order of decreasing preference.

The end result is that a perfect and stable matching is achieved in $O(n^2)$. Everyone has a partner and nobody mutually prefers to be with another member of the opposite group than their partner. But there is a catch. This algorithm guarantees the *best possible* outcome for members of group $A$ (proposers) and the *worst possible* outcome for members of group $B$ (acceptors).

So now the pertinent question is *"how do we make this algorithm fair?"* Which leaves us with a new problem:

The Equitable Stable Marriage Problem (ESMP)

The objective is now not only a perfect and stable matching like in the Stable Marriage Problem, bot for members from both groups to be equally satisfied. This results in this problem now not only being hard, but NP-hard.
