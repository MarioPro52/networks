# networksconst Web3 = require('web3');

// Replace with your Infura project endpoint
const infuraUrl = 'https://mainnet.infura.io/v3/YOUR_INFURA_PROJECT_ID';

const web3 = new Web3(new Web3.providers.HttpProvider(infuraUrl));

// Replace with your Ethereum address
const address = '0xYourEthereumAddress';

// Function to get the balance of the address
async function getBalance() {
    try {
        const balance = await web3.eth.getBalance(address);
        console.log('Balance:', web3.utils.fromWei(balance, 'ether'), 'ETH');
    } catch (error) {
        console.error('Error getting balance:', error);
    }
}

// Function to send a transaction
async function sendTransaction() {
    try {
        const accounts = await web3.eth.getAccounts();
        const transaction = {
            from: accounts[0],
            to: '0xRecipientAddress',
            value: web3.utils.toWei('0.01', 'ether'),
            gas: 21000,
        };

        const signedTransaction = await web3.eth.accounts.signTransaction(transaction, 'YOUR_PRIVATE_KEY');
        const receipt = await web3.eth.sendSignedTransaction(signedTransaction.rawTransaction);
        console.log('Transaction receipt:', receipt);
    } catch (error) {
        console.error('Error sending transaction:', error);
    }
}

// Call the functions
getBalance();
// sendTransaction(); // Uncomment to send a transaction
