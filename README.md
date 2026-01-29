### Mapping from address to struct

``` solidity
// SPDX-License-Identifier: MIT
pragma solidity  ^0.8.26;

contract MappingStructPractice {
    
    // Declare student structure having three attribute
    struct Student{
    string name;
    string email;
    bool isAttended;
}
    
   // Declare a mapping from address to struct student
   mapping(address => Student) private students;

   // Declare a function to set student attendance
   function setStudentAttendance(address _addr, string memory _name, string memory _email, bool _isAttended) public {
    students[_addr] = Student ({
        name: _name,
        email: _email,
        isAttended: _isAttended    
        });
   }
    
    // Declare a function to get student attendabce info 
    function getStudentAttendance (address _addr) public view returns (string memory, string memory,bool) {
    
    return (students[_addr].name,
            students[_addr].email,
            students[_addr].isAttended
            );
       }

       // Declare a function to toggle to student attendance 
       function toggleStudentAttendance (address _addr) public {
        students[_addr].isAttended = !students[_addr].isAttended;
       }
 
 // Declare a function to update student email
     function modifyDtudentEmail (address _addr, string memory _email) public{
        students[_addr].email = _email;
     }
        }
    
```




### Nested Mapping Practice
This is a practice mapping from address to string and to boolean

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.26;

contract NestedMappingPractice {

    // Declare a state variable as nested mapping datatype
    mapping (address => mapping (string => bool)) private attendanceSheet;

    // Declare a funciton to set values for a student
    function setAttendance (address _addr, string memory _name, bool _isPresent) public {
        attendanceSheet[_addr][_name] = _isPresent;
    }

    // Declare a function to get the value for a student
    function getAttendance (address _addr, string memory _name) public view returns (bool) {
        return attendanceSheet[_addr][_name];
    }

    // Declare a function to toggle the value for a student
    function toggleAttendance (address _addr, string memory _name) public {
        attendanceSheet[_addr][_name] = !attendanceSheet[_addr][_name];
    }
}

```

## Mapping Practice

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.26;

contract PractisingMapping {

    // declare a State Variable mapping from address to string
    mapping(address => string) private names;

    // declare a set function to set the value for the state variable
    function setName (address _addr, string memory _name) public {
        names[_addr] = _name;
    }

    // Declare a get function to get the value from the state variable
    function getName (address _addr) public view returns (string memory) {
        return names[_addr];
    }

    // Declare a function to remove the currently defined value
    function removeName (address _addr) public {
        delete names[_addr];
    }

}

```


## First Smart Contract Practice

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.26;

// This is the contract to hash strings using keccak256
contract YongHashingString {
    // declare state varible
    bytes32 private yongString;
    // hashing the string
    function hashing (string memory _str) public {
        yongString = keccak256(bytes(_str));
    }
    //get the digest of the hasing process
    function getDigest () public view returns (bytes32) {
        return yongString;
    }    
}

```
