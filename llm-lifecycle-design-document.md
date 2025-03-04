# LLM Lifecycle for Stock Market Analysis
## System Design Document

**Version:** 1.0  
**Date:** March 4, 2025  
**Authors:** LLM Engineering Team

## 1. Introduction

### 1.1 Purpose
This document outlines the design of a comprehensive application that demonstrates the complete lifecycle of Large Language Models (LLMs) for stock market analysis. The application focuses on implementing core algorithms from scratch to provide educational value and transparency in how LLMs process OHLC (Open, High, Low, Close) data.

### 1.2 Scope
The system covers all phases of the LLM lifecycle:
- Data Collection & Preparation
- Model Architecture Design
- Pre-training
- Fine-tuning
- Evaluation & Testing
- Deployment & Inference
- Monitoring & Maintenance
- Safety & Alignment

Each phase will feature custom-built algorithms without relying on external machine learning frameworks.

### 1.3 System Overview
The application consists of a Next.js frontend and a Spring Boot backend. The frontend provides an intuitive step-by-step interface for users to navigate through the LLM lifecycle, while the backend implements all core algorithms from scratch and handles data processing.

## 2. Architecture

### 2.1 System Architecture

```
┌───────────────────┐     REST API      ┌────────────────────┐
│   Next.js Client  │<----------------->│  Spring Boot API   │
│   (React)         │    WebSockets     │  (Java)            │
└───────────────────┘                   └────────────────────┘
        │                                        │
        │                                        │
        ▼                                        ▼
┌───────────────────┐                   ┌────────────────────┐
│  UI Components    │                   │  Custom Algorithm  │
│  - Stage Wizards  │                   │  Implementations   │
│  - Visualizations │                   │  (All from scratch)│
└───────────────────┘                   └────────────────────┘
                                                 │
                                                 ▼
                                        ┌────────────────────┐
                                        │  H2 Database       │
                                        │  - OHLC Data       │
                                        │  - Model Parameters│
                                        │  - Results Storage │
                                        └────────────────────┘
```

### 2.2 Component Architecture

#### 2.2.1 Frontend Components
- **Stage Navigation**: Controls movement between lifecycle stages
- **Stage Components**: Specialized interfaces for each lifecycle stage
- **Status Panel**: Real-time system status monitoring
- **Visualization Components**: Charts and diagrams for algorithm insights

#### 2.2.2 Backend Components
- **Controllers**: REST endpoints for each lifecycle stage
- **Services**: Business logic implementing the LLM workflow
- **Custom Algorithms**: From-scratch implementations of core algorithms
- **Repositories**: Data access layer for persistence
- **WebSocket Handlers**: Real-time updates for long-running processes

## 3. Detailed Design

### 3.1 Data Collection & Preparation

#### 3.1.1 Custom Algorithms
- **StratifiedVolatilitySampler**: Implements stratified sampling based on market volatility
  - Algorithm complexity: O(n log n)
  - Key methods:
    - `sample(List<StockDataPoint> allData, int sampleSize)`: Returns a stratified sample
    - `calculateVolatility(StockDataPoint point)`: Calculates volatility for a data point
    - `classifyVolatility(StockDataPoint point)`: Classifies data point into volatility strata

- **ChronologicalSampler**: Preserves temporal patterns in time series data
  - Algorithm complexity: O(n)
  - Key methods:
    - `sample(List<StockDataPoint> allData, int sampleSize)`: Returns chronologically representative sample

#### 3.1.2 Data Model
```java
public class StockDataPoint {
    private Long id;
    private String symbol;
    private LocalDate date;
    private double open;
    private double high;
    private double low;
    private double close;
    private long volume;
    private double dailyReturn;
    private double volatility;
}

public class Dataset {
    private Long id;
    private String name;
    private LocalDateTime uploadDate;
    private long rowCount;
    private String timeRange;
    private String[] symbols;
    private int missingValues;
    private String samplingMethod;
    private double lowVolatilityPercentage;
    private double mediumVolatilityPercentage;
    private double highVolatilityPercentage;
}
```

