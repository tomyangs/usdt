## Wallet
### abandontransaction "txid"
    Mark in-wallet transaction <txid> as abandoned
    This will mark this transaction and all its in-wallet descendants as abandoned which will allow
    for their inputs to be respent.  It can be used to replace "stuck" or evicted transactions.
    It only works on transactions which are not included in a block and are not currently in the mempool.
    It has no effect on transactions which are already conflicted or abandoned.
    将钱包内交易<txid>标记为已放弃
    这将标记此交易及其所有钱包后代将被允许放弃
    因为他们的投入是重生的。 它可以用来代替“卡住”或被驱逐的交易。
    它仅适用于未包含在块中且当前不在mempool中的事务。
    它对已经冲突或放弃的交易没有影响。
    
    Arguments:
    1. "txid"    (string, required) The transaction id
    
    Result:
### addmultisigaddress nrequired ["key",...] ( "account" )
    Add a nrequired-to-sign multisignature address to the wallet.
    Each key is a Bitcoin address or hex-encoded public key.
    If 'account' is specified (DEPRECATED), assign address to that account.
    在钱包中添加一个不需要签名的多重签名地址。
    每个密钥都是比特币地址或十六进制编码的公钥。
    如果指定了“帐户”（DEPRECATED），请为该帐户分配地址。
    Arguments:
    1. nrequired        (numeric, required) The number of required signatures out of the n keys or addresses.
    2. "keysobject"   (string, required) A json array of bitcoin addresses or hex-encoded public keys
         [
           "address"  (string) bitcoin address or hex-encoded public key
           ...,
         ]
    3. "account"      (string, optional) DEPRECATED. An account to assign the addresses to.
### addwitnessaddress "address"
    Add a witness address for a script (with pubkey or redeemscript known).
    It returns the witness script.
    添加脚本的见证地址（已知pubkey或redeemscript）。
    它返回见证脚本。
    Arguments:
    1. "address"       (string, required) An address known to the wallet
### backupwallet "destination"
    Safely copies current wallet file to destination, which can be a directory or a path with filename.
    安全地将当前钱包文件复制到目标，目标可以是目录或具有文件名的路径。

    Arguments:
    1. "destination"   (string) The destination directory or file
### dumpprivkey "bitcoinaddress"
    eveals the private key corresponding to 'bitcoinaddress'.
    Then the importprivkey can be used with this output
    显示对应于“比特币地址”的私钥。 然后importprivkey可以与此输出一起使用

    Arguments:
    1. "bitcoinaddress"   (string, required) The bitcoin address for the private key
    
    Result:
    "key"                (string) The private key
### dumpprivkey "bitcoinaddress"
    Reveals the private key corresponding to 'bitcoinaddress'.
    Then the importprivkey can be used with this output
    显示与“bitcoinaddress”对应的私钥。
    然后importprivkey可以与此输出一起使用
    Arguments:
    1. "bitcoinaddress"   (string, required) The bitcoin address for the private key
    
    Result:
    "key"                (string) The private key
### dumpwallet "filename"
    Dumps all wallet keys in a human-readable format.
    以人类可读的格式转储所有钱包密钥。

    Arguments:
    1. "filename"    (string, required) The filename
### encryptwallet "passphrase"
    Encrypts the wallet with 'passphrase'. This is for first time encryption.
    After this, any calls that interact with private keys such as sending or signing 
    will require the passphrase to be set prior the making these calls.
    Use the walletpassphrase call for this, and then walletlock call.
    If the wallet is already encrypted, use the walletpassphrasechange call.
    Note that this will shutdown the server.
    使用'密码'加密钱包。 这是第一次加密。
    在此之后，任何与私钥交互的呼叫，例如发送或签名
    将要求在进行这些调用之前设置密码短语。
    为此使用walletpassphrase调用，然后使用walletlock调用。
    如果钱包已加密，请使用walletpassphrasechange调用。
    请注意，这将关闭服务器。
    Arguments:
    1. "passphrase"    (string) The pass phrase to encrypt the wallet with. It must be at least 1 character, but should be long.
