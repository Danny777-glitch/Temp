# BCT_QP.md

# Blockchain Technologies -- Module 1

## Previous Year Question Paper -- Detailed Exam Answers

**16-mark formula:** Introduction → Objectives → Architecture/Diagram →
Components → Working → Security/Advantages → Conclusion.

------------------------------------------------------------------------

# PART A -- SHORT ANSWERS

## Q1. Importance of Blockchain Technology for real-world security

Blockchain is a distributed ledger technology that records transactions
across multiple participating nodes. It improves security using
**decentralization, cryptography, consensus and immutability**.

### Points

1.  **Decentralization:** Data is distributed across several nodes,
    reducing a single point of failure.
2.  **Immutability:** Valid records are difficult to alter after being
    added to the chain.
3.  **Cryptographic security:** Hashing protects integrity and digital
    signatures authenticate transactions.
4.  **Transparency:** Authorized participants can verify recorded
    transactions.
5.  **Traceability:** Transactions can be followed through their
    history.
6.  **Fault tolerance:** Failure of one node does not necessarily
    destroy the complete ledger.

**Conclusion:** Blockchain provides a tamper-resistant, transparent and
decentralized method for maintaining trusted records.

**Keywords:** Decentralization, Immutability, Cryptography, Consensus,
Transparency, Traceability.

------------------------------------------------------------------------

## Q2. Risks of blockchain-based banking transaction systems

1.  **51% attack:** Majority control of consensus power can potentially
    enable transaction-history manipulation.
2.  **Private key theft:** A stolen key can enable unauthorized
    transactions.
3.  **Smart contract bugs:** Coding errors may cause incorrect execution
    or financial loss.
4.  **Scalability:** High transaction volume can cause delay or
    performance problems.
5.  **Privacy:** Poor design may expose sensitive financial information.
6.  **Regulation:** Banking applications must satisfy legal and
    compliance requirements.
7.  **Interoperability:** Blockchain must integrate with existing
    banking systems.
8.  **Key loss:** Lost private keys can make assets or records
    inaccessible.

**Conclusion:** Strong key management, encryption, access control,
auditing and secure smart contracts are required.

------------------------------------------------------------------------

## Q3. Role of Merkle Tree in blockchain

A **Merkle Tree** is a hierarchical structure of cryptographic hashes
used to efficiently verify transaction integrity.

``` text
                         Merkle Root
                             H1234
                           /                               H12         H34
                       /  \        /                       H1   H2      H3   H4
                     |    |       |    |
                    Tx1  Tx2     Tx3  Tx4
```

### Points

-   Every transaction is converted into a hash.
-   Hashes are combined pairwise until one **Merkle Root** remains.
-   The Merkle Root is stored in the block header.
-   Any transaction modification changes its hash and ultimately the
    root.
-   A **Merkle Proof** allows efficient verification without checking
    every transaction.

**Conclusion:** Merkle Trees provide efficient, compact and
tamper-evident transaction verification.

------------------------------------------------------------------------

## Q4. Differentiate Coin and Token

  -----------------------------------------------------------------------
  Coin                                Token
  ----------------------------------- -----------------------------------
  Normally has its own blockchain.    Normally runs on an existing
                                      blockchain.

  Usually represents the network's    Can represent utility, assets,
  native digital asset.               rights or other values.

  Requires its own blockchain         Uses the underlying blockchain
  infrastructure.                     infrastructure.

  Examples: Bitcoin, Ether.           Example: ERC-20 tokens.

  Often used to pay network fees.     Usually uses the underlying coin
                                      for network fees.
  -----------------------------------------------------------------------

**Memory:** Coin = own blockchain; Token = existing blockchain.

------------------------------------------------------------------------

## Q5. Structural diagram of a block

``` text
+----------------------------------------------+
|                    BLOCK                     |
+----------------------------------------------+
|                 BLOCK HEADER                 |
| Previous Block Hash                          |
| Timestamp                                    |
| Merkle Root                                  |
| Nonce                                        |
| Version / Difficulty Information             |
+----------------------------------------------+
|                 TRANSACTIONS                 |
| Transaction 1                                |
| Transaction 2                                |
| Transaction 3                                |
| ...                                          |
+----------------------------------------------+
```

### Components

-   **Previous Block Hash:** links the current block to the previous
    block.
-   **Timestamp:** records block-related time information.
-   **Merkle Root:** represents all transactions through their hashes.
-   **Nonce:** used in Proof-of-Work mining.
-   **Transactions:** records included in the block.

