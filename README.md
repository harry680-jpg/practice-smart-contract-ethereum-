# practice-smart-contract-ethereum
This is a repo for me to practice my solidity 

##First smart contract practice
``` solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.26;

contract MappingPractice{

    // Declare a state variable to save the value
    mapping(address => string) private students;

   // Declare a function to set a value for a student
   function setStudent(address _addr, string memory _name) public{
      students[_addr] = _name;
   }

   // Declare a function to show/get the value from the state variable
   function getStudent(address _addr) public view returns ( string memory){
    return students [_addr];
   }
 
   // Declare a function to remove a student 
   function removeStudent (address _addr) public {
    delete students[_addr];
   }

}
```
