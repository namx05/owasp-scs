---
title: Lack of Decentralized Oracle Sources
id: SCWE-029
alias: lack-of-decentralized-oracle-sources
platform: []
profiles: [L1]
mappings:
  scsvs-cg: [SCSVS-BRIDGE]
  scsvs-scg: [SCSVS-BRIDGE-1]
  cwe: [20]
status: new
---

## Relationships
- CWE-20: Improper Input Validation  
  [CWE-20 Link](https://cwe.mitre.org/data/definitions/20.html)

## Description  
Lack of decentralized oracle sources refers to the reliance on a single oracle for critical data, which can be manipulated or compromised. This can lead to:
- Unauthorized actions by malicious actors.
- Loss of funds or data.
- Exploitation of the contract's logic.

## Remediation
- **Use multiple oracles:** Leverage multiple decentralized oracles for critical data.
- **Validate inputs:** Ensure all oracle data is properly validated before use.
- **Implement fallback mechanisms:** Use fallback oracles in case of failure.

## Examples
- **Single Oracle Source**
    ```solidity
    pragma solidity ^0.8.0;

    contract SingleOracle {
        function getPrice(address oracle) public view returns (uint) {
            return Oracle(oracle).getPrice(); // Single oracle
        }
    }
    ```

- **Decentralized Oracle Sources**
    ```solidity
    pragma solidity ^0.8.0;

    contract DecentralizedOracles {
        function getPrice(address[] memory oracles) public view returns (uint) {
            uint totalPrice = 0;
            for (uint i = 0; i < oracles.length; i++) {
                totalPrice += Oracle(oracles[i]).getPrice();
            }
            return totalPrice / oracles.length; // Average price from multiple oracles
        }
    }
    ```

---