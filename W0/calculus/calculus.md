# Integration and Differentiation

Derivative - how fast the function increases or decreases (near zero - stays the same).

Integration - area under the curve, meaning that if integration function is almost linear - the same value is added each time (constant function - the ending of the sigmoid).

Eigenfunction - integration and differentiation turns them into themselves with some scaling. For example, family of exponentials $e^{ax}$.

Slope of the function as the proxy for the derivative. This idea can be extended to taking the derivative of the data which can't be expressed as a well-defined function.

## Example: PSP

Good approximation for PSP (post-synaptic potential - small deflection in the membrane voltage
when spike arrives) shape - alpha-function (product of linear function with negative exponential one).

$$
\text{PSP}(t) = \frac{t}{\tau}\text{exp}(\frac{-t-t_{\text{sp}}}{\tau})
$$

Neuron membrane is like an integrator; thus by taking the derivative one may find what was the value of the current (synaptic conductance) which was responsible for creating this deflection.

## Example: Neuron Transfer Function.

While injecting constant current in the neuron, its firing rate changes as a function of strength of the injected current ($\text{rate}(I)$) - this is called input-output transfer function or just the transfer function or I/O Curve of the neuron. For most neurons this can be approximated by a sigmoid function (think of it as being activation function for ANN):

$$
\text{rate}(I) = \frac{1}{1 + \text{exp}(-a*(I - \theta))} - \frac{1}{\text{exp}(a*\theta)} + \eta
$$

where $\eta$ is Gaussian noise (noise = zero mean).
Slope of this function is gain of the neuron as it tells how the neuron output will change if the input is changed (how much the firing rate of the neuron is sensitive to input change).

Visual notice: the bigger $a$ - the more vertically extended the plot is. The bigger $\theta$ - the more shifted to the right the point of saturation of sigmoid is. Gain function looks like Gaussian bell (which is predictable considering the derivative of sigmoid function).

**Note:** The numerical estimate of the derivative will result in a time series whose length is one short of the original time series. In the example of sine function, the bigger step size $h$ is, the more shifted derivative plot to the left is.

In reality, neurons don't receive injected current, instead - excitatory and inhibitory inputs thus its firing rate is more correctly described as "sigmoid fashion" looking and the parameters depend on the situation overall (how many spikes arrived from which neurons). We can then visualize function as both - dependence from excitation as well as from inhibition (two-variables function).

The Jacobian is used to determine the dynamics and stability of a system.

**Observation**: Neurons cannot have negative firing rates. In models, we either choose the operating point such that the output does not go below zero, or else we clamp the neuron output to zero if it goes below zero.

Analytically-derived error for numerically calculating the integral as Riemann sum is:

$$
\epsilon \le M\frac{b-a}{2n}
$$

where $M$ is the max $|\frac{\partial{f}}{\partial{t}}|$ and $n$ - number of bins.
If we make trapezoids instead of rectangles, the error is going to decrease with factor $\frac{1}{n^{2}}$.

## Example: PSP

Total charge delivered by the PSP in the area under the curve.

Alternatives to Riemann sum are Lebesgue integral and Runge Kutta. The Riemann sum is the basis of Euler's method of integration for solving ordinary differential equations.

**Extremely interesting observations**: differentiation can be thought of high-pass filter: if we have the signal with slow component togehter with fast fluctuations while considering differentiation, we completely throw away slow frequency (as we take difference of adjacent samples and common part which is the slow signal is removed by the difference). Integration works in the opposite direction - we add up adjacent samples thus removing fast changes (they cancel each other) thus it can be thought as low-pass filter.

# Differential Equations

Differential equation can be thought as some constraint on how the change is executed or propagated (which rules it follows), "rate of change". The most famous of these in neuroscience is the Nobel Prize winning Hodgkin Huxley equation, which describes a neuron by modelling the gating of each axon.

First order DE take form of:

$$
\frac{\partial}{\partial t}y(t) = f(t, y(t))
$$

By saying that

$$
\frac{\partial}{\partial t}p(t) \propto p(t)
$$

one can read it as change of population is proportional to the population itself (the bigger the population is, the faster it increases). To solve DE we need initial condition (point from which we start observing the system).

The proposed equation is pretty limited: it assumes that dynamics are static over time (= birth rate depends only on current population but not time which is basically not true). Still, this equation is of use in Drift Diffusion Model which describes the accumulation of evidence in decision making process.

## Example: Leaky Integrate and Fire Equation (LIF)

It models the single neuron and is of distinct popularity due to its inexpensive computations (bedrock of many simulations).

It is described as:

$$
\tau_{m} \frac{\partial}{\partial t} V(t) = -(V(t) - E_{L}) + R_{m}I
$$

where $V(t)$ - membrane potential, $\tau_{m}$ - time constant, $E_{L}$ - resting potential, $R_{m}$ - resistance and $I$ - input (external and internal all together).

