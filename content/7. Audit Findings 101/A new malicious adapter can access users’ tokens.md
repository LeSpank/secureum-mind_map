
# 19 - [A new malicious adapter can access users’ tokens](./A%20new%20malicious%20adapter%20can%20access%20users’%20tokens.md)

The purpose of the `MetaSwap` contract is to save users gas costs when dealing with a number of different aggregators.

They can just `approve()` their tokens to be spent by `MetaSwap` (or in a later architecture, the Spender contract). They can then perform trades with all supported aggregators without having to reapprove anything. 

A downside to this design is that a malicious (or buggy) adapter has access to a large collection of valuable assets. 

Even a user who has diligently checked all existing adapter code before interacting with `MetaSwap` runs the risk of having their funds intercepted by a new malicious adapter that’s added later.

### Recommendation:
Make `MetaSwap` contract the only contract that receives token approval. It then moves tokens to the Spender contract before that contract `DELEGATECALL`s to the appropriate adapter. In this model, newly added adapters shouldn’t be able to access users’ funds.
___
## Slide Screenshot
![019.png](../../images/7.%20Audit%20Findings%20101/019.png)
___
## Slide Text
- ConsenSys Audit MetaSwap Finding 4.2
- Access Control
- Medium Severity
- Malicious Adapter
- User Tokens
___
## References
- Youtube Reference
- Medium severity finding from [Consensys Diligence Audit of MetaSwap](https://consensys.net/diligence/audits/2020/08/metaswap/#a-new-malicious-adapter-can-access-users-tokens)
___
## Tags
