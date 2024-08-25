# ZK TLSNotary P2P Order Smart Contract

## Overview

This smart contract implements a peer-to-peer (P2P) order system for cryptocurrency trading, leveraging Zero-Knowledge TLS Notary proofs for secure and private transactions. The contract supports partial order filling, allowing for flexible trading options.

## Features

- Create sell orders for cryptocurrencies
- Support for partial order filling
- ZK TLS Notary proof verification for secure transactions
- Cancel orders (including partially filled orders)
- Retrieve user orders

## Contract Structure

The main components of the contract are:

1. `Order<CoinType>`: Struct representing an order
2. `P2POrderbook<CoinType>`: Struct managing the orderbook
3. Key functions for order management and execution

## Key Functions

### `initialize<CoinType>(account: &signer)`
Initializes the P2P orderbook for a specific coin type.

### `create_order<CoinType>(...)`
Creates a new sell order with the following parameters:
- `fiat_currency`: The fiat currency for payment
- `total_crypto_amount`: Total amount of cryptocurrency to sell
- `fiat_price_per_crypto`: Price per unit of cryptocurrency in fiat
- `payment_method`: Accepted payment method
- `min_crypto_amount`: Minimum amount that can be purchased in a single transaction

### `cancel_order<CoinType>(account: &signer, order_id: u64)`
Cancels an open or partially filled order.

### `fill_order<CoinType>(account: &signer, order_id: u64, crypto_amount: u64, zk_proof: vector<u8>)`
Fills an order (partially or fully) with ZK proof verification.

### `get_user_orders<CoinType>(user: address): vector<u64>`
Retrieves all order IDs associated with a user.

## Order Statuses

- `ORDER_STATUS_OPEN`: Newly created order
- `ORDER_STATUS_PARTIALLY_FILLED`: Order that has been partially filled
- `ORDER_STATUS_FILLED`: Completely filled order
- `ORDER_STATUS_CANCELLED`: Cancelled order

## Usage

1. Initialize the orderbook for a specific coin type.
2. Sellers create orders specifying the total amount, price, and minimum fill amount.
3. Buyers fill orders by providing the amount they want to purchase and a ZK proof of payment.
4. The contract verifies the ZK proof and updates the order status accordingly.
5. Sellers can cancel unfilled or partially filled orders at any time.

## ZK Proof Verification

The `verify_zk_proof<CoinType>` function is a placeholder that needs to be implemented with the specific ZK TLS Notary proof verification logic. This function should verify:

1. The buyer has made the fiat payment
2. The proof demonstrates knowledge of the TLS session key
3. The payment details match the order and the crypto amount being purchased

## Security Considerations

- Ensure proper implementation of the ZK proof verification logic.
- Implement secure fund locking and transfer mechanisms (not included in this contract).
- Consider adding time limits or expirations for orders.
- Implement proper access controls and ensure only authorized actions are permitted.

## Testing

Use the `initialize_for_testing<CoinType>` function to set up the contract in a test environment.

## Future Improvements

- Implement a dispute resolution mechanism.
- Add support for buy orders in addition to sell orders.
- Integrate with a price oracle for real-time price updates.
- Implement an order matching engine for automatic order filling.

## License