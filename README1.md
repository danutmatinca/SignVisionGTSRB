# SignVisionGTSRB

**Verkehrszeichenerkennung mit CNN (GTSRB-Datensatz)**

Dieses Projekt implementiert ein Convolutional Neural Network (CNN) zur Erkennung deutscher Verkehrsschilder basierend auf dem **German Traffic Sign Recognition Benchmark (GTSRB)**.  
Es enthält ein ausführbares Notebook sowie Anleitungen für Colab, Binder, GitHub Codespaces und die lokale Nutzung – inkl. klarer Schritte zum Download der GTSRB-Daten (Kaggle API).
---
## Beispiel-Ausgaben
Für eine komplette Übersicht, wie das Notebook ausgeführt wird und welche Ergebnisse (Accuracy, Confusion Matrix, Plots etc.) entstehen, siehe:

➡️ [Colab-Run mit Outputs](docs/SignVisionGTSRB_Colab_Outputs.pdf)
---

## Features

- Datenimport aus GTSRB (Kaggle) – CSV/Ordner-Struktur
- Daten-Pipeline inkl. Normalisierung & (optional) Augmentierung
- CNN-Modell (Keras/TensorFlow)
- Training mit Validation, Checkpoints & EarlyStopping
- Auswertung (Accuracy, Confusion Matrix, Beispiel-Vorhersagen)
- Speichern/Laden trainierter Modelle (`.keras`)
- **Notebook** (direkt ausführbar)
- **Python-Variante** (vorbereitet, optional in `src/` erweiterbar)
- Beispielausgaben als PDF: `docs/SignVisionGTSRB_Colab_Outputs.pdf`

---

## Schnell testen – im Browser

### ▶️ Mit Google Colab testen
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/danutmatinca/SignVisionGTSRB/blob/main/SignVisionGTSRB.ipynb)  
- Benötigt einen **Google-Account**.
- Läuft sofort im Browser, optional mit GPU/TPU (kostenlos, limitiert).
- Keine lokale Installation nötig.

