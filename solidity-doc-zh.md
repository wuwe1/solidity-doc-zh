## 目录
- [目录](#目录)
- [介绍](#介绍)
- [安全相关的总结](#安全相关的总结)
    - [solidity 中有几种转移 ether 的方式？](#solidity-中有几种转移-ether-的方式)
    - [哪些操作可以消耗掉所有的gas](#哪些操作可以消耗掉所有的gas)
- [evm](#evm)
    - [mload(0x40)是什么意思?](#mload0x40是什么意思)
- [internals 内部原理](#internals-内部原理)
    - [calldata的布局](#calldata的布局)
    - [memory的布局](#memory的布局)
        - [与storage布局不同的地方](#与storage布局不同的地方)
    - [storage的布局](#storage的布局)
        - [mapping和动态数组](#mapping和动态数组)
        - [JSON输出](#json输出)
    - [清除变量](#清除变量)
    - [源映射](#源映射)
    - [优化器](#优化器)
- [Contract ABI Specification 合约编码规范](#contract-abi-specification-合约编码规范)
    - [基本设计](#基本设计)
    - [函数选择器](#函数选择器)
    - [参数编码](#参数编码)
    - [将solidity类型映射为ABI类型](#将solidity类型映射为abi类型)
    - [编码的设计准则](#编码的设计准则)
    - [ABI编码的正式规范](#abi编码的正式规范)
    - [函数选择器和参数编码](#函数选择器和参数编码)
    - [使用动态类型](#使用动态类型)
    - [事件](#事件)
    - [JSON](#json)
    - [严格编码模式](#严格编码模式)
    - [非标准紧凑模式](#非标准紧凑模式)
    - [索引事件参数的编码](#索引事件参数的编码)
- [Types 类型](#types-类型)
    - [值类型有哪些](#值类型有哪些)
    - [引用类型有哪些](#引用类型有哪些)
    - [有理数字面量和整数字面量如何表示](#有理数字面量和整数字面量如何表示)
    - [字符串字面量](#字符串字面量)
    - [Unicode字面量怎么表示](#unicode字面量怎么表示)
    - [地址字面量如何表示](#地址字面量如何表示)
    - [数组字面量如何表示](#数组字面量如何表示)
    - [移位操作有啥细节](#移位操作有啥细节)
    - [如何表示一个数组类型 Arrays aka. 如何在 storage 中分配一个数组](#如何表示一个数组类型-arrays-aka-如何在-storage-中分配一个数组)
    - [如何访问数组中的元素](#如何访问数组中的元素)
    - [如何在内存中分配一个数组](#如何在内存中分配一个数组)
    - [bytes byte[] bytes32 有啥区别](#bytes-byte-bytes32-有啥区别)
    - [solidity 里能操作 string 吗](#solidity-里能操作-string-吗)
    - [如何声明一个mapping](#如何声明一个mapping)
    - [delete 关键字如何使用](#delete-关键字如何使用)
    - [internal external public 之间的区别](#internal-external-public-之间的区别)
    - [solidity 里的引用类型有哪些](#solidity-里的引用类型有哪些)
    - [不同数据存放位置的变量是如何互相赋值的](#不同数据存放位置的变量是如何互相赋值的)
    - [solidity中的基本类型之间是如何进行转换的](#solidity中的基本类型之间是如何进行转换的)
    - [solidity中字面量和基本类型之间是如何转换的](#solidity中字面量和基本类型之间是如何转换的)
- [Uints and Globally Available Variables 单位和全局可用变量](#uints-and-globally-available-variables-单位和全局可用变量)
    - [solidity中有哪些ether单位](#solidity中有哪些ether单位)
    - [solidity中有哪些时间单位](#solidity中有哪些时间单位)
    - [abi编码和解码函数有哪些](#abi编码和解码函数有哪些)
    - [有哪些关于错误处理的关键字](#有哪些关于错误处理的关键字)
    - [类似keccak256的密码学函数有哪些](#类似keccak256的密码学函数有哪些)
    - [this是啥](#this是啥)
    - [selfdestruct(address payable recipient)有啥细节](#selfdestructaddress-payable-recipient有啥细节)
    - [type关键字是啥](#type关键字是啥)
- [Expressions and Control Structures 表达式和控制结构](#expressions-and-control-structures-表达式和控制结构)
    - [如何进行函数调用](#如何进行函数调用)
    - [如何用new创建一个合约](#如何用new创建一个合约)
    - [啥是create2](#啥是create2)
    - [如何进行解构赋值](#如何进行解构赋值)
    - [给引用类型赋值会有什么行为](#给引用类型赋值会有什么行为)
    - [unchecked关键字是啥](#unchecked关键字是啥)
    - [异常处理如何进行的](#异常处理如何进行的)
    - [assert和require有什么区别](#assert和require有什么区别)
    - [revert关键字如何使用](#revert关键字如何使用)
    - [try catch 如何使用](#try-catch-如何使用)
- [Contracts 合约](#contracts-合约)
    - [library 中为啥不能有状态变量](#library-中为啥不能有状态变量)
    - [constant 和 immutable 有什么区别](#constant-和-immutable-有什么区别)
    - [定义在合约外的函数和定义在合约内的函数有啥区别](#定义在合约外的函数和定义在合约内的函数有啥区别)
    - [函数参数](#函数参数)
    - [返回变量](#返回变量)
    - [view 修饰符如何使用](#view-修饰符如何使用)
    - [pure 修饰符如何使用](#pure-修饰符如何使用)
    - [receive函数是个啥函数](#receive函数是个啥函数)
    - [fallback函数是个啥函数](#fallback函数是个啥函数)
    - [函数重载](#函数重载)
    - [重载解析和参数匹配](#重载解析和参数匹配)
    - [事件](#事件-1)
    - [继承](#继承)
    - [函数重写](#函数重写)
    - [修饰符重写](#修饰符重写)
    - [构造器](#构造器)
    - [基构造器的参数](#基构造器的参数)
    - [多继承和线性化](#多继承和线性化)
    - [继承相同名的成员的不同种类](#继承相同名的成员的不同种类)
    - [抽象合约](#抽象合约)
    - [接口](#接口)
    - [库 Libraries](#库-libraries)
    - [库的调用保护](#库的调用保护)
    - [using for](#using-for)
- [Inline Assembly 内联汇编](#inline-assembly-内联汇编)
    - [访问外部的变量，函数和库](#访问外部的变量函数和库)
    - [solidity里的约定](#solidity里的约定)
- [Contract Metadata 合约元数据](#contract-metadata-合约元数据)
    - [字节码中的元数据哈希的编码](#字节码中的元数据哈希的编码)


## 介绍
这是[wuwe1](wuwe1.com)翻译的Solidity文档，基本按照[solidity官方文档](https://docs.soliditylang.org/en/v0.8.0/index.html)的顺序翻译，但是添加了诸如EVM和一些和安全相关的一些章节，这些章节会随着我的学习慢慢丰富起来。翻译力求通顺，我尽量做到指代是明确的。我认为不管是针对以太坊生态的安全还是开发的学习，solidity都是很重要的一个工具，solidity本身是对EVM的一层抽象，如果在阅读文档的时候读到了一些和EVM相关的知识无法理解，最好还是先去补充一下EVM的相关知识。

我推荐的EVM学习博客列在下面

- [Diving Into The Ethereum VM Part 1 - Introduction to the EVM assembly code.](https://blog.qtum.org/diving-into-the-ethereum-vm-6e8d5d2f3c30)
- [Diving Into The Ethereum VM Part 2 - How fixed-length data types are represented.](https://medium.com/@hayeah/diving-into-the-ethereum-vm-part-2-storage-layout-bc5349cb11b7)
- [Diving Into The Ethereum VM Part 3 - How dynamic data types are represented.](https://medium.com/@hayeah/diving-into-the-ethereum-vm-the-hidden-costs-of-arrays-28e119f04a9b)
- [Diving Into The Ethereum VM Part 4 - How ABI Encodes External Method Calling.](https://medium.com/@hayeah/how-to-decipher-a-smart-contract-method-call-8ee980311603)
- [Diving Into The Ethereum VM Part 5 - The Smart Contract Creation Process](https://medium.com/@hayeah/diving-into-the-ethereum-vm-part-5-the-smart-contract-creation-process-cb7b6133b855)
- [Diving Into The Ethereum VM Part 6 - How Solidity Events Are Implemented](https://blog.qtum.org/how-solidity-events-are-implemented-diving-into-the-ethereum-vm-part-6-30e07b3037b9)

- [Deconstructing a Solidity Contract — Part I: Introduction](https://blog.openzeppelin.com/deconstructing-a-solidity-contract-part-i-introduction-832efd2d7737/)
- [Deconstructing a Solidity Contract — Part II: Creation vs. Runtime](https://blog.openzeppelin.com/deconstructing-a-solidity-contract-part-ii-creation-vs-runtime-6b9d60ecb44c/)
- [Deconstructing a Solidity Contract — Part III: The Function Selector](https://blog.openzeppelin.com/deconstructing-a-solidity-contract-part-iii-the-function-selector-6a9b6886ea49/)
- [Deconstructing a Solidity Contract — Part IV: Function Wrappers](https://blog.openzeppelin.com/deconstructing-a-solidity-contract-part-iv-function-wrappers-d8e46672b0ed/)
- [Deconstructing a Solidity Contract — Part V: Function Bodies](https://blog.openzeppelin.com/deconstructing-a-solidity-contract-part-v-function-bodies-2d19d4bef8be/)
- [Deconstructing a Solidity Contract — Part VI: The Metadata Hash](https://blog.openzeppelin.com/deconstructing-a-solidity-contract-part-vi-the-swarm-hash-70f069e22aef/)

目前来说，文档翻译自`0.8.0`版本的文档，其中每个条目的翻译情况如下

- BASICS 基本信息
    - Introduction to Smart Contracts 智能合约简介: 不打算翻译
    - Installing the Solidity Compiler 安装solidity编译器: 不打算翻译
    - Solidity by Example 例子: 不打算翻译
- LANGUAGE DESCRIPTION 语言描述
    - Layout of a Solidity Source File 源文件布局: 可能会翻译
    - Structure of a Contract 合约的结构: 可能会翻译
    - Types 类型: 完成翻译✅
    - Uints and Globally Available Variables 单位和全局可用变量: 完成翻译✅
    - Expressions and Control Structures 表达式和控制结构: 完成翻译✅
    - Contract 合约: 完成翻译✅
    - Inline Assembley 内联汇编: 完成翻译✅
    - Cheatsheet: 可能加入notion参考手册大礼包
    - Language Grammar 语言语法: 想写编译器的同学自己看吧
- INTERNALS 内部原理
    - Layout of State Variables in Storage 状态变量的布局: 完成翻译✅
    - Layout of Memory 内存的布局: 完成翻译✅
    - Layout of Call Data 调用数据的布局: 完成翻译✅
    - Cleaning Up Variables 清理变量: 完成翻译✅
    - Source Mapping 源映射: 完成翻译✅
    - The Optimiser 优化器: 完成翻译✅
    - Contract Metadata 合约元信息: 完成翻译✅
    - Contract ABI Specification 合约ABI规范: 完成翻译✅
- ADDITIONAL MATERIAL 额外资料
    - Solidity v0.5.0 Breaking Changes: 准备翻
    - Solidity v0.6.0 Breaking Changes: 准备翻
    - Solidity v0.7.0 Breaking Changes: 准备翻
    - Solidity v0.8.0 Breaking Changes: 准备翻
    - NatSpec Format: 准备翻
    - Security Considerations: 准备翻
    - Resources: 不打算翻译
    - Using the compiler: 准备翻
    - Yul: 准备翻
    - Style Guide: 准备翻
    - Common Patterns: 准备翻
    - List of Known Bugs: 准备翻
    - Contributing: 准备翻
    - Solidity Brand Guide: 不打算翻译
    - Keyword Index: 不打算翻译


## 安全相关的总结
### solidity 中有几种转移 ether 的方式？
`<address payable>.transfer(uint256 amount)`: 当发送失败时会 revert, 只会传递2300 Gas 供调用，防止重入

`<address payable>.send(uint256 amount) returns (bool)`: 当发送失败时会返回 false, 只会传递2300 Gas 供调用，防止重入

`<address>.call(bytes memory) returns (bool, bytes memory)`: 当发送失败时会返回 false, 传递所有可用 Gas 供调用，不能有效防止重入

`selfdestruct(address)`: 这个就不是很常见了，但是确实可以转移ether, 可以给任意的地址打钱

最后一条和solidity关系不大，通过指定`coinbase transaction`的接受者为某个合约地址，也可以给合约打钱，也就是挖矿的收款人的意思


### 哪些操作可以消耗掉所有的gas
导致Panic异常的操作，比如`assert(false)`

见[异常处理如何进行的](#异常处理如何进行的)


## evm
[我整理的OPCODE表格](https://www.notion.so/EVM-OPCODES-YUL-INSTRUCTIONS-b65ebd1477f54ce1b77d93ee7ddfdeab)

> evm 是 ethereum virtual machine 的缩写，solidity 的编译目标是 evm,所有的 solidity 代码在经过编译变成字节码后，都会交给 evm 来执行，evm 中包含了许多 opcode,这些 opcode 能执行不同的操作，你可以查看[geth 的具体实现](https://github.com/ethereum/go-ethereum/blob/61469cfeaf2a6d0b1598afbaf35dd2d1872604ce/core/vm/interpreter.go), 诸如基本的算数运算以及以太坊特有的 gas 查询操作和 call 操作等等都囊括在了 evm 的 opcode 中

> yul 则是一门特殊的语言，你可以在 solidity 中写它来获得更加细粒度的控制，也就是 assembly{}，花括号中的语言，其中每个关键字都对应一个 opcode


### mload(0x40)是什么意思?
evm 中的 memory 里的 0x40 这个 slot 是一个特殊的 slot, 被称为`free memory pointer` 他会指向最新被分配的内存的最后一个位置，所以你每次写入内存的时候只要用这个`pointer`就可以往新的内存里写东西了

细心的你应该可以看到所有的EVM字节码都是由`6080604052`开始的

对这一小段字节码反汇编之后就是

```
00000: PUSH1 0x80
00002: PUSH1 0x40
00004: MSTORE
```

也就是`mstore(0x40, 0x80)`，即在内存的`0x40`存放32个字节的值，这个值是`0x80`

也就是说每次自由内存指针都会初始化为`0x80`。那么在`0x00`到`0x40`之间有啥呢，答案是是啥都没有，这是solidity保留来进行哈希计算的，在使用mapping和其他的动态类型的时候会用到。


## internals 内部原理
### calldata的布局
函数调用的输入数据的格式是由ABI规范定义的，ABI规范要求参数被填充为32字节的倍数。`internal function calls内部函数调用`使用不同的约定

合约的构造器的参数直接追加在合约的代码的末尾，也是ABI编码的。构造器可以通过硬编码的偏移访问他们，而不是通过`codesize`操作码，因为在往代码追加数据的时候这个肯定会变

### memory的布局
solidity保留4个32字节的slot

- `0x00-0x3f`: 暂存空间 scratch space
- `0x40-0x5f`: 自由内存指针
- `0x60-0x7f`: 零slot

零slot被用作动态内存数组的初始值且永远不应该被写入

solidity总是把新的对象放在自由内存指针而且内存永远不会被释放(这之后可能会改)

solidity中的内存数组的元素总是占用32字节的倍数(这对`byte[]`成立但是对`bytes`和`string`不成立)。多维内存数组是指向内存数组的指针。动态数组的长度被存放在数组的第一个slot, 第一个slot后面跟着数组元素

solidity中有些操作可能会使用大于64个字节的临时内存，因此暂存空间可能放不下。那solidity就会把数据暂存在自由内存指针指向的地方，考虑到这个暂存数据生命周期很短，指针不会更新。内存可能会清零也可能不会，所以不要假设自由内存数组会指向一个清零了的内存

利用`msize`来获取一个肯定清零了的内存空间看起来是个好主意，但是用这样的非临时的指针的同时又不更新自由内存指针会导致预料外的结果


#### 与storage布局不同的地方
下面的数组在storage里占用32个字节(1个slot), 但是在memory里占用128个字节(4个32字节的元素)

```typescript
uint8[4] a;
```

下面的结构体在storage中占用96个字节(3个slot), 但是在memory里占用128个字节(4个32字节的元素)

```typescript
struct S {
    uint a;
    uint b;
    uint8 c;
    uint8 d;
}
```


### storage的布局
静态长度变量(除了mapping和动态长度数组类型)在storage是从位置0开始连续存放的。多个连续的小于32个字节的元素在可能的情况下塞进(packed)一个storage slot里面，塞进slot的操作遵从以下规则

- storage slot的第一个元素低序对齐
- 基本类型只用他们需要的字节来存放
- 如果基本类型不能全塞进storage slot剩余的部分，就会被移到下一个slot里
- 结构体和数组数据总是从一个新的slot开始并且占用一整个slot(但是结构体或者数组内部的元素会根据上面的规则存放`tightly packed`)

对于使用了继承的合约，状态变量的顺序由合约的C3线性化顺序决定。如果满足上面的条件，不同合约的状态变量会共享一个`storage slot`

当使用小于32个字节的元素时，你的合约的gas消耗可能会更高。这是因为EVM是操作32个字节。因此，如果元素小于32个字节，EVM会用更多的操作来把这个元素的大小从32个字节变成想要的大小

只有在处理storage的值的时候使用比32字节的参数才是有好处的，因为编译器会把多个元素打包进一个storage slot里，因此，会把多个读写操作组合成一个操作。当处理函数参数或者memory的值的时候，这就没啥好处了，因为编译器不会把这些值打包

为了让EVM去优化这些，你得让storage变量的struct成员是按照可以被`tightly packed`的顺序来书写的，举个例子，把storage变量声明成`uint128, uint128, uint256`而不是`uint128, uint256, uint128`，因为第一个方式只会占用2个slot，第二个会占用3个

#### mapping和动态数组
由于其大小的不可预测，mapping和动态大小的数组类型使用Keccak-256哈希来找到值或数组数据的起始位置。这些起始位置总是`full stack slots`。

根据上述规则，mapping或动态数组本身会在某个位置`p`上占用storage中的一个slot(对于mapping的mapping或者数组的数组会递归的使用上面的规则)。对于动态数组而言，这些slot存放数组中的元素的个数(字节数组和字符串是个例外)。对于mapping而言，这些slot是不会使用的(但是需要占用，这样才能确保两个连续定义的mapping会使用不同的哈希分布)。数组(array)数据定位在`keccak256(p)`，而mapping键`k`对应的值定位在`keccak256(k . p)`，`.`代表合并字符串的操作。如果这个值是非基础类型，位置则还要再加上一个`keccak(k . p)`的偏移

所以对于接下来的合约代码`data[4][9].b`的位置是`keccak256(uint256(9) . keccak256(uint256(4) . uint256(1))) + 1`， `uint256(1)`指的是data这个变量是第二个slot，最后的`+1`是指结构体`S`的`b`成员是第二个slot

```typescript
contract C {
    struct S { uitn a; uint b; }
    uint x;
    mapping(uint => mapping(uint => S)) data;
}
```

`bytes`和`string`的编码是一样的。对于短的字节数组，数据会和长度一起存放。特别的，如果数据最多31个字节长，这个数据混存在高序字节(左对齐)然后低序字节存放`length * 2`。对于长度大于等于32个字节的字节数组，主slot存放`length * 2 + 1`，数据存放在`keccak256(slot)`里。这意味着你可以通过奇偶(最后一位是1还是0，是1就是奇，是0就是偶)来辨别这个数组是长的还是短的


#### JSON输出
合约的storage布局可以通过标准JSON接口来请求。输出是一个包含两个键的JSON对象，`storage`和`types`。`storage`对象是一个数组，数组里的每个元素的格数如下

```json
{
    "astId": 2,
    "contract": "fileA:A",
    "label": "x",
    "offset": 0,
    "slot": "0",
    "type": "t_uint256"
}
```

上面的例子是来自名为`fileA`的`源代码单元 source uint`的`contract A { uint x; }`的storage布局

- `astId`状态变量声明的抽象语法树节点的id
- `contract`是包含了路径作为前缀的合约的名字
- `label`是状态变量的名字
- `offset`是storage slot里由编码确定的偏移，单位是字节
- `slot`是状态变量开始或存放的storage slot。这个数字可能会非常大，所以它的JSON值是字符串
- `type`是一个用来当变量的类型信息的键的标识符

上面例子里的`type`的值`t_uint256`代表`types`里的一个元素，格式如下

```json
{
    "encoding": "inplace",
    "label": "uint256",
    "numberOfBytes": "32",
}
```

- `encoding`是指storage中这个数据是如何编码的，有下面几个可能的值
    - `inplace`: 数据在storage中连续存放
    - `mapping`: 基于keccak-256哈希的方法
    - `dynamic_array`: 基于keccak-256哈希的方法
    - `bytes`: 根据数据大小要么是一个slot要么是基于keccak-256哈希的方法
- `label`是标准类型名
- `numberOfBytes`是需要使用的字节的数量，如果`numberOfBytes > 32`那就是说不止一个slot会被用

一些类型会有除了上面四个之外的别的信息。mapping有`key`和`value`类型，数组有`base`类型，结构体会列出它的`members`

> 合约的storage布局的JSON输出格式目前还被认为是实验性的

下面一个包含了值类型和引用类型，编码打包了的类型和嵌套类型的例子

```typescript
contract A {
    struct S {
        uint128 a;
        uint128 b;
        uint[2] staticArray;
        uint[] dynArray;
    }

    uint x;
    uint y;
    S s;
    address addr;
    mapping (uint => mapping (address => bool)) map;
    uint[] array;
    string s1;
    bytes b1;
}
```

```json
"storageLayout": {
  "storage": [
    {
      "astId": 14,
      "contract": "fileA:A",
      "label": "x",
      "offset": 0,
      "slot": "0",
      "type": "t_uint256"
    },
    {
      "astId": 16,
      "contract": "fileA:A",
      "label": "y",
      "offset": 0,
      "slot": "1",
      "type": "t_uint256"
    },
    {
      "astId": 18,
      "contract": "fileA:A",
      "label": "s",
      "offset": 0,
      "slot": "2",
      "type": "t_struct(S)12_storage"
    },
    {
      "astId": 20,
      "contract": "fileA:A",
      "label": "addr",
      "offset": 0,
      "slot": "6",
      "type": "t_address"
    },
    {
      "astId": 26,
      "contract": "fileA:A",
      "label": "map",
      "offset": 0,
      "slot": "7",
      "type": "t_mapping(t_uint256,t_mapping(t_address,t_bool))"
    },
    {
      "astId": 29,
      "contract": "fileA:A",
      "label": "array",
      "offset": 0,
      "slot": "8",
      "type": "t_array(t_uint256)dyn_storage"
    },
    {
      "astId": 31,
      "contract": "fileA:A",
      "label": "s1",
      "offset": 0,
      "slot": "9",
      "type": "t_string_storage"
    },
    {
      "astId": 33,
      "contract": "fileA:A",
      "label": "b1",
      "offset": 0,
      "slot": "10",
      "type": "t_bytes_storage"
    }
  ],
  "types": {
    "t_address": {
      "encoding": "inplace",
      "label": "address",
      "numberOfBytes": "20"
    },
    "t_array(t_uint256)2_storage": {
      "base": "t_uint256",
      "encoding": "inplace",
      "label": "uint256[2]",
      "numberOfBytes": "64"
    },
    "t_array(t_uint256)dyn_storage": {
      "base": "t_uint256",
      "encoding": "dynamic_array",
      "label": "uint256[]",
      "numberOfBytes": "32"
    },
    "t_bool": {
      "encoding": "inplace",
      "label": "bool",
      "numberOfBytes": "1"
    },
    "t_bytes_storage": {
      "encoding": "bytes",
      "label": "bytes",
      "numberOfBytes": "32"
    },
    "t_mapping(t_address,t_bool)": {
      "encoding": "mapping",
      "key": "t_address",
      "label": "mapping(address => bool)",
      "numberOfBytes": "32",
      "value": "t_bool"
    },
    "t_mapping(t_uint256,t_mapping(t_address,t_bool))": {
      "encoding": "mapping",
      "key": "t_uint256",
      "label": "mapping(uint256 => mapping(address => bool))",
      "numberOfBytes": "32",
      "value": "t_mapping(t_address,t_bool)"
    },
    "t_string_storage": {
      "encoding": "bytes",
      "label": "string",
      "numberOfBytes": "32"
    },
    "t_struct(S)12_storage": {
      "encoding": "inplace",
      "label": "struct A.S",
      "members": [
        {
          "astId": 2,
          "contract": "fileA:A",
          "label": "a",
          "offset": 0,
          "slot": "0",
          "type": "t_uint128"
        },
        {
          "astId": 4,
          "contract": "fileA:A",
          "label": "b",
          "offset": 16,
          "slot": "0",
          "type": "t_uint128"
        },
        {
          "astId": 8,
          "contract": "fileA:A",
          "label": "staticArray",
          "offset": 0,
          "slot": "1",
          "type": "t_array(t_uint256)2_storage"
        },
        {
          "astId": 11,
          "contract": "fileA:A",
          "label": "dynArray",
          "offset": 0,
          "slot": "3",
          "type": "t_array(t_uint256)dyn_storage"
        }
      ],
      "numberOfBytes": "128"
    },
    "t_uint128": {
      "encoding": "inplace",
      "label": "uint128",
      "numberOfBytes": "16"
    },
    "t_uint256": {
      "encoding": "inplace",
      "label": "uint256",
      "numberOfBytes": "32"
    }
  }
}
```

### 清除变量
当一个值短于256位短时候，有些情况下剩余的位必须被清除。编译器会在可能被剩余的位里的脏数据影响的操作之前清理剩余位。比方说，在往memory写入值的时候，剩余的位需要被清除，因为内存的内容可以被用来计算哈希或者作为消息调用的数据。相似的，在往storage里存放值的时候，剩余的位需要被清除，否则就会有脏数据

另一方面，如果接下来的操作没有被影响，编译器就不会清理剩余位。比如说，因为`JUMPI`指令认为非零的值是`true`，编译器不会在这个布尔值被用做`JUMPI`的条件时候清除布尔值

除了上面说的，编译器还会在数据加载到堆栈的时候清除输入数据

不同的类型有不同的清除规则

| 类型        | 有效值    | 无效值代表                    |
|-----------|--------|--------------------------|
| n个成员的enum | 0到n-1  | 异常                       |
| 布尔类型      | 0或1    | 1                        |
| 有符号整型     | 有符号扩展字 | 目前会silently wraps，未来会是异常 |
| 无符号整型     | 高位清零   | 目前会silently wraps，未来会是异常 |


### 源映射
作为抽象语法树(AST)输出的一部分，编译器提供了由对应的AST节点代表的源码。这可以用来干很多事，从基于AST报告错误的静态分析工具到能高亮本地变量的调试工具等等。

不仅如此，编译器还能生成从字节码到源码的映射。这对在字节码级别操作的静态分析工具和展示源码在调试器中的位置十分有用。这个映射还包括了其他的信息，比如`jump type 跳转类型`和`modifier depth 修饰符深度`

两种源码映射都使用整数标识符来引用源文件。源文件的标识符存放在`output['sources']['sourceName']['id]`里，其中`output`是编译器标准JSON接口的输出。

AST内的源映射使用这样的符号`s:l:f`，其中`s`是源代码段开始的位置的字节偏移，`l`是源代码段的长度，单位是字节，`f`是源码索引

字节码的源映射更加复杂，是一个由`;`分隔的`s:l:f:j:m`列表。每一个元素对应一个指令，也就是说你不能用字节偏移，你得用指令偏移。`s`,`l`,`f`和上面的定义是一样的。`j`可以是`i`,`o`或者`-`，用来表示jump指令是不是跳转进函数，还是从函数返回还是一个普通的跳转，比如说用来循环的跳转。最后一个`m`是一个用来标记修饰符深度的整数。这个深度在每一次修饰符里的占位语句(`_`)进入的时候增加，从占位语句中出来的时候减少。这允许调试器去追踪一些复杂的用例，比如同一个修饰符被用了两次或者有多个占位语句用在了一个修饰符里

为了压缩这些源映射，尤其是压缩字节码的，会用这几个规则

- 如果有一个filed(s,l,f,j,m之类的)是空的，那么这个值就会用这个filed的前一个元素的filed的值
- 如果缺少了`:`,所有的filed都被认为是空的

下面是两个表示相同信息的源映射

`1:2:1;1:9:1;2:1:2;2:1:2;2:1:2`

`1:2:1;:9;2:1:2;;`


### 优化器



## Contract ABI Specification 合约编码规范
### 基本设计
合约应用二进制接口(Contract Application Binary Interface ABI)是和以太坊生态上的合约进行交互的标准办法，有从区块链外部和合约之间两种交互方式。数据根据类型来编码。编码本身不足以自描述，因此需要一个解码的模式

我们假设合约的接口函数是强类型的，接口函数在编译时已知而且是静态的。我们假设所有的合约在编译时都有这个合约所有调用了的合约的接口定义。


### 函数选择器
函数调用的call data的前4个字节指定了被调用的函数。这是函数签名的Keccak256哈希的前4个字节。也就是函数名加上括号和参数的类型，不需要参数名，函数的返回类型不是签名的一部分。


### 参数编码
从第五个字节开始，就是编码后的参数了。这个编码也被用在其他的地方，比如说返回值和事件参数都是用相同的方式编码的。

参数有如下几种基本类型

- `uint<M>`: `M`位的无符号整型，`0 < M <= 256`，`M % 8 == 0`，比如`uint32`，`uint8`，`uint256`
- `int<M>`: `M`位的有符号整型，`0 < M <= 256`，`M % 8 == 0`
- `address`: 等于`uint160`，计算函数选择器的时候，用的是`address`
- `uint`，`int`: 分别等于`uint256`，`int256`，计算函数选择器的时候用`uint256`，`int256`
- `bool`: 和`uint8`相同，但是值被限制在了0和1，计算函数选择器的时候用`bool`
- `fixed<M>x<N>`: `M`位的有符号定点小数，`8 <= M <= 256`，`M % 8 == 0`，和`0 < N <= 80`，将值`v`表示为`v / (10 ** N)`
- `ufixed<M>x<N>`: 无符号版本的`fixed<M>x<N>`
- `fixed`，`ufixed`: 分别和`fixed128x18`，`ufixed128x18`相同。计算函数选择器的时候，使用`fixed128x18`和`ufixed128x18`
- `bytes<M>`: `M`字节，`0 < M <= 32`
- `function`: 和`bytes24`的编码一样，由一个address(20字节)和函数选择器(4字节)组成

参数有如下固定长度数组类型

- `<type>[M]`: `M`个指定类型元素的固定长度数组，`M >= 0`

> 虽然ABI规范可以用0个元素表达固定长度数组，但是编译器不支持

参数有如下非固定长度数组类型

- `bytes`: 动态长度的数组序列
- `string`: 动态长度的unicode字符串，假定为UTF-8编码
- `<type>[]`: 给定类型的元素的动态长度数组

通过用括号包住类型和逗号分隔，类型可以被组合成元组：`(T1, T2,...,Tn)`由类型`T1`，...，`Tn`，`n >= 0`组成

元组的元组，元组的数组还有空元组都是可以的


### 将solidity类型映射为ABI类型
solidity支持所有上面出现的类型，而且名字都是一样的，除了元组。另一方面有一些solidity类型ABI规范是不支持的。下面的表格左边一列展示solidity中不是ABI部分的类型，右边一列是表示这些类型的ABI类型

| solidity | ABI |
|----------|-----|
| address payable | `address` |
| contract | `addreess` |
| enum | `uint8` |
| struct | `tuple` |


### 编码的设计准则
编码被设计出来拥有以下属性，这些属性在一些参数为嵌套数组的时候尤其有用

1. 访问一个值的需要的读的次数最多就是值在参数数组结构里的深度。也就是说，访问`a_i[k][l][r]`需要4次读。在之前版本的ABI里，最坏情况下，读的次数会随着动态参数的总数线性增长
2. 变量或数组元素的数据和其他的数组不能交错而且需要能重新定位，也就是说这些数据只用`相对地址`


### ABI编码的正式规范
我们区别静态和动态类型。静态类型被就地编码而动态类型的编码会在当前数据块之后分散的分配位置

定义：下面的类型被称为"动态"

- `bytes`
- `string`
- `T[]`T为任何类型
- `T[k]`T为任何动态类型，`k >= 0`
- `(T1,...,Tk)`如果其中某个元素是动态的

所有其他的类型都被称为"静态"

定义：`len(a)`是二进制字符串`a`的字节数。`len(a)`的类型被假定为`uint256`

我们把`enc`定义为实际的编码，作为从ABI类型的值到二进制字符串的映射，当且仅当`X`的类型是动态的时候`len(enc(X))`依赖于`X`的值

定义：对于任意的ABI值`X`，我们递归的定义`enc(X)`，根据`X`的类型的不同: 

- `(T1,...,Tk)`其中`k >= 0`，`enc(X) = head(X(1)) ... head(X(k)) tail(X(1)) ... tail(X(k))，其中`X = (X(1), ..., X(K))`且`Ti`的`head`和`tail`定义如下：
    - 如果`Ti`为静态：`head(X(i)) = enc(X(i))`且`tail(X(i)) = ""`(空字符串)
    - 如果`Ti`为动态：`head(X(i)) = enc(len( head(X(1)) .. head(X(k)) tail(X(1)) ... tail(X(i-1)) )) tail(X(i)) = enc(X(i))`，在动态类型的情况下，`head(x(i))`是明确的，因为head部分的长度只依赖于类型而不依赖于值。`head(X(i))`的值是`tail(X(i))`相对于`enc(X)`开头的偏移量
- `T[k]`T为任何动态类型，`k >= 0`: `enc(X) = enc((X[0], ... X[k-1]))`，也就是它的编码就像是k个相同类型元素的元组
- `T[]`其中`X`有`k`个元素(`k`被假定为`uint256`类型): `enc(X) = enc(k) pad_right(X)`，也就是字节的数量被编码为了`uint256`，然后后面跟上`X`的实际值，这个值是作为字节序列编码的，最后跟上最小数量的零字节让`len(enc(X))`是32的倍数
- `string`: `enc(X) = enc(enc_utf8(X))`，也就是`X`是utf-8编码并且它的值被解释为`bytes`类型。请注意后续编码使用的长度是utf-8编码字符串的字节数，而不是字符数
- `uint<M>`: `enc(X)`是`X`的大端序编码，高序侧(左边)填充0来让长度为32字节
- `address`: 和`uint160`一样
- `int<M>`: `enc(X)`是`X`的大端序二进制补码编码，高序侧(左边)填充0(非负的情况下)或者填充`0xff`(负的情况下)来让长度为32字节
- `bool`: 和`uint8`一样，`1`代表`true`，`0`代表`false`
- `fixed<M>x<N>`: `enc(X)`为`enc(X * 10**N)`其中`X * 10**N`被解释为`int256`
- `fixed`: 和`fixed128x18`一样
- `ufixed<M>x<N>`: `enc(X)`为`enc(X * 10**N)`其中`X * 10**N`被解释为`uint256`
- `ufixed`: 和`ufixed128x18`一样
- `bytes<M>`: `enc(X)`是`X`的字节序列，在尾部填充零字节来让长度为32字节

请注意，任何`X`，`len(enc(X))`为32的倍数


### 函数选择器和参数编码
总的来说，用参数`a_1, ... , a_n`调用函数`f`会被编码成

`function_selector(f) enc((a_1, ... , a_n))`

而`f`的返回值`v_1, ... , v_k`会被编码为

`enc((v_1, ... , v_k))`

也就是说值会被组合成元组然后在被编码

举个例子，给定下面的合约

```typescript
contract Foo {
    function bar(bytes32[2] memory) public pure {}
    function baz(uint32 x, bool y) public pure returns (bool r) { r = x > 32 || y;}
    function sam(bytes memory, bool, uint[] memory) public pure {}
}
```

如果我们用参数`69`和`true`调用`baz`，我们会传入总共68个字节，分解成以下

- `0xcdcd77c0`: 函数选择器(方法ID)，这是由签名`baz(uint32,bool)`的ASCII形式的keccak哈希的前4个字节得来的
- `0x0000000000000000000000000000000000000000000000000000000000000045`: 第一个参数，一个被填充为32个字节的`uint32`值
- `0x0000000000000000000000000000000000000000000000000000000000000001`: 第二个参数，一个被填充为32个字节的布尔`true`

组合起来就是

```
0xcdcd77c000000000000000000000000000000000000000000000000000000000000000450000000000000000000000000000000000000000000000000000000000000001
```

这个函数返回一个`bool`，如果返回的是`false`，那么输出就会是一个字节数组`0x0000000000000000000000000000000000000000000000000000000000000000`，一个布尔值

如果用参数`["abc", "def"]`调用`bar`，我们总共会传入68个字节，分解成

- `0xfce353f6`: 函数选择器(方法ID)，这是由签名`bar(bytes3[2])`的ASCII形式的keccak哈希的前4个字节得来的
- `0x6162630000000000000000000000000000000000000000000000000000000000`: 第一个参数的第一部分，一个`bytes3`值`"abc"`(左对齐)
- `0x6465660000000000000000000000000000000000000000000000000000000000`: 第一个参数的第二部分，一个`bytes3`值`"def"`(左对齐)

组合起来就是

```
0xfce353f661626300000000000000000000000000000000000000000000000000000000006465660000000000000000000000000000000000000000000000000000000000
```

如果用参数`"dave"` `true` `[1,2,3]`调用`sam`的话，总共会传入292个字节，分解为

- `0xa5643bf2`: 方法ID，来自签名`sam(bytes,bool,uint256[])`，其中`uint`被替换为了`uint256`
- `0x0000000000000000000000000000000000000000000000000000000000000060`: 第一个参数的数据部分的位置，从参数块的开始位置开始计算，单位是字节
- `0x0000000000000000000000000000000000000000000000000000000000000001`: 第二个参数：布尔真
- `0x00000000000000000000000000000000000000000000000000000000000000a0`: 第三个参数的数据部分的位置，单位是字节
- `0x0000000000000000000000000000000000000000000000000000000000000004`: 第一个参数的数据部分，从元素的字节数组的长度开始，这个例子里就是4
- `0x6461766500000000000000000000000000000000000000000000000000000000`: 第一个餐素的内容，UTF-8编码(这个例子里和ASCII一样)的`"dave"`，右边填充0到32个字节
- `0x0000000000000000000000000000000000000000000000000000000000000003`: 第三个参数的数据部分，从长度开始，这个例子里就是3
- `0x0000000000000000000000000000000000000000000000000000000000000001`: 第三个参数的第一个条目
- `0x0000000000000000000000000000000000000000000000000000000000000002`: 第三个参数的第二个条目
- `0x0000000000000000000000000000000000000000000000000000000000000003`: 第三个参数的第三个条目

组合起来就是

```
0xa5643bf20000000000000000000000000000000000000000000000000000000000000060000000000000000000000000000000000000000000000000000000000000000100000000000000000000000000000000000000000000000000000000000000a0000000000000000000000000000000000000000000000000000000000000000464617665000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000003000000000000000000000000000000000000000000000000000000000000000100000000000000000000000000000000000000000000000000000000000000020000000000000000000000000000000000000000000000000000000000000003
```

### 使用动态类型
使用签名`f(uint,uint32[],bytes10,bytes)`和值`(0x123, [0x456, 0x789], "1234567890", "Hello, world!")`去调用一个函数会按如下方式编码

首先取`sha3("f(uint256,uint32[],bytes10,bytes)")`的前4个字节，也就是`0x8be65246`。然后我们编码这四个参数的头部。对于静态类型`uint256`和`bytes10`，直接就编码为我们想要传的值，然而对于动态类型`uint32[]`和`bytes`，我们使用从他们的数据区域开始的单位是字节的偏移量，这个偏移量是从值的编码开始的位置开始计算的，也就是不计算前四个包含了函数签名哈希的字节

头部如下

- `0x0000000000000000000000000000000000000000000000000000000000000123`
- `0x0000000000000000000000000000000000000000000000000000000000000080`: 第二个参数的数据部分的开始位置相对于起始位置(第五个字节开始)的偏移，4*32 个字节，就是头部的大小
- `0x3132333435363738393000000000000000000000000000000000000000000000`: `"1234567890"`右边填充0到32个字节
- `0x00000000000000000000000000000000000000000000000000000000000000e0`: 第四个参数的数据部分的开始位置相对于起始位置的偏移，也就是第一个动态参数的偏移加上第一个动态参数的大小，也就是`4*32 + 3*32`

在这之后，首先是第一个动态参数的数据部分，`[0x456, 0x789]`如下

- `0x0000000000000000000000000000000000000000000000000000000000000002`: 数组元素的个数，2
- `0x0000000000000000000000000000000000000000000000000000000000000456`: 第一个元素
- `0x0000000000000000000000000000000000000000000000000000000000000789`: 第二个元素

最后，我们编码第二个动态参数的数据部分，`"Hello, world!"`:

- `0x000000000000000000000000000000000000000000000000000000000000000d`: 元素的个数，这个例子里就是字节的个数: `13`
- `0x48656c6c6f2c20776f726c642100000000000000000000000000000000000000`: `"Hello, world!"`右侧填充0到32个字节

组合起来就是

```
0x8be65246
  0000000000000000000000000000000000000000000000000000000000000123
  0000000000000000000000000000000000000000000000000000000000000080
  3132333435363738393000000000000000000000000000000000000000000000
  00000000000000000000000000000000000000000000000000000000000000e0
  0000000000000000000000000000000000000000000000000000000000000002
  0000000000000000000000000000000000000000000000000000000000000456
  0000000000000000000000000000000000000000000000000000000000000789
  000000000000000000000000000000000000000000000000000000000000000d
  48656c6c6f2c20776f726c642100000000000000000000000000000000000000
```

让我们来用同样的规则去给函数签名`g(uint[][], string[])`和值`([[1,2], [3]], ["one", "two", "three"])`编码数据，不过这一次从最原子性的部分开始

首先我们编码第一个动态数组`[[1,2], [3]]`里的第一个动态数组`[1, 2]`的长度和数据

- `0x0000000000000000000000000000000000000000000000000000000000000002`: 数组的元素数量，2；元素本身为`1`和`2`
- `0x0000000000000000000000000000000000000000000000000000000000000001`: 第一个元素
- `0x0000000000000000000000000000000000000000000000000000000000000002`: 第二个元素

然后我们编码第一个动态数组`[[1,2], [3]]`的第二个动态数组`[3]`的长度和数据

- `0x0000000000000000000000000000000000000000000000000000000000000001`: 第二个数组的元素数量，1；元素为`3`
- `0x0000000000000000000000000000000000000000000000000000000000000003`: 第一个元素

然后我们分别计算出动态数组`[1,2]`和`[3]`的偏移`a`和`b`。为了计算这个偏移我们可以看下第一个数组`[[1,2], [3]]`的编码数据，然后枚举编码的每一行

```
0 - a                                                                - [1, 2]的偏移
1 - b                                                                - [3]的偏移
2 - 0000000000000000000000000000000000000000000000000000000000000002 - [1, 2]的元素个数
3 - 0000000000000000000000000000000000000000000000000000000000000001 - 1的编码
4 - 0000000000000000000000000000000000000000000000000000000000000002 - 2的编码
5 - 0000000000000000000000000000000000000000000000000000000000000001 - [3]的元素个数
6 - 0000000000000000000000000000000000000000000000000000000000000003 - 3的编码

```

偏移`a`指向数组`[1,2]`的内容的开头，也就是行号为2(64字节)的位置，因此`a = 0x0000000000000000000000000000000000000000000000000000000000000040`

偏移`b`指向数组`[3]`的内容的开头，也就是行号为5(160字节)的位置，因此`b = 0x00000000000000000000000000000000000000000000000000000000000000a0`

然后我们编码字符串数组，也就是第二个动态数组

- `0x0000000000000000000000000000000000000000000000000000000000000003`字符串`"one"`中字符的数量
- `0x6f6e650000000000000000000000000000000000000000000000000000000000`字符串`"one"`的utf8表示
- `0x0000000000000000000000000000000000000000000000000000000000000003`字符串`"two"`中字符的数量
- `0x74776f0000000000000000000000000000000000000000000000000000000000`字符串`"two"`的utf8表示
- `0x0000000000000000000000000000000000000000000000000000000000000005`字符串`"three"`中字符的数量
- `0x7468726565000000000000000000000000000000000000000000000000000000`字符串`"three"`的utf8表示

和第一个动态数组类似，因为字符串是动态的，我们需要找到偏移量`c`,`d`和`e`

```
0 - c                                                                - "one"的偏移量
1 - d                                                                - "two"的偏移量
2 - e                                                                - "three"的偏移量
3 - 0000000000000000000000000000000000000000000000000000000000000003 - "one"的字节数
4 - 6f6e650000000000000000000000000000000000000000000000000000000000 - "one"的编码
5 - 0000000000000000000000000000000000000000000000000000000000000003 - "two"的字节数
6 - 74776f0000000000000000000000000000000000000000000000000000000000 - "two"的编码
7 - 0000000000000000000000000000000000000000000000000000000000000005 - "three"的字节数
8 - 7468726565000000000000000000000000000000000000000000000000000000 - "three"的编码
```

偏移量`c`指向了字符串`"one"`内容的开头位置，也就是行号3的位置(96字节)，因此`c = 0x0000000000000000000000000000000000000000000000000000000000000060`

偏移量`d`指向了字符串`"two"`内容的开头位置，也就是行号5的位置(160字节)，因此`c = 0x00000000000000000000000000000000000000000000000000000000000000a0`

偏移量`e`指向了字符串`"three"`内容的开头位置，也就是行号7的位置(224字节)，因此`c = 0x00000000000000000000000000000000000000000000000000000000000000e0`

请注意，数组的元素的编码相互不依赖，而且

然后我们编码第一个动态数组的长度

- `0x0000000000000000000000000000000000000000000000000000000000000002`: 第一个动态数组的元素的个数，2；元素本身是`[1,2]`和`[3]`

然后我们编码第二个动态数组的长度

- `0x0000000000000000000000000000000000000000000000000000000000000003`: 第二个动态数组的字符串的数量，3；字符串本身是`"one"`，`"two"`和`"three"`

最后我们为动态数组`[[1,2],[3]]`和`["one","two","three"]`计算出偏移量`f`和`g`

```
0x2289b18c                                                            - 函数签名
 0 - f                                                                - [[1, 2], [3]]的偏移
 1 - g                                                                - ["one", "two", "three"]的偏移
 2 - 0000000000000000000000000000000000000000000000000000000000000002 - [[1, 2], [3]]的长度
 3 - 0000000000000000000000000000000000000000000000000000000000000040 - [1, 2]的偏移
 4 - 00000000000000000000000000000000000000000000000000000000000000a0 - [3]的偏移
 5 - 0000000000000000000000000000000000000000000000000000000000000002 - [1, 2]的长度
 6 - 0000000000000000000000000000000000000000000000000000000000000001 - 1的编码
 7 - 0000000000000000000000000000000000000000000000000000000000000002 - 2的编码
 8 - 0000000000000000000000000000000000000000000000000000000000000001 - [3]的长度
 9 - 0000000000000000000000000000000000000000000000000000000000000003 - 3的编码
10 - 0000000000000000000000000000000000000000000000000000000000000003 - ["one", "two", "three"]的长度
11 - 0000000000000000000000000000000000000000000000000000000000000060 - "one"的偏移
12 - 00000000000000000000000000000000000000000000000000000000000000a0 - "two"的偏移
13 - 00000000000000000000000000000000000000000000000000000000000000e0 - "three"的偏移
14 - 0000000000000000000000000000000000000000000000000000000000000003 - "one"的长度
15 - 6f6e650000000000000000000000000000000000000000000000000000000000 - "one"的编码
16 - 0000000000000000000000000000000000000000000000000000000000000003 - "two"的长度
17 - 74776f0000000000000000000000000000000000000000000000000000000000 - "two"的偏移
18 - 0000000000000000000000000000000000000000000000000000000000000005 - "three"的长度
19 - 7468726565000000000000000000000000000000000000000000000000000000 - "three"的编码
```

偏移`f`指向的是数组`[[1,2],[3]]`的内容的开始位置，也就是行号2(64字节)；`f = 0x0000000000000000000000000000000000000000000000000000000000000040`

偏移`g`指向的是数组`["one", "two", "three"]`的内容的开始位置，也就是行号10(320字节)；`f = 0x0000000000000000000000000000000000000000000000000000000000000140`


### 事件
事件是对于以太坊 `logging/event-watching` 协议的抽象。日志条目提供了合约地址，一系列最多4个主题和一些任意长度的二进制数据。事件利用已有的函数ABI来解释这些数据(和接口标准一起)为合适的类型数据结构

给定事件名和一系列事件参数，我们它们分为两个子序列：索引了的和没索引的。索引的最多有3个，是和事件签名的keccak哈希一起使用来形成日志条目的主题。没有索引的形成事件的字节数组

实际上，日志条目使用如下ABI

- `address`: 合约的地址(以太坊内部提供)
- `topics[0]`: `keccak(EVENT_NAME+"("+EVENT_ARGS.map(canonical_type_of).join(",")+")")`，`canonical_type_of`是一个简单的返回给定参数的标准类型的函数。比方说，对于`uint indexed foo`，他会返回`uint256`。如果事件被标记为`anonymous`，那么`topics[0]`不会生成
- `topics[n]`: `abi_encode(EVENT_INDEXED_ARGS[n - 1])`，`EVENT_INDEXED_ARGS`是一系列索引了的`EVENT_ARGS`
- `data`: `EVENT_NON_INDEXED_ARGS`的ABI编码，`EVENT_NON_INDEXED_ARGS`是一系列没有索引的`EVENT_ARGS`，`abi_encode`是用来从函数返回一系列有类型的值的ABI编码函数

对于最多32个字节的所有类型，`EVENT_INDEXED_ARGS`的数组直接包含值，填充或者符号扩展(对于有符号整型)到32个字节。然而，对于所有的"复杂"类型或者动态长度的类型，包括所有的数组，`string`，`bytes`和结构体，`EVENT_INDEXED_ARGS`会包含一个特别的就地编码的值的keccak哈希，而不直接是编码的值。这允许应用高效的查询动态长度类型的值(通过设定编码值的哈希为主题)，应用开发者在快速搜索预先决定的值(如果参数索引了)和任意值的可读性(需要参数没有被索引)之间面临取舍。开发者或许可以通过用两个参数来定义事件来克服这些取舍，一个索引了的和一个没索引的，两个参数都存同一个值


### JSON
合约接口的JSON格式可以由一组函数和/或一组事件描述给出。函数描述是一个JSON对象，对象里有这些域

- `type`: `"function"`，`"constructor"`，`"receive"`或者`"fallback"`
- `name`: 函数名
- `inputs`: 对象数组，每个对象包含
    - `name`: 参数的名字
    - `type`: 参数的标准类型
    - `components`: 给元组类型使用的
- `outputs`: 和`inputs`相似的对象数组
- `stateMutability`: 是一个有以下值的字符串
    - `pure`: 不读区块链状态
    - `view`: 不改变区块链状态
    - `nonpayable`: 不接受以太坊
    - `payable`: 接受以太坊

`constructor`和`fallback`都没有`name`和`outputs`。`fallback`也没有`inputs`

事件描述是一个JSON对象，它具有相似的域

- `type`: 总是`event`
- `name`: 事件名
- `inputs`: 对象数组，每一个元素包含
    - `name`: 参数名
    - `type`: 参数的标准类型
    - `components`: 元组类型会用
    - `indexed`: `true`如果这个域是日志主题的一部分的话，`false`如果是日志数据段的一部分
- `anonymous`: `true`如果事件被声明成`anonymous`

```typescript
contract Test {
    bytes32 b;
    constructor() { b = hex"12345678901234567890123456789012"; }
    event Event(uint indexed a, bytes32 b);
    event Event2(uint indexed a, bytes32 b);
    function foo(uint a) public { emit Event(a, b); }
}
```

会输出以下JSON

```json
[{
"type":"event",
"inputs": [{"name":"a","type":"uint256","indexed":true},{"name":"b","type":"bytes32","indexed":false}],
"name":"Event"
}, {
"type":"event",
"inputs": [{"name":"a","type":"uint256","indexed":true},{"name":"b","type":"bytes32","indexed":false}],
"name":"Event2"
}, {
"type":"function",
"inputs": [{"name":"a","type":"uint256"}],
"name":"foo",
"outputs": []
}]
```

### 严格编码模式
严格编码模式下一定会获得上面正式规范一样的编码。这就是说偏移量必须要尽可能小，同时不能创造出数据区域中的重叠，所以因此间隙是不允许的

通常来说，ABI解码器是用尊崇偏移指针的比较直接的方式写的，但是一些解码器可能会强制严格模式。Solidity的ABI解码器现在不会强制严格模式，但是编码器总是会在严格模式下创建数据


### 非标准紧凑模式
通过`abi.encodePacked()`，solidity支持非标准紧凑模式，其中

- 比32字节还短的类型既不会零填充也不会符号扩展
- 动态类型就地编码且没有长度
- 数组元素会被填充，但依然就地编码

此外，结构体和嵌套数组是不支持的

举个例子，`int16(-1), bytes1(0x42), uint16(0x03), string("Hello, world!")`编码的结果

```
0xffff42000348656c6c6f2c20776f726c6421
  ^^^^                                 int16(-1)
      ^^                               bytes1(0x42)
        ^^^^                           uint16(0x03)
            ^^^^^^^^^^^^^^^^^^^^^^^^^^ string("Hello, world!") 没有长度
```

更特殊的

- 在编码过程中，所有东西都是就地编码。这意味着头部和尾部没有区别，就比如上面的例子里面，字符串的长度是不编码进去的
- `abi.encodePacked`的直接参数可以在不需要填充的情况下被编码，只要没有数组或者`string`或者`bytes`
- 一个数组的编码是有填充的它的元素的编码的连接
- 动态大小类型比如`string`，`bytes`或者`uint[]`编码的时候不需要长度域
- `string`或者`bytes`的编码不需要在末尾填充，除非他是数组或者结构体的一部分，这种情况下填充为32字节的倍数

通常来说，非标准紧凑模式的编码是多义的，一旦有两个动态大小元素连续编码在了一起，这就是没有长度域带来的问题

如果需要填充，则需要显式类型转换

`abi.encodePacked(uint16(0x12)) == hex"0012"`

由于紧凑编码在调用函数的时候不会使用，所以没有特殊的在开头附加函数选择器的支持。因为编码是多义的，也没有解码函数

如果你使用`keccak256(abi.encodePacked(a, b))`，而且`a`和`b`都是动态类型，是很容易造成造成哈希值的冲突的，主要是通过移动一部分`a`到`b`里，或者移动一部分`b`到`a`里。更具体一点，`abi.enodePacked("a", "bc") == abi.encodePacked("ab", "c")`。如果你对签名，验证或者数据完整性使用`abi.encodePacked`，请确保总是使用了相同的类型，并且最多只有一个参数是动态的。除非有什么不可抗拒的理由，`abi.encode`总是更好的


### 索引事件参数的编码
索引事件参数中不是值类型的参数(也就是数组和结构体)不会直接存储，而是会存储编码的keccak256哈希。编码定义如下

- `bytes`和`string`的编码就是没有填充或者长度前缀的字符串内容
- 结构体的编码就是它的成员的编码的连接，他成员的编码总是被填充为32字节的倍数
- 数组(动态和静态)的编码是它的元素的编码的连接，总是被填充为32字节的倍数，而且没有长度前缀

通常，一个负数会被符号扩展填充而不是零填充。`bytesNN`类型会在右边填充，而`uintNN`/`intNN`会在左边填充

> 当有超过一个动态大小数组的时候，结构体的编码就是多义的。因此，总是重复检查事件数据，不要只依赖基于索引参数的搜索结果


## Types 类型
solidity是静态类型的语言，任何变量(状态变量和本地变量)都需要指定一个类型


### 值类型有哪些
值类型(value types)在作为函数参数和赋值的时候都会拷贝一份新的

值类型有以下几个: 
- Booleans 布尔类型
    - `bool`: 可能的值有`true`和`false`
    - 操作符:
        - `!`: 逻辑非
        - `&&`: 逻辑与
        - `||`: 逻辑或
        - `==`: 等于
        - `!=`: 不等于
- Integers 整型
    - `int`/`uint`: 各种大小的有符号和无符号类型，从8开始以8为阶，最小8, 最大256, 比如`uint8`, `uint16`, `uint256`等等，`int`和`uint`分别是`int256`和`uint256`的别名
    - 操作符:
        - 比较: `<=`, `<`, `==`, `!=`, `>=`, `>`
        - 位操作: `&`, `|`, `^`(位异或), `~`(按位非)
        - 移位操作: `<<`, `>>`
        - 算数操作: `+`, `-`, 一元`-`(有符号整型才有), `*`, `/`, `%`, `**`(幂)
- Address 地址类型
    - 有两种地址类型
        - `address`: 20 byte 长度的值
        - `address payable`: 和`address`一样，但有额外的成员`transfer`和`send`
    - 类型转换
        - 隐式的从`address payable`转换为`address`是可以的，然而从`address`转换为`address payable`必须式显式的
        - 显式的将`address`和 (`uint160`, 整型字面量，`bytes20`, `contract类型`)这些相互转换是可以的
        - 只有`address`类型和`contract`类型可以通过`payable(...)`转换成`address payable`, 对于`contract`类型来说，这个转换只有在合约能够接收ether的时候，也就是合约要么有一个`receive`函数，要么有一个`payable fallback function`. 最后，`payable(0)`是合法的，他是上面的限制的例外
    - [成员](https://docs.soliditylang.org/en/v0.8.0/units-and-global-variables.html#address-related)
        - `<address>.balance (uint256)`: 地址的余额，单位是wei, 在`0.5.0`之前你可以在contract实例里访问address类型的成员，比如`this.balance`, 但在`0.5.0`之后，这种行为被禁止了，你必须用`address(this).balance`
        - `<address>.code (bytes memory)`: 地址的代码
        - `<address>.codehash (bytes32)`: 地址的代码的哈希
        - `<address payable>.transfer(uint256 amount)`: 发送一定量的wei到address里，失败会回滚，只传递2300 gas
        - `<address payable>.send(uint256 amount) returns (bool)`: 发送一定量的wei到address里，失败返回false不回滚，只传递2300 gas
        - `<address>.call(bytes memory) returns (bool, bytes memory)`: 发送一个底层的`CALL`, 并携带给定的payload, 返回是否成功和数据，传递所有可用的gas
        - `<address>.delegatecall(bytes memory) returns (bool, bytes memory)`: 发送一个底层的`DELEGATECALL`, 并携带给定的payload, 返回是否成功和数据，传递所有可用的gas
        - `<address>.staticcall(bytes memory) returns (bool, bytes memory)`: 发送一个底层的`STATICCALL`, 并携带给定的payload, 返回是否成功和数据，传递所有可用的gas
- Contract 合约类型
    - 每一个合约都定义了自己的类型，你可以把一个合约隐式转换为这个合约继承的合约，也可以把一个合约类型和一个地址类型相互显式转换
- Fixed-size byte arrays 固定长度的字节数组
    - `bytes1`, `bytes2`, `bytes3`, ... ，`bytes32`
    - 操作符:
        - 比较: `<=`, `<`, `==`, `!=`, `>=`, `>`
        - 位操作: `&`, `|`, `^`(位异或), `~`(按位非)
        - 移位操作: `<<`, `>>`
        - 索引访问: 如果`x`的类型是`bytesI`那么`x[k]`其中`0 <= k < I`会返回第`k`个字节，比如`bytes2 b = 0x1234`, `b[0]`返回`0x12`, `b[1]`返回`0x34`



### 引用类型有哪些
- Dynamically-sized byte array 动态长度字节数组
    - `bytes`: 动态长度的字节数组
    - `string`: 动态长度的UTF8编码字符串
- Arrays 数组
    - T[]
    - bytes
    - string


### 有理数字面量和整数字面量如何表示
整数字面量由一系列的0-9中的数字组成，有理数字面量由一个`.`和最少一个数字组成，比如`1.`, `.1`, `1.3`

科学计数法也是支持的，基数可以是分数，而指数不能是，比如`2e10`, `-2e10`, `2e-10`, `2.5e1`

数值字面量在被转换成一个非字面量的类型之前都是任意精度的，换句话说数值字面量之间的运算不会溢出


### 字符串字面量
单引号双引号都可，连续的写也可，比如`"foo""bar"`

字符串字面量只能包含可打印的ASCII字符，也就是`0x1F..0x7E`之间的字符

此外还包含如下几个转义字符
- `\<newline>`: 转义一个换行
- `\\`: 反斜杠
- `\'`: 单引号
- `\"`: 双引号
- `\b`: 退格符
- `\f`: 换页符
- `\n`: 换行
- `\r`: 回车
- `\t`: tab
- `\v`: 垂直制表符
- `\xNN`: 十六进制转义 接受一个十六进制值然后插入一个合适的字节
- `\uNNNN`: unicode转义 接受一个unicode码点然后插入一个UTF-8序列


### Unicode字面量怎么表示
`string memory a = unicode"Hello 😀";`


### 地址字面量如何表示
地址字面量就是一个十六进制字面量，不过要满足[校验测试](https://github.com/ethereum/EIPs/blob/master/EIPS/eip-55.md)

比如 0xdCad3a6d3569DF655070DEd06cb7A1b2Ccd1D3AF

显式的将`bytes20`或者一个整型转换为`address`会得到一个`address payable`

`address a`可以这样`payable(a)`转换成`address payable`


### 数组字面量如何表示
一个逗号分隔的列表，用`[...]`包围起来，必须有一个所有的元素都隐式转换过去的`common type`

数组字面量总是固定长度的内存数组(staticall-sized memory arrays)

`[1,2,3]`是一个`uint8[3] memory` 如果你想让这个字面量变成`uint[3] memory`你需要显式转换第一个元素`[uint(1), 2, 3]`

固定长度的内存数组(Fixed size memory arrays)是不能赋值给动态长度的内存数组(dynamically-sized memory arrays)的 (有计划要移除这个限制)

```typescript
contract C {
    function f() public {
        // The next line creates a type error because uint[3] memory
        // cannot be converted to uint[] memory.
        uint[] memory x = [uint(1), 3, 4];
    }
}
```


### 移位操作有啥细节
移位操作的结果的类型和左侧的操作数的类型一致，结果的值会被截断来匹配这个类型，右侧的操作数**必须**是一个无符号类型

- 对于正数和负数值`x`, `x<<y`和`x * 2**y`相等
- 对于正数值`x`，`x>>y`和`x / 2**y`相等
- 对于负数`x`, `x>>y`和`(x+1) / 2**y - 1`相等
- (0.5.0 之前)对于负数`x`, `x>>y`和`x / 2**y`相等


### 如何表示一个数组类型 Arrays aka. 如何在 storage 中分配一个数组
> 数组可以是(编译时)固定大小的，也可以是动态大小的

- 固定长度: `T[k]` 其中 T 为数组元素的类型，而 k 为数组的大小
- 动态长度: `T[]` 其中 T 为数组元素的类型

举个例子`uint[][5]`代表的是一个长度为 5 的类型为`uint[]`的数组，也就是说这个数组里的每个元素都是动态长度的 uint 数组


### 如何访问数组中的元素
> solidity 的索引是从 0 开始的

举个例子 `uint[][5] memory x` 你可以用`x[2][1]`来访问第 3 个 uint 数组的第 2 个 uint 元素

数组的越界操作会导致一个(assertion)断言失败，换句话说就是你越界了会报错

你可以用`.push()`或者`.push(value)`给数组追加一个元素`.push()`会追加一个用 0 初始化的元素然后返回它的引用，所以你可以写`x.push() = b` `x.push().a = 2`

array 有如下几个成员:
- length: 数组包含的元素的数量
- push(): 动态长度的storage数组和`bytes`有这个成员函数
- push(x): 动态长度的storage数组和`bytes`有这个成员函数
- pop(): 动态长度的storage数组和`bytes`有这个成员函数，返回数组末尾的元素，并隐式的对被移除的元素调用`delete`

> 如果你想在external(而不是public)函数中使用数组的数组的话，你必须开启`ABI coder v2`

> 在Byzantium之前版本的EVM中，是不能访问函数调用返回的动态长度数组的，如果你调用了一个函数返回了动态长度数组，需要确保你EVM设置了Byzantium mode


### 如何在内存中分配一个数组
> 内存中的动态长度数组可以用`new`这个操作符来创建

和 storage 中的数组相反的是，不能改变内存中的数组的大小(`.push`这样的成员函数是不可以访问的), 要么提前计算需要的大小，要么创建一个新的内存数组

```typescript
pragma solidity >=0.4.16 <0.9.0;

contract C {
    function f(uint len) public pure {
        uint[] memory a = new uint[](7);
        bytes memory b = new bytes(len);
    }
}
```


### bytes byte[] bytes32 有啥区别
`bytes`和`byte[]`是很类似的，`byte[]`是一个元素类型是`byte`的动态数组，`bytes32`其实是`byte[32]`也就是长度为 32 个元素，类型是`byte`的固定长度数组

`bytes`和`byte[]`不同的地方在于 bytes 在`memory`和`calldata`中都是`packed tightly`的

`string`和`bytes`是等价的，但是有两个不同的地方，其一，`string`是不能用索引去访问的，这个倒是挺反直觉的，不过如果这么做了编译器会告诉你`TypeError: Index access for string is not possible`, 其二，`string`也没有 length 这个成员

一般来说你应该用`bytes`而不是`byte[]，`因为`bytes`更加便宜，`byte[]`会在每个元素之间添加 31 个`padding bytes`用来凑齐 32 个 bytes


### solidity 里能操作 string 吗
solidity 本身是不支持任何 string 相关的操作函数的，不过有一些第三方的 library

你可以通过`keccak256-hash`来比较两个 string。`keccak256(abi.encodePacked(s1))==keccak256(abi.encodePacked(s2))`

你可以通过`abi.encodePacked(s1,s2)`合并两个 string

如果你想访问一个 string 类型的变量的 byte 形式，假设你有一个变量`string s`, 你可以这样`bytes(s).length` `bytes(s)[7]='x';`


### 如何声明一个mapping
mapping类型的语法是`mapping(_keyType => _valueType)`, 你可以这样声明一个mapping变量`mapping(_keyType => _valueType) _variableName`

mapping类型的变量只能是storage的

和函数中的storage引用类型，library函数中的参数一样，mapping类型的变量都是不能作为`publicly visible`的函数的入参或者返回参数的，这条限制对任何包含了mapping的数组和结构体都是成立的

### delete 关键字如何使用
`delete a`会给`a`赋上`a`这个变量的类型的初始值

例子:
- a为整型，a=0
- a为动态长度数组，赋值长度为0的动态长度数组
- a为固定长度数组，赋值相同长度的固定长度数组，但是每个值都是0
- a为结构体，重置所有结构体成员

`delete`对mapping是没有效果的(因为mapping的键是任意的而且一般是未知的), 所以当你delete一个结构体，他会重置所有不是mapping的成员，并对所有不是mapping类型的成员递归调用这个delete, 但是你还是能用`delete a[x]`来删除存储在x的值

```typescript
contract DeleteExample {
    uint data;
    uint[] dataArray;

    function f() public {
        uint x = data;
        delete x; // 把x设为0, 对data没有影响
        delete data; // 把data设为0, 对x没有影响
        uint[] storage y = dataArray;
        delete dataArray; 
        // 把dataArray.length设为0, 由于uint[]是一个complex object, 
        //y也会被影响，因为y是这个storage对象的别名. 另一方面"delete y"是不行的，
        //因为对一个局部的引用到一个storage对象的变量的赋值只能够来自于一个已经存在的storage对象
        assert(y.length == 0);
    }
}
```


### internal external public 之间的区别
> solidity 中，函数分成两种，也就是 internal 和 external

显然，internal 是只能在内部访问，而这个内部指的是`current code uint` 包括了`internal library function` 和继承的函数

external 函数会被当作一个 function 类型，假设你声明了一个 external 函数 e1, 一个 internal 函数 i1, 那么你可以通过 this.e1 访问 e1, 但是你不能通过 this.i1 访问 i1。

public 函数既可以被当作 internal 也可以被当作 external, 假设你声明了一个 public 函数`f`,那么当你把它当作 internal 函数的时候你就用`f`,当你把它当作 external 函数的时候你就用`this.f`

external 函数拥有两个 member

- `.address` 返回函数的合约的地址
- `.selector` 返回 ABI 函数选择器


### solidity 里的引用类型有哪些
有`struct`, `array` 和 `mapping`, 当你使用引用类型的时候你必须显式的提供这个类型的数据存放的位置

- `memory`: 生命周期在一个外部函数调用(external function call)之内
- `storage`: 生命周期为合约的生命周期
- `calldata`: 一个包含了函数参数的特殊数据位置


### 不同数据存放位置的变量是如何互相赋值的
- `storage`和`memory`之间的赋值总是会创建一个独立的拷贝
- 从`calldata`到`storage`和`memory`的赋值总是会创建一个独立的拷贝
- `memory`之间的赋值只会创建引用，这意味着你改变了一个 memory 变量的值之后，所有引用了这个变量的值都会改变
- 从`storage`向local的`storage`赋值的时候只会赋一个引用
- 所有其他的赋值给`storage`的操作都会拷贝一份

```typescript
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.5.0 <0.9.0;

contract C {
    // x的数据位置是storage
    // 这是唯一一个数据位置可以省略的地方
    uint[] x;

    // memoryArray的数据位置是memory.
    function f(uint[] memory memoryArray) public {
        x = memoryArray; // 行，把整个数组拷贝到storage里
        uint[] storage y = x; // 行，赋值一个指针，y的数据位置是storage
        y[7]; // 行，返回第8个元素
        y.pop(); // 行，通过y这个指针修改y
        delete x; // 行，清空数组，也会修改y
        // y = memoryArray; // 不行，它试图去把y作为一个临时的放在storage里的数组，但是storage必须是"静态"分配的
        // delete y; // 不行，因为这会"重置"这个指针，然而又没有一个合理位置给这个指针指向
        g(x); // 调用 g, 把x的引用传过去
        h(x); // 调用 h, 并在内存里创建一个独立的临时的拷贝
    }

    function g(uint[] storage) internal pure {}
    function h(uint[] memory) public pure {}
}
```


### solidity中的基本类型之间是如何进行转换的
- 隐式类型转换
隐式类型转换会在一些赋值的情况下被编译器自动完成，当给一个函数穿参和当应用操作符的时候，通常来说一个`值类型`之间的隐式类型转换在没有信息丢失并且语义上合理的情况下都可行

比方说，`uint8`可以转换成`uint16`, `int128`可以转换成`int256`, 但是`int8`就不能转换成`uint256`因为`uint256`不能表示`-1`这样的值

当一个操作符被应用到两个不同类型的操作数上的时候，编译器会尝试去做隐式类型转换，把一个操作数转换成另一个(赋值的时候也会有这种隐式类型转换)

在下面的例子中，y和z是不同的类型，由于y可以转换成z但是z不能专程y, `y + z`的结果的类型就是`uint16`, 接着`uint16`又赋值给了`uint32`, 编译器又做了一次隐式类型转换

```typescript
uint8 y;
uint16 z;
uint32 x = y + z;
```

- 显式类型转换
当编译器不允许隐式类型转换但你很确定这个转换没问题的时候，就可以试试显式类型转换，但这可能会导致是一些预料之外的行为，所以最好测试一下

```typescript
int y = -3;
uint x = uint(y);
```

x的值是`0xffffff...fd`

如果一个整型被转换成了一个更小的类型，左边的位会被截掉

```typescript
uint32 a = 0x12345678;
uint16 b = uint16(b); // b is 0x5678
```

如果一个整型被转换成了更大的类型，左边的位会被pad, 结果和原来的整型是一致的

```typescript
uint16 a = 0x1234;
uint32 b = uint32(a); // b is 0x00001234
assert(a == b);
```

固定长度bytes类型和整型相反，他们被视为单独的字节的序列，当被转换为一个更小的类型的时候，会截断这个序列

```typescript
bytes2 a = 0x1234;
bytes1 b = bytes1(a); // b is 0x12
```

当固定长度bytes类型被显式转换为更大的类型时，右边会被pad, 这样子可以在转换后，用固定的索引去访问一个byte的时候有一致的结果

```typescript
bytes2 a = 0x1234;
bytes4 b = bytes4(a); // b is 0x12340000
assert(a[0] == b[0]);
assert(b[1] == b[1]);
```

由于整型和固定长度的byte数组在truncating和padding上的行为不一样，整型和固定长度byte数组之间的显式转换只有在这两个类型的大小相等时才能进行

```typescript
bytes2 a = 0x1234;
uint32 b = uint16(a); // b is 0x00001234
uint32 c = uint32(bytes4(a)); // c is 0x12340000
uint8 d = uint8(uint16(a)); // d is 0x34
uint8 e = uint8(bytes1(a)); // e is 0x12
```


### solidity中字面量和基本类型之间是如何转换的
十进制和十六进制数字字面量在没有截断的情况下都可以隐式转换成任何整型

```typescript
uint8 a = 12; //行
uint32 a = 1234; //行
uint16 c = 0x123456; //不行，发生了截断
```

在0.8.0之前的版本里，十进制和十六进制数字字面量是可以显式转换成整型的(允许截断), 但在0.8.0之后，这样的显式转换和隐式转换一样的严格

十进制数字字面量不能隐式转换成固定长度的byte数组，十六进制数字字面量可以，但只有十六进制数字的位数完全和固定长度byte数组的大小相等才可以，上面这个限制对0不成立，字面量的值为0的可以转换成任意大小的固定长度byte数组

```typescript
bytes2 a = 54321; //不行
bytes2 b = 0x12; //不行
bytes2 c = 0x123; //不行
bytes2 d = 0x1234; //行
bytes2 e = 0x0012; //行
bytes4 f = 0; //行
bytes4 g = 0x0; //行
```

字符串字面量和十六进制字符串字面量可以隐式转换为固定大小的byte数组，如果它们的字符数与字节类型的大小匹配的话

```typescript
bytes2 a = hex"1234"; // 行
bytes2 b = "xy"; // 行
bytes2 c = hex"12"; // 不行
bytes2 d = hex"123"; // 不行
bytes2 e = "x"; // 不行
bytes2 f = "xyz"; // 不行
```

## Uints and Globally Available Variables 单位和全局可用变量
### solidity中有哪些ether单位
```typescript
assert(1 wei == 1);
assert(1 gwei == 1e9);
assert(1 ether == 1e18;
```

0.7.0以前是有`finney`和`szabo`这两个单位的


### solidity中有哪些时间单位
- `1 == 1 seconds`
- `1 minutes == 60 seconds`
- `1 hours == 60 minutes`
- `1 days == 24 hours`
- `1 weeks == 7 days`

0.5.0 以后就没有year了，因为不是每年都有365天


### abi编码和解码函数有哪些
- `abi.decode(bytes memory encodedData, (...)) returns (...)`: 将给定的数据进行ABI解码 e.g. `(uint a, uint[2] memory b, bytes memory c) = abi.decode(data, (uint, uint[2]，bytes))`
- `abi.encode(...) returns (bytes memory)`: 对给定的参数进行ABI编码
- `abi.encodePacked(...) returns (bytes memory)`: 对给定的参数进行Non-standard Packed
- `abi.encodeWithSelector(bytes4 selector, ...) returns (bytes memory)`: 将给定的参数(从第二个参数开始)进行ABI编码，然后在和4个字节的selector合并，selector在前编码后的参数在后
- `abi.encodeWithSignature(string memory signature, ...) returns (bytes memory)`: 和`abi.encodeWithSelector(bytes4(keccak256(bytes(signature))))`是相等的


### 有哪些关于错误处理的关键字
solidity 使用状态回滚异常处理错误，这样的异常会取消所有当前调用(以及所有子调用)对状态的改变，并且给调用者标记一个错误

- `assert(bool condition)`: 会导致一个`Panic error`因此如果条件没有满足的话，会回滚状态，一般用在内部错误里
- `require(bool condition)`: 条件没满足的话会回滚，一般用在检测输入的错误和外部组件上
- `require(bool condition, string memory message)`: 同上，还会提供一个错误信息
- `revert()`: 取消执行程序，回滚状态
- `revert(string memory reason)`: 同上，还会提供一个错误信息

当异常发生在子调用的时候，他们会`冒泡 bubble up`, 也就是说异常发生后整个调用链都会回滚. 有4个例外分别是，`send`, `call`, `delegatecall`, `staticcall`, 他们会返回`false`而不是`冒泡 bubble up`


### 类似keccak256的密码学函数有哪些
- `addmod(uint x, uint y, uint k) returns (uint)`: 计算`(x + y) % k`, 其中的加法是任意精度的，也就是超过了`2**256`也不会溢出，从`0.5.0`开始断言`k != 0`
- `mulmod(uint x, uint y, uint k) returns (uint)`: 计算`(x * y) % k`, 其中的乘法是任意精度的，也就是超过了`2**256`也不会溢出，从`0.5.0`开始断言`k != 0`
- `keccak256(bytes memory) returns (bytes32)`: 计算输入的`Keccak-256`哈希，`0.5.0`以前`keccak256`有个别名叫`sha3`, `0.5.0`之后被移除了
- `sha256(bytes memory) returns (bytes32)`: 计算输入的`SHA-256`哈希
- `ripemd160(bytes memory) returns (bytes20)`: 计算输入的`RIPEMD-160`哈希
- `ecrecover(bytes32 hash, uint8 v, bytes32 r, bytes32 s) returns (address): 从一个椭圆曲线签名中恢复一个与公钥相关联的地址，或者在出错的时候返回0
    - r = 签名的第一个32 bytes
    - s = 签名的第二个32 bytes
    - v = 签名的最后一个byte


### this是啥
this是当前合约的实例，可以显式转化为address类型


### selfdestruct(address payable recipient)有啥细节
- 接受ether的函数的`receive function`不会执行
- 合约只有在交易的最后才会被真正的destruct, 所以`revert`是可以取消这个destruct的

`0.5.0`之前`selfdestruct`有个别名叫`suicide`


### type关键字是啥
`type(X)`可以用来获取`X`类型的信息，就目前而言(0.8.0), X的类型只能是合约类型或者整型，将来可能会增加支持

下面是和合约类型相关的属性
- `type(C).name`: 合约的名字
- `type(C).creationCode`: `memory bytes` 合约创建时的字节码，可以用在内联汇编yul里来自定义新建合约的流程，尤其是使用`create2`操作码的时候，合约本身不能访问这个属性，因为这会导致这个字节码包含在了字节码里面，也就是循环引用
- `type(C).runtimeCode`: `memory bytes` 合约运行时的字节码，这是被合约`C`的构造器部署的那部分代码

下面是和接口类型相关的属性
- `type(I).interfaceId`: `bytes4` 包含了一个[EIP-165](https://eips.ethereum.org/EIPS/eip-165)定义的接口标识符，这个标识符被定义为是接口中的所有函数选择器的异或(XOR), 除了继承的函数

下面是和整型相关的属性
- `type(T).min`: T类型能表示的最小的数
- `type(T).max`: T类型能表示的最大的数


## Expressions and Control Structures 表达式和控制结构
大部分的花括号语言有的控制结构，在solidity里都有

`if`, `else`, `while`, `do`, `for`, `break`, `continue`, `return`

solidity还支持`try`/`catch`形式的异常处理，但是只对外部函数调用(external function calls)和合约创建调用(contract creation calls)有用

条件语句的括号**不能省略**，但是花阔号在单条语句的情况下**可以省略**

非布尔类型向布尔类型的类型转换是不行的，所以`if (1) {}`是无效的


### 如何进行函数调用
**内部函数调用**

```typescript
//这个写完全没有什么意义，只是演示一下递归调用`内部函数 internal function`
contract C {
    function g(uint a) public pure returns (uint ret) {return a + f()};
    function f() internal pure returns (uint ret) {return g(7) + f()};
}
```

当前合约的函数可以被直接调用或者递归的调用，你需要避免大量的递归，因为每个内部函数调用都会占用至少一个`stack slot`只有1024个这样的slot


**外部函数调用**

诸如`this.g(8)` `c.g(2)`的表达式也属于有效的函数调用，但是这种情况下，被称为外部函数调用. 和内部函数调用的区别，外部函数调用是通过一个`message call`消息调用，而不是直接使用`jump`

对于this的函数调用是不能发生在`constructor`里的，因为这时候实际的合约还没有创造出来

其他合约的函数必须是`external`调用的，对于`external`调用而言，所有函数参数必须被拷贝到内存里

> 一个合约对另一个合约的函数调用不会创建一个交易，这个调用是一个message call, 是整个交易的一部分

当调用其他的合约的函数的时候，你可以指定value和gas

在`0.6.2`之前，推荐的指定value和gas的写法是`f.value(x).gas(g)()`, 但这个写法在`0.6.2`之后被废弃了，而且在`0.7.0`之后不合法了

```typescript
contract InfoFeed {
    function info() public payable returns (uint ret) { return 42 };
}

contract Consumer {
    InfoFeed feed;
    function setFeed(InfoFeed addr) public { feed = addr; }
    function callFeed() public { feed.info{value: 10, gas: 800}; }
}
```

由于EVM会把所有的对于不存在的合约进行的函数调用当作是成功的调用，solidity会用`extcodesize`这个操作码来检查被调用的合约是否真的存在，如果不存在会导致异常


**具名调用**

函数调用的参数在被`{ }`包裹的情况下，可以给定名字，任意顺序

参数列表的名字**必须**和函数声明的参数的名字一致

```typescript
contract C {
    mapping(uint => uint) data;
    function f() public {
        set({value: 2, key: 3});
    }

    function set(uint key, uint value) public {
        data[key] = value;
    }
}
```

**省略函数参数的名字**

没有被用到的参数的名字是可以被省略的(尤其是返回参数), 这些参数会出现在栈上，但是是不能访问的

```typescript
contract C{
    function func(uint k, uint) public pure returns (uint) {
        return k;
    }
}
```


### 如何用new创建一个合约
合约A可以用`new`创建另一个合约B, 在编译合约A的时候合约B的完整代码需要是已知的，这样递归的`creation-dependencies`创建依赖才是不可能的 

```typescript
contract B {
    uint public X;
    constructor(uint a) payable {
        x = a;
    }
}

contract A {
    B b = new B(4); // 会在A的constructor里执行

    function createB(uint arg) public {
        B newB = new B(arg);
    }

    function createAndEndowB(uint arg, uint amount) public payable {
        B newB = new B{value: amount}(arg);
    }
}
```

创建B的实例的时候可以指定value, 但是不能指定gas


### 啥是create2
创建一个合约的时候，新创建的合约的地址是由发起这个创建的合约的地址和一个计数器(这个计数器每次发起一个合约创建就增加一次)计算出来的

如果你指定了一个盐`salt`(一个bytes32的值), 那么咋们搞出新创建的合约地址的机制就不一样了，这会用`发起创建的合约地址`和`salt`和新建的合约的`creation bytecode`和`构造器的参数`来计算这个新合约的地址

之前会使用的计数器，在这个新的机制里就不会使用了，这么做可以在新合约创建之前就计算出它的地址

```typescript
contract D {
    uint public x;
    constructor(uint a) {
        x = a;
    }
}

contract C {
    function createDSalted(bytes32 salt, uint arg) public {
        //下面这个表达式是用来提前计算新合约的地址的
        address predictedAddress = address(uint160(uint(keccak256(abi.encodePacked(
            bytes1(0xff),
            address(this),
            salt,
            keccak256(abi.encodePacked(
                type(D).creationCode,
                arg
            ))
        )))));

        D d = new D{salt: salt}(arg);
        require(address(d) == predictedAddress);
    }
}
```

`create2`会导致一些奇怪的行为，用`create2`创造的合约，可以在被摧毁之后再创造一次


### 如何进行解构赋值
solidity内部允许元组类型，也就是一个长度是固定的，可以是不同类型的对象的列表

元组可以被用来返回多个值，这些返回值可以赋值给新声明的变量或者已经存在的变量

```typescript
contract C {
    uint index;
    function f() public pure returns (uint, bool, uint) {
        return (7, true, 2);
    }

    function g() public {
        (uint x, ，uint y) = f(); //不需要所有的元素都指定，但是数量必须匹配
        (x, y) = (y, x); // swap
        (index, ，) = f(); // 变量声明可以省去
        // (x, uint y) = (1, 2); // 混合使用变量声明和无声明赋值是无效的
    }
}
```

`0.5.0`之前是允许赋值的左右边的元组长度不一样的，要么填满左边，要么填满右边，现在不允许了，两边长度必须一致


### 给引用类型赋值会有什么行为
为引用类型(类似数组和结构体还有`bytes`和`string`)赋值的时候会有比较复杂的行为

```typescript
contract C {
    uint[20] x;
    function f() public {
        g(x);
        h(x);
    }

    function g(uint[20] memory y) internal pure {
        y[2] = 3; // 创建一个storage值x的memory的副本，对x没有任何效果
    }

    function h(uint[20] storage y) internal {
        y[3] = 4; // y是一个指针，可以改变x
    }
}
```


### unchecked关键字是啥
`0.8.0`之前，会发生下溢和上溢算术运算会被wrap, 也就是`0x0000 - 1 = 0xffff`, 在`0.8.0`之后，这会直接revert

想要在`0.8.0`之后的版本获得`0.8.0`之前的行为，你需要使用`unchecked`

```typescript
contract C {
    function f(uint a, uint b) pure public returns (uint) {
        unchecked { return a - b; }
    }
}
```


### 异常处理如何进行的
当异常发生在子调用的时候，他们会`冒泡 bubble up`, 也就是说异常发生后整个调用链都会回滚. 有4个例外分别是，`send`, `call`, `delegatecall`, `staticcall`, 他们会返回`false`而不是`冒泡 bubble up`

外部函数调用的异常可以被`try`/`catch`语句捕获，异常可以包含一个数据返回给调用者，这个数据有一个4字节的函数选择器和ABI编码的数据组成

目前`0.8.0`, solidity支持两种错误签名，`Error(string)`和`Panic(uint256)`

Panic异常在下面几种情况下生成，错误码提供了Panic的类型

- `0x01`: 如果你调用`assert`的参数求出来的值是`false`
- `0x11`: 如果在`unchecked {...}`代码块外的算术运算导致了溢出
- `0x12`: 如果你除0了 `5 / 0` `23 % 0`
- `0x21`: 如果你把一个太大的数或者负数转换为了枚举类型
- `0x22`: 如果你访问了一个没有正确编码的`storage byte array`storage里的字节数组
- `0x31`: 如果对一个空数组调用了`.pop()`
- `0x32`: 如果你访问一个数组，`bytesN`, 或者一个数组切片的时候，用了错误的索引(`x[i] 其中 i >= x.length 或者 i < 0`)
- `0x41`: 如果你分配了过多的内存或者创建了一个过大的数组
- `0x51`: 如果调用了一个内部函数类型的`0初始化`变量，就是声明了但是没实现

Error异常会在以下几种情况生成

- 调用`require`的参数求出来的值是`false`
- 如果你对一个没有代码的合约进行了外部函数调用
- 如果你的合约通过一个public函数接受了Ether但是没有`payable`这个修饰符
- 如果你的合约通过`public getter`函数接受了Ether

下面几种情况会转发来自外部函数调用的错误数据，这意味着这要么导致一个`Error`要么导致一个`Panic`

- 如果`.transfer()`失败了
- 如果你通过消息调用调用了一个函数，但没有正确的完成(gas用光了，没有匹配的函数，抛出了一个异常), 除了`call`, `send`, `delegatecall`, `callcode`, `staticcall`被用了的情况，这些个操作不会抛出异常而是返回`false`
- 如果你用`new`关键字创建了一个合约但是合约的创建过程没有正确的完成


### assert和require有什么区别
`assert`函数会创建`Panic(uint256)`类型的错误，`require`函数会创建`Error(string)`类型的错误

`assert`应该被用来测试内部错误，用来检查不变量，一个正常的代码永远都不应该抛出一个Panic错误，甚至无效的外部输入也不能导致Panic

`require`应该被用来保证执行过程中才能被监测到的有效条件，这包括了输入的检测或者对外部合约的调用产生的返回值的检测

你可以选择性的给`require`提供一个字符串来表示错误消息，但是不能给`assert`提供

如果你没有给`require`提供参数，那么他会回滚并返回一个空的错误数据，甚至不包括错误函数的选择器

在`0.8.0`之前Panic异常使用的是`invalid`操作码，这会消耗掉所有可用的gas

在`Metropolis`大都会版本的EVM之前`require`会消耗掉所有可用的gas


### revert关键字如何使用
`revert`会创建一个`Error(string)`异常

下面是用`revert`和`require`写的等价的语句

```typescript
contract VendingMachine {
    function buy(uint amount) public payable {
        if (amount > msg.value / 2 ether) 
            revert("Not enough Ether provided.")
        require(
            amount <= msg.value / 2 ether,
            "Not enough Ether provided."
        )
    }
}
```

`0.4.13`的时候与`revert`有相同语义的`throw`被废弃了，在`0.5.0`之后被移除了

这里的错误信息这个string会被ABI编码，就好像是对函数`Error(string)`进行了调用一样，在上面的例子里，`revert("Not enough Ether provided.")`会被编码成如下的错误数据

```typescript
0x08c379a0 // "Error(string)"这个函数的选择器
0x0000000000000000000000000000000000000000000000000000000000000020 // 数据偏移
0x000000000000000000000000000000000000000000000000000000000000001a // 字符串长度
0x4e6f7420656e6f7567682045746865722070726f76696465642e000000000000 // 字符串数据
```


### try catch 如何使用
try catch 用来捕获异常

```typescript
interface DataFeed { function getData(address token) external returns (uint value); }

contract FeedConsumer {
    DataFeed feed;
    uint errorCount;
    function rate(address token) public returns (uint value, bool success) {
        require(errorCount < 10); //如果错误计数超过10次，永久关闭
        try feed.getData(token) returns (uint v) {
            return (v, true);
        } catch Error(string memory /*reson*/) {
            // 如果getData中调用了revert('balabala')
            errorCount++;
            return (0, false);
        } catch (bytes memory /*lowLevelData*/) {
            // 如果getData中调用了revert()
            errorCount++;
            return (0, false);
        }
    }
}
```

try 后面**必须**紧跟一个代表外部函数调用或者合约创建的(`new ContractName()`)的表达式，表达式本身如果报错了，这个是不会catch的

solidity支持不同种类的catch代码块，如果错误是由`revert("reasonString")`或者`require(false, "reasonString")` 那么`catch Error(string memory reason)`对于的代码块会被执行

如果没有错误签名不匹配其他的语句，那么`catch (bytes memory lowLevelData)`就会执行

如果对错误数据不感兴趣可以简单的用`catch {...}`


## Contracts 合约
### library 中为啥不能有状态变量
这主要是出于安全考虑，当使用`delegatecall`去调用一个合约的时候，是在当前调用方的语境下运行被调用方的代码，如果被调用方的代码中包含修改状态变量的代码，那么调用方的变量就会被改变


### constant 和 immutable 有什么区别
状态变量可以被声明为`constant`或`immutable`, 这两种情况下，变量在创建之后都不能修改，对于`constant`变量，它的值在编译时是固定的，对于`immutable`来说，他可以在构造时赋值

你可以在文件层面定义`constant`变量

编译器不会为这些变量保留`storage slot`每一次出现这些变量的时候，就会被编译器替换为对应的值

对比正常的状态变量，`constant`和`immutable`变量的gas消耗会更加低，对于一个`constant`变量，如果赋值一个表达式给这个变量，那么这个变量每次出现的时候都会被这个表达式替换，而且每次都会重新求值. 对于一个`immutable`变量来说，它在构造时会求一次值，然后这个值会被复制到所有这个变量出现的地方，编译器会给这些值预留32个字节即使这些值可能小于32个字节，这也是为什么`constant`变量有时候比`immutable`变量更便宜

目前`0.8.0`, 不是所有的类型都可以声明成`constant`或者`immutable`的，只实现了`string`(只对constant), 和值类型

```typescript
uint constant X = 32**22 + 8;
contract C {
    string constant TEXT = "abc";
    bytes32 constant MY_HASH = keccak256("abc");
    uint immutable decimals;
    uint immutable maxBalance;
    address immutable owner = msg.sender;
    
    constructor(uint _decimals, address _reference) {

    }
}
```

对于`constant`变量，在编译时它的值必须是常量，并且这个变量在声明的时候必须赋值，任何访问storage, 区块链数据(`block.timestamp`, `address(this).balance`或者`block.number`)或者执行时数据(`msg.value`, `gasleft()`)或者对外部合约进行调用的操作都是不允许的

对于内存分配有副作用的表达式是允许的，但是可能对其他内存有副作用的操作就不被允许了. 内置函数诸如`keccak256`, `sha256`, `ripemd160`, `ecrecover`, `addmod`和`mulmod`都是允许的，尽管`keccak256`确实会调用外部合约

允许内存分配的副作用背后的原因是构建一个复杂对象应该是可能的，但是这个特性没有完全可用

对于`immutable`变量，他比起`constant`变量限制要更少一点，`immutable`可以在构造器里面赋任意的值，或者在声明的时候赋任意的值，他们在构造时不能读取，并且只能赋值一次，编译器生成的`creation code`在它执行完之前会改变它返回的`runtime code`, 具体来说他会把所有对`immutable`变量的引用都替换为赋给这个变量的值，这一点对于在比较编译器生成的`runtime code`和实际存放在区块链中的`runtime code`的人来说还是很重要的


### 定义在合约外的函数和定义在合约内的函数有啥区别
函数可以定义在合约的外面和内部

合约外部的函数被称为"free functions 自由函数"，它总是隐式的被设为`internal`, 他们的代码被包含在了所有的调用了他们的合约中，类似于`internal library`函数

```typescript
function sum(uint[] memory _arr) pure returns (uint s) {
    for (uint i = 0; i < _arr.length; i++)
        s += _arr[i];
}

contract ArrayExample {
    bool found;
    function f(uint[] memory _arr) public {
        uint s = sum(_arr);
        require(s >= 10);
        found = true;
    }
}
```

定义在合约外部的函数还是可以在合约的语境下执行的，可以访问`this`变量，可以调用其他的合约，发送以太坊，主要区别就是`free function`不能够直接访问storage变量

### 函数参数
函数可以把一个有类型的参数作为输入，并且不像其他的语言，还可以返回任意数量的值作为输出

函数参数声明的方式和定义变量的方式是一样的，没有用到的变量的名字可以省略

函如果你想要你的合约接受一种具有两个整型的`external`调用的话，你就需要这样

```typescript
contract simple {
    uint sum;
    function taker(uint _a, uint _b) public {
        sum = _a + _b;
    }
}
```

函数参数可以用做一个本地变量，也可以给他赋值

一个外部函数是不能接受一个多维数组作为输入参数的，这个功能可以通过在源文件里添加`pragma abicoder v2;`来开启. 一个内部函数可以接受一个多维数组作为输入参数，即使没开启这个


### 返回变量
返回变量的声明和函数参数声明的语法是一样的，不过要跟在`returns`后面

假设你想要返回两个结果，两个整数的和以及两个整数的积

```typescript
contract C {
    function arithmetic(uint _a, uint _b)
        public
        pure
        returns (uint o_sum, uint o_product)
    {
        o_sum = _a + _b;
        o_product = _a * _b;
    }
}
```

返回变量的名字可以省略，返回变量可以用作本地变量，返回变量会初始化为默认值

你可以显式的给返回变量赋值然后就把它放在那里，也可以选择直接把这些值放在`return`语句里

```typescript
contract C {
    function arithmetic(uint _a, uint _b)
        public
        pure
        returns (uint o_sum, uint o_product)
    {
        return (_a + _b, _a * _b);
    }
}
```


### view 修饰符如何使用
如果一个函数被声明为了`view`那么它必须不修改状态

以下情况被认为是修改了状态
- 写入状态变量
- 发出一个事件
- 创建其他合约
- 使用`selfdestruct`
- 通过`calls`来发送Ether
- 调用了没被标记为`view`或者`pure`的函数
- 使用了底层的`calls`
- 使用了包含某些操作码的内联汇编

`0.5.0`之前`用来修饰函数的`constant`是`view`的别名，`0.5.0`之后被移除

getter函数被自动标记为`view`

在`0.5.0`之前编译器不会为`view`函数使用`STATICCALL`操作码，这会导致状态可以被一些无效的显式类型转换所改变


### pure 修饰符如何使用
被声明为`pure`的函数不能**读取**和**修改**状态

除了上一小节提到的改变状态的例子，下面的被认为是读取状态

- 读取状态变量
- 访问`address(this).balance`或者`<address>.balance`
- 访问任何`block`, `tx`, `msg`的成员除了`msg.sig`和`msg.data`
- 调用了没被标记为`pure`的函数
- 使用了包含某些操作码的内联汇编


### receive函数是个啥函数
一个合约最多有一个`receive`函数，用`receive() external payable { ... }`声明(不需要`function`关键字), 这个函数不能有参数，不能返回任何东西，并且必须有`external`和`payable`的，可以是`virtual`, 可以重写并且可以有修饰符

`receive`函数会在你对一个合约发出了一个空的`calldata`的调用的时候执行，在普通的Ether转移操作(`.send()` `.transfer()`)时也会执行，如果没有这样的函数存在，但是有个`payable fallback`函数存在的话，这个`fallback`函数会在Ether转移操作时调用，如果既没有`receive函数`也没有`payable fallback`函数的存在的话，这个合约就不能通过常规交易接收Ether并且会抛出一个异常

`receive`函数只能依赖2300 gas, 当用了`send`或`transfer`的时候，以下操作会消耗多于2300 gas

- 写入storage
- 创建合约
- 调用消耗大量gas的外部函数
- 发送Ether

一个没有`receive`函数的合约可以做为`coinbase transaction`的接受者，或者`selfdestruct`的接受者


### fallback函数是个啥函数
一个合约最多有一个`fallback`函数，用`fallback() external [payable]`或`fallback (bytes calldata _input) external [payable] returns (bytes memory _output)`(不需要`function`关键字) 这个函数必须是`external`的，可以是`virtual`, 可以重写并且可以有修饰符

如果对一个合约发起`call`的时候，没有其他的函数匹配给定的函数签名，那么`fallback`函数就会执行，或者当没有任何数据提供且没有`receive`函数的时候

`fallback`函数总是会接收数据，但是为了接收Ether, 它必须标记为`payable`

```typescript
contract Test {
    uint x;
    // 所有的消息发送到这个合约都会调用这个函数(因为没有其他的函数)
    // 发送Ether到这合约会导致异常
    fallback() external { x = 1; }
}

contract TestPayable {
    // 所有发送到这个合约的消息，除了普通的Ether转移都会调用这个函数
    // 任何具有非空的calldata来call这个合约的都会执行这个函数，即使
    // call的时候还附带了Ether
    fallback() external payable { x = 1; y = msg.value; }

    // `plain Ether tranfers`普通Ether转移会调用这个函数
    // 也就是所有具有空calldata的call
    receive() external payable { x = 2; y = msg.value; }
    uint x;
    uint y;
}

contract Caller {
    function callTest(Test test) public returns (bool) {
        (bool success,) = address(test).call(abi.encodeWithSignature("nonExisting()"))
        require(success);
        // test.x 会变成 1

        // address(test) 不会允许直接调用send, 因为test没有payable的fallback函数
        // 必须转换为address payable才能允许调用send
        address payable testPayable = payable(address(test));
    }

    function callTestPayable(TestPayable test) public returns (bool) {
        (bool success,) = address(test).call(abi.encodeWithSignature("nonExisting()"));
        require(success);
        // test.x 会变成 1 test.y 会变成 0

        (success,) = address(test).call{value: 1}(abi.encodeWithSignature("nonExisting()"));
        require(success);
        // test.x 会变成 1 test.y 会变成 1 wei

        // 如果给TestPayable合约发送Ether, TestPayable的receive函数会被调用
        require(payable(test).send(2 ether));
        // test.x 会变成 2 test.y 会变成 2 ether
    }
}
```


### 函数重载
一个合约可以有多个不同参数类型相同名字的函数，这个过程就是**重载**并且对继承的函数也适用，下面的例子展示了合约`A`作用域里的函数`f`的重载

```typescript
contract A {
    function f(uint _in) public pure returns (uint out) {
        out = _in;
    }

    function f(uint _in, bool _really) public pure returns (uint out) {
        if (_really)
            out = _in;
    }
}
```

重载函数也会出现在外部接口上，如果两个外部可见的函数在solidity类型上是不同的，但是外部类型是一致的就会报错，这个有点不好理解，看下面的代码

```typescript
contract A {
    function f(B _in) public pure returns (B out) {
        out = _in;
    }

    function f(address _in) public pure returns (address out) {
        out = _in;
    }
}

contract B {
}
```

虽然在solidity内部这两个函数的参数类型是不一样的，但是在ABI的层面，他们都是接收address类型的，所以是错误的


### 重载解析和参数匹配
重载函数是通过匹配当前作用域和函数调用的参数来选择的，如果所有参数都可以被隐式转换成所期待的类型，那么这个函数就会被选为候选函数，如果没有候选函数，重载解析就会失败

> 返回参数不会被考虑近重载解析

```typescript
contract A {
    function f(uint8 _in) public pure returns (uint8 out) {
        out = _in;
    }

    function f(uint256 _in) public pure returns (uint256 out) {
        out = _in;
    }
}
```

调用`f(50)`会创建一个类型错误，因为`50`可以被隐式转换为`uint8`和`uint256`

调用`f(256)`会解析为`f(uint256)`因为`256`不能隐式转换为`uint8`


### 事件
solidity的事件在EVM的logging功能上添加了一层抽象，应用可以通过一个以太坊客户端的RFC接口订阅和监听这些事件

事件是可继承的合约成员，当你调用他们的时候，他们会导致参数被存放在交易的log里，这是区块链的一个特殊的数据结构，这个log是和合约的地址相关联 的，log是合并在区块链里的，只要区块可以访问log都可以访问(现在是永久可以访问，但是Serenity之后可能会边)

log和它的事件数据不能从合约访问(即使从创建这个事件的合约处也不行)

获取一个log的`Merkle proof`是可以的，所以如果一个外部实体提供了一个有这个证明的合约的话，那么他就可以检查是否真的存在于区块链里，你必须支持区块头因为合约只能看到最近的256个区块哈希

你可以添加给三个参数添加`indexed`属性，这会把他们加入到一个特殊的被称为`topics`的数据结构里，而不是作为log的数据部分，如果你使用数组(包括`string`和`bytes`)作为`indexed`参数，那么他们的`Keccak-256`哈希会被保存在topic里面，因为topic只能存放一个字(32 字节)

所有没有`indexed`属性的参数都会被ABI编码作为log的数据部分

`topic`允许你搜索事件，比如用指定的事件过滤一段区块，你也可以用发出这个事件的合约的地址来过滤事件

比如，下面的例子使用web3.js`subscribe("log")`方法来过滤匹配特定地址的topic的logs

```typescript
var options = {
    fromBlock: 0,
    address: web3.eth.defaultAccount,
    topics: ["0x0000000000000000000000000000000000000000000000000000000000000000"，null, null]
}
web3.eth.subscribe('logs'，options, function(error, result) {
    if(!error)
        console.log(result)
}).on("data"，function(log){
    console.log(log)
}).on("changed"，function(log) {

})
```

事件的签名的哈希是一个topics, 除非你给事件声明了一个`anonymous`, 这意味着不可能通过名字来过滤一个匿名的事件，你只能通过合约地址来过滤，匿名事件的优点就是他们部署和调用更加便宜

```typescript
contract ClientReceipt {
    event Deposit(
        address indexed _from,
        bytes32 indexed _id,
        uint _value
    )
    
    function deposit(bytes32 _id) public payable {
        // 事件可以使用emit发出，跟着事件的名字和括号里的参数
        // 任何这样的事件都可以用JS API来检测
        emit Deposit(msg.sender, _id, msg.value); 
    }
```
JS API如下

```typescript
var abi = //
var ClientReceipt = web3.eth.contract(abi)
var clientReceipt = ClientReceipt.at("")
var event = clientReceipt.Deposit()

// watch for changes
event.watch(function(error, result){
    if (!error)
        console.log(result)
})

// 直接传入回调函数立即watch
var event = clientReceipt.Deposit(function(error, result){
    if(!error)
        console.log(result)
})
```

- [web3 event](https://github.com/ethereum/web3.js/blob/1.x/docs/web3-eth-contract.rst#events)
- [event 例子](https://github.com/ethchange/smart-exchange/blob/master/lib/contracts/SmartExchange.sol)
- [如何用js访问他们](https://github.com/ethchange/smart-exchange/blob/master/lib/exchange_transactions.js)


### 继承
solidity支持包含多态的多继承

当一个合约继承了其他合约，只有一个合约被创建在了区块链，所有的`base contract`都会被编译到被创建的合约里，这意味着所有的对`base contract`内部函数调用也会用内部函数调用(`super.f(..)`会使用`JUMP`而不是消息调用)

状态变量覆盖被认为是错误，一个衍生合约只能声明一个没有重复过的变量

```typescript
contract Owned {
    constructor() { owner = payable(msg.sender); }
    address payable owner;
}

// 使用is来继承另一个合约，衍生的合约可以访问所有
// 非私有成员包括内部函数和状态变量，
// 不过这些都不能通过this来进行外部访问
contract Destructible is Owned {
    // 关键字virtual代表了函数在衍生类中可以改变他的行为，也就是重载
    function destroy() virtual public {
        if (msg.sender == owner) selfdestruct(owner);
    }
}

// 这些抽象合约只是用来让编译器知道这个接口interface的
// 抽象合约的函数是没有函数体的
// 如果一个合约不能够实现所有的函数，他只能被当作一个接口interface
abstract contract Config {
    function lookup(uint id) public virtual returns (address adr);
}

abstract contract NameReg {
    function register(bytes32 name) public virtual;
    function unregister() public virtual;
}

// 多继承是可以的，Owned是Destructible的基类，但是只有一个Owned的实例
contract Named is Owned, Destructible {
    constructor(bytes32 name) {
        Config config = Config(0xD5f9D8D94886E70b06E474c3fB14Fd43E2f23970);
        NameReg(config.lookup(1)).register(name);
    }

    // 函数可以被其他有相同名字和相同数量的输入的函数重写
    // 如果重写函数有不同类型的输出参数，会导致错误
    // 这个重写在本地的和基于消息的函数调用都算数
    // 如果你想要重写函数，你需要指定`override`
    // 如果你想要你的重写函数继续能被重写，你需要指定`virtual`
    function destroy() public virtual override {
        if (msg.sender == owner) {
            Config config = Config(0xD5f9D8D94886E70b06E474c3fB14Fd43E2f23970);
            NameReg(config.lookup(1)).unregister();
            // 被重写了的函数还是可以调用的
            Destructible.destroy();
        }
    }
}


contract PriceFeed is Owned, Destructible, Named("GoldFeed") {
    uint info;

    function updateInfo(uint newInfo) public {
        if (msg.sender == owner) info = newInfo;
    }

    // 这里只指定了override但是没有virtual, 则意味着任何从PriceFeed继承的合约不能改变destroy的行为
    function destroy() public override(Destructible, Named) { Named.destroy(); }
    function get() public view returns(uint r) { return info; }
    }
```

像上面那样直接调用`Destructible.destroy()`是有问题的

```typescript
contract owned {
    address payable owner;
    constructor() { owner = payable(msg.sender); }
}

contract Destructible is owned {
    functionn destroy() public virtual {
        if (msg.sender == owner) selfdestruct(owner);
    }
}

contract Base1 is Destructible {
    function destroy() public virtual {
        if (msg.sender == owner) selfdestruct(owner);
    }
}

contract Base2 is Destructible {
    function destroy() public virtual {
        if (msg.sender == owner) selfdestruct(owner);
    }
}

contract Final is Base1, Base2 {
    function destroy() public override(Base1, Base2) { Base2.destroy(); }
}
```

调用`Final.destory()`会调用`Base2.destroy`因为我们显式的在最后的重写中指定了，但是这个函数会绕过`Base1.destroy`, 这时我们就需要`super`了

```typescript
contract owned {
    address payable owner;
    constructor() { owner = payable(msg.sender); }
}

contract Destructible is owned {
    functionn destroy() public virtual {
        if (msg.sender == owner) selfdestruct(owner);
    }
}

contract Base1 is Destructible {
    function destroy() public virtual {
        if (msg.sender == owner) super.destroy();
    }
}

contract Base2 is Destructible {
    function destroy() public virtual {
        if (msg.sender == owner) super.destroy();
    }
}

contract Final is Base1, Base2 {
    function destroy() public override(Base1, Base2) { super.destroy(); }
}
```

如果`Base2`调用了`super`的函数，他不会简单的调用它的一个基合约的函数，而是调用继承图上的下一个基合约，所以会调用`Base1.destroy()`(继承序列是这样的: `Final`, `Base2`, `Base1`, `Destructible`, `owned`)


### 函数重写
如果基类的函数被标记为了`virtual`, 那么它可以被继承了它的合约重写来改变它的行为

重写函数必须在函数的头部使用`override`关键字，重写函数可以只把被重写函数的可见性从`external`改为`public`, `nonpayable`可以被重写为`view`和`pure`, `view`可以被重写为`pure`, `payable`是个例外并且不能被改为其他的可变性

`private`的可见性的函数的可变性不能是`virtual`

在interface外的没有实现的函数必须被标记为`virtual`, 在interface内，所有的函数都被视为`virtual`

这个例子展示了可变性和可见性

```typescript
contract Base {
    function foo() virtual external view {}
}

contract Middle is Base {}

contract Inherited is Middle {
    function foo() override public pure {}
}
```

如果一个合约从多个基合约继承了相同的函数，必须显式的重写它

```typescript
contract Base1 {
    function foo() virtual public {}
}

contract Base2 {
    function foo() virtual public {}
}

contract Inherited is Base1, Base2 {
    function foo() public override(Base1, Base2) {}
}
```

在函数的参数和返回类型和状态变量的getter匹配的时候，可以用状态变量可以重写外部函数

```typescript
contract A {
    function f() external view virtual returns(uint) { return 5; }
}

contract B is A {
    uint public override f;
}
```

虽然public状态变量可以重写外部函数，他们自己本身不能被重写


### 修饰符重写
函数修饰符可以相互重写，这和函数重写是一样的(除了修饰符没有重载), 被重载的修饰符必须使用`virtual`, 重载的修饰符必须使用`override`

```typescript
contract Base {
    modifier foo() virtual {_;}
}

contract Inherited is Base {
    modifier foo() override {_;}
}
```

在多继承的情况下，所有直接的基合约都必须显式指定

```typescript
contract Base1
{
    modifier foo() virtual {_;}
}

contract Base2
{
    modifier foo() virtual {_;}
}

contract Inherited is Base1, Base2
{
    modifier foo() override(Base1, Base2) {_;}
}

```


### 构造器
构造器是一个可选的函数，它在合约创建的时候执行，是运行合约初始化代码的地方

在构造器代码执行之前，状态变量被初始化为内联的值或者0

在构造器运行后，最终的合约的代码被部署在区块链上，合约部署消耗的gas费用和代码的长度线性相关，代码包含了`public interface`部分的所有函数和可以通过函数调用调用的函数，不包括构造器代码和只在构造器中出现的内部函数

如果没有构造器，那么合约会采用一个默认的构造器，也就是`constructor() {}`

```typescript
abstract contract A {
    uint public a;

    constructor(uint _a) {
        a = _a;
    }
}

contract B is A(1) {
    constructor() {}
}
```

`0.4.22`之前，构造器被定义为和合约具有相同名字的函数，这个语法在`0.5.0`后被废弃，且不再允许了

`0.7.0`之前，你必须给构造器指定一个可见性，`internal`或者`public`


### 基构造器的参数
所有的基合约的构造器都会根据下面解释的线性化规则调用一遍

如果基构造器有参数，衍生合约需要指定所有的参数，这有两个做法

```typescript
contract Base {
    uint x;
    constructor(uint _x) { x = _x; }
}

// 1. 直接在继承列表里指定
contract Derived1 is Base(7) {
    constructor() {}
}

// 或者通过衍生构造器的修饰符
contract Derived2 is Base {
    constructor(uint _y) Base(_y * _y) {}
}
```

如果构造器参数是常量那么第一种方式更方便，如果构造的参数是依赖于衍生合约的话，那么第二个方式更方便

参数只能在1处指定，两处都指定参数会报错

如果衍生合约没有指定它的所有的基合约的构造器的参数，那么这个衍生合约是一个抽象`abstract`的


### 多继承和线性化
允许多继承的语言必须要处理几个问题，一个就是[钻石问题](https://en.wikipedia.org/wiki/Multiple_inheritance#The_diamond_problem), solidity和python相似的地方在于使用[C3 线性化](https://zh.wikipedia.org/wiki/C3%E7%BA%BF%E6%80%A7%E5%8C%96)在基类的有向无环图中强制指定顺序，这导致了单调性的理想特性，但是有一些继承图就不允许了

另一个简单的解释这个的方式是一个在不同合约中定义了多次的函数被调用时，指定的基类会被从右到左深度优先搜索(Python是从左到右), 第一匹配就停下

如果基合约以及被找到，那么就跳过


### 继承相同名的成员的不同种类

如果下面的几个对在合约中由于继承有相同的名字，那么会报错

- 函数和修饰符
- 函数和事件
- 事件和修饰符

例外是，状态变量的getter可以重写一个外部函数


### 抽象合约
当至少有一个函数没被实现的时候，合约必须被标记为`abstract`, 即使所有的函数都被实现了，合约还是可以被标记为`abstract`

```typescript
abstract contract Feline {
    function utterance() public virtual returns (bytes32);
}
```

抽象合约不能直接被实例化，就算抽象合约实现了所有函数也不行

```typescript
abstract contract Feline {
    function utterance() public virtual returns (bytes32);
}

contract Cat is Feline {
    function utterance() public override returns (bytes32) { return "miaow"; }
}
```

没有实现的函数和函数类型变量是不一样的，虽然他们的语法看上去很相似

```typescript
// 没有实现的函数
function foo(address) external returns (address);
// 函数类型的变量
function (address) external returns (address) foo;
```

抽象合约不能有一个没有实现的函数去重写一个实现了的`virtual`函数


### 接口
接口和抽象函数很相似，但是他们不能有任何函数实现，以下是其他限制

- 他们不能继承其他的合约，但他们可以继承其他的接口
- 所有声明的函数必须是外部的
- 他们不能定义构造器
- 他们不能定义状态变量

接口基本上被限制在了合约ABI能表示的东西里，并且ABI和接口之间的转换应该是可以没有信息损失的

```typescript
interface Token {
    enum TokenType { Fungible, NonFungible }
    struct Coin { string obverse; string reverse; }
    function transfer(address recipent, uint amount) external;
}
```

合约可以继承接口

所有定义在接口里的函数都是隐式的`virtual`的，这意味着他们可以被重写

接口可以继承其他的接口，这和普通的继承有一样的规则

```typescript
interface ParentA {
    function test() external returns (uint256);
}

interface ParentB {
    function test() external returns (uint256);    
}

interface SubInterface is ParentA, ParentB {
    function test() external override(ParentA, ParentB) returns (uint256);
}
```

定义在接口和其他的类似合约的结构里的类型都可以从其他的合约访问`Token.TokenType` `Token.Coin`


### 库 Libraries
和合约相比，库有下面几个限制
- 不能有状态变量
- 不能继承或被继承
- 不能接收Ether
- 不能被摧毁

库类似于其他的合约，但是它的目的是只部署在某个地址一次，并且它的代码会用`DELEGATECALL`复用，这意味这如果库函数被调用了，它的代码会在调用库函数的合约的语境下执行，特别要注意的是调用库函数的合约的storage是可以被库函数访问的

如果一个库函数没有改变状态(`view`或者`pure`), 那么他不能被直接调用，`0.4.20`之前，可以通过绕过solidity的类型系统来摧毁一个库，之后库就引入了不允许更改状态的函数在没有用`DELEGATECALL`的情况下直接发起`call`

因为库被认为是无状态的，所以是不可能摧毁一个库的

库可以被视为一个使用了库的合约的基合约，虽然他们在继承层级里不是显式可见的，但是对库函数的调用就像是在调用一个显式的基合约里的函数一样。当然，调用内部函数还是要是用内部调用约定的，这个约定就是可以传递内部类型而且memory中的类型会被用按引用传递，而不是拷贝。为了在EVM里实现这一点，内部库函数的代码和所有被调用的函数在编译时必须被包含在调用库函数的合约里，这样就可以使用`JUMP`而不是`DELEGATECALL`了

下面的例子展示了如何使用库，之后会讲解`using for`

```typescript
struct Data {
    mapping(uint => bool) flags;
}

library Set {
    // 第一个参数的类型是storage引用，也可以说是storage的指针
    // 所以传参的时候传的是地址而不是真的内容，则是库函数的特点
    
    // 如果函数可以被视为是一个对象的方法的话，那么第一个参数命名为self是一个习惯写法
    function insert(Data storage self, uint value) public returns (bool) {
        if (self.flags[value])
            return false;
        self.flags[value] = true;
        return true;
    }

    function remove(Data storage self, uint value) public returns (bool) {
        if (!self.flags[value])
            return false;
        self.flags[value] = false;
        return true;
    }

    function contains(Data storage self, uint value) public view returns (bool) {
        return self.flags[value];
    }
}

contract C {
    Data knownValues;

    function register(uint value) public {
        // 库函数可以在没有具体的库的实例的时候调用
        // 因为这个"实例"就是当前合约
        require(Set.insert(knownValues, value));
    }
    // 在这个合约里，我们可以直接访问knownValues.flags
}
```

当然，你也不需要这样去使用库，库可以在不需要定义结构体数据类型的情况下使用，函数也可以在没有storage引用参数的情况下工作，而且函数也可以在任何位置有多个storage引用参数

`Set.contains`, `Set.insert`和`Set.remove`这样的调用都被编译成了对于外部合约和库的`DELEGATECALL`。 如果你在使用库，要注意实际会发生的外部函数调用。 `msg.sender`, `msg.value`和`this`会在这个调用里保持他们原来的值(不过在`Homestead`版本之前，由于用的是`CALLCODE`, `msg.sender`和`msg.value`会变化)

下面的例子展示了如何用memory类型和库的内部函数来在没有外部函数调用的开销的情况下实现自定义类型的

```typescript
struct bigint {
    uint[] limbs;
}

library BigInt {
    function fromUint(uint x) internal pure returns (bigint memory r) {
        r.limbs = new uint[](1);
        r.limbs[0] = x;
    }

    function add(bigint memory _a, bigint memory _b) internal pure returns (bigint memory r) {
        r.limbs = new uint[](_a.limbs.length, _b.limbs.length);
        uint carry = 0;
        for (uint i = 0; i < r.limbs.length; i++) {
            uint a = limb(_a, i);
            uint b = limb(_b, i);
            r.limbs[i] = a + b + carry;
            if (a + b < a || (a + b == type(uint).max && carry > -))
                carry = 1;
            else
                carry = 0;
        }
        if (carry > 0) {
            // 加个limb
            uint[] memory newLimbs = new uint[](r.limbs.length + 1);
            uint i;
            for (i=0; i < r.limbs.length; i++)
                newLimbs[i] = r.limbs[i];
            newLimbs[i] = carry;
            r.limbs = newLimbs;
        }
    }

    function limb(bigint memory _a, uint _limb) internal pure returns (uint) {
        return _limb < a.limbs.length ? _a.limbs[_limb] : 0;
    }

    function max(uint a, uint b) private pure returns (uint) {
        return a > b ? a : b;
    }
}

contract C {
    using BigInt for bigint;
    function f() public pure {
        bigint memory x = BigInt.fromUint(7);
        bigint memory y = BigInt.fromUint(type(uint).max);
        bigint memory z = x.add(y);
        assert(z.limb(1) > 0);
    }
}
```

通过把`library`类型转换为`address`类型来获得库的地址是可以的`address(libraryName)`

因为编译器不知道库会被部署在那个地址，编译后的十六进制代码会包含类似`__$30bbc0abd4d6364515865950d3e0d10953$__`的占位符，这个占位符有34个字符，是`完全限定库名 fully qualified library name`的keccak256哈希编码的34个前缀，完全限定库名就是一个类似这样的`libraries/bigint.sol:BigInt`的名字，库在`libraries/`目录下的`bigint.sol`文件里

这样的字节码是不完整的，也不应该被部署

占位符需要被替换为实际的地址，你可以在库被编译的时候把实际地址传给编译器，或者通过`linker`来更新已经被编译的字节码


### 库的调用保护
如果库的代码是使用`CALL`调用而不是`DELEGATECALL`调用的，那么他就会`revert`, 除非调用的函数是`view`或者`pure`

EVM并没有直接检测是否这个合约有没有被`CALL`调用，但是可以用`ADDRESS`操作码来找到当前运行代码的地址，编译器为库生成的代码会比较这个地址和构造时的地址来确定调用的类型

更具体一点，运行时的库的代码总是从一个push操作开始，push的值在编译时是20字节的空数据，在部署的时候，这个常量会被内存里的当前地址替换，经过这么一次替换后的代码会保存在合约里。在运行时，这会导致部署时的地址会成为第一个push进堆栈的常量，调度代码会给每个不是`view`或`pure`的函数比较当前的地址和这个常量

这就意味着实际上保存在链上的代码和编译器报告为`deployedBytecode`的代码不一样


### using for
指令`uisng A for B`可以用来给合约上下文的类型`B`附加库`A`的函数。这些函数会接收他们调用时的对象作为第一个参数(就像Python里的`self`变量)

`using A for *;`的效果就是给所有类型都附加上库`A`的函数

两种情况下，所有库中的函数都会被附加上，就算第一个参数的类型和对象的类型不匹配也会附加上去。在函数调用的时候才会做类型检查，函数重载解析也会进行

`using A for B`只有在当前合约才有有效，在合约外部无效，这个指令只能用在合约里不能用在函数里

```typescript
struct Data {
    mapping(uint => bool) flags;
}

library Set {
    function insert(Data storage self, uint value) public returns (bool) {
        if (self.flags[value])
            return false;
        self.flags[value] = true;
        return true;
    }

    function remove(Data storage self, uint value) public returns (bool) {
        if (!self.flags[value])
            return false;
        self.flags[value] = false;
        return true;
    }

    function contains(Data storage self, uint value) public view returns (bool) {
        return self.flags[value];
    }
}

contract C {
    using Set for Data; // 这是一个重要的变化
    Data knownValues;

    function register(uint value) public {
        // 所有Data类型的变量都会有对应的成员函数
        // 下面的函数调用和`Set.insert(knownValues, value)`
        // 是相同的
        require(knownValues.insert(value));
    }
}
```

也可以用这个方式扩展基本类型

```typescript
library Search {
    function indexOf(uint[] storage self, uint value) public view returns (uint) {
        for (uint i = 0; i < self.length; i++)
            if (self[i] == value) return i;
        return type(uint).max;
    }
}

contract C {
    using Search for uint[];
    uint[] data;

    function append(uint value) public {
        data.push(value);
    }

    function replace(uint _old, uint _new) public {
        uint index = data.indexOf(_old);
        if (index == type(uint).max)
            data.push(_new);
        else
            data[index] = _new;
    }
}
```

记住，所有的`external library calls 外部库调用`实际上都是`EVM function calls EVM函数调用`, 即使是`self`变量。唯一没有拷贝发生的情况是storage引用变量被使用或者`internal library functions 内部库函数`被调用的时候


## Inline Assembly 内联汇编
内联汇编是一个可以和solidity语句写一起的更加贴近EVM的语言，内联汇编会给予你更加细粒度的控制，在你想要通过库来增强solidity的能力的时候尤其有用

solidity的内联汇编语言叫[Yul](https://docs.soliditylang.org/en/v0.8.0/yul.html#yul), 本章主要描述内联汇编如何和solidity的代码交互的

内联汇编会绕过很多重要的安全特性和solidity的检查，你应该只在需要的场合使用它，并且只在你知道自己在干嘛的时候使用它

内联汇编代码块又`assembly { ... }`标记，花括号内部的代码为Yul语言

不同的内联汇编代码块不分享命名空间

下面的代码提供了一个能够访问另一个合约的代码并将代码加载进一个`bytes`类型的变量里，这是一定要用内联汇编来做的，而内联汇编背后的思想就是用复用的汇编库来在不需要编译器变化的情况下增强solidity语言

```typescript
library GetCode {
    function at(address _addr) public view returns (bytes memory o_code) {
        assembly {
            // 获取代码的大小，这需要汇编
            let size := extcodesize(_addr)
            // 分配输出字节数组，这个操作不汇编也能完成
            // o_code = new bytes(size)
            o_code := mload(0x40)
            mstore(0x40, add(o_code, and(add(add(size, 0x20), 0x1f), not(0x1f))))
            // 在内存中存储长度
            mstore(o_code, size)
            // 获取代码，这需要汇编
            extcodecopy(_addr, add(o_code, 0x20), 0, size)
        }
    }
}
```

内联汇编在优化器不能产生有效率的代码的时候也是有很大的帮助的

```typescript
library VectorSum {
    // 这个函数效率不是很高，因为现在的优化器不能够移除数组访问的越界检查
    function sumSolidity(uint[] memory _data) public pure returns (uint sum) {
        for (uint i = 0; i < _data.length; ++i)
            sum += _data[i]
    }

    // 我们知道我们不会越界，所以我们可以避免检查，给数组加0x20是因为第一个slot放的是数组的长度
    function sumAsm(uint[] memory _data) public pure returns (uint sum) {
        for (uint i = 0; i < _data.length; i++) {
            assembly {
                sum := add(sum, mload(add(add(_data, 0x20), mul(i, 0x20))))
            }
        }
    }

    // 和上面的一样，但是全部代码都是内联汇编
    function sumPureAsm(uint[] memory _data) public pure returns (uint sum) {
        assembly {
            // 加载数组长度(第一个32字节)
            let len := mload(_data)

            // 跳过存放长度的域
            let data := add(_data, 0x20)

            // 遍历
            for 
                { let end := add(data, mul(len, 0x20))}
                lt(data, end)
                { data := add(data, 0x20) }
            {
                sum := add(sum, mload(data))
            }
        }
    }
}
```


### 访问外部的变量，函数和库
可以通过名字来访问solidity的变量和其他的标识符

值类型的本地变量可以直接在内联汇编中使用

引用了`memory`或者`calldata`的本地变量的值会是变量在内存的地址而不是变量的值本身

对于本地storage变量或者状态变量，一个yul标识符是不足以表示的，因为这些变量不一定就占用一整个storage slot。因此，他们的"地址"是由slot和slot内的字节偏移组成的。为了获得指向变量`x`的slot, 你需要使用`x.slot`, 用`x.offset`获得字节偏移。使用`x`本身会导致错误

对于动态calldata数组，你可以访问calldata的偏移`x.offset`和长度`x.length`。这两个表达式都可以被赋值

本地solidity变量也是可以赋值的

```typescript
contract C {
    uint b;
    function f(uint x) public view returns (uint r) {
        assembly {
            // 我们忽略了storage slot偏移，因为这个情况下是0
            r := mul(x, sload(b.slot))
        }
    }
}
```

如果你访问一个小于256位的类型(比如`uint64`, `address`, `bytes16`)的变量。不要假设变量是0, 安全起见，在重要的场景下，总是在你使用变量之前合适的清理他: `uint32 x = f(); assembly { x := and(x, 0xffffffff) /* 现在再使用x */}` 可以使用`signextend`操作服清理有符号类型: `assembly { signextend(<num_bytes_of_x_minus_one>，x) }`


### solidity里的约定
和EVM汇编不同，solidity有短于256位的类型(`uint24`)。为了效率，大多数的算数操作忽略了类型可以比256位短的事实，并且必要的时候高阶的位会被清理。这意味着如果你在内联汇编里访问一个短于256位的变量，你可能首先需得手动清理高阶位

solidity是这样管理内存的。在内存的`0x40`这个位置有一个"自由内存指针"，如果你想要分配内存，从这个指针指向的内存开始然后更新这个指针，没有办法保证指向的这块内存之前是否被用过所以你不能指望这块内存的内容是0。没有内置的机制去释放已经分配了的内存。

下面的例子演示了如何用刚刚提到的方式分配内存

```typescript
function allocate(length) -> pos {
    pos := mload(0x40)
    mstore(0x40, add(pos, length))
}
```

内存里的前64个字节(0x00-0x3f)被用做`scratch space 暂存空间`作为短期分配，自由内存指针(0x40-0x5f)之后的32个字节(0x60-0x7f)永远是0并且是用来作为空的动态内存数组的初始值的。这意味着可分配的内存是从`0x80`开始的，这也是自由内存指针的初始值

solidity中的内存数组的元素总是占用32字节的倍数(这对`byte[]`成立但是对`bytes`和`string`不成立)。多维内存数组是指向内存数组的指针。动态数组的长度被存放在数组的第一个slot, 第一个slot后面跟着数组元素

静态长度内存数组没有长度slot, 但是之后可能会有，用来允许刚好的静态和动态长度数组之间的可转换性，所以不要依赖这个特点


## Contract Metadata 合约元数据
solidity编译器自动生成合约元数据的JSON文件，包含了被编译的合约的信息。你可以用这个文件来查询编译器的版本，ABI和NatSpec文档来更安全的与合约交互

编译器默认会在每个合约字节码的末尾追加元信息的IPFS哈希，所以你可以在不求助于中心化数据提供者的情况下获取文件。另一个可选的是用Swarm哈希然后不在字节码后面追加元数据哈希。这都是可以配置的

你需要把元信息文件发布在IPFS，Swarm或者其他的服务上，这样其他人才能访问。使用`solc --metadata`命令来生成一个名为`ContractName_meta.json`的文件。它包含了对于源代码的IPFS和Swarm引用，所以你必须更新所有的源文件和元数据文件

元数据文件的格式如下。下面的例子是人可读的。真实的元数据格式应该正确的使用引号，把空格减到最少并且给所有对象的键排序。注释是不允许的，这里只是为了解释

```json
{
  // Required: 元数据格式的版本
  version: "1",
  // Required: 源码的语言
  language: "Solidity",
  // Required: 编译器的细节, 具体看语言
  compiler: {
    // Required for Solidity: 编译器版本
    version: "0.4.6+commit.2dabbdf0.Emscripten.clang",
    // Optional: 编译器的二进制的哈希
    keccak256: "0x123..."
  },
  // Required: 编译源文件/源单元, 键是文件名
  sources:
  {
    "myFile.sol": {
      // Required: 源文件的keccak256哈希
      "keccak256": "0x123...",
      // Required (除非"content"用了, 下面会解释): 排序了的源文件URL, 协议可以随意, 但是推荐Swarm URL
      "urls": [ "bzzr://56ab..." ],
      // Optional: 源文件指定的 SPDX 许可证标识符
      "license": "MIT"
    },
    "destructible": {
      // Required: 源文件的keccak256哈希
      "keccak256": "0x234...",
      // Required (除非"url"用了): 源文件内容的字面量
      "content": "contract destructible is owned { function destroy() { if (msg.sender == owner) selfdestruct(owner); } }"
    }
  },
  // Required: 编译器设定
  settings:
  {
    // Required for Solidity: 排序的重新映射的列表
    remappings: [ ":g=/dir" ],
    // Optional: 优化器设置 "enabled"和"runs"废弃了，并且只在向后兼容的时候给出
    optimizer: {
      enabled: true,
      runs: 500,
      details: {
        // 默认为 "true"
        peephole: true,
        // jumpdestRemover默认为"true"
        jumpdestRemover: true,
        orderLiterals: false,
        deduplicate: false,
        cse: false,
        constantOptimizer: false,
        yul: true,
        // Optional: 只有"yul"为"true"时才出现
        yulDetails: {
          stackAllocation: false,
          optimizerSteps: "dhfoDgvulfnTUtnIf..."
        }
      }
    },
    metadata: {
      // 默认为 false
      useLiteralContent: true,
      // 默认为 "ipfs"
      bytecodeHash: "ipfs"
    }
    // Required for Solidity: 用于生成这个元数据的合约或者库的文件和名字
    compilationTarget: {
      "myFile.sol": "MyContract"
    },
    // Required for Solidity: 用了的库的地址
    libraries: {
      "MyLib": "0x123123..."
    }
  },
  // Required: 编译器生成的合约信息
  output:
  {
    // Required: 合约的ABI定义
    abi: [ ... ],
    // Required: 合约的NatSpec用户文档
    userdoc: [ ... ],
    // Required: 合约的NatSpec开发者文档
    devdoc: [ ... ],
  }
}
```


### 字节码中的元数据哈希的编码
元数据一般是编译完之后编译器追加在runtime代码的末尾的

![](https://tva1.sinaimg.cn/large/008eGmZEly1gmgqdojm1yj30jg048mxk.jpg)

你在反汇编的时候如果看到了`LOG1`后面跟着`PUSH6`大概率就是看到了元数据被反汇编的结果，元数据不是用来执行的，只是一堆数据而已


因为未来可能会支持其他的获取元数据文件的方式，`{"ipfs": <IPFS hash>, "solc": <compiler version>}`是用[CBOR编码](https://tools.ietf.org/html/rfc7049)的方式存储的。这个映射可能包含更多的键并且编码的开始不容易找到。当前版本的solidity编译器通常添加如下的字节码在部署的字节码的末尾

```
0xa2
0x64 'i' 'p' 'f' 's' 0x58 0x22 <34 bytes IPFS hash>
0x64 's' 'o' 'l' 'c' 0x43 <3 byte version encoding>
0x00 0x33
```

所以为了获取数据，可以检查部署字节码的末尾是否和这个模式匹配并且用IPFS哈希获取这个文件