**Key point:** Previous hash creates the chain; Merkle Root protects
transaction integrity.

------------------------------------------------------------------------

## Q6. Example of Avalanche Effect

The **Avalanche Effect** means a small change in input produces a large
and unpredictable change in a cryptographic hash.

``` text
BLOCKCHAIN
    ↓ SHA-256
   Hash A

BLOCKCHAIN.
    ↓ SHA-256
   Hash B
```

Only a small input change can make the entire hash output different.

### Importance

-   Detects small data changes.
-   Strengthens integrity.
-   Makes hash prediction difficult.
-   Helps prevent unnoticed manipulation.

------------------------------------------------------------------------

# PART B -- DESCRIPTIVE QUESTIONS

# Q7(a). DRMCET digital certificates using Merkle Trees

## 1. Introduction

A university can issue digital certificates using blockchain so that
certificates become easy to verify and tamper-evident. Each certificate
is converted into a cryptographic hash. Certificate hashes are organized
into a **Merkle Tree**, and the final Merkle Root is recorded on
blockchain.

## 2. Objectives

-   Certificate authenticity.
-   Certificate integrity.
-   Tamper detection.
-   Efficient verification.
-   Permanent audit trail.
-   Reduction of certificate forgery.
-   Easy verification by employers.

## 3. Architecture

``` text
                    UNIVERSITY
                        |
                 Issue Certificate
                        |
                        v
              +-------------------+
              | Digital Certificate|
              +---------+---------+
                        |
                        v
                    SHA-256
                        |
                        v
                 Certificate Hashes
                    H1 H2 H3 H4
                        |
                        v
                  Merkle Tree
                        |
                        v
                   Merkle Root
                        |
                        v
                  Blockchain
                 /     |                   Node 1  Node 2  Node 3
```

## 4. Certificate creation

A certificate can contain student name, register number, course,
department, grade, year, certificate ID and issuing institution.

The certificate is passed through SHA-256:

``` text
Certificate Data → SHA-256 → Certificate Hash
```

A hash acts as a digital fingerprint of the data.

## 5. Merkle Tree construction

For four certificates:

``` text
Certificate 1 → H1
Certificate 2 → H2
Certificate 3 → H3
Certificate 4 → H4
```

``` text
                         MERKLE ROOT
                              |
                         H(H12 + H34)
                         /                                  H12           H34
                      /  \          /                      H1   H2       H3   H4
                    |    |        |    |
                   C1   C2       C3   C4
```

H12 = Hash(H1 + H2)\
H34 = Hash(H3 + H4)\
Root = Hash(H12 + H34)

The Merkle Root is stored in the block header.

## 6. Blockchain storage

A practical system can store: - Certificate ID. - Certificate hash. -
Merkle Root/proof information. - Issuer information. - Timestamp. -
Transaction metadata.

Large certificate files can be kept in secure off-chain storage while
their hashes are recorded on-chain.

## 7. Verification of Certificate 2

1.  Obtain Certificate 2.
2.  Calculate H2 using SHA-256.
3.  Obtain the required Merkle proof, such as H1 and H34.
4.  Calculate H12 = Hash(H1 + H2).
5.  Calculate Root' = Hash(H12 + H34).
6.  Compare Root' with the blockchain Merkle Root.

``` text
Certificate 2 → H2
                 + H1 → H12
                       + H34 → Calculated Root
                                  ↓
                          Compare with
                       Blockchain Root
```

If both roots match, the certificate is consistent with the recorded
certificate set. If they do not match, the certificate or proof is
invalid or the data may have been modified.

## 8. Efficient verification

A Merkle Proof contains only the hashes needed along the path from the
selected transaction to the root. For a balanced binary tree, proof size
grows approximately as **O(log n)** instead of requiring all n
transactions.

## 9. Security

-   **Integrity:** changed certificate → changed hash.
-   **Tamper detection:** changed leaf affects parent hashes and root.
-   **Authenticity:** university digital signatures can establish the
    issuer.
-   **Immutability:** blockchain makes historical alteration difficult.
-   **Efficiency:** only a Merkle Proof is needed for individual
    verification.

## 10. Advantages

1.  Fast verification.
2.  Less verification data.
3.  Tamper detection.
4.  Permanent audit trail.
5.  Scalable for many certificates.
6.  Reduces manual verification.
7.  Helps prevent forged certificates.

## Conclusion

A combination of **hashing, Merkle Trees, Merkle Proofs, digital
signatures and blockchain** provides secure and efficient digital
certificate verification.

------------------------------------------------------------------------

