# ITNPA4-34 Assessments (2026): Questions 1–4

## Project overview

This project analyses research abstracts and research articles using Python. It contains **four Jupyter notebooks** and **one Streamlit web application**.

| Question | What the design does | How to run it |
|---|---|---|
| **Question 1** | Cleans research abstracts, creates TF-IDF features, and evaluates a Naive Bayes baseline classifier. | Jupyter Notebook |
| **Question 2** | Compares classification models, tunes a Random Forest model, saves the trained classifier, and provides a Streamlit prediction interface. | Jupyter Notebook and Streamlit |
| **Question 3** | Cleans five research articles and produces summaries, word-frequency visuals, word clouds, and a TextRank summary. | Jupyter Notebook |
| **Question 4** | Uses LDA to discover topics in the five articles and creates an interactive topic-distance map. | Jupyter Notebook; output HTML file |

**Important:** Only **Question 2** has a web app (`app.py`). Questions 1, 3, and 4 are analysis notebooks, not separate websites. The web app uses the trained model supplied in the project; it does not rerun all four notebooks.

## 1. Project files

Keep these files together in the **same extracted project folder**:

```text
ITNPA4-34 Assessments (2026) 2/
├── ITNPA Question1.ipynb
├── ITNPA Question2.ipynb
├── ITNPA Question3.ipynb
├── ITNPA Question4.ipynb
├── MAFUMA MODIEGI ITNPA PROJECT 1 Doc.pdf
└── README.md
```

- `research_abstracts.json` is used by Questions **1 and 2**.
- `research_corpus.zip` contains five `.txt` articles and is used by Questions **2 (test predictions), 3, and 4**. **Do not unzip this smaller corpus file:** the notebooks read the text directly from it.
- `abstract_classifier.pkl` is the **already-trained model** used by `app.py`.
- `lda_intertopic_map.html` is **created after Question 4 runs**. It is not part of the original files.
- `.ipynb_checkpoints/`, if visible, is an automatic Jupyter backup folder and can be ignored.

## 2. Requirements

- A computer with **Python 3.11** installed (recommended).
- Internet access for the **first installation** and downloading NLTK language resources.
- A terminal (Command Prompt, PowerShell, Terminal, or VS Code terminal).
- A browser to open Jupyter and the Streamlit app.

### Step A: Extract and open the project

1. Extract the downloaded **ITNPA4-34 Assessments (2026) 2.zip** file.
2. Open the extracted folder in **VS Code**, or open a terminal **inside that folder**.
3. Check that `app.py`, `requirements.txt`, and the four `.ipynb` files are in the folder you opened.

> **Why this matters:** The code uses relative file names such as `research_abstracts.json` and `abstract_classifier.pkl`. Running it from another folder can cause **FileNotFoundError**.

### Step B: Install the Python packages

**Windows — PowerShell or Command Prompt:**

```powershell
py -3.11 -m venv .venv
.\.venv\Scripts\python.exe -m pip install --upgrade pip
.\.venv\Scripts\python.exe -m pip install -r requirements.txt
.\.venv\Scripts\python.exe -m nltk.downloader stopwords wordnet punkt punkt_tab averaged_perceptron_tagger_eng
```

This uses the virtual environment directly, so you do **not** have to activate it or change PowerShell security settings.

**macOS / Linux:**

```bash
python3.11 -m venv .venv
source .venv/bin/activate
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
python -m nltk.downloader stopwords wordnet punkt punkt_tab averaged_perceptron_tagger_eng
```

If Python 3.11 is not available, install it first. All packages used by the four questions are listed in `requirements.txt`.

## 3. Run Questions 1–4 in Jupyter

**Windows:**

```powershell
.\.venv\Scripts\python.exe -m notebook
```

**macOS / Linux (with the virtual environment active):**

```bash
python -m notebook
```

Jupyter should open in your browser (usually at `http://localhost:8888`). Open a notebook and select the Python environment you installed above. Choose **Run → Run All Cells** or run the cells from top to bottom.

**Recommended order:**

