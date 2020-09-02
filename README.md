# Detection of a squash ball from a 2D video in real time

In racket sport analytics, being able to detect the ball is an essential step. In squash, this problem is non trivial due to the velocity at which the ball travels and the size of the ball. This repository will attempt to detect a squash ball from a 2D video, in real time. The ability to correctly position a ball can be used in the following cases:
- Shot detection (where the ball bounces on the court and the speed can be used to determine shots)
- Score counting
- Player strengths / weakness exposure

There are two phases to this problem:
1. Tracking the ball position in a 2D squash video
2. Real time application of tracking algorithm

## 1. Tracking
Tracking a small and fast moving white ball in a series of images using standard computer vision techniques with colour and shape yielded poor results. This repo uses a deep learning model, TrackNet, for ball detection. TrackNet performs particularly well on squash detection as it uses a technique whereby three frames are fed into the neural net at a time. Here are the [source code](https://nol.cs.nctu.edu.tw:234/open-source/TrackNet/) and [research paper](https://arxiv.org/pdf/1907.03698.pdf) of this model.
This model was originally developed for tennis ball detection, but was extended to [badminton shuttle detection](https://inoliao.github.io/CoachAI/). The best pre-trained model uses the weights saved in [new_trimmed.2](/Users/jeffreykayne/Documents/HomeRepo/SquashTracker/squash-ball-detector/bin/TrackNet/Code_Python3/TrackNet_Three_Frames_Input/weights/new_trimmed.2), which is assumed to be the model weights trained on badminton.
This model provides good initial results with ~40% of balls being correctly positioned. It is believed that this could be greatly improved by training on a squash specific dataset (>90% accuracy on badminton and tennis trained models).

## 2. Real time tracking