### 3.2 Model Architecture Design

#### 3.2.1 Custom Algorithms
- **MatrixOperations**: Implements basic matrix operations from scratch
  - Key methods:
    - `matrixMultiply(double[][] A, double[][] B)`: Matrix multiplication
    - `transpose(double[][] matrix)`: Matrix transposition
    - `softmax(double[][] matrix)`: Softmax activation function
    - `initializeWeights(int rows, int cols)`: Xavier/Glorot weight initialization

- **SelfAttention**: Implements the self-attention mechanism
  - Algorithm complexity: O(n²·d) where n is sequence length and d is embedding dimension
  - Key methods:
    - `forward(double[][] inputs)`: Computes attention mechanism forward pass
    - `forwardMultiHead(double[][] inputs)`: Computes multi-head attention

#### 3.2.2 Data Model
```java
public class ModelArchitecture {
    private Long id;
    private String name;
    private String architecture;
    private int attentionLayers;
    private int embeddingDimension;
    private int headCount;
    private int sequenceLength;
    private double dropoutRate;
    private LocalDateTime createdAt;
    private Long datasetId;
}
```

### 3.3 Pre-training

#### 3.3.1 Custom Algorithms
- **AdamOptimizer**: Implements adaptive moment estimation
  - Algorithm complexity: O(p) where p is number of parameters
  - Key methods:
    - `updateParameters(Map<String, double[]> parameters, Map<String, double[]> gradients)`: Updates model parameters
    - `reset()`: Resets optimizer state

- **LossFunction**: Implements various loss functions
  - Key methods:
    - `meanSquaredError(double[] predictions, double[] targets)`: MSE loss
    - `binaryCrossEntropy(double[] predictions, double[] targets)`: BCE loss
    - `meanSquaredErrorGradient(double[] predictions, double[] targets)`: MSE gradient

#### 3.3.2 Data Model
```java
public class TrainingStatus {
    private Long id;
    private Long modelId;
    private String stage; // pretraining, finetuning
    private String status; // not_started, in_progress, completed
    private LocalDateTime startTime;
    private LocalDateTime endTime;
    private int totalEpochs;
    private int currentEpoch;
    private List<Double> lossHistory;
}
```

### 3.4 Fine-tuning

#### 3.4.1 Custom Algorithms
- **KnowledgeDistillation**: Implements teacher-student model training
  - Algorithm complexity: O(n·p) where n is batch size and p is parameter count
  - Key methods:
    - `distill(TransformerModel teacherModel, TransformerModel studentModel)`: Transfers knowledge
    - `calculateKLDivergence(double[] studentProbs, double[] teacherProbs)`: Calculates loss

#### 3.4.2 Data Model
Extension of the TrainingStatus model with:
```java
public class TrainingStatus {
    // Same fields as pre-training, plus:
    private String targetSymbol;
    private String finetuningMethod;
}
```

### 3.5 Evaluation & Testing

#### 3.5.1 Custom Algorithms
- **DieboldMarianoTest**: Implements statistical forecast comparison
  - Algorithm complexity: O(n·log(n)) where n is number of predictions
  - Key methods:
    - `testSignificance(double[] actualValues, double[] forecast1, double[] forecast2)`: Runs test
    - `calculateHACVariance(double[] series)`: Calculates heteroskedasticity-consistent variance

- **ConfusionMatrixMetrics**: Implements classification performance metrics
  - Algorithm complexity: O(n)
  - Key methods:
    - `calculateBinaryMetrics(boolean[] actualPositive, boolean[] predictedPositive)`: Calculates metrics
    - `calculateDirectionalMetrics(double[] actualPrices, double[] predictedPrices)`: For direction prediction

