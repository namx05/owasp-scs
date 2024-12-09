---
id: SCSTG-TEST-0001
scsvs_cg_id:
- SCSVS-AUTH
scsvs_scg_id:
- SCSVS-AUTH-1
platform: android
title: Multi-Signature Schemes
scsvs_cg_levels:
- L2
tests: SCSTG-TEST-0001 
---

Ensure that the visibility modifier for all functions is appropriate, preventing unnecessary exposure of internal functions.

 - If a function is only meant to be used internally, it should be marked as internal or private. This ensures it cannot be called externally or by other contracts.

```solidity
function internalFunction() internal { ... }  // internal function, only accessible within the contract
function privateFunction() private { ... }	// private function, not even accessible by derived contracts
```