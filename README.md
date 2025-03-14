# Roast Me - Hyperbolic x Succinct App
In **Roast Me**, you get roasted by `Hyperbolic's API` and generate a proof of it by `Succinct's SP1 zkVM`!

## Overview
This app combines:
- **Hyperbolic API**: Generates humorous, crypto-themed roasts.
- **Succinct SP1**: Creates zero-knowledge proofs to verify a username was roasted without revealing the roast itself.
- **Flask**: Powers the web frontend.
- **Node.js**: Manages the backend for proof generation.

---

## System Requirements
Generating proofs requires a good machine with good RAM. You can consider:
* Setting up Ubuntu via WSL on Windows using this [Guide](https://github.com/0xmoei/Install-Linux-on-Windows)
* Using a VPS

---

## Prerequisites
The proof generation might need a good pc resources, You can use a VPS server to  install it or install Ubuntu via WSL using this [guide](https://github.com/0xmoei/Install-Linux-on-Windows) on your windows
**Important:**
* After running each of these commands, follow the on-screen prompts to complete the installation.
* For example: In my enviorment, after installing one of them, it asks me to enter `source /$HOME/.bashrc` to verify the installation.

**1. Python**
```bash
sudo apt install python3 python3-pip
```

**2. Node.js and npm**
```bash
sudo apt-get update

curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -
sudo apt install -y nodejs

node -v
npm -v
```

**3. Rust and Cargo**
```bash
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```
It asks you to enter a command to add it `cargo` to your `shell`. In my environment, it was: `. "$HOME/.cargo/env"`

**4. Sp1 Toolchain(`succinct`)**
```bash
curl -L https://sp1up.succinct.xyz | bash
```
```
source /$HOME/.bashrc
```
```
sp1up
```

---

## Clone Repository
```bash
git clone https://github.com/0xmoei/RoastMe-SP1.git
cd RoastMe-SP1
```

---

## Hyperbolic API Key
The `app.py` file includes a placeholder API key for Hyperbolic. To use your own:
1. Sign up at [Hyperbolic](https://app.hyperbolic.xyz/) and get your **API key** in **Setting**.
2. Replace the `HYPERBOLIC_API_KEY` value in `app.py` directly using:
```bash
nano app.py
```

---

## Setting Up the Environment
### Install the SP1 Toolchain
The app uses Succinct's SP1 zkVM for zero-knowledge proofs. Install it with:
```bash
curl -L https://sp1up.succinct.xyz | bash
sp1up
```

---

## Configure the Rust Toolchain
Navigate to the `roast_proof` directory and set the appropriate Rust toolchain:
```bash
cd roast_proof
rustup override set succinct
cd ..
```

---

## Installing Dependencies
### Python Dependencies
Install the required Python packages for the Flask app:
```bash
pip install -r requirements.txt
```

---

### Node.js Dependencies
Install the backend dependencies:
```bash 
cd backend
npm install
cd ..
```

---

### Rust Dependencies
Build the Rust proof generation script:
```bash
cd roast_proof/script
cargo build --release
cd ../..
```

---

## Running the Application
Launch the Flask web frontend:
```bash
python3 app.py
```
This runs on `http://localhost:5000` or `http://vps-ip:5000` by default.

---

## Start the Node.js Backend
Open a new terminal, and launch the Node.js backend:
```bash
cd backend
node server.js
```
This should run on `http://localhost:3000` or `http://vps-ip:5000`.

---

## Access the App
Open your browser and navigate to `http://localhost:5000` or `http://vps-ip:5000`.

---

## Using the App
**1. Get Roasted:**
  - Enter your name in the input box.
  - Click "Roast me" to receive a crypto-themed roast generated by Hyperbolic’s API.

**2. Generate a Proof:**
  - After getting your roast, click "Prove (SP1)" to generate a zero-knowledge proof.
  - The proof confirms your name was processed (roasted) without revealing the roast content.
  - The proof result, including a hash, will appear below the roast.
  - The script generates and verifies the proof, saving it to `roast_proof.bin` in `RoastMe-SP1/roast-proof/script` directory
