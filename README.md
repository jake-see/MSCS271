# Recursive Stochastic L-system for Simulation Arterial Branching
Semester Project for MSCS-271: Formal Languages and Finite Automata

The goal of our project was to find and reproduce an application of a concept that we learned in this class, specifically formal grammars.\
In a formal language, we have an alphabet (symbols), rules for generating strings (productions), and a set of valid strings (the language). Lindenmayer systems (L-systems) use the same underlying principles. We have created an interactive code that simulates how arteries branch using L-systems as the underlying recursive algorithm.

(Main features here?)


## Context
In 1968, theoretical biologist Aristid Lindenmayer published a paper with a mathematical theory of biological development, defining a formal rewriting system to model how cells change over time.

Normally in a formal grammar, we re-write one (non-terminal) symbol at a time, with sequential derivation. In L-systems, we just re-write the symbols (entire string) simultaneously.

In 1990, Lindenmayer co-authored a paper with computer scientist Przemyslaw Prusinkiewicz to use L-systems and Turtle graphics for generating lifelike plant forms and visualizing them. Turtle graphics uses symbols as graphical commands: F,+,-,[,] represent draw forward, rotate right, rotate left, push state, and restore state respectively. However, in our code we have opted to draw our branches using the python library Matplotlib (typically used for visualizing plots) since we use it more often in our studies and find it easier and more intuitive.

### Main Simulation Features

## Simulation Code
### Initial model
Our first simulation was based on an example of an L-system described in this paper, which describes the following grammar:

<p align="center">
  G=(Σ,ω,P)
</p>

where:\
&emsp;• Σ is the alphabet of symbols,\
&emsp;• ω is the initial symbol, and\
&emsp;• P is the set of substitution rules that determine the patterns.

The specific example had these symbols:\
&emsp;• Σ={a(θ),s(l),t(l),[,]},\
&emsp;• ω=t(1), and\
&emsp;• P =t(l) → s(.6l)[a(−45)t(.4l)][a(45)t(.4l)]

and these symbols were defined as:\
&emsp;• a(θ): make a turn of θ degrees clockwise,\
&emsp;• s(l): create a middle segment of length l (these segments will not be modified further),\
&emsp;• t(l): create a leaf (terminal) segment of length l (these segments will be subdivided in further steps),\
&emsp;• [: start a new branch from the end of the previous middle segment,\
&emsp;• ]: end of the branch that was started most recently;

Here we highlight the main production again, which we use for the recursion:
<p align="center">
t(l) → s(.6l)[a(−45)t(.4l)][a(45)t(.4l)]
</p>

In simple terms, with an intial branch length, we recursively draw a middle branch and at the end of it, two shorter child branches at 45 degrees left and right. These child branches would be at 40% of the previous length. The new middle branch would then be 60% of the previous length. This would continue for a specified number of layers (depth). Here's an example of what they looked like, after we tweaked the scaling lengths and depth for better visibility:


### Second model
In real-life, arteries don't usually branch symmetrically and at fixed lengths, so we decided to make our model stochastic. We randomized the number of branches and their lengths and angles (with defined upper and lower bounds).
We then added an interactive element so the user could input their desired bounds. Here's an example of what it looked like:




