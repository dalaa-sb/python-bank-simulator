# 🏦 Central D Bank – Python Banking Simulator

A command-line banking simulator that lets two users open accounts in different currencies, then deposit, withdraw and transfer money between them. It focuses on secure data handling, live currency conversion and simple AI features for spotting unusual transactions.

> ⚠️ Educational project. Don't use it with real money or real personal data. See [DISCLAIMER.md](DISCLAIMER.md).

---

## Features

- **PIN login** with bcrypt hashing (PINs are never stored in plain text)
- **Encrypted storage**: balances and transaction logs are encrypted with Fernet before being saved to SQLite
- **Multi-currency accounts**: USD, EUR, GBP and AED, with live exchange rates and a fallback to stored rates when offline
- **Fraud flagging**: an Isolation Forest model flags unusual transaction amounts
- **AI insights (optional)**: with an OpenAI API key, the app explains flagged transactions and gives short balance tips
- **Transfer suggestions (experimental)**: a small reinforcement learning demo built with Stable-Baselines3
- **Rate limiting** on account actions and **input validation** on names, amounts and currencies

## Tech stack

Python · SQLAlchemy · SQLite · cryptography (Fernet) · bcrypt · scikit-learn · OpenAI API · Stable-Baselines3 · Gymnasium

---

## Getting started

### 1. Clone the repo

```bash
git clone https://github.com/dalaa-sb/python-bank-simulator.git
cd python-bank-simulator
```

### 2. Install dependencies

Python 3.9 or higher is recommended.

```bash
pip install -r requirements.txt
```

### 3. Set up your keys

Copy the example file:

```bash
cp .env.example .env
```

Generate an encryption key and paste it into `.env` as `ENCRYPTION_KEY`:

```bash
python -c "from cryptography.fernet import Fernet; print(Fernet.generate_key().decode())"
```

Adding an `OPENAI_API_KEY` is optional. Without it, everything still works and the AI insights are simply skipped.

### 4. (Optional) Customize the config

The app reads `config_sample.json` by default. To change the fallback exchange rates or the fraud model's sample data, copy it to `config.json` and edit that copy.

### 5. Run it

```bash
python bankSimulator.py
```

---

## How it works

1. Create two accounts, each with a name, base currency, starting balance and 4-digit PIN.
2. Choose an account and log in with its PIN.
3. Check the balance, deposit, withdraw, or transfer to the other account in any supported currency.
4. Amounts are converted to the account's base currency automatically, and unusual amounts are flagged.

## Project structure

```
python-bank-simulator/
├── bankSimulator.py      # main app
├── config_sample.json    # fallback exchange rates and fraud model sample data
├── requirements.txt
├── .env.example          # template for your keys
└── DISCLAIMER.md
```

## What I'd improve next

- Train the fraud model on a larger, realistic transaction dataset
- Support more than two accounts
- Add unit tests and a simple web interface

---

Built by [Dalaa El Sabbagh](https://github.com/dalaa-sb)
