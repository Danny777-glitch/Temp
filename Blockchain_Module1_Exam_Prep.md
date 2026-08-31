# Blockchain Technologies — Module I Exam Prep
**Pattern: 6 × 2 marks + 2 × 16 marks (choice) + 1 × 16 marks Scenario (choice)**

---

## PART A — 2 MARK QUESTIONS & ANSWERS (All 25)

### 1. Define Blockchain. Mention any two characteristics.
Blockchain is a distributed, decentralized digital ledger that records transactions across multiple computers in the form of linked, cryptographically secured blocks, such that the record cannot be altered retroactively.
**Characteristics:** (i) Decentralization – no single authority controls it. (ii) Immutability – once recorded, data cannot be changed.

### 2. Key features of Blockchain technology.
Decentralization, Immutability, Transparency, Security (cryptography-based), Consensus-driven validation, Distributed ledger, Anonymity/Pseudonymity.

### 3. Evolution of Blockchain (1.0 to 3.0).
- **Blockchain 1.0 – Currency:** Introduced with Bitcoin; used for cryptocurrency and payment applications.
- **Blockchain 2.0 – Smart Contracts:** Ethereum introduced programmable contracts for finance, real estate, etc.
- **Blockchain 3.0 – DApps:** Decentralized applications beyond finance — healthcare, governance, supply chain, IoT.

### 4. Chaining concept in Blockchain.
Each block contains the hash of the previous block along with its own transaction data and timestamp. This links blocks sequentially into a chain; changing any block changes its hash and breaks the chain, ensuring tamper-evidence.

### 5. Cryptographic token — define and list two types.
A cryptographic token is a digital asset issued on a blockchain representing value, utility, or ownership rights.
**Types:** Utility tokens, Security tokens (others: payment tokens, asset tokens).

### 6. Utility tokens vs Security tokens.
| Utility Token | Security Token |
|---|---|
| Gives access to a product/service on a platform | Represents ownership/investment (like equity) |
| Not regulated as a financial security | Subject to securities regulations |
| Example: filecoin (storage access) | Example: tokenized shares |

### 7. Hash function — define and two properties.
A hash function converts input data of any size into a fixed-size output (hash/digest).
**Properties:** (i) Deterministic – same input always gives same output. (ii) Collision-resistant – hard to find two inputs with the same hash. (Also: pre-image resistance, avalanche effect.)

### 8. Merkle Tree — define and purpose.
A Merkle Tree is a binary tree of hashes where leaf nodes are hashes of data blocks and each non-leaf node is a hash of its children, ending in a single root hash (Merkle Root).
**Purpose:** Efficiently and securely verifies the integrity/contents of large data sets (transactions) without needing the full data.

### 9. Consensus in Blockchain — define and importance.
Consensus is a mechanism by which distributed nodes agree on a single, valid version of the ledger. It is important because it eliminates the need for a central authority and prevents issues like double-spending.

### 10. PoW vs PoS.
| Proof of Work | Proof of Stake |
|---|---|
| Miners solve complex puzzles | Validators chosen based on coins staked |
| High energy consumption | Energy efficient |
| Used in Bitcoin | Used in Ethereum 2.0 |

### 11. Blockchain mining — define and objectives.
Mining is the process of validating transactions and adding them to the blockchain by solving computational puzzles.
**Objectives:** Validate transactions, secure the network, achieve consensus, and issue new coins as a reward.

### 12. Blockchain wallet — define; hot vs cold.
A wallet is software/hardware that stores public/private keys and enables users to send, receive, and manage crypto assets.
**Hot wallet:** Connected to the internet, convenient, less secure (e.g., mobile app wallets).
**Cold wallet:** Offline storage, more secure, less convenient (e.g., hardware wallets).

### 13. P2P networking — define and why used.
Peer-to-Peer networking is a decentralized network model where each node (peer) communicates directly with others without a central server. It is used in blockchain to distribute the ledger, avoid single points of failure, and maintain decentralization.

### 14. Four types of Blockchain nodes.
Full nodes, Light (SPV) nodes, Mining nodes, Master nodes (also: Archival nodes, Staking nodes).

### 15. Four security features of Blockchain.
Cryptographic hashing, Digital signatures, Consensus mechanisms, Immutability of ledger (also: decentralization, encryption).

### 16. How data is stored; why immutable.
Data is stored in blocks containing transaction records, timestamp, and the previous block's hash, linked in a chain and replicated across nodes. It is immutable because altering any block changes its hash, breaking the chain link, which is immediately detectable across the distributed network.

### 17. Four risks associated with Blockchain solutions.
51% attack, Private key loss/theft, Scalability issues, Regulatory/legal uncertainty (also: smart contract bugs, energy consumption).

### 18. Life cycle of a Blockchain transaction (draw & explain).
1. Transaction initiated by user (signed with private key).
2. Broadcast to P2P network.
3. Nodes validate the transaction.
4. Transaction added to a candidate block.
5. Consensus mechanism validates the block (mining/staking).
6. Block appended to the chain.
7. Transaction confirmed and immutable.

