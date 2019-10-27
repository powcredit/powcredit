# PoW Credit

Proof of Work Credit aims to solve the creditiblity problem in decentralized world.

## Problem

DeFi apps that can lend some crypto assets to a borrower, face the problem that the cost of creating an address is very cheap. So the only solution is to require a borrower address depsoit collaterals with market value much greater than value of crypto assets to borrow. Otherwise, a borrower can repeatly creating new addresses to more and more crypto assets, opening an unlimited leverage.

This problem is similiar to the sybil attack in Bitcoin and other blockchains when making consensus. The collaterals solution is similiar to Proof of Stake (PoS) consensus. In contrast, we propose the Proof of Work solution to creating credit for a borrower. Therefore, the borrowers can use their credibilities to borrower more crypto assets than they own.

## Solution 1: Static PoW Address

In most blockchains, an address is often calculated from the public key with multiple runs of hashing. Similar to PoW in Bitcoin, we can define a valid static PoW address following a pre-defined and static prefix, with the length of prefix as the difficulty.

Take Ethereum as an example, we define a static PoW address with number of leading 0s as difficulty, i.e.,
- PoW address with difficulty 4: 0x00005ED00f891Aaf0Ff3F30D3a3C6E4B5DbBfb3B
- PoW address with difficulty 3: 0x000fc8B6b7EE3f3342943935391EA48BAB50512A
- Invalid PoW address: 0x12Dd7832f353475cc5FeC667EFa90C1462dcBAb0

The number of leading 0s indicates the computing resources required to generate this address, and only assocaited to this address (unlike collaterals which can be transferred after unlocked).

A DeFi app can use the difficulty to control the number of new borrowers in certain period of time. For example,
1. Every 24 hours of blocks, it can lend crypto assets to 10 new borrowers that haven't borrowered anything before.
2. After 2 weeks, if the average creation time of 10 new borrowers per period is less/higher than certain threshold, the difficulty for next 2 weeks are adjusted accordingly, to make that on average, 10 new borrowers per 24 hours of blocks.

## Solution 2: Chained PoW Address

In above solution, the prefix is pre-defined and static, in which some attackers may pre-generate bunch of addresses meeting certain difficulty requirement. So following Bitcoin's idea, we define a valid chained PoW address during a given N-th period of time, meeting the following requirements:
- Only certain number of valid chained PoW addresses can be saved in the N-th period
- Given a hashing algorithm of the valid chained PoW address in N-th period and all valid chained PoW addresses saved in (N-1)-th period, the hashing result following a given prefix with length as difficulty

Also take Ethereum as an example:
1. We denote a period of time as a credit block covering 24 hours of Ethereum blocks.
2. In any credit block, only 10 new borrowers can join the network to borrower crypto assets with less collaterals.
3. A credit block consists of credit block time, and the list of 10 new borrowers during the period.
4. The hashing algorithm is sha256(sha256(sha256(sha256(credit block N-1)) + new address X)
5. The difficulty is defined as the number of leading 0s of the hashing result.

In this case, no attacker may be able to pre-generate new borrower addresses in a new credit block.

## Economics model

TBD

## PoW Credit Protocol

Although every DeFi app can create its own rule of static or chained PoW addresses, and saving all new borrower addresses of its own. It is more meaningful to create a protocol to keep and share PoW borrower addresses, used by all DeFi apps. Therefore, the DeFi apps can calculate credit or risk of a given PoW address accross each other DeFi apps.

The protocol is something this project is going to implement.
