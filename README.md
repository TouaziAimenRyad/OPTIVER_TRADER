# Optiver Trading Bot (HackUPC 2023)

This repository contains a Python script for an automated trading bot developed for the Optiver challenge at HackUPC 2023. The bot is designed to trade the "C2_GREEN_ENERGY_ETF" instrument, along with its constituent stocks "C2_SOLAR_CO" and "C2_WIND_LTD", by implementing a spread trading and market-making strategy.

## Project Overview

The trading bot aims to:

-   Exploit arbitrage opportunities by trading the ETF against its underlying stocks.
-   Provide liquidity to the market through market-making.
-   Manage positions and liquidate when necessary.
-   Maintain a delta-neutral position.

## Files

-   `optiver_trading_bot.py`: Python script containing the trading bot logic.
-   `README.md`: This file, providing an overview of the project.

## Dependencies

-   optibook (Optiver API client)
-   logging
-   time
-   typing
-   functools

To install the required dependencies, ensure you have the Optiver API client installed.

## Usage

1.  **Clone the repository:**

    ```bash
    git clone [repository URL]
    cd [repository directory]
    ```

2.  **Run the Python script:**

    ```bash
    python optiver_trading_bot.py
    ```

3.  **Ensure you have the Optiver API credentials configured correctly.**

## Trading Logic

The script implements the following trading strategies:

-   **Spread Trading:**
    -      Calculates the spread between the ETF and the combined price of its constituent stocks.
    -      Executes trades when the spread deviates from predefined limits, aiming to profit from arbitrage.
    -      Uses `buy_high` and `sell_low` functions to place orders at slightly improved prices.
-   **Market Making:**
    -      Provides liquidity by placing bid and ask orders for the ETF.
    -      Adjusts order prices based on market conditions and the calculated spread.
    -   Uses the `market_making` function to place limit orders.
-   **Liquidation:**
    -      Monitors positions and initiates liquidation when predefined limits are exceeded.
    -      Uses `liquidate` function to close out positions.
-   **Delta Neutral:**
    -   Uses the function `delta_neutral` to ensure that any trade that happened in the ETF is replicated in the underlying securities.
    -   This is done by monitoring the trades that happen in the ETF, and if a buy trade happens, the underlying securities are sold, and vice versa.
-   **Position Balancing:**
    -   Uses the `balance` function to maintain equal positions across the ETF and its constituent stocks.
    -   Adjusts positions by buying or selling the underlying stocks as needed.

## Functions

-   `get_spread(pb)`: Calculates the bid-ask spread for a given price book.
-   `get_basket_stocks_spread(e)`: Calculates the spread between the ETF and the combined price of its constituent stocks.
-   `buy_high(e, instrument_id, vol, pb)`: Places a buy order at a slightly higher price.
-   `sell_low(e, instrument_id, vol, pb)`: Places a sell order at a slightly lower price.
-   `spread_trade(e)`: Executes spread trading logic.
-   `liquidate(e)`: Executes liquidation logic.
-   `balance(e)`: Balances positions across instruments.
-   `market_making(e, d)`: Executes market-making logic.
-   `get_market_price(e, instrument_id)`: Retrieves the last traded price for an instrument.
-   `get_diffrence_to_buy(e)`: Retrieves the difference between the ETF and the combined price of the stocks.
-   `get_price_book(e)`: Retrieves the price books for the instruments.
-   `sell_market_price(e, instrument_id, vol, order_type)`: Places a sell order at the market price.
-   `buy_market_price(e, instrument_id, vol, order_type)`: Places a buy order at the market price.
-   `delta_neutral(e, depth)`: Ensures delta neutrality by replicating ETF trades in underlying stocks.
-   `hack_out(e)`: Closes out all positions.
-   `check_connection(e)`: Checks and reconnects to the exchange if necessary.
-   `main()`: Main execution loop.

## Notes

-      This bot is provided as an example and may not be profitable in all market conditions.
-      Adjust the trading parameters and logic to suit your trading strategy and risk tolerance.
-      Ensure you understand the Optiver API and the risks associated with automated trading.
-   The `hack_out` function is used to close all positions at the end of the competition.
-   The trading logic is designed to be robust against disconnections and errors.
