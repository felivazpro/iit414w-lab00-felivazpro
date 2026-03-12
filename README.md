# IIT414W · Lab 00 — Setup and Orientation

> **Note on this file:** This README was drafted with the assistance of GitHub Copilot. I provided the necessary details (system info, steps followed, problems encountered, and expected outputs), and the AI helped structure them into the required format.

| Field | Value |
|---|---|
| **Full name** | Felipe Vazquez |
| **GitHub username** | felivazpro |
| **Course** | IIT414W |
| **Date** | March 11, 2026 |

---

## System Info

| Field | Value |
|---|---|
| **Operating system** | Microsoft Windows 11 Home Single Language (10.0.26200) |
| **Python version** | 3.14.3 |
| **pip version** | 26.0.1 |

> Python is managed via **uv**. There is no conda environment — dependencies are installed directly with pip into a virtual environment.

---

## Setup Instructions

Follow these steps exactly in order. Commands are for **PowerShell** on Windows.

> **Prerequisite:** Git must be installed. Download from https://git-scm.com if not already present. After installing, restart your terminal.

### 1. Create a virtual environment

```powershell
python -m venv .venv
```

### 2. Activate the virtual environment

```powershell
.\.venv\Scripts\Activate.ps1
```

You should see `(.venv)` appear at the start of your prompt.

> If PowerShell blocks the script, run this first:
> ```powershell
> Set-ExecutionPolicy -Scope CurrentUser -ExecutionPolicy RemoteSigned
> ```

### 3. Install dependencies

```powershell
pip install -r requirements.txt
```

### 4. Register the environment as a Jupyter kernel

```powershell
pip install ipykernel
python -m ipykernel install --user --name iit414w --display-name "Python (iit414w)"
```

### 5. Open VS Code in the project folder

```powershell
code .
```

Select **Python (iit414w)** as the kernel when opening either notebook.

---

## How to Run

The notebooks must be run in the following order:

1. **`setup_check.ipynb`** — Run all cells top to bottom (`Run All`). This notebook verifies the environment, loads F1 data, and sets up the FastF1 cache. It must complete successfully before running the second notebook.

2. **`data_check.ipynb`** — Run all cells top to bottom after `setup_check.ipynb` has been completed. This notebook depends on the FastF1 cache created in the first run.

> In VS Code: open the notebook → click **Run All** in the toolbar → select the **Python (iit414w)** kernel if prompted.

---

## Problems Encountered

### Problem 1 — `FileNotFoundError: [WinError 2]` when checking Git

**What happened:** The environment verification cell in `setup_check.ipynb` crashed with `FileNotFoundError: [WinError 2]` on the `subprocess.run(['git', '--version'], ...)` line. The notebook could not continue past that point.

**Cause:** Git was not installed on the machine. The Jupyter kernel could not find the `git` executable.

**Solution:** Downloaded and installed Git from https://git-scm.com. After installation, restarted VS Code so the new PATH was picked up by the kernel. Re-ran the notebook — the error was gone.

---

### Problem 2 — Unfamiliarity with Formula 1 terminology and context

**What happened:** Several cells required filling in answers, predictions, and reflections that assumed basic knowledge of Formula 1 — driver names, race formats, qualifying sessions, and what metrics are meaningful in that sport. Without that context, it was difficult to give informed answers rather than generic ones.

**Cause:** No prior familiarity with F1 as a data domain.

**Solution:** Used external resources (Gemini) to get a quick overview of the 2025 driver lineup, the structure of a qualifying session, and what statistics are typically used to evaluate driver performance. This made it possible to fill in the prediction card and reflection answers with reasoning grounded in actual F1 context.

---

## Expected Outputs

### `setup_check.ipynb`

A successful run produces:

- A 6-row package table confirming all dependencies are installed (numpy, pandas, sklearn, matplotlib, seaborn, fastf1) with their versions.
- A printed working directory path and FastF1 cache path.
- Git version string and recent commit history (or `No commit history available` if the repo is fresh).
- Two side-by-side qualifying lap time plots for the 2024 Abu Dhabi GP top 5 drivers.
- A best lap summary table with gap-to-pole times.
- A synthetic classification demo printing an accuracy score (~0.85).
- A 3-row ML paradigms table.

### `data_check.ipynb`

A successful run produces printed confirmation that the FastF1 cache is accessible and session data can be loaded without re-downloading.
