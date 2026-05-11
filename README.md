# Karaoke Klassificatie 2026

Deze repo bevat het notebook voor Deep Learning Portfolioopdracht 2. Het notebook werkt vier onderdelen uit:

- Opdracht 1: Exploratieve Data Analyse van audio, lyrics en genres.
- Opdracht 2: LSTM-model op alleen audioclips.
- Opdracht 3: LSTM-model op alleen songteksten.
- Opdracht 4: Hugging Face-transformer fine-tuning op songteksten.

## Bestanden

- `main.ipynb`: hoofdnotebook met markdown, code, bestaande outputs en de transformer-pijplijn.
- `requirements.txt`: Python dependencies.
- `models/`: opgeslagen Keras-modellen uit de eerdere LSTM-experimenten.
- `model_summary.txt`: tekstuele samenvatting van het audiomodel.

## Data

De Kaggle-data staat niet in git. De notebook zoekt de data automatisch op gangbare locaties, inclusief:

```text
C:\Users\fspar_j8qt2o6\Downloads\karaoke-k-klassificatie-2026
```

Een andere locatie kan worden gebruikt door `KARAOKE_DATA_DIR` te zetten of een pad mee te geven aan `loading_data(path)`.

## Uitvoeren

Installeer dependencies:

```bash
pip install -r requirements.txt
```

Open daarna `main.ipynb` en voer de cellen in volgorde uit. De transformer-sectie downloadt `distilbert-base-uncased` via Hugging Face en kan op CPU merkbaar langer duren.
