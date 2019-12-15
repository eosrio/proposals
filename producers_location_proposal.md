
# Deploy eosio.contracts v1.7.1 - Producers Location Patch


## Requirements

- [eosio.cdt 1.6.3](https://github.com/EOSIO/eosio.cdt/tree/v1.6.3)
- [eosio 1.8.6](https://github.com/EOSIO/eos/tree/v1.8.6)
- [eosio.contracts v1.7.1-location](https://github.com/eosrio/eosio.contracts/tree/eos-mainnet/v1.7.1-location)


### 1. Build and verify checksums:

#### Build:

- Clone branch [eos-mainnet/v1.7.1-location](https://github.com/eosrio/eosio.contracts/tree/eos-mainnet/v1.7.1-location)
- Build

```
./build.sh -c [eosio.cdt Path] -e [eosio Path]
```

#### Verify checksums:

This proposal only affects the code file. There is no need to updtade the abi.

You can check the checksums, running the following command:

##### Current Mainnet eosio.system contract:

```
cleos -u http://api.eosrio.io get code eosio
code hash: 612b7eb30654473e6b943e58d49c0393eea619d7e53dbc8a166f484546ed02cc

```

##### eosio.system contract patched:

```
openssl dgst -sha256 eosio.system/eosio.system.wasm
SHA256(eosio.system.wasm)= df5aa4c8295011e055baa631045844b1363cb7c15b5a4804756f7b24b4280143
```

### 2. Review our proposal

```
cleos -u http://api.eosrio.io multisig review eosriobrazil producers-location
```

***Before approve the multisig, please update your location:***

```
cleos -u http://api.eosrio.io system regproducer {producer_name} {prodcer_key} {url} {location}
```
Where the location is the producer timezone. Please refer to the map below to check your timezone, remember to not use a negative timezone.

![timezone](timezone.png)

E.g.:
EOSRio (Rio de Janeiro) is UTC-3. In this case, will be 21.
```
cleos -u http://api.eosrio.io  system regproducer eosriobrazil EOS1234567890XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX eosrio.io 21
```

Made with ♥ by [EOS Rio](https://eosrio.io/)
