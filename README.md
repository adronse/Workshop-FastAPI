# Workshop 1 - FastAPI :open_book:

During this workshop, you will create a simple backend using the python web framework FastAPI

FastAPI is a modern, fast (high-performance), web framework for building APIs with Python 3.6+ based on standard Python type hints.

Please make sure to read each step carefully, as very useful links are given with the instructions.

Every Python files contains TODO instructions. Take a look at them to get more details and context about the task.

## Step 0 : Initialization :rocket:

First, download and extract the `source.zip` file [here](https://github.com/adronse/Workshop-FastAPI/blob/main/workshop.zip).
It contains all necessary files, but for the moment they're empty :wink:

The project structure should be the following :

```
.
├── requirements.txt
├── step1
│   └── main.py
├── step2
├── step3
├── step4
└── step5

```

At the root directory, create a virtual environment like so:
   - python3 -m venv (NAME_ENV)
   - source (NAME_ENV)/bin/activate
Then, run `pip install -r requirements.txt` at the root of the downloaded folder.

## Step 1 : Running the backend server

As said before, the web framework you'll use to create your backend is FastAPI.
It's all based on standard Python 3.6 type declarations (thanks to Pydantic). No new syntax to learn. Just standard modern Python.

FastAPI uses the ASGI server implementation you can see that like the as the "node server".

### To launch the server

- cd step1/

- If you have been following the instructions: run uvicorn main:app

- You should see a prompt telling you the server is running on http://127.0.0.1:8000

## Step 2 : Compiling the contract :gear:

Now that you've written the contract, you need to compile it !
The compiler used is `solc`, and has already been included to your `package.json` dependencies file.

You need to do the following steps to get the bytecode & ABI (Application Binary Interface) of the contract :

- Retrieve the file content. The solc compiler obviously needs the contract's code to compile it, but instead of juste copy/paste the code for the next step you may wan't to automate this process by reading the file dynamically. 

- Give the content to the compiler. Note that the `compile.js` file already contains a variable, but the `sources['Inbox.sol']` field is empty.

- Compile and extract the bytecode & ABI from the result (check [this](https://github.com/ethereum/solc-js) out :wink:).

- Write the bytecode & ABI to the corresponding file in the `out` folder.

As you've probably guessed, the bytecode contains a compiled version of your contract that will be executed by the EVM.
You will use the ABI to interact with the contract.

## Step 3 : Tests using mocha & assert :test_tube:

Time to test !
The tests are very important while writing a smart contract, because once they're deployed on a real blockchain, you can not update or delete it.
So make sure that everything is working as expected before deploying a contract.

You'll use mocha as a testing framework and chai as an assertion library.

Two more things before you start :

- If you've looked at the packages in the dependencies, you probably saw `ganache`.
    Ganache will launch a virtual Ethereum network on your local environment.
    There is also a gui version available [here](https://www.trufflesuite.com/ganache).

- The ABI is an interface between you (the developer) and the EVM.
    If you take a look at its content, and it's highly recommended, you'll see your contract functions name & variables.
    Web3, an API developed by the Ethereum foundation, is responsible for connecting your javascript code with the contract bytecode actually running on an Ethereum node.
    Web3 requires a provider to work properly. We'll use the ganache provider for this workshop, but in the real world it could be the [Metamask](https://metamask.io/) one.

Okay, time to test !

- The first thing you want to test is that the contract deployment works correctly.
    For this part, you must know that deploying a contract is just a method from the `Contract` subclass of the `Web3` class.
    A contract must be deployed by an account. Hopefully, Ganache creates a list of 10 accounts whenever it is loaded.

- Then, test all of your functions.
    Note that when you declare a `public` variable in Solidity, the EVM automatically creates an accessor for this variable (a `call`).
    Whenever you call a function that modifies the contract state (i.e. stored variables), you must send a transaction to the targeted function.
    You must test the following features :
  
    - The contract has been deployed properly
    - The initial message has been set to "PoC"
    - Every account can access the message
    - Every account can set a new message
    
- Here is an example on how you can use mocha : 
    ```javascript
    const assert = require('assert');
    
    function add(a, b) {
        return a + b;
    }
  
    describe('Add', () => {
        it('should add two numbers', () => {
            let a = 20;
            let b = 22;
  
            assert.equal(add(a, b), 42);
        });
    });
    ```
    If you run `npm run tests`, you should see the test passing.
    
    Check [this](https://web3js.readthedocs.io/en/v1.3.0/web3-eth-contract.html#methods-mymethod-call) link for more information about how you can call your contract functions.

## Step 4 : Time to deploy :outbox_tray:

Until now, you've only worked on your local ethereum network.
Your smart contract is fully tested and ready to be deployed on the real blockchain !

But deploying a smart contract is done by sending a transaction, and you probably don't want to pay real money to accomplish this step wright ?

This is why testnet are useful :wink:, they behave the same way as the mainnet does, but their ether value is null. 

So first, you need to install Metamask extension on your browser.
Follow the steps required and don't forget to set the network to be the Ropsten Test Network.
Then, go to [this faucet](https://faucet.dimensions.network/) and paste your wallet account address to get 5 ether.

You also need a new provider, since ganache only works locally. You will use the `HDWalletProvider` one provided in the `deploy.js` file.
Because you are sending a transaction to the real network, you have to know the endpoint of an ethereum node.

Infura can provide this information. As we support decentralisation of the Ethereum blockchain here is an endpoint you can use :

https://ropsten.infura.io/v3/510289ba8f254e46891aaa84a718ddd9

Feel free to use the code you've written during tests to deploy and interact with the contract on the Ropsten Network.

### Authors

[Luca Georges Francois](https://github.com/PtitLuca)
