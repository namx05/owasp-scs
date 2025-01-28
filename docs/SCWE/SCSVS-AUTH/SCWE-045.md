---
title: Insecure Use of Modifiers
id: SCWE-045
alias: insecure-use-of-modifiers
platform: []
profiles: [L1]
mappings:
  scsvs-cg: []
  scsvs-scg: []
  cwe: [732]
status: new
---

## Relationships
- CWE-732: Incorrect Permission Assignment for Critical Resource  
  [CWE-732 Link](https://cwe.mitre.org/data/definitions/732.html)

## Description  
Insecure use of modifiers refers to vulnerabilities that arise when modifiers are used improperly. This can lead to:
- Unauthorized actions by malicious actors.
- Loss of funds or data.
- Exploitation of vulnerabilities in contract logic.

## Remediation
- **Restrict access:** Ensure only authorized addresses can use the modifier.
- **Validate inputs:** Ensure all inputs to the modifier are properly validated.
- **Test thoroughly:** Conduct extensive testing to ensure modifiers are secure.

## Examples
- **Insecure Modifier Usage**
    ```solidity
    pragma solidity ^0.8.0;

    contract InsecureModifier {
        modifier onlyAdmin() {
            require(msg.sender == address(0), "Unauthorized"); // Insecure condition
            _;
        }

        function updateBalance(uint newBalance) public onlyAdmin {
            // Update balance
        }
    }
    ```

- **Secure Modifier Usage**
    ```solidity
    pragma solidity ^0.8.0;

    contract SecureModifier {
        address public admin;

        constructor(address _admin) {
            admin = _admin;
        }

        modifier onlyAdmin() {
            require(msg.sender == admin, "Unauthorized"); // Secure condition
            _;
        }

        function updateBalance(uint newBalance) public onlyAdmin {
            // Update balance
        }
    }
    ```