---
title: Deep Reinforcement Learning for skeleton-based action recognition
layout: page
---

<a href="https://github.com/FarzanehEntezari/rl-action-recognition">code</a>
&emsp;
<a href="https://youtu.be/wDJ7TjHDkPE">presentation video</a>

## Intro

Humans easily recognize and identify actions in video, but automating this procedure is challenging. Human action recognition in video is of interest for applications such as automated surveillance, elderly behavior monitoring, human-computer interaction, content-based video retrieval, and video summarization. For an action recognition task, we need to keep track of the movements of body parts. Therefore, capturing the body pose would enable us to detect the action going on in a sequence of frames. We consider an illustration of human body which contains the 3D coordinates of body joints for each frame.
We are using skeletal joint locations from <cite>UTKinect-Action3D</cite> dataset.


## Approach

The key idea of our framework, inspired by <cite> Tang et al</cite>, is that there are a few frames in each video which are more informative than others. 

Basically, there are two sub-networks in our method: frame distillation network (FDNet) and convolutional neural network (CNN). The FDNet selects the most informative frames from the sequence of input frames with a deep progressive reinforcement learning method in an episodic task. The selected key frames are then fed into the CNN to recognize the action. The frame selection problem is formulated as a Morkov decision process (MDP), where the action is deciding whether each frame is a key frame or not. And the reward is provided by
the CNN during training, based on its confidence in the correct label. We are optimising the agent with Monte-Carlo policy gradient (REINFORCE) algorithm by maximizing the expected discounted reward.

<!-- <img src="../assets/img/projects/project-RL-skeleton/pipeline.jpg" width="300"/> -->

## Experiments
We evaluated our framework on <cite>UTKinect-Action3D</cite> dataset. The dataset contains recordings from 10 subjects, performing 10 actions twice. The classes consist walk, sit down, pick up, carry,throw, push, pull, etc. Three channels of RGB, depth and joint locations are recorded for this data. For our algorithm, we are using the xyz coordinates of 20 joint locations.

![Alt text](../assets/img/projects/project-RL-skeleton/dataset.png?raw=true "Title")

The average rewards obtained after running the algorithm for 100 episodes over all videos is depicted below. The test accuracy before and after frame selection is 91.66% and 95.83% respectively, and the number of selected frames is one third of the number of original frames on average. The results show a considerable improvement in accuracy when we perform frame selection on the data. Therefore, the network would process fewer frames and would be able to make smarter guess about the action being performed in the video with less computation cost.

![Alt text](../assets/img/projects/project-RL-skeleton/rewards.png?raw=true "Title")
