# Aptos CLI

## 命令总览

```bash
$ aptos -h
Command Line Interface (CLI) for developing and interacting with the Aptos blockchain

Usage: aptos <COMMAND>

Commands:
  account     Tool for interacting with accounts
  config      Tool for interacting with configuration of the Aptos CLI tool
  genesis     Tool for setting up an Aptos chain Genesis transaction
  governance  Tool for on-chain governance
  info        Show build information about the CLI
  init        Tool to initialize current directory for the aptos tool
  key         Tool for generating, inspecting, and interacting with keys
  move        Tool for Move smart contract related operations
  multisig    Tool for interacting with multisig accounts
  node        Tool for operations related to nodes
  stake       Tool for manipulating stake and stake pools
  update      Update the CLI or other tools it depends on
  help        Print this message or the help of the given subcommand(s)

Options:
  -h, --help     Print help
  -V, --version  Print version
```

## info - 查看客户端信息

```bash
$ aptos info
{
  "Result": {
    "build_branch": "main",
    "build_cargo_version": "cargo 1.78.0 (54d8815d0 2024-03-26)",
    "build_clean_checkout": "true",
    "build_commit_hash": "4a202570804db6d27ba1ca6cb374228052be5bcb",
    "build_is_release_build": "true",
    "build_os": "linux-x86_64",
    "build_pkg_version": "4.1.0",
    "build_profile_name": "release",
    "build_rust_channel": "1.78.0-x86_64-unknown-linux-gnu",
    "build_rust_version": "rustc 1.78.0 (9b00956e5 2024-04-29)",
    "build_tag": "",
    "build_time": "2024-09-06 12:07:47 +00:00",
    "build_using_tokio_unstable": "true"
  }
}
```

## config - 配置相关

### 命令总览

```bash
$ aptos config -h
Tool for interacting with configuration of the Aptos CLI tool

Usage: aptos config <COMMAND>

Commands:
  delete-profile              Delete the specified profile
  generate-shell-completions  Generate shell completion files
  rename-profile              Rename the specified profile
  set-global-config           Set global configuration settings
  show-global-config          Shows the properties in the global config
  show-private-key            Show the private key for the given profile
  show-profiles               Shows the current profiles available
```

### show-private-key - 查看私钥

```bash
$ aptos config show-private-key --profile default
{
  "Result": "0x2a88.....................80020b45"
}

> 读取的是这个文件中的私钥
$ cat .aptos/config.yaml
---
profiles:
  default:
    network: Testnet
    private_key: "0x2a88.....................80020b45"
    public_key: "0xd6a31c9c8c707d9f2e0b936a05b9427527c879bcebcbdcab1339b7daea327ea6"
    account: cb3303e6b96a1a666347bd06e27d24cc0cb09e204fedb6223a7bc9091dc49022
    rest_url: "https://fullnode.testnet.aptoslabs.com"
    faucet_url: "https://faucet.testnet.aptoslabs.com"
```

## init - 初始化本地配置并创建账户

- **创建默认 profile**

```bash
$ aptos init
Configuring for profile default
Choose network from [devnet, testnet, mainnet, local, custom | defaults to devnet]
testnet
Enter your private key as a hex literal (0x...) [Current: None | No input: Generate new key (or keep one if present)]

No key given, generating key...
Account 0x47946eb78dcc85eda351217d42288e6d4669159113c7efbe7ec87bf6c07f5e97 doesn't exist, creating it and funding it with 100000000 Octas
Account 0x47946eb78dcc85eda351217d42288e6d4669159113c7efbe7ec87bf6c07f5e97 funded successfully

---
Aptos CLI is now set up for account 0x47946eb78dcc85eda351217d42288e6d4669159113c7efbe7ec87bf6c07f5e97 as profile default!
 See the account here: https://explorer.aptoslabs.com/account/0x47946eb78dcc85eda351217d42288e6d4669159113c7efbe7ec87bf6c07f5e97?network=testnet
 Run `aptos --help` for more information about commands
{
  "Result": "Success"
}
```

- **创建指定名称 profile**

```bash
$ aptos init --profile jason
Configuring for profile jason
Choose network from [devnet, testnet, mainnet, local, custom | defaults to devnet]
mainnet
Enter your private key as a hex literal (0x...) [Current: None | No input: Generate new key (or keep one if present)]

No key given, generating key...
Account 0x7ac59d3368d1eb46c599ed1fb57d6f51d2b926f2d12b4573f6954fcde602c334 does not exist, you will need to create and fund the account by transferring funds from another account

---
Aptos CLI is now set up for account 0x7ac59d3368d1eb46c599ed1fb57d6f51d2b926f2d12b4573f6954fcde602c334 as profile jason!
 See the account here: https://explorer.aptoslabs.com/account/0x7ac59d3368d1eb46c599ed1fb57d6f51d2b926f2d12b4573f6954fcde602c334?network=mainnet
 Run `aptos --help` for more information about commands
{
  "Result": "Success"
}
```

- **命令执行后，生成内容将会写到文件：`.aptos/config.yaml`中**

```bash
 cat .aptos/config.yaml
---
profiles:
  default:
    network: Testnet
    private_key: "0x9e974b31cabc31b19ed0e1debe97efb0a1f7db88cc6735cc1b326a7d1460e8f1"
    public_key: "0x71bbee6b99ef2805d3f900a0b9ca1faa2a2c863076aa1d6d4d0ec0e13e71126b"
    account: 47946eb78dcc85eda351217d42288e6d4669159113c7efbe7ec87bf6c07f5e97
    rest_url: "https://fullnode.testnet.aptoslabs.com"
    faucet_url: "https://faucet.testnet.aptoslabs.com"
  jason:
    network: Mainnet
    private_key: "0x065700c413f3bf6d9632ace4dc841d422a846bac4949b4c1eb2483fdc855ced8"
    public_key: "0xc31ae7a8fb5b794a22f902e47fb7b956c3448a2ecfcb3e3303c637e872e118fb"
    account: 7ac59d3368d1eb46c599ed1fb57d6f51d2b926f2d12b4573f6954fcde602c334
    rest_url: "https://fullnode.mainnet.aptoslabs.com"
```

# 参考资料

https://gushi10546.gitbook.io/aptos-kai-fa-zhe-wen-dang/aptos-cli/shi-yong-aptos-cli
