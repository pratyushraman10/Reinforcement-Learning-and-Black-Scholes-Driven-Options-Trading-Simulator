# Reinforcement Learning and Black-Scholes Driven Options Trading Simulator

## Overview
This project combines live options market data, the Black-Scholes option pricing model, and Reinforcement Learning (RL) to create an intelligent options trading simulator.
It fetches real option chain data using Yahoo Finance (yfinance), calculates theoretical option values, and uses a PPO (Proximal Policy Optimization) RL agent from Stable-Baselines3 to optimize a simple buy/hold/sell trading strategy within a custom OpenAI Gym environment.

## Features
- Fetches **live option chain data** for any stock ticker using `yfinance`
- Uses **implied volatility** directly from the options data instead of proxies
- Implements **Black-Scholes pricing** for European call options as a benchmark
- Custom **OpenAI Gym trading environment** tailored for a single option contract
- RL agent training with **Stable-Baselines3 PPO** to learn trading strategies
- Simple agent test run with cumulative reward output
- Fully modular — can be extended to Heston or Neural SDE pricing, multi-options, or complex portfolios

## Requirements
- Python 3.8+
- Packages:
    - yfinance
    - numpy
    - pandas
    - scipy
    - matplotlib
    - gym
    - stable-baselines3

Install dependencies:
pip install yfinance numpy pandas scipy matplotlib gym stable-baselines3


## How It Works
1. **Data Retrieval**
   - Pulls the latest option chain for a selected symbol and expiry date.
   - Filters for calls/puts with valid implied volatility and price.
   - Adds the latest underlying asset price to the dataset.

2. **Black-Scholes Pricing**
   - Computes theoretical European call option prices.
   - Compares with actual market prices for benchmarking.

3. **Custom Trading Environment**
   - Observations: Underlying price, strike price, time-to-expiry, implied vol, option price.
   - Actions: Hold (0), Buy (1), or Sell (2).
   - Reward: P&L from option price changes based on held position.

4. **Reinforcement Learning**
   - Trains a PPO RL agent to make trading decisions in the custom environment.
   - The agent learns patterns from historical step-by-step option price movements.

5. **Evaluation**
   - Runs the trained agent over the environment and reports cumulative reward.
   - Prints key steps and trading positions during simulation.

## Usage
1. Clone this repository and save the Python script (e.g., `main.py`).
2. Install dependencies listed above.
3. Run:
python main.py

4. The script will:
   - Display sample option chain data
   - Show theoretical vs market Black-Scholes prices
   - Train the RL model
   - Run a trading simulation and print total reward

## Possible Extensions
- Add **Heston Model** and **Neural SDE** pricing
- Handle **multiple options and portfolio strategies**
- Incorporate **transaction costs and slippage**
- Use richer state features for RL (Greeks, historical vol, macro data)
- Optimize reward functions for **Sharpe ratio** or **risk-adjusted returns**

## Disclaimer
This project is for **educational purposes only**.
It is **not financial advice** and should not be used for live trading.
Past simulated results do not guarantee future performance.
