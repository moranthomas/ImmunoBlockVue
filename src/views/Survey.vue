<template>
    <div class="trn-container">

        <div class="row">
            <div class="col-md-8">
                    <h3> Autoimmune Diagnosis History </h3>
            </div>
        </div>
        <hr>
        <div>
            <form onSubmit={this.handleSubmit}>
                <div className="field">
                    <label className="label">
                        1 - Please select the autoimmune diseases you have been diagnosed with.
                    </label>
                    <div className="control">
                        <div className="select">
                            <select
                                name="qA-0"
                                onChange={this.handleChange}
                                value={quizAnswers[0]}
                                required={true}
                            >
                                <option value="0" disabled={true}>Select an option</option>
                                <option value="1">Type 1 diabetes</option>
                                <option value="2">Rheumatoid arthritis (RA)</option>
                                <option value="3">Psoriasis/psoriatic arthritis</option>
                                <option value="4">Multiple sclerosis</option>
                            </select>
                        </div>
                    </div>
                </div>
                <br />

                <div className="field">
                    <label className="label">
                        2 - At what age did you first seek medical advice for your symptoms?
                    </label>
                    <div className="control">
                        <input
                            className="input"
                            type="text"
                            name="qA-1"
                            required={true}
                            value=""
                            onChange={this.handleChange}
                        />
                    </div>
                </div>
                <br />

                <div className="field">
                    <label className="label">
                        3 - Was your diagnosis of an autoimmune disease confirmed by a specialist?
                    </label>
                    <div className="control">
                        <label className="radio">
                            <input
                                type="radio"
                                name="qA-2"
                                required={true}
                                value="1"
                                checked="1"
                                onChange={this.handleChange}
                            />
                            Yes
                        </label>
                        <label className="radio">
                            <input
                                type="radio"
                                name="qA-2"
                                value="2"
                                checked="0"
                                onChange={this.handleChange}
                            />
                            No
                        </label>
                    </div>
                </div>
                <br />

                <div className="field">
                    <label className="label">
                        4 - At what age were you first diagnosed by a specialist?
                    </label>
                    <div className="control">
                    <input
                        className="input"
                        type="number"
                        name="qA-3"
                        required={true}
                        value={quizAnswers[3]}
                        onChange={this.handleChange}
                    />
                    </div>
                </div>
                <br />

                <div className="field">
                    <label className="label">
                        5 - How many doctors have you seen for your autoimmune disease?
                    </label>
                    <div className="control">
                    <input
                        className="input"
                        type="number"
                        name="qA-4"
                        required={true}
                        value={quizAnswers[4]}
                        onChange={this.handleChange}
                    />
                    </div>
                </div>
                <br />

                <div className="field">
                    <label className="label">
                        6 - How many doctors did you see before you were correctly diagnosed?
                    </label>
                    <div className="control">
                    <input
                        className="input"
                        type="number"
                        name="qA-5"
                        required={true}
                        value={quizAnswers[5]}
                        onChange={this.handleChange}
                    />
                    </div>
                </div>
                <br />

                <div className="field">
                    <label className="label">
                        7 - Do you have first degree relatives with an autoimmune disease?
                    </label>
                    <div className="control">
                        <label className="radio">
                            <input
                                type="radio"
                                name="qA-6"
                                required={true}
                                value="1"
                                checked=""
                                onChange={this.handleChange}
                            />
                            Yes
                        </label>
                        <label className="radio">
                            <input
                                type="radio"
                                name="qA-6"
                                value="2"
                                checked=""
                                onChange={this.handleChange}
                            />
                            No
                        </label>
                    </div>
                </div>
                <br />

                <div className="field">
                    <label className="label">
                        8 - Do you currently smoke tobacco?
                    </label>
                    <div className="control">
                    <label className="radio">
                            <input
                                type="radio"
                                name="qA-7"
                                required={true}
                                value="1"
                                checked=""
                                onChange={this.handleChange}
                            />
                            Yes
                        </label>
                        <label className="radio">
                            <input
                                type="radio"
                                name="qA-7"
                                value="2"
                                checked=""
                                onChange={this.handleChange}
                            />
                            No
                        </label>
                    </div>
                </div>
                <br />

                <div className="field is-grouped">
                    <div className="control">
                        <!--<input type="submit" className="button is-primary" value="Submit" />-->
                        <button>Submit</button>
                    </div>
                </div>
            </form>
        </div>




    </div>   <!-- end  container div -->
</template>


