### Experiment 1: Decentralized Certificate Verification
## Aim:
  To develop a smart contract for issuing and verifying academic certificates on Ethereum, preventing forgery and ensuring authenticity.
## Algorithm:
### step 1:
Deploy a smart contract where universities can issue certificates.
### step 2:
Store a hash of certificate data on-chain.
### step 3:
Provide a verification function that checks certificate authenticity.
### step 4:
Users can verify the certificate by comparing the stored hash.
## Program:
#### Developed by: Prem Kumar G
#### Register number: 212223230158
#### Date: 16/04/2025
```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract CertificateVerification {
    address public university;
    mapping(bytes32 => bool) public certificates; 
    event CertificateIssued(bytes32 indexed certHash);
    constructor() {
        university = msg.sender;
        }
        function issueCertificate(string memory studentName, string memory degree, uint256 year) public {
            require(msg.sender == university, "Only university can issue certificates");
            bytes32 certHash = keccak256(abi.encodePacked(studentName, degree, year));
            certificates[certHash] = true;
            emit CertificateIssued(certHash);
        }
        function verifyCertificate(string memory studentName, string memory degree, uint256 year) public view returns (bool) {
            bytes32 certHash = keccak256(abi.encodePacked(studentName, degree, year));
            return certificates[certHash];
        }
}
```
# Expected Output:
```
● When the university issues a certificate, it gets stored as a hash.
● A student or employer can verify the certificate by entering the details.
● If valid, it returns true; otherwise, false.
High-Level Overview:
● Used to prevent fake certificates.
● Enables quick verification by employers or other institutions.
● Shows how blockchain can be used in education and credential verification.
```
# Output:
![alt text](<Full output.png>)
![alt text](<Output 2.png>)
![alt text](<Output 3.png>)
# Result:
   Thus,to develop a smart contract for issuing and verifying academic certificates on Ethereum, preventing forgery and ensuring authenticity is successfully executed. 
