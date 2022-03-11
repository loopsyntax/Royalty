# Royalty
This guide is on Window

## Creating account

near create-account royalty.%NFT_CONTRACT_ID% --masterAccount %NFT_CONTRACT_ID% --initialBalance 25
set ROYALTY_NFT_CONTRACT_ID=royalty.%NFT_CONTRACT_ID%

cd nft-contracts

## Deploying on testnet
near deploy --wasmFile res/nft_simple.wasm --accountId %ROYALTY_NFT_CONTRACT_ID%

## Initialization and minting
near call %ROYALTY_NFT_CONTRACT_ID% new_default_meta "{\"owner_id\": \""%ROYALTY_NFT_CONTRACT_ID%"\"}" --accountId %ROYALTY_NFT_CONTRACT_ID%

near call %ROYALTY_NFT_CONTRACT_ID% nft_mint "{\"token_id\": \"approval-token\", \"metadata\": {\"title\": \"Approval Token\", \"description\": \"testing out the new approval extension of the standard\", \"media\": \"https://bafybeiftczwrtyr3k7a2k4vutd3amkwsmaqyhrdzlhvpt33dyjivufqusq.ipfs.dweb.link/goteam-gif.gif\"}, \"receiver_id\": \""%ROYALTY_NFT_CONTRACT_ID%"\", \"perpetual_royalties\": {\"jameswee1.testnet\": 2000, \"jameswee2.testnet\": 1000}}" --accountId %ROYALTY_NFT_CONTRACT_ID% --amount 0.1

near view %ROYALTY_NFT_CONTRACT_ID% nft_tokens_for_owner "{\"account_id\": \""%ROYALTY_NFT_CONTRACT_ID%"\", \"limit\": 10}"

## NFT payout
near view %ROYALTY_NFT_CONTRACT_ID% nft_payout "{\"token_id\": \"approval-token\", \"balance\": \"100\", \"max_len_payout\": 100}"