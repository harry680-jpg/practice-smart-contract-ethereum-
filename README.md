#### StructArrayPractice
``` solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.26;

contract StructArrayPractice {

    // Declare a structure for a student 
    struct Student {
        string name ;
        bool isRegistered;
    }

    // Declare an array to hold all the students defined
    Student[] private students;

    // Declare a function as internal to register a student
    function _registerStudent(string memory _name ) internal {
        students.push(Student({
            name: _name,
            isRegistered: true
        }));
    }
    // Declare a function as external to register a student for external accounts
    function registerStudent(string calldata _name) external {
        _registerStudent( _name);
    }

    
    // Declare a function to get student information by index
    function getStudentById (uint256 _index) external view returns (string memory, bool) {
        return (students[_index].name, students[_index].isRegistered);
    }


    // Declare a function to return all the students registred 
    function getAllStudents() external view returns (Student[] memory) {
        return students;
    }

    // Declare a function to popup the last student 
    function popUpStudent() external  {
        students.pop();
    }

// Declare a function to return the lenght of the student array 
function getArrayLength() external view returns (uint256) {
    return students.length;
}

}
```



##### CCMP606 – PiggyBank Ethereum Smart Contract
``` solidity

// SPDX-License-Identifier: MIT
pragma solidity ^0.8.26;

contract PiggyBank {
  address public owner;
    uint256 public savingGoal;
    mapping(address => uint256) private deposits;

   // Declare an events for logging activities
event DepositRecorded(address indexed depoitor, uint256 amount);
event SavingGoalReached(uint256 totalBalance);
event BankEmptied(address indexed owner, uint256 amount);

// Declare a Modifier to restricts accesss to owner only
modifier onlyOwner() {
    require(msg.sender == owner, "Only owner can perform this action");
    _;

}

// Declare a Constructor to initialize the contract with an owner and a saving goal
constructor(uint256 _savingGoal) {
    owner = msg.sender;
    savingGoal = _savingGoal;
}
// Function to Deposit ETH into the PiggyBank
function depositToBank() external payable {
    require(msg.value > 0, "Seposit must be greater than 0");

    // Track Deposits per address
    deposits[msg.sender] += msg.value;

    // Emit Deposit Event
    emit DepositRecorded(msg.sender, msg.value);

    // Check if saving goal is reached
    if (address(this).balance >= savingGoal) {
        emit SavingGoalReached(address(this).balance);

    }
}

// Get currunt contract Balance (Wei)
function getBalance() external view returns (uint256) {
    return address(this).balance;
}

// Get total deposits made by a specific address
function getDepositsValue(address depositor) external view returns (uint256) {
    return deposits[depositor];
}

// Withdraw all ETH (only owner & only after goal reahed)
function emptyTheBank() external onlyOwner {
    require(address(this).balance >= savingGoal, "Saving goal not reached yet");

    uint256 amount = address(this).balance;

    (bool success, ) = payable(owner).call{value: amount}("");
    require(success, "ETH transfer failed");

    emit BankEmptied(owner, amount);
}
}
```


#### Mapping from address to struct with msg.sender and modifier
``` solidity

// SPDX-License-Identifier: MIT
pragma solidity  ^0.8.26;

contract  MappingStructPractice2 {

    // Declare a struct for student
    struct Student {
        string name;
        string email;
        bool isRegistered;
    }

    // Declare a Mapping from address to struct Student
    mapping (address => Student) private students;


    // Declare a function to set a student registration
      function setRegistereation (string memory _name, string memory _email) public {
        require(students[msg.sender].isRegistered == false, "you have registered!!");
        students[msg.sender] = Student ({
            name: _name,
            email: _email,
            isRegistered: true
        });
      }
// Declare a function for student who registered to see the results 
function getResults() public view returns (string memory, string memory){
    require (students[msg.sender].isRegistered == true, "You haven't Registered");
    return (
        students[msg.sender].name,
        students[msg.sender].email);
}
  }

```


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
