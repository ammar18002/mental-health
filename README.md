# My Mental-Health
🌱 1. Starting Point

The goal was to use AutoGluon Tabular to train a high-quality model on a dataset containing ~140k rows and 19 features for a binary classification problem (“Depression”).

At first, the setup used:

AutoGluon v1.4.0

Python 3.10 / 3.12

Jupyter Notebook

macOS Intel (no GPU)

# ❌ 2. Major Problems Encountered

While using AutoGluon 1.4.0, the notebook repeatedly crashed before or during training.

Cause of crashes:

AutoGluon v1.4.0 automatically loads PyTorch + Transformer models
Even when only LightGBM was requested.

PyTorch CPU builds are unstable on macOS Intel, especially inside Jupyter Notebook.

LightGBM multi-threading (OpenMP-like) caused kernel crashes due to thread handling issues on macOS.

Jupyter Notebook’s renderer also crashed after large text output.

This resulted in repeated kernel deaths and the inability to finish training.

# ⚙️ 3. The Fix — Using AutoGluon 0.8.2 (Tabular Only)
# 🛠️ 4. Fixing the Final Crash — LightGBM Threading

Even with AutoGluon 0.8.2, LightGBM attempted multi-threaded training, which crashed macOS kernels.

# 🧠 5. Key Lessons Learned
✔ AutoGluon 1.4.0 is not stable on macOS Intel

Because it forces PyTorch / Transformers internally.

✔ AutoGluon 0.8.2 (Tabular-only) is perfect for Mac

It has everything needed for tabular ML and nothing heavy.

✔ LightGBM must run with n_jobs = 1 on macOS

Multi-threading leads to kernel death due to Apple Clang limitations.

✔ Crashes after training are often Jupyter rendering issues

Not model failures.

✔ The trained model was saved even if the UI crashed afterwards

Using a new notebook to load it works fine.