<script>

    import Web3 from 'web3';

    let web3;
    let web3Provider;
    let contract_instance;

    // Get the contract address from the remix deploy tab
    let contract_address = "0x10ff1115b527fa00b58afd62eae7c419d0052979";
    // Get the ABI from the remix compile tab > details
    let contract_abi = [ { "constant": false, "inputs": [], "name": "kill", "outputs": [], "payable": false, "stateMutability": "nonpayable", "type": "function" }, { "constant": false, "inputs": [ { "name": "myNewVariable", "type": "uint256" } ], "name": "setMyVariable", "outputs": [], "payable": false, "stateMutability": "nonpayable", "type": "function" }, { "inputs": [], "payable": true, "stateMutability": "payable", "type": "constructor" }, { "payable": true, "stateMutability": "payable", "type": "fallback" }, { "constant": true, "inputs": [], "name": "getMyBalance", "outputs": [ { "name": "", "type": "uint256" } ], "payable": false, "stateMutability": "view", "type": "function" }, { "constant": true, "inputs": [], "name": "getMyVariable", "outputs": [ { "name": "", "type": "uint256" } ], "payable": false, "stateMutability": "view", "type": "function" } ];

    export default {
        data () {
            return {
                selected: '0',
                accounts: [],
                networks: ['ganache', 'infura', 'metamask', 'rinkeby']
            }
        },
        mounted() {
            this.loadWeb3Provider();
            contract_instance = new web3.eth.Contract(contract_abi, contract_address);
        },
        methods: {

            // See https://web3js.readthedocs.io/en/1.0/web3-eth-contract.html for docs

            getMyVariable() {
                //To-Do - create a dropdown of accounts and populate the from using that

                contract_instance.methods.getMyVariable().call({from: contract_address}, (error, result) => {
                    this.$refs.myVariableInputField.value = result;
                    console.log("SUCCESSFUL CALL OF CONSTANT (VIEW) METHOD - NO NEED FOR GAS!");
                });
            },
            setMyVariable() {
                contract_instance.methods.setMyVariable(12).call({from: contract_address}, (error, result) => {
                    console.log("SUCCESSFULLY UPDATED!");
                });
            },
            loadWeb3Provider: function () {

                const infuraUrl = "http://mainnet.infura.io/v3/53dbf207e63c42e99cacb63c2d41ec4f";
                const ganacheUrl = "http://localhost:8545";

                const chosenNetwork = localStorage.getItem('selectedNetwork');

                if(chosenNetwork === "ganache") {
                    web3Provider = new Web3.providers.HttpProvider(ganacheUrl);
                }
                else if (chosenNetwork === "infura") {
                    web3Provider = new Web3.providers.HttpProvider(infuraUrl);
                }
                else {
                    // Modern dapp browsers...
                    if (window.ethereum) {
                        web3Provider = window.ethereum;
                        try {
                            // Request account access
                            window.ethereum.enable();
                        } catch (error) {
                            // User denied account access...
                            console.error("User denied account access")
                        }
                    }
                    // Legacy dapp browsers...
                    else if (window.web3) {
                        web3Provider = window.web3.currentProvider;
                    }
                    // If no injected web3 instance is detected, fall back to Ganache
                    else {
                        web3Provider = new Web3.providers.HttpProvider(ganacheUrl);
                    }
                }

                web3 = new Web3(web3Provider);

            },
            getNodeInfoClicked: function() {
                /* Get Node Info*/
                this.$refs.NodeInfoInputField.value = web3.currentProvider.host
            },
            populateAccountsClicked: function(event) {
                let self = this       // to get around lexical scoping issue - could use another outer arrow fn instead
                web3.eth.getAccounts(function(error, accounts) {
                    if(error) {
                        console.log(error);
                    }
                    else{
                        self.accounts = accounts
                        for(var account of accounts) {
                            console.log(self.$refs.accountRef.value)
                        }
                    }
                });
            },
            checkBalanceClicked: function() {
               //Get Balance
               let balanceinEther;
               let self = this       // to get around lexical scoping issue - could use another outer arrow fn instead
               let selectedAccount = this.$refs.accountRef.value
               web3.eth.getBalance(selectedAccount).then(result => {
                    balanceinEther = web3.utils.fromWei(result, 'ether');
                    self.$refs.balanceRef.value = balanceinEther;
               });
            },
            onChange: function (event) {
                var index = event.srcElement.value;
                this.$refs.accountRef.value = event.srcElement[index].label
            },
            onChangeNetwork: function (event) {
                var index = event.srcElement.value;
                localStorage.setItem('selectedNetwork', event.srcElement[index].label )
                this.loadWeb3Provider();
            },
            transferFunds: function () {
                const _from = this.$refs.fromRef.value
                const _to = this.$refs.toRef.value
                const _amount = this.$refs.amountRef.value
                let self = this
                var txnObject = {
                    "from":_from,
                    "to": _to,
                    "value": web3.utils.toWei(_amount,'ether'),
                    "gas": 1000,         //(optional)
                    // "gasPrice": 4500000,  (optional)
                    // "data": 'For testing' (optional)
                    // "nonce": 10           (optional)
                }

                web3.eth.sendTransaction(txnObject, function(error, result){
                    if(error){
                        console.log( "Transaction error" ,error);
                        self.$refs.resultRef.value = "Transaction Failed"
                    }
                    else{
                        //Get transaction hash
                        self.$refs.txHashRef.value = result;
                        self.$refs.resultRef.value = "Transaction Succeeded!"
                    }
                });
            },
        },
    }
</script>


<style>

.trn-body {
    background-color:#F0F0F0;
    padding: 2em;
    font-family: 'Raleway','Source Sans Pro', 'Arial';
}

label {
    display: block;
    margin-bottom:10px;
    margin-right: 20px;
    float: left;
}
input {
    padding:10px;
    width: 100%;
    margin-bottom: 1em;
    border-color: #2dce89;
}
.node-input{
    width: 70%;
}

button {
    margin: 2em 0;
    padding: 1em 4em;
    display:block;
}

.trn-container {
    width: 60%;
    margin: 0 auto;
    padding-right: 15px;
    padding-left: 15px;
    max-width: 1040px;
}


#instructor {
    padding:1em;
    background-color:#fff;
    margin: 1em 0;
}
</style>