# Q7(b). ShopSafe e-commerce encryption solution

## 1. Introduction

Online transactions contain customer, order and payment information.
ShopSafe must protect **confidentiality, integrity and authenticity**
using a combination of symmetric encryption, asymmetric cryptography,
hashing and digital signatures.

## 2. Security objectives

-   **Confidentiality:** prevent unauthorized reading.
-   **Integrity:** detect modification.
-   **Authenticity:** verify the sender or transaction origin.
-   **Non-repudiation:** signatures can provide evidence associated with
    the signer under the relevant identity and signature system.

## 3. Symmetric encryption

Symmetric encryption uses the same secret key for encryption and
decryption.

``` text
Plaintext
   ↓
Secret Key + Encryption
   ↓
Ciphertext
   ↓
Secret Key + Decryption
   ↓
Plaintext
```

Example: **AES**

### Advantages

-   Fast.
-   Efficient for large data.
-   Suitable for high-volume transactions.

### Limitation

The secret key must be established and protected securely.

## 4. Asymmetric encryption

Asymmetric cryptography uses: - **Public Key** - **Private Key**

Examples: RSA and ECC.

``` text
          Key Pair
          /          Public Key  Private Key
```

The public key can be distributed; the private key must remain secret.

## 5. Public/private keys for confidentiality

``` text
Customer
   |
Transaction Data
   |
Encrypt using ShopSafe Public Key
   |
Ciphertext
   |
ShopSafe
   |
Decrypt using ShopSafe Private Key
   |
Original Data
```

## 6. Hashing for integrity

``` text
Transaction Data
      ↓
   SHA-256
      ↓
   Hash Value
```

If data changes, its hash changes:

``` text
Original Data  → Hash A
Modified Data  → Hash B
```

If Hash A ≠ Hash B, modification is detected.

## 7. Digital signature for authenticity

``` text
Transaction
    ↓
   Hash
    ↓
Message Digest
    ↓
Sign using Sender Private Key
    ↓
Digital Signature
```

The receiver verifies the signature using the sender's public key.

It supports authentication, integrity and non-repudiation properties.

## 8. Key usage table

  Operation                    Key
  ---------------------------- ----------------------
  Encrypt for ShopSafe         ShopSafe Public Key
  Decrypt corresponding data   ShopSafe Private Key
  Create digital signature     Sender Private Key
  Verify digital signature     Sender Public Key

## 9. Complete architecture

``` text
                    CUSTOMER
                       |
                  Transaction
                       |
             +---------+---------+
             |                   |
             v                   v
          Hashing            Encryption
             |                   |
             v                   v
       Message Digest         AES/Data Key
             |                   |
             v                   v
      Digital Signature       Ciphertext
             |                   |
             +---------+---------+
                       |
                 Secure Channel
                       |
                       v
                    SHOPSAFE
                 /                           v             v
       Verify Signature    Decrypt Data
                |             |
                +------ +-----+
                       |
                Process Order
```

## 10. Key management

ShopSafe should use secure key storage, key rotation, access control,
certificate-based identity management and protection against private-key
theft.

## Conclusion

Use **AES for efficient confidentiality, public/private-key cryptography
for secure key establishment or protected communication, hashing for
integrity and digital signatures for authenticity**.

------------------------------------------------------------------------

# Q8(a). FreshTrack blockchain supply chain

## 1. Introduction

Supply chains involve multiple independent participants. Separate
databases can produce inconsistent records. FreshTrack can use a
**permissioned blockchain** to provide a shared, traceable and
tamper-evident ledger.

Participants: - Farmers. - Transporters. - Warehouses. - Distributors. -
Retailers. - Auditors. - Customers.

## 2. Objectives

-   Track product origin.
-   Track batches.
-   Monitor quality.
-   Track custody/ownership.
-   Secure information sharing.
-   Detect tampering.
-   Improve auditing.
-   Reduce disputes.

## 3. Reference architecture

``` text
+------------------------------------------------+
| APPLICATION LAYER                              |
| Farmer App | Retailer App | Customer Portal   |
+-------------------------+----------------------+
                          |
+------------------------------------------------+
| API / SERVICE LAYER                            |
| Identity | Data Access | System Integration   |
+-------------------------+----------------------+
                          |
+------------------------------------------------+
| SMART CONTRACT LAYER                           |
| Quality | Ownership | Delivery | Payment       |
+-------------------------+----------------------+
                          |
+------------------------------------------------+
| BLOCKCHAIN / LEDGER LAYER                      |
| Blocks | Transactions | Distributed Ledger     |
+-------------------------+----------------------+
                          |
+------------------------------------------------+
| CONSENSUS LAYER                                |
| Transaction Validation / Agreement             |
+-------------------------+----------------------+
                          |
+------------------------------------------------+
| NETWORK / PARTICIPANTS                         |
| Farmer | Transporter | Warehouse | Retailer    |
+------------------------------------------------+
```

