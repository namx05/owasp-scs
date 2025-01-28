---
title: Insecure Use of Inline Assembly
id: SCWE-039
alias: insecure-use-of-inline-assembly
platform: []
profiles: [L1]
mappings:
  scsvs-cg: []
  scsvs-scg: []
  cwe: [704]
status: new
---

## Relationships
- CWE-704: Incorrect Type Conversion or Cast  
  [CWE-704 Link](https://cwe.mitre.org/data/definitions/704.html)

## Description  
Insecure use of inline assembly refers to vulnerabilities that arise when low-level assembly code is used improperly. This can lead to:
- Incorrect type conversions or casts.
- Exploitation of vulnerabilities in low-level operations.
- Loss of funds or data.

## Remediation
- **Avoid inline assembly:** Use high-level Solidity code whenever possible.
- **Validate inputs:** Ensure all inputs to assembly code are properly validated.
- **Test thoroughly:** Conduct extensive testing to ensure assembly code is secure.

## Examples
- **Insecure Inline Assembly**
    ```solidity
    pragma solidity ^0.8.0;

    contract InsecureAssembly {
        function add(uint a, uint b) public pure returns (uint) {
            uint result;
            assembly {
                result := add(a, b)
            }
            return result;
        }
    }
    ```

- **Secure High-Level Code**
    ```solidity
    pragma solidity ^0.8.0;

    contract SecureHighLevel {
        function add(uint a, uint b) public pure returns (uint) {
            return a + b; // High-level code
        }
    }
    ```

---