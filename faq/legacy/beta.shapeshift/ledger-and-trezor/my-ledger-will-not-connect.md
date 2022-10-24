# 🔌 My Ledger Will Not Connect

_**Are you experiencing connection issues with your Ledger?**_ Please review [**this article**](https://support.ledger.com/hc/en-us/articles/360023518653-Solutions-to-most-common-issues?support=true) from Ledger.

_Additionally, here are some troubleshooting steps:_

**Ledger Nano S**

Update Ledger via Ledger Live. (If you have trouble connecting to Ledger Live, please reach out to Ledger Support team)

Ledger firmware 1.5.5 or later for it to work with the Platform. Ledger’s pre 1.5.5. Firmware does not have WebUSB support.

**Ledger Nano X**

Update Ledger via Ledger Live. (If you have trouble connecting to Ledger Live, please reach out to Ledger Support team)

Ledger Nano X firmware 1.2.4 or later for it to work with the Platform.

**Ledger Apps**

Have the following apps on their Ledger updated to:

BTC app update (1.3.17) or later

ETH app update (1.2.11) or later

**Add multiple Bitcoin accounts (Nano X only)**

Ledger Nano X platform users won’t be able to create/add multiple BTC accounts via the Platform. This can only be done via Ledger Live.

**Bitcoin Cash**

Bitcoin Cash is not supported on the Nano S or Nano X.

####

**Windows Connectivity Issues**

Here is the official troubleshooting solution from Ledger: [https://github.com/LedgerHQ/ledgerjs/tree/master/packages/hw-transport-webusb](https://github.com/LedgerHQ/ledgerjs/tree/master/packages/hw-transport-webusb)

_The problem is with Windows. It doesn't play well with any devices that speak WebUSB including Trezor and KeepKey. The work around until Microsoft addresses this issue is to use_[ _Zadig_ ](replacing-your-driver-using-zadig.md)_to change your driver so it speaks WebUSB._

####

#### **Multiple Accounts - Non BTC SegWit accounts**

Ledger supports SegWit accounts for other assets besides Bitcoin. Unfortunately, the Platform does not support SegWit for non-Bitcoin assets. Therefore, Ledger users will only be able to see their BTC SegWit accounts in the Platform.

To use non-BTC SegWit accounts, you are going to need to use Ledger Live.

#### **Ethereum Accounts Created via the old Ledger Live Chrome App**

Like KeepKey, Ledger has an old client that was a Chrome App. If a user created an Ethereum account via that older Ledger Chrome App, it will not show up in the platform. This is due to the account derivation path for these accounts being different than the account derivation path when a user creates an Ethereum account via Ledger Live or the ShapeShift Platform.

Solution: _Move your Ethereum and ERC20 assets to an Ethereum account created via Ledger Live._
