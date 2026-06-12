You're absolutely right! The notation can be confusing. Let me rewrite the **exact same example** but with **clear, intuitive names** instead of letters like z, h, y.

---

## The Network With Clear Names

```
    Input      Hidden        Output
    Layer      Layer         Layer
    
      x ─────► Neuron1 ─────► Neuron2
     
    Weights:              Biases:
    w_in_hidden = 0.5     bias_hidden = 0.2
    w_hidden_out = 0.8    bias_out = 0.1
```

**Goal:** Learn that when input = 1, output should be 1

---

## STEP 0: Starting Point

```
Initial random values:
┌────────────────────────────────────────────────────────────┐
│                                                            │
│   w_in_hidden = 0.5    bias_hidden = 0.2                  │
│   w_hidden_out = 0.8   bias_out = 0.1                     │
│                                                            │
│   Training example: input = 1, correct_answer = 1         │
│                                                            │
└────────────────────────────────────────────────────────────┘
```

---

## PART 1: FORWARD PROPAGATION (Getting the Prediction)

### Step 1.1: Calculate Hidden Neuron Value

```
STEP A: Multiply input by weight, then add bias
─────────────────────────────────────────────────────────────

hidden_before_activation = (input × w_in_hidden) + bias_hidden

hidden_before_activation = (1 × 0.5) + 0.2
hidden_before_activation = 0.5 + 0.2
hidden_before_activation = 0.7


STEP B: Apply activation function (sigmoid) to squash it between 0 and 1
─────────────────────────────────────────────────────────────

hidden_after_activation = sigmoid(0.7) 
                        = 1 / (1 + 2.718^(-0.7))
                        = 0.668

┌─────────────────────────────────────────────────────────────┐
│  hidden_after_activation = 0.668                           │
└─────────────────────────────────────────────────────────────┘
```

### Step 1.2: Calculate Output Neuron Value

```
STEP A: Multiply hidden output by weight, then add bias
─────────────────────────────────────────────────────────────

output_before_activation = (hidden_after_activation × w_hidden_out) + bias_out

output_before_activation = (0.668 × 0.8) + 0.1
output_before_activation = 0.5344 + 0.1
output_before_activation = 0.6344


STEP B: Apply activation function (sigmoid)
─────────────────────────────────────────────────────────────

prediction = sigmoid(0.6344) = 0.653

┌─────────────────────────────────────────────────────────────┐
│  prediction = 0.653                                        │
│  correct_answer = 1.0                                      │
│  ERROR = 1.0 - 0.653 = 0.347                               │
└─────────────────────────────────────────────────────────────┘
```

---

## PART 2: BACKPROPAGATION (Adjusting Weights)

Now we work **backwards** from the error to fix the weights.

### Step 2.1: Adjust w_hidden_out (weight from hidden to output)

**Formula in words:**
```
change_in_weight = 
   learning_rate × 
   error × 
   derivative_of_sigmoid(prediction) × 
   hidden_after_activation
```

**Step-by-step calculation:**

```
First, calculate derivative of sigmoid at the prediction:
derivative = prediction × (1 - prediction)
derivative = 0.653 × (1 - 0.653)
derivative = 0.653 × 0.347
derivative = 0.226

Now multiply everything:
change_in_weight = 0.5 × 0.347 × 0.226 × 0.668
                 = 0.5 × 0.347 × 0.151
                 = 0.5 × 0.0524
                 = 0.0262

Update the weight:
NEW w_hidden_out = OLD w_hidden_out + change_in_weight
NEW w_hidden_out = 0.8 + 0.0262 = 0.8262
```

**What this means:**
```
Before: w_hidden_out = 0.8  →  prediction was 0.653
After:  w_hidden_out = 0.826 →  prediction will be higher (closer to 1) ✓
```

---

### Step 2.2: Adjust bias_out (output bias)

**Formula in words:**
```
change_in_bias = 
   learning_rate × 
   error × 
   derivative_of_sigmoid(prediction)
```

**Step-by-step calculation:**

```
change_in_bias = 0.5 × 0.347 × 0.226
               = 0.5 × 0.0784
               = 0.0392

NEW bias_out = 0.1 + 0.0392 = 0.1392
```

---

### Step 2.3: Adjust w_in_hidden (weight from input to hidden)

This is where the error travels **backward** to the hidden layer.

**Step A: Calculate how much the hidden neuron contributed to the error**

```
hidden_error = error × derivative_of_sigmoid(prediction) × w_hidden_out
             = 0.347 × 0.226 × 0.8
             = 0.347 × 0.1808
             = 0.0627
```

