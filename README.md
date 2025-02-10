# Blockchain Simulation

## Introduction
This project is a **Blockchain Simulation** implemented in Java. It demonstrates the fundamental concepts of blockchain, such as block creation, mining (proof-of-work), and validation of the blockchain.

## Features
- **Block Creation**: Each block contains an index, timestamp, transaction data, previous block hash, and its own hash.
- **SHA-256 Hashing**: Uses SHA-256 to secure each block's data.
- **Proof-of-Work (Mining)**: Implements a mining mechanism to find a valid hash based on difficulty level.
- **Blockchain Validation**: Checks the integrity of the blockchain by verifying hashes and linking between blocks.
- **Genesis Block**: Initializes the blockchain with the first block.
- **Adding New Blocks**: Transactions can be added as new blocks to the blockchain.

## Prerequisites
- **Java JDK 8+**
- Any Java IDE (Eclipse, IntelliJ, VS Code, etc.)

## How It Works
1. **Create a Genesis Block**: The first block with a predefined hash.
2. **Add Transactions**: Blocks are created with transaction details and linked to the previous block.
3. **Mine Blocks**: Uses proof-of-work to ensure computational difficulty before adding blocks.
4. **Verify Blockchain Integrity**: Ensures that the chain remains valid and unaltered.

## Code Structure
### Block.java
- Represents a single block in the blockchain.
- Contains attributes such as `index`, `timestamp`, `transactions`, `previousHash`, `hash`, and `nonce`.
- Implements `computeHash()` to generate a SHA-256 hash.
- Implements `mineBlock(int difficulty)` to perform proof-of-work.

### Blockchain.java
- Represents the entire blockchain.
- Maintains an `ArrayList<Block>` to store the chain.
- Implements `addBlock()` to create and mine a new block.
- Implements `isChainValid()` to verify blockchain integrity.

### Main Class (Assignment_project.java)
- Initializes a blockchain with a difficulty level.
- Adds multiple blocks with transactions.
- Prints the blockchain details and verifies its integrity.

## How to Run
1. **Clone the repository**:
   ```bash
   git clone https://github.com/your-username/your-repo.git
   ```
2. **Navigate to the project directory**:
   ```bash
   cd your-repo
   ```
3. **Compile and Run**:
   ```bash
   javac Assignment_project.java
   java Assignment_project
   ```

## Sample Output
```
Block Mined: 0000a4f5bc...
Block Mined: 0000c7d8e1...
Index: 0
Timestamp: 1712345678901
Transactions: Genesis Block
Previous Hash: 0
Hash: 0000a4f5bc...
Nonce: 98231
--------------------------------------
Index: 1
Timestamp: 1712345689012
Transactions: Alice pays Bob 10 BTC
Previous Hash: 0000a4f5bc...
Hash: 0000c7d8e1...
Nonce: 123456
--------------------------------------
Blockchain is valid: true
```

## License
This project is open-source and available for learning purposes.

## Author
**Your Name** - Java Blockchain Enthusiast

