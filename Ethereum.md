## Smart Contract Security And Best Practices

* [Ethereum Contract Security Techniques and Tips](https://github.com/ConsenSys/smart-contract-best-practices)
* [Call Depth Stack Attack](http://ethereum.stackexchange.com/questions/10976/questions-about-simpleauction-contract-example)
* [Recursive Call Vulnerability](http://ethereum.stackexchange.com/questions/6176/what-is-a-recursive-calling-vulnerability/6181#6181)
* [How do I make my DAPP “Serenity-Proof?”](http://ethereum.stackexchange.com/questions/196/how-do-i-make-my-dapp-serenity-proof)

<br />

## Send Ethers In `geth` Console

> eth.sendTransaction({from: "from account", to: "to account", value: web3.toWei(ethers, "ether")});

<br />

## Check Whether Contract Is An ERC20 Token

    var erc20Address = "0xB802b24E0637c2B87D2E8b7784C055BBE921011a";
    var erc20ABI = [{"constant":false,"inputs":[{"name":"_spender","type":"address"},{"name":"_value","type":"uint256"}],"name":"approve","outputs":[{"name":"success","type":"bool"}],"payable":false,"type":"function"},{"constant":true,"inputs":[],"name":"totalSupply","outputs":[{"name":"totalSupply","type":"uint256"}],"payable":false,"type":"function"},{"constant":false,"inputs":[{"name":"_from","type":"address"},{"name":"_to","type":"address"},{"name":"_value","type":"uint256"}],"name":"transferFrom","outputs":[{"name":"success","type":"bool"}],"payable":false,"type":"function"},{"constant":true,"inputs":[{"name":"_owner","type":"address"}],"name":"balanceOf","outputs":[{"name":"balance","type":"uint256"}],"payable":false,"type":"function"},{"constant":false,"inputs":[{"name":"_to","type":"address"},{"name":"_value","type":"uint256"}],"name":"transfer","outputs":[{"name":"success","type":"bool"}],"payable":false,"type":"function"},{"constant":true,"inputs":[{"name":"_owner","type":"address"},{"name":"_spender","type":"address"}],"name":"allowance","outputs":[{"name":"remaining","type":"uint256"}],"payable":false,"type":"function"},{"anonymous":false,"inputs":[{"indexed":true,"name":"_from","type":"address"},{"indexed":true,"name":"_to","type":"address"},{"indexed":false,"name":"_value","type":"uint256"}],"name":"Transfer","type":"event"},{"anonymous":false,"inputs":[{"indexed":true,"name":"_owner","type":"address"},{"indexed":true,"name":"_spender","type":"address"},{"indexed":false,"name":"_value","type":"uint256"}],"name":"Approval","type":"event"}];
    var erc20 = web3.eth.contract(erc20ABI).at(erc20Address);
    console.log("symbol(): " + erc20.symbol());
    console.log("name(): " + erc20.name());
    console.log("totalSupply(): " + erc20.totalSupply());

## Eclipse For Editing Solidity And Saving To Github

Install the following plug-ins into Eclipse:

* https://eclipse.github.io/

And set the Preference -> General -> Editors -> File Associations *.sol to the JS Editor