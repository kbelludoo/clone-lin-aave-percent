# clone-lin-aave-percent

Experimental LIN clone of Aave V3 `PercentageMath.percentMul` / `percentDiv` (i64-positive scale: 128-bit `(a*b+HALF_PERCENTAGE_FACTOR)/PERCENTAGE_FACTOR` half-up, fail-closed if the quotient does not fit i64).

- **Upstream:** [aave/aave-v3-core](https://github.com/aave/aave-v3-core) `contracts/protocol/libraries/math/PercentageMath.sol` commit `782f51917056a53a2c228701058a6c3fb233684a` (MIT after BUSL-1.1 Change Date 2023-01-27).
- **LIN kernel:** [`src/lin_aave_percent.lin`](src/lin_aave_percent.lin)
- **C11 oracle copy:** [`test/oracles/aave_percent_c11.c`](test/oracles/aave_percent_c11.c)
- **Proofs (lin-open only):** [kbelludoo/lin-open](https://github.com/kbelludoo/lin-open) `examples/aave_percent/` and `python3 test/prove_aave_percent_external.py`
- **Class:** EXPERIMENTAL. Not Ethereum Aave V3 uint256. Not a production replacement. Not floor `(a*b)/1e4`.

Named goldens (i64-positive, PERCENTAGE_FACTOR=1e4): `percentMul(10000,10000)` → **10000**; `percentMul(3, 0.5e4)` → **2** vs floor **1**; `percentDiv(2,3)` → **6667** vs floor **6666**; `percentMul(3e18, 5000)` → **1500000000000000000** vs naive i64 wrap **2797068074134536192**; `percentMul(4e18, 30000)` fail-closed **0**.
