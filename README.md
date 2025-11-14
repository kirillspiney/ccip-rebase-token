# Cross‑Chain Rebase Token

## Overview

This project implements a cross‑chain **rebasing token** backed by
deposits in a vault.
Users deposit assets into the vault and receive rebasing tokens that
represent their proportional ownership of the underlying pool.
The token supply and user balances adjust dynamically to reflect yield
or changes in the total underlying asset amount.

Key features: 
- Users receive rebasing tokens proportional to their
share of the vault. 
- Token balances automatically adjust (rebase) based
on global growth/yield. 
- Global interest rate can decrease over time to
reward early participants. 
- Designed for cross‑chain usage using.
  
**Chainlink CCIP**.

## Architecture

The system is composed of: 
- **Vault contract(s)** managing deposits and
the underlying asset pool. 
- **Rebasing ERC‑20 token**, whose
`balanceOf` updates according to global scaling factors. 
- **CCIP
cross‑chain components** for transferring balances or shares across
chains. 
- **Foundry-based testing and deployment scripts**.

## How It Works

1.  Users deposit tokens into the vault using `deposit()`.
2.  The protocol mints rebasing tokens representing the user's share.
3.  As yield accumulates or global rate changes, user balances adjust
    proportionally.
4.  Users can redeem their tokens to withdraw their share of the
    underlying vault assets.

## Installation & Build

``` bash
git clone https://github.com/kirillspiney/ccip-rebase-token
cd ccip-rebase-token
forge build
forge test
```

## Deployment

1.  Configure environment variables in `.env` (RPC URL, private key,
    etc.).
2.  Deploy using Foundry:

``` bash
forge script script/Deploy.s.sol --rpc-url <RPC_URL> --broadcast --verify
```

3.  Ensure CCIP configuration (receiver contracts, chain selectors,
    authorized senders) is properly set before cross‑chain usage.

## Configuration

-   **Global interest rate** --- can only decrease over time.
-   **Per‑user interest rate configuration** --- optional.
-   **CCIP messaging parameters** --- target chain IDs, router
    addresses, roles.
-   **Security constraints** --- minimum deposit size, limits, access
    control.

## Security Considerations

-   Validate share accounting on mint, burn, transfers, and cross‑chain
    operations.
-   Rebase tokens require careful rounding and precision handling.
-   Protect against "small‑deposit front‑running" attacks.
-   Ensure CCIP messages cannot be replayed or trigger duplicated state
    transitions.
-   Restrict admin functions that modify economic parameters.

## Contributing

Contributions are welcome: 
- Open issues or pull requests. 
- Follow Foundry formatting (`forge fmt`). 
- Include tests for all new features.
- Treat economic‑logic changes with extra caution.

## License

MIT