# Passport and Visa application

This Solidity program is a simple demo code for error handling. The purpose of the program is to demonstrate the error handling while creation and updation of passport and application for visa using ```require(), assert() and revert()```.
## Description
This contract is written in Solidity language, a programming language used for developing smart contracts on the Ethereum blockchain. First there is an enum ```enum nation {India, Russia, UK, Germany}``` to denote the nationality. Then ```struct candidates {..}``` is used to store the name, age, phone number, nationality and isHavingPassport. ```mapping(address =>candidates) public candidate;``` is used to map different candidate to their address. After this we have addCandidate function to add new candidate. Now we have 3 functions where 1st is ```createNewPassport``` with require(), it will check for age; if true then passport will be created. 2nd is ```updatePassport``` which will update the passport only if there is a existing passport and revert() is used to perform this action. 3rd and last function ```applyVisa``` where revert() is used to check if passport exist and assert() is then used to check nationality, here in this case only India and Russia is considerd, UK and Germany is not eligle. 
## Getting Started

### Executing program

To run this program, you can use Remix, an online Solidity IDE. To get started, go to the Remix website at https://remix.ethereum.org/.

Once you are on the Remix website, create a new file by clicking on the "+" icon in the left-hand sidebar. Save the file with a .sol extension (e.g., Visa.sol). Copy and paste the following code into the file:

```javascript
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.7;

contract Visa{

    // India and Russia allowed for visa , UK and Germany not allowed.
    enum nation {India, Russia, UK, Germany}

    //createing a structure to keep data of candidate.
    struct candidates {
        string name;
        uint age;
        uint phNo;
        nation nationality;
        bool isHavingPassport;
    }
    
    //mapping of candidate struct with address.
    mapping(address =>candidates) public candidate;

    //function to add a new candidate
    function addCandidate(address _candidateAddress, string memory _name, uint _age, uint _phNo, nation _nationality, bool _isHavingPassport)public{
        candidate[_candidateAddress].name = _name;
        candidate[_candidateAddress].age = _age;
        candidate[_candidateAddress].phNo = _phNo;
        candidate[_candidateAddress].nationality = _nationality;
        candidate[_candidateAddress].isHavingPassport = _isHavingPassport;
    }

    //fucntion to create a new passport only if age is greate that 18.
    function createNewPassport(address _candidateAddress)public returns(bool){
        //using require err handling if age fall below 18.
        require(candidate[_candidateAddress].age>=18,"Under age, application is rejected");
        candidate[_candidateAddress].isHavingPassport= true;

        return true;
    }

    function updatePassport(address _candidateAddress,uint _newPhoneNo)public returns(candidates memory,string memory){
        if(candidate[_candidateAddress].isHavingPassport!= true){
            revert("No existing passport to update, first create a new one");
        }
        candidate[_candidateAddress].phNo= _newPhoneNo;
        return (candidate[_candidateAddress],"Passport updated");
    }

    function applyVisa(address _candidateAddress)public view returns (string memory){
        if(candidate[_candidateAddress].isHavingPassport!= true){
            revert("No existing passport to update, first create a new one");
        }
        assert(candidate[_candidateAddress].nationality == nation.India ||
        candidate[_candidateAddress].nationality == nation.Russia);
        return("visa applied successfully");
    }
}

```

To compile the code, click on the "Solidity Compiler" tab in the left-hand sidebar. Make sure the "Compiler" option is set to "0.8.7" (or another compatible version), and then click on the "Compile MyToken.sol" button.

Once the code is compiled, you can deploy the contract by clicking on the "Deploy & Run Transactions" tab in the left-hand sidebar. Select the "Visa" contract from the dropdown menu, and then click on the "Deploy" button.

Once the contract is deployed, you can interact with it. Click on the "Visa" contract in the left-hand sidebar, and then expand addCandidate and enter values and click transact, this will add the candidate. now enter the candidate address in updatePassport with new phone number and transact, if the conditions are fulfilled then transaction will be successful else terminated, next paste the address of exisiting candidate in applyVisa and click call. if candidate has a passport and condition of nationality is fulfilled then visa will be applied else it will be terminated. 
you may change the values of enum nation according to your own comfort and can also change the eligible nations. 

## Authors

Saksham Sethi
sakshamsethi40037@gmail.com


## License

This MyToken is licensed under the MIT License 