- **BootstrapConfidenceInterval**: Implements resampling for uncertainty estimation
  - Algorithm complexity: O(b·n·log(n)) where b is bootstrap samples and n is data points
  - Key methods:
    - `calculateInterval(double[] data, Function<double[], Double> statistic, double confidenceLevel, int numResamples)`: Calculates interval

### 3.6 Deployment & Inference

#### 3.6.1 Custom Algorithms
- **LinearQuantizer**: Implements bit-precision reduction
  - Algorithm complexity: O(n) where n is number of parameters
  - Key methods:
    - `quantize(double[] paramValues)`: Quantizes parameters to reduced precision
    - `dequantize(QuantizedParams quantizedParams)`: Recovers approximate original values

- **WeightPruning**: Implements model sparsification
  - Algorithm complexity: O(n·log(n)) where n is number of parameters
  - Key methods:
    - `pruneByThreshold(double[] weights, double pruningRate)`: Zeros out small weights
    - `calculateSparsity(double[] weights)`: Measures sparsity level

- **LRUCache**: Implements efficient inference caching
  - Algorithm complexity: O(1) for get/put operations
  - Key methods:
    - `get(K key)`: Retrieves cached value
    - `put(K key, V value)`: Stores value in cache

#### 3.6.2 Data Model
```java
public class DeploymentConfig {
    private Long id;
    private Long modelId;
    private int quantizationBits;
    private int batchSize;
    private boolean enableCaching;
    private LocalDateTime deployedAt;
    private String status; // deploying, active, inactive
    private double originalSizeMb;
    private double quantizedSizeMb;
    private double latencyMs;
    private double throughputPredPerSec;
    private double accuracyLossPercent;
}
```

### 3.7 Monitoring & Maintenance

#### 3.7.1 Custom Algorithms
- **CUSUMDetector**: Implements cumulative sum control chart
  - Algorithm complexity: O(1) per data point
  - Key methods:
    - `detectDrift(double newErrorValue)`: Processes new value and checks for drift
    - `reset()`: Resets detector state

- **ExponentialMovingAverage**: Implements weighted moving average
  - Algorithm complexity: O(1) per update
  - Key methods:
    - `update(double newValue)`: Updates the EMA with a new observation
    - `getCurrentValue()`: Gets current EMA value

- **ShewhartControlChart**: Implements statistical process control
  - Algorithm complexity: O(n) where n is historical points
  - Key methods:
    - `addValue(double value)`: Adds new observation and checks limits
    - `isInControl()`: Checks if process is in control

#### 3.7.2 Data Model
```java
public class MonitoringStatus {
    private Long id;
    private Long deploymentId;
    private boolean active;
    private double driftThreshold;
    private boolean driftDetected;
    private LocalDateTime lastCheckedAt;
    private List<Double> cumsumValues;
    private int datapointsProcessed;
    private double currentErrorRate;
    private double baselineErrorRate;
    private double directionalAccuracy;
}
```

### 3.8 Safety & Alignment

#### 3.8.1 Custom Algorithms
- **AdversarialAttackGenerator**: Implements adversarial example creation
  - Algorithm complexity: O(i·n·p) where i is iterations, n is sequence length, p is parameters
  - Key methods:
    - `generateAdversarialExamples(List<StockDataPoint> originalData)`: Creates perturbed inputs
    - `calculateInputGradients(List<StockDataPoint> sequence, StockDataPoint target)`: Approximates gradients

#### 3.8.2 Data Model
```java
public class SafetyCheckResult {
    private Long id;
    private Long deploymentId;
    private LocalDateTime checkedAt;
    private int robustnessScore;
    private int passedTests;
    private int totalTests;
    private List<String> vulnerabilities;
}
```

## 4. Database Design

### 4.1 Entity Relationship Diagram

