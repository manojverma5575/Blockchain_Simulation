import java.security.MessageDigest;
import java.util.ArrayList;
import java.util.Date;

// Class representing a Block in the Blockchain
class Block {
    public int index; // Block number
    public long timestamp; // Timestamp of block creation
    public String transactions; // Transactions stored in the block
    public String previousHash; // Hash of the previous block
    public String hash; // Hash of the current block
    public int nonce; // Used for proof-of-work

    // Constructor to create a new block
    public Block(int index, String transactions, String previousHash) {
        this.index = index;
        this.timestamp = new Date().getTime();
        this.transactions = transactions;
        this.previousHash = previousHash;
        this.nonce = 0;
        this.hash = computeHash(); // Generate hash for the block
    }

    // Method to compute the hash of the block
    public String computeHash() {
        String data = index + timestamp + transactions + previousHash + nonce;
        return applySHA256(data);
    }

    // Proof-of-work mechanism (mining)
    public void mineBlock(int difficulty) {
        String target = new String(new char[difficulty]).replace('\0', '0');
        while (!hash.substring(0, difficulty).equals(target)) {
            nonce++;
            hash = computeHash();
        }
        System.out.println("Block Mined: " + hash);
    }

    // Static method to apply SHA-256 hashing algorithm
    public static String applySHA256(String input) {
        try {
            MessageDigest digest = MessageDigest.getInstance("SHA-256");
            byte[] hash = digest.digest(input.getBytes("UTF-8"));
            StringBuilder hexString = new StringBuilder();
            for (byte b : hash) {
                String hex = Integer.toHexString(0xff & b);
                if (hex.length() == 1) hexString.append('0');
                hexString.append(hex);
            }
            return hexString.toString();
        } catch (Exception e) {
            throw new RuntimeException(e);
        }
    }
}

// Class representing the Blockchain
class Blockchain {
    private ArrayList<Block> chain; // List of blocks forming the chain
    private int difficulty; // Mining difficulty level

    // Constructor to initialize the blockchain
    public Blockchain(int difficulty) {
        this.chain = new ArrayList<>();
        this.difficulty = difficulty;
        chain.add(createGenesisBlock()); // Adding the first block
    }

    // Method to create the Genesis Block (First Block in the chain)
    private Block createGenesisBlock() {
        return new Block(0, "Genesis Block", "0");
    }

    // Method to get the latest block in the chain
    public Block getLatestBlock() {
        return chain.get(chain.size() - 1);
    }

    // Method to add a new block to the chain
    public void addBlock(String transactions) {
        Block newBlock = new Block(chain.size(), transactions, getLatestBlock().hash);
        newBlock.mineBlock(difficulty); // Mining the block before adding
        chain.add(newBlock);
    }

    // Method to validate the blockchain integrity
    public boolean isChainValid() {
        for (int i = 1; i < chain.size(); i++) {
            Block currentBlock = chain.get(i);
            Block previousBlock = chain.get(i - 1);

            // Check if the stored hash is valid
            if (!currentBlock.hash.equals(currentBlock.computeHash())) {
                return false;
            }
            // Check if the previous hash matches
            if (!currentBlock.previousHash.equals(previousBlock.hash)) {
                return false;
            }
        }
        return true;
    }

    // Method to print the blockchain details
    public void printBlockchain() {
        for (Block block : chain) {
            System.out.println("Index: " + block.index);
            System.out.println("Timestamp: " + block.timestamp);
            System.out.println("Transactions: " + block.transactions);
            System.out.println("Previous Hash: " + block.previousHash);
            System.out.println("Hash: " + block.hash);
            System.out.println("Nonce: " + block.nonce);
            System.out.println("--------------------------------------");
        }
    }
}

// Main class to run the blockchain simulation
public class Assginment_project  {
    public static void main(String[] args) {
        Blockchain blockchain = new Blockchain(4); // Set mining difficulty level
        blockchain.addBlock("Alice pays Bob 10 BTC"); // Adding first transaction block
        blockchain.addBlock("Bob pays Charlie 5 BTC"); // Adding second transaction block

        blockchain.printBlockchain(); // Print the blockchain details

        // Validate the blockchain integrity
        System.out.println("Blockchain is valid: " + blockchain.isChainValid());
    }
}

