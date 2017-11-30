# ethereum-solidity-tutorial
Ethereum Solidity tutorial notes

Notes from the following video series: https://www.youtube.com/watch?v=v_hU0jPtLto

## 1 The Basics


* We're going to be using the Web IDE: 

http://remix.ethereum.org/

* We're going to do a basic contract with getters, setters and variables.
* Clear out the default file in Remix and create a file `myfirstcontract.sol`

* Now we define which version we'll be using

```
pragma solidity ^0.4.0;
```

*  Next we define a contract"

```
contract MyFirstContract{

}
```

* That is actualyl all that is needed for a contract. You now have a contract. However, we will be adding some more variables.

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

## 2 Inheritance















.