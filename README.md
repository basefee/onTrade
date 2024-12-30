# onTrade

### Directly Backed Trading On-Chain: Real Assets, Real Security

Our project addresses a crucial gap in the current landscape of De-Fi on the blockchain. Traditional synthetic RWAs only mint tokens based on price feeds, creating an abstraction layer that does not connect directly to the underlying assets. Our solution takes a more direct approach by enabling RWAs that are directly backed by real assets.

By utilizing Gelato functions, our platform executes stock purchases off-chain, ensuring that the tokens you hold are genuinely backed by real stocks on the market. This enhances trust, transparency, and the overall value proposition of RWAs on-chain, effectively bridging the gap between traditional finance and blockchain technology.

#### Currently Deployed on EDUChain Sepolia and Supports the Following Stocks:
- [AAPL](https://edu-chain-testnet.blockscout.com/address/0xB084e51B2DE5aDf85AF9E20fC5588488354bA1a4)
- [AMZN](https://edu-chain-testnet.blockscout.com/address/0x5c7cC8C50ABCAFe4F246D7Bf07800C38cfC7eD63)
- [NASDAQ](https://edu-chain-testnet.blockscout.com/address/0x94C1863a76407F10b077e057C2FF742DF4200d21)
- [S&P500](https://edu-chain-testnet.blockscout.com/address/0xDB01b6391b244C3Fd1D5677ab67d613C659F0c46)

#### The flow of the Dapp is as follows:-
- Approve and deposit the suffcient amount of USDT to the contract.
- Select the stock and the correct amount.
- Redstone's core price feed wraps the transaction with its oracle data.
- After calling the `buyRStock` function, a `BuyRequest` gets emmitted.
- The event is picked up by Gelato's web3-function, which calls the Alpaca API to buy the respective stock in the exchange.
- It then excutes the `mintRStock` function, which mints the directly backed ERC20 of the RWA on-chain.
- In a similar manner, it can be sold and the USDT can be withdrawn. 

![plot](public/image.png)

This repository includes the contract and Web3 functions, which need to be deployed separately for testing.

### For Contract:
```
$ forge init // Move the contract to foundry directory
$ forge install redstone-finance/redstone-oracles-monorepo --no-commit
$ forge install OpenZeppelin/openzeppelin-contracts@v4.9.5 --no-commit
```

### For web3-function
```
$ git clone https://github.com/gelatodigital/web3-functions-sdk.git
// Move the stocks and updates folder to web3-function
$ npx hardhat w3f-deploy stocks // to get the typescript function IPFS CID
```

### For web-app
```
$ npm i
$ npm run dev
```


### Environment Variables:
Environment variables are needed for Web3 functions as they use the [Alpaca API](https://app.alpaca.markets/signup) for stock trading.

#### Gelato Deployed Functions:
- [MarketAAPL](https://app.gelato.network/functions/task/0x1a7bd34a35be8c1d28b272ae1d03c34cd6e6870f2728034f7ec90453b9f0c54a:656476)
- [BuyAAPL](https://app.gelato.network/functions/task/0x6af6c86865bbb9a9840fca5acd94823281be1834912fcbca49669e25956ae756:656476)
- [SellAAPL](https://app.gelato.network/functions/task/0x302deddd8c891b4620b7e4f5a75b426766723451309f0ec21af84071f7394861:656476)
- [MarketAMZN](https://app.gelato.network/functions/task/0xfc23dcba6c872af226b561ba489a5cbc304e8cf9fdd1146b83ab6884c6888747:656476)
- [BuyAMZN](https://app.gelato.network/functions/task/0x99c390435da4fed9d0f78eb2c789881238fe59f9d61a62abbfd10049ca610a7a:656476)
- [SellAMZN](https://app.gelato.network/functions/task/0x5b4f80e5f393b1af79b3a9f277535654187f3f8c74b2fb7caf810f115e2ab6d9:656476)
- [MarketNASDAQ](https://app.gelato.network/functions/task/0x34d21448395fd59dfb1cf79d1277dcaa6a6941e2597c1778312823a303152e9a:656476)
- [BuyNDAQ](https://app.gelato.network/functions/task/0xd498debbeb02798ec8e6ce90f82acdb861e8b64638a2ed4fb8330aa85666a3c8:656476)
- [SellNDAQ](https://app.gelato.network/functions/task/0x2789a73c6a5f52b78dce27fd0f969b4d5f5f628987ddc84ef8d0afd5a01a86a0:656476)
- [MarketSPY](https://app.gelato.network/functions/task/0x3a32435c120a49b60bb40c733ed95b7aecad23b696c74d21e3b78b450a4335e9:656476)
- [BuySPY](https://app.gelato.network/functions/task/0x028b0378a870186f1335675349bcef56882c30e628a196578de2a745ab17d002:656476)
- [SellSPY](https://app.gelato.network/functions/task/0x8d2541e30f994ae2a13abfc7c98b7fc291fdf39dd6125befa72d93cb40d41321:656476)

- **Market Function**: Manages pausing and unpausing of the contract based on market status.
- **Buy Function**: Listens for `BuyRequest` events, interacts with the Alpaca API to purchase stock, and mints the corresponding ERC20 token to the trader.
- **Sell Function**: Listens for `SellRequest` events, interacts with the Alpaca API to sell stock, and burns the corresponding ERC20 token from the trader.

### [Demo Video]()

## Built during EDUChain X Hackquest Mega Co-Learning Camp - Bangalore
