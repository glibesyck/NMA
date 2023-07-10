# "What", "How" and "Why" Models

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
