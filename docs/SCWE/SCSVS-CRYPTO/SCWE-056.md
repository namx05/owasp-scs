---
title: Lack of Proper Signature Verification
id: SCWE-056
alias: lack-proper-signature-verification
platform: []
profiles: [L1]
mappings:
  scsvs-cg: [SCSVS-CRYPTO]
  scsvs-scg: [SCSVS-CRYPTO-1]
  cwe: [345]
status: new
---

## Relationships  
- CWE-345: Insufficient Verification of Data Authenticity  
  [https://cwe.mitre.org/data/definitions/345.html](https://cwe.mitre.org/data/definitions/345.html)  

## Description
Failure to properly verify the authenticity of a signature can lead to unauthorized access or malicious actions. In smart contracts, signatures are often used for authentication, and insufficient verification may allow an attacker to bypass authentication checks. This can result in unauthorized transactions, contract state manipulation, or other unintended behaviors.

## Remediation
To mitigate this vulnerability, always implement proper signature verification using secure cryptographic methods. Use the `ecrecover` function to recover the signer’s address and ensure that the recovered address matches the expected address. Additionally, verify that the signature is valid for the intended message or transaction and that the signer is authorized to perform the action.

### Vulnerable Contract Example
```solidity
contract SignatureVerificationExample {
    function authenticate(bytes32 message, uint8 v, bytes32 r, bytes32 s) public view returns (address) {
        address signer = ecrecover(message, v, r, s);
        return signer;  // No further validation of the signer or message
    }
}
```

### Fixed Contract Example
```solidity
contract SecureSignatureVerificationExample {
    address public authorizedSigner;

    constructor(address _authorizedSigner) {
        authorizedSigner = _authorizedSigner;
    }

    function authenticate(bytes32 message, uint8 v, bytes32 r, bytes32 s) public view returns (bool) {
        address signer = ecrecover(message, v, r, s);
        require(signer == authorizedSigner, "Invalid signer");  // Proper validation of the signer
        return true;
    }
}
```