## 4. Farm registration

The farmer records: - Product ID. - Batch ID. - Farm identity. - Harvest
date. - Product type. - Quantity.

The transaction is digitally signed.

## 5. Quality monitoring

Record: - Temperature. - Humidity. - Weight. - Grade. - Inspection
result. - Expiry date.

IoT devices can provide environmental data.

Example:

``` text
IF temperature > permitted limit
THEN create Quality Risk alert
```

## 6. Transportation

The custody transfer is recorded:

``` text
Farmer → Transporter → Warehouse
```

GPS/IoT systems may provide location and environmental information.

## 7. Warehouse

Record arrival time, batch number, quantity, storage conditions and
inspection results.

## 8. Distribution

``` text
Farmer
  ↓
Transporter
  ↓
Warehouse
  ↓
Distributor
  ↓
Retailer
  ↓
Consumer
```

Each important custody/ownership change can be recorded as a
transaction.

## 9. Smart contracts

Examples:

``` text
IF temperature exceeds threshold
THEN create quality alert

IF delivery confirmed
THEN update custody status

IF delivery and quality conditions are satisfied
THEN trigger payment process
```

## 10. Information management across nodes

``` text
             Blockchain Network
          /          |                 Farm Node  Warehouse Node  Retailer Node
          \          |           /
                 Shared Ledger
```

Typical flow:

``` text
Transaction
    ↓
Digital Signature
    ↓
Validation
    ↓
Consensus
    ↓
Block Added
    ↓
Ledger State Updated
```

## 11. On-chain and off-chain data

Continuous sensor readings and large files can be stored off-chain.
Blockchain can store: - Hash. - Timestamp. - Batch ID. - Status. -
Reference information.

## 12. Benefits

-   Transparency.
-   End-to-end traceability.
-   Quality monitoring.
-   Tamper resistance.
-   Faster auditing.
-   Counterfeit reduction.
-   Better coordination.

## Conclusion

A **permissioned blockchain + smart contracts + IoT + digital
signatures + distributed ledger** gives FreshTrack secure end-to-end
supply-chain visibility.

------------------------------------------------------------------------

# Q8(b). AuthenticLux product authenticity and ownership

## 1. Introduction

Counterfeit luxury goods are difficult to distinguish from genuine
products. AuthenticLux can give every physical product a unique digital
identity linked to a blockchain record.

## 2. Objectives

-   Authenticity.
-   Provenance.
-   Ownership history.
-   Secure ownership transfer.
-   Counterfeit detection.
-   Customer verification.
-   Warranty/service tracking.

## 3. Basic architecture

``` text
AuthenticLux
     |
Product Creation
     |
Unique Product ID
     |
Digital Identity
     |
+----+----------------+
|                     |
v                     v
QR/NFC/RFID        Blockchain
Physical Tag          Record
|                     |
+----------+----------+
           |
           v
   Customer Verification
```

## 4. Product registration

Store: - Product ID. - Serial number. - Model. - Manufacturing date. -
Factory. - Batch. - Warranty information.

A hash can be associated with the blockchain record.

## 5. Permissioned blockchain

Authorized participants can include manufacturer, dealers, retailers and
service centres.

``` text
Manufacturer
      |
Permissioned Blockchain
 /       |        Dealer  Retailer  Service Centre
```

### Advantages

-   Controlled participation.
-   Privacy.
-   Known participants.
-   Enterprise-friendly governance.

## 6. Public blockchain

Selected proofs can be recorded publicly for customer verification.

### Advantages

-   Transparency.
-   Public verification.
-   Stronger external auditability.

### Limitation

Sensitive business information should not be exposed unnecessarily.

## 7. Hybrid blockchain

``` text
PRIVATE SYSTEM
Sensitive Product/Business Data
          |
       Hash/Proof
          ↓
PUBLIC BLOCKCHAIN
          |
Public Authenticity Verification
```

This balances privacy and public verification.

## 8. QR/NFC/RFID

``` text
Product
  ↓
QR / NFC / RFID
  ↓
Product ID
  ↓
Blockchain Record
  ↓
Authenticity + Ownership
```

