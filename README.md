[README.md](https://github.com/user-attachments/files/21960784/README.md)
# SignVisionGTSRB
📄 Beispiel-Ausgaben: [Colab-Run mit Outputs](docs/SignVisionGTSRB_Colab_Outputs.pdf)

**Verkehrszeichenerkennung mit CNN (GTSRB-Datensatz)**

Dieses Projekt implementiert ein Convolutional Neural Network (CNN) zur Erkennung deutscher Verkehrsschilder basierend auf dem **German Traffic Sign Recognition Benchmark (GTSRB)**.

---

## Features
- Laden und Vorbereiten der GTSRB-Daten (CSV oder Ordnerstruktur)  
- Datenaufbereitung inkl. Normalisierung & Augmentierung  
- Training eines CNN mit Keras/TensorFlow  
- Validierung & Test mit Confusion-Matrix  
- Speichern & Laden trainierter Modelle (`.keras`)  
- Notebook-Variante (`notebooks/SignVisionGTSRB.ipynb`)  
- Python-CLI-Variante (`src/`)  

---

## Getting Started

### Voraussetzungen
- Python 3.10 oder neuer  
- Virtuelle Umgebung empfohlen  
- Pakete siehe `requirements.txt`  

### Installation
```
git clone https://github.com/<dein-user>/SignVisionGTSRB.git
cd SignVisionGTSRB
python -m venv .venv
source .venv/bin/activate   # Windows: .venv\Scripts\activate
pip install -r requirements.txt
```

---

## Training starten (Beispiel)
```
python src/train.py --data-root ./data --epochs 15 --batch-size 64
```
- `--data-root` : Pfad zum GTSRB-Datensatz  
- `--epochs` : Anzahl Trainings-Epochen (Standard: 10–15)  
- `--batch-size` : Größe der Batches (Standard: 64)  
- Ergebnisse werden im Ordner `models/` gespeichert  

---

## Inferenz (Einzelbild)
```
python src/infer.py --image ./testbild.png --model models/latest.keras
```
- `--image` : Pfad zum Bild, das klassifiziert werden soll  
- `--model` : Pfad zu einem gespeicherten `.keras`-Modell  
- Ausgabe: erkannte Klasse + Wahrscheinlichkeit  

---

## Projektstruktur
```
SignVisionGTSRB/
├─ notebooks/            # Jupyter/Colab Notebooks
│   └─ SignVisionGTSRB.ipynb
├─ src/                  # Python-Quellcode (Model, Training, Inferenz)
│   ├─ data.py
│   ├─ model.py
│   ├─ train.py
│   ├─ infer.py
│   └─ utils.py
├─ models/               # gespeicherte Modelle (.keras)
├─ data/                 # Trainings-/Testdaten (nicht ins Repo pushen!)
├─ requirements.txt      # Abhängigkeiten
├─ README.md
├─ LICENSE
└─ THIRD_PARTY_LICENSES.md
```

---

## Datenquelle
- **GTSRB Dataset** – German Traffic Sign Recognition Benchmark  
  🔗 https://benchmark.ini.rub.de/gtsrb_news.html  

Hinweis: Die Original-Daten werden **nicht ins Repo hochgeladen** (Lizenz & Dateigröße). Bitte lade sie separat herunter und lege sie lokal in `./data/` ab.

---

## Lizenz
- Projektlizenz: MIT License (`LICENSE`)  
- Drittanbieter-Lizenzen: siehe `THIRD_PARTY_LICENSES.md`  
