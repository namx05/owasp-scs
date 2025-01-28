---
title: Oracle Price Manipulation
id: SCWE-028
alias: oracle-price-manipulation
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
Oracle price manipulation refers to the exploitation of vulnerabilities in price oracles to manipulate contract logic. This can lead to:
- Unauthorized actions by malicious actors.
- Loss of funds or data.
- Exploitation of the contract's logic.

## Remediation
- **Use decentralized oracles:** Leverage multiple decentralized oracles for price data.
- **Validate inputs:** Ensure all oracle data is properly validated before use.
- **Implement circuit breakers:** Add mechanisms to halt operations in case of suspicious activity.

## Examples
- **Vulnerable to Oracle Manipulation**
    ```solidity
    pragma solidity ^0.8.0;

    contract VulnerableOracle {
        function getPrice(address oracle) public view returns (uint) {
            return Oracle(oracle).getPrice(); // No validation
        }
    }
    ```

- **Protected Against Oracle Manipulation**
    ```solidity
    pragma solidity ^0.8.0;

    contract ProtectedOracle {
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