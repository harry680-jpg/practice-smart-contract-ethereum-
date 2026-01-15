# practice-smart-contract-ethereum-

##First smart contract practice

\\\ solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.26;

// This is the contract o hash string using keccak256
contract SetAndGetString {

    string private harryString = "Harry";

    function getString () public view returns (string memory) {
        return harryString;
    }

function setString (string memory _str) public{
     harryString = _str;
}
}



\\\
