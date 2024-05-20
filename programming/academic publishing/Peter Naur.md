---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
## Programming as Theory Building (1985)

Superb artcle where he makes the argument that what is valuable about a program is not the program text and accompanying documents, but rather the theory of program that lives in the mind of the programmers who work on it.

PDF: https://pages.cs.wisc.edu/~remzi/Naur.pdf
nicer HTML version: https://gist.io/@danielkaczmarczyk/5a025f7439c38b6db21205e563837d9b

> This observation leads to the important conclusion that the problems of program modification arise from acting on the assumption that programming consists of program text production, instead of recognizing programming as an activity of theory building.

> On the basis of the Theory Building View the decay of a program text as a result of modifications made by programmers without a proper grasp of the underlying theory becomes understandable. As a matter of fact, if viewed merely as a change of the program text and of the external behaviour of the execution, a given desired modification may usually be realized in many different ways, all correct. At the same time, if viewed in relation to the theory of the program these ways may look very different, some of them perhaps conforming to that theory or extending it in a natural way, while others may be wholly inconsistent with that theory, perhaps having the character of unintegrated patches on the main part of the program. This difference of character of various changes is one that can only make sense to the programmer who possesses the theory of the program. At the same time the character of changes made in a program text is vital to the longer term viability of the program. For a program to retain its quality it is mandatory that each modification is firmly grounded in the theory of it. Indeed, the very notion of qualities such as simplicity and good structure can only be understood in terms of the theory of the program, since they characterize the actual program text in relation to such program texts that might have been written to achieve the same execution behaviour, but which exist only as possibilities in the programmer’s understanding.

New programmers need to learn, not from documentation or program study, but from intense contact with the team that already possesses the theory of the program:

> For a new programmer to come to possess an existing theory of a program it is insufficient that he or she has the opportunity to become familiar with the program text and other documentation. What is required is that the new programmer has the opportunity to work in close contact with the programmers who already possess the theory, so as to be able to become familiar with the place of the program in the wider context of the relevant real world situations and so as to acquire the knowledge of how the program works and how unusual program reactions and program modifications are handled within the program theory.

Programs, once dead, cannot reasonably be revived:

> A very important consequence of the Theory Building View is that program revival, that is reestablishing the theory of a program merely from the documentation, is strictly impossible. Lest this consequence may seem unreasonable it may be noted that the need for revival of an entirely dead program probably will rarely arise, since it is hardly conceivable that the revival would be assigned to new programmers without at least some knowledge of the theory had by the original team

The Scientific method should be thought of as not as a guideline for how scientists work, but rather an incomplete description of the work they do:

> The first argument is that software development should be based on scientific manners, and so should employ procedures similar to scientific methods. The flaw of this argument is the assumption that there is such a thing as scientific method and that it is helpful to scientists. This question has been the subject of much debate in recent years, and the conclusion of such authors as Feyerabend [1978], taking his illustrations from the history of physics, and Medawar [1982], arguing as a biologist, is that the notion of scientific method as a set of guidelines for the practising scientist is mistaken.

Programmers with deep knowledge of the theory of program have outsized value:

> More generally, much current discussion of programming seems to assume that programming is similar to industrial production, the programmer being regarded as a component of that production, a component that has to be controlled by rules of procedure and which can be replaced easily... Since this theory by its very nature is part of the mental possession of each programmer, it follows that the notion of the programmer as an easily replaceable component in the program production activity has to be abandoned

There's a final section that doesn't appear to be written by Naur himself? Anyway I like this line:

> Experienced designers often start their documentation with just

> -   The metaphors
> -   Text describing the purpose of each major component
> -   Drawings of the major interactions between the major components

> These three items alone take the next team a long way to constructing a useful theory of the design.