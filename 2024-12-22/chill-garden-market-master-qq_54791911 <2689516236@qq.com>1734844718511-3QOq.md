根据提供的git diff记录，以下是对代码变更的评审：

### 1. 配置文件变更
- **application-dev.yml**:
  - **变更描述**: 数据库连接URL从`xfg_frame_archetype`更改为`big_market`。
  - **评审**: 
    - 确认`big_market`数据库存在并且有适当的权限和表结构。
    - 建议不要在配置文件中直接使用默认密码，应使用环境变量或加密存储。

### 2. MyBatis Mapper文件
- **新增文件**:
  - `award_mapper.xml`: 增加了查询奖品列表的Mapper。
  - `strategy_award_mapper.xml`: 增加了查询抽奖策略奖品配置的Mapper。
  - `strategy_mapper.xml`: 增加了查询抽奖策略的Mapper。
  - `strategy_rule_mapper.xml`: 增加了查询策略规则的Mapper。
  - **评审**:
    - 确保所有的Mapper文件与数据库表结构一致。
    - 检查`limit 10`是否是正确限制返回记录数的方式，如果是演示或测试，可能需要调整。

- **删除文件**:
  - `frame_case_mapper.xml`: 删除了框架案例的Mapper。
  - **评审**:
    - 确认`frame_case`相关的功能不再需要，或者已经迁移到其他Mapper。
    - 如果是删除废弃的代码，确保没有遗留引用。

### 3. 测试文件
- **新增文件**:
  - `AwardRepositoryTest.java`: 测试奖品仓库。
  - **评审**:
    - 确保测试覆盖了所有的业务场景和异常情况。
    - 检查测试用例是否使用了适当的测试数据。

### 4. 代码结构变更
- **包重命名**:
  - 将`xxx`重命名为`Award`。
  - **评审**:
    - 确认重命名后代码的引用都进行了相应的更新。
    - 重命名后代码更直观地反映了其功能。

- **新增文件**:
  - `AwardEntity.java`: 定义奖品实体类。
  - `IAwardRepository.java`: 定义奖品仓库接口。
  - **评审**:
    - 实体类与数据库表结构一致。
    - 仓库接口定义清晰，便于后续实现。

- **删除文件**:
  - `xxx/service/package-info.java`: 删除了废弃的包信息。
  - **评审**:
    - 确认该包信息不再需要，或者已经迁移到其他位置。

### 5. 其他变更
- **Mapper类新增**:
  - `IAwardDao.java`, `IStrategyAwardDao.java`, `IStrategyDao.java`, `IStrategyRuleDao.java`: 新增了DAO接口。
  - **评审**:
    - 确保接口方法定义符合业务需求。
    - 接口应该定义清晰，便于实现。

- **PO类新增**:
  - `Award.java`, `Strategy.java`, `StrategyAward.java`, `StrategyRule.java`: 新增了持久化对象类。
  - **评审**:
    - PO类应该与数据库表结构一致。
    - 使用Lombok注解可以简化代码。

总体来说，这次代码变更似乎是为了增加新的功能（如奖品管理、抽奖策略等）。所有的变更都经过了适当的组织和管理，但需要注意确保所有的数据库变更、接口变更和代码引用都得到了适当的处理。