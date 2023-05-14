<p align="left" >
  <img width="240"  src="assets/logo.png">
</p>

# Motoko bootcamp 2023 for dapp-contest

This repository is meant to give [Svelte](https://svelte.dev/) developers an easy on-ramp to get started with developing decentralized applications (Dapps in short) for the Internet Computer blockchain. Dapps, also known as smart contracts are specialized software that run on a blockchain.

This template contains

- a Svelte frontend app under `src/frontend` to be hosted on-chain, with support for authentication using Internet Identity
- a Motoko dapp under `src/backend` to serve as a backend to the Svelte frontend

You can see a deployed version of this template here: https://zixfv-4yaaa-aaaam-aaatq-cai.ic0.app/

### What is the Internet Computer?

The Internet Computer is a novel blockchain that has the unique capability to serve web content while not requiring the end users to use a browser extension, such as Metamask.

Coupled with super fast execution the Internet Computer provides the worlds first truly user friendly Web 3.0 experience.

### What are canisters?

Dapps on the Internet Computer live in canisters, which are special smart contracts that run WebAssembly, and can respond to regular HTTP requests, among other capabilities.

This repository uses Svelte for the frontend running in the browser, and the backend dapp is written in Motoko, it serves as the business logic of your dapp.

You will build and deploy the following _canisters_:

- `backend` that is written in Motoko, and will hold the business logic of your dapp.
- `frontend` that is your regular Svelte app, transferred into a `frontend asset` canister.
- `internet_identity` that this repository uses as an authentication provider. It is written in Rust.

### What is Motoko?

Motoko is a new language designed for the Internet Computer. Easy to learn for JavaScript and Solidity developers. Created by the Motoko team at the DFINITY Foundation, led by WebAssembly co-creator Andreas Rossberg. To learn more about the language, check out the [SDK](https://smartcontracts.org/docs/language-guide/motoko.html).

### What is Internet Identity?

This starter template also includes integration with Internet Identity. Internet Identity is a new authentication framework similar to Github or Google login, but providing complete anonimity to the users. To learn more about Internet Identity check out the [documentation](https://smartcontracts.org/docs/ic-identity-guide/what-is-ic-identity.html).

## Security Considerations and Security Best Practices

If you base your application on this example, we recommend you familiarize yourself with and adhere to the [Security Best Practices](https://internetcomputer.org/docs/current/references/security/) for developing on the Internet Computer. This example may not implement all the best practices.

For example, the following aspects are particularly relevant for creating frontends:
* [Use a well-audited authentication service and client side IC libraries](https://internetcomputer.org/docs/current/references/security/web-app-development-security-best-practices#use-a-well-audited-authentication-service-and-client-side-ic-libraries)
* [Define security headers including a Content Security Policy (CSP)](https://internetcomputer.org/docs/current/references/security/web-app-development-security-best-practices#define-security-headers-including-a-content-security-policy-csp)
* [Don’t load JavaScript (and other assets) from untrusted domains](https://internetcomputer.org/docs/current/references/security/web-app-development-security-best-practices#dont-load-javascript-and-other-assets-from-untrusted-domains)

## Install dependencies

Make sure you have [node.js](https://nodejs.org/) installed.

### How to get this template

To clone this template without downloading the entire repository, run the following command:

```
git clone https://github.com/higayasuo/mbc2023-day6
```

### DFX

Install `dfx` by running

```
DFX_VERSION=0.12.0 sh -ci "$(curl -fsSL https://smartcontracts.org/install.sh)"
```

### Rust

To compile a local version of Internet Identity, you need to have [Rust](https://www.rust-lang.org/learn/get-started) installed.

Also install that target `wasm32-unknown-unknown` by running the command:

```
rustup target add wasm32-unknown-unknown
```

## Start the local replica

Open a new terminal window _in the project directory_, and run the following command to start the local replica. The replica will not start unless `dfx.json` exists in the current directory.

```
dfx start --background
```

When you're done with development, or you're switching to a different dfx project, running

```
dfx stop
```

from the project directory will stop the local replica.

## Build & run the dapp

Make sure you switch back to the project root directory.

First, install the frontend dependencies by running

```
cd src/frontend
npm install
cd ../..
```

To build and deploy the project run

```
dfx deploy
```

### Svelte frontend

You can serve the frontend in development mode like you normally develop a svelte app using the command

```
npm run dev
```

from the project root directory, it is not necessary to deploy it to the frontend canister during development.

## Deploying to the IC

To host the frontend and backend on the IC, you'll need to have some cycles available. Cycles pay for the execution of your app, and they are also needed to create canisters.

You can get $20 worth of cycles for free from the Cycles Faucet, if you have a GitHub account. To claim them, follow [this guide](https://smartcontracts.org/docs/quickstart/cycles-faucet.html).

You should have a canister running the cycles wallet on the IC at this point. The cycles wallet makes it easy to pay for canister creation.

You can check the balance by running

```
dfx wallet --network ic balance
```

After making sure you have cycles available you can run

```
dfx deploy --network ic
```

The command will build the project, create two new canisters on the IC and deploy both the Svelte and Motoko dapps. The command will also create a new file `canister_ids.json` which will help the dfx tool deploy to the same canisters in future updates. You can commit this file in your repository.

You can now open your Svelte app running on the IC. You can find the canister ID in the deploy command output, or use the `frontend` ID in `canister_ids.json`.

The link to your app is `<frontend canister id>.ic0.app`. For example if your `frontend` canister ID is `zixfv-4yaaa-aaaam-aaatq-cai`, your app will be at `https://zixfv-4yaaa-aaaam-aaatq-cai.ic0.app/`.
