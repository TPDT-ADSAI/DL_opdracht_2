# Karaoke Klassificatie 2026

Deze repo bevat het notebook voor Deep Learning Portfolioopdracht 2. Het notebook werkt vijf onderdelen uit:

- Opdracht 1: Exploratieve Data Analyse van audio, lyrics en genres.
- Opdracht 2: LSTM-model op alleen audioclips.
- Opdracht 3: LSTM-model op alleen songteksten.
- Opdracht 4: Hugging Face-transformer fine-tuning op songteksten.
- Opdracht 5: Vrij gekozen soft-voting ensemble van audio en lyrics.

## Bestanden

- `main.ipynb`: hoofdnotebook met markdown, code, evaluatieplots, transformer-pijplijn en ensemble voor Opdracht 5.
- `requirements.txt`: Python dependencies.
- `models/`: opgeslagen Keras-modellen uit de eerdere LSTM-experimenten.
- `model_summary.txt`: tekstuele samenvatting van het audiomodel.

## Data

De Kaggle-data staat niet in git. De notebook zoekt de data automatisch op gangbare locaties, inclusief:

```text
C:\Users\fspar_7ib22z2\Downloads\karaoke-k-klassificatie-2026
```

Een andere locatie kan worden gebruikt door `KARAOKE_DATA_DIR` te zetten of een pad mee te geven aan `loading_data(path)`.

## Uitvoeren

Installeer dependencies:

```bash
pip install -r requirements.txt
```

Open daarna `main.ipynb` en voer de cellen in volgorde uit. Gebruik bij voorkeur de WSL GPU-kernel. De transformer-sectie downloadt `distilbert-base-uncased` via Hugging Face en kan op CPU merkbaar langer duren.

## Op RunPod

Geteste pod: **RunPod PyTorch 2.8.0**, 1x RTX 6000 Ada (48 GB VRAM, 62 GB RAM, 14 vCPU).

1. Start de pod met de PyTorch 2.8 template. `torch` + CUDA 12 zitten al in de image, dus `requirements.txt` pint torch niet.
2. Upload de dataset naar de pod, bijvoorbeeld in `/workspace/DL_opdracht_2/data/karaoke-k-klassificatie-2026/` (of in `data/` naast `main.ipynb`).
3. Open `main.ipynb` in Jupyter en draai **cel 0** (`RUNPOD_BOOTSTRAP`). Die installeert alle ontbrekende dependencies via pip en zet `KARAOKE_DATA_DIR` automatisch als `./data/` bestaat.
4. Draai de rest van het notebook van boven naar beneden.

Als de data ergens anders staat:
```bash
export KARAOKE_DATA_DIR=/workspace/elders/karaoke-k-klassificatie-2026
```

> opmerking: `tensorflow==2.17` en `torch` (van de image) draaien naast elkaar. De GPU wordt door beide herkend; `TF_FORCE_GPU_ALLOW_GROWTH=true` (al gezet in het notebook) voorkomt dat TF al het VRAM grijpt.
