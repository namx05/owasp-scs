---
title: Insecure Use of Fallback Functions
id: SCWE-043
alias: insecure-use-of-fallback-functions
platform: []
profiles: [L1]
mappings:
  scsvs-cg: []
  scsvs-scg: []
  cwe: [250]
status: new
---

## Relationships
- CWE-250: Execution with Unnecessary Privileges  
  [CWE-250 Link](https://cwe.mitre.org/data/definitions/250.html)

## Description  
Insecure use of fallback functions refers to vulnerabilities that arise when the fallback function is used improperly. This can lead to:
- Unauthorized actions by malicious actors.
- Loss of funds or data.
- Exploitation of vulnerabilities in contract logic.

## Remediation
- **Restrict access:** Ensure only authorized addresses can trigger the fallback function.
- **Validate inputs:** Ensure all inputs to the fallback function are properly validated.
- **Test thoroughly:** Conduct extensive testing to ensure the fallback function is secure.

## Examples
- **Insecure Fallback Function**
    ```solidity
    pragma solidity ^0.8.0;

    contract InsecureFallback {
        fallback() external {
            // No access control
        }
    }
    ```

- **Secure Fallback Function**
    ```solidity
    pragma solidity ^0.8.0;

    contract SecureFallback {
        address public admin;

        constructor(address _admin) {
            admin = _admin;
        }

        modifier onlyAdmin() {
            require(msg.sender == admin, "Unauthorized");
            _;
        }

        fallback() external onlyAdmin {
            // Restricted to admin
        }
    }
    ```

---