The physical tag itself must be protected from cloning/replacement.
Blockchain cannot by itself prove that a physical tag has not been
copied.

## 9. Ownership transfer

``` text
Owner A
   ↓
Ownership Transfer Transaction
   ↓
Smart Contract
   ↓
Blockchain
   ↓
Owner B
```

## 10. Smart contract

``` text
IF seller authorized
AND buyer verified
AND required payment condition satisfied
THEN transfer ownership
```

## 11. Data storage

### On-chain

-   Product ID.
-   Ownership events.
-   Certificate hash.
-   Timestamps.
-   Verification proofs.

### Off-chain

-   High-resolution images.
-   Detailed invoices.
-   Service documents.
-   Private customer data.

## 12. Benefits

-   Counterfeit detection.
-   Traceable ownership.
-   Product provenance.
-   Customer confidence.
-   Easier resale verification.
-   Tamper-evident history.
-   Better warranty/service tracking.

## Conclusion

A **permissioned or hybrid blockchain with digital identity,
QR/NFC/RFID, hashing and smart contracts** can create a verifiable
authenticity and ownership history.

------------------------------------------------------------------------

# PART C -- SCENARIO BASED QUESTIONS

# Q9(a). Blockchain architecture for patient health records

## 1. Introduction

Healthcare records contain diagnoses, prescriptions, laboratory results,
scans and treatment history. A blockchain solution can improve
**integrity, auditability, controlled sharing and traceability**.

Complete medical files should generally not be placed directly on-chain.
A practical design stores encrypted records off-chain and stores hashes,
permissions and audit metadata on a permissioned blockchain.

## 2. Requirements

-   Patient privacy.
-   Data integrity.
-   Controlled access.
-   Secure sharing.
-   Auditability.
-   Tamper detection.
-   Availability.
-   Traceable access.

## 3. Architecture

``` text
                         PATIENT
                            |
                            v
                    Patient Portal
                            |
                            v
                     API / Gateway
                     /                               v             v
        Identity & Access     Encrypted
           Management       Off-chain Storage
                    |
                    v
              Smart Contracts
                    |
                    v
        +-----------------------------+
        |    PERMISSIONED BLOCKCHAIN  |
        | Patient/Record ID           |
        | Record Hash                 |
        | Permissions                 |
        | Timestamp                   |
        | Audit Information           |
        +-----------------------------+
             /        |                    v         v         v
       Hospital     Doctor      Lab
          Node        Node      Node
```

## 4. Why permissioned blockchain?

Healthcare data is sensitive. Only approved participants should interact
with the network.

Possible participants: - Hospitals. - Doctors. - Laboratories. -
Pharmacies. - Insurers. - Patients. - Authorized health authorities.

## 5. Record creation

Doctor creates a record containing diagnosis, prescription, test
results, date and doctor ID.

``` text
Medical Record → Encryption → Encrypted Record
```

## 6. Off-chain storage

Large files such as MRI scans, X-rays, CT scans and PDFs can be stored
securely off-chain.

Blockchain stores a cryptographic hash and relevant reference/metadata.

## 7. Hash generation

``` text
Medical Record
      ↓
    SHA-256
      ↓
Record Hash
```

If the record changes, the hash changes.

## 8. Blockchain transaction

Possible fields: - Patient ID. - Record ID. - Record hash. - Doctor
ID. - Timestamp. - Access permissions. - Storage reference.

The transaction is validated before being added to the ledger.

## 9. Consensus and nodes

``` text
New Transaction
       ↓
Digital Signature
       ↓
Validation
       ↓
Consensus
       ↓
Block Creation
       ↓
Ledger Update
       ↓
Authorized Nodes
```

## 10. Access control

``` text
Patient
   |
Permission
   ↓
Smart Contract
   |
   ↓
Authorized Doctor
   |
   ↓
Encrypted Record
```

Role-based access can be applied: - Doctor: treatment-related records. -
Lab: relevant test records. - Insurance: authorized billing
information. - Patient: own records.

## 11. Smart contracts

``` text
IF doctor is authorized
AND patient permission is valid
THEN allow access
ELSE deny access
```

Access events can also be logged.

## 12. Integrity verification

``` text
Retrieved Record
      ↓
Calculate Hash
      ↓
Compare with Blockchain Hash
      ↓
    Match?
   /       YES       NO
 |          |
Valid     Possible
Record    Modification
```

## 13. Node management

``` text
Hospital Node
      |
Doctor Node ---- Blockchain ---- Laboratory Node
      |
Insurance Node
```

