# Adversarial Machine Learning Simulation

A simulation of how a neural network can be fooled by small pixel changes, and how adversarial training makes it harder to fool.

Everything runs on a model that was trained locally on the public MNIST dataset. No live system, API, or third-party model is used.

## What this project shows

I built an attack tool to show how a neural network can be fooled by small pixel changes. For my defense, I trained a model to resist those attacks on MNIST, and it held up well. I haven't yet tested it on my own project's model, and I'd want to test it against stronger attacks before claiming it's safe.

## Contents

| File or folder | What it is |
|---|---|
| `adversarial_ml_simulation.ipynb` | The full project as one Google Colab notebook. Use this to run everything. |
| `src/model.py` | The small CNN classifier |
| `src/train_baseline.py` | Normal training of the baseline model |
| `src/fgsm.py` | FGSM attack, epsilon sweep, and example images |
| `src/pgd.py` | PGD attack and comparison with FGSM |
| `src/adv_train.py` | Adversarial training and robustness comparison |
| `models/` | Trained weights (`baseline_cnn.pt`, `adv_cnn.pt`) |
| `results/` | Output plots |
| `PROJECT_PLAN.md` | Build plan and status checklist |
| `REPORT.md` | Written report with results, limitations, and reproduction steps |

## How to run it on Google Colab

No installation is needed. Colab already includes PyTorch, torchvision, and matplotlib, and the dataset downloads automatically.

1. Open Google Colab and choose **File > Upload notebook**. Select `adversarial_ml_simulation.ipynb`.
2. Turn on the GPU: **Runtime > Change runtime type > Hardware accelerator > T4 GPU**.
3. Run everything: **Runtime > Run all**.
4. Wait for the last cell to finish. The full run takes roughly 10 to 20 minutes on a T4 GPU.
5. Plots appear inline below their cells. The last cell packages the plots and models into `adversarial_ml_results.zip` and offers it for download.

Without a GPU, the adversarial training step can take hours, so make sure the T4 is on before you run.

## How to run the scripts locally (Windows)

The scripts are an alternative to the notebook. Run them from this folder:

    py -3.14 src/train_baseline.py   # baseline model
    py -3.14 src/fgsm.py             # FGSM sweep and examples
    py -3.14 src/pgd.py              # PGD sweep and comparison with FGSM
    py -3.14 src/adv_train.py        # adversarial training and final comparison

Each script saves its outputs to `models/` or `results/`. Local runs need PyTorch, torchvision, torchattacks, and matplotlib installed.

## Results summary

Accuracy under attack on MNIST (attack: PGD with 20 steps):

| ε | Baseline model | Adversarially trained model |
|---|---|---|
| 0.00 (clean) | 98.92% | 98.69% |
| 0.10 | 72.04% | 97.46% |
| 0.20 | 0.37% | 95.67% |
| 0.30 | 0.00% | 92.81% |

Full details are in `REPORT.md`.

## Limits

- Tested on MNIST digits only.
- The defense was tested against PGD only. Stronger attacks, such as AutoAttack, have not been tested.
- Results come from one training run with a fixed random seed.
- The defense has not been tested on any other project's model yet.

## Scope

Attacks are used only on models trained locally for this project, or on public open-weight models run on this machine. They are not used against any live system, API, or model that I do not own or have permission to test.
