# Fixing RX 6700 XT losing hashrate

If you have some RX 6700 XT cards and apply the same overclock settings, unfortunately you may find that some cards have unexpectedly lower hashrates than others after working for a while (such as overnight).

You can check their actual power consumption and core VDD by running a command (```amd-info``` in HiveOS). Because their core VDD will go a little higher after running for a while and eventually stabilize.
You will find that the core VDD and power consumption of those low hashrate cards are lower than others. I think that is why their hashrate got lower.

To fix this, you need to increse their core VDD setting to match the others, and that is it.
