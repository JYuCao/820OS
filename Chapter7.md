---
title: 文件管理
markmap:
  colorFreezeLevel: 3
---
# 文件管理
## 文件系统
### 几个概念
- 数据项：基本数据项和组合数据项
- 记录：关键字(Key)
- 文件：文件类型、长度、物理位置、建立时间

### 文件名和类型
- 文件名和扩展名
- 文件类型
    - 用途：系统、用户、库文件
    - 数据形式：源文件、目标文件、可执行文件
    - 存取控制：只执行、只读、读写
    - 组织形式和处理方式：普通、目录、特殊文件

### 文件系统的层次结构
- 对象和属性（最底层）：文件、目录、磁盘存储空间
- 对对象操纵和管理的软件集合
    - 功能：对文件存储空间的管理；对文件目录的管理；将文件的逻辑
    地址转换成物理地址；对文件读写的管理；对文件的共享与保护等
    - 分层：I/O控制层、基本文件系统层、基本I/O管理程序、逻辑文件系统
- 文件系统的接口：命令接口、程序接口

### 文件操作
- 最基本的文件操作：创建、删除、读、写、设置文件读写位置
- 打开与关闭
- 其他文件操作：对文件属性的操作、有关目录的操作等

## 文件的逻辑结构
### 类型
#### 按文件是否有结构分类
- 有结构文件：定长记录、变长记录
- 无结构文件（流式文件）

#### 按文件的组织方式分类
- 顺序文件、索引文件、索引顺序文件

### 顺序文件
- 排列方式：串结构、顺序结构
- 优点：便于批量存取和顺序存取设备
- 缺点：查找和修改单个记录耗时长，增删记录开销大

### 记录寻址
- 隐式寻址方式：Wptr+L
- 显式寻址方式：通过记录位置和通过关键字

### 索引文件