### getaccount "bitcoinaddress"
    DEPRECATED. Returns the account associated with the given address.
    已过时。 返回与给定地址关联的帐户。

    Arguments:
    1. "bitcoinaddress"  (string, required) The bitcoin address for account lookup.
    
    Result:
    "accountname"        (string) the account address
### getaccountaddress "account"
    DEPRECATED. Returns the current Bitcoin address for receiving payments to this account.
    已过时。 返回用于接收此帐户付款的当前比特币地址。

    Arguments:
    1. "account"       (string, required) The account name for the address. It can also be set to the empty string "" to represent the default account. The account does not need to exist, it will be created and a new address created  if there is no account by the given name.
    
    Result:
    "bitcoinaddress"   (string) The account bitcoin address
### getaddressesbyaccount "account"
    DEPRECATED. Returns the list of addresses for the given account.
    已过时。 返回给定帐户的地址列表。

    Arguments:
    1. "account"  (string, required) The account name.
    
    Result:
    [                     (json array of string)
      "bitcoinaddress"  (string) a bitcoin address associated with the given account
      ,...
    ]
### getbalance
    If account is not specified, returns the server's total available balance.
    If account is specified (DEPRECATED), returns the balance in the account.
    Note that the account "" is not the same as leaving the parameter out.
    The server total may be different to the balance in the default "" account.
    如果未指定account，则返回服务器的总可用余额。
    如果指定了帐户（DEPRECATED），则返回帐户中的余额。
    请注意，帐户“”与退出参数不同。
    服务器总数可能与默认“”帐户中的余额不同。
    Arguments:
    1. "account"      (string, optional) DEPRECATED. The selected account, or "*" for entire wallet. It may be the default account using "".
    2. minconf          (numeric, optional, default=1) Only include transactions confirmed at least this many times.
    3. includeWatchonly (bool, optional, default=false) Also include balance in watchonly addresses (see 'importaddress')
    
    Result:
    amount              (numeric) The total amount in BTC received for this account.
### getnewaddress ( "account" )
    Returns a new Bitcoin address for receiving payments.
    If 'account' is specified (DEPRECATED), it is added to the address book 
    so payments received with the address will be credited to 'account'.
    返回用于接收付款的新比特币地址。
    如果指定了“帐户”（DEPRECATED），则会将其添加到地址簿中
    因此，使用该地址收到的付款将记入“帐户”。
    Arguments:
    1. "account"        (string, optional) DEPRECATED. The account name for the address to be linked to. If not provided, the default account "" is used. It can also be set to the empty string "" to represent the default account. The account does not need to exist, it will be created if there is no account by the given name.
    
    Result:
    "bitcoinaddress"    (string) The new bitcoin address
### getrawchangeaddress
    Returns a new Bitcoin address, for receiving change.
    This is for use with raw transactions, NOT normal use.
    返回一个新的比特币地址，用于接收更改。
    这适用于原始交易，而非正常使用。
    Result:
    "address"    (string) The address
### getreceivedbyaccount "account" ( minconf )
    DEPRECATED. Returns the total amount received by addresses with <account> in transactions with at least [minconf] confirmations.
    已过时。 返回至少在[minconf]确认的事务中使用<account>的地址接收的总金额。
    
    Arguments:
    1. "account"      (string, required) The selected account, may be the default account using "".
    2. minconf          (numeric, optional, default=1) Only include transactions confirmed at least this many times.
    
    Result:
    amount              (numeric) The total amount in BTC received for this account.
### getreceivedbyaddress "bitcoinaddress" ( minconf )
    Returns the total amount received by the given bitcoinaddress in transactions with at least minconf confirmations.
    返回至少具有minconf确认的事务中给定bitcoinaddress接收的总量。

    Arguments:
    1. "bitcoinaddress"  (string, required) The bitcoin address for transactions.
    2. minconf             (numeric, optional, default=1) Only include transactions confirmed at least this many times.
