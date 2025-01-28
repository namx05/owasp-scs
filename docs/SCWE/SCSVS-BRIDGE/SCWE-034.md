---
title: Insecure Cross-Chain Messaging
id: SCWE-034
alias: insecure-cross-chain-messaging
platform: []
profiles: [L1]
mappings:
  scsvs-cg: [SCSVS-BRIDGE]
  scsvs-scg: [SCSVS-BRIDGE-2]
  cwe: [20]
status: new
---

## Relationships
- CWE-20: Improper Input Validation  
  [CWE-20 Link](https://cwe.mitre.org/data/definitions/20.html)

## Description  
Insecure cross-chain messaging refers to vulnerabilities that arise when communicating between different blockchains. This can lead to:
- Unauthorized actions by malicious actors.
- Loss of funds or data.
- Exploitation of vulnerabilities in cross-chain logic.

## Remediation
- **Validate messages:** Ensure all cross-chain messages are properly validated.
- **Use secure protocols:** Leverage secure cross-chain communication protocols.
- **Test thoroughly:** Conduct extensive testing to ensure cross-chain logic is secure.

## Examples
- **Insecure Cross-Chain Messaging**
    ```solidity
    pragma solidity ^0.8.0;

    contract InsecureCrossChain {
        function processMessage(bytes memory message) public {
            // Process message without validation
        }
    }
    ```

- **Secure Cross-Chain Messaging**
    ```solidity
    pragma solidity ^0.8.0;

    contract SecureCrossChain {
        function processMessage(bytes memory message, bytes memory signature) public {
            bytes32 messageHash = keccak256(message);
            address signer = ecrecover(messageHash, signature);
            require(signer == msg.sender, "Invalid signature");
            // Process message
        }
    }
    ```

---