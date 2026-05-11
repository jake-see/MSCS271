# Recursive Stochastic L-system for Simulation Arterial Branching
Semester Project for MSCS-271: Formal Languages and Finite Automata

The goal of our project was to find and reproduce an application of a concept that we learned in this class, specifically formal grammars.\
In a formal language, we have an alphabet (symbols), rules for generating strings (productions), and a set of valid strings (the language). Lindenmayer systems (L-systems) use the same underlying principles. We have created an interactive code that simulates how arteries branch using L-systems as the underlying recursive algorithm.

## Context
In 1968, theoretical biologist Aristid Lindenmayer published a paper with a mathematical theory of biological development, defining a formal rewriting system to model how cells change over time.

Normally in a formal grammar, we re-write one (non-terminal) symbol at a time, with sequential derivation. In L-systems, we just re-write the symbols (entire string) simultaneously.

In 1990, Lindenmayer co-authored a paper with computer scientist Przemyslaw Prusinkiewicz to use L-systems and Turtle graphics for generating lifelike plant forms and visualizing them. Turtle graphics uses symbols as graphical commands: F,+,-,[,] represent draw forward, rotate right, rotate left, push state, and restore state respectively. However, in our code we have opted to draw our branches using the python library Matplotlib (typically used for visualizing plots) since we use it more often in our studies and find it easier and more intuitive.

## Simulation Code
### <u>Initial model</u>
Our first simulation was based on an example of an L-system described in this paper, which describes the following grammar:

<p align="center">
  G=(Σ,ω,P)
</p>

where:\
• Σ is the alphabet of symbols,\
• ω is the initial symbol, and\
• P is the set of substitution rules that determine the patterns.

The specific example had these symbols:\
• Σ={a(θ),s(l),t(l),[,]},\
• ω=t(1), and\
• P =t(l) →s(.6l)[a(−45)t(.4l)][a(45)t(.4l)]\

and these symbols were defined as:\
• a(θ): make a turn of θ degrees clockwise,\
• s(l): create a middle segment of length l (these segments will not be modified
further),\
• t(l): create a leaf (terminal) segment of length l (these segments will be
subdivided in further steps),\
• [: start a new branch from the end of the previous middle segment,\
• ]: end of the branch that was started most recently;

In simple terms, it would recursively draw a middle branch and at the end of it, two shorter child branches at 45 degrees and 40% of the previous length. The new middle branch would then be 60% of the previous length.

### <u>Second model</u>



