# ATP Project Part A

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
   cd ATP-Project-PartA
