# Vectors

Linear Algebra - "language of data".

When one says about neuron "fires at X Hertz", it means "X spikes per minute".

Stack vectors "tip to tail".

2D plane in 3D != $\mathbb{R}^{2}$ :) Lower-dimensional structure.

## Example: LGN

Hierarchial Visual Processing Scheme

[Hierarchial Visual Processing Scheme](https://drive.google.com/uc?export=download&id=116eP5jVVfqNoIJMnzyo0lDOAlMDYbVFE)
Retina is in the back of the eye, while LGN (Lateral Geniculate Nucleus) is located in thalamus. Neurons in LGN are fired by the activity of retina neurons.

Inner product - how many information is shared between the vectors.

# Matrices

Properties of transformations in linear manner:

- origin remains on its place;
- grid lines are straight, parallel and evenly-spaced;

Eigenvectors are important for understanding the behaviour of dynamical system as well as they
may visually explain better what kind of transformation we have (rotation, contraction, expansion, horizontal vs vertical, projection onto an axis, reflection).

# Discrete Dynamical Systems

## Example: Neural Circuit

Returning back to the example with retina neurons firing LGN ones, here we add more dimensionality - time (by
making it discrete - chop the time up into little bins).

If we have our initial condition $\mathbf{a}_{0} = c_{1}\mathbf{v}_{1} + c_{2}\mathbf{v}_{2}$, where $\mathbf{v}_{1}, \mathbf{v}_{2}$ are eigenvectors of matrix $W$ which corresponds to the dynamics of the system (meaning $\mathbf{a}_{t} = W*\mathbf{a}_{t-1}$), then:

$$
\mathbf{a}_{t} = c_{1}\lambda_{1}^{t}\mathbf{v}_{1} + c_{2}\lambda_{2}^{t}\mathbf{v}_{2}
$$

If all eigenvalues are real and at least one has an absolute value above 1, the neural activities explode to infinity or negative infinity, except for special cases where the initial condition lies along an eigenvector with an eigenvalue whose absolute value is below 1.

If eigenvalues are complex, the neural activities rotate in space and decay or explode depending on the amplitude of the complex eigenvalues.
