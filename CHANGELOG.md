### 2024-10-24

- network fee api changes:
    
    1. Added transfer_with_native_token information for supported payout cryptos. Amount is the volume of crypto will be converted to native token, Currency is the symbol of the native token.
    ```
    {
      "id": "<string>",
      "destination_amount": "<string>",
      "destination_currency": "<string>",
      "destination_network": "<string>",
      "destination_network_description": "<string>",
      "destination_transaction_fee_fixed": "<string>",
      "destination_transaction_fee_percentage": "<string>",
      "destination_transaction_fee_type": "<string>",
      "destination_transaction_fee_currency": "<string>",
      "destination_network_fee": "<string>",
      "destination_network_fee_currency": "<string>",
      "destination_network_fee_monetary": "<string>",
      "transfer_with_native_token": {
        "amount": "<string>",
        "network": "<string>",
        "currency": "<string>"
      }
    }
    ```

    example of transfer native token in etherum network:
    ```
    "transfer_with_native_token": {
        "amount": "500",
        "network": "etheruem",
        "currency": "ERCUSDC"
    }
    ```

    2. Added following fields in the destination_network_details
    ```
    "destination_transaction_fee_fixed": "<string>",
    "destination_transaction_fee_percentage": "<string>",
    "destination_transaction_fee_type": "<string>",
    "destination_transaction_fee_currency": "<string>",
    ```
    destination_transaction_fee_type: platform fee type, either charge in fixed amount or charge percentage of the transaction volume. 

    if it's fixed, look at the amount in "destination_transaction_fee_fixed"

    if it's percentage, look at the number in destination_transaction_fee_percentage

    example: IMXUSDC payout is charged in percentage will be the following:
    ```
    "destination_transaction_fee_fixed": null,
    "destination_transaction_fee_percentage": "0.005",
    "destination_transaction_fee_type": "percentage",
    "destination_transaction_fee_currency": "IMXUSDC",
    ``` 

- create payout api changes: 
    
    Added transfer_with_native_token option, client can set transfer_with_native_token to true, to convert portion of crypto to network's native token and send to the receiver.
    ```
    PayoutCreateParams payoutParams =
                PayoutCreateParams
                        .builder()
                        .setAmount("2000")
                        .setCurrency("USDC")
                        .setDescription("withdraw #1234")
                        .setCustomer(customerParams)
                        .setTransferNativeToken(true)
                        .build();
    ```

- payout object changes:
  
  Added following new fields in destination_network_details
  ```
    "destination_transaction_fee_fixed": "<string>",
    "destination_transaction_fee_percentage": "<string>",
    "destination_transaction_fee_type": "<string>",
    "destination_transaction_fee_currency": "<string>",
  ```
  