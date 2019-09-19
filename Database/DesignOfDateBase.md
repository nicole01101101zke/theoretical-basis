# 数据库设计

## 数据依赖

- 关系数据库内数据之间存在一定的数据依赖关系

### 函数依赖FD

- 一个属性的值可以唯一的决定其它属性的值

### 多值依赖MVD

- 一个属性的值决定其它属性的一组值
- 实际生活存在但很少

### 连接依赖JD

- 关系属性之间能够无损连接
  - 无损连接：连接后的元组数一个不多，一个不少
- 实际生活存在但很少

## 关系模式的规范化

### 关系模式的范式理论

#### 1 NF 一范式

- 不支持表中套表
- 关系中的每一个元组必须是原子【即不可再分】

#### 2 NF 二范式

- 数据库设计时，设计出来的表满足一范式，并且该表内不存在属性对主键的部分函数依赖。

##### 例子：

- 若属性由（学号、姓名、班级、课程号、成绩）五个属性组成，其中（学号，课程号）共同组成主键。
  - 此时不满足二范式。
  - 其中的姓名和班级，只需要依赖主键中的学号就可以得到。

##### 不满足2范式容易出现的问题：

- 插入异常
  - 上例中，不能插入一个还未选课的学生的信息
- 删除异常
  - 上例中，如果一个学生申请休学，把选过的课退了，那么他的信息也会被删除
- 更新异常
  - 更新中难以保持数据的一致性，上例的设计有大量的数据冗余

##### 解决方法

- 设计时，一视一地。
  - 一张表只管一件事情

#### 3 NF 三范式

- 在满足二范式的前提下，不存在属性对主键的传递依赖。

##### 例子

- 若属性由（职工编号、工资级别、工资）三个属性组成，其中（职工编号）为主键。

##### 分析

- 工资取决于工资级别，取决于职工编号

##### 上例不满足3范式的问题

- 插入异常：当一个人的工资级别还没定的时候，他对应的工资也没有
- 删除异常：若只是删除一个员工的工资信息时，会把对应的工资级别信息也删除了
- 更新异常：数据内有大量的冗余

##### 解决方法

- 设计时，一视一地。
  - 一张表只管一件事情

#### 4 NF 四范式

- 在满足三范式的前提下，消除多值依赖。

#### 5 NF 五范式

- 在满足四范式的前提下，消除连接依赖。

## 数据库设计方法

### 面向过程的方法

- 根据单位日常处理的流程，以过程为中心。
  - 好处
    - 在设计初期，能比较快的实现
  - 缺点
    - 没分析数据之间的关系，数据由冗余和矛盾，当流程进行改动时，会有很多问题

### 面向对象的方法

- 以数据为中心的方法
- 分析数据之间的关系，设计一些符合3NF的模式

## 数据库设计流程

- 需求分析，与用户交流确定需求
- 概念设计，分析数据之间的关系、实体及实体间的逻辑
- 逻辑设计，看采用的数据库系统，生成基表
- 物理设计，考虑数据在内存上到底如何存储



## 各阶段主要工作

### 需求分析阶段

- 数据字典
  - 把所有的基本数据元素都找出来
    - 解决问题：
      - 名字冲突：同名异意
      - 概念冲突
      - 域冲突
      - 编码问题
        - 压缩信息
        - 基本信息
        - 实体识别

### 概念设计阶段

- 用ER图抽象出实体
- 哪些数据项抽象成实体
- 实体间的联系
- 相关ER图工具

### 逻辑设计阶段

- 把ER图表达的数据模型进行建表
- 表和属性的命名规则
- 逆规范化
- 定义视图
- 考虑遗留系统的表的设计

### 物理设计阶段

- 根据DBMS特点对每个表的存储和索引情况进行权衡
- 分区设计

## 总结

- 仅仅在结构上满足3范式是不够的
- 一事一地包括每项信息的唯一，要提取出问题的本质，识别本质上同一概念的信息项
- 对于表达类似信息、能合并尽量合并
- 考虑到效率、用途等因素、该分开的要分开
- 结合DBMS内部实现技术，合理设计索引和文件结构，为查询优化准备号存取路径
- 在结构规范化、减少数据冗余和提高数据库访问性能之间仔细权衡，适当折中

## 案例分析一

- 一些表内数据相似，概念不清
  - 在做需求分析时没有以数据为中心，没有找到基本的数据元素
  - 数据应该来源唯一，责任唯一

## 案例分析二


