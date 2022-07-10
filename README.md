# Test coverage for TON SDK Manifest

- Cryptography
    - sha256
        - basic checks:
            - [different length](https://github.com/ton-blockchain/ton/blob/eb86234a1120fc3f9c6b390f4471cfd92b875044/tdutils/test/crypto.cpp#L179)
            - [expected values](https://github.com/ton-blockchain/ton/blob/eb86234a1120fc3f9c6b390f4471cfd92b875044/tdutils/test/crypto.cpp#L243)
        - check usage in cell hash computation
    - crc32c
        - check mistakes in signed/unsigned conversions
        - wrong crc32c table
            - [expected values](https://github.com/ton-blockchain/ton/blob/eb86234a1120fc3f9c6b390f4471cfd92b875044/tdutils/test/crypto.cpp#L278)
            - checks in `serialized_boc#b5ee9c72.crc32c:has_crc32c?uint32`
                - [serialization](https://github.com/andreypfau/ton-kotlin/blob/363504ec96e821d4178dc09a2234377fd02808e9/ton-boc/src/commonMain/kotlin/org/ton/boc/BagOfCellsUtils.kt#L169)
                - deserialization
            - checks in `serialized_boc_idx_crc32c#acc3a728.crc32c:uint32`
                - serialization
                - deserialization
    - crc32
        - check mistakes in signed/unsigned conversions
        - wrong crc32 table
            - check usage in TL constructor prefixes
                - serialization boxed types
                - deserialization boxed types
            - check usage in TL-B constructor prefixes
                - serialization
                - deserialization
    - crc16
        - check mistakes in signed/unsigned conversions
        - wrong crc16 table
            - [basic checks](https://github.com/andreypfau/ton-kotlin/blob/main/ton-crypto/src/commonTest/kotlin/org/ton/crypto/Crc16Test.kt)
            - check usage in `liteServer.runSmcMethod` function in Lite-API for method names
            - check usage in user-friendly (base64) address parsing
  - hex
      - check `UPPER CASE` and `lower case`
      - check invalid characters
      - [basic checks with expected values](https://github.com/andreypfau/ton-kotlin/blob/main/ton-crypto/src/commonTest/kotlin/org/ton/crypto/HexTest.kt)
      - incomplete hex (`AA_`) aka Fift-hex should be implemented as a separate function that reuses basic
        hex-function
  - ed25519 keypair
      - [check expected keypair generation](https://github.com/andreypfau/ton-kotlin/blob/6e2f83fc80f19466c84289c40e6de396b7320752/ton-smartcontract/src/jvmTest/kotlin/org/ton/smartcontract/wallet/v1/WalletV1R3Test.kt#L42)
- BitString
    - [BitString creation](https://github.com/andreypfau/ton-kotlin/blob/363504ec96e821d4178dc09a2234377fd02808e9/ton-bitstring/src/commonTest/kotlin/org/ton/bitstring/BitStringTest.kt#L11)
    - [BitString concatenation without shifting](https://github.com/andreypfau/ton-kotlin/blob/363504ec96e821d4178dc09a2234377fd02808e9/ton-bitstring/src/commonTest/kotlin/org/ton/bitstring/BitStringTest.kt#L44)
    - [BitString concatenation with shifting](https://github.com/andreypfau/ton-kotlin/blob/363504ec96e821d4178dc09a2234377fd02808e9/ton-bitstring/src/commonTest/kotlin/org/ton/bitstring/BitStringTest.kt#L57)
    - [BitString concatenation with double-shifting](https://github.com/andreypfau/ton-kotlin/blob/363504ec96e821d4178dc09a2234377fd02808e9/ton-bitstring/src/commonTest/kotlin/org/ton/bitstring/BitStringTest.kt#L68)
    - [BitString.toString() on a zero number](https://github.com/andreypfau/ton-kotlin/blob/363504ec96e821d4178dc09a2234377fd02808e9/ton-bitstring/src/commonTest/kotlin/org/ton/bitstring/BitStringTest.kt#L107)
    - [check BitString.size in `0..1023`](https://github.com/andreypfau/ton-kotlin/blob/3b02ad6c729e14fff8c023801062f9505cc6ed4a/ton-bitstring/src/commonMain/kotlin/org/ton/bitstring/ByteBackedBitString.kt#L167)
    - [BitString assertions for all tests](https://github.com/andreypfau/ton-kotlin/blob/363504ec96e821d4178dc09a2234377fd02808e9/ton-bitstring/src/commonTest/kotlin/org/ton/bitstring/BitStringTest.kt#L114)
        - [from binary == from hex](https://github.com/andreypfau/ton-kotlin/blob/363504ec96e821d4178dc09a2234377fd02808e9/ton-bitstring/src/commonTest/kotlin/org/ton/bitstring/BitStringTest.kt#L119)
        - [from binary toString() == from hex toString()](https://github.com/andreypfau/ton-kotlin/blob/363504ec96e821d4178dc09a2234377fd02808e9/ton-bitstring/src/commonTest/kotlin/org/ton/bitstring/BitStringTest.kt#L121)
        - [from binary toBooleanArray() == from hex toBooleanArray()](https://github.com/andreypfau/ton-kotlin/blob/363504ec96e821d4178dc09a2234377fd02808e9/ton-bitstring/src/commonTest/kotlin/org/ton/bitstring/BitStringTest.kt#L125)
        - [from binary toByteArray() == from hex toByteArray()](https://github.com/andreypfau/ton-kotlin/blob/363504ec96e821d4178dc09a2234377fd02808e9/ton-bitstring/src/commonTest/kotlin/org/ton/bitstring/BitStringTest.kt#L126)
        - [from binary .size == from hex .size](https://github.com/andreypfau/ton-kotlin/blob/363504ec96e821d4178dc09a2234377fd02808e9/ton-bitstring/src/commonTest/kotlin/org/ton/bitstring/BitStringTest.kt#L127)
        - [from binary with the specified size == from hex with the specified size](https://github.com/andreypfau/ton-kotlin/blob/363504ec96e821d4178dc09a2234377fd02808e9/ton-bitstring/src/commonTest/kotlin/org/ton/bitstring/BitStringTest.kt#L128)
        - [created from byte array](https://github.com/andreypfau/ton-kotlin/blob/363504ec96e821d4178dc09a2234377fd02808e9/ton-bitstring/src/commonTest/kotlin/org/ton/bitstring/BitStringTest.kt#L132)
        - [created from boolean array](https://github.com/andreypfau/ton-kotlin/blob/363504ec96e821d4178dc09a2234377fd02808e9/ton-bitstring/src/commonTest/kotlin/org/ton/bitstring/BitStringTest.kt#L133)
- Cell
    - check `cell.bits.size` in `0..1023`
    - check references count
        - check for `ORDINARY(-1)` in `0..4`
        - check for `PRUNED(1)` == `0`
        - check for `LIBRARY_REFERENCE(2)` in `1..4`
        - check for `MERKLE_PROOF(3)` == `1`
        - check for `MERKLE_UPDATE(4)` == `2`
    - [check representation bytes](https://github.com/andreypfau/ton-kotlin/blob/363504ec96e821d4178dc09a2234377fd02808e9/ton-cell/src/commonMain/kotlin/org/ton/cell/DataCell.kt#L97)
        - [check computation of max depth](https://github.com/andreypfau/ton-kotlin/blob/363504ec96e821d4178dc09a2234377fd02808e9/ton-cell/src/commonTest/kotlin/org/ton/cell/CellTest.kt#L9)
        - [check computation of cell descriptors d1,d2](https://github.com/andreypfau/ton-kotlin/blob/363504ec96e821d4178dc09a2234377fd02808e9/ton-cell/src/commonTest/kotlin/org/ton/cell/CellTest.kt#L81)
            - [check reference descriptor (d1)](https://github.com/andreypfau/ton-kotlin/blob/363504ec96e821d4178dc09a2234377fd02808e9/ton-cell/src/commonMain/kotlin/org/ton/cell/DataCell.kt#L86)
            - [check bits descriptor (d2)](https://github.com/andreypfau/ton-kotlin/blob/363504ec96e821d4178dc09a2234377fd02808e9/ton-cell/src/commonMain/kotlin/org/ton/cell/DataCell.kt#L89)
        - [check augment bytes](https://github.com/andreypfau/ton-kotlin/blob/363504ec96e821d4178dc09a2234377fd02808e9/ton-cell/src/commonMain/kotlin/org/ton/cell/DataCell.kt#L92)
    - check computation of cell hash
        - usage of sha256
- CellSlice
    - check `.endParse()` throws exception if `bitsPosition != bits.size`
    - check `.loadRef()` underflow if `refsPosition > refs.size`
    - check `.loadBit()` use-cases
        - check bits overflow if `bitsPosition == bits.size`
    - check `.loadBits(bits: Int)` use-cases
        - check bits overflow
        - check that `bits` in `0..1023` range
    - check `.loadInt(bits: Int)`
        - check bits overflow
        - check that `bits` in `0..257` range
    - check `.loadUint(bits: Int)`
        - check bits overflow
        - check returns positive integer
        - check that `bits` in `0..257` range
    - check `.toString()` returns string in `x{FF},2` format where `2` equals `refs.size`
- CellBuilder
    - check `beginCell().endCell()` equals empty cell
    - check `beginCell().storeBit(true).endCell()` size equals 1
    - check storing BitString with size divide by 8
    - check storing BitString with size divide by 4
    - check storing BitString with size not divide by 4
    - check storing more than 1023 bits
    - [check storing ints](https://github.com/andreypfau/ton-kotlin/blob/addf79aeed62e87da74049aa1e720f96a791edde/ton-cell/src/commonTest/kotlin/org/ton/cell/CellBuilderTest.kt#L50)
- Bag-of-Cells
    - [check Bag-of-Cells (de)serialization equals](https://github.com/andreypfau/ton-kotlin/blob/addf79aeed62e87da74049aa1e720f96a791edde/ton-boc/src/jvmTest/kotlin/BagOfCellsTest.kt#L12)
    - check Bag-of-Cells crc32c checksum calculation
    - [check that cell offset indexes greater than previous](https://github.com/andreypfau/ton-kotlin/blob/addf79aeed62e87da74049aa1e720f96a791edde/ton-boc/src/commonMain/kotlin/org/ton/boc/BagOfCellsUtils.kt#L71)
    - [check cell references count in `0..4`](https://github.com/andreypfau/ton-kotlin/blob/addf79aeed62e87da74049aa1e720f96a791edde/ton-boc/src/commonMain/kotlin/org/ton/boc/BagOfCellsUtils.kt#L95)
    - [check invalid cell reference indexes](https://github.com/andreypfau/ton-kotlin/blob/addf79aeed62e87da74049aa1e720f96a791edde/ton-boc/src/commonMain/kotlin/org/ton/boc/BagOfCellsUtils.kt#L121)
    - [check cell depth less than 1024](https://github.com/andreypfau/ton-kotlin/blob/6e2f83fc80f19466c84289c40e6de396b7320752/ton-boc/src/commonMain/kotlin/org/ton/boc/CachedBagOfCells.kt#L62)
    - [check cell order algorithm. TODO: make unit-tests for illegal cell order](https://github.com/andreypfau/ton-kotlin/blob/6e2f83fc80f19466c84289c40e6de396b7320752/ton-boc/src/commonMain/kotlin/org/ton/boc/CachedBagOfCells.kt#L89)
- Addresses
    - [check raw address parsing](https://github.com/andreypfau/ton-kotlin/blob/6e2f83fc80f19466c84289c40e6de396b7320752/ton-block/src/commonTest/kotlin/org/ton/block/MsgAddressIntTest.kt#L10)
    - [check user-friendly (base64) address parsing](https://github.com/andreypfau/ton-kotlin/blob/6e2f83fc80f19466c84289c40e6de396b7320752/ton-block/src/commonTest/kotlin/org/ton/block/MsgAddressIntTest.kt#L28)
        - [check crc16 checksum calculation & validation](https://github.com/andreypfau/ton-kotlin/blob/6e2f83fc80f19466c84289c40e6de396b7320752/ton-block/src/commonMain/kotlin/org/ton/block/AddrStd.kt#L133)
    - [check .toString() raw address](https://github.com/andreypfau/ton-kotlin/blob/6e2f83fc80f19466c84289c40e6de396b7320752/ton-block/src/commonTest/kotlin/org/ton/block/MsgAddressIntTest.kt#L104)
    - [check .toString() user-friendly (base64) address](https://github.com/andreypfau/ton-kotlin/blob/6e2f83fc80f19466c84289c40e6de396b7320752/ton-block/src/commonTest/kotlin/org/ton/block/MsgAddressIntTest.kt#L140)
- Coins
    - String to BigInt (nanocoins) coins conversion
    - BigInt (nanocoins) to string conversion
- Smart Contract interfaces
    - Wallet Contracts
        - [tonweb test-cases](https://github.com/toncenter/tonweb/blob/master/test/typescripted/wallet-contract.test.js)
        - WalletV1R3
            - [check expected StateInit cell generation](https://github.com/andreypfau/ton-kotlin/blob/6e2f83fc80f19466c84289c40e6de396b7320752/ton-smartcontract/src/jvmTest/kotlin/org/ton/smartcontract/wallet/v1/WalletV1R3Test.kt#L49)
            - [check expected address calculation](https://github.com/andreypfau/ton-kotlin/blob/6e2f83fc80f19466c84289c40e6de396b7320752/ton-smartcontract/src/jvmTest/kotlin/org/ton/smartcontract/wallet/v1/WalletV1R3Test.kt#L63)
            - [check expected non-bounceable address calculation](https://github.com/andreypfau/ton-kotlin/blob/6e2f83fc80f19466c84289c40e6de396b7320752/ton-smartcontract/src/jvmTest/kotlin/org/ton/smartcontract/wallet/v1/WalletV1R3Test.kt#L72)
            - [check expected bounceable address calculation](https://github.com/andreypfau/ton-kotlin/blob/6e2f83fc80f19466c84289c40e6de396b7320752/ton-smartcontract/src/jvmTest/kotlin/org/ton/smartcontract/wallet/v1/WalletV1R3Test.kt#L81)
            - [check expected external message cell for initialization generation](https://github.com/andreypfau/ton-kotlin/blob/6e2f83fc80f19466c84289c40e6de396b7320752/ton-smartcontract/src/jvmTest/kotlin/org/ton/smartcontract/wallet/v1/WalletV1R3Test.kt#L90)
            - [check expected Bag-of-Cell for deploy generation](https://github.com/andreypfau/ton-kotlin/blob/6e2f83fc80f19466c84289c40e6de396b7320752/ton-smartcontract/src/jvmTest/kotlin/org/ton/smartcontract/wallet/v1/WalletV1R3Test.kt#L104)
            - [check expected external message cell with wallet commentary generation](https://github.com/andreypfau/ton-kotlin/blob/6e2f83fc80f19466c84289c40e6de396b7320752/ton-smartcontract/src/jvmTest/kotlin/org/ton/smartcontract/wallet/v1/WalletV1R3Test.kt#L128)
            - [check expected Bag-of-Cell for transfer generation](https://github.com/andreypfau/ton-kotlin/blob/6e2f83fc80f19466c84289c40e6de396b7320752/ton-smartcontract/src/jvmTest/kotlin/org/ton/smartcontract/wallet/v1/WalletV1R3Test.kt#L143)
            - [example usage](https://github.com/andreypfau/ton-kotlin/blob/6e2f83fc80f19466c84289c40e6de396b7320752/ton-smartcontract/src/jvmTest/kotlin/org/ton/smartcontract/wallet/v1/WalletV1R3Example.kt#L19)
        - WalletV2R2
            - same cases like in WalletV1R3
        - WalletV3R2
            - same cases like in WalletV1R3
        - WalletV4R2
            - same cases like in WalletV1R3
            - [tonweb test-cases](https://github.com/toncenter/tonweb/blob/master/src/test-wallet4.js)
    - NFT
        - [tonweb test-cases](https://github.com/toncenter/tonweb/blob/master/src/test-nft.js)
    - Jettons
        - [tonweb test-cases](https://github.com/toncenter/tonweb/blob/master/src/test-jetton.js)
    - DNS
        - [tonweb test-cases](https://github.com/toncenter/tonweb/blob/master/src/test-dns.js)
    - Payments
        - [tonweb test-cases](https://github.com/toncenter/tonweb/blob/master/src/test-payments.js)