Notice! Any activity which is higher than resting potential impacts negatively on the value of change in membrane potential (returns it back).

Usually, $\tau\_{m} = 10\text{ms}$ and $E_{L} = -75\text{mV}$. Initial condition is $V(0) = V_{\text{Reset}}$.

An exact solution of LIF model equation without input part (no sensory information at all) is

$$
V(t) = E_{L} + (V_{\text{Reset}} - E_{L})e^{-\frac{t}{\tau_{m}}}
$$

The exact solution with input part is the following equation:

$$
V(t) = E_{L} + R_{m}I + (V_{\text{Reset}} - E_{L} - R_{m}I)e^{-\frac{t}{\tau_{m}}}
$$

The solution is something that exponentially increases and then plateau - which is not physiologically correct. Thus we need to model the fire part of the neuron. If $V(t)$ is above $V_{\text{th}}$, then the neuron is firing; below - it follows the described dynamics. We need to record the spiking time - $t_{\text{spi}}$ and set $V(t_{\text{spi}}) = V_{\text{Reset}}$.

Finally, the exact solution with firing part will look like:

$$
V(t) = E_{L} + R_{m}I + (V_{\text{Reset}} - E_{L} - R_{m}I)e^{-\frac{-t - t_{\text{spi}}}{\tau_{m}}}
$$

Raster plot of spikes - dots whenever spike occurs.
Rate model - when we learn how the input impacts the total number of spikes (frequency of neuron being fired).

Spiking here is the form of discontinuity which is hard to deal with and the model itself is pretty abstracted from biology. Moreover, while having small constant $I$, it still doesn't reach desired threshold value and saturates on the plateau which is not biologically plausible. Also, there is a limit of spikes due to the refractory period which is not accounted here.

# Numerical Methods

Lots of equations in mathematics can't be solved directly -> numerical methods for approximation.

Consider secant through points $(t_{0}, y_{0})$ and $(t_{1}, y_{1})$. When $t_{1}$ is very close to $t_{0}$ it almost becomes the tangent to the function. As the conclusion, it follows that:

$$
\frac{\partial}{\partial t} y(t) = \frac{y_{1} - y_{0}}{t_{1} - t_{0}}
$$

and thus it can be derived that

$$
y_{1} \approx y_{0} + \frac{\partial}{\partial t} y(t) * (t_{1} - t_{0})
$$

It doesn't give the exact answer; indeed, on each step, as we don't know the true function, the error term is going to be accumulated. Such method for prediction of the next value of the function is called Euler method. The error $e_1$ from one time-step is known as the local error. For the Euler method the local error is linear, which means that the error decreases linearly as a function of timestep and is written as $O(\Delta t)$.

In iterative maneer of the prediction it looks in the following way:

$$
y[k+1] = y[k] + \Delta t \frac{\partial}{\partial t[k]} y(t)[k]
$$

$\Delta t \frac{\partial}{\partial t[k]} y(t)[k]$ part is called "dynamics of the system" (what happens to it).

On each next time step, the error becomes bigger - it is the global error which is the propagation of the local ones (accumulates all small ones). The analytical constraint on its value can be derived from Taylor expansion.

**Note**: electrophysiologists normally listen to spikes when conducting experiments (one can transform membrane potential change into the sound).

System of DEs can be used to describe the couple of processes interact. In neuroscience, Wilson-Cowan model describes how excitation and inhibition populations do that. Phase-plane plots are used then to examine DEs (when there are 2 variables f.e. and the plot describes the relationship between them, the overall dynamics which excludes temporal resolution from the plot itself but it is incorporated in the relationship).

When the dynamics of populations are not bounded - warning sign (it can be the seizure or the wrong model). Quadrants in phase-plane plot show the derivative signs - where the functions increase and decrease (to have the division lines, one should find them by making the derivatives equal to zero). The solution is stable if we see the same trajectory over and over in the phase-plane plot.

RK 4th order is easy to implement but the accuracy is much higher than in Euler method. It is 4th order meaning that error is $O(\Delta t^{4})$

## Example: Neural oscillations

A great deal of experimental and neurophysiological studies have investigated whether the brain oscillates and/or entrain to a stimulus. In the paper by Keith Dowlin and M. Florencia Assaneo published in May 2021, the question was approached from the math point of view by discussing what creates oscillations and how do the oscillators (systems which create oscillations) look like.

The interesting observation is that even if the input is periodic (= oscillation), it doesn't necessarily provoke oscillation in the output (the system itself plays important role - reminds me of the randomness from Stephen Wolfram: we don't need random input to create random output).

Moreover, their research illustrates an oscillations does not have to maintain all the time, so experimentally we should not expect perfectly maintained oscillations. We see this all the time in $\alpha$-band oscillations in EEG the oscillations come and go.
