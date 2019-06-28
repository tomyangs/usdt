## Blockchain命令
### clearmempool
    Clears the memory pool and returns a list of the removed transactions.
    清除内存池并返回已删除事务的列表

    Result:
    [ (json array of string)
        "hash" (string) The transaction hash
        ,...
    ]

### getbestblockhash
    Returns the hash of the best (tip) block in the longest block chain.
    返回最长块链中最佳（tip）块的哈希值。
    
    Result
    "hex"    (string) the block hash hex encoded
    
### getblock "hash" ( verbose )
    If verbose is false, returns a string that is serialized, hex-encoded data for block 'hash'.
    If verbose is true, returns an Object with information about block <hash>.
    
    如果verbose为false，则返回序列化的字符串，块'hash'的十六进制编码数据。
    如果verbose为true，则返回一个Object，其中包含有关block <hash>的信息。

    Arguments:
    1. "hash"          (string, required) The block hash
    2. verbose           (boolean, optional, default=true) true for a json object, false for the hex encoded data
    
    Result (for verbose = true):
    {
      "hash" : "hash",     (string) the block hash (same as provided)
      "confirmations" : n,   (numeric) The number of confirmations, or -1 if the block is not on the main chain
      "size" : n,            (numeric) The block size
      "strippedsize" : n,    (numeric) The block size excluding witness data
      "weight" : n           (numeric) The block weight (BIP 141)
      "height" : n,          (numeric) The block height or index
      "version" : n,         (numeric) The block version
      "versionHex" : "00000000", (string) The block version formatted in hexadecimal
      "merkleroot" : "xxxx", (string) The merkle root
      "tx" : [               (array of string) The transaction ids
         "transactionid"     (string) The transaction id
         ,...
      ],
      "time" : ttt,          (numeric) The block time in seconds since epoch (Jan 1 1970 GMT)
      "mediantime" : ttt,    (numeric) The median block time in seconds since epoch (Jan 1 1970 GMT)
      "nonce" : n,           (numeric) The nonce
      "bits" : "1d00ffff", (string) The bits
      "difficulty" : x.xxx,  (numeric) The difficulty
      "chainwork" : "xxxx",  (string) Expected number of hashes required to produce the chain up to this block (in hex)
      "previousblockhash" : "hash",  (string) The hash of the previous block
      "nextblockhash" : "hash"       (string) The hash of the next block
    }
    
    Result (for verbose=false):
    "data"             (string) A string that is serialized, hex-encoded data for block 'hash'.

### getblockchaininfo
    Returns an object containing various state info regarding block chain processing.
    返回包含有关块链处理的各种状态信息的对象。
    Result:
    {
      "chain": "xxxx",        (string) current network name as defined in BIP70 (main, test, regtest)
      "blocks": xxxxxx,         (numeric) the current number of blocks processed in the server
      "headers": xxxxxx,        (numeric) the current number of headers we have validated
      "bestblockhash": "...", (string) the hash of the currently best block
      "difficulty": xxxxxx,     (numeric) the current difficulty
      "mediantime": xxxxxx,     (numeric) median time for the current best block
      "verificationprogress": xxxx, (numeric) estimate of verification progress [0..1]
      "chainwork": "xxxx"     (string) total amount of work in active chain, in hexadecimal
      "pruned": xx,             (boolean) if the blocks are subject to pruning
      "pruneheight": xxxxxx,    (numeric) lowest-height complete block stored
      "softforks": [            (array) status of softforks in progress
         {
            "id": "xxxx",        (string) name of softfork
            "version": xx,         (numeric) block version
            "enforce": {           (object) progress toward enforcing the softfork rules for new-version blocks
               "status": xx,       (boolean) true if threshold reached
               "found": xx,        (numeric) number of blocks with the new version found
               "required": xx,     (numeric) number of blocks required to trigger
               "window": xx,       (numeric) maximum size of examined window of recent blocks
            },
            "reject": { ... }      (object) progress toward rejecting pre-softfork blocks (same fields as "enforce")
         }, ...
      ],
      "bip9_softforks": {          (object) status of BIP9 softforks in progress
         "xxxx" : {                (string) name of the softfork
            "status": "xxxx",    (string) one of "defined", "started", "locked_in", "active", "failed"
            "bit": xx,             (numeric) the bit (0-28) in the block version field used to signal this softfork (only for "started" status)
            "startTime": xx,       (numeric) the minimum median time past of a block at which the bit gains its meaning
            "timeout": xx          (numeric) the median time past of a block at which the deployment is considered failed if not yet locked in
         }
      }
    }

### getblockcount
    Returns the number of blocks in the longest block chain.
    返回最长块链中的块数。
    Result:
    n    (numeric) The current block count
    
