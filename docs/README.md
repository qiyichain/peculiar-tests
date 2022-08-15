# 奇异链测试用例（文字版）


# 功能测试

所有系统合约采用的测试类型：**白箱测试**

## AddressList.sol 功能测试

黑白名单合约

函数测试：

- 开启验证：enableDevVerify 
- 关闭验证：disableDevVerify
- 修改amdin：commitChangeAdmin
- 确认修改admin：confirmChangeAdmin
- 增加user：addDeveloper
- 删除user：removeDeveloper
- 判断是否是白名单用户：isDeveloper
- 判断是否是黑名单用户： isBlackAddress
- 获取黑白名单：getBlacksFrom, getBlacksTo， 注意：数量不要太大，
- 增加黑名单用户：addBlacklist
- 删除黑名单:removeBlacklist
- 增加rules：addOrUpdateRule
- 删除rules：removeRule
- rules长度：rulesLen
- 获取rule：getRuleByKey

链功能测试：
- 开启B端白名单验证功能情况下：
  - *仅*白名单中的B端账户*可以*发送普通交易(转账)
  - *仅*白名单中的B端账户*可以*创建智能合约
- 关闭B端白名单验证功能情况下:
  - 所有地址都可以发送普通交易
  - 所有地址都可以创建合约

## Governance.sol 功能测试

链治理合约

- admin修改: commitChangeAdmin
- 确认admin修改：confirmChangeAdmin
- 提交proposal：commitProposal
- 获取proposal数量：getProposalsTotalCount
- 获取proposal：getProposalById
- 获取已经通过的proposal数量：getPassedProposalCount
- 通过索引获取proposal：getPassedProposalByIndex
- 通过proposal：finishProposal， 注意：需要验证节点配合操作


## Punish.sol 功能测试

和VotePool.sol有关联

注意：此合约的测试需要实际的验证节点的配合，比如，需要故意让节点长时间掉线，
以达到被惩罚要求，我们观察节点收益被扣除、被监禁的情况是否达到我们的要求

- 惩罚验证节点:punish ，注意：需要验证节点操作进行配合
- 减少错失的区块计数器：decreaseMissedBlocksCounter, 注意：需要验证节点操作进行配合
- 获取验证节点的数量:getPunishValidatorsLen
- 获取惩罚记录:getPunishRecord
- 清空惩罚记录：cleanPunishRecord


## UserAddressList.sol 功能测试

用户白名单，目前此合约仅存储用户地址，并没有在链上对黑白名单中的地址进行一个限制，只需要进行增删改查功能测试

- 开启验证：enableUserVerify
- 关闭验证：disableUserVerify
- 修改amdin：commitChangeAdmin
- 确认修改admin：confirmChangeAdmin
- 增加user：addUser
- 删除user：removeUser
- 判断是否是白名单用户：isUser
- 判断是否是黑名单用户：isBlackAddress
- 增加黑名单用户：addBlacklist
- 删除黑名单:removeBlacklist


## Validators.sol + VotePool.sol 功能测试（重点测试）

- 切换admin: changeAdmin
- 参数更新：updateParams
- 更新销毁比例：updateRates
- 更新组织账户：updateFoundation
- 提取组织收益：withdrawFoundationReward
- 添加验证节点：addValidator， 注意：此测试用例需要配合实际的节点加入，才能验证此函数的功能是否能生效
- 更新验证节点状态： updateValidatorState，注意：同上，需要配合实际的验证节点
- 更新节点集合：updateActiveValidatorSet，注意：同上
- 获取活跃验证节点：getActiveValidators
- 分发区块收益：distributeBlockReward，注意：要结合区块收益、验证节点数量，对比节点所获的收益数是否正确
- 提取收益：withdrawReward，注意：此函数不是真正提取收益到验证节点账户余额上，
- 修改验证节点的manager：changeManager
- 提交比例：submitPercentChange
- 确认比例：confirmPercentChange
- 增加margin：addMargin
- 切换节点状态：switchState
- 惩罚：punish，注意：此函数仅供punish合约调用，需要配合punish合约中的punish逻辑进行测试
- 删除节点收入：removeValidatorIncoming
- 节点退出：exit
- 提取margin：withdrawMargin
- 接受收益：receiveReward
- 提取收益：withdrawValidatorReward，注意：此函数会真正发送收益到验证节点账户余额上
- 获取验证节点的未提取的收益：getValidatorPendingReward
- 获取投票人的收益：getPendingReward 。TODO： ？？？ 此函数需要讨论是否需要删掉，我们支持用户进行投票？？？
- 充值：deposit，？？允许用户抵押？ TODO：此函数需要讨论是否需要删掉，我们支持用户进行投票？？？
- 退出投票：exitVote， ？？ 
- 提取收益：withdraw


# 性能测试

## 普通转账交易测试
- 合约数量：1、5、10、20
- 账户数量：10、100、1000
- 交易数量: 100、1000、10000、100000

## ERC721合约调用交易测试

- mint、transfer调用的TPS测试
- 合约数量：1、5、10、20
- 账户数量：10、100、1000
- 交易数量: 100、1000、10000、100000

## ERC1155合约调用交易测试

- batchMint、batchTransfer调用的TPS测试
- 合约数量：1、5、10、20
- 账户数量：10、100、1000
- 交易数量: 100、1000、10000、100000

