## Generating
### generate numblocks ( maxtries )
    Mine up to numblocks blocks immediately (before the RPC call returns)
    矿立即采取numblocks块（在RPC调用返回之前）

    Arguments:
    1. numblocks    (numeric, required) How many blocks are generated immediately.
    2. maxtries     (numeric, optional) How many iterations to try (default = 1000000).
    
    Result
    [ blockhashes ]     (array) hashes of blocks generated
### generatetoaddress numblocks address (maxtries)
    Mine blocks immediately to a specified address (before the RPC call returns)
    矿块立即发送给指定的地址（在RPC 调用返回之前）
    Arguments:
    1. numblocks    (numeric, required) How many blocks are generated immediately.
    2. address    (string, required) The address to send the newly generated bitcoin to.
    3. maxtries     (numeric, optional) How many iterations to try (default = 1000000).
    
    Result
    [ blockhashes ]     (array) hashes of blocks generated
