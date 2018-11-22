```
  Layer: Applications
  Title: 3-of-4 Multisignature Escrow
  Author: Yuki Aoki <ayukiyhs at gmail.com>
  Created: 2018-11-17
```

## Abstract

This extends 2-of-3 multisignature escrow so that administrators can control funds in a more decentralized way.

## Motivation

2-of-3 multisignature escrow is a safe and usable solution when buying something with cryptocurrency.
But when it comes to using in practice, administrators of the platforms may want to collect a charge for use or apply additional rules.

This method extends 2-of-3 multisig escrow. It provides not only users but also administrators to control their funds.
By this, for example, administrators can make platform users pay fees without depriving users of their fund ownership. 
Besides, administrators can enforce some rules.

## Definitions

* Seller - He opens on the escrow platform
* Buyer - He wants to buy some goods from the seller
* Platform Administrator - A person or organization running the escrow platform.
* Platform server - An online computer which is run by platform administrator and manages users' order.

Each has own private key.

## Specification

1. Buyer clicks "Buy" button on the escrow platform.
2. Collect public key of buyer and seller.
3. Issue a 3-of-4 multisig P2SH(or P2WSH if SegWit) address, which is made up of public keys below.
  - Buyer
  - Seller
  - Platform Server
  - Platform Administrator
4. Buyer deposits money, including the price and the blockchain fee and platform usage fee, into the multisignature address.
5. Seller recognizes the deposit so he can send buyer merchandise.
6. Buyer notifies the platform that he received merchandise.
7. Platform server creates and signs a transaction.
  * Signed with platform server's private key
  * Outputs are the seller's address, a platform fee pool.
8. Buyer and seller sign the transaction.
9. Broadcast the transaction.

If the seller doesn't send merchandise, or buyer and seller have trouble signing the transaction: for instance, due to the lack of blockchain skills, platform administrator can intervene and rollback with platform administrator's private key.

Even if the well-trained user were to modify the transaction and try to deny paying the usage fee, it is no use trying it, because it has already been signed by platform server.
By this mechanism, the platform forces users to pay a charge. That makes a difference between 2-of-3 multisig escrow.

This method will fit when there are a cryptocurrency wallet app and the app can sign separately with Deep Link API and so on.

The disadvantage is that buyer and seller must trust administrator to an extent.
If platform server go down, the transaction will not be created.
But platform administrator cannot access funds in multisignature address directly, so administrator have no incentive to stop service on purpose.
So, I conclude that this method is far safer than fully-centralized escrow service like almost all of cryptocurrency exchanges.

## Implementation

In development

## See also

[Add the draft of Deep Link Payment Protocol spec](https://github.com/bitcoincashorg/bitcoincash.org/pull/145)

## Acknowledgement

## Documentation History

* 2018-11-22 Created repository and moved from gists
* 2018-11-20 Made public and moved to my gists.
* 2018-11-17 Initial

## Copyright

Copyright (c) 2018 Yuki Aoki
All rights reserved
