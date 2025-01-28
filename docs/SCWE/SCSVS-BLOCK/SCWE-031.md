---
title: Insecure Block Timestamp Usage
id: SCWE-031
alias: insecure-block-timestamp-usage
platform: []
profiles: [L1]
mappings:
  scsvs-cg: [SCSVS-BLOCK]
  scsvs-scg: [SCSVS-BLOCK-2]
  cwe: [682]
status: new
---

## Relationships
- **CWE-682: Incorrect Calculation**  
  [https://cwe.mitre.org/data/definitions/682.html](https://cwe.mitre.org/data/definitions/682.html)

## Description
In blockchain networks like Ethereum, block timestamps are provided by miners, and they can be manipulated to some extent within a predefined window. This flexibility can lead to unintended behaviors in contracts that rely on these timestamps for time-dependent logic, such as deadlines or restrictions on actions.

Block timestamps are not guaranteed to be accurate or consistent, and miners can influence them within a certain range. This can cause issues when contracts depend on precise timing for critical functionality, such as token distribution, access control, or other time-sensitive events.

Potential issues that arise from insecure timestamp usage include:

- **Manipulated deadlines**: Timestamps used to enforce deadlines may be adjusted, allowing users or miners to bypass critical contract conditions.
- **Unpredictable contract behavior**: If the contract logic is tied to a specific block timestamp, manipulation of these values could lead to unexpected outcomes.
- **Exploitable vulnerabilities**: Attackers or miners could manipulate timestamps to trigger or avoid certain contract actions, leading to financial or security vulnerabilities.

## Remediation
- **Avoid timestamp-based conditions**: Where possible, use block numbers instead of timestamps. Block numbers are more reliable and less subject to manipulation.
- **Use Oracles**: For time-sensitive contracts, consider using trusted oracles to provide external time data.

## Examples

### Insecure Block Timestamp Usage

```solidity
pragma solidity ^0.4.0;

contract TimestampExample {
    uint public deadline;

    function setDeadline(uint _deadline) public {
        deadline = _deadline;
    }

    function checkDeadline() public view returns (string) {
        if (now > deadline) {
            return "Deadline passed";
        } else {
            return "Deadline not passed";
        }
    }
}
```

In the above example, the `now` keyword retrieves the block's timestamp to compare with the deadline. This creates a potential vulnerability as miners can manipulate the block timestamp within a predefined window.

### Fixed Block Timestamp Usage
```solidity
pragma solidity ^0.4.0;

contract SafeTimestampExample {
    uint public deadline;
    uint public blockNumber;

    function setDeadline(uint _deadline) public {
        deadline = _deadline;
        blockNumber = block.number;
    }

    function checkDeadline() public view returns (string) {
        if (block.number > blockNumber + 1000) { // Assuming a reasonable number of blocks for a deadline
            return "Deadline passed";
        } else {
            return "Deadline not passed";
        }
    }
}
```
In this fixed version, the contract uses `block.number` instead of `now`. This makes the contract less susceptible to timestamp manipulation, as block numbers are more reliable and consistent.

