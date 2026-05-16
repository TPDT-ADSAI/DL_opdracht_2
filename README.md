# Karaoke klassificatie 2026

Notebook voor Deep Learning Portfolioopdracht 2, team `groep 1 dh` (TPDT-ADSAI).

Het notebook werkt vijf onderdelen uit:

- Opdracht 1: exploratieve data analyse van audio, lyrics en genres.
- Opdracht 2: audio CRNN (Conv1D + Bi-LSTM) op MFCC + delta features.
- Opdracht 3: Bi-LSTM op opgeschoonde songteksten.
- Opdracht 4: DistilBERT fine-tuning op songteksten via Hugging Face.
- Opdracht 5: soft-voting ensemble van audio CRNN en DistilBERT.

## Bestanden

- `main.ipynb` hoofdnotebook met alle modellen, EDA, evaluatie en submission-generatie.
- `requirements.txt` Python dependencies.
- `models/` opgeslagen Keras-modellen (lokaal, niet alles in git).
- `submissions/` per model een CSV om handmatig op Kaggle te uploaden.

## Data

De Kaggle data staat **niet** in git. Twee opties:

1. Auto-download via Kaggle API (aanbevolen op RunPod). Zet `KAGGLE_USERNAME` en `KAGGLE_KEY` als env vars, cel 0 downloadt en unzipt de competition data automatisch naar `./data/karaoke-klassificatie-2026/`.
2. Handmatig: leg de dataset zelf in `./data/karaoke-klassificatie-2026/` naast `main.ipynb`.

```text
DL_opdracht_2/
  data/
    karaoke-klassificatie-2026/
      train.csv
      test.csv
      Train/
      Test/
```

Een ander pad kan via `KARAOKE_DATA_DIR`.

## Op RunPod

Geteste pods: **PyTorch 2.8.0** image op RTX 6000 Ada (48 GB) of RTX PRO 6000 (96 GB).

1. Start de pod met de PyTorch 2.8 template. `torch` + CUDA 12 zitten al in de image.
2. Zet environment variables in Pod -> Edit -> Environment:

   | Variabele | Doel | Default |
   | --- | --- | --- |
   | `KAGGLE_USERNAME` | Kaggle username, voor auto-download | leeg |
   | `KAGGLE_KEY` | Kaggle API key uit `kaggle.json` | leeg |
   | `KAGGLE_COMP` | competition slug | `karaoke-klassificatie-2026` |
   | `HF_TOKEN` | Hugging Face token, optioneel | leeg |
   | `AUDIO_OPTUNA_TRIALS` | aantal Optuna trials audio | 5 |
   | `LYRICS_OPTUNA_TRIALS` | aantal Optuna trials lyrics | 5 |

3. Open `main.ipynb` en draai **cel 0** (`RUNPOD_BOOTSTRAP`). Die installeert deps, schrijft `~/.kaggle/kaggle.json`, downloadt de competition data, en zet `KARAOKE_DATA_DIR`.
4. Draai de rest van het notebook van boven naar beneden.

> De cuDNN-RNN bug op deze image (`Dnn is not supported`) wordt omzeild doordat elke LSTM `recurrent_dropout>0` heeft, waardoor de TF fallback wordt gebruikt.

## Kaggle submission (handmatig)

Het notebook schrijft per model een CSV naar `submissions/`:

- `submissions/submission_audio_lstm.csv` voor Opdracht 2
- `submissions/submission_lyrics_lstm.csv` voor Opdracht 3
- `submissions/submission_transformer.csv` voor Opdracht 4
- `submissions/submission_ensemble.csv` voor Opdracht 5 (verwacht de hoogste score)

Upload deze handmatig via https://www.kaggle.com/competitions/karaoke-klassificatie-2026/submit en vul de public score in in sectie 6.3.

## Secrets

`kaggle.json`, `.env` en alle credentials staan in `.gitignore`. Commit ze nooit, ook niet per ongeluk. Gebruik altijd env vars op de pod.