```
+---------------+       +-------------------+       +------------------+
| Dataset       |       | ModelArchitecture |       | TrainingStatus   |
+---------------+       +-------------------+       +------------------+
| id            |<----->| id                |<----->| id               |
| name          |       | name              |       | modelId          |
| uploadDate    |       | architecture      |       | stage            |
| rowCount      |       | attentionLayers   |       | status           |
| timeRange     |       | embeddingDimension|       | startTime        |
| symbols       |       | headCount         |       | endTime          |
| missingValues |       | sequenceLength    |       | totalEpochs      |
| samplingMethod|       | dropoutRate       |       | currentEpoch     |
+---------------+       | datasetId         |       | lossHistory      |
        |               +-------------------+       | targetSymbol     |
        |                       |                   | finetuningMethod |
        v                       |                   +------------------+
+---------------+               |                           |
| StockDataPoint|               |                           |
+---------------+               |                           |
| id            |               |                           |
| symbol        |               v                           v
| date          |       +-------------------+       +------------------+
| open          |       | DeploymentConfig  |       | MonitoringStatus |
| high          |       +-------------------+       +------------------+
| low           |       | id                |<----->| id               |
| close         |       | modelId           |       | deploymentId     |
| volume        |       | quantizationBits  |       | active           |
| dailyReturn   |       | batchSize         |       | driftThreshold   |
| volatility    |       | enableCaching     |       | driftDetected    |
+---------------+       | deployedAt        |       | lastCheckedAt    |
                        | status            |       | cumsumValues     |
                        | originalSizeMb    |       | datapointsProc.  |
                        | quantizedSizeMb   |       +------------------+
                        | latencyMs         |               |
                        | throughputPredSec |               |
                        | accuracyLossPerc. |               |
                        +-------------------+               |
                                |                           |
                                v                           v
                        +-------------------+       +------------------+
                        | SafetyCheckResult |       | PredictionResult|
                        +-------------------+       +------------------+
                        | id                |       | id               |
                        | deploymentId      |       | deploymentId     |
                        | checkedAt         |       | timestamp        |
                        | robustnessScore   |       | inputData        |
                        | passedTests       |       | prediction       |
                        | totalTests        |       | actual           |
                        | vulnerabilities   |       | error            |
                        +-------------------+       +------------------+
```

## 5. API Design

### 5.1 REST API Endpoints

#### 5.1.1 Data Collection API
- `POST /api/data/upload`: Upload OHLC dataset
- `GET /api/data/{datasetId}`: Get dataset details

#### 5.1.2 Model Architecture API
- `POST /api/model/design`: Create model architecture
- `GET /api/model/{modelId}`: Get model details

#### 5.1.3 Training API
- `POST /api/model/pretrain`: Start pre-training
- `POST /api/model/finetune`: Start fine-tuning
- `GET /api/model/training-status/{modelId}/{stage}`: Get training status

#### 5.1.4 Evaluation API
- `POST /api/model/evaluate`: Evaluate model
- `GET /api/model/evaluation/{evaluationId}`: Get evaluation results

#### 5.1.5 Deployment API
- `POST /api/model/deploy`: Deploy model
- `GET /api/model/deployment-status/{modelId}`: Get deployment status

#### 5.1.6 Monitoring API
- `POST /api/monitoring/start`: Start monitoring
- `POST /api/monitoring/stop`: Stop monitoring
- `POST /api/monitoring/reset`: Reset monitoring
- `GET /api/monitoring/{deploymentId}`: Get monitoring status

#### 5.1.7 Safety API
- `POST /api/model/safety`: Run safety checks
- `GET /api/model/safety/{deploymentId}`: Get safety history

### 5.2 WebSocket Endpoints

- `/topic/training-updates`: Real-time updates during training
- `/topic/deployment-updates`: Updates during deployment
- `/topic/monitoring-updates`: Updates from drift monitoring

## 6. User Interface Design

### 6.1 Main Dashboard Layout