### gettransaction "txid" ( includeWatchonly )
    Get detailed information about in-wallet transaction <txid>
    获取有关钱包内交易<txid>的详细信息

    Arguments:
    1. "txid"    (string, required) The transaction id
    2. "includeWatchonly"    (bool, optional, default=false) Whether to include watchonly addresses in balance calculation and details[]
    
    Result:
    {
      "amount" : x.xxx,        (numeric) The transaction amount in BTC
      "confirmations" : n,     (numeric) The number of confirmations
      "blockhash" : "hash",  (string) The block hash
      "blockindex" : xx,       (numeric) The index of the transaction in the block that includes it
      "blocktime" : ttt,       (numeric) The time in seconds since epoch (1 Jan 1970 GMT)
      "txid" : "transactionid",   (string) The transaction id.
      "time" : ttt,            (numeric) The transaction time in seconds since epoch (1 Jan 1970 GMT)
      "timereceived" : ttt,    (numeric) The time received in seconds since epoch (1 Jan 1970 GMT)
      "bip125-replaceable": "yes|no|unknown"  (string) Whether this transaction could be replaced due to BIP125 (replace-by-fee);
                                                       may be unknown for unconfirmed transactions not in the mempool
      "details" : [
        {
          "account" : "accountname",  (string) DEPRECATED. The account name involved in the transaction, can be "" for the default account.
          "address" : "bitcoinaddress",   (string) The bitcoin address involved in the transaction
          "category" : "send|receive",    (string) The category, either 'send' or 'receive'
          "amount" : x.xxx,                 (numeric) The amount in BTC
          "label" : "label",              (string) A comment for the address/transaction, if any
          "vout" : n,                       (numeric) the vout value
        }
        ,...
      ],
      "hex" : "data"         (string) Raw data for transaction
    }
    Result:
    amount   (numeric) The total amount in BTC received at this address.
### getunconfirmedbalance
    Returns the server's total unconfirmed balance
    返回服务器的未确认总余额
### getwalletinfo
    Returns an object containing various wallet state info.
    返回包含各种钱包状态信息的对象。

    Result:
    {
      "walletversion": xxxxx,       (numeric) the wallet version
      "balance": xxxxxxx,           (numeric) the total confirmed balance of the wallet in BTC
      "unconfirmed_balance": xxx,   (numeric) the total unconfirmed balance of the wallet in BTC
      "immature_balance": xxxxxx,   (numeric) the total immature balance of the wallet in BTC
      "txcount": xxxxxxx,           (numeric) the total number of transactions in the wallet
      "keypoololdest": xxxxxx,      (numeric) the timestamp (seconds since Unix epoch) of the oldest pre-generated key in the key pool
      "keypoolsize": xxxx,          (numeric) how many new keys are pre-generated
      "unlocked_until": ttt,        (numeric) the timestamp in seconds since epoch (midnight Jan 1 1970 GMT) that the wallet is unlocked for transfers, or 0 if the wallet is locked
      "paytxfee": x.xxxx,           (numeric) the transaction fee configuration, set in BTC/kB
      "hdmasterkeyid": "<hash160>", (string) the Hash160 of the HD master pubkey
    }
### importaddress "address" ( "label" rescan p2sh )
    Adds a script (in hex) or address that can be watched as if it were in your wallet but cannot be used to spend.
    添加一个脚本（十六进制）或可以观看的地址，就好像它在你的钱包里但不能用来消费。

    Arguments:
    1. "script"           (string, required) The hex-encoded script (or address)
    2. "label"            (string, optional, default="") An optional label
    3. rescan               (boolean, optional, default=true) Rescan the wallet for transactions
    4. p2sh                 (boolean, optional, default=false) Add the P2SH version of the script as well
    
    Note: This call can take minutes to complete if rescan is true.
    If you have the full public key, you should call importpubkey instead of this.
    
    Note: If you import a non-standard raw script in hex form, outputs sending to it will be treated
    as change, and not show up in many RPCs.
