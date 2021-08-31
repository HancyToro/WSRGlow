# WSRGlow

The official implementation of the Interspeech 2021 paper [*WSRGlow: A Glow-based Waveform Generative Model for Audio Super-Resolution*](https://arxiv.org/abs/2106.08507). Audio samples can be found [here](https://zkx06111.github.io/wsrglow/).

Feel free to create issues or send an email to [kexunz@zju.edu.cn](mailto:kexunz@zju.edu.cn) if you have problems running the code.

Before running the code, you need to install the dependicies by `pip install -r requirements.txt`.

The configs for model architecture and training scheme is saved in `config.yaml`. You can overwrite some of the attributes by adding the `--hparams` flag when running a command. The general way to run a python script is

`python $SRC$ --config $CONFIG$ --hparams $KEY1$=$VALUE1$,$KEY2$=$VALUE2$,...`

See `hparams.py` for more details.

### To prepare data

Before training, you need to binarize the data first. The raw wav files should be put in the `hparams['raw_data_path']`. The binarized data would be put in the `hparams['binary_data_path']`.

Specifically, for the VCTK corpus, the file structure should be like

```
.
|--data
    |--raw
        |--VCTK-Corpus
            |--wav48
                |--$WAVS
|--checkpoints
    |--wsrglow
    
```

where the model checkpoints are in `checkpoints/wsrglow`.

The command to binarize is

`python binarizer.py --config config.yaml`

### To modify the architecture of the model

The current WSRGlow model in `model.py` is designed for x4 super-resolution and takes waveform, spectrogram and phase information as input.

### To train

Run `python train.py --config config.yaml` on a GPU.

### To infer

Change the code in `infer.py` to specify the checkpoint you want to load and the sample inputs you want to use for inference.
Run `python infer.py --config config.yaml` on a GPU, modify the code for the correct path of checkpoints and wav files.

### Colab Sample

You can experiment with the colab sample and trained checkpoint [here](https://colab.research.google.com/drive/1uJ9bcUdK3VUwWYt0aU1C1mXAXp6JzCLh?usp=sharing).

Note that the released checkpoint is trained for 2x super-resolution. You should select the GPU runtime to run the sample.

`p225_001_lr.wav` and `p225_001_hr.wav` are the LR version and HR version of the same utterance taken from the test set.