Authorized nodes maintain/access ledger state according to the network's
permission model. No single node needs to be the only authoritative
copy.

## 14. Privacy

Use: - Encryption. - Permissioned access. - Role-based access control. -
Secure key management. - Off-chain storage. - Minimal sensitive
information on-chain. - Audit logging.

## 15. Complete workflow

``` text
Patient Visit
     ↓
Doctor Creates Record
     ↓
Encrypt Record
     ↓
Secure Off-chain Storage
     ↓
Generate Hash
     ↓
Blockchain Transaction
     ↓
Validation + Consensus
     ↓
Block Added
     ↓
Authorized Nodes Updated
     ↓
Authorized User Retrieves Record
     ↓
Hash Verification
```

## 16. Advantages

-   Data integrity.
-   Secure sharing.
-   Controlled access.
-   Auditability.
-   Tamper detection.
-   Better resilience.
-   Reduced fraud.

## Conclusion

The recommended architecture is **permissioned blockchain + encrypted
off-chain storage + cryptographic hashes + digital signatures +
smart-contract access control**.

**Important line:** Store large/sensitive medical files securely
off-chain; store their hashes, identifiers, permissions and audit
information on-chain.

------------------------------------------------------------------------

# Q9(b). Secure blockchain-based voting system

## 1. Introduction

A blockchain voting system should guarantee voter eligibility,
one-person-one-vote, vote integrity, ballot secrecy, resistance to
tampering and auditability.

Blockchain helps provide a distributed, tamper-evident ledger, but
identity management and ballot privacy require additional cryptographic
and application-level mechanisms.

## 2. Requirements

1.  Only eligible voters can vote.
2.  Each eligible voter can vote only once.
3.  Accepted votes cannot be secretly modified.
4.  Unauthorized vote injection is prevented.
5.  Ballot choices remain confidential where required.
6.  Results can be audited.
7.  Election service remains available.

## 3. Architecture

``` text
                         VOTER
                           |
                           v
                Identity Verification
                           |
                           v
                Authentication Service
                           |
                           v
                   Voting Application
                           |
                           v
              +-------------------------+
              |   SMART CONTRACT LAYER  |
              | Eligibility Check       |
              | One Vote Rule           |
              | Election Time            |
              +------------+------------+
                           |
                           v
                 BLOCKCHAIN NETWORK
              /             |                          v              v              v
           Node 1         Node 2         Node 3
              \             |             /
                       Vote Ledger
                           |
                           v
                    Counting / Result
```

## 4. Registration

Eligible voters are registered before the election and receive a secure
credential or identity.

Personal information should not be unnecessarily exposed on a public
ledger.

## 5. Authentication

``` text
Voter
  ↓
Digital Identity/Credential
  ↓
Authentication
  ↓
Eligibility Check
  ↓
Voting Permission
```

## 6. Vote casting

The voter selects a candidate. Where secrecy is required, the ballot is
protected cryptographically before submission.

``` text
Candidate Choice
      ↓
Cryptographic Protection
      ↓
Vote Transaction
      ↓
Blockchain
```

The design should avoid publicly linking a vote to the voter's identity.

## 7. Smart contract validation

``` text
IF voter eligible
AND voter has not voted
AND election is active
THEN accept vote
ELSE reject vote
```

This enforces the one-vote rule at the application/contract layer.

## 8. Digital signatures

Digital signatures can authenticate authorized voting requests or
credentials.

``` text
Voting Request
      ↓
Digital Signature
      ↓
Public-Key Verification
      ↓
Valid?
```

Invalid signatures are rejected.

## 9. Hashing

``` text
Vote/Transaction Data
       ↓
      Hash
       ↓
Hash Value
```

Changes to recorded transaction data can be detected.

## 10. Consensus

``` text
Vote Transaction
       ↓
Validation
       ↓
Consensus
       ↓
Block
       ↓
Distributed Ledger
```

Multiple authorized nodes reduce dependence on a single central
database.

## 11. Protection against fraud

### One-person-one-vote

The system records whether the voter has already voted.

### Immutability

Accepted transactions are protected against unauthorized alteration by
cryptographic linking and consensus.

### Digital signatures

Invalid or unauthorized transactions can be rejected.

### Distributed ledger

Multiple nodes maintain the ledger.

### Smart contracts

Election rules are executed consistently.

### Auditability

Authorized auditors can verify the recorded election process.

## 12. Protection against unauthorized access

Use: - Strong voter authentication. - Digital signatures. -
Public/private-key cryptography. - Role-based access control. -
Encryption. - Permissioned blockchain. - Secure key management. -
Multi-factor authentication where appropriate.

