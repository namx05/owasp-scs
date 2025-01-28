---
title: Insecure Use of External Calls
id: SCWE-042
alias: insecure-use-of-external-calls
platform: []
profiles: [L1]
mappings:
  scsvs-cg: []
  scsvs-scg: []
  cwe: [829]
status: new
---

## Relationships
- CWE-829: Inclusion of Functionality from Untrusted Control Sphere  
  [CWE-829 Link](https://cwe.mitre.org/data/definitions/829.html)

## Description  
Insecure use of external calls refers to vulnerabilities that arise when calling external contracts without proper validation or safeguards. This can lead to:
- Unauthorized actions by malicious actors.
- Loss of funds or data.
- Exploitation of vulnerabilities in the called contract.

## Remediation
- **Validate targets:** Ensure the target contract is trusted and secure.
- **Use secure libraries:** Leverage well-audited libraries for external calls.
- **Test thoroughly:** Conduct extensive testing to ensure external calls are secure.

## Examples
- **Insecure External Call**
    ```solidity
    pragma solidity ^0.8.0;

    contract InsecureExternalCall {
        function callExternal(address target, bytes memory data) public {
            (bool success, ) = target.call(data); // No validation
            require(success, "Call failed");
        }
    }
    ```

- **Secure External Call**
    ```solidity
    pragma solidity ^0.8.0;

    contract SecureExternalCall {
        address public trustedTarget;

        constructor(address _trustedTarget) {
            trustedTarget = _trustedTarget;
        }

        function callExternal(bytes memory data) public {
            (bool success, ) = trustedTarget.call(data); // Restricted to trusted target
            require(success, "Call failed");
        }
    }
    ```

---
