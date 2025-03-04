# **AI-Powered Trading System: MetaTrader 4 (MT4) & Java AI Server**

## **Overview**
This project integrates **MetaTrader 4 (MT4)** with a **Java-based AI trading server** using **ZeroMQ**. The system enables automated trading by predicting **BUY/SELL signals** using **LSTM deep learning models** and **Reinforcement Learning (RL4J)**.

---

## **Features**
✅ **Real-time market data exchange between MT4 & Java AI Server**  
✅ **Deep Learning-based trade signal prediction (LSTM)**  
✅ **Reinforcement Learning (RL4J) for dynamic strategy optimization**  
✅ **ZeroMQ messaging for fast, reliable communication**  
✅ **Automated trade execution in MT4**  
✅ **Logging and debugging for trade monitoring**

---

## **System Requirements**
### **Hardware Requirements**
- Minimum **4GB RAM** (8GB+ recommended)
- Dual-core **CPU or higher**
- **Stable Internet connection**

### **Software Requirements**
- **MetaTrader 4 (MT4)**
- **Java 17+ (JDK)**
- **Maven** (for Java dependency management)
- **ZeroMQ** (installed and configured)
- **MetaEditor** (for MQL4 script compilation)
- **libzmq.dll** (placed in `MQL4/Libraries/` folder)

---

## **Installation & Setup**
### **1️⃣ Install Required Software**
#### **MetaTrader 4 (MT4)**
- Download and install from your broker’s website.

#### **Java & Maven Setup**
- Install Java JDK 17+:  
  ```sh
  sudo apt install openjdk-17-jdk   # Linux
  brew install openjdk@17           # macOS
  choco install openjdk17           # Windows
  ```
- Install Maven:  
  ```sh
  sudo apt install maven   # Linux
  brew install maven       # macOS
  choco install maven      # Windows
  ```

#### **ZeroMQ Setup**
- Install ZeroMQ:  
  ```sh
  sudo apt-get install libzmq3-dev  # Linux
  brew install zeromq               # macOS
  choco install zeromq               # Windows
  ```

### **2️⃣ Configure MetaTrader 4 (MT4)**
1. **Copy `libzmq.dll` to the MT4 Libraries folder:**  
   ```
   C:\Users\YourUser\AppData\Roaming\MetaTrader 4\MQL4\Libraries\libzmq.dll
   ```
2. **Restart MT4** after adding the DLL.

### **3️⃣ Setup Java AI Server**
1. Clone the AI Trading project:
   ```sh
   git clone https://github.com/your-repo/ai-trading-bot.git
   cd ai-trading-bot
   ```
2. **Compile & Run the AI Trading Server:**
   ```sh
   mvn clean package
   mvn exec:java -Dexec.mainClass="com.trading.ai.ZeroMQAITradingServer"
   ```
✅ Expected output:
```
ZeroMQ AI Trading Server is running...
```

---

## **Running the AI Trading Expert Advisor (EA) in MT4**
### **1️⃣ Move the EA to the Correct Folder**
1. Copy **`ZeroMQClientEA.mq4`** to:
   ```
   C:\Users\YourUser\AppData\Roaming\MetaTrader 4\MQL4\Experts\ZeroMQClientEA.mq4
   ```
2. Open **MetaTrader 4** and **MetaEditor (`F4`)**.
3. Open `ZeroMQClientEA.mq4` and click **Compile (`F5`)**.

### **2️⃣ Attach EA to a Chart**
1. Open **MT4 Navigator (`Ctrl + N`) → Experts**.
2. Drag & Drop **ZeroMQClientEA** onto an active chart.
3. Enable **Auto Trading (`Ctrl + E`)**.
4. Check **MT4 Terminal (`Ctrl + T`) → Experts tab**.

✅ Expected log output:
```
🚀 ZeroMQ AI Trading EA Initialized - Running Test
📩 Received AI Response: {"signal":"BUY"}
🚀 AI Signal: BUY - Simulated Trade
```

---

## **Troubleshooting & Debugging**
| **Issue** | **Solution** |
|-----------|-------------|
| `libzmq.dll not found` | Ensure `libzmq.dll` is in `MQL4/Libraries/`, then restart MT4. |
| `EA does not attach` | Ensure you placed the EA in `MQL4/Experts/` and compiled it. |
| `No response from AI server` | Ensure the Java AI server is running (`mvn exec:java`). |
| `Invalid JSON Format` | Check Java server logs to ensure correct responses. |

---

## **Future Enhancements**
✅ **Enable AI-based Stop-Loss and Take-Profit**  
✅ **Implement Multi-Symbol Support (EURUSD, GBPJPY, etc.)**  
✅ **Enhance AI Model for Improved Trade Predictions**  

🚀 **For advanced configurations, refer to the AI Trading API documentation.**