**Step B: Calculate derivative of sigmoid at hidden output**

```
hidden_derivative = hidden_after_activation × (1 - hidden_after_activation)
                  = 0.668 × (1 - 0.668)
                  = 0.668 × 0.332
                  = 0.222
```

**Step C: Calculate change in weight**

```
change_in_weight = learning_rate × hidden_error × hidden_derivative × input

change_in_weight = 0.5 × 0.0627 × 0.222 × 1
                 = 0.5 × 0.0627 × 0.222
                 = 0.5 × 0.0139
                 = 0.00695

NEW w_in_hidden = 0.5 + 0.00695 = 0.50695
```

---

### Step 2.4: Adjust bias_hidden

```
change_in_bias = learning_rate × hidden_error × hidden_derivative

change_in_bias = 0.5 × 0.0627 × 0.222
               = 0.5 × 0.0139
               = 0.00695

NEW bias_hidden = 0.2 + 0.00695 = 0.20695
```

---

## PART 3: Complete Summary Table

```
┌─────────────────────────────────────────────────────────────────────────┐
│                           BEFORE              AFTER                     │
├─────────────────────────────────────────────────────────────────────────┤
│  w_in_hidden (input → hidden)      0.50000  ──►   0.50695  (+0.00695)   │
│  bias_hidden                       0.20000  ──►   0.20695  (+0.00695)   │
│  w_hidden_out (hidden → output)    0.80000  ──►   0.82620  (+0.02620)   │
│  bias_out                          0.10000  ──►   0.13920  (+0.03920)   │
├─────────────────────────────────────────────────────────────────────────┤
│  Prediction                        0.653    ──►   0.666    (better ✓)   │
│  Error                             0.347    ──►   0.334    (smaller ✓)  │
└─────────────────────────────────────────────────────────────────────────┘
```

---

## PART 4: Visual Flow With Clear Names

```
                    FORWARD PASS
                    ════════════
                    
    input=1 ──► [×w_in_hidden=0.5] ──► [+bias_hidden=0.2] ──► [sigmoid] ──► hidden=0.668
                                                                              │
                                                                              │ [×w_hidden_out=0.8]
                                                                              ▼
                                                                         [+bias_out=0.1] ──► [sigmoid] ──► prediction=0.653
                                                                              │
                                                                              │
                                                                         correct_answer=1.0
                                                                              │
                                                                              ▼
                                                                         ERROR = 0.347


                    BACKWARD PASS
                    ═════════════
                    
    ERROR = 0.347
         │
         │ 1. How much should w_hidden_out change?
         ▼
    change_w_hidden_out = 0.0262 ──────────────────────┐
         │                                             │
         │ 2. How much should bias_out change?        │
         ▼                                             │
    change_bias_out = 0.0392 ──────────────────────────┤
         │                                             │
         │ 3. Send error BACK to hidden layer        │
         ▼                                             │
    hidden_error = 0.0627                              │
         │                                             │
         ├──► change_w_in_hidden = 0.00695 ────────────┤
         │                                             │
         └──► change_bias_hidden = 0.00695 ────────────┤
                                                        │
                                                        ▼
                                          UPDATE EVERYTHING:
                                          w_in_hidden = 0.50695
                                          bias_hidden = 0.20695  
                                          w_hidden_out = 0.82620
                                          bias_out = 0.13920
```

---

## PART 5: What Each Variable Means (Dictionary)

| My new name | What it represents | Old confusing name |
|-------------|-------------------|-------------------|
| `input` | The value we feed into the network | x |
| `hidden_before_activation` | Hidden neuron's raw sum (before squishing) | z_h |
| `hidden_after_activation` | Hidden neuron after squishing (0 to 1) | h_out |
| `output_before_activation` | Output neuron's raw sum (before squishing) | z_y |
| `prediction` | Final answer (0 to 1) | y_pred |
| `correct_answer` | What the answer should be | y_true |
| `error` | How wrong we were | error |
| `w_in_hidden` | Weight from input to hidden | w1 |
| `w_hidden_out` | Weight from hidden to output | w2 |
| `bias_hidden` | Hidden neuron's bias | b1 |
| `bias_out` | Output neuron's bias | b2 |

---

## The One-Sentence Summary With Clear Names

**Backpropagation =** 
1. Calculate `prediction` by flowing forward: `input → multiply → add bias → sigmoid → hidden → multiply → add bias → sigmoid → prediction`
2. Calculate `error = correct_answer - prediction`
3. Spread error backward to find how much each weight contributed
4. Adjust each weight and bias by a small amount
5. Repeat until error is tiny

---

Does this clearer naming help? Which part still feels confusing?