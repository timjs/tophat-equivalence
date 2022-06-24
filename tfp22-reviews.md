SUBMISSION: 10
TITLE: Semantic equivalence of task-oriented programs in TopHat

----------------------- REVIEW 1 ---------------------
SUBMISSION: 10
TITLE: Semantic equivalence of task-oriented programs in TopHat
AUTHORS: Tosca Klijnsma and Tim Steenvoorden

----------- Overall evaluation -----------
SCORE: 2 (accept)
----- TEXT:
## Summary

Task-oriented programming (Top) captures a description of the work and
its interaction between users. TOP programs can be constructed through
task combinators. Existing work has provided formal semantics for TOP,
in particular via TopHat, a formal language with operational semantics
for reasoning about task-oriented programs. However, deciding whether
two tasks are equivalent has been a long-standing open research
question. This paper defines the semantic equivalence relation between
tasks using three observations (failing F, value V, inputs I). It then
discusses five conditions of tasks and the equivalence between tasks
of the same condition. The paper then presents laws on tasks.

## Comments

Pros:

- The paper is well-written, and I enjoyed reading it. All
  explanations are clear and easy to follow. I appreciate that all
  definitions come with examples that help understand the key ideas.

- The definition of semantic equivalence and laws on tasks contribute
  to the foundation of task-oriented programming. I expect to see more
  reasoning work using those definitions and laws in future work in
  task-oriented programming.

Cons:

- I am not very satisfied with Section 2.5, which defines the semantic
  relations used by TopHat formalization. In particular, explanations
  about some of the definitions (e.g., handle and interact) are
  missing. There is also no definition for fixation or normalization.
  I understand that those definitions are from existing work, and they
  may not be crucial for this work. Still, I don't feel comfortable
  reading a paper on semantic equivalence without even learning how
  semantics is defined.

Minor:

- page 3: "... of the program. Which in turn could be useful.." ->
  "... of the program, which in turn could be useful.."

- page 7: "We write t, \sigma, \delta \Downarrow t', \sigma'" to
  denote the fixation ... given the dirty set \delta, ... The set
  \delta' contains all heap locations ..."

  Two questions: 1) What is a dirty set? 2)What is \delta'? Should it
  be \sigma'?

- Figure 4 on page 10 includes the syntax for share `share E` and
  assign `E1 := E2`, but they are not mentioned in the paper. You may
  consider including a short discussion about what those constructs
  are and whether they play a role in defining semantic equivalence.

----------------------- REVIEW 2 ---------------------
SUBMISSION: 10
TITLE: Semantic equivalence of task-oriented programs in TopHat
AUTHORS: Tosca Klijnsma and Tim Steenvoorden

----------- Overall evaluation -----------
SCORE: 0 (borderline paper)
----- TEXT:
The aim of the paper is to use a formal semantics for task oriented programming language TOP-HAT, to determine when two such programs are equivalent.

Comments:
Introduction: For someone unfamiliar with Task Oriented Programming, it would be beneficial to include a small use-case example. From what I gather TOP is used to generate web-interaces for some kind of web-services? Could you please introduce the context of TOP a bit more? In the end of the Related work it's very briefly mentioned that it's been used to some sort of tax-subsidy-calculation service for solar panels, but it would be nice to have an concrete example up front to help the reader understand what TOP is used for. You later have some toy-programs to explain the semantics, but it would be beneficial to also get the big picture.

In example 1: Notation hasn't been introduced. What does BOX INT mean? What does the Box-with-circle-inside mean? This is only explained in 2.1

If you need more space, reduce the "Structure" section.

Section 2.5 mentions a "dirty set". What do you mean by a dirty set?

Section 5: "To satisfy the first property of Section 3..." --> give the property a name/number to refer to it more concisely: e.g. "to satisfy property 1"

Proposition 8:
Please clarify: does left/right identity hold for tasks other than failing? Should these then be conditional laws saying forall t != fail ==> left/right identify? I read the inequality laws as being implicitly universally quantified over t, so then left/right identity would say " Forall tasks t, it is NOT the case that BOX{} BOWTIE t is equal to t?

But in the proof you talk just about t = fail, as kind of a counterexample, so what you prove is then (if I understand correctly) that EXISTS t s.t. left/right identity does not hold.

Same comment to some laws in Proposition 9, 10,11. Please check and clarify.

Summary of comments:
I think the paper looks OK, although for someone unfamiliar with Task-oriented programming, a concrete use-case  in the Introduction would be beneficial to place this work in a wider context.  Please also check the comments on propositions 8-11, I think there were some unclarities there that should be adressed to avoid readers getting confused. Normally, I'd expect to see properties that hold (forall quantified) listed, as these are useful in the use-case mentioned, compiler optimisation. It is unclear what the status are for the inequalities, are they never true, or just for some values of task t? This should be fixed if the paper is to be accepted.

----------------------- REVIEW 3 ---------------------
SUBMISSION: 10
TITLE: Semantic equivalence of task-oriented programs in TopHat
AUTHORS: Tosca Klijnsma and Tim Steenvoorden

----------- Overall evaluation -----------
SCORE: 2 (accept)
----- TEXT:
This paper builds on the second author's previous work on TopHot,
which is a formal model of task-oriented programming (TOP) as
implemented, for example, by iTasks. Here, the authors define
observational equivalence, which might be useful for optimizing or
refactoring TOP programs, and use it to derive some laws about TopHat
operators. It turns out, for example, that some operators aren't
monads, as they might at first appear to be.

The work is generally well presented, I detect no technical flaws, and
both the definition of observational equivalence and derived laws seem
useful for reasoning about a TOP language. The presentation is also
reasonably self-contained; it relies on a previous presentation of
TopHat in some ways, including the grammar of expressions of the
definition of normalization, but that's fair, since repeating all
details here would take a lot more space.

The presentation could be improved in a couple of ways:

 * Spend a little more time explaining how the syntax of TopHat
   combines source terms with editor state (assuming I understand
   correctly). For example, something like "⊟^k 42" seems not to be
   analogous to an iTasks expression, but a combination of code with
   an editor that currently holds the value 42. A more conventional
   choice might be to separate a term like "⊟^k" and an editor store
   that maps k to 42. With that split, it seems like the distinction
   between ⊟ and ⊞ would not be needed. Also, the split might reduce
   the need for explanation on page 13, for example. Still, the choice
   here appears to work, and it could just use more explanation and
   motivation up front.

 * Provide more concrete examples to show how they are modeled by
   TopHat terms. The 2019 paper provides some of that, but brief
   examples here would help to recap and improve the reader's
   intuition. In particular, it's not really clear to me why `↯ ⨝ t`
   should not counted as equivalent to `↯`, and an example would
   probably help. My best guess is that `t` could involve an input,
   which would involve a user-visible editor (even if that editor
   result is never usefully consumed), and so it shouldn't be
   optimized to `↯` and erase the editor.

As a nit, it seems that section 7 may mix up metavariables and terms.
The paper uses `t` in various places as a metavariable standing for an
expression. In the observational (non)equivalences in section 7,
shouldn't the `t`s there be `x`s, so that they're variables whose
value is supplied by context? (That is, the nonequivalences aren't
meant to hold for all task expressions `t`. It's a question of how far
out the implicit "for all" is lifted.)