*(Diagram: User → Sign Tx → Broadcast → Validation → Block Formation → Consensus → Append to Chain → Confirmed)*

### 19. Blockchain Relevance Evaluation Framework.
A structured framework used to assess whether blockchain is the right solution for a given business problem, evaluating factors like need for shared data, multiple writers, absence of trust, and need for disintermediation. It is used to avoid adopting blockchain unnecessarily where a traditional database would suffice.

### 20. Blockchain Reference Architecture — major components.
Application layer, Smart contract layer, Consensus layer, Network (P2P) layer, Data/Ledger layer, Infrastructure/Hardware layer.

### 21. Public vs Private vs Consortium vs Hybrid blockchains.
- **Public:** Open to anyone, fully decentralized (e.g., Bitcoin).
- **Private:** Restricted access, controlled by one organization.
- **Consortium:** Controlled by a group of organizations (semi-decentralized).
- **Hybrid:** Combines public and private features — some data open, some restricted.

### 22. Major layers of Blockchain architecture.
- **Application layer:** DApps, smart contracts UI.
- **Execution layer:** Smart contract execution.
- **Consensus layer:** Validates and agrees on blocks.
- **Network layer:** P2P communication between nodes.
- **Data layer:** Blocks, hashes, Merkle trees, ledger storage.

### 23. Key considerations while architecting a Blockchain solution.
Scalability, Security, Privacy, Interoperability, Governance, Performance/throughput, Consensus mechanism choice, Regulatory compliance.

### 24. Steps in designing a Blockchain application.
1. Requirement analysis, 2. Choose blockchain type (public/private/consortium), 3. Select platform, 4. Design architecture & data model, 5. Develop smart contracts, 6. Test, 7. Deploy, 8. Monitor & maintain.

### 25. Factors to evaluate before implementing Blockchain.
Need for decentralization, number of stakeholders, trust deficit among parties, transaction volume/scalability needs, cost vs benefit, regulatory environment, data privacy requirements.

---

## PART B — IMPORTANT 16 MARK QUESTIONS (with choice pairs to prepare)

### Q1. Characteristics of Blockchain and their significance
**Answer outline:**
- **Decentralization:** No central authority; control distributed among nodes → removes single point of failure, builds trust.
- **Immutability:** Once written, data cannot be altered → ensures data integrity, audit trail.
- **Transparency:** All participants can view the ledger (in public chains) → builds accountability.
- **Security:** Cryptographic hashing + digital signatures → protects against tampering and fraud.
- **Consensus-driven:** Validation happens via agreed protocols (PoW/PoS) → eliminates need for intermediaries.
- **Anonymity/Pseudonymity:** Users transact via addresses, not identities → privacy.
- **Distributed ledger:** Copies maintained across nodes → resilience and fault tolerance.
- **Significance:** Together these enable trustless transactions, reduce fraud, cut intermediary costs, and support secure decentralized systems across finance, supply chain, healthcare, etc.

### Q2. Evolution of Blockchain (1.0 → 4.0) + chaining concept diagram
- **1.0 – Currency (Bitcoin):** Peer-to-peer digital cash, no intermediaries.
- **2.0 – Smart Contracts (Ethereum):** Self-executing code enabling DApps, ICOs, DeFi.
- **3.0 – DApps:** Blockchain applied beyond finance — governance, healthcare, IoT, identity.
- **4.0 – Industry Integration:** Blockchain integrated with AI, IoT, big data for enterprise/Industry 4.0 use cases.
- **Chaining concept:** Each block header stores the hash of the previous block. Block N's hash depends on Block N-1's hash, transactions, and timestamp — forming an unbreakable, tamper-evident chain.
*(Diagram: [Block 1: Hash0, Data, Hash1] → [Block 2: Hash1, Data, Hash2] → [Block 3: Hash2, Data, Hash3])*

### Q6. Compare PoW, PoS, DPoS
| Mechanism | Working | Pros | Cons |
|---|---|---|---|
| PoW | Miners solve cryptographic puzzles | Highly secure, battle-tested | Energy-intensive, slow |
| PoS | Validators chosen by stake amount | Energy efficient, faster | Rich-get-richer risk |
| DPoS | Stakeholders vote for delegates who validate | Very fast, democratic | More centralized, trust in delegates |

### Q9. Security mechanisms & threats
**Mechanisms:** Cryptographic hashing, digital signatures (public/private key pairs), consensus protocols, immutability, encryption of data, multi-signature wallets.
**Threats:** 51% attack, Sybil attack, double spending, phishing, private key theft, smart contract vulnerabilities.
**Mitigations:** Strong consensus design, decentralization, cold storage of keys, code audits, multi-factor authentication.

### Q14 / #18 (Part A basis). Life cycle of a Blockchain transaction
(Expand Part A Answer 18 into full 16-mark form with diagram + explanation of each stage: initiation, broadcasting, validation, mining/block formation, consensus, appending, confirmation — plus discuss role of nodes and finality.)

