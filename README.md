# LectureNotes

Repository for lecture notes, scripts and notebooks for the NDL3 Deep Learning course.

## Structure

Each exercise is its own self-contained folder with all necessary notebooks, utility scripts, and data files.

```
LectureNotes/
├── exercise_8/          # Keras fundamentals
├── exercise_9/          # Image classification with FCNNs, Hyperparameter search
├── assignments/         # Graded assignments
└── pyproject.toml       # Environment configuration
```

## Environment

The Python environment is managed with [uv](https://docs.astral.sh/uv/), but usage is optional. You can also use pip, poetry, or any other package manager of your choice.

**With uv:**

```bash
uv sync
```

## Exercises

| Exercise       | Topic                | Description                                                                                                                                   |
| -------------- | -------------------- | --------------------------------------------------------------------------------------------------------------------------------------------- |
| **Exercise 8** | Keras Fundamentals   | Introduction to Keras, activation functions (Sigmoid, ReLU, Leaky ReLU), dropout, batch normalization, skip connections, Keras Functional API |
| **Exercise 9** | Image Classification | Fully Connected Neural Networks (FCNNs) for Fashion MNIST, limitations of dense networks for images, random hyperparameter search             |

## Requirements

- Keras 3.x with TensorFlow backend (or PyTorch/JAX)
- See `pyproject.toml` for full dependency list

## TensorFlow GPU Notes (RTX 50xx)

If TensorFlow reports `Cannot dlopen some GPU libraries`, your CUDA wheel paths are not on `LD_LIBRARY_PATH`.
This repository's devcontainer setup now auto-generates `/home/vscode/.venv/.cuda_env.sh` and sources it from `.bashrc`.

Quick checks:

```bash
uv run python - <<'PY'
import tensorflow as tf
print(tf.__version__)
print(tf.config.list_physical_devices("GPU"))
print(tf.sysconfig.get_build_info().get("cuda_compute_capabilities"))
PY
```

On RTX 5070 (compute capability `12.0a`), current `tf-nightly` may show a warning that kernels are JIT-compiled from PTX.
This is expected until TensorFlow ships native `sm_120` binaries.
