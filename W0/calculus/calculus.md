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

Usually, $\tau\_{m} = 10\text{ms}$ and $E_{L} = -75\text{mV}$. Initial condition is $V(0) = V_{text{Reset}}$.

An exact solution of LIF model equation without input part (no sensory information at all) is

$$
V(t) = E_{L} + (V_{text{Reset}} - E_{L})e^{-\frac{t}{\tau_{m}}}
$$

The exact solution with input part is the following equation:

\begin{equation}
V(t) = E*L+R_mI+(V*{reset}-E_L-R_mI)e^{\frac{-t}{\tau_m}}
\end{equation}

The solution is something that exponentially increases and then plateau - which is not physiologically correct. Thus we need to model the fire part of the neuron. If $V(t)$ is above $V_{text{th}}$, then the neuron is firing; below - it follows the described dynamics. We need to record the spiking time - $t_{text{spi}}$ and set $V(t_{text{spi}}) = V_{text{Reset}}$.

Finally, the exact solution with firing part will look like:

\begin{equation}
V(t) = E*L+R_mI+(V*{reset}-E_L-R_mI)e^{\frac{-t - t\*{spi}}{\tau_m}}
\end{equation}

Raster plot of spikes - dots whenever spike occurs.
Rate model - when we learn how the input impacts the total number of spikes (frequency of neuron being fired).

Spiking here is the form of discontinuity which is hard to deal with and the model itself is pretty abstracted from biology. Moreover, while having small constant $I$, it still doesn't reach desired threshold value and saturates on the plateau which is not biologically plausible. Also, there is a limit of spikes due to the refractory period which is not accounted here.

# Numerical Methods

Lots of equations in mathematics can't be solved directly -> numerical methods for approximation.
