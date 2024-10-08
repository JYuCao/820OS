---
title: 处理机调度与死锁
markmap:
  colorFreezeLevel: 4
---

# 处理机调度与死锁
## 处理机调度层次
- 高级调度：调度对象为外存中的作业。主要用于多道批处理系统。
- 低级调度：调度对象为（内核级）进程。是必需的调度。
- 中级调度：存储器管理中的对换功能。

## 处理机调度算法
### 设计目标
#### 处理机调度算法的共同目标
- 提高系统的资源利用率：$CPU利用率=\frac{CPU有效工作时间}{CPU有效工作时间+CPU空闲等待时间}$
- 公平性：使每个进程都能获得合理的CPU时间分配，不会发生饥饿现象。
- 平衡性：尽可能保持系统中各个设备的忙碌。
- 策略强制执行：如有需要，即使造成某些工作的延迟也要强制执行某些策略。

#### 批处理系统的目标
- 平均周转时间短
    - 周转时间、平均周转时间和平均带权周转时间
- 系统吞吐量高
    - 吞吐量：单位时间内系统完成的作业数
- 处理机利用率高

#### 分时系统的目标
- 响应时间快
- 均衡性：系统响应时间的快慢应与服务复杂性相适应

#### 实时系统的目标
- 截止时间的保证
- 可预测性

### 作业与作业调度（批处理系统）
- 作业(Job)：包含程序、数据和作业说明书
- 作业步(Job Step)
- 作业控制块(JCB)
- 作业运行的三个阶段和三种状态
    - 后备状态、运行状态、完成状态
    - 收容阶段、运行阶段、完成阶段

### 作业调度的主要任务
- 接纳多少个作业：多道程序度
- 接纳哪些作业：调度算法

### 调度算法
#### 先来先服务（FCFS）
- 等待时间最长的作业优先

#### 短作业优先（SJF）
- 以作业长短来计算优先级
- 缺点
    - 必须预知作业的运行时间
    - 长作业周转时间增长，甚至会出现饥饿现象
    - 采用SJF算法时，人-机无法实现交互
    - 未考虑作业的紧迫程度

#### 优先级调度算法（PSA）
- 根据优先级进行调度

#### 高响应比调度算法（HRRN）
- 响应比$R_p=\frac{等待时间+要求服务时间}{要求服务时间}=\frac{响应时间}{要求服务时间}$ 

## 进程调度
### 进程调度的任务
- 保存处理机的现场信息
- 按某种算法选取进程
- 把处理器分配给进程

### 进程调度的机制
- 排队器、分派器、上下文切换器

### 进程调度方式
- 非抢占方式
- 抢占方式：优先权原则、短进程优先原则、时间片原则

### 调度算法
#### 轮转(Round Robin, RR)调度算法
- 基本原理
- 进程切换时机
    - 进程运行结束
    - 时间片用完
- 时间片大小的确定
    - 太长：退化为FCFS
    - 太短：上下文切换开销大
    - 合适：略大于一次典型的交互时间

#### 优先级调度算法
- 调度算法的类型：非抢占式、抢占式
- 优先级的类型：静态优先级（根据进程类型、资源需求和用户要求确定）、动态优先级

#### 多队列调度算法

### 多级反馈队列调度算法
#### 调度机制
1. 设置多个就绪队列，每个队列有不同的优先级，优先级越高时间片越短
2. 每个队列使用FCFS算法，每次轮转完一个时间片，进程放入低一级优先
级队列，最后一级采用RR算法
3. 按队列优先级调度，抢占式调度高优先级队列

#### 算法性能
- 规定第一个队列的时间片略大于多数人机交互所需的处理时间，便能较好
满足各种类型用户的需要

### 基于公平原则的调度算法
- 保证调度算法
- 公平分享调度算法（对用户）

## 实时调度
### 实现实时调度的基本条件
- 提供必要的信息：就绪时间、开始截止时间和完成截止时间、处理时间、资源要求、优先级
- 系统处理能力强：限制条件:$\sum_{i=1}^m\frac{C_i}{P_i}\leq 1(N)$
- 采用抢占式调度机制
- 具有快速切换机制：对中断有快速的响应能力、快速的任务分配能力

### 实时调度算法的分类
#### 非抢占式调度算法
- 非抢占式轮转调度算法：用于不太严格的实时系统
- 非抢占式优先调度算法：用于有一定要求的实时系统

#### 抢占式调度算法
- 基于时钟中断的抢占式优先级调度算法：可用于大多数的实时系统
- 立即抢占的优先级调度算法：非常快

### 最早截止时间优先EDF算法
- 非抢占式调度方式用于非周期实时任务
- 抢占式调度方式用于周期实时任务

### 最低松弛度优先LLF(Least Laxity First)算法
- 松弛度 = 截止时间距现在的时间 - 运行所需的时间

### 优先级倒置
- 优先级倒置的形成：临界资源
- 解决办法：动态优先级继承

## 死锁
### 资源问题
#### 可重用性资源
- 每一个单元只能分配个一个进程使用，不能共享
- 使用资源时需要按照顺序：请求资源、使用资源、释放资源
- 资源单元数目固定，进程运行期间不能创建和删除

#### 可消耗性资源
- 资源单元数目可变
- 可在进程运行过程中创造并放入缓冲区
- 进程运行过程可申请消耗，不再将其返回资源类中

#### 可抢占性资源

#### 不可抢占性资源

### 死锁种类
- 竞争不可抢占资源引起死锁
- 竞争可消耗资源引起死锁
- 进程推进顺序不当引起死锁

### 定义(Deadlock)
- 如果一组进程中的每一个进程都在等待仅由该组进程中的其它进程才能引发的事件，那么该组进程是死锁的

### 产生死锁的必要条件
- 互斥条件：一段时间内，某资源只能被一个进程占用
- 请求和保持条件：进程保持了至少一个资源，并提出新的资源请求
- 不可抢占条件：进程已获得的资源在未使用完之前不能被抢占
- 循环等待条件：发生死锁时，必然存在一个进程-资源的循环链

### 预防死锁
#### 破坏请求与保持条件
- 第一种协议
    - 所有进程开始运行之前，必须一次性申请
    其在整个运行过程中所需的全部资源
    - 缺点：资源被严重浪费；进程常发生饥饿现象
- 第二种协议
    - 允许一个进程只获得初期需要的资源后开始运行

#### 破坏不可抢占条件
- 一个已经保持了某些不可被抢占资源的进程，提出新的资源请求而不能得
到满足，它必须释放已经保持的资源

#### 破坏循环等待条件
- 对系统资源进行线性编号，要求只能按序号递增顺序请求资源
- 缺点：限制了新类型设备的增加；造成对资源的浪费；限制用户简单、自主的编程

### 避免死锁
#### 系统安全状态
- 系统按某种进程推进顺序为每个进程分配其所需资源，直至满足每个进程对资源的最大需求

#### 银行家算法
##### 数据结构
- 可利用资源向量Available
- 最大需求矩阵Max
- 分配矩阵allocation
- 需求矩阵Need

##### 银行家算法与安全性算法

### 死锁的检测
- 资源分配图
- 死锁定理：当且仅当S状态的资源分配图是不可完全简化的
- 死锁检测中的数据结构

### 死锁的解除
#### 终止进程
- 终止所有死锁进程
- 逐个终止进程

#### 付出代价最小的死锁解除算法
