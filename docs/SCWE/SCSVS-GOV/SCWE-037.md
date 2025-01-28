---
title: Insufficient Protection Against Front-Running
id: SCWE-037
alias: insufficient-protection-against-front-running
platform: []
profiles: [L1]
mappings:
  scsvs-cg: [SCSVS-GOV]
  scsvs-scg: [SCSVS-GOV-3]
  cwe: [20]
status: new
---

## Relationships
- CWE-20: Improper Input Validation  
  [CWE-20 Link](https://cwe.mitre.org/data/definitions/20.html)

## Description  
Insufficient protection against front-running refers to vulnerabilities that allow malicious actors to exploit the order of transactions for profit. This can lead to:
- Unauthorized actions by malicious actors.
- Loss of funds or data.
- Exploitation of the contract’s logic.

## Remediation
- **Use commit-reveal schemes:** Implement commit-reveal mechanisms to hide transaction details until they are finalized.
- **Add delays:** Introduce time delays for critical operations to reduce the risk of front-running.
- **Test thoroughly:** Conduct extensive testing to ensure front-running protection is effective.

## Examples
- **Vulnerable to Front-Running**
    ```solidity
    pragma solidity ^0.8.0;

    contract FrontRunningVulnerable {
        function buyTokens(uint amount) public {
            // Buy tokens without front-running protection
        }
    }
    ```

- **Protected Against Front-Running**
    ```solidity
    pragma solidity ^0.8.0;

    contract FrontRunningProtected {
        mapping(address => bytes32) public commitments;

        function commit(bytes32 hash) public {
            commitments[msg.sender] = hash;
        }

        function reveal(uint amount, bytes32 secret) public {
            require(commitments[msg.sender] == keccak256(abi.encodePacked(amount, secret)), "Invalid commitment");
            // Buy tokens
        }
    }
    ```

---