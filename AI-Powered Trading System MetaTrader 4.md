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

## **🛠 Troubleshooting & Debugging**

### **1️⃣ Check if AI Server is Listening on Port 5555**  
Run this command on **Windows**:  
```sh
netstat -ano | findstr :5555
```
✅ **Expected Output (AI Server Running)**:  
```
TCP    0.0.0.0:5555    0.0.0.0:0    LISTENING    12345
```
If **no output appears**, restart the AI server:  
```sh
mvn exec:java -Dexec.mainClass="com.trading.ai.ZeroMQAITradingServer"
```

### **2️⃣ Verify AI Server is Receiving Requests from MT4**  
Modify **Java AI Server** (`ZeroMQAITradingServer.java`) to print received messages:  
```java
while (!Thread.currentThread().isInterrupted()) {
    byte[] request = socket.recv(0);
    String requestStr = new String(request, StandardCharsets.UTF_8);
    System.out.println("📩 Received from MT4: " + requestStr);

    // Respond with trade signal
    String response = "{"signal":"BUY"}";
    socket.send(response.getBytes(StandardCharsets.UTF_8), 0);
}
```
✅ **Expected Output in Java Console**:  
```
📩 Received from MT4: {"Symbol":"GBPJPY", "Open":200.50, "High":201.20, "Low":200.10, "Close":200.80, "Volume":100000}
```  
If no messages appear, **MT4 is not sending requests**.

### **3️⃣ Check MT4 ZeroMQ Connection Logs**  
Modify **MQL4 EA (`ZeroMQClientEA.mq4`)** to print connection status:  
```mql4
int zmqContext, zmqSocket;

void ZeroMQ_Init() {
    zmqContext = zmq_ctx_new();
    zmqSocket = zmq_socket(zmqContext, ZMQ_REQ);
    
    Print("🔗 Connecting to AI Server...");
    int status = zmq_connect(zmqSocket, "tcp://127.0.0.1:5555");
    
    if (status == -1) {
        Print("🚨 ZeroMQ Connection Failed!");
        int errorCode = GetLastError();
        Print("❌ Error Code: ", errorCode);
    } else {
        Print("✅ Connected to AI Server");
    }
}
```
✅ **Expected Output in MT4 Logs**:  
```
🔗 Connecting to AI Server...
✅ Connected to AI Server
```
If **connection fails**, **check the AI server and firewall rules**.

### **4️⃣ Check Windows Firewall Rules for Port 5555**  
Run:  
```sh
netsh advfirewall firewall show rule name=all | findstr "5555"
```
✅ **Expected Output (Port 5555 Allowed)**:  
```
Rule Name: Allow ZeroMQ 5555
Enabled: Yes
Direction: In
Action: Allow
Protocol: TCP
Local Port: 5555
```
❌ **If No Output**, add the rule:  
```sh
netsh advfirewall firewall add rule name="Allow ZeroMQ 5555" dir=in action=allow protocol=TCP localport=5555
```
Then verify again:  
```sh
netsh advfirewall firewall show rule name=all | findstr "5555"
```

### **5️⃣ Restart Everything & Test Again**  
1. **Restart AI Server**:  
   ```sh
   mvn exec:java -Dexec.mainClass="com.trading.ai.ZeroMQAITradingServer"
   ```
2. **Restart MT4** and attach **ZeroMQClientEA to Chart**.
3. Check the **MT4 Logs** (`Experts Tab - Ctrl + T`) for:  
   ```
   ✅ Connected to AI Server
   📩 AI Response: {"signal":"BUY"}
   🚀 AI Signal: BUY - Simulated Trade
   ```

🚀 **If issues persist, re-run the above troubleshooting steps!**

