# ForwardTacotron

Inspired by Microsofts [FastSpeech](https://www.microsoft.com/en-us/research/blog/fastspeech-new-text-to-speech-model-improves-on-speed-accuracy-and-controllability/)
we modified Tacotron to generate speech in a single forward pass using a duration predictor to align text and generated mel spectrograms. 
The model has following advantages:
- Robustness: No repeats and failed attention modes for challenging sentences. 
- Speed: The generation of a mel spectogram takes about 0.04s on a GeForce RTX 2080.
- Controllability: It is possible to control the speed of the generated utterance.
- Efficiency: In contrast to FastSpeech and Tacotron, the model of ForwardTacotron
does not use attention at all. Hence, the required memory grows linearly with text size, which makes it possible to synthesize large articles at once.


# Samples

[Can be found here.](https://as-ideas.github.io/ForwardTacotron/)

# Installation

Ensure you have:

* Python >= 3.6
* [Pytorch 1 with CUDA](https://pytorch.org/)

Then install the rest with pip:

> pip install -r requirements.txt

# Training your own Models

1 - Download the [LJSpeech](https://keithito.com/LJ-Speech-Dataset/) Dataset.

> python preprocess.py --path /path/to/ljspeech

2 - Train Tacotron with:

> python train_tacotron.py

3 - Use the trained tacotron model to create alignment features with

> python train_tacotron.py --force_align

4 - Train Forward Tacotron with 

> python train_forward.py

5 - Generate Sentences with Griffin-Lim vocoder

> python gen_forward.py --alpha 1 --input_text "this is whatever you want it to be" griffinlim

As in the original repo you can also use a trained WaveRNN vocoder:

> python gen_forward.py --input_text "this is whatever you want it to be" wavernn

____

### References

* [FastSpeech: Fast, Robust and Controllable Text to Speech](https://arxiv.org/abs/1905.09263)

### Acknowlegements

* [https://github.com/keithito/tacotron](https://github.com/keithito/tacotron)
* [https://github.com/fatchord/WaveRNN](https://github.com/fatchord/WaveRNN)
* [https://github.com/xcmyz/LightSpeech](https://github.com/xcmyz/LightSpeech)
