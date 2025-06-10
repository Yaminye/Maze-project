# Maze project

A Java-based framework for generating, compressing, transmitting and solving mazes over a client-server architecture.  
Implements multiple maze generators and search algorithms, plus custom compressor/decompressor streams and JUnit test suites.

---

## Table of Contents

1. [Features](#features)  
2. [Prerequisites](#prerequisites)  
3. [Getting Started](#getting-started)  
4. [Project Structure](#project-structure)  
5. [Configuration](#configuration)  
6. [Running the Server & Client](#running-the-server--client)  
7. [Compression I/O](#compression-io)  
8. [Algorithms & Tests](#algorithms--tests)  
9. [Building the JAR](#building-the-jar)  
10. [Contributing](#contributing)  
11. [License](#license)  

---

## Features

- **Maze generation**  
  - Simple random maze generator  
- **Search algorithms**  
  - Depth-First Search (DFS)  
  - Breadth-First Search (BFS)  
  - Best-First Search (using heuristic)  
- **Client–Server communication**  
  - Transmit maze definitions from server to client  
  - Solve maze on the client side and return the solution  
- **Custom compressor/decompressor streams**  
  - `MyCompressorOutputStream` / `SimpleCompressorOutputStream`  
  - `MyDecompressorInputStream` / `SimpleDecompressorInputStream`  
- **JUnit test suites** for algorithms, I/O and end-to-end flows

---

## Prerequisites

- Java 8 or higher (JDK)  
- Maven or Gradle (optional, if you prefer to manage dependencies/build outside IntelliJ)  
- IntelliJ IDEA (project files provided), or any Java IDE / text editor  
- (Optional) Git for version control

---

## Getting Started

1. **Clone the repository**  
   ```bash
   git clone <your-repo-url>
   cd Maze-project
   ```

2. **Import into IntelliJ**  
   - Open `ATP-Project-PartA.iml` or the root directory as a project  
   - Let IntelliJ configure SDK and module settings  

3. **Configure properties** (see [Configuration](#configuration))

---

## Project Structure

```
Maze-project/
├── .idea/                     # IntelliJ configs
├── JUnit/
│   └── algorithms/search/BestFirstSearchTest.java
├── resources/
│   └── config.properties      # Server/client config
├── src/
│   ├── Client/
│   │   ├── Client.java
│   │   └── IClientStrategy.java
│   ├── IO/
│   │   ├── MyCompressorOutputStream.java
│   │   ├── SimpleCompressorOutputStream.java
│   │   ├── MyDecompressorInputStream.java
│   │   └── SimpleDecompressorInputStream.java
│   ├── Server/
│   │   └── Configurations.java
│   └── algorithms/
│       ├── mazeGenerators/
│       │   └── SimpleMazeGenerator.java
│       └── search/
│           ├── ASearchingAlgorithm.java
│           ├── AState.java
│           ├── BestFirstSearch.java
│           ├── BreadthFirstSearch.java
│           ├── DepthFirstSearch.java
│           ├── ISearchable.java
│           ├── ISearchingAlgorithm.java
│           ├── MazeState.java
│           └── SearchableMaze.java
└── src/test/
    ├── GeneralCheckingFunctions.java
    ├── RunCommunicateWithServers.java
    ├── RunCompressDecompressMaze.java
    ├── RunMazeGenerator.java
    └── RunSearchOnMaze.java
```

---

## Configuration

All configurable parameters live in `resources/config.properties`.  
Typical entries include:

```properties
# Server settings
server.port=5400
server.timeoutMs=5000

# Client settings
client.serverHost=127.0.0.1
client.serverPort=5400
client.timeoutMs=5000
```

Edit values as needed before starting.

---

## Running the Server & Client

1. **Start the Server**  
   ```bash
   cd out/production/ATP-Project-PartA   # or your build/classes folder
   java Server.Main
   ```
   or, if you have a fat JAR:
   ```bash
   java -jar ATP-Project-PartA.jar server
   ```

2. **Start the Client** (in a separate terminal)  
   ```bash
   java Client.Client
   ```
   You will be prompted to choose a maze size or a search strategy, then the solution steps will display.

---

## Compression I/O

To compress a maze’s byte array before transmitting:

```java
try (OutputStream out = 
       new SimpleCompressorOutputStream(
         new FileOutputStream("maze.deflated"))) {
    out.write(mazeByteArray);
}
```

To decompress:

```java
try (InputStream in =
       new SimpleDecompressorInputStream(
         new FileInputStream("maze.deflated"))) {
    byte[] data = in.readAllBytes();
}
```

---

## Algorithms & Tests

- **Maze generation:** `SimpleMazeGenerator`  
- **Search algorithms:** implement `ISearchingAlgorithm`  
  - `DepthFirstSearch`  
  - `BreadthFirstSearch`  
  - `BestFirstSearch` (uses `MazeState` heuristic)  

JUnit runners under `src/test/`:
- `RunMazeGenerator` – generate & serialize sample maze  
- `RunSearchOnMaze` – solve a maze end-to-end  
- `RunCompressDecompressMaze` – verify lossless compression  
- `RunCommunicateWithServers` – integration test client/server handshake  

To run all tests in IntelliJ, right-click `JUnit` folder → **Run ‘All Tests’**.

---

## Building the JAR

If you prefer a standalone JAR:

1. In IntelliJ:  
   - Open Project Artifacts (Preferences → Build, Execution, Deployment → Artifacts)  
   - Build “ATP-Project-PartA.jar”  

2. From command line (with Maven/Gradle):  
   ```bash
   mvn clean package
   # or
   gradle clean jar
   ```

---

## Contributing

1. Fork the repo  
2. Create a feature branch (`git checkout -b feature/NewAlgorithm`)  
3. Commit your changes (`git commit -m 'Add A* search'`)  
4. Push branch (`git push origin feature/NewAlgorithm`)  
5. Open a Pull Request  

Please include unit tests for any new algorithm or I/O class.

---

## License

This project is released under the MIT License. See [LICENSE](LICENSE) for details.
