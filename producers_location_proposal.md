
# Deploy eosio.contracts v1.7.1 - Producers Location Patch


## Prerequisites

- [eosio.cdt 1.6.3](https://github.com/EOSIO/eosio.cdt/tree/v1.6.3)
- [eosio 1.8.6](https://github.com/EOSIO/eos/tree/v1.8.6)
- [eosio.contracts v1.7.1](https://github.com/EOSIO/eosio.contracts/tree/v1.7.1) smart contract. **ARRUMAR**


### 1. Build and verify checksums:

#### Build:

clone branch [mainnet/v1.7.1](https://github.com/EOSLaoMao/eosio.contracts/tree/mainnet/v1.7.1) and build: **ARRUMAR**

`./build.sh -c [eosio.cdt Path] -e [eosio Path]`

#### Verify checksums:

You can verify the build result under `build` folder once build succeed.

We have put our build under `contracts/1.7.1` for your review, which is used to deploy on EOS Mainnet.

Here are the checksums we got, please verify:

This proposal only affects the code file. There is no need to updtade the abi.

Current Mainnet eosio.system contract:
##### eosio.system.wasm:

```
openssl dgst -sha256 eosio.system/eosio.system.wasm
SHA256(eosio.system.wasm)= 612b7eb30654473e6b943e58d49c0393eea619d7e53dbc8a166f484546ed02cc

```
***ARRUMAR***
eosio.system contract patched:
##### eosio.system.wasm:

```
openssl dgst -sha256 eosio.system/eosio.system.wasm
SHA256(eosio.system.wasm)= ??????????????????
```

### 2. Review our proposal

```
cleos multisig review eosriobrazil producers-location
```

***Before approve please update your location:***

```
cleos system regproducer {producer_name} {prodcer_key} {url} {location}
```
Where the location is the producer timezone. Please refer to the map bellow to check yor timezone, remeber to not use negative timezone.

![timezone](timezone.png)

E.g.:
Brazil is UTC-3. In this case, will be 21.
```
cleos system regproducer eosriobrazil EOS1234567890XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX eosrio.io 21
```

Made with ♥ by [EOS Rio](https://eosrio.io/)
