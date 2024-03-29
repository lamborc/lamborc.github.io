# NEAR 


## NEAR协议之彩虹桥

> 一个在密码学领域独特且高价值的完全去信任的桥，可以在以太坊与NEAR之间，以及最终与极光(Aurora)之间转移通证。

> 假设我要从以太坊转移20枚DAI到NEAR上。当然不可能在两个网络之间将通证进行物理转移，这意味着我们需要将20枚DAI移出以太坊上的流通，再投放20枚DAI到NEAR上流通，这样总的DAI流通量保持不变

##### 以下是通过无需许可且去信任的方式完成该需求的方法

- 告诉以太坊网络我要把20个DAI转移到其他地方；
- 以太坊锁定我的20个DAI到一个保管库（一个智能合约），这样它们就退出流通了；
- 一旦确认这20枚DAI已经被锁定在以太坊上了，我就告诉NEAR给我创建20个新的DAI；
- 然而空口无凭，NEAR要求我提供20枚DAI已经在以太坊上锁定的证明；
- 我向NEAR提交以太坊上的锁定证明；
- NEAR独立验证这个证明，通过后给我创建NEAR上流通的20枚DAI。

  之后，一旦我想把DAI转移回以太坊，只要简单逆转上述流程即可，很优雅
  
### 彩虹桥UI

> https://rainbowbridge.app/transfer

- 轻节点(LiteNode) — 它是一个区块链节点，不过仅仅存储区块头，因此极大的减少了存储占用。轻节点是以智能合约实现的，一个部署在以太坊网络上，存储NEAR区块头，另一个部署在NEAR网络上，存储以太坊区块头

- 中继(Relayer) — 轻节点是智能合约，它们不会自己运行和更新信息。中继是一些脚本，运行于传统服务器上，它们周期性地从一个区块链上读取块，传递给运行于另一个链上的轻节点。也就是说，中继保持轻节点的数据最新

  每次更新轻节点都是一笔交易，因此会消耗gas费。NEAR上的轻节点（含有以太坊区块）逐个以太坊块进行更新（因为NEAR上的gas费便宜），而以太坊上的轻节点（含有NEAR区块）更新频率是可配置的，受限于经济性（目前是12到16小时更新一次）

- 连接器(Connector) — 连接器是种智能合约，负责特定资产类型的跨链管理逻辑。与轻节点类似，它们成对出现。一个运行于以太坊，另一个运行于NEAR。例如，有一对“ETH连接器”，负责在链之间转移ETH资产。
还有一对“ERC-20连接器”， 负责转移ERC-20通证。其他人可以根据他们的需要，开发一个“NFT连接器”、“预测市场结果连接器”、“DAO投票结果连接器”等。只要有对应的连接器，任何资产或数据都可以通过彩虹桥移动!

### 把组件合起来

- 使用 彩虹桥UI, 我发起了从以太坊到NEAR的20个DAI的转移。
- 当我在MetaMask上确认了前两笔交易(approve 和 transfer)，彩虹桥与以太坊上的ERC-20 连接器通信 (因为DAI是一个ERC-20通证)，连接器将这20枚DAI锁定在它的保管库中。至此，这笔DAI就不再在以太坊上流通了。
- 基于我这笔交易区块的区块头数据，彩虹桥UI 计算出一个密码学“证明” 表明我确实锁定了20枚DAI。
- 接下来我要请求NEAR网络基于刚才以太坊上活动而创建一些DAI，就先要等待中继发送大概20个以太坊区块头给运行在NEAR上的轻节点。这是为了安全的考虑，跟你充值给虚拟币交易所时需要等一些确认一样。
- 之后，彩虹桥UI就允许我们执行流程中的第二步 — 让NEAR上的ERC-20 连接器为你在NEAR链上创建20枚新的DAI。
- 当向ERC-20 连接器发起这个请求时，我们要提供那个早先收到的密码学“证明”，以证明我们确实在以太坊上锁定了20枚DAI。
- NEAR上的ERC-20 连接器接下来查找NEAR上轻节点的以太坊区块头，然后创建一个独立计算出来的密码学证明。
- 如果我们提供的证明匹配上连接器算出的那个，它就知道20枚DAI已经被安全的被我锁定在以太坊上了！ 接下来就在NEAR上创建20个新的DAI，并转账给我的钱包。