```
┌─────────────────────────────────────────────────────────────────┐
│ LLM Lifecycle for Stock Market Analysis                         │
├─────────────┬─────────────────────────────────┬─────────────────┤
│             │                                 │                 │
│   Stage     │                                 │    System       │
│  Navigation │         Current Stage           │    Status       │
│             │          Interface              │                 │
│  □ Data     │                                 │  Dataset: ✓     │
│  □ Model    │                                 │  Architecture: ✓│
│  ■ Training │                                 │  Pre-training:  │
│  □ Eval     │                                 │    [=====>  ]   │
│  □ Deploy   │                                 │  Fine-tuning: □ │
│  □ Monitor  │                                 │  Deployment: □  │
│  □ Safety   │                                 │  Monitoring: □  │
│             │                                 │                 │
│             │                                 │                 │
│             │                                 │    Lifecycle    │
│             │                                 │      Flow       │
│             │                                 │                 │
│             │                                 │   [Diagram of   │
│             │                                 │    connected    │
│             │                                 │     stages]     │
│             │                                 │                 │
└─────────────┴─────────────────────────────────┴─────────────────┘
```

### 6.2 Key Interface Elements

#### 6.2.1 Data Collection Interface
- Dataset upload control
- Sampling method selection
- Data preview table
- Statistics visualization

#### 6.2.2 Model Architecture Interface
- Architecture type selection
- Layer configuration controls
- Parameter visualization
- Interactive diagram

#### 6.2.3 Training Interface
- Training configuration controls
- Real-time loss curve
- Epoch progress indicator
- Parameter update visualization

#### 6.2.4 Evaluation Interface
- Metric selection
- Results visualization
- Comparative analysis
- Statistical significance indicators

#### 6.2.5 Deployment Interface
- Quantization settings
- Inference optimization controls
- Performance metrics
- Size/speed tradeoff visualization

#### 6.2.6 Monitoring Interface
- CUSUM chart
- Error rate trends
- Drift detection indicators
- Control limits visualization

#### 6.2.7 Safety Interface
- Adversarial example generation
- Vulnerability visualization
- Robustness score display
- Risk assessment dashboard

## 7. Implementation Strategy

### 7.1 Development Phases

#### 7.1.1 Phase 1: Core Architecture
- Set up Spring Boot backend with H2 database
- Implement basic Next.js frontend with routing
- Establish REST API and WebSocket communication

#### 7.1.2 Phase 2: Custom Algorithm Implementation
- Implement data processing algorithms
- Develop attention mechanism from scratch
- Create optimization algorithms
- Build evaluation metrics

#### 7.1.3 Phase 3: Service Integration
- Connect algorithms to service layer
- Implement end-to-end workflow
- Add persistence using JPA repositories

#### 7.1.4 Phase 4: UI Refinement
- Enhance visualization components
- Add real-time updates
- Implement responsive design
- Create algorithm explainer sections

### 7.2 Testing Strategy

#### 7.2.1 Unit Testing
- Test each algorithm with known inputs/outputs
- Verify mathematical correctness
- Test edge cases

#### 7.2.2 Integration Testing
- Test algorithm chains (e.g., sampling → attention → optimization)
- Verify data flow between stages
- Test WebSocket communication

#### 7.2.3 Performance Testing
- Benchmark algorithm performance
- Test with varying data sizes
- Measure response times

## 8. Mathematical Foundations

### 8.1 Self-Attention Mechanism

The core attention calculation:

$$
\text{Attention}(Q, K, V) = \text{softmax}\left(\frac{QK^T}{\sqrt{d_k}}\right)V
$$

Where:
- $Q = X W^Q$ (Query matrix)
- $K = X W^K$ (Key matrix)
- $V = X W^V$ (Value matrix)
- $d_k$ is the dimension of the key vectors
- $X$ is the input sequence matrix

### 8.2 Adam Optimization

The parameter update rule:

$$
\theta_{t+1} = \theta_t - \frac{\eta}{\sqrt{\hat{v}_t} + \epsilon} \cdot \hat{m}_t
$$

