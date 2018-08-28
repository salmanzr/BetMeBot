# BetMeBot
A decentralized betting platform that allows anyone to create predictions, bet on outcomes, and vote on the resolution of those bets.
The reason it is called BetMe 'bot' is because it's essentially an automated tool that provides "intelligent" smart contracts for betting.
Betting with outcomes resolved by voters staking ether is essential for creating a truly trust-less platform. Because all outcomes are
determined by voters, predictions no longer need to be resolved by an individual, and we can have prediction markets that don't have single 
"resolvers" that are single-points of failures, as in other existing prediction market platforms.

## Setup

1. Download source code:

```git clone https://github.com/salmanzr/betmebot```

2. Install packages:

```npm install```

3. Compile Smart Contracts:

```truffle compile```

4. Start Ganache or use Ganache-CLI:

```ganache-cli```

5. Run Tests:

```truffle test```

6. Close and re-open Ganache

7. Deploy Smart Contracts:

```truffle migrate```
After migration, look at the end in the console log for the address of the PredictionMarket contract. It will look like this "PredictionMarket: 0xb726b385d13e298250f035303f9c17fb3430db4c".
Copy this address and paste it into line 16 of [constants.js](https://github.com/salmanzr/betmebot/master/src/constants.js) for the Ganache network.

8.Build the app:

```npm run build```

9. Start UI server:

```npm run start```
The front-end app should start at http://localhost:3000
Make sure you are using Google Chrome with the Metamask extension configured to use a private network at http://127.0.0.1:8545

**Because the contracts for this project are also deployed on the Rinkeby testnet, you can go into [constants.js](https://github.com/salmanzr/betmebot/master/src/constants.js) and change the target live network variable to 'rinkeby' and simply call 
'npm run start' without using Ganache or Truffle.**


## Usage

### Create a prediction

1. Click "Create a New Prediction" on the bottom of the list, or click "Make Bet" at the top
2. Enter a statement, resolution date, and withdrawl period. You can type anything into the statement and use the defaults for the other two, then click "Create Prediction". Note that the "Explore Contract" links will only work when interacting with contracts on Rinkeby, not Ganache.

### Bet on a prediction

1. Click "View Bets" at the top and select the new prediction you just created.
2. You will see that you cannot bet nor vote on your prediction because you are the owner/creator. You can however call the "Stop all bets" kill switch to prevent anymore betting (this is a toggle, so you can stop/start betting again. To place a bet, you will have to switch your account in Metamask or make a new one (if you're using Ganache you can click 'create account' and it will be filled with ether). 
3. After switching accounts, you can see two buttons for whether or not the prediction will happen. Enter the amount of Ether you want to bet and then click one of the buttons. Refresh the page and you will see the net bet value at the top along with your bet history at the bottom.

### Vote on a prediction

1. You can only vote on a prediction after betting is closed and the contract State is 'closed'. The time this happens is specified when creating the prediction. Because in the previous steps we just used the default, let's make a new prediction but this time enter in a resolution datetime that is ~2 minutes from now. And make the withdrawl period just only 5 minutes.
2. After following the same process as above for betting, wait until the resolution time is reached. **Now, in order to move the contract to the next state of 'betting closed', attempt to bet one more time and click "accept" on the transaction even though it will fail.**  This will move the contract state to closed.
3. Now you will see options to vote on the outcome of the prediction. Enter the amount of ether you will stake on your vote and select the outcome you want to vote for. Refresh the page and you will see a net vote value at the top.

### Resolve a prediction

1. Switch your account in Metamask back to the original one and you will see the option to resolve this prediction. The owner has the ability to resolve a prediction himself, but if he truly believes in the democratic process, then he will select "Use votes", as you should. Refresh the page and you will see the status of the prediction is now 'Resolved for Yes'. 
2. Withdraw the fees you earned for creating this prediction by clicking "Withdraw x". If you refresh the page, you will see you cannot withdraw again.

### Purge the prediction

1. If you switch accounts back to the second one (the one you bet and voted with), you will see that you can withdraw your prize too. However, for this demo, let's say you forget to withdraw your winnings and now the withdrawl deadline of 5 minutes (as we specified at the time of creation) has passed. Now one would think this money is stuck in the contract, but that is incorrect. The owner of the prediction has the ability to purge and obtain any leftover funds of the prediction if any are left after the withdrawl deadline. Attempt to withdraw your funds after the deadline has passed and accept the transaction in Metamask even though it will fail. This will move the contract to the next final state.
2. Switch back to the original account and refresh the page. You will see the button to "Purge the contract". Click this to remove all funds from the Prediction contract and send it back to your account. Now the prediction is completey finished.

### Send me donations

1. If you enjoyed this dapp and want to fund my next ones, then feel free to send me Eth at betmebot.atethereum.eth, as linked at the bottom of the page. Hope you enjoyed!
