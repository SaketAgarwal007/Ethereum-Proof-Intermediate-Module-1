# Ethereum-Proof-Intermediate-Module-1
# Hanger Management Smart Contract

This Solidity program is a simple Hanger Management smart contract that allows the owner to manage the docking and undocking of planes at different hangers. The contract includes functionalities to dock and undock planes, ensure the availability of hangers, utilizing concepts such as function modifiers and error handling.

## Description

This program is a basic smart contract written in Solidity, a programming language used for developing smart contracts on the Ethereum blockchain. The contract allows the owner to:

        1. Dock Planes at available Hangers
        2. Undock planes from Hangers
        3. Ensure the availability of hangers and handle errors effectively using required statements

## Getting Started

### Executing Program

To run this program, we can use Remix, an online Solidity IDE. Follow the steps below to get started:

    1. Go to the Remix website.
    2. Create a new file by clicking on the "+" icon in the left-hand sidebar.
    3. Save the file with a .sol extension (e.g., HangerManagement.sol).
    4. Copy and paste the following code into the file:
    
```solidity
//SPDX-License-Identifier: MIT
pragma solidity 0.8.25;

contract airdock{
    address public owner;
    uint public totalhangers=6;
    uint public total_planes=0;

    constructor(){
        owner=msg.sender;
    }

    modifier onlyOwner(){
        require(msg.sender==owner,"Only Owner Can Access");
        _;
    }

    mapping(uint=>bool) public hangeravailability;
    mapping(uint=>address) public planeathanger;

    function dockPlane(address _planeaddress) public onlyOwner{
        require(total_planes<6,"no hanger available");
        for(uint i=1;i<=6;i++){
            if(hangeravailability[i]==false){
                hangeravailability[i]=true;
                planeathanger[i]=_planeaddress;
                total_planes++;
                break;
            }
        }
    }

    function undockPlane(address _planeaddress)public onlyOwner{
        require(total_planes>0,"no plane to remove");
        uint hangerofplane=1;
        bool planefound=false;

        for(uint i=1;i<=6;i++){
            if(planeathanger[i]==_planeaddress){
                hangerofplane=i;
                planefound=true;
            }
        }

        planeathanger[hangerofplane]=address(0);
        hangeravailability[hangerofplane]=false;
        total_planes--;

        if(!planefound){
            revert("Plane Not Found!");
        }

    }

    function assertAvailabilty() public view{
        assert(total_planes>0 && total_planes<=6);
    }
}
```
### Compiling the Code

    1. Click on the "Solidity Compiler" tab in the left-hand sidebar.
    2. Ensure the "Compiler" option is set to "0.8.25" (or another compatible version).
    3. Click on the "Compile HangerManagement.sol" button.

### Deploying the Contract

    1. Go to the "Deploy & Run Transactions" tab in the left-hand sidebar.
    2. Select the "HangerManagement" contract from the dropdown menu.
    3. Click on the "Deploy" button.
    4. Interacting with the Contract.

You can interact with the contract by calling the functions once the contract is deployed. Ensure you are connected to the owner's address to perform owner-restricted functions.

#### Dock plane:
    1. Select the dockPlane function.
    2. Enter the plane's address to dock.
    3. Click on the "transact" button.

#### Undock plane:
    1. Select the undockPlane function.
    2. Enter the plane's address to undock.
    3. Click on the "transact" button.

#### AssertAvailabilty
    1. Select the assertAvailability function.
    2. Relevant output will be visible on the screen.
    
## Authors
Saket Agarwal
[@rajeevsingh](https://www.linkedin.com/in/saket-agarwal007)