------------------------------------------------------------------------

# 13. Types of blockchain architecture for voting

## A. Public Blockchain

``` text
Voters/Public
      ↓
Public Blockchain
      ↓
Distributed Nodes
```

### Advantages

-   High transparency.
-   Public verification.
-   Strong decentralization.

### Limitations

-   Privacy challenges.
-   Scalability concerns.
-   Public visibility must be carefully controlled.
-   Performance/transaction costs may be unsuitable for some systems.

------------------------------------------------------------------------

## B. Private Blockchain

``` text
Election Authority
       ↓
Private Blockchain
       ↓
Authorized Nodes
```

### Advantages

-   High control.
-   Better privacy.
-   Faster governance.
-   Controlled participation.

### Limitations

-   More centralized.
-   Greater dependence on the controlling authority.

------------------------------------------------------------------------

## C. Consortium Blockchain

Multiple trusted organizations jointly govern the network.

``` text
Election Authority
       |
Independent Auditors
       |
Authorized Institutions
       |
       v
Consortium Blockchain
     /  |  |     Node Node Node Node
```

### Advantages

-   Shared governance.
-   Better decentralization than one private authority.
-   Controlled access.
-   Suitable for institutional/government scenarios.

### Limitations

-   Requires agreement among members.
-   Governance can become complex.

------------------------------------------------------------------------

## D. Hybrid Blockchain

``` text
PRIVATE SIDE
Sensitive Voter Information
        |
     Hash/Proof
        ↓
PUBLIC SIDE
Public Verification / Audit
```

### Advantages

-   Sensitive data remains private.
-   Selected proofs can be publicly verified.
-   Balances transparency and privacy.

------------------------------------------------------------------------

## 14. Comparison

  -------------------------------------------------------------------------------
  Feature            Public         Private        Consortium      Hybrid
  ------------------ -------------- -------------- --------------- --------------
  Control            Low            High           Shared          Mixed

  Transparency       High           Medium         High            High for
                                                                   selected data

  Privacy            Lower          High           High            High

  Decentralization   High           Low            Medium/High     Medium

  Governance         Open           Single         Multiple        Mixed
                                    authority      authorities     

  Suitable use       Public         Controlled     Institutional   Privacy +
                     verification   elections      elections       public audit
  -------------------------------------------------------------------------------

## 15. Recommended architecture

For many institutional elections, a **permissioned consortium or hybrid
architecture** is attractive because it provides controlled
participation, identity management, privacy, distributed validation and
auditability.

The exact choice depends on legal, privacy and governance requirements.

## 16. Complete workflow

``` text
Voter Registration
       ↓
Identity Verification
       ↓
Secure Credential
       ↓
Voter Authentication
       ↓
Eligibility Check
       ↓
Vote Selection
       ↓
Cryptographic Protection
       ↓
Smart Contract Validation
       ↓
Consensus
       ↓
Block Added
       ↓
Distributed Ledger
       ↓
Auditable Counting
       ↓
Election Result
```

## Conclusion

A secure voting system combines **identity management, cryptography,
smart contracts, consensus, access control and distributed ledger
technology**. Public, private, consortium and hybrid architectures offer
different trade-offs between transparency, privacy, decentralization and
control.

------------------------------------------------------------------------

# MODULE 1 -- THEORY BANK

## 1. Blockchain

Blockchain is a distributed ledger in which transactions are grouped
into blocks and linked using cryptographic hashes.

### Core properties

-   Decentralization.
-   Immutability.
-   Transparency.
-   Security.
-   Traceability.
-   Consensus.
-   Fault tolerance.

------------------------------------------------------------------------

## 2. Cryptographic Hashing

A cryptographic hash function converts input data into a fixed-length
output.

``` text
Input → Hash Function → Fixed-size Hash
```

### Properties

-   Deterministic.
-   Fast to compute.
-   One-way under intended cryptographic assumptions.
-   Small changes produce substantially different outputs.
-   Collision resistance is important.

------------------------------------------------------------------------

## 3. Block Structure

A block commonly contains: - Previous block hash. - Timestamp. - Merkle
Root. - Nonce. - Version/difficulty information depending on the
platform. - Transaction data.

------------------------------------------------------------------------

## 4. Hash Linking

``` text
Block N
   |
Previous Hash
   ↓
Block N+1
   |
Previous Hash
   ↓
Block N+2
```

Changing an old block changes its hash and breaks the expected link to
later blocks, making tampering detectable.