### importprivkey "bitcoinprivkey" ( "label" rescan )
    Adds a private key (as returned by dumpprivkey) to your wallet.
    将一个私钥（由dumpprivkey返回）添加到您的钱包。

    Arguments:
    1. "bitcoinprivkey"   (string, required) The private key (see dumpprivkey)
    2. "label"            (string, optional, default="") An optional label
    3. rescan               (boolean, optional, default=true) Rescan the wallet for transactions
    
    Note: This call can take minutes to complete if rescan is true.
### importprunedfunds
    Imports funds without rescan. Corresponding address or script must previously be included in wallet. Aimed towards pruned wallets. The end-user is responsible to import additional transactions that subsequently spend the imported outputs or rescan after the point in the blockchain the transaction is included.
    无需重新扫描即可进口资金。 之前必须在钱包中包含相应的地址或脚本。 针对修剪过的钱包。 最终用户负责导入随后花费导入的输出的其他事务，或者在包含事务的区块链中的点之后重新扫描。
    
    Arguments:
    1. "rawtransaction" (string, required) A raw transaction in hex funding an already-existing address in wallet
    2. "txoutproof"     (string, required) The hex output from gettxoutproof that contains the transaction
### importpubkey "pubkey" ( "label" rescan )
    Adds a public key (in hex) that can be watched as if it were in your wallet but cannot be used to spend.
    添加一个可以观看的公钥（十六进制），就好像它在钱包里但不能用来消费。
    
    Arguments:
    1. "pubkey"           (string, required) The hex-encoded public key
    2. "label"            (string, optional, default="") An optional label
    3. rescan               (boolean, optional, default=true) Rescan the wallet for transactions
    
    Note: This call can take minutes to complete if rescan is true.
### importwallet "filename"
    Imports keys from a wallet dump file (see dumpwallet).
    从钱包转储文件导入密钥（请参阅dumpwallet）。

    Arguments:
    1. "filename"    (string, required) The wallet file
### keypoolrefill ( newsize )
    Fills the keypool.
    填写键池。

    Arguments
    1. newsize     (numeric, optional, default=100) The new keypool size
