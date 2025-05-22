# Let's verify step by step

Comparison of ORM vs PRM
ORM can be obtained without supervision, since you just need to check the final answer.
PRM requires supervision for each intermediate step.
According to their results PRM performs better than ORM.

## Data Collection

They labelled each step of MATH problems with positive, negative, neutral.
A neutral label indicates ambiguity.
Final created dataset [PRM800K](https://github.com/openai/prm800k), 800K steps-level labels across 75K solutions to 12K problems.
They included 4.5K math test problems in the training set, that's why they test only on MATH500.

## ORM

Trained using sam emethods as Cobbe 2021. Generate fixed number of solutions per problem, train ORM to predicted whether each soliution
is correct or incorret. Use ORM's prediction at the final token as the overlall oscore for the solution. ORM has a major problem
false positives, solutions that reach the correct answer with incorrect reasoning.

## PRM

PRMs are trained to predict the correctness of each step after the last token in each step. Maximize the log-likelihood of the these token during training. To determing the step-level predictions at test time, it suffices to perform a  single PRM forward pass over the whole solution. The PRM score for a solution is thhe probability that every step is correct under the PRM. Implemented as the product of the correctness probabilities for each step. They chose to supervise only up to the first incorrect step.

## Evaluation

They also evaluated on OOD(out of distribution) Stem problems, and PRM outperforms both ORM and Majority Voting.
