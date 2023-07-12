# IBL Behaviour Dataset

IBL - international brain laboratory. Visual decision-making task, that is very similar to the one used in the Steinmetz dataset.

A two alternative forced choice decision task. Difficulty is controlled by varying the constrast of a Gabor stimulus. Automated training protocol, choices are made with wheel. Animal is in the behavioural rig with fixed head, high-speed camera. Water as the reward (noise burst in wrong case), little "peep" noise when the stimuli appears (in low-contrast situations it's hard to notice). Then, bias is introduced and measured whether trained mice respond to it.

# Caltech Mouse Social Behaviour

Complex sensory environment + internal state, choice on how to respond. Correlate behaviour with neural activity. Manual scoring of frames (what did mice do in each frame of the video) - it's very subjective and time-consuming. Instead, Mouse Action Recognition System (MARS), CV pipeline for interacting poses (anatomical keypoints) and use these features to apply frame-to-frame actions labels.

There is training and test dataset for supervised learning! Each frame is (7, 2, 2) (7 keypoints of 2 coordinates of 2 mice) and label (only four of them: attack, investigate, mount or other). Sequence of frames is around 10 minutes. Input trajectory - past frames + current frame + future frames. In dataset there are also scores of confidence for each of the frames (whether their MARS algorithm is confident enough in the estimated pose). Also there are pre-computed features that might be useful (from a model trained with task programming on the trajectory data), there are 32 of them.

# Bayesian Heuristic for Perceptual Decision-Making

Motion direction estimation task. We are constatly guessing (from texture | crowd). Probabilistic noisy sensory information we collect from the environment with prior knowledge. Crowd - complex environment, instead - random dot kinematogram (RDK setup): coherent motion with noisy Brownian (mix of two type of motion). Estimate as fast and as accurate as possible.

There are 12 subjects. Prior mean (it is fixed to be 225) and prior standard deviation. The maximum number of runs for each subject is 44. Block never lasts more tham 226 trials. Motion coherence - 6%, 12% and 24%.
