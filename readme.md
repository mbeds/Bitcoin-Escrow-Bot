# Bitcoin Escrow Telegram Bot

A Python-based Telegram bot designed to facilitate secure Bitcoin escrow transactions between a buyer and a seller. The bot automates the creation of unique HD Wallets for every deal, monitors balances, and handles the distribution of funds (including service fees).

## 🚀 Features

* **Automated Wallet Generation:** Creates a unique Bitcoin HD Wallet (BIP32/44) for every transaction using `bitcoinlib`.
* **Role-Based Workflow:** Distinct command paths for Buyers and Sellers to ensure all necessary data (like receiving addresses) is collected.
* **Database Integration:** Uses MongoDB to persist deal details, escrow IDs, and wallet seeds.
* **Admin Logging:** Automatically forwards sensitive deal data (seeds/IDs) to a private admin channel for moderation and backup.
* **Fee Management:** Calculates and deducts a configurable percentage fee (default 5%) before releasing funds.
* **Real-time Balance Checks:** Allows users to scan the blockchain for the current balance of the escrow wallet.

## 🛠 Tech Stack

* **Language:** Python 3
* **API Wrapper:** `python-telegram-bot` (v12.x or legacy)
* **Blockchain:** `bitcoinlib`
* **Database:** MongoDB (`pymongo`)
* **Environment:** Linux/Unix (recommended)

---

## 📋 Prerequisites

Before running the bot, ensure you have the following installed:

1.  **MongoDB:** Running locally on the default port `27017`.
2.  **Bitcoinlib Dependencies:** You may need `libssl-dev` and `python3-dev` on your system to compile `bitcoinlib`.
3.  **Telegram Bot Token:** Obtain one from [@BotFather](https://t.me/botfather).

---

## ⚙️ Installation & Setup

1.  **Clone the repository:**
    ```bash
    git clone https://github.com/yourusername/btc-escrow-bot.git
    cd btc-escrow-bot
    ```

2.  **Install Python dependencies:**
    ```bash
    pip install python-telegram-bot==12.8 bitcoinlib pymongo
    ```

3.  **Configure the Script:**
    Open the script and update the following variables:
    * `TOKEN`: Your Telegram Bot API Key.
    * `escrow_channel`: The ID of your private Telegram channel for moderation.
    * `GCTM_Multisig_Wallet`: The Bitcoin address where your service fees will be sent.

4.  **Run the Bot:**
    ```bash
    python bot_script.py
    ```

---

## 📖 How It Works (Usage)

1.  **Initiation:** The buyer starts the process by typing `/start` followed by `/buyer @username`.
2.  **Seller Setup:** The seller provides their identity and destination address: `/seller @username <BTC_ADDRESS>`.
3.  **Escrow Generation:** Run `/generate`. The bot creates a new wallet, provides the address to the users, and saves the seed to the database.
4.  **Funding:** The buyer deposits the agreed-upon Bitcoin into the generated Escrow Wallet.
5.  **Release:** Once the buyer is satisfied, they run `/release`. The bot:
    * Calculates the network fee and service fee.
    * Sends the remaining balance to the seller's address.
    * Sends the service fee to the Admin wallet.

---

## ⚠️ Security Note

> **Disclaimer:** This bot handles raw private keys and mnemonic seeds. Ensure your MongoDB instance is secured with a password and not exposed to the public internet. The `escrow_channel` should be strictly private, as it contains the "keys to the castle" for every transaction.

## 📄 License

This project is for educational purposes. Please review local regulations regarding cryptocurrency escrow services before deployment.
