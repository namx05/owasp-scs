---
hide:
  - toc
search:
  exclude: true
---

# OWASP Smart Contract Top 10

<img src="../assets/sctop10.png" 
     align="right" 
     style="border-radius: 3px; margin-left: 5em; box-shadow: rgba(149, 157, 165, 0.2) 0px 8px 24px;" 
     width="550px" 
     height="400px">


The **OWASP Smart Contract Top 10** is a standard awareness document that aims to provide Web3 developers and security teams with insights into the top 10 vulnerabilities found in smart contracts.

- **Awareness**: Understand the most common and critical vulnerabilities affecting smart contracts.
- **Prevention**: Implement best practices to safeguard against these known issues.
- **Standard Compliance**: A reference to ensure secure development and assessment of smart contracts.
- **Security Audits**: Use as a checklist for penetration testing and securing smart contracts.

<br>

<button class="scs-button" onclick="window.location.href='https://owasp.org/www-project-smart-contract-top-10/';"> Visit the Smart Contract Top 10</button>

<br>

| **ID**  | **Title**                           | **Description**                                                                                                                                                                                                                                  |
|---------|-------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| SC01    | Reentrancy Attacks                 | A reentrancy attack exploits the vulnerability in smart contracts when a function makes an external call to another contract before updating its own state. This allows the external contract, possibly malicious, to reenter the original function and repeat certain actions, like withdrawals, using the same state. Through such attacks, an attacker can possibly drain all the funds from a contract. |
| SC02    | Integer Overflow and Underflow     | The Ethereum Virtual Machine (EVM) defines fixed-size data types for integers, which limits the range of values they can represent. Overflow occurs when an arithmetic operation exceeds the maximum value a data type can hold, while underflow happens when an operation goes below the minimum value. For unsigned integers, underflow results in the maximum value, and for signed integers, exceeding the minimum value wraps around to the maximum positive value. |
| SC03    | Timestamp Dependence               | Smart contracts often use `block.timestamp` for time-sensitive functions. However, miners can slightly adjust this timestamp, creating a vulnerability where they can manipulate the timing to gain an unfair advantage.                         |
| SC04    | Access Control Vulnerabilities     | An access control vulnerability is a security flaw that allows unauthorized users to access or modify a contract’s data or functions. These vulnerabilities occur when the contract’s code fails to properly restrict access based on user permissions. |
| SC05    | Front-running Attacks              | Front-running is an attack where a malicious actor exploits knowledge of pending transactions to gain an unfair advantage. Attackers observe the mempool and place their own transactions with higher gas fees to be processed before the target transaction, leading to potential financial losses and disruption of smart contract functionality. |
| SC06    | Denial of Service (DoS) Attacks    | A Denial of Service (DoS) attack in Solidity targets vulnerabilities within smart contracts to exhaust critical resources such as gas, CPU cycles, or storage. These attacks aim to render the contract non-functional, disrupting its intended operation and potentially causing financial harm. |
| SC07    | Logic Errors                       | Logic errors, or business logic vulnerabilities, are subtle flaws found in smart contracts where the code deviates from its intended behavior. These errors can be challenging to detect as they reside within the contract’s logic, potentially leading to unintended outcomes or exploitable conditions. |
| SC08    | Insecure Randomness                | Generating true randomness in smart contracts on blockchain networks is challenging due to their deterministic nature. Predictability or influence over a supposedly random number can allow attackers to exploit contracts for their benefit, undermining fairness and security measures. |
| SC09    | Gas Limit Vulnerabilities          | Gas limits on blockchain platforms like Ethereum impose constraints on smart contract computations per transaction. Functions exceeding the block gas limit, particularly those involving loops over dynamic data structures such as arrays, risk transaction failure due to resource exhaustion, highlighting a common vulnerability in contract design. |
| SC10    | Unchecked External Calls           | In Ethereum smart contracts, failing to properly verify the outcome of external function calls can lead to unintended consequences. If the called function fails and the calling contract does not check for this, it may incorrectly proceed under the assumption of success, potentially compromising contract integrity and functionality. |
