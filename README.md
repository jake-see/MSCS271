# Recursive Stochastic L-system for Simulation Arterial Branching
Semester Project for MSCS-271: Formal Languages and Finite Automata

The goal of our project was to find and reproduce an application of a concept that we learned in this class, specifically formal grammars.\
In a formal language, we have an alphabet (symbols), rules for generating strings (productions), and a set of valid strings (the language). Lindenmayer systems (L-systems) use the same underlying principles. We have created an interactive code that simulates how arteries branch using L-systems as the underlying recursive algorithm.

## Context
In 1968, theoretical biologist Aristid Lindenmayer published a paper with a mathematical theory of biological development, defining a formal rewriting system to model how cells change over time.

Normally in a formal grammar, we re-write one (non-terminal) symbol at a time, with sequential derivation. In L-systems, we just re-write the symbols (entire string) simultaneously.

In 1990, Lindenmayer co-authored a paper with computer scientist Przemyslaw Prusinkiewicz to use L-systems and Turtle graphics for generating lifelike plant forms and visualizing them. Turtle graphics uses symbols as graphical commands: F,+,-,[,] represent draw forward, rotate right, rotate left, push state, and restore state respectively. However, in our code we have opted to draw our branches using the python library Matplotlib (typically used for visualizing plots) since we use it more often in our studies and find it easier and more intuitive.

## Code
Our first simulation was based on an example of an L-system described in this paper, which describes the following grammar:
G=(Σ,ω,P)

where:
• Σis the alphabet of symbols,
• ω is the initial symbol, and
• P is the set of substitution rules that determine the patterns.