### getblockhash index
    Returns hash of block in best-block-chain at index provided.
    返回在提供的索引处的最佳块链中的块的散列。

    Arguments:
    1. index         (numeric, required) The block index

    Result:
    "hash"         (string) The block hash
    
### getblockheader "hash" ( verbose )
    If verbose is false, returns a string that is serialized, hex-encoded data for blockheader 'hash'.
    If verbose is true, returns an Object with information about blockheader <hash>.
    
    如果verbose为false，则返回序列化的字符串，用于blockheader'hash'的十六进制编码数据。
    如果verbose为true，则返回一个Object，其中包含有关blockheader <hash>的信息。
    
    Arguments:
    1. "hash"          (string, required) The block hash
    2. verbose           (boolean, optional, default=true) true for a json object, false for the hex encoded data
    
    Result (for verbose = true):
    {
      "hash" : "hash",     (string) the block hash (same as provided)
      "confirmations" : n,   (numeric) The number of confirmations, or -1 if the block is not on the main chain
      "height" : n,          (numeric) The block height or index
      "version" : n,         (numeric) The block version
      "versionHex" : "00000000", (string) The block version formatted in hexadecimal
      "merkleroot" : "xxxx", (string) The merkle root
      "time" : ttt,          (numeric) The block time in seconds since epoch (Jan 1 1970 GMT)
      "mediantime" : ttt,    (numeric) The median block time in seconds since epoch (Jan 1 1970 GMT)
      "nonce" : n,           (numeric) The nonce
      "bits" : "1d00ffff", (string) The bits
      "difficulty" : x.xxx,  (numeric) The difficulty
      "previousblockhash" : "hash",  (string) The hash of the previous block
      "nextblockhash" : "hash",      (string) The hash of the next block
      "chainwork" : "0000...1f3"     (string) Expected number of hashes required to produce the current chain (in hex)
    }
    
    Result (for verbose=false):
    "data"             (string) A string that is serialized, hex-encoded data for block 'hash'.

### getchaintips
    Return information about all known tips in the block tree, including the main chain as well as orphaned branches.
    返回有关块树中所有已知提示的信息，包括主链和孤立分支。

    Result:
    [
      {
        "height": xxxx,         (numeric) height of the chain tip
        "hash": "xxxx",         (string) block hash of the tip
        "branchlen": 0          (numeric) zero for main chain
        "status": "active"      (string) "active" for the main chain
      },
      {
        "height": xxxx,
        "hash": "xxxx",
        "branchlen": 1          (numeric) length of branch connecting the tip to the main chain
        "status": "xxxx"        (string) status of the chain (active, valid-fork, valid-headers, headers-only, invalid)
      }
    ]
    Possible values for status:
    1.  "invalid"               This branch contains at least one invalid block
    2.  "headers-only"          Not all blocks for this branch are available, but the headers are valid
    3.  "valid-headers"         All blocks are available for this branch, but they were never fully validated
    4.  "valid-fork"            This branch is not part of the active chain, but is fully validated
    5.  "active"                This is the tip of the active main chain, which is certainly valid

### getdifficulty
    Returns the proof-of-work difficulty as a multiple of the minimum difficulty.
    将工作量证明难度作为最小难度的倍数返回。

    Result:
    n.nnn       (numeric) the proof-of-work difficulty as a multiple of the minimum difficulty.
    
### getmempoolancestors txid (verbose)
    If txid is in the mempool, returns all in-mempool ancestors.
    如果txid在mempool中，则返回所有in-mempool祖先。

    Arguments:
    1. "txid"                   (string, required) The transaction id (must be in mempool)
    2. verbose                  (boolean, optional, default=false) true for a json object, false for array of transaction ids
    
    Result (for verbose=false):
    [                       (json array of strings)
      "transactionid"           (string) The transaction id of an in-mempool ancestor transaction
      ,...
    ]
    
    Result (for verbose=true):
    {                           (json object)
      "transactionid" : {       (json object)
        "size" : n,             (numeric) transaction size in bytes
        "fee" : n,              (numeric) transaction fee in BTC
        "modifiedfee" : n,      (numeric) transaction fee with fee deltas used for mining priority
        "time" : n,             (numeric) local time transaction entered pool in seconds since 1 Jan 1970 GMT
        "height" : n,           (numeric) block height when transaction entered pool
        "startingpriority" : n, (numeric) priority when transaction entered pool
        "currentpriority" : n,  (numeric) transaction priority now
        "descendantcount" : n,  (numeric) number of in-mempool descendant transactions (including this one)
        "descendantsize" : n,   (numeric) size of in-mempool descendants (including this one)
        "descendantfees" : n,   (numeric) modified fees (see above) of in-mempool descendants (including this one)
        "ancestorcount" : n,    (numeric) number of in-mempool ancestor transactions (including this one)
        "ancestorsize" : n,     (numeric) size of in-mempool ancestors (including this one)
        "ancestorfees" : n,     (numeric) modified fees (see above) of in-mempool ancestors (including this one)
        "depends" : [           (array) unconfirmed transactions used as inputs for this transaction
            "transactionid",    (string) parent transaction id
           ... ]
      }, ...
    }
    
