# Secret Network Notes

* Progress
	* [X] Introduction
	* [ ] Development

* Help
	* Docs
    * Secret docs https://github.com/SecretFoundation/docs
		* Secret.js docs https://secretjs.scrt.network/
		* Secret Python SDK - https://github.com/secretanalytics/secret-sdk-python
		* Rust Docs
      * Secret Network Toolkit
        * [ ] Storage - https://docs.rs/secret-toolkit-storage/0.10.0/secret_toolkit_storage/index.html
			* CosmWasm
				* [ ] https://docs.rs/cosmwasm-std/latest/cosmwasm_std/
				* [ ] https://docs.cosmwasm.com/docs/1.0/
            * Rust CosmWasm - https://docs.rs/cosmwasm-std/latest/cosmwasm_std
  * Guides
		* [ ] Snakepath whitepaper - https://uploads-ssl.webflow.com/632b43ea48475213272bcef4/632dd73d6dfc1b0cba06bbd6_Snakepath_whitepaper.pdf
    * [ ] Architecture of Secret - https://docs.scrt.network/secret-network-documentation/development/example-contracts/guides-tutorials
    * [ ] In-depth guide to Secret contracts - https://docs.scrt.network/secret-network-documentation/development/example-contracts/guides-tutorials
    * [ ] Run your own Relayer at the step "configuring the relayer" https://docs.scrt.network/secret-network-documentation/confidential-computing-layer/ethereum-evm-developer-toolkit/basics/cross-chain-messaging/secretpath/how-to-deploy-secretpath-on-your-chain
  * Examples
		* VRF Developer Tutorial - https://docs.scrt.network/secret-network-documentation/confidential-computing-layer/ethereum-evm-developer-toolkit/usecases/vrf/vrf-developer-tutorial#request-random-numbers
			* encrypted payloads in EVM Gateway - https://docs.scrt.network/secret-network-documentation/confidential-computing-layer/ethereum-evm-developer-toolkit/usecases/vrf/using-encrypted-payloads-for-vrf
		* Key-Value Store Developer Tutorial - https://docs.scrt.network/secret-network-documentation/confidential-computing-layer/ethereum-evm-developer-toolkit/usecases/storing-encrypted-data-on-secret-network/key-value-store-developer-tutorial
			* Note: Uses submit.js, similar to this https://github.com/writersblockchain/secretpath-ballz/blob/master/src/functions/submit.js#L32
    * https://github.com/SecretFoundation/Secretpath-tutorials
			* https://github.com/SecretFoundation/Secretpath-tutorials/blob/master/encrypted-payloads/evm-contract/contracts/Gateway.sol#L418
    * https://github.com/SecretSaturn/SecretPath
      * Gateway TNLS
        * https://github.com/SecretSaturn/SecretPath/blob/main/TNLS-Gateways/public-gateway/src/Gateway.sol
      * Relayer 
    * https://github.com/writersblockchain/secretpath-ballz 
    * https://github.com/writersblockchain/aes-encrypt
    * Sealed Bid Auction Walkthrough
      * https://darwinzero.medium.com/creating-my-first-secret-contract-on-secret-network-scrt-db0d04597051
      * https://github.com/baedrik/SCRT-sealed-bid-auction/blob/master/WALKTHROUGH.md
    * https://github.com/scrtlabs/examples
		* https://github.com/secretchaingirl/secret-contracts-guide
    * Hackathon submissions
      * https://taikai.network/ethrome/hackathons/ethrome-24/projects
      * Uses Aztec Noir https://github.com/MihRazvan/SHIELDSPACE-ETHRome
      * https://github.com/ethdam24-quadratic/secret-repo
		* Tests and Integration Tests
			* https://github.com/CosmWasm/cosmwasm/blob/main/contracts/hackatom/src/contract.rs
	* Q&A
		* Meetings
			* [ ] Secret Network - Weekly Dev calls Mondays 5pm UTC Discord - https://discord.com/invite/secret-network-360051864110235648
		* [ ] Forum https://forum.scrt.network/
		* [Other](https://docs.scrt.network/secret-network-documentation#join-the-community)
    * Discord https://scrt.network/discord
		* Telegram t.me/SecretNetworkDevs
  * Resources
    * Block Explorer
      * https://testnet.ping.pub/secret
    * Gateways Deployed https://docs.scrt.network/secret-network-documentation/confidential-computing-layer/ethereum-evm-developer-toolkit/supported-networks/evm/evm-testnet-gateway-contracts
    * Secret Network repo - https://github.com/SecretFoundation/SecretNetwork
    * Secret Network Testnet
      * Secret compatible wallet: Keplr - https://keplr.crunch.help/en/getting-started/installing-keplr-wallet
      * Faucet - pulsar-3 testnet faucet - https://faucet.pulsar.scrttestnet.com/
      * Connect to Testnet connect wallet to pulsar-3 https://keplr-connect-pulsar3.vercel.app/
        * https://connect.pulsar.scrttestnet.com
        * https://rpc.pulsar.scrttestnet.com
        * https://testnet.ping.pub/secret/
          ```
          Contract Address Testnet Chain
          SSCRT
          secret1gvn6eap7xgsf9kydgmvpqwzkru2zj35ar2vncj
          Pulsar-3
          ```

* Secret network
	* Secret network is a Layer 1 sovereign in Cosmos ecosystem built with Cosmos SDK
	
	* Relayers are off-chain actors that ensure "physical" connection between two chains using light clients, monitoring the state of the two interconnected chains and verifying incoming messages for intentions to send a transaction on a chain and then relaying the data and submitting its proof of commitment (a commit of the hash of the data packet in its own state machine) to the other chain, where this IBC is Byzantine resistant due to this proof validation by the light client. IBC security is mostly done by light clients that verify these proofs of commitments and the state of the two interconnected blockchain. If a relayer were malicious, the packet would be rejected by the counterparty chain because the proof would be invalid (because light client and relayers are independent).
	
	* Inter-Blockchain Communication Protocol (IBC) is responsible for interconnecting heterogeneous blockchains by relaying data packets between arbitrary state machines (i.e application blockchains). It has two layers that are wrapped up in a "light client" and relayers are external components for passing messages through blockchains:
		* Transport layer (IBC/TAO) - provides infrastructure for establishing secure connections and data packets authentication between chains
		* Application layer (IBC/APP) - defines how data packets should be packaged and interpreted by sending and receiving chains
	IBC has native security by avoiding trusting third parties compared to existing bridge solutions that may even require a multisig. Relayers need to be operating with ports open and successful authentication for message passing.
	IBC analogy to internet:
		* Channel -> IP connection
		* IBC portID -> IP port
		* IBC channelID -> IP address
	IBC allows for token transfer, multi-chain smart contracts, and interchain interaction between accounts on source and destination chains. This allows other Cosmos chains to store and manipulate private data (even private keys) on Secret Network from the comfort of their own chain.

	* Tendermint interactions (e.g. proving tokens locked on one chain before giving voucher on another chain)
		* Cosmos SDK allows faster way to interact with Tendermint using plugins rather than directly interacting with Tendermint core from the application layer using ABCI protocol
	
	* Secret contract interactions
		* binaries are executed by validators and publicly visible to them 
		* read/write from state at rest from Tendermint is encrypted 
		* transactions that are valid through `CheckTx` ABCI message are processed by node local cache mempool including encrypted data inputs
		* decryption and requested contract functions executed inside Trusted Execution Environment (TEE)
		* outputs encrypted

	* CosmWasm
		* Modular framework for writing secure smart contracts in Rust for use in any blockchain built with the Cosmos SDK (e.g. Secret Network). CosmWasm smart contracts run securely inside WebAssemby (WASM) virtual machine (VM), where WASM acts as an intermediate language compiler of the VM.
		* CosmWasm smart contracts are a set of rules that describe how parties interact with each other and are stored on-chain where they may be executed by that network.
		* CosmWasm wraps Rust binaries as secure smart contracts

	* Encryption Protocols
		* Asymmetric cryptography is used for achieving consensus and sharing secrets between nodes and users, whenever a transaction is sent from the user to a Secret Network contract. e.g.
			* Elliptic-Curve Diffie-Hellman (ECDH) key exchange mechanism (x25519) function for generating public / private key pairs
				* e.g. https://docs.scrt.network/secret-network-documentation/introduction/secret-network-techstack/privacy-technology/encryption-key-management/key-derivation-and-encryption-techniques#elliptic-curve-diffie-hellman
		* Symmetric cryptography is used for input/output encryption with users of Secret Contracts, as well as internal contract state encryption. e.g. 
			* RFC 5297: Advanced Encryption Standard Synthetic Initialization Vector (SIV) (AES-128-SIV) symmetric encryption scheme - a symmetric block cipher standardized by NIST with 128 bit long keys and fixed data block size of 16 bytes https://tools.ietf.org/html/rfc5297
				* e.g. https://docs.scrt.network/secret-network-documentation/introduction/secret-network-techstack/privacy-technology/encryption-key-management/key-derivation-and-encryption-techniques#aes-128-siv-rijndael
			* HMAC-based Key Derivation Function (HKDF-SHA256) function for deterministic key derivation - https://datatracker.ietf.org/doc/html/rfc5869#section-2
				* e.g. https://docs.scrt.network/secret-network-documentation/introduction/secret-network-techstack/privacy-technology/encryption-key-management/key-derivation-and-encryption-techniques#hkdf-sha256

	* Transaction Encryption
		* Transactions initiated by network users derive an Input Key Material (IKM) from their own private key and the network-generated public key, the network derives the same IKM using the user's public key and the network-generated private key. An encryption key for the transaction is then derived inside the TEE from the IKM, the salt, and a random number generated with the consensus seed. The encryption key is used to encrypt the input specific to this transaction. Only the protocol and the user signing the transaction have access to the encryption key, and therefore access to the input, output, and state related to this specific smart contract computation.
			* e.g. https://docs.scrt.network/secret-network-documentation/introduction/secret-network-techstack/privacy-technology/encryption-key-management/transaction-encryption

	* Contract Encryption
		* `consensus_state_ikm` An input keyring material (IKM) for HKDF-SHA256 is used to derive encryption keys for contract state - https://docs.scrt.network/secret-network-documentation/introduction/secret-network-techstack/privacy-technology/encryption-key-management/bootstrap-process
			```
			consensus_state_ikm = hkdf({
			  salt: hkdf_salt,
			  ikm: consensus_seed.append(uint8(3)),
			}); // 256 bits
			```

		* `consensus_callback_secret` A curve25519 private key is used to create callback signatures when contracts call other contracts - https://docs.scrt.network/secret-network-documentation/introduction/secret-network-techstack/privacy-technology/encryption-key-management/bootstrap-process
			```
			consensus_state_ikm = hkdf({
			  salt: hkdf_salt,
			  ikm: consensus_seed.append(uint8(4)),
			}); // 256 bits
			```

		* Contract can call 3 different functions. `field_name` remains constant between contract calls. Detailed code shown here https://docs.scrt.network/secret-network-documentation/introduction/secret-network-techstack/privacy-technology/encryption-key-management/contract-state-encryption#id-3.-callback-function-logic
			* `write_db(field_name, value)`
			* `read_db(field_name)`
			* `remove_db(field_name)`

		* Contract Key
			* `contract_key` is the encryption key for the contract state, concatenating these two values so two contracts with same code are unique, protect from malicious node runners, and where every contract has its own unforgeable encryption key. Each time a contract execution is calledthe `contract_key` us send to the enclave and verification occurs to proove it is genuine as shown here https://docs.scrt.network/secret-network-documentation/introduction/secret-network-techstack/privacy-technology/encryption-key-management/contract-state-encryption#id-2.-at-execution-share-contract_key-with-enclave
				* `signer_id`
				* `authenticated_contract_key`

	* Contract Queries
		* Secret contracts are an altered version of the CosmWasm Rust based smart contract framework. Secret contracts are written in Rust and compile to a Wasm binary that is then run by the Wasmd module of the cosmos SDK. Secret executions are done inside the secure enclave requiring additional data verification. Queries of the Secret contract state or contract execution are permissioned to only the signer of the transaction themselves. Contract state queries requiring opening up the VM in the enclave and are therefore more intensive to run than generic plaintext cosmos-sdk queries.