Where:
- $\theta_t$ are the parameters at time $t$
- $\eta$ is the learning rate
- $\hat{m}_t = \frac{m_t}{1-\beta_1^t}$ is the bias-corrected first moment
- $\hat{v}_t = \frac{v_t}{1-\beta_2^t}$ is the bias-corrected second moment
- $m_t = \beta_1 \cdot m_{t-1} + (1 - \beta_1) \cdot g_t$ is the exponential moving average of gradients
- $v_t = \beta_2 \cdot v_{t-1} + (1 - \beta_2) \cdot g_t^2$ is the exponential moving average of squared gradients
- $g_t$ is the gradient at time $t$
- $\beta_1, \beta_2$ are hyperparameters (typically 0.9 and 0.999)
- $\epsilon$ is a small constant for numerical stability

### 8.3 CUSUM Detection

The CUSUM update rules:

$$
S^+_t = \max(0, S^+_{t-1} + (X_t - \mu_0) - k)
$$

$$
S^-_t = \max(0, S^-_{t-1} - (X_t - \mu_0) - k)
$$

Where:
- $S^+_t$ is the upper CUSUM at time $t$
- $S^-_t$ is the lower CUSUM at time $t$
- $X_t$ is the observed value at time $t$
- $\mu_0$ is the target mean
- $k$ is the reference value (allowable slack)

Drift is detected when either $S^+_t > h$ or $S^-_t > h$, where $h$ is the decision threshold.

### 8.4 Diebold-Mariano Test

The DM test statistic:

$$
\text{DM} = \frac{\bar{d}}{\sqrt{\hat{V}(\bar{d})}}
$$

Where:
- $\bar{d} = \frac{1}{T}\sum_{t=1}^T d_t$ is the mean of the loss differential series
- $d_t = L(\hat{y}_{1,t}, y_t) - L(\hat{y}_{2,t}, y_t)$ is the loss differential at time $t$
- $\hat{V}(\bar{d})$ is the HAC variance estimator
- $L$ is the loss function
- $\hat{y}_{1,t}, \hat{y}_{2,t}$ are forecasts from model 1 and 2
- $y_t$ is the actual value

## 9. Appendices

### 9.1 Glossary of Terms

- **OHLC**: Open, High, Low, Close - key price points in financial data
- **Attention Mechanism**: Neural network component that weighs input sequences
- **CUSUM**: Cumulative Sum control chart for detecting changes in time series
- **HAC**: Heteroskedasticity and Autocorrelation Consistent variance estimator
- **Quantization**: Reducing numerical precision of model weights
- **KL Divergence**: Kullback-Leibler divergence, measures difference between probability distributions

### 9.2 References

1. Vaswani, A. et al. (2017). "Attention Is All You Need"
2. Kingma, D. P., & Ba, J. (2014). "Adam: A Method for Stochastic Optimization"
3. Page, E. S. (1954). "Continuous Inspection Schemes"
4. Diebold, F. X., & Mariano, R. S. (1995). "Comparing Predictive Accuracy"
5. Hinton, G., Vinyals, O., & Dean, J. (2015). "Distilling the Knowledge in a Neural Network"

### 9.3 Algorithm Complexity Summary

| Algorithm | Time Complexity | Space Complexity |
|-----------|-----------------|------------------|
| StratifiedVolatilitySampler | O(n log n) | O(n) |
| Self-Attention | O(n² · d) | O(n² + nd) |
| AdamOptimizer | O(p) | O(p) |
| DieboldMarianoTest | O(n log n) | O(n) |
| LinearQuantizer | O(n) | O(n) |
| CUSUMDetector | O(1) per update | O(1) |
| LRUCache | O(1) per operation | O(capacity) |
| BootstrapConfidenceInterval | O(b · n log n) | O(b · n) |

Where:
- n: number of data points
- d: embedding dimension
- p: number of parameters
- b: number of bootstrap samples
