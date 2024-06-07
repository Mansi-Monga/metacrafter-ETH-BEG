
## Title
**CustomToken: A Smart Contract for Mintable and Burnable Tokens on the Ethereum Blockchain**

## Description
The `CustomToken` project is a smart contract written in Solidity for the Ethereum blockchain. This contract allows for the creation, minting, and burning of a custom cryptocurrency. The contract includes functionalities to define a token with a specific name and symbol, mint new tokens to increase the total supply, burn tokens to decrease the total supply, and track balances of different addresses. Events are used to log significant actions, ensuring transparency and enabling interaction with off-chain applications.

## Program Executing
To deploy and execute the `CustomToken` smart contract, follow these steps:

1. **Setup Environment**:
   - Use Remix Ethereum IDE or a local development environment with Truffle or Hardhat.
   - Ensure you have an Ethereum client like MetaMask for deployment and interaction.

2. **Deploy the Contract**:
   - Copy the contract code into Remix or your preferred IDE.
   - Compile the contract using Solidity compiler version 0.8.18.
   - Deploy the contract by providing the token name and symbol during deployment.

3. **Interact with the Contract**:
   - Use the deployed contract's functions `mint` and `burn` to manage tokens.
   - Monitor events for logging and external application interactions.

## Explanation
### Solidity Version and License
The contract starts with the SPDX license identifier and Solidity version declaration to ensure compatibility and licensing clarity.

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.18;
```

### Contract Declaration
The `CustomToken` contract is declared, and public variables to store token details are defined.

```solidity
contract CustomToken {
    string public tokenName;
    string public tokenSymbol;
    uint256 public totalTokens;
```

### Mapping for Balances
A mapping is used to track the balances of each address.

```solidity
    mapping(address => uint256) public accountBalances;
```

### Constructor
The constructor initializes the token's name, symbol, and sets the initial total supply to zero.

```solidity
    constructor(string memory _tokenName, string memory _tokenSymbol) {
        tokenName = _tokenName;
        tokenSymbol = _tokenSymbol;
        totalTokens = 0;
    }
```

### Mint Function
The `mint` function allows creating new tokens by increasing the total supply and the recipient's balance. An event is emitted to log this action.

```solidity
    function mint(address recipient, uint256 amount) public {
        require(amount > 0, "Mint amount must be greater than zero");
        totalTokens += amount;
        accountBalances[recipient] += amount;
        emit TokenTransfer(address(0), recipient, amount);
    }
```

### Burn Function
The `burn` function allows destroying tokens by decreasing the total supply and the holder's balance, ensuring the holder has sufficient tokens. An event is emitted to log this action.

```solidity
    function burn(address holder, uint256 amount) public {
        require(amount > 0, "Burn amount must be greater than zero");
        require(accountBalances[holder] >= amount, "Insufficient balance to burn");
        totalTokens -= amount;
        accountBalances[holder] -= amount;
        emit TokenTransfer(holder, address(0), amount);
    }
```

### Event Declaration
The `TokenTransfer` event logs token transfer actions, including minting and burning.

```solidity
    event TokenTransfer(address indexed from, address indexed to, uint256 value);
}
```

## Output
Upon deploying and interacting with the `CustomToken` contract, the following outputs can be observed:

1. **Deployment**: The contract is deployed with the specified token name and symbol. Initial total supply is zero.
2. **Minting Tokens**: Tokens are minted to the specified address, increasing the total supply and updating the recipient's balance.
3. **Burning Tokens**: Tokens are burned from the specified address, decreasing the total supply and updating the holder's balance.
4. **Event Logs**: `TokenTransfer` events are emitted for both minting and burning actions, providing a transparent log of these actions.

### Example Outputs
- **Minting**: 
  ```plaintext
  TokenTransfer(address(0), recipient_address, 100);
  ```
- **Burning**:
  ```plaintext
  TokenTransfer(holder_address, address(0), 50);
  ```

## Thanks Note
Thank you for exploring the `CustomToken` project. This smart contract demonstrates the foundational concepts of token creation and management on the Ethereum blockchain. By understanding and utilizing these principles, you can develop more complex and feature-rich decentralized applications. Should you have any questions or need further assistance, feel free to reach out. Happy coding!

---

This overview provides a comprehensive understanding of the `CustomToken` project, its implementation, and its functionality.
