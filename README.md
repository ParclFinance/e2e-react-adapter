# @parcl-finance/e2e-react-adapter

## What is it?

@parcl-finance/e2e-react-adapter is a fork of the test adapter developed by @jet-lab for solana decentralised applications. It allows to interact with your application without having to go through a browser extension, this in turn enables end-to-end testing. It also allows to programmatically reject transaction, so you can test the sad paths too.

We forked this in order to add missing functionality quickly without having to bother the @jet-lab team.

## Why?

We have found difficult to integrate a solid end-to-end test suite by using what's currently available in the ecosystem. As we care about bug free code, it was a no-brainer to create an adapter that enabled e2e testing.

## Installation

To install: `yarn add @parcl-finance/e2e-react-adapter` or `npm -i @parcl-finance/e2e-react-adapter`

## Usage

Simply add your wallet adapter to the array of adapters you normally send to your `wallet-adapter-react`

```tsx
import {  WalletProvider  }  from  '@solana/wallet-adapter-react';
import {
  PhantomWalletAdapter,
  MathWalletAdapter,
  SolflareWalletAdapter,
  SolongWalletAdapter,
  SolletWalletAdapter
} from '@solana/wallet-adapter-wallets';
import { E2EWalletAdapter } from 'e2e-react-adapter';
import { useMemo } from 'react';
import Main from './Main'

export function App() {
  const wallets = useMemo(() => [
    new PhantomWalletAdapter(),
    new MathWalletAdapter(),
    new SolflareWalletAdapter(),
    new SolongWalletAdapter(),
    new SolletWalletAdapter(),
    new SlopeWalletAdapter(),
    new E2EWalletAdapter()
  ]}, []);
  
  return (
    <WalletProvider wallets={wallets}  autoConnect>
	    <Main />
    </WalletProvier>
  )
}
```

The library will generate a new kepair each time is re-run so you either need to have an airdrop functionality on your localnet / devnet instance or you can pass a keypair object to the constructor like so:

```
new E2EWalletAdapter({
  keypair: <your_keypair>
})
```

optionally you can also programmatically reject to send or signing a transaction with `adapter.rejectNext()` or `window.solanaE2E.rejectNext()`
