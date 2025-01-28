---
title: Signature Malleability
id: SCWE-054
alias: signature-malleability
platform: []
profiles: [L1]
mappings:
  scsvs-cg: []
  scsvs-scg: []
  cwe: [345]
status: new
---

## Relationships  
- CWE-345: Insufficient Verification of Data Authenticity  
  [https://cwe.mitre.org/data/definitions/345.html](https://cwe.mitre.org/data/definitions/345.html)  

## Description
Signature malleability refers to the ability to modify a valid signature without changing its validity. This can occur when signatures are not properly verified or when certain components of a signature (like the `v`, `r`, and `s` values) can be altered while still producing a valid signature. Attackers can exploit this vulnerability, leading to potential replay attacks or the ability to manipulate transaction data.

## Remediation
To mitigate signature malleability, ensure that the signature verification process is robust. Use secure cryptographic libraries that properly handle signature validation, such as ECDSA or EdDSA with additional checks to prevent malleability. When verifying signatures, consider using a canonical format for signature components to avoid malleability.

### Vulnerable Contract Example
```solidity
contract MalleableSignatureExample {
    function verifySignature(bytes32 message, uint8 v, bytes32 r, bytes32 s) public pure returns (bool) {
        address signer = ecrecover(message, v, r, s);  // Signature malleability risk
        return signer != address(0);
    }
}
```
### Fixed Contract Example
```solidity
contract SecureSignatureExample {
    function verifySignature(bytes32 message, uint8 v, bytes32 r, bytes32 s) public pure returns (bool) {
        // Ensure canonical signature format to prevent malleability
        require(v == 27 || v == 28, "Invalid v value");
        address signer = ecrecover(message, v, r, s);
        return signer != address(0);
    }
}
```