### Q16. Blockchain Reference Architecture — layers
Explain each layer in detail:
1. **Application Layer** – End-user DApps and interfaces.
2. **Smart Contract/Execution Layer** – Business logic execution (e.g., EVM).
3. **Consensus Layer** – Agreement protocol (PoW/PoS/PBFT).
4. **Network Layer** – P2P node communication, gossip protocol.
5. **Data Layer** – Blocks, Merkle trees, cryptographic hashes, ledger.
6. **Infrastructure Layer** – Hardware, storage, nodes.
Draw as a stacked layer diagram, top to bottom.

### Q17. Key architectural considerations
Scalability (throughput, sharding), Privacy (public vs permissioned data), Interoperability (cross-chain communication), Governance (who controls upgrades/rules), Performance (latency, transaction speed), Security, Cost of consensus.

### Q18. Compare Bitcoin, Ethereum, Hyperledger Fabric, Corda
| Platform | Type | Consensus | Use Case |
|---|---|---|---|
| Bitcoin | Public | PoW | Digital currency |
| Ethereum | Public | PoS (post-merge) | Smart contracts/DApps |
| Hyperledger Fabric | Permissioned | PBFT/Raft | Enterprise use cases |
| Corda | Permissioned | Notary-based | Finance/legal agreements |

### Q19. Approach for developing a Blockchain application
1. Requirement gathering & problem definition, 2. Feasibility/relevance check, 3. Choose blockchain type & platform, 4. Design architecture (nodes, consensus, data model), 5. Develop smart contracts, 6. Build front-end/DApp, 7. Testing (unit, security audit), 8. Deployment on testnet then mainnet, 9. Monitoring and maintenance.

---

## SCENARIO-BASED QUESTION (16 Marks)

**Question:** A supply chain company plans to implement a Blockchain-based solution for product traceability. Explain how you would design the Blockchain architecture, select an appropriate platform, define the transaction flow, and address security and scalability considerations.

**Model Answer:**

**1. Problem Understanding:**
The company needs to track a product from raw material to end customer, ensuring transparency, authenticity, and prevention of counterfeiting/fraud among multiple stakeholders (suppliers, manufacturers, distributors, retailers).

**2. Relevance Check (Blockchain Relevance Evaluation):**
- Multiple untrusted parties? Yes.
- Need for shared, tamper-proof record? Yes.
- Need to remove intermediaries? Yes.
→ Blockchain is justified here.

**3. Choice of Blockchain Type:**
A **Consortium/Permissioned blockchain** (e.g., Hyperledger Fabric) is most suitable since participants are known business entities (suppliers, manufacturers, retailers) who need controlled access, not full public anonymity.

**4. Platform Selection:**
Hyperledger Fabric is preferred because it supports permissioned access, channel-based privacy between partners, pluggable consensus, and chaincode (smart contracts) for business logic — ideal for enterprise supply chains. (Ethereum could be an alternative if a more open, tokenized ecosystem is desired.)

**5. Architecture Design:**
- **Application Layer:** Web/mobile DApp for stakeholders to scan and update product status (QR/RFID integration).
- **Smart Contract (Chaincode) Layer:** Encodes rules — e.g., only the current custodian can update status; ownership transfer logic.
- **Consensus Layer:** Practical Byzantine Fault Tolerance (PBFT) or Raft for fast, permissioned consensus.
- **Network Layer:** P2P network of nodes representing each organization (supplier, manufacturer, distributor, retailer).
- **Data Layer:** Each product batch gets a unique ID; every movement/transformation recorded as a transaction, linked via hashes; Merkle tree used for efficient verification.

**6. Transaction Flow:**
1. Raw material supplier registers batch on-chain (creates asset with unique ID).
2. Manufacturer records processing/transformation as a new transaction linked to the batch ID.
3. Distributor updates shipment and custody transfer.
4. Retailer records final receipt; consumer can scan QR to view full provenance.
5. Each step is validated by relevant peer nodes and committed via consensus before appending to the ledger.

**7. Security Considerations:**
- Use digital signatures for every stakeholder action (non-repudiation).
- Role-based access control — only authorized nodes can write specific data.
- Encrypt sensitive commercial data; use channels/private data collections for confidentiality between competing partners.
- Regular smart contract audits to prevent logic exploits.

**8. Scalability Considerations:**
- Use off-chain storage (e.g., IPFS) for large files (certificates, images) with only hashes stored on-chain.
- Choose a lightweight, fast consensus (PBFT/Raft) rather than energy-heavy PoW, since participants are permissioned and trust is partially established.
- Use sharding/channels to separate data by product line or region, reducing node load.

**9. Conclusion:**
This design ensures end-to-end traceability, tamper-proof history, reduced fraud, and trust among stakeholders, while balancing performance and privacy needs of the supply chain — directly leveraging blockchain's core characteristics of immutability, decentralization, and consensus-based trust.

---

## Quick Revision Checklist
- [ ] All 25 Part-A definitions memorized (short crisp 2-mark answers)
- [ ] PoW vs PoS, Public vs Private vs Consortium vs Hybrid tables
- [ ] Transaction life cycle diagram
- [ ] Blockchain Reference Architecture layers
- [ ] Scenario answer structure (Problem → Type → Platform → Architecture → Flow → Security → Scalability → Conclusion)

**Good luck for your exam tomorrow!**
