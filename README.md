# Silo V2 protected shares on Sonic

Silo Finance V2 ERC-20 protected-collateral share tokens on Sonic (non-borrowable collateral). Each emitted address is the market entity's spToken address, rather than the lending vault itself.

## Specific source documentation

Silo Finance's own [snapshot documentation](https://github.com/silo-finance/lenders-snapshot/blob/58dbfc612906307137c305d56adf9f1a7ea61dce/scripts/lender-snapshot/README.md)
describes the `subgraph_url` configuration and identifies `snapshot_lenders.py`
as its canonical configuration. That [documented configuration](https://github.com/silo-finance/lenders-snapshot/blob/58dbfc612906307137c305d56adf9f1a7ea61dce/scripts/lender-snapshot/snapshot_lenders.py)
explicitly selects Sonic's subgraph
`8wcbzcdNirQvk1ETh25wpVzb5GWs8DvugpbwrYnTCcxj`. This is a reference to that
specific subgraph, without inferring authorization for other publications by
the same address. The project also identifies these chain endpoints as legacy
V2 sources in its [borrower tooling](https://github.com/silo-finance/actions/blob/0e0a4f79772a176846e181483d1f22adf5b26948/scripts/pull_borrowers/fetch_legacy_borrowers.py).

The [named subgraph](https://thegraph.com/explorer/subgraphs/8wcbzcdNirQvk1ETh25wpVzb5GWs8DvugpbwrYnTCcxj?chain=arbitrum-one&view=About)
resolved on 2026-10-28 to deployment
`QmQUcPAEpUQJL3AYK21hsgNnj6XmWepTXJXySHdFXMmp7p`. The module queries that
explicit deployment through The Graph gateway, with the supplied key only in
the authorization header. Recheck the named source before filing an item.

## Retrieval and naming

Every market row is retrieved at one block hash with an unfiltered first page, strictly ascending unique-ID cursor pages and a final metadata seal. The spToken relation supplies the emitted token address. Missing or invalid identities, duplicate cursors, unhealthy metadata and unfinished pagination throw, without a partial return or removed rows. A finite page bound throws rather than truncating.

Names combine the source Silo ID and market index. Notes identify the associated lending vault, Silo configuration and token role. A repeated name uses the complete emitted token address; no fabricated instance number or skipped market is introduced. The output is a single token category.

The UI link is the protocol application; it does not claim that a particular legacy market is currently usable or listed in the UI.

## Build

Use Yarn and run yarn build. All logic is in src/main.mts, which exports only the async two-string-argument returnTags function. MIT licensed; authored from our own original Silo V2 module.