###getmempooldescendants txid (verbose)

    If txid is in the mempool, returns all in-mempool descendants.
    如果txid在mempool中，则返回所有in-mempool后代。
    
    Arguments:
    1. "txid"                   (string, required) The transaction id (must be in mempool)
    2. verbose                  (boolean, optional, default=false) true for a json object, false for array of transaction ids
    
    Result (for verbose=false):
    [                       (json array of strings)
      "transactionid"           (string) The transaction id of an in-mempool descendant transaction
      ,...
    ]
    
    Result (for verbose=true):
    {                           (json object)
      "transactionid" : {       (json object)
        "size" : n,             (numeric) transaction size in bytes
        "fee" : n,              (numeric) transaction fee in BTC
        "modifiedfee" : n,      (numeric) transaction fee with fee deltas used for mining priority
        "time" : n,             (numeric) local time transaction entered pool in seconds since 1 Jan 1970 GMT
        "height" : n,           (numeric) block height when transaction entered pool
        "startingpriority" : n, (numeric) priority when transaction entered pool
        "currentpriority" : n,  (numeric) transaction priority now
        "descendantcount" : n,  (numeric) number of in-mempool descendant transactions (including this one)
        "descendantsize" : n,   (numeric) size of in-mempool descendants (including this one)
        "descendantfees" : n,   (numeric) modified fees (see above) of in-mempool descendants (including this one)
        "ancestorcount" : n,    (numeric) number of in-mempool ancestor transactions (including this one)
        "ancestorsize" : n,     (numeric) size of in-mempool ancestors (including this one)
        "ancestorfees" : n,     (numeric) modified fees (see above) of in-mempool ancestors (including this one)
        "depends" : [           (array) unconfirmed transactions used as inputs for this transaction
            "transactionid",    (string) parent transaction id
           ... ]
      }, ...
    }
    
### getmempoolentry txid
    Returns mempool data for given transaction
    返回给定事务的mempool数据

    Arguments:
    1. "txid"                   (string, required) The transaction id (must be in mempool)
    
    Result:
    {                           (json object)
        "size" : n,             (numeric) transaction size in bytes
        "fee" : n,              (numeric) transaction fee in BTC
        "modifiedfee" : n,      (numeric) transaction fee with fee deltas used for mining priority
        "time" : n,             (numeric) local time transaction entered pool in seconds since 1 Jan 1970 GMT
        "height" : n,           (numeric) block height when transaction entered pool
        "startingpriority" : n, (numeric) priority when transaction entered pool
        "currentpriority" : n,  (numeric) transaction priority now
        "descendantcount" : n,  (numeric) number of in-mempool descendant transactions (including this one)
        "descendantsize" : n,   (numeric) size of in-mempool descendants (including this one)
        "descendantfees" : n,   (numeric) modified fees (see above) of in-mempool descendants (including this one)
        "ancestorcount" : n,    (numeric) number of in-mempool ancestor transactions (including this one)
        "ancestorsize" : n,     (numeric) size of in-mempool ancestors (including this one)
        "ancestorfees" : n,     (numeric) modified fees (see above) of in-mempool ancestors (including this one)
        "depends" : [           (array) unconfirmed transactions used as inputs for this transaction
            "transactionid",    (string) parent transaction id
           ... ]
    }
    
### getmempoolinfo
    Returns details on the active state of the TX memory pool.
    返回有关TX内存池活动状态的详细信息。

    Result:
    {
      "size": xxxxx,               (numeric) Current tx count
      "bytes": xxxxx,              (numeric) Sum of all tx sizes
      "usage": xxxxx,              (numeric) Total memory usage for the mempool
      "maxmempool": xxxxx,         (numeric) Maximum memory usage for the mempool
      "mempoolminfee": xxxxx       (numeric) Minimum fee for tx to be accepted
    }

