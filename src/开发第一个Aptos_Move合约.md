# 开发第一个Aptos Move合约：Todo list

## 工程创建

```bash
$ mkdir aptos_todo_list && cd aptos_todo_list

$ aptos move init --name  aptos_todo_list
{
  "Result": "Success"
}
```

## 合约开发

https://learn.aptoslabs.com/zh/code-examples/todo-list

## 合约编译

```bash
$ aptos move build
Compiling, may take a little while to download git dependencies...
UPDATING GIT DEPENDENCY https://github.com/aptos-labs/aptos-core.git
INCLUDING DEPENDENCY AptosFramework
INCLUDING DEPENDENCY AptosStdlib
INCLUDING DEPENDENCY MoveStdlib
BUILDING aptos_todo_list
{
  "Result": [
    "0000000000000000000000000000000000000000000000000000000000000000::todo_list"
  ]
}
```

## 执行单测

```bash
$ aptos move test
INCLUDING DEPENDENCY AptosFramework
INCLUDING DEPENDENCY AptosStdlib
INCLUDING DEPENDENCY MoveStdlib
BUILDING aptos_todo_list
Running Move unit tests
[debug] "todo_list_owner: @0x100"
[debug] "todo_list_length: 1"
[debug] "todo_content: \"New Todo\""
[debug] "todo_completed: false"
[debug] "todo_completed: true"
[ PASS    ] 0xcb3303e6b96a1a666347bd06e27d24cc0cb09e204fedb6223a7bc9091dc49022::todo_list::test_end_to_end
[ PASS    ] 0xcb3303e6b96a1a666347bd06e27d24cc0cb09e204fedb6223a7bc9091dc49022::todo_list::test_end_to_end_2_todo_lists
[ PASS    ] 0xcb3303e6b96a1a666347bd06e27d24cc0cb09e204fedb6223a7bc9091dc49022::todo_list::test_todo_already_completed
[ PASS    ] 0xcb3303e6b96a1a666347bd06e27d24cc0cb09e204fedb6223a7bc9091dc49022::todo_list::test_todo_does_not_exist
[ PASS    ] 0xcb3303e6b96a1a666347bd06e27d24cc0cb09e204fedb6223a7bc9091dc49022::todo_list::test_todo_list_does_not_exist
Test result: OK. Total tests: 5; passed: 5; failed: 0
{
  "Result": "Success"
}
```

## 环境初始化

```bash
$ aptos init
Configuring for profile default
Choose network from [devnet, testnet, mainnet, local, custom | defaults to devnet]
testnet
Enter your private key as a hex literal (0x...) [Current: None | No input: Generate new key (or keep one if present)]

No key given, generating key...
Account 0xcb3303e6b96a1a666347bd06e27d24cc0cb09e204fedb6223a7bc9091dc49022 doesn't exist, creating it and funding it with 100000000 Octas
Account 0xcb3303e6b96a1a666347bd06e27d24cc0cb09e204fedb6223a7bc9091dc49022 funded successfully

---
Aptos CLI is now set up for account 0xcb3303e6b96a1a666347bd06e27d24cc0cb09e204fedb6223a7bc9091dc49022 as profile default!
 See the account here: https://explorer.aptoslabs.com/account/0xcb3303e6b96a1a666347bd06e27d24cc0cb09e204fedb6223a7bc9091dc49022?network=testnet
 Run `aptos --help` for more information about commands
{
  "Result": "Success"
}
```

>   **注：若未进行初始化，部署合约将报错：**
>
>   ```bash
>   $ aptos move publish
>   Compiling, may take a little while to download git dependencies...
>   UPDATING GIT DEPENDENCY https://github.com/aptos-labs/aptos-core.git
>   INCLUDING DEPENDENCY AptosFramework
>   INCLUDING DEPENDENCY AptosStdlib
>   INCLUDING DEPENDENCY MoveStdlib
>   BUILDING aptos_todo_list
>   package size 4525 bytes
>   {
>     "Error": "Unable to find config /root/.aptos/config.yaml, have you run `aptos init`?"
>   }
>   ```

## 领水

```bash
$ aptos account fund-with-faucet --account 0xcb3303e6b96a1a666347bd06e27d24cc0cb09e204fedb6223a7bc9091dc49022
{
  "Result": "Added 100000000 Octas to account 0xcb3303e6b96a1a666347bd06e27d24cc0cb09e204fedb6223a7bc9091dc49022"
}
```

## 合约部署

```bash
$ aptos move publish
Compiling, may take a little while to download git dependencies...
UPDATING GIT DEPENDENCY https://github.com/aptos-labs/aptos-core.git
INCLUDING DEPENDENCY AptosFramework
INCLUDING DEPENDENCY AptosStdlib
INCLUDING DEPENDENCY MoveStdlib
BUILDING aptos_todo_list
package size 4576 bytes

Do you want to submit a transaction for a range of [274000 - 411000] Octas at a gas unit price of 100 Octas? [yes/no] >
yes
Transaction submitted: https://explorer.aptoslabs.com/txn/0x0b7b5b75a81040352741c1342db44a57faea5b8492f2248bab54577b6fd146a3?network=testnet
{
  "Result": {
    "transaction_hash": "0x0b7b5b75a81040352741c1342db44a57faea5b8492f2248bab54577b6fd146a3",
    "gas_used": 2740,
    "gas_unit_price": 100,
    "sender": "cb3303e6b96a1a666347bd06e27d24cc0cb09e204fedb6223a7bc9091dc49022",
    "sequence_number": 0,
    "success": true,
    "timestamp_us": 1725804736732089,
    "version": 5954581859,
    "vm_status": "Executed successfully"
  }
}
```