### ▶️ Mit Binder testen
[![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/danutmatinca/SignVisionGTSRB/HEAD?filepath=SignVisionGTSRB.ipynb)  
- **Kein Login erforderlich.**
- Start kann 1–2 Minuten dauern (Umgebung wird gebaut).
- Änderungen gehen nach der Session verloren.

### ▶️ Mit GitHub Codespaces testen
- In GitHub: **Code → Open with Codespaces**.
- Benötigt **GitHub-Account**.
- Vollwertige Cloud-IDE (VS Code im Browser), Freikontingent zeitlich limitiert.

---

## Notebook & Beispielausgaben

- Notebook: `SignVisionGTSRB.ipynb` (Repo-Root)
- Beispiel-Outputs (Accuracy, Confusion Matrix, Plots):  
   `docs/SignVisionGTSRB_Colab_Outputs.pdf`

---

## GTSRB-Daten beziehen (Kaggle)

Du hast zwei Wege: **(A) Colab + Kaggle API** (empfohlen) oder **(B) Download über Website & lokal ablegen**.

### A) Kaggle API in Google Colab (empfohlen)

1. **Kaggle-API-Token erzeugen**
   - Bei Kaggle einloggen → Profil-Icon → **Account** → Bereich **API** → **Create New API Token**  
   - Es wird eine Datei `kaggle.json` heruntergeladen.

2. **`kaggle.json` in Colab hochladen & konfigurieren**
   ```python
   from google.colab import files
   files.upload()  # wähle deine kaggle.json
   ```
   ```bash
   mkdir -p ~/.kaggle
   cp kaggle.json ~/.kaggle/
   chmod 600 ~/.kaggle/kaggle.json
   ```

3. **GTSRB-Dataset per API laden & entpacken**
   ```bash
   kaggle datasets download -d meowmeowmeowmeowmeow/gtsrb-german-traffic-sign
   unzip -q gtsrb-german-traffic-sign.zip -d ./data
   ```
   Danach liegt der Datensatz unter `./data/` (z. B. `data/Train`, `data/Test`, `data/Meta`).

> **Wichtig:** Die Inhalte der `kaggle.json` dürfen nicht ins Repo. Nutze `.gitignore` (siehe unten).

### B) Download über die Website (lokal)

1. Öffne: https://www.kaggle.com/datasets/meowmeowmeowmeowmeow/gtsrb-german-traffic-sign  
2. Mit Kaggle-Account einloggen → **Download**.  
3. ZIP lokal entpacken und den Inhalt in deinen Projektordner `data/` legen (nicht ins Repo pushen).

---

## Projekt lokal ausführen

### Voraussetzungen
- Python 3.10+  
- Virtuelle Umgebung empfohlen

### Installation
```bash
git clone https://github.com/danutmatinca/SignVisionGTSRB.git
cd SignVisionGTSRB
python -m venv .venv
# Linux/macOS:
source .venv/bin/activate
# Windows:
# .venv\Scripts\activate

pip install -r requirements.txt
```

### Notebook lokal starten
```bash
jupyter notebook SignVisionGTSRB.ipynb
```

> Stelle sicher, dass der Datensatz im Ordner `./data/` liegt (siehe oben).

---

### Python-Variante ohne Notebook

Falls du die Python-CLI nutzen möchtest (später erweiterbar, z. B. in `src/`):

- **Training (Beispiel)**  
  ```bash
  python src/train.py --data-root ./data --epochs 15 --batch-size 64
  ```
  Ergebnisse/Modelle landen in `models/`.

- **Inferenz (Einzelbild)**  
  ```bash
  python src/infer.py --image ./testbild.png --model models/latest.keras
  ```
  Ausgabe: Klasse + Wahrscheinlichkeit.

> Hinweis: Die Dateien `src/data.py`, `src/model.py`, `src/train.py`, `src/infer.py` sind als Struktur vorgesehen und können schrittweise befüllt/erweitert werden.

---

## Repository-Struktur (Empfehlung)

```
SignVisionGTSRB/
├─ SignVisionGTSRB.ipynb        # Notebook (Root)
├─ docs/
│   └─ SignVisionGTSRB_Colab_Outputs.pdf
├─ data/                        # GTSRB-Daten (nicht committen)
│   └─ .gitkeep
├─ models/                      # Trainierte Modelle (nicht committen)
│   └─ .gitkeep
├─ src/                         # (optional) Python-Variante/Module
│   ├─ data.py
│   ├─ model.py
│   ├─ train.py
│   └─ infer.py
├─ requirements.txt
├─ .gitignore
├─ LICENSE
├─ THIRD_PARTY_LICENSES.md
└─ README.md
```

**.gitignore (wichtig)** sollte u. a. enthalten:
```
# Secrets/Umgebungen
.env
kaggle.json

# Jupyter
.ipynb_checkpoints/

# Daten/Modelle
data/
models/
outputs/

# Python/Cache
__pycache__/
*.py[cod]
*.egg-info/

# OS/IDE
.DS_Store
Thumbs.db
.idea/
.vscode/
```

---

## Sicherheit & gute Praxis

- **API-Keys/`kaggle.json` niemals committen.**  
- Notebook-Ausgaben vor dem Commit prüfen (keine Geheimnisse anzeigen).  
- Für reproduzierbare Runs: `requirements.txt` aktuell halten.

---

## Datenquelle & Lizenzen

- **GTSRB Dataset** – German Traffic Sign Recognition Benchmark  
  https://benchmark.ini.rub.de/gtsrb_news.html  
  (Kaggle-Mirror: `meowmeowmeowmeowmeow/gtsrb-german-traffic-sign`)

- **Lizenz dieses Projekts:** siehe [`LICENSE`](LICENSE) (MIT)  
- **Drittanbieter-Lizenzen:** siehe [`THIRD_PARTY_LICENSES.md`](THIRD_PARTY_LICENSES.md)

---

## Support

Fragen oder Vorschläge?  
Issues & Diskussionen gern über GitHub **Issues** im Repo.

--- 

*Viel Erfolg und viel Spaß beim Trainieren & Testen! 