### listaccounts ( minconf includeWatchonly)
    DEPRECATED. Returns Object that has account names as keys, account balances as values.
    已过时。 返回将帐户名称作为键，帐户余额作为值的对象。

    Arguments:
    1. minconf          (numeric, optional, default=1) Only include transactions with at least this many confirmations
    2. includeWatchonly (bool, optional, default=false) Include balances in watchonly addresses (see 'importaddress')
    
    Result:
    {                      (json object where keys are account names, and values are numeric balances
      "account": x.xxx,  (numeric) The property name is the account name, and the value is the total balance for the account.
      ...
    }
### listaddressgroupings
    Lists groups of addresses which have had their common ownership
    made public by common use as inputs or as the resulting change
    in past transactions
    列出具有共同所有权的地址组
    通过共同使用作为输入或由此产生的变化公开
    在过去的交易中
    
    Result:
    [
      [
        [
          "bitcoinaddress",     (string) The bitcoin address
          amount,                 (numeric) The amount in BTC
          "account"             (string, optional) The account (DEPRECATED)
        ]
        ,...
      ]
      ,...
    ]
### listlockunspent
    Returns list of temporarily unspendable outputs.
    See the lockunspent call to lock and unlock transactions for spending.
    返回暂时不可连接的输出列表。
    请参阅lockunspent调用以锁定和解锁支出的交易。
    
    Result:
    [
      {
        "txid" : "transactionid",     (string) The transaction id locked
        "vout" : n                      (numeric) The vout value
      }
      ,...
    ]
### listreceivedbyaccount ( minconf includeempty includeWatchonly)
    DEPRECATED. List balances by account.
    已过时。 按帐户列出余额。

    Arguments:
    1. minconf      (numeric, optional, default=1) The minimum number of confirmations before payments are included.
    2. includeempty (bool, optional, default=false) Whether to include accounts that haven't received any payments.
    3. includeWatchonly (bool, optional, default=false) Whether to include watchonly addresses (see 'importaddress').
    
    Result:
    [
      {
        "involvesWatchonly" : true,   (bool) Only returned if imported addresses were involved in transaction
        "account" : "accountname",  (string) The account name of the receiving account
        "amount" : x.xxx,             (numeric) The total amount received by addresses with this account
        "confirmations" : n,          (numeric) The number of confirmations of the most recent transaction included
        "label" : "label"           (string) A comment for the address/transaction, if any
      }
      ,...
    ]
### listreceivedbyaddress ( minconf includeempty includeWatchonly)
    List balances by receiving address.
    通过接收地址列出余额。

    Arguments:
    1. minconf       (numeric, optional, default=1) The minimum number of confirmations before payments are included.
    2. includeempty  (bool, optional, default=false) Whether to include addresses that haven't received any payments.
    3. includeWatchonly (bool, optional, default=false) Whether to include watchonly addresses (see 'importaddress').
    
    Result:
    [
      {
        "involvesWatchonly" : true,        (bool) Only returned if imported addresses were involved in transaction
        "address" : "receivingaddress",  (string) The receiving address
        "account" : "accountname",       (string) DEPRECATED. The account of the receiving address. The default account is "".
        "amount" : x.xxx,                  (numeric) The total amount in BTC received by the address
        "confirmations" : n,               (numeric) The number of confirmations of the most recent transaction included
        "label" : "label"                (string) A comment for the address/transaction, if any
      }
      ,...
    ]
### listsinceblock ( "blockhash" target-confirmations includeWatchonly)
    Get all transactions in blocks since block [blockhash], or all transactions if omitted
    从块[blockhash]获取块中的所有事务，或者省略所有事务
    
    Arguments:
    1. "blockhash"   (string, optional) The block hash to list transactions since
    2. target-confirmations:    (numeric, optional) The confirmations required, must be 1 or more
    3. includeWatchonly:        (bool, optional, default=false) Include transactions to watchonly addresses (see 'importaddress')
    Result:
    {
      "transactions": [
        "account":"accountname",       (string) DEPRECATED. The account name associated with the transaction. Will be "" for the default account.
        "address":"bitcoinaddress",    (string) The bitcoin address of the transaction. Not present for move transactions (category = move).
        "category":"send|receive",     (string) The transaction category. 'send' has negative amounts, 'receive' has positive amounts.
        "amount": x.xxx,          (numeric) The amount in BTC. This is negative for the 'send' category, and for the 'move' category for moves 
                                              outbound. It is positive for the 'receive' category, and for the 'move' category for inbound funds.
        "vout" : n,               (numeric) the vout value
        "fee": x.xxx,             (numeric) The amount of the fee in BTC. This is negative and only available for the 'send' category of transactions.
        "confirmations": n,       (numeric) The number of confirmations for the transaction. Available for 'send' and 'receive' category of transactions.
        "blockhash": "hashvalue",     (string) The block hash containing the transaction. Available for 'send' and 'receive' category of transactions.
        "blockindex": n,          (numeric) The index of the transaction in the block that includes it. Available for 'send' and 'receive' category of transactions.
        "blocktime": xxx,         (numeric) The block time in seconds since epoch (1 Jan 1970 GMT).
        "txid": "transactionid",  (string) The transaction id. Available for 'send' and 'receive' category of transactions.
        "time": xxx,              (numeric) The transaction time in seconds since epoch (Jan 1 1970 GMT).
        "timereceived": xxx,      (numeric) The time received in seconds since epoch (Jan 1 1970 GMT). Available for 'send' and 'receive' category of transactions.
        "comment": "...",       (string) If a comment is associated with the transaction.
        "label" : "label"       (string) A comment for the address/transaction, if any
        "to": "...",            (string) If a comment to is associated with the transaction.
      ],
      "lastblock": "lastblockhash"     (string) The hash of the last block
    }
### listtransactions ( "account" count from includeWatchonly)
    Returns up to 'count' most recent transactions skipping the first 'from' transactions for account 'account'.
    最多返回'计数'最近的交易，跳过帐户“帐户”的第一个“来自”交易。

    Arguments:
    1. "account"    (string, optional) DEPRECATED. The account name. Should be "*".
    2. count          (numeric, optional, default=10) The number of transactions to return
    3. from           (numeric, optional, default=0) The number of transactions to skip
    4. includeWatchonly (bool, optional, default=false) Include transactions to watchonly addresses (see 'importaddress')
    
    Result:
    [
      {
        "account":"accountname",       (string) DEPRECATED. The account name associated with the transaction. 
                                                    It will be "" for the default account.
        "address":"bitcoinaddress",    (string) The bitcoin address of the transaction. Not present for 
                                                    move transactions (category = move).
        "category":"send|receive|move", (string) The transaction category. 'move' is a local (off blockchain)
                                                    transaction between accounts, and not associated with an address,
                                                    transaction id or block. 'send' and 'receive' transactions are 
                                                    associated with an address, transaction id and block details
        "amount": x.xxx,          (numeric) The amount in BTC. This is negative for the 'send' category, and for the
                                             'move' category for moves outbound. It is positive for the 'receive' category,
                                             and for the 'move' category for inbound funds.
        "vout": n,                (numeric) the vout value
        "fee": x.xxx,             (numeric) The amount of the fee in BTC. This is negative and only available for the 
                                             'send' category of transactions.
        "abandoned": xxx          (bool) 'true' if the transaction has been abandoned (inputs are respendable).
        "confirmations": n,       (numeric) The number of confirmations for the transaction. Available for 'send' and 
                                             'receive' category of transactions. Negative confirmations indicate the
                                             transaction conflicts with the block chain
        "trusted": xxx            (bool) Whether we consider the outputs of this unconfirmed transaction safe to spend.
        "blockhash": "hashvalue", (string) The block hash containing the transaction. Available for 'send' and 'receive'
                                              category of transactions.
        "blockindex": n,          (numeric) The index of the transaction in the block that includes it. Available for 'send' and 'receive'
                                              category of transactions.
        "blocktime": xxx,         (numeric) The block time in seconds since epoch (1 Jan 1970 GMT).
        "txid": "transactionid", (string) The transaction id. Available for 'send' and 'receive' category of transactions.
        "time": xxx,              (numeric) The transaction time in seconds since epoch (midnight Jan 1 1970 GMT).
        "timereceived": xxx,      (numeric) The time received in seconds since epoch (midnight Jan 1 1970 GMT). Available 
                                              for 'send' and 'receive' category of transactions.
        "comment": "...",       (string) If a comment is associated with the transaction.
        "label": "label"        (string) A comment for the address/transaction, if any
        "otheraccount": "accountname",  (string) For the 'move' category of transactions, the account the funds came 
                                              from (for receiving funds, positive amounts), or went to (for sending funds,
                                              negative amounts).
        "bip125-replaceable": "yes|no|unknown"  (string) Whether this transaction could be replaced due to BIP125 (replace-by-fee);
                                                         may be unknown for unconfirmed transactions not in the mempool
      }
    ]
### lockunspent unlock ([{"txid":"txid","vout":n},...])
    Updates list of temporarily unspendable outputs.
    Temporarily lock (unlock=false) or unlock (unlock=true) specified transaction outputs.
    If no transaction outputs are specified when unlocking then all current locked transaction outputs are unlocked.
    A locked transaction output will not be chosen by automatic coin selection, when spending bitcoins.
    Locks are stored in memory only. Nodes start with zero locked outputs, and the locked output list
    is always cleared (by virtue of process exit) when a node stops or fails.
    Also see the listunspent call
    更新暂时不可靠输出的列表。
    临时锁定（unlock = false）或解锁（unlock = true）指定的事务输出。
    如果在解锁时未指定任何事务输出，则解锁所有当前锁定的事务输出。
    在使用比特币时，自动硬币选择不会选择锁定的交易输出。
    锁仅存储在内存中。 节点以零锁定输出和锁定输出列表开始
    当节点停止或失败时，始终清除（通过进程退出）。
    另请参阅listunspent调用
    Arguments:
    1. unlock            (boolean, required) Whether to unlock (true) or lock (false) the specified transactions
    2. "transactions"  (string, optional) A json array of objects. Each object the txid (string) vout (numeric)
         [           (json array of json objects)
           {
             "txid":"id",    (string) The transaction id
             "vout": n         (numeric) The output number
           }
           ,...
         ]
    
    Result:
    true|false    (boolean) Whether the command was successful or not
### lockunspent unlock ([{"txid":"txid","vout":n},...])
    Updates list of temporarily unspendable outputs.
    Temporarily lock (unlock=false) or unlock (unlock=true) specified transaction outputs.
    If no transaction outputs are specified when unlocking then all current locked transaction outputs are unlocked.
    A locked transaction output will not be chosen by automatic coin selection, when spending bitcoins.
    Locks are stored in memory only. Nodes start with zero locked outputs, and the locked output list
    is always cleared (by virtue of process exit) when a node stops or fails.
    Also see the listunspent call
    更新暂时不可靠输出的列表。
    临时锁定（unlock = false）或解锁（unlock = true）指定的事务输出。
    如果在解锁时未指定任何事务输出，则解锁所有当前锁定的事务输出。
    在使用比特币时，自动硬币选择不会选择锁定的交易输出。
    锁仅存储在内存中。 节点以零锁定输出和锁定输出列表开始
    当节点停止或失败时，始终清除（通过进程退出）。
    另请参阅listunspent调用
    Arguments:
    1. unlock            (boolean, required) Whether to unlock (true) or lock (false) the specified transactions
    2. "transactions"  (string, optional) A json array of objects. Each object the txid (string) vout (numeric)
         [           (json array of json objects)
           {
             "txid":"id",    (string) The transaction id
             "vout": n         (numeric) The output number
           }
           ,...
         ]
    
    Result:
    true|false    (boolean) Whether the command was successful or not
### move "fromaccount" "toaccount" amount ( minconf "comment" )
    DEPRECATED. Move a specified amount from one account in your wallet to another.
    已过时。 将指定金额从钱包中的一个帐户移动到另一个帐户。
    
    Arguments:
    1. "fromaccount"   (string, required) The name of the account to move funds from. May be the default account using "".
    2. "toaccount"     (string, required) The name of the account to move funds to. May be the default account using "".
    3. amount            (numeric) Quantity of BTC to move between accounts.
    4. minconf           (numeric, optional, default=1) Only use funds with at least this many confirmations.
    5. "comment"       (string, optional) An optional comment, stored in the wallet only.
    
    Result:
    true|false           (boolean) true if successful.
### removeprunedfunds
    Deletes the specified transaction from the wallet. Meant for use with pruned wallets and as a companion to importprunedfunds. This will effect wallet balances.
    从钱包中删除指定的事务。 适用于修剪过的钱包，也可作为进口商品的伴侣。 这将影响钱包余额。

    Arguments:
    1. "txid"           (string, required) The hex-encoded id of the transaction you are deleting
### sendfrom "fromaccount" "tobitcoinaddress" amount ( minconf "comment" "comment-to" )
    DEPRECATED (use sendtoaddress). Sent an amount from an account to a bitcoin address.
    DEPRECATED（使用sendtoaddress）。 从帐户向比特币地址发送金额。

    Arguments:
    1. "fromaccount"       (string, required) The name of the account to send funds from. May be the default account using "".
    2. "tobitcoinaddress"  (string, required) The bitcoin address to send funds to.
    3. amount                (numeric or string, required) The amount in BTC (transaction fee is added on top).
    4. minconf               (numeric, optional, default=1) Only use funds with at least this many confirmations.
    5. "comment"           (string, optional) A comment used to store what the transaction is for. 
                                         This is not part of the transaction, just kept in your wallet.
    6. "comment-to"        (string, optional) An optional comment to store the name of the person or organization 
                                         to which you're sending the transaction. This is not part of the transaction, 
                                         it is just kept in your wallet.
    
    Result:
    "transactionid"        (string) The transaction id.
### sendmany "fromaccount" {"address":amount,...} ( minconf "comment" ["address",...] )
    Send multiple times. Amounts are double-precision floating point numbers.
    发送多次。 数量是双精度浮点数。

    Arguments:
    1. "fromaccount"         (string, required) DEPRECATED. The account to send the funds from. Should be "" for the default account
    2. "amounts"             (string, required) A json object with addresses and amounts
        {
          "address":amount   (numeric or string) The bitcoin address is the key, the numeric amount (can be string) in BTC is the value
          ,...
        }
    3. minconf                 (numeric, optional, default=1) Only use the balance confirmed at least this many times.
    4. "comment"             (string, optional) A comment
    5. subtractfeefromamount   (string, optional) A json array with addresses.
                               The fee will be equally deducted from the amount of each selected address.
                               Those recipients will receive less bitcoins than you enter in their corresponding amount field.
                               If no addresses are specified here, the sender pays the fee.
        [
          "address"            (string) Subtract fee from this address
          ,...
        ]
    
    Result:
    "transactionid"          (string) The transaction id for the send. Only 1 transaction is created regardless of 
                                        the number of addresses.
### sendtoaddress "bitcoinaddress" amount ( "comment" "comment-to" subtractfeefromamount )
    Send an amount to a given address.
    将金额发送到给定地址。

    Arguments:
    1. "bitcoinaddress"  (string, required) The bitcoin address to send to.
    2. "amount"      (numeric or string, required) The amount in BTC to send. eg 0.1
    3. "comment"     (string, optional) A comment used to store what the transaction is for. 
                                 This is not part of the transaction, just kept in your wallet.
    4. "comment-to"  (string, optional) A comment to store the name of the person or organization 
                                 to which you're sending the transaction. This is not part of the 
                                 transaction, just kept in your wallet.
    5. subtractfeefromamount  (boolean, optional, default=false) The fee will be deducted from the amount being sent.
                                 The recipient will receive less bitcoins than you enter in the amount field.
    
    Result:
    "transactionid"  (string) The transaction id.
### setaccount "bitcoinaddress" "account"
    DEPRECATED. Sets the account associated with the given address.
    已过时。 设置与给定地址关联的帐户。

    Arguments:
    1. "bitcoinaddress"  (string, required) The bitcoin address to be associated with an account.
    2. "account"         (string, required) The account to assign the address to.
### settxfee amount
    Set the transaction fee per kB. Overwrites the paytxfee parameter.
    设置每kB的交易费用。 覆盖paytxfee参数。

    Arguments:
    1. amount         (numeric or string, required) The transaction fee in BTC/kB
    
    Result
    true|false        (boolean) Returns true if successful
### signmessage "bitcoinaddress" "message"
    Sign a message with the private key of an address
    使用地址的私钥对邮件进行签名

    Arguments:
    1. "bitcoinaddress"  (string, required) The bitcoin address to use for the private key.
    2. "message"         (string, required) The message to create a signature of.
    
    Result:
    "signature"          (string) The signature of the message encoded in base 64
