# Generate gentx guide

## Instruction

### Install RIZON Blockchain

```bash
$ git clone https://github.com/rizon-world/rizon.git && cd rizon
$ git checkout v0.2.3
$ make install
```

### Setup initial node

If you had setup node, you'd better clean existing configurations.

```bash
# remove old genesis.json file and gentxs
$ rm -rf ~/.rizon/config/genesis.json
$ rm -rf ~/.rizon/config/gentx

# reset old blockchain data
$ rizond unsafe-reset-all
```

And init your node.

```bash
$ rizond init <moniker> --chain-id groot-011 
```

### Prepare validator wallet

Probably you already have your own wallet. If you don't, please refer to [here](https://docs.rizon.world/resource/cli/general#keys) and make one.

### Create gentx

After init node and prepare wallet, you need to create your genesis tx.

```bash
# add genesis account
$ rizond add-genesis-account $(rizond keys show <your_wallet_name> -a) 120000000uatolo
# generate gentx
$ rizond gentx <your_wallet_name> 100000000uatolo --chain-id groot-011
```

If there is no error, you have `gentx-<your_node_id>.json` file on `~/.rizon/config/gentx/` directory like this.

```json
{
    "auth_info": {
        "fee": {
            "amount": [],
            "gas_limit": "200000",
            "granter": "",
            "payer": ""
        },
        "signer_infos": [
            {
                "mode_info": {
                    "single": {
                        "mode": "SIGN_MODE_DIRECT"
                    }
                },
                "public_key": {
                    "@type": "/cosmos.crypto.secp256k1.PubKey",
                    "key": "A/KvQ+4OTSaPNahFeEf7vOB2VO8Xwx5RgPWWE/VF2UYB"
                },
                "sequence": "0"
            }
        ]
    },
    "body": {
        "extension_options": [],
        "memo": "184a1687932d63bfe85418b4821faffb98a2079e@192.168.1.71:26656",
        "messages": [
            {
                "@type": "/cosmos.staking.v1beta1.MsgCreateValidator",
                "commission": {
                    "max_change_rate": "0.010000000000000000",
                    "max_rate": "0.200000000000000000",
                    "rate": "0.100000000000000000"
                },
                "delegator_address": "rizon1uz6yyl4hd47acn4zxz0jl6thz6vjuz9xr3uurc",
                "description": {
                    "details": "",
                    "identity": "",
                    "moniker": "drill_test",
                    "security_contact": "",
                    "website": ""
                },
                "min_self_delegation": "1",
                "pubkey": {
                    "@type": "/cosmos.crypto.ed25519.PubKey",
                    "key": "hrdbPmEHSmIBMGv1velR+a+rWHcBYz/Nzq4Kcql06Yc="
                },
                "validator_address": "rizonvaloper1uz6yyl4hd47acn4zxz0jl6thz6vjuz9xs47apg",
                "value": {
                    "amount": "100000000",
                    "denom": "uatolo"
                }
            }
        ],
        "non_critical_extension_options": [],
        "timeout_height": "0"
    },
    "signatures": [
        "Ymn/j3aZinVVoi2OFWnNhLx0+T3QBcR4h+TUystoD7cZp4grDBPIxzEO+lrDRpCmw9j0Npb/oZyRp+UjL0jlFQ=="
    ]
}
```

### Create pull request

You need to send us your gentx, submit a pull request with your gentx file on `drill-1/gentxs/` directory of this repository `drill-1` branch with filename `<validator_name>.json` format.

### Optional. Provide public seed or peer

If you can provide public seed or peer, you also can submit a pr here, just edit `drill-1/peers.md` file and fill your information.

## Next step

After aggregate all of gentxs, we introduce genesis file and notice here and discord channel.