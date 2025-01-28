---
title: Inadequate Gas Limit Handling
id: SCWE-036
alias: inadequate-gas-limit-handling
platform: []
profiles: [L1]
mappings:
  scsvs-cg: []
  scsvs-scg: []
  cwe: [400]
status: new
---

## Relationships
- CWE-400: Uncontrolled Resource Consumption  
  [CWE-400 Link](https://cwe.mitre.org/data/definitions/400.html)

## Description  
Inadequate gas limit handling refers to the failure to properly manage gas limits in contract operations, which can lead to:
- Failed transactions if gas limits are exceeded.
- Exploitation of vulnerabilities in gas-intensive operations.
- Loss of funds or data.

## Remediation
- **Optimize gas usage:** Minimize gas consumption in contract operations.
- **Avoid unbounded loops:** Ensure loops have a fixed upper limit.
- **Test thoroughly:** Conduct extensive testing to ensure operations stay within gas limits.

## Examples
- **Inadequate Gas Handling**
    ```solidity
    pragma solidity ^0.8.0;

    contract InadequateGas {
        function processArray(uint[] memory data) public {
            for (uint i = 0; i < data.length; i++) {
                // Process each element
            }
        }
    }
    ```

- **Adequate Gas Handling**
    ```solidity
    pragma solidity ^0.8.0;

    contract AdequateGas {
        function processArray(uint[] memory data, uint start, uint end) public {
            require(end <= data.length, "Invalid range");
            for (uint i = start; i < end; i++) {
                // Process each element
            }
        }
    }
    ```

---