# Recursive Stochastic L-system for Simulation Arterial Branching
Semester Project for MSCS&ndash;271: Formal Languages and Finite Automata (Spring 2026)\
University of Wisconsin&ndash;Stout\
by Evelyn Vo and Jake See

The goal of our project was to find and reproduce an application of a concept that we learned in this class, specifically formal grammars.\
In a formal language, we have an alphabet (symbols), rules for generating strings (productions), and a set of valid strings (the language). Lindenmayer systems (L-systems) use the same underlying principles. We have created an interactive code that simulates how arteries branch using L-systems as the underlying recursive algorithm.

Special thanks to our instructor, Dr. Seth Dutter.

### Main Simulation Features
Each vessel segment produces:
- A forward-growing main vessel
- Multiple child branches with randomized angles and lengths

Biological inspiration:
- Arterial bifurcation patterns
- Murray's Law for vessel radius scaling
- Progressive vessel thinning

Mathematical concepts:
- Recursive fractal geometry
- Trigonometric coordinate transformations
- Stochastic parameter sampling

## Code Instructions
We have included both a python file (.py) and a Jupyter Notebook file (.ipynb) of our final model. After running the code, simply input the upper and lower bounds for randomizing the angle and length changes. The starting angle is 45 degrees and starting length is 100 units, so the bounds add and subtract from them to form new bounds, and then a random number is chosen within those bounds. The default depth is 6. You may decline from inputting anything and press enter for the default values to be used. After all 5 inputs, the visual will be generated.

## Context
In 1968, theoretical biologist Aristid Lindenmayer published a paper with a mathematical theory of biological development, defining a formal rewriting system to model how cells change over time [[1]](#ref1).

Normally in a formal grammar, we re-write one (non-terminal) symbol at a time, with sequential derivation. In L-systems, we just re-write the symbols (entire string) simultaneously.

In 1990, Lindenmayer co-authored a paper with computer scientist Przemyslaw Prusinkiewicz to use L-systems and Turtle graphics for generating lifelike plant forms and visualizing them [[2]](#ref2). Turtle graphics uses symbols as graphical commands: F,+,-,[,] represent draw forward, rotate right, rotate left, push state, and restore state respectively. However, in our code we have opted to draw our branches using the python library Matplotlib (typically used for visualizing plots) since we use it more often in our studies and find it easier and more intuitive.



## Simulation Model Iterations
### Initial model
Our first simulation was based on an example of an L-system described in [this bachelor thesis](https://upcommons.upc.edu/server/api/core/bitstreams/1466f8fb-4396-47f9-8e99-7c241aa3b7d6/content) by Sergi L&aacute;zaro [[3]](#ref3), which describes the following grammar:

<p align="center">
  G=(Σ,ω,P)
</p>

where:
- Σ is the alphabet of symbols,
- ω is the initial symbol, and
- P is the set of substitution rules that determine the patterns.

The specific example had these symbols:
- Σ={a(θ),s(l),t(l),[,]},
- ω=t(1), and
- P =t(l) → s(.6l)[a(−45)t(.4l)][a(45)t(.4l)]

and these symbols were defined as:
- a(θ): make a turn of θ degrees clockwise,
- s(l): create a middle segment of length l (these segments will not be modified further),
- t(l): create a leaf (terminal) segment of length l (these segments will be subdivided in further steps),
- [: start a new branch from the end of the previous middle segment,
- ]: end of the branch that was started most recently;

Here we highlight the main production again, which we use for the recursion:
<p align="center">
t(l) → s(.6l)[a(−45)t(.4l)][a(45)t(.4l)]
</p>

In simple terms, we recursively draw a middle branch and at the end of it, two shorter child branches at 45 degrees left and right. These child branches would be at 40% of the previous length. The new middle branch would then be 60% of the previous length. This would continue for a specified number of layers (depth). Here's a visual example, after we tweaked the scaling lengths and depth for better visibility:

<img width="378" height="350" alt="Screenshot 2026-05-11 184511" src="https://github.com/user-attachments/assets/b4437449-ee21-4c5a-9cdb-78a0ecc826d3" />

### Second model
In real-life, arteries don't usually branch symmetrically and at fixed lengths, so we decided to make our model stochastic. We randomized the number of branches and their lengths and angles (with defined upper and lower bounds, and slightly heavier weighting for certain number of branches).
We then added an interactive element so the user could input their desired bounds. This was the updated production:

<p align="center">
 t(l) → s(0.6l)[a(random angle 1)t(random length 1)][a(random angle 2)t(random length 2)]...[a(random angle n)t(random length n)]
  
  for n number of branches.
</p>

Here's a visual example:

<img width="423" height="350" alt="Screenshot 2026-05-11 184318" src="https://github.com/user-attachments/assets/b9a97123-afee-4e1f-a26d-7d2f23f091f7" />

### Final model
To make it even more realistic, we decided to use implement Murray's law for scaling the radius of the vessel as it splits and narrows (in this case the width of the child branch since it's 2D).
Murray's law states that the radius of a parent vessel equals the sum of the cubes of the radii of its daughter branches [[4]](#ref4). This implies that as vessels branch, the radii narrow in a specific proportion.
We also changed the color to red to make it look more like blood vessels (the gradient is an aesthetic choice to reflect depth of the branches and doesn't reflect real biology). Here is the updated production:

<p align="center">
 t(l,w) → s(0.6l)[a(random angle 1)t(random length 1, child width)][a(random angle 2)t(random length 2, child width)]...[a(random angle n)t(random length n, child width)]
  
  for n number of branches.
</p>

Here is a visual example:

<img width="500" height="634" alt="image" src="https://github.com/user-attachments/assets/20396e4d-fc0e-4068-ae67-19607461a8f7" />

## References
<a id="ref1"></a>
[1] A. Lindenmayer, “Mathematical models for cellular interactions in development I. Filaments with one-sided inputs,” Journal of Theoretical Biology, vol. 18, no. 3, pp. 280–299, 1968.

<a id="ref2"></a>
[2] P. Prusinkiewicz and A. Lindenmayer, *The Algorithmic Beauty of Plants*. New York, NY, USA: Springer-Verlag, 1990.

<a id="ref3"></a>
[3] S. Lázaro, *Modelling of Realistic Blood Vessel Geometry*, Bachelor thesis, Gottfried Wilhelm Leibniz Universität Hannover, Hannover, Germany, Sep. 2011. Available: https://upcommons.upc.edu/server/api/core/bitstreams/1466f8fb-4396-47f9-8e99-7c241aa3b7d6/content

<a id="ref4"></a>
[4] C. D. Murray, “The physiological principle of minimum work: I. The vascular system and the cost of blood volume,” Proceedings of the National Academy of Sciences, vol. 12, no. 3, pp. 207–214, 1926.
