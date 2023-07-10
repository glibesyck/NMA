# Intro to Models

Typically everyone understands what type of analysis to use but it's hard
to answer such question in the perspective of the models.

“What” model can compactly describe the distribution and data properties (descriptive level).

"How” model proposes a specific way that a system produces the observed behavior (mechanistic level).

“Why” model asks about the underlying principles of a phenomenon (explanatory level).

In any research, we typically start with descriptive (“what”) models. Next, we often ask about the mechanisms and build “how” models to generate or test hypotheses of underlying mechanisms. Ultimately, we are usually interested in the underlying reason of why the phenomenon exists in the first place, “why” models are often the hardest to achieve.

Experiments <-> Data Analysis <-> Modeling.

Models synthesize knowledge (make it more compact), we can infer underlying or latent information.

Models are an abstraction of reality! Keep it as simple as possible, but as detailed as needed (Occam's razor). Models allow for understanding and control. Requires model validation through experiments (model is a hypothesis).

ISI (inter-spike-interval) - Poisson process with Gaussian refractory period.

Metascience - how does the science work.

## Cosine Tuning Model of Neuronal Activity - "What" Model

The neural activity of the monkey which is moving from the central point into one of the directions (measured by angle) is recorded from a primary motor cortex pyramidal cell. It is captured as rastor plot where each line corresponds to the movement and each tick represents action potential.

Cosine function approximates the firing rate of a particular neuron corresponding to the chosen direction of movement (so it is the function of the direction).

It is purely descriptive model, it provides scientifically limited insight (no consideration how|why cosine tuning arises).

## Hodgkin & Huxley (HH) Model

Alan Hodgkin and Andrew Huxley recorded the intracellular potential of the giant axons of the squid. It was the first action potential recording. They wanted to know what are the underlying mechanisms of depolarization and hyperpolarization. First, sodium channels are opened, leading to the rise of the potential and then it leads to the opening of potassium channels and as they close slowly, it leads to the refractory period (when spiking is suppressed, hyperpolarization).

H&H generated the model equation of the first-order differential equation where the neuron is abstracted by a capacitor. Individual ions and leakage channel reversal potentials are represented as batteries while the corresponding channels are resistors.

This model provides a mechanism for the generation of action potentials and synthesizes large amounts of neural data. We can also study effect of interventions and make predictions. Still, we have no idea why ion channels open and close (molecular mechanism).

## Reinforcement Learning

How agents should be acting to maximize the reward? It also synthesizes large amounts of behavioural and neural data. Still, with this model we don't know how brain achieves it.

# "What" Models

Just look at the data and try to describe it.

Heavy tail distribution (left-skewed) is very typical for any kinds of brain data. By looking at the inter-spikes intervals we can learn about the biophysics of the neurons.

Refractory period - there are almost no ISIs near zero as neuron's firing rate is limited due to the ion channels chemistry.

While considering "what" models, we would like to find the equation which describes the data. With the right set of parameters, exponential function describes data greatly!

# "How" Models

It is the most popular type of the models in the neuroscience. We observed that ISIs follow expoenential distribution but
how do the neurons produce this? Neurons have capacitors, so they should integrate signals they receive from other neurons - is it enough to describe exponential nature of the ISIs distribution? Model - LIF-neuron.

Only with excitatory input, the behaviour is very predictable. We will model the balanced excitation and inhibition with $I = \alpha(\text{Poisson}(\lambda) - \text{Poisson}(\lambda))$. The higher the noise the more probability of hitting the threshold we have.

The storage of energy by maintaining a field potential across an insulating membrane can be modeled by a capacitor. The leakage of charge across the membrane can be modeled by a resistor.

# "Why" Models

We don't what the equation which describes how the brain does it but the equation which tells us a story of why it might be a good idea to do it in the described way.

Then we can look at the problem through optimization prism: we would like to maximize the transmitted information (which ISI distribution will trasmit the most amount of information?). We also have the constraint - each neuron can only producea certain number of spikes (we are normalizing for energy expenditure).

Entropy is calculated via $H_b (X) = - \sum_{x \in X} p(x) log_b p(x)$
where the most common bases for $b$ are $2$ - bits and $e$ - nats.

For unimodal distribution, entropy is zero; for bimodal it is one. It answers, how many bits (nats) do we need to describe the data fully (or the measure of uncertainty - which point in the distribution the sample will fall on). From the uniform distribution we have the upper bound on the entropy value - $log_b N$ for $N$ points in the dataset.

If we have the fixed mean value for the ditribution to have, then entropy exponential distribution outperforms uniform one. In fact, it can be analytically shown that among all distributions with fixed mean over positive numbers, exponential has the biggest entropy value.

In "Why" models we start with the question what biology might optimize (we hypothesize constraints and search for the solution in the constrained setup of the real world that the brains need to solve).
