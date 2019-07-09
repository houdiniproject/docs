# Definitions

## Instance
A copy of Houdini running. An organization with a server running Houdini is running their own instance.

## Instance owner
The entity responsible for running an instance of Houdini. In cases of a Houdini hosted service, like CommitChange, this is an organization independent of the nonprofits using this instance of Houdini. In other cases, this may be an organization with some sort of oversight of all of the nonprofits on their instance of Houdini, such as a fiscal sponsor. In other cases, a single nonprofit may also be their own instance owner. The instance owner has access to the superuser role which gives them access to the information of ALL of the nonprofits on their instance.

## Nonprofit
Short hand for an organization registered on an instance of Houdini. The nonprofit doesn't have to formally be a nonprofit or NGO but they often are.

## Payment
A payment represents a description of a non-expense transaction that the user of Houdini cares about. It can be of positive or negative value. Money could have changed hands through Houdini, like via Stripe or Paypal, or offline, via paper check. It's, more or less, like a checkbook entry but, in cases of an offline donation, the money could be handled outside of Houdini. Notably, non-payment expenses are NEVER handled through Houdini. Houdini only cares about contributions to an organization (such as a donation, ticket purchase, etc) and any disputes, refunds, or fees related to those contributions.

## Merchant Provider Plugin (MPP)
A Merchant Provider Plugin (or MPP) is used for making online transactions through a merchant provider. A MPP, which is usually provided to Houdini as a Rails engine, handles the transaction flow for a given merchant provider, both on the backend and the front end. Additionally, it keeps any necessary state used by the transaction flow. This could include ids used for different transaction sources that are meaningful to a transaction provider, records of transactions in different states, the current balance for a given nonprofit, etc. A MPP may also need to handle events created by merchant provider, such as notification of a dispute, a change in status of a transaction, etc and routed to an instance via a webhook or some other out of process notification.

## Merchant provider
The service, system or source used for making transactions. In the case of a service like Stripe, there might be specific accounts related to the service for both the Instance Owner and the Nonprofit (depending on setup, they could differ or not). In the case of cryptocurrency, the transaction provider could relate to transfers between wallets and the instance owner and nonprofits may have wallet addresses.

## Transaction source
The database and data entity which contains an transaction source id. Each one has a source type, since they're only meaningful for a given transaction source type on a particular merchant provider.

### Transaction source type
A transaction source type is an identifier used for routing actions related to a transaction source to the proper MPP. Every MPP registers one or more source types.

### Transaction source ID
A identification of an account belonging to a supporter which can make transactions. This could be an address for a cryptocurrency wallet, a Stripe card identifier or, in the case where the Houdini instance works with a raw merchant account, the credit card number and expiration date. This is something the supporter has given to the nonprofit for making transactions. Stored by the MPP in an entry source.

## Supporter
An individual who is in the nonprofit's CRM in Houdini. A supporter, if they have any payments with the nonprofit, may have associated transaction sources.

## Transaction
The logical process of making money change hands from a supporter to a nonprofit as well as in the reverse direction for disputes, refunds, etc. happens. If a transaction completes, money changes hands.
