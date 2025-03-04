# ZeroMQ Bridge for MetaTrader 4 (MT4) and Java

## 1. Introduction

This project provides a bridge for bidirectional communication between MetaTrader 4 (MT4) and a Java application using ZeroMQ (ZMQ).  It allows MT4 to send requests to the Java application and receive responses (using the REQ/REP pattern) or subscribe to data published by the Java application (using the PUB/SUB pattern). This enables integration of MT4 with external systems for advanced order management, data analysis, and other custom trading logic.

## 2. Architecture

The bridge comprises three main components:

*   **Java Server Application (`ZMQServer.java`):**  A standalone Java application that acts as the ZMQ server.  It listens for connections from MT4, processes requests, and either sends replies or publishes data.
*   **MQL4 Wrapper DLL (`MQL4ZMQ.dll`):**  A C++ Dynamic Link Library (DLL) that wraps the ZeroMQ library and exposes functions callable from MQL4.  This DLL acts as an intermediary, handling the low-level communication with ZeroMQ.
*   **MQL4 Expert Advisor (`ZMQBridgeEA.mq4`):** An MQL4 script that runs within MT4.  It uses the functions provided by the `MQL4ZMQ.dll` to communicate with the Java server.

## 3. Prerequisites

*   **Software:**
    *   MetaTrader 4 Platform
    *   Java Development Kit (JDK) - version 8 or later
    *   C++ Compiler (e.g., Microsoft Visual Studio on Windows, GCC on Linux)
    *   ZeroMQ Library (precompiled binaries, including `libzmq.dll`, `libzmq.lib`, `zmq.h`, and `zmq_utils.h`) - **Important:** Ensure you download the correct 32-bit or 64-bit version to match your MT4 installation. Download from: [https://zeromq.org/download/](https://zeromq.org/download/)
    *   JeroMQ (Java binding for ZeroMQ). Add the following to your Maven `pom.xml` or download the JAR:
        ```xml
        <dependency>
            <groupId>org.zeromq</groupId>
            <artifactId>jeromq</artifactId>
            <version>0.5.4</version>
        </dependency>
        ```
    *   Text Editor/IDE (e.g., VS Code, IntelliJ IDEA, MetaEditor)

*   **Knowledge:**
    *   Basic MQL4 programming
    *   Basic Java programming
    *   Familiarity with C++ (for the DLL)
    *   Understanding of ZeroMQ concepts

## 4. Project Structure
MT4-Java-ZMQ-Bridge/
├── JavaServer/          (Java project)
│   └── src/main/java/
│       └── com/example/
│           └── ZMQServer.java  (The main Java server)
├── MQL4Wrapper/        (C++ DLL project)
│   ├── zmq.h             (ZeroMQ header)
│   ├── zmq_utils.h      (ZeroMQ utils header)
│   ├── MQL4ZMQ.cpp      (The C++ wrapper source)
│   └── MQL4ZMQ.def      (Module definition file)
└── MT4EA/              (MQL4 files)
└── Experts/
└── ZMQBridgeEA.mq4  (The example Expert Advisor)
└── Include/
└── MQL4ZMQ.mqh      (MQL4 include file)

## 5. Setup and Installation

**5.1. Java Server (`JavaServer`)**

1.  **Create Project:** Create a new Java project in your IDE.
2.  **Add JeroMQ:** Add the JeroMQ dependency (Maven or JAR).
3.  **Copy Code:** Copy the provided `ZMQServer.java` code into your project, ensuring the package declaration matches your project structure.
4.  **Build:** Build the Java project.

**5.2. MQL4 Wrapper DLL (`MQL4Wrapper`)**

1.  **Create Project:** Create a new C++ DLL project in your IDE.
2.  **Add ZMQ:**
    *   Copy `zmq.h` and `zmq_utils.h` to your project.
    *   Add `libzmq.lib` to your linker settings (Project Properties -> Linker -> Input -> Additional Dependencies).
    *   Add the path to `libzmq.lib` to your library directories (Project Properties -> Linker -> General -> Additional Library Directories).
3.  **Copy Code:** Copy `MQL4ZMQ.cpp` and `MQL4ZMQ.def` into your project.
4.  **Build DLL:** Build the C++ project to create `MQL4ZMQ.dll`.
5.  **Place `libzmq.dll`:** Copy `libzmq.dll` to the *same directory* as `MQL4ZMQ.dll`.

**5.3. MQL4 Expert Advisor (`MT4EA`)**

1.  **MetaEditor:** Open MetaEditor from within MT4.
2.  **Create EA:** Create a new Expert Advisor named `ZMQBridgeEA`.
3.  **Copy Code:** Copy the provided `ZMQBridgeEA.mq4` code into the EA.
4.  **Create Include:** Create a new Include file named `MQL4ZMQ.mqh` in `MT4\MQL4\Include`. Copy the `#import` block from `ZMQBridgeEA.mq4` into `MQL4ZMQ.mqh`.
5.  **Copy DLLs:** Copy `MQL4ZMQ.dll` *and* `libzmq.dll` to the `MT4\MQL4\Libraries` directory.
6.  **Compile EA:** Compile `ZMQBridgeEA.mq4` in MetaEditor.

## 6. Running the Bridge

1.  **Start Java Server:** Run the `ZMQServer.java` application.
2.  **Attach EA:** In MT4, open a chart and drag `ZMQBridgeEA` onto it.
3.  **Enable DLL Imports:** In the EA's properties (Common tab), check "Allow DLL imports".
4.  **Observe Output:** Check the "Experts" tab in MT4's Terminal and the Java server's console for messages.

## 7. Troubleshooting

See the detailed troubleshooting section in the full integration document (provided in previous responses). Common issues include:

*   Missing DLLs (`MQL4ZMQ.dll` or `libzmq.dll`).
*   Incorrect DLL versions (32-bit vs. 64-bit mismatch).
*   Firewall blocking connections.
*   Incorrect ZMQ endpoints.
*   Java server not running.
*  "Allow DLL imports" not enabled.

## 8.  Key Files and Their Roles

*   **`ZMQServer.java`:** The main Java server application.  Handles ZMQ communication on the Java side (REQ/REP and PUB/SUB examples).
*   **`MQL4ZMQ.cpp`:** The C++ source code for the DLL.  Wraps the ZeroMQ functions and provides an interface for MQL4.
*   **`MQL4ZMQ.def`:**  A module definition file that specifies which functions in the DLL are exported and can be called from MQL4.
*   **`MQL4ZMQ.dll`:** The compiled DLL.  This is the bridge between MQL4 and the ZeroMQ library.
*   **`libzmq.dll`:** The core ZeroMQ library.  This is *essential* for the bridge to function.
*   **`ZMQBridgeEA.mq4`:** The MQL4 Expert Advisor that uses the DLL to communicate with the Java server.
*   **`MQL4ZMQ.mqh`:** An MQL4 include file containing the function prototypes for the DLL.  This makes it easier to use the DLL functions in multiple MQL4 scripts.

## 9. Customization

*   **Messaging Patterns:**  Choose REQ/REP, PUB/SUB, or other ZMQ patterns.
*   **Data Serialization:**  Use JSON (recommended), Protocol Buffers, or a custom format.
*   **Error Handling:** Implement robust error handling and logging.
*   **Security:** Use ZMQ's security features for network communication.

This README provides a concise overview of the MT4-Java ZeroMQ bridge project. Refer to the detailed integration guide for more in-depth explanations and troubleshooting steps.