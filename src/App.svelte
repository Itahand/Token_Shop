<script>
	import { ethers } from 'ethers';
	import Token from '../artifacts/contracts/OxyDjinn.sol/Token.json';
	fetch("https://api.nomics.com/v1/currencies?key=your-key-here&ids=BTC,ETH,XRP&attributes=id,name,logo_url&platform-currency=ETH")
  .then(response => response.json())
  .then(data => console.log(data))


  const address = "0x5fbdb2315678afecb367f032d93f642f64180aa3"; // Enviroment variable/OxyDjinn token
  let amount = 0;
	let name, symbol;

	const provider = new ethers.providers.JsonRpcProvider(); //Localhost provider/connection to the blockchain(read only)
	let hardhat1 = new ethers.Wallet( "ac0974bec39a17e36ba4a6b4d238ff944bacb478cbed5efcae784d7bf4f2ff80", provider )
	let hardhat2 = "0x70997970C51812dc3A010C7d01b50e0d17dc79C8"

	async function providerFunctions () {

	}
	providerFunctions()
	// Fetch token contract from the blockchain.
	async function sendTokens() {
		const oxyDjinnContract = new ethers.Contract(address, Token.abi, hardhat1)
		name = await oxyDjinnContract.name()
		symbol = await oxyDjinnContract.symbol()

		const oxyDjinnConnection = oxyDjinnContract.connect(hardhat1);
		const coo = ethers.utils.parseUnits(amount.toString(), 18);

		// Send 1 DAI to "ricmoo.firefly.eth"
		let tx = oxyDjinnConnection.transfer(hardhat2, coo);
		console.log('Transaction sent!')

	}
	// Request MetaMask provider and fetch the signer.
	async function getSigner() {
		// A Web3Provider wraps a standard Web3 provider, which is
		// what MetaMask injects as window.ethereum into each page
		let provider = new ethers.providers.Web3Provider(window.ethereum)
		// MetaMask requires requesting permission to connect users accounts
		await provider.send("eth_requestAccounts", []);
		// The MetaMask plugin also allows signing transactions to
		// send ether and pay to change state within the blockchain.
		// For this, you need the account signer...
		let signer = provider.getSigner()
		console.log('Connected MetaMask!', provider)
	}
// Look up the current block number

</script>

<main>
	<div>
		<button on:click={getSigner}>Connect MetaMask</button>
	</div>
	<h2>
		The name of the token is: <h1>'{name}'</h1> and the symbol is <h1>'{symbol}'</h1>
	</h2>
	<div>
		<input bind:value={amount} placeholder="Set amount of COO to buy">
		<button on:click={sendTokens}>Buy Tokens</button>
	</div>
</main>

<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}

	h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>