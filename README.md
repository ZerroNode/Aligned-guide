# Aligned-guide

## Step 1: Install Aligned

First, you’ll need to install the Aligned toolset to interact with the testnet. This will allow you to submit and verify proofs.

To install, run the following command in your terminal:

```
curl -L https://raw.githubusercontent.com/yetanotherco/aligned_layer/main/batcher/aligned/install_aligned.sh | bash
```

If you encounter any issues or need to update your installation, simply run the command again.

## Step 2: Download Proof Files

Next, you’ll need to download a pre-generated SP1 proof and its associated ELF file (this contains the necessary program logic to verify the proof). Run the command below to get the files:

```
curl -L https://raw.githubusercontent.com/yetanotherco/aligned_layer/main/batcher/aligned/get_proof_test_files.sh | bash
```

These files will be essential for submitting proofs to Aligned.

## Step 3: Submit the Proof

Now that you have the proof files, it’s time to submit them to the Aligned network. Run the following command to send your proof:

```
rm -rf ~/.aligned/aligned_verification_data/ &&
aligned submit \
--proving_system SP1 \
--proof ~/.aligned/test_files/sp1_fibonacci.proof \
--vm_program ~/.aligned/test_files/sp1_fibonacci.elf \
--aligned_verification_data_path ~/.aligned/aligned_verification_data \
--conn wss://batcher.alignedlayer.com \
--rpc https://ethereum-holesky-rpc.publicnode.com \
--batcher_addr 0x815aeCA64a974297942D2Bbf034ABEe22a38A003
```
This command sends your proof to the Aligned network via the EigenLayer and retrieves results from the Ethereum Holesky testnet. You should see a response like this:

```
[2024-06-17T22:06:03Z INFO  aligned] Proof submitted to aligned. See the batch in the explorer:
    https://explorer.alignedlayer.com/batches/0x8ea98526e48f72d4b49ad39902fb320020d3cf02e6506c444300eb3619db4c13
```

You can use the explorer link to track your proof submission status in real-time.

## Step 4: Verify the Proof On-Chain

After submitting the proof, you can check its verification status on-chain by running the following command:

```
aligned verify-proof-onchain \
--aligned-verification-data ~/aligned_verification_data/*.json \
--rpc https://ethereum-holesky-rpc.publicnode.com \
--chain holesky
```

You’ll receive one of two responses:

Proof verified: Your proof has been successfully included in the batch and verified on-chain.

Proof not included: Your proof was not verified in the current batch.

Bonus: Use Aligned in Your Own Smart Contract

If you want to integrate Aligned into your own project, you can perform a static call to the Aligned contract in your smart contract. The Aligned documentation provides a Caller Contract example to help you get started.
