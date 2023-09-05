# Analyze tracks in major

## [Carver Commodore - Drown Me In Emotions](https://www.youtube.com/watch?v=bLaipK9lisc)

- Found in everynoise's scan. Feels like it's in major.
- [Search for chords](https://www.google.com/search?q=Carver+Commodore+-+Drown+Me+In+Emotions+chords). 
- Found [chordify](https://chordify.net/chords/carver-commodore-drown-me-in-emotions-official-music-video-carver-commodore) - it's auto chords. It's a rare track, so neither midi nor human-entered chords.
- It's in E Major, because if we assume that, we get verse IV-I-V and chorus I-(iii)-ii-V, pretty straightforward.
- How do we extract the melody? Let's try demucs and RipX.
- `youtube-dl -x --audio-format "best" --audio-quality 0 --embed-thumbnail --add-metadata https://www.youtube.com/watch\?v\=bLaipK9lisc`
- [Stem Separation Comparison Dec 2022](https://www.youtube.com/watch?v=gl5AKCgMSSc)
   - Start with [demucs](https://github.com/facebookresearch/demucs) as it's free and cli-based
- What do we want to extract from this track? Drums, bass guitar, vocals. Can we separate [two guitars](https://www.youtube.com/watch?v=h6ytkmZEEUU) - lead from rhythm?
- Then feed the output of demucs to [Basic Pitch](https://basicpitch.spotify.com/) (bass)
- Try [Omnizart for drums](). Omnizart uses spleeter under the hood, and maybe replacing it with demucs can give better results.
   - Also [MT3](https://github.com/magenta/mt3)
   - Also see [MusicNetEM](https://benadar293.github.io/)
   - `omnizart beat` can't run on Replicate
- For piano: either [bytedance](https://github.com/bytedance/piano_transcription) or "Onsets and Frames"
- Also try RipX
- Merge midi files:
   - Caveat: Basic Pitch produces midi with resolution 480, whereas omnizart outputs in 220. Merging them can lead to errors when using online tools
   - Can merge midi tracks in Ableton
   - Can also use [midisox](https://pjb.com.au/midi/midisox.html)
- Unplayable drum midi tracks is fixed by copy-pasting drum track onto a fresh track in signal. Probably, some important setup midi messages are created this way
- Maybe check ISMIR Slack
- [Docker installation for cog on Ubuntu](https://docs.docker.com/engine/install/ubuntu/)
- Can probably use [WaveBeat](https://github.com/csteinmetz1/wavebeat) for downbeat estimation - instead of omnizart beat
   - Run on Ubuntu 20.04 with python3.8, numpy==1.19 and madmom==0.16.1 recompiled after installing numpy. [Installation](https://gist.github.com/vpavlenko/6d88bd19b4017c0bf63d70ca5a9738e7)

### Automatic drum transription

Options:
- [Magenta OaF Drums](https://magenta.tensorflow.org/oaf-drums)
- [Omnizart: adt_with_a2md](https://replicate.com/e7mac/omnizart)

### Chords

[Omnizart](https://replicate.com/e7mac/omnizart) on the original file.

## Singing

Can we sing something on this meeting?


# Obsolete notes

## Install omnizart

If fails due to PyYAML: [run this](https://github.com/yaml/pyyaml/issues/601#issuecomment-1693730229). (It also fails on colab).

I try on `pyenv global 3.8.10`.

`python3 -m pip install tensorflow-macos`

Maybe I should fix omnizart installation right in a colab.

Try on Colab. The issue: since May 2023, the default colab python is 3.10, and the original colab for omnizart is for 3.8. So there are two options:
- try to port it to 3.10 (which will be obsolete in 1-2 years again)
- try to bring the env version back to 3.8 (which requires installing an old ipykernel)

### Port it to 3.10

P
madmom 0.16 will crash on `from collections import MutableSequence`

### Bring env to 3.8

Find the right ipykernel install commands.

### wavebeat hosting prompt

```
I want to make a cog to host a wavebeat model on Replicate.

I think that I should prepare two files: cog.yaml and scripts/predict.py

Let's look at what another ML model, omnizart, does to host:

omnizart/cog.yaml:

build:
  gpu: true
  python_version: "3.8"
  system_packages:
    - "libgl1-mesa-glx"
    - "libglib2.0-0"
    - "libsndfile1-dev"
    - "ffmpeg"
  python_packages:
    - "ipython==7.30.1"
    - "numpy==1.21.4"
  run:
    - pip install -U pip
    - pip install --upgrade cython
    - pip install omnizart
    - apt-get update && apt-get install -y fluidsynth
    - pip install pyfluidsynth

predict: "scripts/predict.py:Predictor"

omnizart/scripts/predict.py:

"""
To push this predictor to replicate.com, first run download_checkpoints() and save files to omnizart/checkpoints.
Then run cog push. Further documentation can be found at https://replicate.com/docs
"""

import os
import tempfile
import subprocess
import shutil
from pathlib import Path

import cog
import scipy.io.wavfile as wave

from omnizart.remote import download_large_file_from_google_drive
from omnizart.beat import app as bapp
from omnizart.chord import app as capp
from omnizart.drum import app as dapp
from omnizart.music import app as mapp
from omnizart.vocal import app as vapp
from omnizart.vocal_contour import app as vcapp


class Predictor(cog.Predictor):
    def setup(self):
        self.SF2_FILE = "general_soundfont.sf2"
        if not os.path.exists(self.SF2_FILE):
            print("Downloading soundfont...")
            download_large_file_from_google_drive(
                "https://ftp.osuosl.org/pub/musescore/soundfont/MuseScore_General/MuseScore_General.sf2",
                file_length=215614036,
                save_name=self.SF2_FILE,
            )
        self.app = {"music": mapp, "chord": capp, "drum": dapp, "vocal": vapp, "vocal-contour": vcapp, "beat": bapp}
        self.model_path = {"piano": "Piano", "piano-v2": "PianoV2", "assemble": "Stream", "pop-song": "Pop", "": None}

    @cog.input(
        "audio",
        type=Path,
        help="Path to the input music. Supports mp3 and wav format.",
    )
    @cog.input(
        "mode",
        type=str,
        default="music-piano-v2",
        options=["music-piano", "music-piano-v2", "music-assemble", "chord", "drum", "vocal", "vocal-contour", "beat"],
        help="Transcription mode",
    )
    def predict(self, audio, mode):
        assert str(audio).endswith(".mp3") or str(audio).endswith(".wav"), "Please upload mp3 or wav file."
        temp_folder = "cog_temp"
        os.makedirs(temp_folder, exist_ok=True)
        try:
            audio_name = str(os.path.splitext(os.path.basename(audio))[0])
            if str(audio).endswith(".wav"):
                wav_file_path = str(audio)
            else:
                wav_file_path = f"{temp_folder}/{audio_name}.wav"
                subprocess.run(["ffmpeg", "-y", "-i", str(audio), wav_file_path])
            model = ""
            if mode.startswith("music"):
                mode_list = mode.split("-")
                mode = mode_list[0]
                model = "-".join(mode_list[1:])

            app = self.app[mode]
            model_path = self.model_path[model]
            midi = app.transcribe(wav_file_path, model_path=model_path)

            if mode == "vocal-contour":
                out_name = f"{audio_name}_trans.wav"
            else:
                print("Synthesizing MIDI...")
                out_name = f"{temp_folder}/{audio_name}_synth.wav"
                raw_wav = midi.fluidsynth(fs=44100, sf2_path=self.SF2_FILE)
                wave.write(out_name, 44100, raw_wav)

            out_path = Path(tempfile.mkdtemp()) / "out.mp3"  # out_path is automatically cleaned up by cog
            subprocess.run(["ffmpeg", "-y", "-i", out_name, str(out_path)])
        finally:
            shutil.rmtree(temp_folder)
            if os.path.exists(f"{audio_name}.mid"):
                os.remove(f"{audio_name}.mid")
            if os.path.exists(f"{audio_name}_trans.wav"):
                os.remove(f"{audio_name}_trans.wav")
        return out_path

now let's see what we have in wavebeat repo:

csteinmetz1 Merge pull request #1 from nicolasanjoran/main
…
cfb9ed9
on Nov 11, 2021
Git stats
 71 commits
Files
Type
Name
Latest commit message
Commit time
checkpoints
adding link to pre-trained model on Zenodo
2 years ago
docs/resources
updating links
2 years ago
util
script to write out simple beat format for gtzan
2 years ago
wavebeat
fix: pass use_gpu param to the predict_beats function
2 years ago
.gitignore
adding webpage and updating pdf
2 years ago
LICENSE
Initial commit
2 years ago
README.md
adding link to arXiv paper
2 years ago
predict.py
adding detail about 3.8 and remove import from predict.py
2 years ago
requirements.txt
adding improvements for macOS support in requirements
2 years ago
setup.py
finalizing the interface
2 years ago
simple_test.py
removing extra models
2 years ago
train.py
removing extra models
2 years ago
train_cv.py
training scripts for cross validation as well as multi-dataset
2 years ago
README.md
WaveBeat
End-to-end beat and downbeat tracking in the time domain.

| Paper | Code | Video | Slides |


Setup
First clone the repo.

git clone https://github.com/csteinmetz1/wavebeat.git
cd wavebeat
Setup a virtual environment and activate it. This requires that you use Python 3.8.

python3 -m venv env/
source env/bin/activate
Next install numpy, cython, and aiohttp first, manually.

pip install numpy cython aiohttp
Then install the wavebeat module.

python setup.py install
This will ensure that madmom installs properly, as it currently fails unless cython, numpy, and aiohttp are installed first.

Predicting beats
To begin you will first need to download the pre-trained model here. Place it in the checkpoints/ directory, rename to get the .ckpt file.

cd checkpoints
wget https://zenodo.org/record/5525120/files/wavebeat_epoch%3D98-step%3D24749.ckpt?download=1
mv wavebeat_epoch=98-step=24749.ckpt?download=1 wavebeat_epoch=98-step=24749.ckpt
Functional interface
If you would like to use the functional interface you can create a script and import wavebeat as follows.

from wavebeat.tracker import beatTracker

beat, downbeats = beatTracker('audio.wav')
Script interface
We provide a simple script interface to load an audio file and predict the beat and downbeat locations with a pre-trained model. Run the model by providing a path to an audio file.

python predict.py path_to_audio.wav

wavebeat/predict.py:

import os
import glob
import torch
import torchaudio
import pytorch_lightning as pl
from argparse import ArgumentParser

from wavebeat.dstcn import dsTCNModel

parser = ArgumentParser()
parser.add_argument('input', type=str)
parser.add_argument('--model', type=str, default="checkpoints/")

args = parser.parse_args()

# find the checkpoint path
ckpts = glob.glob(os.path.join(args.model, "*.ckpt"))
if len(ckpts) < 1:
    raise RuntimeError(f"No checkpoints found in {args.model}.")
else:
    ckpt_path = ckpts[-1]

# construct the model, and load weights from checkpoint
model = dsTCNModel.load_from_checkpoint(ckpt_path)

# set model to eval mode
model.eval()

# get the locations of the beats and downbeats
beats, downbeats = model.predict_beats(args.input)

# print some results to terminal
print(f"Beats found in {args.input}")
print("-" * 32)
for beat in beats:
    print(f"{beat:0.2f}")

print()
print(f"Downbeats found in {args.input}")
print("-" * 32)
for downbeat in downbeats:
    print(f"{downbeat:0.2f}")

as I yesterday played with installing and running wavebeat on a fresh VPS, I found this setup working (some steps are redundant and can be squashed):

Run on Ubuntu 20.04 with python3.8, numpy==1.19 and madmom==0.16.1 recompiled after installing numpy.

# history
    1  apt update
    2  python3.8 
    3  git clone https://github.com/csteinmetz1/wavebeat.git
    4  cd wavebeat
    5  python3 -m venv env/
    6  source env/bin/activate
    7  apt install python3.8-venv
    8  alias apt='apt -y'
    9  python3 -m venv env/
   10  source env/bin/activate
   11  pip install numpy cython aiohttp
   12  python setup.py install
   13  pip install scipy==1.11.2
   14  pip install scipy==1.10.1
   15  python setup.py install
   16  pip --version
   17  cat requirements.txt | grep mat
   18  pip install matplotlib==3.3.4
   19  python setup.py install
   20  apt install gcc python3.8-dev
   21  python setup.py install
   22  python3 predict.py /tmp/Carver\ Commodore\ -\ Drown\ Me\ In\ Emotions-bLaipK9lisc.mp3 
   23  ack np.float
   24  apt install ack
   25  ack np.float
   26  pip freeze
   27  cat requirements.txt 
   28  pip uninstall numpy
   29  pip install numpy==1.19
   30  pip install numpy==1.19.5
   31  python3 predict.py /tmp/Carver\ Commodore\ -\ Drown\ Me\ In\ Emotions-bLaipK9lisc.mp3 
   32  pip uninstall madmom
   33  pip install madmom==0.16.1
   34  python3 predict.py /tmp/Carver\ Commodore\ -\ Drown\ Me\ In\ Emotions-bLaipK9lisc.mp3 
   35  cd checkpoints/
   36  ll
   37  wget https://zenodo.org/record/5525120/files/wavebeat_epoch%3D98-step%3D24749.ckpt?download=1
   38  mv wavebeat_epoch=98-step=24749.ckpt?download=1 wavebeat_epoch=98-step=24749.ckpt
   39  python3 predict.py /tmp/Carver\ Commodore\ -\ Drown\ Me\ In\ Emotions-bLaipK9lisc.mp3 
   40  cd ..
   41  python3 predict.py /tmp/Carver\ Commodore\ -\ Drown\ Me\ In\ Emotions-bLaipK9lisc.mp3 
   42  python3 predict.py /tmp/Carver\ Commodore\ -\ Drown\ Me\ In\ Emotions-bLaipK9lisc.mp3 > wavebeat.txt
```
