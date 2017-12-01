# ethereum-solidity-tutorial
Ethereum Solidity tutorial notes

Notes from the excellent video series on the What's Solidity
YouTube channel: https://www.youtube.com/watch?v=v_hU0jPtLto

This github repo is just for my notes of that series. I have mostly followed what the author suggests though sometimes have added my own additional comments.

## --- 1 The Basics


* We're going to be using the Web IDE called Remix on the Ethereum site: 

http://remix.ethereum.org/

* We're going to do a basic contract with getters, setters and variables.
* Clear out the default file in Remix and create a file `myfirstcontract.sol`

* Now we define which version we'll be using

```
pragma solidity ^0.4.0;
```

*  Next we define a contract

```
contract MyFirstContract{

}
```

* That is all that is needed for a contract. You now have a contract. However, we will be adding some more variables.

* We'll start by creating String and and Integer. (optional) you can make it private by adding private after string. The integer can be signed (pos) or unsigned (neg/pos). This is uint - unsigned integer

```
string private name;
uint private age; 
```

* Now we'll do the setter:

```
function setName(string newName) {
    name = newName;
}
```

* To return the newName (getter):

```
function getName() returns (string) {
    return name;
}
```

* We now have our 2 methods.

* To test this, in Remix we can click on the right side "create".
* Once that is finished you can test it with the console on the right side, put in a name like "Chris" (use quotes because it's JSON) in setName and then hit getName
* When the result comes in the main console, check detaisl to make sure it was decoded correctly.

* Now add the same for age:

```
    function setAge(uint newAge) {
        age = newAge;
    }
    
    function getAge() returns (uint) {
        return age;
    }
```

* You can check the age in the same way we checked name.

see more: https://github.com/willitscale/learning-solidity/blob/4caaeb93eadf8191618c679675366e2c3d035e9c/tutorial-01/myfirstcontract.sol

## --- 2 Inheritance (13m)
 
* Solidity has 3 aspects of inheritance:
* (1) A general extension of functionality from 1 contract to another.
* So let's start a new contract `Bank` 

```
contract Bank {
    
}
```

* We can extend MyFirstContract by changing the code to `MyFirstContract is Bank`- now any functionality in Bank will also exist in MyFirstContract

* Next we'll add functionality to Bank
* However, there are some attributes to Bank that we want private and not accessed by MyFirstContract.
* Next we put in an unsigned integer call `uint internal myInternalValue` -- internal is the equivalent modifier of protected in other languages
* Change that to private, as we don't want another function to modify that value.
* Change it to `uint private value;`
* We're making this as if it's a bank account, so we'll be adding related bank account methods.
* Deposit Money: 
```
function deposit(uint amount) {
    value += amount;
}
```
* Withdraw Money:
```
function withdraw(uint amount) {
    if (checkValue(amount)) {
        value -= amount;
    }
}
```
* Balance"
```
function balance() returns (uint) {
    return value;
}
```

* Back to console - Create - you should see the buttons for Balance, Withdraw and Deposit

* How do we get value? (actual number, ie. 10) We could put the actual value in the Bank method - however, then all inheriting methods of Bank with have the value of 10
* A better idea is to use a constructor.

```
function Bank(uint amount) {
    value = amount;
}
```

* What this does then is make it so any method that inherits from Bank can also specify the value.

* Let's use 10 as a start value and put that in the `contract MyFirstContract is Bank(10) `

* We can also define a loan in MyFirstContract

```
function loan() returns (bool) {
    return value > 0;
}
```

* Now let's create an abstract interface because we need to make sure we have enough funds in the account to withdraw. 

```
interface Regulator {
    function checkValue(uint amount) returns (bool);
    function loan() returns (bool);
}
```

* AND we must give Bank this functionality, so revise to: `contract Bank is Regulator {`

* Move out function loan() back to Bank, so it can be used by multiple contracts.

* Now in Bank we will add a checkValue to make sure there is enough money in the account.

```
function checkValue(uint amount) returns (bool) {
    // Classic mistake in the tutorial value should be above the amount
    return value >= amount;
}
```












.