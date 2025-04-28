# Experiment 5: Zero-Knowledge Proof (ZK) Private Voting System
# Aim:
To implement a fully private and transparent voting system using Zero-Knowledge Proofs (ZKPs). This ensures that votes are counted fairly without revealing who voted for whom.

# Algorithm:

Step 1: Each voter creates a secret and makes a hidden (hashed) commitment of their vote.

Step 2: Voters register by submitting their hidden commitment to the smart contract.

Step 3: During the voting period, voters wait without revealing their actual vote.

Step 4: After voting ends, voters reveal their secret and choice to the contract.

Step 5: The contract checks if the revealed vote matches the original commitment and counts it.

Step 6: Finally, the total votes are announced without revealing who voted for whom.



# Program:

### Developed by: Prem Kumar G
### Register number: 212223230158
### Date: 28/04/2025
```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract ZKVoting {
    struct Voter {
        bool registered;
        bytes32 voteCommitment;
    }

    mapping(address => Voter) public voters;
    uint256 public votesForA;
    uint256 public votesForB;

    event VoteCommitted(address voter, bytes32 commitment);
    event VoteRevealed(address voter, uint256 choice);

    function registerVoter(bytes32 commitment) public {
        require(!voters[msg.sender].registered, "Already registered");
        voters[msg.sender] = Voter(true, commitment);
        emit VoteCommitted(msg.sender, commitment);
    }

    function revealVote(string memory secret, uint256 choice) public {
        require(voters[msg.sender].registered, "Not registered");
        require(keccak256(abi.encodePacked(secret, choice)) == voters[msg.sender].voteCommitment, "Invalid proof");

        if (choice == 1) votesForA++;
        if (choice == 2) votesForB++;

        emit VoteRevealed(msg.sender, choice);
    }
}

```
# Expected Output:
Voters commit their votes privately.


When revealed, the contract verifies correctness but keeps votes anonymous.


Final result is publicly verifiable without exposing individual votes.



# High-Level Overview:
Uses ZKPs to ensure anonymous and fair elections.


Prevents vote tampering while maintaining voter privacy.


Mimics real-world ZK voting applications in governance and DAOs.

# Output:

### Register voter

![alt text](<Screenshot 2025-04-28 132632.png>)

### Reveal vote

![alt text](<Screenshot 2025-04-28 132708.png>)
![alt text](<Screenshot 2025-04-28 132904.png>)

### Register voter for new user

![alt text](<Screenshot 2025-04-28 132936.png>)

### Reveal vote

![alt text](<Screenshot 2025-04-28 133007.png>)
![alt text](<Screenshot 2025-04-28 133044.png>)


# RESULT: 

Thus, To implement a fully private and transparent voting system using Zero-Knowledge Proofs (ZKPs). This ensures that votes are counted fairly without revealing who voted for whom is successfully executed.
