# BitLock Pro – Next-Generation Bitcoin Collateral Platform

## Overview

**BitLock Pro** is an institutional-grade decentralized lending protocol built on the **Stacks Layer-2** for Bitcoin. The platform transforms idle Bitcoin holdings into productive capital through a **secure, transparent, and trustless collateral management system**.

BitLock Pro bridges traditional finance principles with blockchain innovation, offering:

* Instant loan origination
* Dynamic risk modeling
* Automated liquidation mechanics
* Real-time loan health monitoring
* Multi-asset collateral support (BTC, STX, and extendable)

The protocol is designed for both retail and institutional users, enabling **capital efficiency without sacrificing Bitcoin exposure**.

---

## System Overview

At its core, BitLock Pro enables users to:

1. **Deposit Collateral** – Lock BTC or supported assets as collateral.
2. **Request Loans** – Borrow against collateralized Bitcoin, subject to collateral ratio requirements.
3. **Monitor Loan Health** – Automatic health checks ensure overcollateralization is maintained.
4. **Repay Loans** – Fully repay with interest to release collateral.
5. **Handle Liquidations** – Under-collateralized positions are liquidated transparently for protocol stability.

### Key Features

* **Risk Parameters**: Adjustable minimum collateral ratio and liquidation thresholds for dynamic market conditions.
* **Interest Mechanism**: Block-based compound interest calculation.
* **Governance Layer**: Owner-controlled updates to parameters and oracle feeds.
* **Oracle Integration**: Secured price feeds for BTC and supported assets.
* **Portfolio Management**: User-specific tracking of active loans.

---

## Contract Architecture

The protocol consists of several **logical layers**:

### 1. **System Constants & Errors**

Defines ownership, supported assets, and a structured error handling framework for predictable failure modes.

### 2. **Protocol State Variables**

Maintains dynamic values such as:

* Platform initialization status
* Minimum collateral ratio
* Liquidation thresholds
* Protocol fee rates
* Aggregated statistics (BTC locked, total loans issued)

### 3. **Data Maps**

* **loans**: Registry of loan records (borrower, collateral, loan amount, interest rate, status).
* **user-loans**: Tracks user-specific active loans.
* **collateral-prices**: Maintains oracle-driven price feeds for supported assets.

### 4. **Internal Functions**

* **Collateral Ratio Calculation** – Validates loan safety relative to asset price.
* **Interest Computation** – Computes accrued compound interest per block.
* **Liquidation Logic** – Executes collateral seizure for unhealthy loans.
* **Validation Functions** – Ensures data integrity (loan ID checks, price validation, asset validation).

### 5. **Public API**

* **initialize-platform** – One-time protocol bootstrap.
* **deposit-collateral** – Lock BTC as collateral.
* **request-loan** – Originate a new loan.
* **repay-loan** – Repay and release collateral.

### 6. **Governance Functions**

* **update-collateral-ratio** – Adjust overcollateralization requirements.
* **update-liquidation-threshold** – Adjust liquidation trigger levels.
* **update-price-feed** – Update oracle prices with validation.

### 7. **Read-Only Interfaces**

* **get-loan-details** – Retrieve details of a loan by ID.
* **get-user-loans** – Retrieve active loans for a user.
* **get-platform-stats** – View system-level metrics.
* **get-valid-assets** – Fetch supported assets list.

---

## Data Flow

Below is the simplified **loan lifecycle flow**:

1. **Collateral Deposit**

   * User deposits BTC (or supported asset).
   * Protocol updates `total-btc-locked`.

2. **Loan Request**

   * User requests loan with collateral amount and desired loan amount.
   * System verifies:

     * Platform is initialized
     * Collateral ratio meets threshold
     * Price feeds are valid
   * Loan record is created in `loans`, added to `user-loans`.

3. **Interest Accrual**

   * Interest accrues block by block via the internal interest calculator.

4. **Repayment**

   * User repays full loan amount + accrued interest.
   * Collateral is released, and loan is marked as `repaid`.

5. **Liquidation**

   * If loan collateral ratio falls below threshold, automated liquidation occurs.
   * Loan is marked as `liquidated`, borrower’s active loans are updated.

---

## Security Considerations

* **Authorization Controls** – Only the contract owner can initialize the platform or update governance parameters.
* **Strict Validation** – Input amounts, loan IDs, and oracle prices undergo structured checks.
* **Oracle Trust Assumptions** – Relies on secure, timely updates to collateral price feeds.
* **Overcollateralization** – Maintains system solvency through conservative ratios and liquidation mechanics.

---

## Future Enhancements

* Expanded multi-asset collateral support (sBTC, USDC, and other wrapped assets).
* Dynamic interest rates based on market utilization.
* Delegated liquidation mechanisms for community participation.
* DAO-based governance replacing centralized contract ownership.

---

## License

This project is licensed under the **MIT License**.
