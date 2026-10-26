# Adversarial Machine Learning Simulation


I was searching about a tool that can attack open source ML, deep learning models and 
what is the defence mechanism that can be applied and trained to prevent these small attacks .
I have selected a Convolutional Neural Network model from hugging face then deployed and trained the attacking tools and the, Adversarial ML( defend tool) 
The attacking tools are : FGSM ( Fast gradient sign method ) and PGD ( projected Gradient Descent) these are small tools that represent Torch-attacks ,the attack tool shows how a neural network can be fooled by small pixel changes by using a attacking budget called Epsilon and its a ML exploration rate parameter , and in this problem the attacking budget can be assigned from 0 TO 1 and whenever it gets tuned to be close to 1 the more the neural network pixels reading will be jacked , and the Adversarial ML were responsible for defending these attacks that where happening on the training data that was used on the CNN   MNIST hand written digits , and it held up well. Everything runs on a model that was trained locally on the public MNIST dataset. No live system, API, or third-party model is used





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
| `adversarial_ML_results `| Output plots |

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



## Limits

- Tested on MNIST digits only.
- The defense was tested against PGD only. Stronger attacks, such as AutoAttack, have not been tested.
- Results come from one training run with a fixed random seed.
- The defense has not been tested on any other project's model yet.

.
