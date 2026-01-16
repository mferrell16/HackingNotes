
## 1. What an Activation Function Is

An **activation function** is a mathematical function applied to a neuron’s pre-activation value to produce the neuron’s output.

It determines:
- The numeric output of a neuron
- How much signal flows to the next layer
- Whether the network can model non-linear patterns

---

## 2. Where Activation Functions Fit in a Neural Network

### Step 1: Linear Combination
z = Σ(wᵢ · xᵢ) + b

### Step 2: Activation
a = f(z)
### Variable Meanings

| Symbol | Meaning |
|------|--------|
| xᵢ | Input values |
| wᵢ | Weights |
| b | Bias |
| z | Pre-activation value (raw sum) |
| f(z) | Activation function |
| a | Activation (neuron output) |

Only **a** is passed to the next layer.

---

## 3. Why Activation Functions Are Necessary

Without activation functions:
- Deep networks collapse into a single linear equation
- Complex patterns cannot be learned

Activation functions:
- Introduce non-linearity
- Act as signal filters
- Control gradient flow during learning

---

# ReLU (Rectified Linear Unit)

## Equation
ReLU(z) = max(0, z)

### Variables
| Variable | Meaning |
|--------|--------|
| z | Pre-activation value |
| Output | 0 if z ≤ 0, otherwise z |

### Behavior
- Negative input → output = 0
- Positive input → output = z

### Interpretation
“Only pass the signal forward if it is positive.”

### Common Usage
- Hidden layers in most neural networks

### Key Downside
- Dead neurons (neurons that always output 0)

---

# Sigmoid

## Equation
σ(z) = 1 / (1 + e⁻ᶻ)

### Variables
| Variable | Meaning |
|--------|--------|
| z | Pre-activation value |
| e | Euler’s number (~2.718) |
| Output | Value between 0 and 1 |

### Behavior
- Large negative z → ~0
- Large positive z → ~1

### Interpretation
“How confident am I that this is true?”

### Common Usage
- Binary classification output layers

### Key Downsides
- Vanishing gradients
- Not zero-centered
- Rarely used in hidden layers

---

# Softmax

## Equation
softmax(zᵢ) = eᶻⁱ / Σ(eᶻʲ) for j = 1 to K

### Variables
| Variable | Meaning |
|--------|--------|
| zᵢ | Pre-activation score for class i |
| K | Number of classes |
| e | Euler’s number |
| Output | Probability for class i |

### Behavior
- Outputs sum to 1
- All values between 0 and 1

### Interpretation
“Which class is most likely?”

### Common Usage
- Final layer of multi-class classifiers

### Important Note
Softmax is used **only** in output layers.

---

## 4. Activation Function Comparison

| Function | Output Range | Typical Use |
|--------|-------------|-------------|
| ReLU | [0, ∞) | Hidden layers |
| Sigmoid | (0, 1) | Binary output |
| Softmax | (0, 1), sums to 1 | Multi-class output |

---

## 5. One-Sentence Summary

Activation functions transform a neuron’s weighted sum into an output value, introducing non-linearity and controlling how information and gradients flow through a neural network.
