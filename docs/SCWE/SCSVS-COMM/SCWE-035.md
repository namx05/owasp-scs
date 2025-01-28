---
title: Insecure Delegatecall Usage
id: SCWE-035
alias: insecure-delegatecall-usage
platform: []
profiles: [L1]
mappings:
  scsvs-cg: [SCSVS-COMM]
  scsvs-scg: [SCSVS-COMM-1]
  cwe: [250]
status: new
---

## Relationships
- CWE-250: Execution with Unnecessary Privileges  
  [CWE-250 Link](https://cwe.mitre.org/data/definitions/250.html)

## Description  
Insecure delegatecall usage refers to vulnerabilities that arise when using `delegatecall` to execute code from another contract. This can lead to:
- Unauthorized access to sensitive functions.
- Exploitation of vulnerabilities in the called contract.
- Loss of funds or data.

## Remediation
- **Validate targets:** Ensure the target contract is trusted and secure.
- **Restrict permissions:** Restrict `delegatecall` usage to trusted addresses.
- **Test thoroughly:** Conduct extensive testing to ensure `delegatecall` is used securely.

## Examples
- **Insecure Delegatecall Usage**
    ```solidity
    pragma solidity ^0.8.0;

    contract InsecureDelegatecall {
        function executeDelegatecall(address target, bytes memory data) public {
            (bool success, ) = target.delegatecall(data); // No validation
            require(success, "Delegatecall failed");
        }
    }
    ```

- **Secure Delegatecall Usage**
    ```solidity
    pragma solidity ^0.8.0;

    contract SecureDelegatecall {
        address public trustedTarget;

        constructor(address _trustedTarget) {
            trustedTarget = _trustedTarget;
        }

        function executeDelegatecall(bytes memory data) public {
            (bool success, ) = trustedTarget.delegatecall(data); // Restricted to trusted target
            require(success, "Delegatecall failed");
        }
    }
    ```