### getrawmempool
    Returns all transaction ids in memory pool as a json array of string transaction ids.
    将内存池中的所有事务ID作为字符串事务ID的json数组返回。

    Arguments:
    1. verbose           (boolean, optional, default=false) true for a json object, false for array of transaction ids
    
    Result: (for verbose = false):
    [                     (json array of string)
      "transactionid"     (string) The transaction id
      ,...
    ]
    
    Result: (for verbose = true):
    {                           (json object)
      "transactionid" : {       (json object)
        "size" : n,             (numeric) transaction size in bytes
        "fee" : n,              (numeric) transaction fee in BTC
        "modifiedfee" : n,      (numeric) transaction fee with fee deltas used for mining priority
        "time" : n,             (numeric) local time transaction entered pool in seconds since 1 Jan 1970 GMT
        "height" : n,           (numeric) block height when transaction entered pool
        "startingpriority" : n, (numeric) priority when transaction entered pool
        "currentpriority" : n,  (numeric) transaction priority now
        "descendantcount" : n,  (numeric) number of in-mempool descendant transactions (including this one)
        "descendantsize" : n,   (numeric) size of in-mempool descendants (including this one)
        "descendantfees" : n,   (numeric) modified fees (see above) of in-mempool descendants (including this one)
        "ancestorcount" : n,    (numeric) number of in-mempool ancestor transactions (including this one)
        "ancestorsize" : n,     (numeric) size of in-mempool ancestors (including this one)
        "ancestorfees" : n,     (numeric) modified fees (see above) of in-mempool ancestors (including this one)
        "depends" : [           (array) unconfirmed transactions used as inputs for this transaction
            "transactionid",    (string) parent transaction id
           ... ]
      }, ...
    }
    
### gettxout "txid" n ( includemempool )
    Returns details about an unspent transaction output.
    返回有关未使用的事务输出的详细信息。

    Arguments:
    1. "txid"       (string, required) The transaction id
    2. n              (numeric, required) vout number
    3. includemempool  (boolean, optional) Whether to include the mempool
    
    Result:
    {
      "bestblock" : "hash",    (string) the block hash
      "confirmations" : n,       (numeric) The number of confirmations
      "value" : x.xxx,           (numeric) The transaction value in BTC
      "scriptPubKey" : {         (json object)
         "asm" : "code",       (string) 
         "hex" : "hex",        (string) 
         "reqSigs" : n,          (numeric) Number of required signatures
         "type" : "pubkeyhash", (string) The type, eg pubkeyhash
         "addresses" : [          (array of string) array of bitcoin addresses
            "bitcoinaddress"     (string) bitcoin address
            ,...
         ]
      },
      "version" : n,            (numeric) The version
      "coinbase" : true|false   (boolean) Coinbase or not
    }

### gettxoutproof ["txid",...] ( blockhash )
    Returns a hex-encoded proof that "txid" was included in a block.
    返回一个十六进制编码的证明，其中“txid”包含在一个块中。

    NOTE: By default this function only works sometimes. This is when there is an
    unspent output in the utxo for this transaction. To make it always work,
    you need to maintain a transaction index, using the -txindex command line option or
    specify the block in which the transaction is included manually (by blockhash).
    
    Return the raw transaction data.
    
    Arguments:
    1. "txids"       (string) A json array of txids to filter
        [
          "txid"     (string) A transaction hash
          ,...
        ]
    2. "block hash"  (string, optional) If specified, looks for txid in the block with this hash
    
    Result:
    "data"           (string) A string that is a serialized, hex-encoded data for the proof. 
    
### gettxoutsetinfo
    Returns statistics about the unspent transaction output set.
    返回有关未使用的事务输出集的统计信息。

    Note this call may take some time.
    
    Result:
    {
      "height":n,     (numeric) The current block height (index)
      "bestblock": "hex",   (string) the best block hash hex
      "transactions": n,      (numeric) The number of transactions
      "txouts": n,            (numeric) The number of output transactions
      "bytes_serialized": n,  (numeric) The serialized size
      "hash_serialized": "hash",   (string) The serialized hash
      "total_amount": x.xxx          (numeric) The total amount
    }
### gettxoutsetinfo
    Returns statistics about the unspent transaction output set.
    返回有关未使用的事务输出集的统计信息。

    Note this call may take some time.
    
    Result:
    {
      "height":n,     (numeric) The current block height (index)
      "bestblock": "hex",   (string) the best block hash hex
      "transactions": n,      (numeric) The number of transactions
      "txouts": n,            (numeric) The number of output transactions
      "bytes_serialized": n,  (numeric) The serialized size
      "hash_serialized": "hash",   (string) The serialized hash
      "total_amount": x.xxx          (numeric) The total amount
    }
### verifychain ( checklevel numblocks )
    Verifies blockchain database.
    验证区块链数据库。

    Arguments:
    1. checklevel   (numeric, optional, 0-4, default=3) How thorough the block verification is.
    2. numblocks    (numeric, optional, default=6, 0=all) The number of blocks to check.
    
    Result:
    true|false       (boolean) Verified or not
### verifytxoutproof "proof"
    Verifies that a proof points to a transaction in a block, returning the transaction it commits to
    and throwing an RPC error if the block is not in our best chain
    验证证明指向块中的事务，返回它提交的事务 如果块不在我们最好的链中，则抛出RPC错误
    
    Arguments:
    1. "proof"    (string, required) The hex-encoded proof generated by gettxoutproof
    
    Result:
    ["txid"]      (array, strings) The txid(s) which the proof commits to, or empty array if the proof is invalid
