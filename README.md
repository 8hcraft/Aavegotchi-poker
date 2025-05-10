# Aavegotchi Hold'em: Official Trait-Based Poker Suite
*"A Poker Ecosystem for NFT Utility & DAO Revenue"*

## Table of Contents
1. **Core Game Rules**  
2. **Trait Effects Matrix**  
3. **Detailed Gameplay Scenarios**  
4. **Revenue & Tokenomics Model**  
5. **Smart Contract Architecture**  
6. **Balance Spreadsheet (Embedded)**  
7. **Investor Pitch Deck Slides**  

---

## 1. Core Game Rules (Texas Hold'em Variant)

### Base Rules:
| Component          | Specification              |
|--------------------|---------------------------|
| Players            | 2-8 Gotchis per table     |
| Blinds             | 10/20 GHST (scalable)     |
| Rounds             | Pre-flop → River          |
| DAO Cut            | 5% of all pots            |

### Gotchi Modifiers:
- Each trait activates **once per game**  
- Effects trigger **after community cards**  
- Wearables can **enhance trait powers**  

---

## 2. Trait Effects Matrix (Updated)

| Trait Range  | Poker Effect               | Strategic Value | Counterplay |
|--------------|---------------------------|-----------------|-------------|
| **Energy ≤20** | Upgrade card rank (7→8) | High            | Bluff heavy |
| **Spookiness ≥80** | Peek at hole card | Info advantage | Misdirect   |
| **Brain ≥90** | Swap community card  | Game-changing   | Predict swaps |

*See Appendix A for full 28-trait combos*

---

## 3. Detailed Gameplay Scenarios

### Scenario 1: The Brain Bluff
**Players:**
- *Gotchi A*: Brain=95, Energy=15  
- *Gotchi B*: Aggression=88  

**Action:**
1. *Flop*: 5♦, J♣, 2♥  
   - Gotchi A uses **Energy 15** → 2♥ → 3♥  
2. *Turn*: Q♠  
   - Gotchi B forces call via **Aggression 88**  
3. *River*: 10♣  
   - Gotchi A **swaps 10♣ for K♦** (Brain 95)  

**Outcome**: Gotchi A wins with K♦ high  

---

## 4. Revenue Model (Dual-Token)

### Income Streams:
| Source          | Est. Monthly (10k players) |
|-----------------|---------------------------|
| Pot Rake (5%)   | 50,000 GHST               |
| Wearable Sales  | 20,000 GHST               |
| Tournaments     | 30,000 GHST               |

### Token Utility:
- **GHST**: Buy-ins, rake, wearables  
- **FRENS**: Free tournament entries  

---

## 5. Smart Contract Architecture

### Key Functions:
```solidity
// Upgrade Card Rank
function upgradeCard(uint256 gotchiId, uint8 cardPos) external {
    require(traits[gotchiId].energy <= 20, "Low energy only");
    communityCards[cardPos] = min(communityCards[cardPos] + 1, 14); 
}

// Swap Community Card
function swapCard(uint256 gotchiId) external {
    require(traits[gotchiId].brain >= 90, "Brain 90+ required");
    communityCards[riverPos] = drawNewCard();
}
