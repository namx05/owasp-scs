---
title: Insecure Use of Randomness
id: SCWE-041
alias: insecure-use-of-randomness
platform: []
profiles: [L1]
mappings:
  scsvs-cg: [SCSVS-ORACLE]
  scsvs-scg: [SCSVS-ORACLE-1]
  cwe: [336]
status: new
---

## Relationships
- CWE-336: Predictable Random Number Generator  
  [CWE-336 Link](https://cwe.mitre.org/data/definitions/336.html)

## Description  
Insecure use of randomness refers to vulnerabilities that arise when weak or predictable sources of randomness are used in smart contracts. This can lead to:
- Exploitation of the contract’s logic by malicious actors.
- Loss of funds or data.
- Reduced trust in the contract’s security.

## Remediation
- **Use secure randomness:** Leverage secure randomness sources like Chainlink VRF.
- **Avoid block variables:** Do not rely on block timestamps or hashes for randomness.
- **Test thoroughly:** Conduct extensive testing to ensure randomness is secure.

## Examples
- **Insecure Randomness**
    ```solidity
    pragma solidity ^0.8.0;

    contract InsecureRandomness {
        function generateRandomNumber() public view returns (uint) {
            return uint(keccak256(abi.encodePacked(block.timestamp, block.difficulty))); // Insecure randomness
        }
    }
    ```

- **Secure Randomness**
    ```solidity
    pragma solidity ^0.8.0;

    import "@chainlink/contracts/src/v0.8/VRFConsumerBase.sol";

    contract SecureRandomness is VRFConsumerBase {
        bytes32 internal keyHash;
        uint256 internal fee;
        uint256 public randomResult;

        constructor(address vrfCoordinator, address linkToken, bytes32 _keyHash, uint256 _fee)
            VRFConsumerBase(vrfCoordinator, linkToken) {
            keyHash = _keyHash;
            fee = _fee;
        }

        function getRandomNumber() public returns (bytes32 requestId) {
            require(LINK.balanceOf(address(this)) >= fee, "Not enough LINK");
            return requestRandomness(keyHash, fee);
        }

        function fulfillRandomness(bytes32 requestId, uint256 randomness) internal override {
            randomResult = randomness;
        }
    }
    ```

---