------------------------------------------------------------------------

## 5. Merkle Tree

``` text
Transactions
     ↓
Transaction Hashes
     ↓
Pairwise Hashing
     ↓
Parent Hashes
     ↓
Merkle Root
```

**Purpose:** Efficient transaction integrity verification.

------------------------------------------------------------------------

## 6. Digital Signature

``` text
Message
   ↓
Hash
   ↓
Digest
   ↓
Private Key
   ↓
Digital Signature
```

Receiver verifies using the corresponding public key.

### Provides

-   Authentication.
-   Integrity.
-   Non-repudiation properties.

------------------------------------------------------------------------

## 7. Encryption

### Symmetric

Same secret key for encryption and decryption.

**Example:** AES.

### Asymmetric

Uses a public/private key pair.

**Examples:** RSA, ECC.

------------------------------------------------------------------------

## 8. Consensus

Consensus is the mechanism through which participating blockchain nodes
agree on valid transactions or the ledger state.

Examples: - Proof of Work. - Proof of Stake. - Permissioned consensus
mechanisms.

### Purpose

-   Transaction validation.
-   Agreement among nodes.
-   Prevent conflicting ledger states.

------------------------------------------------------------------------

## 9. Smart Contract

A smart contract is blockchain-based program logic that executes
according to predefined conditions.

``` text
IF payment confirmed
AND delivery confirmed
THEN update ownership
```

Uses: - Supply chain. - Voting. - Payments. - Insurance. - Digital
assets.

------------------------------------------------------------------------

## 10. On-chain vs Off-chain

  On-chain            Off-chain
  ------------------- --------------------------
  Transactions        Large files
  Hashes              Medical images
  Ownership records   Sensor data
  Audit events        Detailed documents
  Metadata            Private application data

Common design:

``` text
Large/Sensitive Data
       ↓
Encrypted Off-chain Storage
       +
Hash / Proof / Metadata
       ↓
Blockchain
```

------------------------------------------------------------------------

# EXAM WRITING METHOD

## For 2 Marks

Write:

1.  Definition.
2.  3--4 key points.
3.  One short concluding line.

## For 16 Marks

Write:

1.  **Introduction** -- 2--4 lines.
2.  **Objectives/Requirements** -- 5--7 points.
3.  **Architecture diagram** -- neat and labelled.
4.  **Components** -- explain each in 2--4 lines.
5.  **Working** -- numbered steps.
6.  **Security mechanisms** -- relevant points.
7.  **Advantages** -- 5--7 points.
8.  **Conclusion** -- 2--3 lines.

## Diagram rule

For scenario questions, always draw at least one clear architecture
diagram.

## Keywords to underline

**Blockchain, Distributed Ledger, Cryptographic Hash, Immutability,
Merkle Tree, Merkle Root, Digital Signature, Public Key, Private Key,
Encryption, Consensus, Smart Contract, Permissioned Blockchain,
Off-chain Storage, Authentication, Integrity, Confidentiality,
Authenticity, Auditability.**

------------------------------------------------------------------------

# LAST-MINUTE PRIORITY

## Very High

1.  Merkle Tree.
2.  Block structure.
3.  Hashing + Avalanche Effect.
4.  Public/Private Key.
5.  Symmetric vs Asymmetric Encryption.
6.  Digital Signature.
7.  Blockchain Architecture.
8.  Smart Contract.
9.  Consensus.
10. Permissioned vs Public Blockchain.

## Scenario Mapping

  Scenario               Main concept
  ---------------------- -------------------------------------------------------
  Digital certificates   Merkle Tree + Hashing
  E-commerce             Encryption + Digital Signature
  Supply chain           Traceability + Smart Contract
  Luxury goods           Digital Identity + Provenance
  Healthcare             Permissioned Blockchain + Off-chain Storage
  Voting                 Authentication + Smart Contract + Privacy + Consensus

## Golden memory rule

**Certificate → Merkle Tree**\
**E-commerce → Encryption + Digital Signature**\
**Supply chain → Traceability + Smart Contract**\
**Luxury goods → Digital Identity + Provenance**\
**Healthcare → Permissioned Blockchain + Off-chain Storage**\
**Voting → Authentication + Privacy + Smart Contract + Consensus**

------------------------------------------------------------------------

# FINAL REMINDER

Do not memorize only the scenario. Memorize the blockchain concept
behind the scenario.

For a detailed answer, **relevant theory + labelled diagram + working +
security + advantages + conclusion** is much stronger than filling pages
with unrelated blockchain terms.
