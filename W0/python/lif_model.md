# Leaky Integrate-and-Fire Model

It doesn't model any physiological charactericts of the neuron but captures its firing mechanism -
so to say the voltage transferring (membrane potential voltage) feature when enough of the signals are coming from dendrites.

$$
\tau_{m} \frac{\partial}{\partial t} V(t) = -(V(t) - E_{L}) + R_{m}I
$$

Left part of the equation models the time evolution of membrane potential and how exactly it is changed
is described in the right part of the equation; the last term is synaptic input while the first one (fully) is leak one (it means that it tries to return voltage back to its resting potential $E_L$).

From the perspective of the neurons, synaptic input is random (or stochastic).

If one has `a = [[1, 2, 3], [4, 5, 6]]`, then `np.sum(a, axis = 0)` will return `[5, 7, 9]` (vertical summing) and
`np.sum(a, axis = 1)` will return `[6, 15]` (horizontal summing).

In histograms, we plotted the distribution in two different timestamps (in the very end and during $\frac{1}{10} of the path).

In our model as soon as neuron reaches the threshold, we send its membrane voltage potential down to its resting value (without considering refractory preiod).
