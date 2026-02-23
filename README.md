# Quanvolution MLP for MNIST

Implementation của paper: **Quantum-Classical Hybrid Machine Learning for Image Classification** - sử dụng PennyLane để reproduce kết quả.

## Mục tiêu

- Reproduce paper với quantum convolution (quanvolution) layer
- So sánh trainable vs non-trainable quantum filters
- Chạy trên MNIST dataset (3 classes: 1, 7, 9)

## Cấu trúc

### Quantum Circuit
- **4 qubits** với **RZ-RX-RZ-RX encoding** (4×4 = 16 pixels input)
- **3 parametric layers** với Circuit 13 (Fig 2(d) trong paper)
- Mỗi layer: 16 parameters → **48 parameters total**
- Output: Pauli-Z expectation values

### Model Architecture
```
Input (14×14) → Quanvolution Layer → Flatten → Linear(36→32) → ReLU → Linear(32→3) → Output
```

### Dataset
- MNIST subset: classes [1, 7, 9]
- Image size: 14×14 (sau MaxPool2d)
- Train: 600 samples | Test: 600 samples
- Batch size: 4

## Yêu cầu

```bash
pip install pennylane torch torchvision
```

## Chạy

```bash
jupyter notebook Quanvolution_MLP.ipynb
```

Hoặc chạy trực tiếp:

```python
# Xem notebook để chạy từng cell
```

## Kết quả (sau 10 epochs)

| Method    | Train Acc | Val Acc |
|-----------|-----------|---------|
| Non-trainable | ~0.84  | ~0.78  |
| Trainable     | ~0.85  | ~0.77  |

## Quantum Circuit Execution

Theo paper, với 28×28 image:
- **Non-trainable**: 7×7 = 49 circuits/sample
- **Trainable** (10 params): 49 + 2×10×49 = 1029 circuits/sample

Notebook hiện tại dùng 14×14 image (3×3 = 9 positions).

## Paper Reference

[Quantum-Classical Hybrid Machine Learning for Image Classification]

## License

MIT
