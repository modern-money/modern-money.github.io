# Scalability

## Scalability Targets
- PayPal: [200 Million Accounts](https://www.statista.com/statistics/218493/paypals-total-active-registered-accounts-from-2010/) and [240  transactions/second](https://www.statista.com/statistics/419778/paypal-annual-payments)
- Bitcoin: [1 Million Addresses](https://blockchain.info/charts/n-unique-addresses) and [7 transactions/second](https://blockchain.info/charts/n-transactions?timespan=all)

We need to increase Bitcoin's current capacity by a factor of about 40 to scale to PayPal's throughput.

## Core Problem
The core problem is the quadratic scaling of messages in the network. On-chain payments must be verified and stored by
every node in the network, meaning that the node with the least resources
limits the overall throughput of the system as a whole. 

- Bitcoin's maximum network throughput is `1 MB / 10 min = 1.66 KB / s`.
- Average transaction size is [745 kb/block](https://blockchain.info/charts/avg-block-size) / [1400 TX/block](https://blockchain.info/charts/n-transactions-per-block) = [532 bytes](https://charts.bitcoin.com/chart/transaction-size)
- [Bitcoin's Weaknesses](https://en.bitcoin.it/wiki/Weaknesses)
- [Bitcoin's P2P Network: The Soft Underbelly of Bitcoin](https://www.youtube.com/watch?time_continue=37&v=Y6kibPzbrIc)
- [On Scaling Decentralized Blockchains](https://www.tik.ee.ethz.ch/file/74bc987e6ab4a8478c04950616612f69/main.pdf)
- [Staled and Orphaned Blocks](https://bitcoin.org/en/glossary/stale-block)
 - [Number of Orphaned Blocks](https://blockchain.info/charts/n-orphaned-blocks?timespan=all)


## Solutions
There are multiple proposed solutions and research efforts:

### On-Chain Solutions
- Faster or larger blocks
  - [Block size following technological growth (Pieter Wuille)](https://github.com/bitcoin/bips/blob/master/bip-0103.mediawiki)
  - [On the Security and Performance of Proof of Work
Blockchains ( Arthur Gervais )](https://eprint.iacr.org/2016/555.pdf)
    - [On the Security and Performance of Proof of Work
  Blockchains [ Talk ]](https://www.youtube.com/watch?time_continue=8857&v=_Z0ID-0DOnc)
  - [Segregated Witness](https://en.bitcoin.it/wiki/Segregated_Witness)
    - [Segregated witness and its impact on scalability (Pieter Wuille)](https://www.youtube.com/watch?v=NOYNZB5BCHM)
- Smaller transactions
  - [Schnorr Signatures](https://en.wikipedia.org/wiki/Schnorr_signature)
      - [BIP Schnorr](https://github.com/sipa/bips/blob/bip-schnorr/bip-schnorr.mediawiki)
  - Signature Aggregation
      - [Simple Schnorr Multi-Signatures with Applications to Bitcoin](https://eprint.iacr.org/2018/068.pdf)
      - [Per-block non-interactive Schnorr signature	aggregation](https://lists.linuxfoundation.org/pipermail/bitcoin-dev/2017-May/014272.html)
      - [Sequential Aggregate Signatures from Trapdoor Permutations](https://hovav.net/ucsd/dist/rsaagg.pdf)
  - [BLS Signatures](https://eprint.iacr.org/2018/483.pdf)
      - [BLS Signatures at Scaling Bitcoin](https://www.youtube.com/watch?v=LDF8bOEqXt4&feature=youtu.be&t=3h4m31s)
  - [Coalescing Transaction](https://github.com/bitcoin/bips/blob/master/bip-0131.mediawiki)
- Faster Block Propagation
  - [Compact Blocks](https://bitcoincore.org/en/2016/06/07/compact-blocks-faq/)
  - [Compact Block Relay (Matt Corallo)](https://github.com/bitcoin/bips/blob/master/bip-0152.mediawiki)
  - [O(1) Block Propagation (Gavin Andresen)](https://gist.github.com/gavinandresen/e20c3b5a1d4b97f79ac2) 
- Sharding
  - [Sidechains](https://www.blockstream.com/sidechains.pdf)
  - [Ethereum 2.0](https://youtu.be/9RtSod8EXn4?t=3h11m45s)
 - Thin Verification
   - [Merkle tree of open transactions for lite mode](https://bitcointalk.org/index.php?topic=21995.0)
   - [Merkle tree of unspent transactions (MTUT), for serverless thin clients and self-verifiable prunned blockchain](https://en.bitcoin.it/wiki/User:DiThi/MTUT)
   - [Ultimate blockchain compression with trust-free lite nodes](https://bitcointalk.org/index.php?topic=88208.0)
   - [Progress on Scaling via Client-Side Validation ( Peter Todd )](https://www.youtube.com/watch?time_continue=6204&v=uO-1rQbdZuk)

### Off-Chain Solutions
- Hashed Timelocked Contracts HTLC / Lightning Network
  - [The Bitcoin Lightning Network:
Scalable Off-Chain Instant Payments ( Joseph Poon, Thaddeus Dryja )](https://lightning.network/lightning-network-paper.pdf)
  - [Scalable Funding of Bitcoin Micropayment (Blockstream et al)](https://www.tik.ee.ethz.ch/file/a20a865ce40d40c8f942cf206a7cba96/Scalable_Funding_Of_Blockchain_Micropayment_Networks.pdf)
  - Eltoo ( Blockstream et al )
    - [Eltoo: A Simple Layer2 Protocol for Bitcoin](https://blockstream.com/eltoo.pdf)
    - [Eltoo: next lightning](https://blockstream.com/2018/04/30/eltoo-next-lightning.html)
- Plasma
  - [Plasma: Scalable Autonomous Smart Contracts ( Joseph Poon, Vitalik Buterin )](https://plasma.io/plasma.pdf)
  - [Scaling Ethereum with Plasma ( Joseph Poon )](https://www.youtube.com/watch?v=plf-kG8jt9c)
  - [Plasma & The Public Ethereum Chain ( Joseph Poon ) ](https://www.youtube.com/watch?v=oOQmnhQrq_U)
  - [Plasma for Bitcoin ( Joseph Poon )](https://www.youtube.com/watch?time_continue=8286&v=QkYXPJMqBNk)
- Zero-knowledge proofs
  - [zk-SNARKs](https://eprint.iacr.org/2013/879.pdf)
  - [zk-STARKs](https://eprint.iacr.org/2018/046.pdf)
  - More Schnorr Magic
    - Script-less scripts
      - [Mimblewimble and Scriptless Scripts ( Andrew Poelstra )](https://www.youtube.com/watch?v=ovCBT1gyk9c)
      - [Using the Chain for what Chains are Good For ( Andrew Poelstra )
    ](https://www.youtube.com/watch?time_continue=5756&v=3pd6xHjLbhs)
    - Discrete Log Contracts
      - [Discreet Log Contracts ( Thaddeus Dryja )](https://www.youtube.com/watch?time_continue=7045&v=LDF8bOEqXt4)
      - [Discreet Log Contracts: Privacy-preserving smart contracts on Bitcoin ( Thaddeus Dryja )](https://www.youtube.com/watch?v=Vpr3vKeByfM)
    - [Bullet Proofs](https://cryptopapers.info/assets/pdf/bulletproofs.pdf)

### Network Layer
- [Peer-to-Peer Communication Across Network Address Translators](http://www.brynosaurus.com/pub/net/p2pnat/)
- [A New Method for Symmetric NAT Traversal in UDP and TCP](http://www.goto.info.waseda.ac.jp/~wei/file/wei-apan-v10.pdf)
- [DHT-based NAT Traversal](http://docs.maidsafe.net/Whitepapers/pdf/DHTbasedNATTraversal.pdf)
