
## 1. What a Neural Network Is
A neural network is a stack of mathematical functions that:
1. Takes numeric inputs
2. Combines them using weights and biases
3. Applies activation functions
4. Produces an output
5. Measures error (cost/loss)
6. Adjusts weights and biases to reduce error

**Learning = adjusting weights and biases to reduce error.**

---

## 2. Core Components

### Inputs
- Raw numbers from data
- Never learned
- Examples: pixel values, metrics, features

### Weights
- Numbers on connections between neurons
- Control importance of inputs
- Learned during training

### Biases
- Numbers inside neurons
- Shift activation thresholds
- Learned during training

### Activation Function
- Transforms a neuron's raw sum into its output
- Introduces non-linearity
- Controls signal strength

**“How much a neuron activates” = what numeric value it outputs.**

### Hidden Layers
- Intermediate layers between input and output
- Each neuron learns one feature
- More neurons = more learned features

### Output Layer
- Combines hidden features into a final prediction
- Output format depends on task (number, probability, class)

### Cost (Loss) Function
- Measures how wrong the prediction is
- Outputs a single number
- Lower is better

### Backpropagation
- Computes how much each weight and bias contributed to the error
- Updates them slightly to reduce future error

---

## 3. What a Learned Feature Is
A learned feature is:
> A specific numeric pattern of the inputs that causes a hidden neuron to output a strong value.

Each hidden neuron learns one way to combine inputs that the network finds useful.

---

# Worked Example: 2 Inputs → 3 Hidden Neurons → 1 Output

## Architecture
(x1, x2)
   ↓
[ Hidden Neuron 1 ]
[ Hidden Neuron 2 ]
[ Hidden Neuron 3 ]
   ↓
[ Output Neuron ]

---

## Step 1: Inputs (Data)
x1 = 2  
x2 = 1

---

## Step 2: Hidden Layer Parameters (Preset, Learnable)

Hidden neuron 1  
w11 = 0.5  
w12 = -1.0  
b1  = 0.1  

Hidden neuron 2  
w21 = -0.3  
w22 = 0.8  
b2  = 0.0  

Hidden neuron 3  
w31 = 1.0  
w32 = 0.2  
b3  = -0.2  

---

## Step 3: Hidden Layer Linear Computation

z1 = (2 × 0.5) + (1 × -1.0) + 0.1 = 0.1  
z2 = (2 × -0.3) + (1 × 0.8) + 0.0 = 0.2  
z3 = (2 × 1.0) + (1 × 0.2) - 0.2 = 2.0  

---

## Step 4: Hidden Layer Activation (ReLU)

a1 = ReLU(0.1) = 0.1  
a2 = ReLU(0.2) = 0.2  
a3 = ReLU(2.0) = 2.0  

These three values are the entire output of the hidden layer.

---

## Step 5: Learned Feature Interpretation

Neuron 1: “Is x1 larger than x2?”  
Neuron 2: “Is x2 larger relative to x1?”  
Neuron 3: “Are the inputs large overall?”  

---

## Step 6: Output Layer Parameters (Preset, Learnable)

w_out1 = 1.5  
w_out2 = -0.7  
w_out3 = 0.4  
b_out  = -0.3  

---

## Step 7: Output Linear Computation

z_out =
(0.1 × 1.5)
+ (0.2 × -0.7)
+ (2.0 × 0.4)
- 0.3

z_out = 0.51

---

## Step 8: Output Activation (Sigmoid)

prediction = sigmoid(0.51) ≈ 0.625

---

## Step 9: Target (Data)

y = 1

---

## Step 10: Cost (Loss)

cost = (0.625 − 1)² ≈ 0.141

---

## Step 11: What Backpropagation Updates

Updated (learned):
- All hidden weights and biases
- All output weights and bias

Never updated:
- Inputs
- Targets
- Activation functions
- Network structure

---

## 4. Why More Hidden Neurons Help
- Each hidden neuron learns one feature
- More neurons = more features
- Output layer learns how to combine them
- Enables modeling complex patterns

Width = more features  
Depth = features of features

---

## One-Sentence Master Summary
A neural network learns by transforming inputs into learned features using weighted sums and activation functions, then adjusting those weights and biases via backpropagation to minimize prediction error.
