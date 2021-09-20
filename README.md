# dss-proxy-actions
Proxy functions to be used via ds-proxy. These functions are based on `dss-cdp-manager` as CDP registry.

https://github.com/velerofinance/dss-proxy-actions

## DssProxyActions

`open(address manager, bytes32 ilk, address usr)`: creates an `UrnHandler` (`cdp`) for the address `usr` (for a specific `ilk`) and allows to manage it via the internal registry of the `manager`.

`give(address manager, uint cdp, address usr)`: transfers the ownership of `cdp` to `usr` address in the `manager` registry.

`giveToProxy(address proxyRegistry, address manager, uint cdp, address usr)`: transfers the ownership of `cdp` to the proxy of `usr` address (via `proxyRegistry`) in the `manager` registry.

`cdpAllow(address manager, uint cdp, address usr, uint ok)`: allows/denies `usr` address to manage the `cdp`.

`urnAllow(address manager, address usr, uint ok)`: allows/denies `usr` address to manage the `msg.sender` address as `dst` for `quit`.

`flux(address manager, uint cdp, address dst, uint wad)`: moves `wad` amount of collateral from `cdp` address to `dst` address.

`move(address manager, uint cdp, address dst, uint rad)`: moves `rad` amount of USDV from `cdp` address to `dst` address.

`frob(address manager, uint cdp, int dink, int dart)`: executes `frob` to `cdp` address assigning the collateral freed and/or USDV drawn to the same address.

`quit(address manager, uint cdp, address dst)`: moves `cdp` collateral balance and debt to `dst` address.

`enter(address manager, address src, uint cdp)`: moves `src` collateral balance and debt to `cdp`.

`shift(address manager, uint cdpSrc, uint cdpDst)`: moves `cdpSrc` collateral balance and debt to `cdpDst`.

`lockVLX(address manager, address vlxJoin, uint cdp)`: deposits `msg.value` amount of VLX in `vlxJoin` adapter and executes `frob` to `cdp` increasing the locked value.

`safeLockVLX(address manager, address VLXJoin, uint cdp, address owner)`: same than `lockVLX` but requiring `owner == cdp owner`.

`lockGem(address manager, address gemJoin, uint cdp, uint wad, bool transferFrom)`: deposits `wad` amount of collateral in `gemJoin` adapter and executes `frob` to `cdp` increasing the locked value. Gets funds from `msg.sender` if `transferFrom == true`.

`safeLockGem(address manager, address gemJoin, uint cdp, uint wad, bool transferFrom, address owner)`: same than `lockGem` but requiring `owner == cdp owner`.

`freeVLX(address manager, address vlxJoin, uint cdp, uint wad)`: executes `frob` to `cdp` decreasing locked collateral and withdraws `wad` amount of VLX from `vlxJoin` adapter.

`freeGem(address manager, address gemJoin, uint cdp, uint wad)`: executes `frob` to `cdp` decreasing locked collateral and withdraws `wad` amount of collateral from `gemJoin` adapter.

`draw(address manager, address jug, address usdvJoin, uint cdp, uint wad)`: updates collateral fee rate, executes `frob` to `cdp` increasing debt and exits `wad` amount of USDV token (minting it) from `usdvJoin` adapter.

`wipe(address manager, address usdvJoin, uint cdp, uint wad)`: joins `wad` amount of USDV token to `usdvJoin` adapter (burning it) and executes `frob` to `cdp` for decreasing debt.

`safeWipe(address manager, address usdvJoin, uint cdp, uint wad, address owner)`: same than `wipe` but requiring `owner == cdp owner`.

`wipeAll(address manager, address usdvJoin, uint cdp)`: joins all the necessary amount of USDV token to `usdvJoin` adapter (burning it) and executes `frob` to `cdp` setting the debt to zero.

`safeWipeAll(address manager, address usdvJoin, uint cdp, address owner)`: same than `wipeAll` but requiring `owner == cdp owner`.

`lockVLXAndDraw(address manager, address jug, address vlxJoin, address usdvJoin, uint cdp, uint wadD)`: combines `lockVLX` and `draw`.

`openLockVLXAndDraw(address manager, address jug, address vlxJoin, address usdvJoin, bytes32 ilk, uint wadD)`: combines `open`, `lockVLX` and `draw`.

`lockGemAndDraw(address manager, address jug, address gemJoin, address usdvJoin, uint cdp, uint wadC, uint wadD, bool transferFrom)`: combines `lockGem` and `draw`.

`openLockGemAndDraw(address manager, address jug, address gemJoin, address usdvJoin, bytes32 ilk, uint wadC, uint wadD, bool transferFrom)`: combines `open`, `lockGem` and `draw`.

`wipeAndFreeVLX(address manager, address vlxJoin, address usdvJoin, uint cdp, uint wadC, uint wadD)`: combines `wipe` and `freeVLX`.

`wipeAllAndFreeVLX(address manager, address vlxJoin, address usdvJoin, uint cdp, uint wadC)`: combines `wipeAll` and `freeVLX`.

`wipeAndFreeGem(address manager, address gemJoin, address usdvJoin, uint cdp, uint wadC, uint wadD)`: combines `wipe` and `freeGem`.

`wipeAllAndFreeGem(address manager, address gemJoin, address usdvJoin, uint cdp, uint wadC)`: combines `wipeAll` and `freeGem`.

`openLockGNTAndDraw(address manager, address jug, address gntJoin, address usdvJoin, bytes32 ilk, uint wadC, uint wadD)`: like `openLockGemAndDraw` but specially for GNT token.

## DssProxyActionsFlip

`exitVLX(address manager, address vlxJoin, uint cdp, uint wad)`: exits `wad` amount of VLX from `vlxJoin` adapter (received in the `cdp` urn after the liquidation auction is over).

`exitGem(address manager, address gemJoin, uint cdp, uint wad)`: exits `wad` amount of collateral from `gemJoin` adapter (received in the `cdp` urn after the liquidation auction is over).

## DssProxyActionsEnd

`freeVLX(address manager, address vlxJoin, address end, uint cdp)`: after system is caged, recovers remaining VLX from `cdp` (pays remaining debt if exists).

`freeGem(address manager, address gemJoin, address end, uint cdp)`: after system is caged, recovers remaining token from `cdp` (pays remaining debt if exists).

`pack(address usdvJoin, address end, uint wad)`: after system is caged, packs `wad` amount of USDV to be ready for cashing.

`cashVLX(address vlxJoin, address end, bytes32 ilk, uint wad)`: after system is caged, cashes `wad` amount of previously packed USDV and returns the equivalent in VLX.

`cashGem(address gemJoin, address end, bytes32 ilk, uint wad)`: after system is caged, cashes `wad` amount of previously packed USDV and returns the equivalent in token.

## DssProxyActionsDsr

`join(address usdvJoin, address pot, uint wad)`: joins `wad` amount of USDV token to `usdvJoin` adapter (burning it) and moves balance to `pot` for USDV Saving Rates.

`exit(address usdvJoin, address pot, uint wad)`: retrieves `wad` amount of USDV from `pot` and exits USDV token from `usdvJoin` adapter (minting it).

`exitAll(address usdvJoin, address pot)`: same than `exit` but all the available amount.