1. **Question 1:** Open `ITNPA Question1.ipynb`. You should see data cleaning, a TF-IDF feature matrix, and classification results.
2. **Question 2:** Open `ITNPA Question2.ipynb`. You should see the model comparison, tuning results, and a saved `abstract_classifier.pkl` file. **The notebook already contains code to overwrite `app.py` and `abstract_classifier.pkl`** when you run all its cells. The trained model and app are supplied, so rerunning this notebook is **not required** just to open the web app. Model tuning performs a grid search and is more computationally demanding than the other steps.
3. **Question 3:** Open `ITNPA Question3.ipynb`. You should see cleaned articles, the first-article summary, the combined TextRank summary, and related graphs/word clouds.
4. **Question 4:** Open `ITNPA Question4.ipynb`. You should see LDA topic results and charts. At the end, the notebook saves **`lda_intertopic_map.html`** in the project folder. Open this HTML file in a browser to interact with the topic map.

The notebooks can be opened independently because each loads its own source data. Running them in the suggested order makes the assessment easier to follow.

## 4. Deploy and use the Question 2 Streamlit app locally

You **do not need to train a model first** because `abstract_classifier.pkl` is already included.

Open a **new terminal in the extracted project folder** and run:

**Windows:**

```powershell
.\.venv\Scripts\python.exe -m streamlit run app.py
```

**macOS / Linux:**

```bash
python -m streamlit run app.py
```

1. Your browser should open **http://localhost:8501**.
2. Type or paste a research abstract into the text box.
3. Select **Classify Abstract**.
4. The app predicts **artificial intelligence** or **classical research**.
5. To stop the app, return to the terminal and press **Ctrl+C**.

### Quick deployment test

Paste this sample text into the app:

> This paper studies machine learning methods, neural networks and artificial intelligence techniques for classifying research articles.

Click **Classify Abstract**. The app should display a classification result without an error. The prediction depends on the trained model and is not guaranteed to be a specific class for every sample.

## 5. Optional: Publish the Streamlit app online

To let someone use **Question 2's app** without installing Python:

1. Create a GitHub repository and upload at least `app.py`, `abstract_classifier.pkl`, and `requirements.txt` to the repository root.
2. Open **[Streamlit Community Cloud](https://share.streamlit.io/)** and sign in.
3. Choose to create a new app from your GitHub repository.
4. Set the main app file to **`app.py`** and deploy.
5. When deployment succeeds, open the generated URL and try a sample abstract.

The app downloads NLTK `stopwords` and `wordnet` at startup, so its hosting environment needs access to those resources on the first run. If the saved model cannot load because of different scikit-learn versions, use matching package versions or regenerate the `.pkl` model from Question 2 in the deployment environment.

**Only the Streamlit classifier becomes a website.** To share Question 4's interactive map, run its notebook first and share the generated `lda_intertopic_map.html` separately. Questions 1 and 3 are demonstrated through their notebook results.

**Privacy:** Do not upload private datasets or confidential research papers to a public GitHub repository.

## 6. Common errors and simple fixes

| Problem | Solution |
|---|---|
| `ModuleNotFoundError` | Install the packages using the commands in Step B. Make sure Jupyter uses the same `.venv` Python environment. |
| `FileNotFoundError: research_abstracts.json` or `research_corpus.zip` | Open the terminal/Jupyter **in the project folder**. Keep the data files alongside the notebooks. |
| `FileNotFoundError: abstract_classifier.pkl` | Keep the supplied `.pkl` next to `app.py`, or rerun the model-saving cell in Question 2. |
| NLTK `LookupError` for `punkt_tab`, `stopwords`, `wordnet`, or POS tagger | Run the NLTK downloader command from Step B, then restart the notebook kernel/app. |
| Error loading the `.pkl` model or unexpected scikit-learn warning | The saved model may have been created with a different scikit-learn version. Use a compatible version, or rerun Question 2 to save the model using the currently installed version. Only load model files from trusted sources. |
| `streamlit` is not recognised | Use `python -m streamlit run app.py` (or the Windows `.venv` version above) rather than calling `streamlit` directly. |
| `Address already in use` on port 8501 | Stop the other running Streamlit process with **Ctrl+C**, or use `python -m streamlit run app.py --server.port 8502`. |
| Question 4 has no interactive HTML output | Run the Question 4 notebook from top to bottom and check the project folder for `lda_intertopic_map.html`. |


**Project purpose:** To demonstrate text preprocessing, classification, summarisation and topic modelling of research documents, and to make the trained research abstract classifier available through a simple web interface.
