# 大纲

## 一、简介

### 1.1 RoboRoute 简介

RoboRoute 是上海仙知机器人科技有限公司（Seer Robotics，以下简称 仙知）开发的多机器人调度系统。  仙知整合 RoboRoute 系统、Roboshop Pro 软件，以及 SRC2000 系列控制器，可针对多种类、多数量移动机器人复杂操作与协同配合的场景，提供快速、专业的整厂解决方案，以此提升工厂的整体作业效率。

![img](https://github.com/qunge12345/roboroute_users_guide/blob/master/pictures/01/clip_image001.png?raw=true)

 

### 1.2 RoboRoute 主要功能

RoboRoute 系统的核心功能如下：

- **机器人调度**

  - 任务分配

      将业务订单分配给最合适的机器人执行。

  - 路线规划

      为执行业务的机器人规划合理的移动路线。

  - 交通管制

      预防机器人之间发生碰撞。

      解决机器人在运行中的路线冲突。

- **场景编辑**

  配合 Roboshop Pro 软件，编辑机器人的移动路线及节点。

  配置工作站、充电桩信息。

  配置机器人可操作的业务类型、动作类型等。

- **状态监控**

  在系统运行期间，实时监控整场机器人的在线状态、所处位置、行进路线、业务进度等。

  也可聚焦具体的机器人，对其进行持续跟踪。

- **机器人管理**

  管理机器人列表，控制机器人在 RoboRoute 系统中上下线。

  指定机器人前往节点或工作站。

  撤销机器人正在执行的业务。

  在不影响生产运输前提下，自动引导低电量机器人回坞充电。

- **业务管理**

  支持可视化地创建业务订单。

  通过执行状态，筛选业务订单列表，并获取订单的详细信息。

  批量撤销业务订单。

- **业务统计**

  统计机器人的累计运行时间、停靠和充电时间，以及整体利用率。

  统计工作站的累计访问时间。

  统计业务订单的分配和执行时间，以及完成情况。

- **交互协议**

  提供简洁的 HTTP 访问协议。通过协议可以：

  创建、查询及撤销业务订单。

  查询机器人的状态，或指定机器人在 RoboRoute 系统中上下线。

## 二、部署环境

### 2.1 RoboRoute 服务器

RoboRoute 的硬件载体选用 联想 ThinkStation P318 工作站，其主要优点有：

- 工作站级主机，满足工厂 7 × 24 小时的不间断生产需求。

- 品牌型号入选节能环保清单，即《[环境标志产品政府采购清单](http://www.ccgp.gov.cn/search/hbqdchaxun.htm)》和《[节能产品政府采购清单](http://www.ccgp.gov.cn/search/jnqdchaxun.htm)》。

RoboRoute 服务器的主要配置：

- CPU：英特尔酷睿Core i7-7700

- RAM：16G DDR4 2133 NECC

- 硬盘：1TB

- 操作系统：Ubuntu 16.04

**请注意：**

**为保证用户权益及系统稳定性，RoboRoute 软件仅在仙知指定的 RoboRoute 服务器上运行。**
 **请勿拆下 RoboRoute 服务器上的授权锁。**

### 2.2 机器人及 RoboShop Pro 软件

加入 RoboRoute 调度序列的机器人，必须满足以下条件：

- 使用仙知 SRC1100 或者 SRC2000 系列机器人主控器。

- 使用含通信功能的电池，能够向 RoboRoute 反馈电量信息。

- 机器人具备自主充电能力。

### 2.3 WIFI 环境

现场无线推荐使用MOXA AWK-3131A无线AP，网络延迟控制在200ms之内，网络环境测试请参考：

<https://www.seer-robotics.com/index.do?detail&id=2c93b6e764c9d7430164cf4c3f6d006e> 

## 三、系统安装

### 3.1 硬件安装

RoboRoute 服务器的主机和显示器均为标准市电电源（AC 220V-50Hz），总峰值用电功率 ≤ 1KW，请合理安排电源，保证可靠接地。

RoboRoute 服务器的主要配件包括：

| 配件清单                               |
| -------------------------------------- |
| Thinkstation P318 主机（含授权锁） × 1 |
| 液晶显示器 × 1                         |
| 键鼠套装 × 1                           |

RoboRoute 服务器应部署在室温环境，10°C~30°C 之间。

RoboRoute 服务器应部署至可以目视、或者视频监控到机器人运行现场的地点。并且在该地点，要求能够使用双绞线，将 RoboRoute 服务器连接到机器人所在的局域网络设备中。

### 3.2 密码和账户

RoboRoute 服务器的初始账户为：RoboRoute，初始密码为：roboroute

### 3.3 网络配置

请使用超五类双绞线，将 RoboRoute 服务器主机连接至现场局域网络。

请为 RoboRoute 服务器配置静态 IP，并且注意，该局域网络内，不能有其他设备和服务器存在 IP 冲突。

请注意现场网络的覆盖范围，必须包含机器人会抵达的所有角落。

### 3.4 更新

软件更新以官网发布版，或者仙知的通知为准。

## 四、场景元素介绍

### 4.1 节点

节点（Point）是用于逻辑映射场景路线中关键位置的元素。在 RoboRoute 操作模式下，机器人总是从场景中的一个节点到另一节点运行。节点分为：地标点和停靠点，其属性如下所述：

![img](https://github.com/qunge12345/roboroute_users_guide/blob/master/pictures/01/clip_image002.png?raw=true)

| 属性          | 描述                       | 属性          | 描述                   |
| ------------- | -------------------------- | ------------- | ---------------------- |
| 名称          | 节点的全局唯一 ID          | 类型          | 地标点，或者停靠点     |
| X-轴坐标      | 场景坐标系中 X 轴坐标      | 元属性        | 用户自定义的键值型属性 |
| Y-轴坐标      | 场景坐标系中 Y 轴坐标      | 节点 X 轴坐标 | 视图坐标系中 X 轴坐标  |
| 角度          | 机器人到点角度（暂未启用） | 节点 Y 轴坐标 | 视图坐标系中 Y 轴坐标  |
| 标签 X 轴坐标 | 节点ID X 轴坐标            | 标签 Y 轴坐标 | 节点ID Y 轴坐标        |
| 节点标签角度  | 节点ID 角度                |               |                        |

#### 4.1.1 地标点

在 RoboRoute 中，地标点（Land Mark）是机器人处理业务订单时可能短暂停留的节点，机器人在到达该节点时，执行工作站的操作；或者机器人在行进路线中经过的一系列节点。地标点标识为灰色圆点。

![img](https://github.com/qunge12345/roboroute_users_guide/blob/master/pictures/01/clip_image002.png?raw=true)

 

#### 4.1.2 停靠点

停靠点（Park Point）是供业务空闲的机器人停靠和待机的节点。机器人执行完毕当前的业务后，若没有新的业务被分配，会前往附近没有被占用的停靠点，等待新的业务订单。如果机器人的电量低于报警阈值，且此时不存在空闲的充电站，机器人也会前往停靠点，但不再接受新的业务订单。停靠点标识为蓝色圆点。

![img](https://github.com/qunge12345/roboroute_users_guide/blob/master/pictures/01/clip_image003.png?raw=true)

 

### 4.2 工作站

工作站（Location）是机器人需要进行业务操作的站点，不可以单独存在，必须使用工作站连接将其和节点关联起来。工作站限定了机器人在该处的工作内容。其属性包含：

![img](https://github.com/qunge12345/roboroute_users_guide/blob/master/pictures/01/clip_image004.png?raw=true)

 

| 属性     | 描述                     | 属性            | 描述                            |
| -------- | ------------------------ | --------------- | ------------------------------- |
| 名称     | 工作站的全局唯一ID       | 标志            | 选择工作站图片区分工作站样式    |
| X-轴坐标 | 场景坐标系中的 X 轴坐标  | 工作站 X 轴坐标 | 视图坐标系中 X 轴坐标           |
| Y-轴坐标 | 场景坐标系中的 Y 轴坐标  | 工作站 Y 轴坐标 | 视图坐标系中 Y 轴坐标           |
| 类型     | 该工作站属于的工作站类型 | 标签 X 轴偏移量 | 视图窗口中工作站ID   X 轴偏移量 |
| 方向角   | 暂不使用                 | 标签 Y 轴偏移量 | 视图窗口中工作站ID   Y 轴偏移量 |
| 元属性   | 用户自定义的键值型属性   |                 |                                 |

 

### 4.3 工作站连接

工作站连接（Link）是用于将工作站和节点进行关联的工具，其属性包含：

![img](https://github.com/qunge12345/roboroute_users_guide/blob/master/pictures/01/clip_image005.png?raw=true)

 

| 属性 | 描述                       | 属性     | 描述                 |
| ---- | -------------------------- | -------- | -------------------- |
| 名称 | 根据起始和终点元素自动生成 | 起始元素 | 地标点或工作站的名称 |
| 动作 | 工作站的操作类型限定       | 终点     | 地标点或工作站的名称 |

如果此处的“动作”内容为空，则在该处工作站，机器人可以执行工作站类型中定义的所有操作。

如果此处的“动作”内容非空，则在该处工作站，机器人只能执行工作站连接的“动作”栏所限定的操作。

 

### 4.4 工作站类型

工作站类型（Location Type）是一个工作站唯一且必需的元素，其主要定义了一组机器人允许执行的操作。其属性包含：

![img](https://github.com/qunge12345/roboroute_users_guide/blob/master/pictures/01/clip_image006.png?raw=true)

 

| 属性 | 描述                     | 属性   | 描述                     |
| ---- | ------------------------ | ------ | ------------------------ |
| 名称 | 该工作站类型的全局唯一ID | 动作   | 一组机器人允许执行的操作 |
| 标志 | 用于区分不同工作站样式   | 元属性 | 用户自定义的键值型属性   |

 

### 4.5 路径

路径（Path）是两个节点之间的有向连接线。其主要属性包含: 

![img](https://github.com/qunge12345/roboroute_users_guide/blob/master/pictures/01/clip_image007.png?raw=true)

 

| 属性         | 描述                         | 属性         | 描述                     |
| ------------ | ---------------------------- | ------------ | ------------------------ |
| 名称         | 路径的全局唯一ID             | 路径曲线类型 | 直线，或者贝塞尔曲线     |
| 长度         | 路径在场景中的长度           | 曲线控制点   | 只有贝塞尔曲线存在控制点 |
| 路径成本     | 路径在路线规划中的成本系数   | 起始元素     | 路径起点                 |
| 最大正向速度 | 路径上允许的最大正向行走速度 | 终点元素     | 路径终点                 |
| 最大反向速度 | 路径上允许的最大反向行走速度 | 锁定路径     | 锁定路径                 |
| 元属性       | 用户自定义的键值型属性       |              |                          |

 若一条路径因故无法通行，可以在系统运行时勾选“锁定路径”，令机器人规划路线时避开此路径。

#### 4.5.1 直线

由于 RoboRoute Viewer 中的场景视图只表示节点间的有向拓扑关系，并非实际的机器人行进路线，因此大多数情况下，使用直线连接节点即可。

#### 4.5.2 2-Bezier & 3-Bezier

贝塞尔曲线，又称贝兹曲线或贝济埃曲线，是应用于二维图形应用程序的数学曲线。一般的矢量图形软件通过它来精确画出曲线，贝塞尔曲线由线段与控制点组成，控制点是可拖动的点，线段像可伸缩的皮筋，编辑模式下路径工具中的2-Bezier & 3-Bezier就是来画这种矢量曲线的。 

### 4.6 机器人

机器人（Robot）是场景中业务订单的执行者，机器人的全局唯一ID要在三处保证统一：机器人铭牌上的ID标识、Roboshop 中定义的名称、RoboRoute 场景中定义的名称。机器人具有以下属性：

![img](https://github.com/qunge12345/roboroute_users_guide/blob/master/pictures/01/clip_image008.png?raw=true)

 

其中，机器人状态如下所述：

| 机器人状态  | 含义                                                         |
| ----------- | ------------------------------------------------------------ |
| UNKNOWN     | 机器人不存在于场景之中                                       |
| UNAVAILABLE | 机器人未释放控制权给 RoboRoute，或机器人连接调度服务器超时等 |
| ERROR       | 机器人故障，或执行任务时出现异常                             |
| IDLE        | 机器人已连接到 RoboRoute，并处于空闲状态                     |
| EXECUTING   | 机器人正在执行业务                                           |
| CHARGING    | 机器人正在充电                                               |

机器人在线状态如下所述：

| 机器人在线状态  | 含义                                                         |
| --------------- | ------------------------------------------------------------ |
| TO_BE_IGNORED   | 机器人处于离线状态                                           |
| TO_BE_NOTICED   | RoboRoute 标识出机器人的位置，但在任何处理中均不考虑该机器人的存在 |
| TO_BE_RESPECTED | RoboRoute 在处理中考虑该机器人的存在，但是不会对其分配任何业务订单和命令 |
| TO_BE_UTILIZED  | 机器人处于完全在线状态                                       |

机器人业务执行状态如下所述：

| 机器人业务执行状态 | 含义                             |
| ------------------ | -------------------------------- |
| UNAVAILABLE        | 无法执行任何业务订单和任务       |
| IDLE               | 空闲状态                         |
| AWAITING_ORDER     | 机器人在等待业务订单中新的子任务 |
| PROCESSING_ORDER   | 机器人正在执行业务订单中的任务   |
机器人的电量状态如下所述：

| 电量状态级别 | 含义                             |
| ------------ | -------------------------------- |
| GOOD         | 电量高于充足阈值                 |
| DEGRADED     | 电量低于充足阈值，但高于报警阈值 |
| CRITICAL     | 电量低于报警阈值                 |

机器人的属性如下所述：

| 属性             | 描述                       | 属性             | 描述                         |
| ---------------- | -------------------------- | ---------------- | ---------------------------- |
| 名称             | 机器人的全局唯一ID         | 机器人长度       | 机器人车体长度（暂未使用）   |
| 路线颜色         | 机器人的路径颜色           | 低电量报警阈值   | 低于该值机器人不再接受业务   |
| 电量充足阈值     | 电量高于该值时认为电量充足 | 最大正向速度     | 机器人运行时最大的前进速度   |
| 最大反向速度     | 机器人运行时最大的反向速度 | 剩余电量         | 机器人当前电量               |
| 电量状态         | 当前电量状态级别           | 负载状态         | 机器人是否载重（暂未使用）   |
| 机器人状态       | 机器人状态                 | 在线状态         | 机器人的在线状态             |
| 业务执行状态     | 机器人的业务执行状态       | 当前节点         | 机器人当前所在的节点         |
| 下一节点         | 机器人即将前往的节点       | 精确节点         | 机器人的精确位置（暂未启用） |
| 机器人方向       | 机器人到点方向             | 元属性           | 用户自定义的键值型属性       |
| 当前业务订单     | 当前执行的业务订单名称     | 当前业务订单序列 | 当前执行的业务订单序列名称   |
| 可执行的业务类型 | 机器人能够执行的业务类型   | 自主充电类型     | 机器人自主充电操作类型       |

其中，

- 当机器人的“电量状态”为 DEGRADED 时，机器人将在业务空闲时回充电桩充电，但如果被分配了新的业务，充电行为将会被撤销。

  当机器人“电量状态”为 CRITICAL 时，机器人将在业务空闲时回充电桩充电。即使存在新的业务，机器人也将在充电至 DEGRADED 后，才接受并执行业务。

- 如果业务订单中指定了业务类型（category），那么机器人必须在“可执行的业务类型”中包含订单中的业务类型，才有资格接受该业务订单。

- 当机器人需要进行自主充电时，场景中必须至少存在一个充电工作站，其 operation 中包含其“自主充电类型”。
### 4.7 互斥区

互斥区（Block）是一个场景元素的集合，如果机器人占用了互斥区中的任何一个元素，将被视为占用了互斥区的全部元素。即机器人在互斥区中是互斥的。在布局中互斥区栏如下图所示。

![img](https://github.com/qunge12345/roboroute_users_guide/blob/master/pictures/01/clip_image022.png?raw=true)

 互斥区的属性如下所述：

| 属性       | 描述                     |
| ---------- | ------------------------ |
| 名称       | 互斥区的全局唯一ID       |
| 互斥区颜色 | 互斥区在场景中表现的颜色 |
| 互斥区元素 | 互斥区包含的元素         |
| 元属性     | 用户自定义的键值型属性   |



### 4.8 元素组

在 Viewer 编辑模式下，点击工具栏"新建元素组"按钮，出现如下对话框。选择需要添加到元素组（Group）中的场景元素，然后单击添加选中元素，可将其添加到元素组中。

![img](https://github.com/qunge12345/roboroute_users_guide/blob/master/pictures/01/clip_image010.png?raw=true)

 

元素组信息栏会显示您所添加的元素，如下图：

![img](https://github.com/qunge12345/roboroute_users_guide/blob/master/pictures/01/clip_image011.png?raw=true)

 使用元素组，可以方便在大型场景中选取关键元素。



## 五、入门

### 5.1 启动 RoboRoute

双击桌面上的 StartAll 文件，会将 redis、Kernel、Viewer 全部自启。

### 5.2关闭 RoboRoute

点击Kernel右上角的关闭按钮或者运行shutdownKernel.bat文件可以关闭Kernel；点击Viewer右上角的关闭按钮可以关闭Viewer。

### 5.3 Kernel 功能及布局

#### 5.3.1 Kernel 模式

Kernel 是进行机器人管理以及核心功能实现的运算软件，分为编辑模式和操作模式。编辑模式可以新建一个空白场景，该场景中不存在任何场景元素，可以在Viewer中使用导入 Kernel 当前场景来编辑该空白场景；操作模式是 Kernel 工作时的运行模式。Kernel 的模式会根据 Viewer 的模式自动切换，不需要手动设置。

#### 5.3.2 菜单栏

Kernel 菜单栏包含两个主要功能：Kernel 和帮助；Kernel 中包含模式切换操作、新建场景操作以及退出关闭操作；帮助中是关于软件的版权信息。

![img](https://github.com/qunge12345/roboroute_users_guide/blob/master/pictures/01/clip_image012.png?raw=true)

 

#### 5.3.3 关键日志页面

Kernel 关键日志负责记录 Kernel 模式切换或者地图同步的状态信息，从中可以获取当前 Kernel 处在哪一种模式以及使用的场景。

![img](https://github.com/qunge12345/roboroute_users_guide/blob/master/pictures/01/clip_image013.png?raw=true)

 

#### 5.3.4 机器人管理页面

机器人管理页面中包含 Kernel 当前场景中所有的机器人信息，机器人栏表示场景中全部的机器人，在是否可用栏选择是否启用该机器人，状态栏实时显示机器人的状态，可以在 State 栏中设置；适配器栏包含当前 Kernel 中可用的适配器，位置栏显示机器人当前所在场景中的位置，可以在机器人信息配置项中的 Pos 中设置；Energy 栏用于设置机器人当前的电量。

![img](https://github.com/qunge12345/roboroute_users_guide/blob/master/pictures/01/clip_image014.png?raw=true)

 

### 5.4 Viewer 功能及布局

![img](https://github.com/qunge12345/roboroute_users_guide/blob/master/pictures/01/clip_image015.png?raw=true)

 Viewer界面包含所有的人机交互功能，在编辑模式下，可以使用工具栏进行场景元素的编辑，包括但不限于元素的添加、名称动作编辑、路线编辑、互斥区编辑等功能；在操作模式下，可以进行机器人的启动与暂停，书写订单，订单撤回等操作，详细使用请见各功能模块详解。

#### 5.4.1 Viewer 模式

Viewer 是用于可视化操作的软件，分为编辑模式和操作模式：

编辑模式：允许在场景视图窗口中进行场景的编辑操作，例如机器人的添加、工作站类型的编辑、路径的微调等一系列可视化操作；

操作模式：在编辑模式将场景保存后，选择将场景同步到 Kernel ，然后选择菜单栏—>文件—>模式功能将模式切换到操作模式，此时界面中会增加显示机器人的信息，以及允许的对机器人的一系列操作；

#### 5.4.2 菜单栏

Viewer 菜单栏包括文件、编辑、动作、视图、帮助等功能：

文件操作：

![img](https://github.com/qunge12345/roboroute_users_guide/blob/master/pictures/01/clip_image016.png?raw=true)

 

| 功能                | 描述                                   |
| ------------------- | -------------------------------------- |
| 新建场景            | 新建一个空白场景，可以任意添加场景元素 |
| 导入场景            | 从文件夹中导入XML格式场景              |
| 保存场景            | 将编辑好的场景保存至文件夹             |
| 场景另存为          | 将编辑好的场景重命名保存至文件夹       |
| 导入 Kernel 场景    | 导入当前 Kernel 中的场景               |
| 将场景同步至 Kernel | 将当前视图中的场景同步到   Kernel 中   |
| 派遣所有机器人      | 一键派遣场景中所有的机器人             |
| 模式                | 选择编辑模式或者操作模式               |
| 显示场景信息        | 显示场景中各个场景元素的数量           |

编辑操作：

![img](https://github.com/qunge12345/roboroute_users_guide/blob/master/pictures/01/clip_image017.png?raw=true)

 

| 功能     | 描述                   |
| -------- | ---------------------- |
| 撤销     | 撤销上一步操作         |
| 重做     | 重复上一步操作         |
| 删除     | 删除选中元素           |
| 复制     | 复制选中元素           |
| 粘贴     | 将复制的元素粘贴至此处 |
| 克隆     | 将选中的元素进行克隆   |
| 剪切     | 剪切选中元素到某处     |
| 全选     | 选中所有元素           |
| 取消全选 | 取消所有元素的选中状态 |

动作操作：

![img](https://github.com/qunge12345/roboroute_users_guide/blob/master/pictures/01/clip_image018.png?raw=true)

 

| 功能                       | 描述                                     |
| -------------------------- | ---------------------------------------- |
| 新建业务订单               | 根据需求手动书写业务订单                 |
| 查找机器人                 | 定位想要查找的场景中的机器人             |
| 视图坐标替换为当前场景坐标 | 将视图窗口中的坐标替换为场景中的坐标     |
| 场景坐标替换为当前视图坐标 | 将场景中的坐标替换为当前视图窗口中的坐标 |

视图操作：

![img](https://github.com/qunge12345/roboroute_users_guide/blob/master/pictures/01/clip_image019.png?raw=true)

 

| 功能             | 描述                                           |
| ---------------- | ---------------------------------------------- |
| 添加背景图片     | 为当前编辑的场景添加一张背景图片               |
| 添加场景视图     | 增加一个场景视图窗口                           |
| 添加业务订单视图 | 增加一个业务订单视图窗口                       |
| 添加订单序列视图 | 增加一个订单序列视图窗口                       |
| 插件             | 集成如下的统计、资源分配、自动生成业务订单功能 |
| 统计             | 用于统计机器人运行的信息以及订单执行情况的信息 |
| 资源分配图       | 用于查看所有机器人运行时在场景中占用资源的信息 |
| 自动生成业务订单 | 用于生成随机业务订单（测试推荐）               |
| 重置窗口布局     | 在窗口布局发生变化时使用可以恢复初始布局       |

 

#### 5.4.3 工具栏

工具栏主要进行场景的编辑操作，进行场景元素的增删改查。

![img](https://github.com/qunge12345/roboroute_users_guide/blob/master/pictures/01/clip_image020.png?raw=true)

 

| 工具       | 功能                               | 工具       | 功能                         |
| ---------- | ---------------------------------- | ---------- | ---------------------------- |
| 选择       | 选择场景中的元素                   | 拖拽       | 拖拽场景位于视图窗口中的位置 |
| 节点       | 添加不同类型的节点                 | 工作站     | 添加工作站                   |
| 路径       | 添加不同类型的路径                 | 工作站连接 | 连接工作站与地标点           |
| 工作站类型 | 添加不同类型的工作站以及允许的动作 | 机器人     | 添加机器人                   |
| 互斥区     | 添加互斥区                         | 元素组     |                              |
| 订单书写   | 手动书写业务订单                   | 查找机器人 | 快速定位场景中的某一台机器人 |
| 布局排版   | 将选中元素置于场景中的位置         | 移动       | 将选中元素上下左右移动       |
| 置于顶层   | 将选中元素置于场景的最上层         | 置于底层   | 将选中元素置于场景的最底层   |

#### 5.4.4 场景元素栏

![img](https://github.com/qunge12345/roboroute_users_guide/blob/master/pictures/01/clip_image021.png?raw=true)

 

场景元素栏显示场景中的元素概括，机器人表示在该场景中包含的机器人数量以及名称，可以在此进行机器人的名称编辑；节点表示场景中所有的地标点和停靠点；路径表示场景中地标点之间或者与停靠点之间的路线连接；工作站表示场景中包含的所有的工作站；工作站类型中可以定义不同的工作站，并对在该工作站允许的操作进行定义；工作站连接表示场景中所有工作站与其地标点之间的连接线；以上均支持增删查功能。

#### 5.4.5 互斥区栏

![img](https://github.com/qunge12345/roboroute_users_guide/blob/master/pictures/01/clip_image022.png?raw=true)

 

互斥区（Block）是只允许一台机器人在该设定区域内进行操作的场景元素集合，当一台机器人进入该互斥区时，如果其他机器人前进路线包含该区域中的元素，那么这些机器人会在互斥区之外最近的地标点进行等候，直到互斥区中的机器人执行完操作并驶离该互斥区。

#### 5.4.6 元素组栏

#### 5.4.7 Kernel 关键日志

![img](https://github.com/qunge12345/roboroute_users_guide/blob/master/pictures/01/clip_image023.png?raw=true)

 

显示 Kernel 中的关键日志信息，例如 Kernel 的状态改变，导入的场景地图的改变都会显示在 Kernel 信息栏。

#### 5.4.8 场景视图

![img](https://github.com/qunge12345/roboroute_users_guide/blob/master/pictures/01/clip_image024.png?raw=true)

 

场景视图窗口是监控整个调度运行界面，它包含场景中的所有元素：机器人、工作站、工作站连接、停靠点、地标点、互斥区、路线等；场景视图工具栏如下图：

![img](https://github.com/qunge12345/roboroute_users_guide/blob/master/pictures/01/clip_image025.png?raw=true)

 

由左至右依次：

| 工具       | 描述                         |
| ---------- | ---------------------------- |
| 缩放比例   | 用于选择场景视图的缩放比例   |
| 屏幕自适应 | 场景视图自适应屏幕大小       |
| 显示栅格   | 是否显示背景中的栅格线       |
| 显示标尺   | 是否显示视图左侧和上方的标尺 |
| 显示标签   | 是否显示元素的标签           |
| 显示互斥区 | 是否显示互斥区               |

 

#### 5.4.9 业务订单视图

![img](https://github.com/qunge12345/roboroute_users_guide/blob/master/pictures/01/clip_image026.png?raw=true)

 

业务订单视图窗口用于显示全部的业务订单，字段具体含义详细见 8.3 小节。

![img](https://github.com/qunge12345/roboroute_users_guide/blob/master/pictures/01/clip_image027.png?raw=true)

 

鼠标双击业务订单，会出现上图所示的业务订单详细页面，其中字段含义如下表：

| 字段       | 释义               | 字段             | 释义                           |
| ---------- | ------------------ | ---------------- | ------------------------------ |
| Name       | 订单名称           | 拒绝/机器人/原因 | 未执行完成的机器人以及失败原因 |
| 创建       | 创建时间           | 订单子任务       | 一个业务订单中包含的子任务     |
| 完成       | 完成时间           | 元属性           | 元属性                         |
| 截止时间   | 订单预期截止时间   | 路线             | 路线                           |
| 机器人     | 执行该订单的机器人 | 目标工作站       | 目标工作站                     |
| 非必要订单 | 是否为非必要订单   | 路线成本         | 路线成本设定                   |
| 业务类型   | 选择业务类型       | 订单依赖         | 该订单执行需要依赖的订单       |

**注释**：非必要订单：如果该订单被置为非必要订单，那么在机器人执行过程中如果有新的未执行业务订单存在，会优先执行其他业务订单，该非必要业务订单会自动流产。

#### 5.4.10 业务订单序列视图

![img](https://github.com/qunge12345/roboroute_users_guide/blob/master/pictures/01/clip_image028.png?raw=true)

 

业务订单序列表示可以将一系列订单统一加入到一个订单序列中，然后供某一台机器人全部执行。

业务订单序列字段解析：

| 字段         | 释义                                                         |
| ------------ | ------------------------------------------------------------ |
| Name         | 业务订单序列名称                                             |
| 指定机器人   | 被指定执行该序列的机器人                                     |
| 执行机器人   | 实际执行该序列的机器人                                       |
| Index        | 序列索引，初始值为-1                                         |
| 创建完成     | 订单序列是否创建完成                                         |
| 执行完成     | 订单序列是否执行完成                                         |
| 允许序列失败 | 是否允许订单序列失败，true   表示任何一个失败即序列失败，false 表示某一个失败会继续执行其他 |

## 六、编辑场景

### 6.1 使用 Roboshop Pro 软件构建原始场景

#### 6.1.1 扫描地图

机器人出厂后只存有一张名为 default.smap 地图，在实际环境中使用时需要扫描环境地图后才能使用。扫描地图分为两种模式，分别为实时扫图（在线SLAM）和离线扫图（离线SLAM）。

**注****1****：** **扫图时请勿控制机器人运动的过快，建议扫图速度为** **0.5 m/s****。**

**注****2****：** **扫图时如果地面较滑，请勿同时控制机器人转向和前进，否则容易造成打滑现象，影响建图效果。**

**注****3****：** **尽量沿着机器人工作时的线路扫描地图，来回扫描可使建图效果更佳。**

#### 6.1.2 离线扫图

离线扫图即先扫描环境数据再进行地图构建。需要遥控机器人在环境中运行一圈后，再进行地图构建。

点击模块工具栏中的开始扫图按钮 ![标题: fig:](https://github.com/qunge12345/roboroute_users_guide/blob/master/pictures/01/clip_image029.png?raw=true)，图标变为 ![标题: fig:](https://github.com/qunge12345/roboroute_users_guide/blob/master/pictures/01/clip_image030.png?raw=true)后说明已开始离线扫图。

手动操控机器人在环境中运行一遍，使机器人的激光雷达扫描到环境中的大部分区域。完成后使机器人停止，点击 ![标题: fig:](https://github.com/qunge12345/roboroute_users_guide/blob/master/pictures/01/clip_image031.png?raw=true)后将弹出地图构建窗口，如下：

![img](https://github.com/qunge12345/roboroute_users_guide/blob/master/pictures/01/clip_image032.png?raw=true)

 

建图参数配置中的参数一般不需要修改，点击确定按钮即开始构建地图。此时窗口中将复现刚才机器人的运动轨迹同时构建地图，当进度条读到 100% 后地图构建完毕，最终效果如下：

![img](https://github.com/qunge12345/roboroute_users_guide/blob/master/pictures/01/clip_image033.png?raw=true)

 

图中的红色轨迹即为机器人扫描地图时的运动轨迹。

此时请勿关闭建图窗口，请点击右上角中的 ![标题: fig:](https://github.com/qunge12345/roboroute_users_guide/blob/master/pictures/01/clip_image034.png?raw=true)按钮将构建的地图保存至计算机磁盘中。在弹出的保存对话框中可以对地图进行命名。

**注****1****：** **在控制机器人扫描环境时，请保持与机器人的网络连接畅通。**

**注****2****：** **在构建地图的过程中请勿关闭建图窗口，除非需要放弃本次地图构建。**

若不慎在建图过程中将建图窗口关闭，或地图构建完成后忘记另存为.smap就关闭了窗口，可以点击模块工具栏中的 按钮将最近一次的扫描数据重新取回并重新唤出建图窗口。

#### 6.1.3 实时扫图

实时扫图即同时进行环境数据的扫描和地图构建。遥控机器人在环境中运行一圈后即可生成地图。

点击模块工具栏中的实时扫图按钮 ![标题: fig:](https://github.com/qunge12345/roboroute_users_guide/blob/master/pictures/01/clip_image035.png?raw=true)，唤出实时建图窗口，如下图：

![img](https://github.com/qunge12345/roboroute_users_guide/blob/master/pictures/01/clip_image036.png?raw=true)

 

点击 ![标题: fig:](https://github.com/qunge12345/roboroute_users_guide/blob/master/pictures/01/clip_image037.png?raw=true)按钮，该按钮会变为 ![标题: fig:](https://github.com/qunge12345/roboroute_users_guide/blob/master/pictures/01/clip_image038.png?raw=true)并建图参数配置对话框，同样不需要对参数进行修改，点击确定即开始实时扫图。

此时请勿关闭实时建图窗口，用鼠标移动至工作空间的范围内并单击鼠标左键一下，目的是将软件的焦点切换回工作空间，这样才能够使用键盘快捷键控制机器人运动。通过键盘的W、A、S、D键控制机器人在环境中运动（与离线扫图相同）。随着机器人的运动，实时建图的窗口中会实时显示机器人的运动轨迹以及当前已经构建完毕的地图，如下图：

![img](https://github.com/qunge12345/roboroute_users_guide/blob/master/pictures/01/clip_image039.png?raw=true)

 

当完成对环境的扫描后，点击 ![标题: fig:](https://github.com/qunge12345/roboroute_users_guide/blob/master/pictures/01/clip_image040.png?raw=true)。此时程序将对地图做最后的优化后完成地图构建，最终效果如下：

![img](https://github.com/qunge12345/roboroute_users_guide/blob/master/pictures/01/clip_image041.png?raw=true)

 

点击 ![标题: fig:](https://github.com/qunge12345/roboroute_users_guide/blob/master/pictures/01/clip_image042.png?raw=true)将构建的地图保存至计算机磁盘。

#### 6.1.4 加载地图

在机器人控制模块加载地图，可以通过 菜单栏->文件->加载地图 唤出文件选择对话框的方式。

若事先在地图编辑模块加载了地图，此时切换到机器人控制模块，加载的地图将保留。即地图编辑模块和机器人控制模块是共用地图的。在机器人控制模块也可以加载多张地图，并在多个地图标签页中切换。

与地图编辑模块不同的是，在机器人控制模块无法对地图进行编辑修改，只能点击地图中的元素以查看其相关属性。

若加载了地图，此时连接上机器人后，当前工作空间中的地图上将显示机器人，如下图：

![img](https://github.com/qunge12345/roboroute_users_guide/blob/master/pictures/01/clip_image043.png?raw=true)

 

图中显示机器人的长宽为实际值，蓝色部分表示机器人头部。红色部分为置信度的颜色，根据置信度的降低，该部分将从绿色渐变为红色。图中呈蓝色放射状的是当前机器人激光雷达扫描到的环境形状。

#### 6.1.5 导出 RoboRoute 地图

![img](https://github.com/qunge12345/roboroute_users_guide/blob/master/pictures/01/clip_image044.png?raw=true)

                      ![1538989881122](C:\Users\dell\AppData\Local\Temp\1538989881122.png?raw=true)

使用 Roboshop 编辑完成整个场景中的路线之后，点击导出功能，选择导出 RoboRoute 地图，选择想要导出的路径，如果地图中线路全部为单向线，则将加入block前面的对勾去掉，然后将 Roboshop 的 smap 地图转换成 RoboRoute 的XML地图（ smap 地图编辑参考 Roboshop 使用手册）。 

### *6.2 使用 Roboshop Pro 软件融合场景文件

![1538990123441](C:\Users\dell\AppData\Local\Temp\1538990123441.png?raw=true)

RoboRoute 地图导出路径：RoboRoute 地图最终存放的位置；

车辆信息地图路径：已存在的且想要将其中的机器人融合到该地图中的 RoboRoute 地图位置；

工作点信息地图路径：已存在的且想要将其中的工作站点融合到该地图中的 RoboRoute 地图位置；

### *6.3 使用 Roboshop Pro 软件更新场景文件

![1538990173451](C:\Users\dell\AppData\Local\Temp\1538990173451.png?raw=true)

RoboRoute 地图导出路径：RoboRoute 地图最终存放的位置；

所需更新文件路径：已存在的 RoboRoute 地图，在 smap 发生变化后需要更新地图但是保留机器人与工作站信息时使用。

### 6.4 切换至编辑模式

打开Viewer，默认模式为编辑模式；手动模式切换需要选择文件菜单下的模式，然后选择编辑模式或者操作模式；或者使用快捷键方式，Alt + M（编辑模式）、Alt + O （操作模式）。

### 6.5 载入场景

选择文件—>导入场景，在导入场景对话框中选择你要导入场景的路径，选择打开，场景自动加载到场景视图中。

![img](https://github.com/qunge12345/roboroute_users_guide/blob/master/pictures/01/clip_image045.png?raw=true)

 

### 6.6 添加机器人

![img](https://github.com/qunge12345/roboroute_users_guide/blob/master/pictures/01/clip_image046.png?raw=true)

 

![img](https://github.com/qunge12345/roboroute_users_guide/blob/master/pictures/01/clip_image047.png?raw=true)

 

在编辑模式下，选择机器人工具进行场景中机器人的添加，在机器人名称栏编辑机器人铭牌上的机器人ID，机器人的实际车长，路线颜色，低电量报警阈值以及充足阈值，最大正向速度与最大反向速度可以根据 Roboshop 的 smap 中的路线速度进行设定，需要根据不同的车型选择自主充电类型。

#### 6.6.1 编辑可执行的业务类型

TODO

#### 6.6.2 编辑自主充电类型

TODO

### 6.7 添加工作站信息

![img](https://github.com/qunge12345/roboroute_users_guide/blob/master/pictures/01/clip_image048.png?raw=true)

 

![img](https://github.com/qunge12345/roboroute_users_guide/blob/master/pictures/01/clip_image049.png?raw=true)

 

在编辑模式下，选择工具栏工作站选项添加工作站，然后在工作站信息栏编辑关键信息，设定该工作站的名称，如果该工作站是由 smap 自动导出生成，那么名称不变，如果是手动添加的工作站，那么需要重新命名，选择该工作站的类型，该类型必须在工作站类型中存在，否则路径规划会报错。

### 6.8 保存场景

在编辑模式下，选择文件—>保存场景，或者使用快捷键 Ctrl + S 保存当前编辑的场景；使用文件—>场景另存为，可以将场景重命名保存到文件夹。

### 6.9 显示场景信息

![img](https://github.com/qunge12345/roboroute_users_guide/blob/master/pictures/01/clip_image050.png?raw=true)

 

选择文件—>显示场景信息，可以显示场景中的如下信息：

| 字段           | 释义                         |
| -------------- | ---------------------------- |
| 地标点数量     | 场景中所包含的地标点总数     |
| 路径数量       | 场景中所包含的路径总数       |
| 工作站数量     | 场景中所包含的工作站总数     |
| 工作站类型数量 | 场景中所包含的工作站类型总数 |
| 互斥区数量     | 场景中所包含的互斥区总数     |
| 机器人数量     | 场景中所包含的机器人总数     |
| 最后修改日期   | 场景的最后修改日期           |

 

### 6.10 Viewer 向 Kernel 同步场景

编辑完成的场景，或者最新导入的场景，都需要同步到 kernel 并且在 Kernel 中进行初始化之后才能使用，选择文件—>将场景同步至 Kernel 功能，Viewer 会在软件上方的连接信息中显示所连接到的 Kernel IP和端口号，如下图：

![img](https://github.com/qunge12345/roboroute_users_guide/blob/master/pictures/01/clip_image051.png?raw=true)

 

然后在 Kernel 中进行初始化操作，初始化完成后，在 Viewer 中选择文件—>模式—>操作模式，在经过一段非常美妙的动画之后，Viewer 会切换到操作模式，此时界面如下：

![img](https://github.com/qunge12345/roboroute_users_guide/blob/master/pictures/01/clip_image052.png?raw=true)

 

### 6.11 Viewer 导入 Kernel 当前场景

选择文件—>导入 Kernel 场景，此时会将 Kernel 中的场景导入到 Viewer 中，导入以后为默认模式：编辑模式。此功能更倾向用于 Viewer 中途退出（这种可能性几乎为0）或者人为不小心关闭后（这种可能性蛮大）以便快速恢复调度系统而进行的操作。

### 6.12 场景编辑规则

#### 6.12.1 单向路线

![img](https://github.com/qunge12345/roboroute_users_guide/blob/master/pictures/01/clip_image053.png?raw=true)

 

场景中的路线设计建议使用单向路线，如上图所示，在某些特殊的工作站需要使用双向线时需要将双向线加入到互斥区中，保证在该区域每次只有一台机器人执行操作。

#### 6.12.2 交叉路线设计

![img](https://github.com/qunge12345/roboroute_users_guide/blob/master/pictures/01/clip_image054.png?raw=true)

 

交叉点是不同方向的路线重叠的必然产物，在实际场景中出现路线交叉情况必须使用节点对整条路线进行分割，若同一个场景中仅有一台机器人，不存在机器人之间共享路径资源的情况，那么交叉线可以分割也可以不分割，若同一个场景中包含两台及以上的机器人，那么会出现不同机器人之间共享路径资源的情况，交叉线必须使用节点进行分割。

#### 6.12.3 停靠点及工作站设计

![img](https://github.com/qunge12345/roboroute_users_guide/blob/master/pictures/01/clip_image055.png?raw=true)

 

如上图中的蓝色地标点即为停靠点，建议在场景中设置大于等于机器人数量的停靠点，停靠点放置于主干道之外（如上图），停靠点的进出建议使用单行线。

工作站的设计很大程度上取决于 smap 中的工作点位，由于实际场景中工作点位需要进行产线对接，物料传送等功能，所以在smap转换为XML地图之后，工作站原则上不需要进行手动编辑，只需要定义不同的工作站类型，然后为每个工作站选择工作站类型即可。

#### 6.12.4 双向路线及互斥区

场景设计时我们推荐优先使用单向路线，但是例如充电点位或者特殊工作站，必须使用双向路线的情况，可以启用互斥区进行该区域的保护。

![img](https://github.com/qunge12345/roboroute_users_guide/blob/master/pictures/01/clip_image056.png?raw=true)

 

在工具栏选择互斥区功能，在信息栏会出现互斥区信息栏，如下图，在场景视图中选择想要添加到该互斥区的元素，然后在该互斥区名称上单击鼠标右键，弹出如下菜单栏，选择添加选中元素至互斥区，被选中元素即可被添加到该互斥区，互斥区颜色可以在信息栏的颜色选择器中进行选择。

![img](https://github.com/qunge12345/roboroute_users_guide/blob/master/pictures/01/clip_image057.png?raw=true)

 

![img](https://github.com/qunge12345/roboroute_users_guide/blob/master/pictures/01/clip_image058.png?raw=true)

 

添加到互斥区之后的场景视图变为如下图所示，颜色相同的为一个互斥区，例如：图中蓝色元素的部分为一个互斥区，红色元素部分为一个互斥区：

![img](https://github.com/qunge12345/roboroute_users_guide/blob/master/pictures/01/clip_image059.png?raw=true)

 

互斥区的生成规则：

![img](https://github.com/qunge12345/roboroute_users_guide/blob/master/pictures/01/clip_image060.png?raw=true)

 

 

#### 6.12.5有向强连通图

强连通图（Strongly Connected Graph）是指在有向图G中，如果对于每一对节点，从A到B和从B到A都存在路径，则称G是强连通图。有向图中的极大强连通子图称做有向图的强连通分量。强连通图具有如下定理：一个有向图G是强连通的，当且仅当G中有一个回路，它至少包含每个节点一次。 

## 七、机器人配置及操作

### 7.1 使用 Roboshop Pro 软件配置机器人

![img](https://github.com/qunge12345/roboroute_users_guide/blob/master/pictures/01/clip_image061.png?raw=true)

 

在 Roboshop 中选择参数配置，将 ServerIP 配置成调度服务器的IP地址，ServerPort 配置成调度服务器的端口号（使用默认即可），将 VehicleID 配置成机器人铭牌ID，最后单击永久修改。

### 7.2 使用 Roboshop Pro 软件载入场景对应的 smap

在机器人控制模块加载地图，可以通过 菜单栏->文件->加载地图 唤出文件选择对话框的方式，找到 smap 文件存放的路径，然后打开。

### 7.3 使用 Roboshop Pro 软件重定位机器人

重定位用于使机器人获得正确的定位状态。通过指定一个比较模糊的初始定位点和方向，让机器人自己计算其精确的位置和方向。重定位也是使机器人能进入正确工作状态的重要一步。

如下图所示：

 ![标题: fig:](https://github.com/qunge12345/roboroute_users_guide/blob/master/pictures/01/clip_image062.png?raw=true)

机器人的激光形状没有和地图匹配上，机器人的颜色为橘色说明置信度比较低，因此机器人当前的定位是不正确的。实际情况，机器人处于途中红色箭头标识处。

点击 ![标题: fig:](https://github.com/qunge12345/roboroute_users_guide/blob/master/pictures/01/clip_image063.png?raw=true)按钮，鼠标变成蓝色箭头状 ![标题: fig:](https://github.com/qunge12345/roboroute_users_guide/blob/master/pictures/01/clip_image064.png?raw=true)。在上图中红色箭头处的位置按下鼠标左键不松开，拖动鼠标拉出方向线，使方向线的朝向与上图中箭头的朝向一致，再松开鼠标左键，如图：

 ![标题: fig:](https://github.com/qunge12345/roboroute_users_guide/blob/master/pictures/01/clip_image065.png?raw=true)

此时会弹出正在重定位的对话框：

 ![标题: fig:](https://github.com/qunge12345/roboroute_users_guide/blob/master/pictures/01/clip_image066.png?raw=true)

稍等片刻重定位完成后得到如下效果：

 ![标题: fig:](https://github.com/qunge12345/roboroute_users_guide/blob/master/pictures/01/clip_image067.png?raw=true)

可以看到机器人的激光已经基本与地图匹配上，此时机器人的定位已经正确。重定位完成后同时会弹出确认位置正确的对话框，点击确定可将机器人定位的状态设置为正确。若点击取消，机器人的定位只是处于定位完成状态，此时仍是无法切换到自动模式的，因为必须将定位状态设置为正确才能切换到自动模式。

如果定位完成后出现如下情况：

 ![标题: fig:](https://github.com/qunge12345/roboroute_users_guide/blob/master/pictures/01/clip_image068.png?raw=true)

可以看到，机器人的激光依然没有与地图匹配上，所以这次重定位是失败的，原因可能为点击的重定位点或者拖出的方向线与机器人实际的位置相差太远。此时在弹窗中不能点确定，而应该点取消，然后重新进行重定位操作。

### 7.4 使用 Roboshop Pro 软件释放控制权

![img](https://github.com/qunge12345/roboroute_users_guide/blob/master/pictures/01/clip_image069.png?raw=true)

 

在 Roboshop 中将机器人放置到某个确定的点位，然后确认机器人定位正确后，单击释放控制权，使机器人自动去连接调度服务器，如果机器人的状态由UNAVAILABLE变为IDLE，表明连接成功，此时 Roboshop 无法控制机器人动作。

![img](https://github.com/qunge12345/roboroute_users_guide/blob/master/pictures/01/clip_image070.png?raw=true)

 

### 7.5 使用 Roboshop Pro 软件回收控制权

![img](https://github.com/qunge12345/roboroute_users_guide/blob/master/pictures/01/clip_image071.png?raw=true)

 

在 Roboshop 中，点击回收控制权可以断开机器人与调度系统的连接，此时可以使用 Roboshop 控制机器人；调度系统中被回收控制权的机器人的状态变为：UNAVAILABLE。

### 7.6 使能机器人通信适配器

![img](https://github.com/qunge12345/roboroute_users_guide/blob/master/pictures/01/clip_image072.png?raw=true)

 

在适配器栏选择机器人使用的适配器，然后在是否可用栏勾选可用，该适配器即生效。

### 7.7 确认机器人位置

![img](https://github.com/qunge12345/roboroute_users_guide/blob/master/pictures/01/clip_image073.png?raw=true)

 

在 Kernel 中确认机器人位置，该位置与机器人实际位置必须一致。

## 八、操作模式

### 8.1 切换至操作模式

在将模型同步到 Kernel 以后，并在 Kernel 中将机器人初始化后，选择文件—>模式，切换到操作模式，或者使用快捷键 Alt + O；此时视图窗口中会出现机器人窗口和场景视图窗口；界面如下：

### 8.2 新建业务订单

创建业务订单的方式有三种：

1、使用创建业务订单功能：单击添加按钮，选择需要目的地工作站以及所要执行的动作，在机器人复选框中可以指定执行该业务订单的机器人，或者选择自动分配机器人。

![img](https://github.com/qunge12345/roboroute_users_guide/blob/master/pictures/01/clip_image074.png?raw=true)

 

2、使用 Web API 创建业务订单：Web API 是与调度对接的标准协议，协议提供：创建业务订单，撤回业务订单，查询业务订单状态和机器人状态等功能，详情请看11.5 Web API 链接。

3、使用自动生成业务订单插件创建业务订单：详情请看10.2小节。

### 8.3 业务订单视图

![img](https://github.com/qunge12345/roboroute_users_guide/blob/master/pictures/01/clip_image075.png?raw=true)

 

| 字段           | 释义                                                 |
| -------------- | ---------------------------------------------------- |
| Name           | 订单名称，具有唯一性                                 |
| 始发工作站     | 该订单执行所要前往的第一个工作站                     |
| 终点工作站     | 该订单执行所要前往的最后一个工作站                   |
| 指定机器人     | 可以选择某个特定的机器人或者由调度系统自动分配机器人 |
| 执行中的机器人 | 该订单被分配至某个特定的机器人                       |
| Status         | 订单的状态                                           |
| 序列           | 订单所属的订单序列，只有存在订单依赖时会显示         |

 

#### 8.3.1 筛选业务订单列表

![img](https://github.com/qunge12345/roboroute_users_guide/blob/master/pictures/01/clip_image076.png?raw=true)

 

业务订单筛选工具：

| 工具                                       | 描述                                    |
| ------------------------------------------ | --------------------------------------- |
| 无法规划的业务订单（状态=RAW）             | 查询订单状态为RAW的业务订单             |
| 待派遣的业务订单（状态=DISPATCHABLE）      | 查询订单状态为DISPATCHABLE的业务订单    |
| 正在处理的业务订单（状态=BEING_PROCESSED） | 查询订单状态为BEING_PROCESSED的业务订单 |
| 已完成的业务订单（状态=FINISHED）          | 查询订单状态为FINISHED的业务订单        |
| 失败的业务订单（状态=FAILED）              | 查询订单状态为FAILED的业务订单          |
| 撤回业务订单                               | 撤回业务订单，支持单个撤回和批量撤回    |

 

#### 8.3.2 查看业务订单状态

业务订单 Status 分析：

Active：订单存在依赖，需要等待被依赖订单处理完成后才能进行派遣；

Unrouteable：订单非法，起始点位无法到达，路径无法规划；

DISPATCHABLE：单例订单，且订单合法，允许派遣机器人；

RAW：订单非法，订单中存在非场景中的元素，请检查元素详细信息；

BEING_PROCESSED：订单合法，且已有机器人正在执行该订单；

FINISHED：订单合法，且该订单已成功执行完成；

FAILED：订单合法，但是由于人为撤回订单或者调度自动撤回订单，导致订单失败；

#### 8.3.3 撤销业务订单

撤销业务订单支持按照订单名称撤回和按照机器人撤回两种方式：

按照订单名称撤回：选中您要撤回的一个或几个订单，然后单击撤回业务订单按钮，将订单撤回。

![img](https://github.com/qunge12345/roboroute_users_guide/blob/master/pictures/01/clip_image077.png?raw=true)

 

按照机器人撤回：在需要撤回订单的机器人图标上单击鼠标右键，弹出如下菜单栏，选择撤销业务订单，根据实际需求选择撤销订单的方式。

![img](https://github.com/qunge12345/roboroute_users_guide/blob/master/pictures/01/clip_image078.png?raw=true)

 

![img](https://github.com/qunge12345/roboroute_users_guide/blob/master/pictures/01/clip_image079.png?raw=true)

 

| 订单撤回方式     | 释义                                               |
| ---------------- | -------------------------------------------------- |
| 并到达下一节点   | 撤销当前执行的订单，但机器人会继续前进到下一个节点 |
| 并立即停止机器人 | 撤销当前执行的订单，机器人立即停止                 |

 

### 8.4 业务订单序列视图

#### 8.4.1 查看业务订单序列状态

![img](https://github.com/qunge12345/roboroute_users_guide/blob/master/pictures/01/clip_image080.png?raw=true)

 

业务订单序列中的指定机器人与执行机器人一栏，理论上是同一台车，Index 索引栏表示订单序列中存在N个子订单，当前执行订单在序列中的索引，由于索引最高数值为N-1，所以在N为0的时候，Index 的起始值为-1，出现显示-1的情况为正常；创建完成表示订单序列中子订单是否全部添加完成；执行完成表示整个订单序列是否执行完成；允许序列失败表示是否允许序列失败，其含义：

允许序列失败：在整个订单序列中如果存在某一个子订单失败，此时整个序列会全部失败，不会继续执行剩余订单；

不允许序列失败：在整个订单序列中如果存在某一个子订单失败，此时整个序列不会全部失败，会继续执行剩余订单；

### 8.5 机器人视图

![img](https://github.com/qunge12345/roboroute_users_guide/blob/master/pictures/01/clip_image081.png?raw=true)

 

机器人视图窗口包含：机器人名称、机器人图标、实时电量、在线状态、机器人状态以及机器人当前位置。

#### 8.5.1 机器人图标说明

| 图标                                                         | 释义                     | 图标                                                         | 释义               |
| ------------------------------------------------------------ | ------------------------ | ------------------------------------------------------------ | ------------------ |
| ![img](https://github.com/qunge12345/roboroute_users_guide/blob/master/pictures/01/clip_image082.png?raw=true) | 正常机器人无负载状态     | ![img](https://github.com/qunge12345/roboroute_users_guide/blob/master/pictures/01/clip_image085.png?raw=true) | 负载机器人正常状态 |
| ![img](https://github.com/qunge12345/roboroute_users_guide/blob/master/pictures/01/clip_image083.png?raw=true) | 故障机器人无负载状态     | ![img](https://github.com/qunge12345/roboroute_users_guide/blob/master/pictures/01/clip_image086.png?raw=true) | 负载机器人故障状态 |
| ![img](https://github.com/qunge12345/roboroute_users_guide/blob/master/pictures/01/clip_image084.png?raw=true) | 正常机器人无负载充电状态 | ![img](https://github.com/qunge12345/roboroute_users_guide/blob/master/pictures/01/clip_image087.png?raw=true) | 负载机器人充电状态 |

 

#### 8.5.2 机器人状态

机器人状态解析：

UNAVAILABLE：机器人未连接到调度服务器，处于离线状态；

IDLE：机器人连接到调度服务器，处于在线可用状态；

ERROR：机器人故障或执行任务失败出现异常，处于不可用状态；

EXECUTING：机器人在线，并正在执行业务订单，处于执行状态；

CHARGING：机器人在线，并正在执行充电操作，处于执行状态；

UNKNOWN：机器人不属于场景之中，处于不可用状态；

#### 8.5.3 机器人在线状态

机器人在线状态解析：

离线：机器人未连接到调度服务器或者机器人仅标记场景中的位置；

在线不可用：机器人连接到调度服务器且机器人状态为不可用状态；

在线可用：机器人连接到调度服务器且机器人状态为可用状态；

#### 8.5.4 机器人电量

机器人的电量等级：

低电量报警阈值：该阈值线表示当机器人低于该线时会自动去充电，此时不会再接受新的业务订单，如果无空闲充电点位，机器人会寻找停靠点进行自动泊车；

电量充足阈值：该阈值线表示当机器人高于该线时会告知调度系统允许派发新的业务订单；

电量不充足：当机器人的电量处于报警阈值与充足阈值之间时，成为电量不充足，此时机器人依然能够正常接受业务订单的派遣；

#### 8.5.5 聚焦和跟踪机器人

![img](https://github.com/qunge12345/roboroute_users_guide/blob/master/pictures/01/clip_image088.png?raw=true)

 

在机器人图标上单击右键，弹出如上图菜单栏，聚焦机器人和跟踪机器人都是为了在复杂的场景中快速定位某台机器人而设定。

聚焦机器人：该机器人的图标颜色会发生如下变化，可以快速区分需要寻找的机器人；

![img](https://github.com/qunge12345/roboroute_users_guide/blob/master/pictures/01/clip_image089.png?raw=true)

 

跟踪机器人：被跟踪的机器人会被动感光圈所环绕，在机器人行走的过程中，光圈会一直伴随其左右，便于人类发现该机器人；

![img](https://github.com/qunge12345/roboroute_users_guide/blob/master/pictures/01/clip_image090.png?raw=true)

 

#### 8.5.6 派遣机器人至节点

![img](https://github.com/qunge12345/roboroute_users_guide/blob/master/pictures/01/clip_image091.png?raw=true)

 

在机器人图标上单击右键，弹出如上图菜单。

派遣至节点提供定点导航功能，选择派遣至节点后选择需要到达的点位，然后单击确定按钮，机器人会自动规划最优路径前往目标节点；

![img](https://github.com/qunge12345/roboroute_users_guide/blob/master/pictures/01/clip_image092.png?raw=true)

 

 

#### 8.5.7 派遣机器人至工作站

派遣至工作站提供定点导航加执行动作功能，选择派遣制工作站后选择需要到达的工作站并指定到达该工作站后需要进行的动作，然后单击确定按钮，机器人会自动规划最优路径前往目标工作站；

![img](https://github.com/qunge12345/roboroute_users_guide/blob/master/pictures/01/clip_image093.png?raw=true)

 

#### 8.5.8 更改机器人在线状态

![img](https://github.com/qunge12345/roboroute_users_guide/blob/master/pictures/01/clip_image091.png?raw=true)

 

在机器人图标上单击右键，弹出如上图菜单。

![img](https://github.com/qunge12345/roboroute_users_guide/blob/master/pictures/01/clip_image094.png?raw=true)

 

在线状态解析：

| 状态                 | 释义                                                         |
| -------------------- | ------------------------------------------------------------ |
| 将机器人置为离线状态 | 断开机器人与调度服务器的连接，并从当前场景视图中移除，在线状态为离线 |
| 仅标记机器人位置     | 将机器人在场景中的位置占用，在线状态为离线                   |
| 仅将机器人载入场景   | 将移除的机器人重新载入场景并占用当前位置，在线状态为在线不可用 |
| 将机器人置为在线状态 | 将机器人连接到调度服务器，并可以接受业务订单派遣，在线状态为在线可用 |

####  8.5.9 一键暂停所有机器人

![1538991758686](C:\Users\dell\AppData\Local\Temp\1538991758686.png?raw=true)

在操作模式下，工具栏最右侧红色按钮是一键暂停所有机器人操作，在遇到紧急情况需要将所有机器人立刻暂停时使用。

### 8.6 典型操作流程

1. 双击桌面 StartAll 文件，将 redis、Kernel、Viewer 全部启动；

   ![1539053537145](C:\Users\dell\AppData\Local\Temp\1539053537145.png?raw=true)

2. 在 Viewer 中导入场景，并将该场景同步到 Kernel 中；

   ![1539053724219](C:\Users\dell\AppData\Local\Temp\1539053724219.png?raw=true)

3. 在 Kernel 中初始化场景，将需要使用的机器人勾选，选择适配器，并为每个机器人初始化位置，此时如果机器人连接调度服务器成功状态会变为IDLE，否则状态为UNAVAILABLE，此时使用 RoboShop 检查是否释放控制权成功；

   ![1539053829689](C:\Users\dell\AppData\Local\Temp\1539053829689.png?raw=true)

4. 在 Viewer 中将模式切换到操作模式，确认机器人所在点位正确后，使用一键派遣所有机器人功能将机器人在线状态全部置为在线可用；

   ![1539054022466](C:\Users\dell\AppData\Local\Temp\1539054022466.png?raw=true)

5. 此时机器人等待MES发送业务订单，在接收到订单后会自动进行订单分配以及机器人派遣，双击运行MES程序，可以在业务订单视图看到已经接收到订单，并分配给机器人，图中不同颜色的路线为不同机器人将要运行的路线；

   ![1539054529923](C:\Users\dell\AppData\Local\Temp\1539054529923.png?raw=true)

   ![1539054558643](C:\Users\dell\AppData\Local\Temp\1539054558643.png?raw=true)

6. 撤销某一台机器人当前执行的业务订单，示例如下：在AMB-300-1808-01机器人图标上单击右键，选择撤销业务订单功能，在二级菜单中选择并立即停止机器人，此时该机器人规划好的行驶路线会消失，机器人状态变为IDLE，等待新的业务订单分配；

   ![1539055149155](C:\Users\dell\AppData\Local\Temp\1539055149155.png?raw=true)

7. 当遇到紧急情况需要立即停止全部机器人时，单击工具栏暂停所有机器人按钮即可；

   ![1538991758686](C:\Users\dell\AppData\Local\Temp\1538991758686.png?raw=true)

## 九、RoboRoute 配置（公司内部人员，以及集成商使用）

### 9.1 Kernel 关键配置列表

| 字段                                       | 含义                 | 字段                                               | 含义                 |
| ------------------------------------------ | -------------------- | -------------------------------------------------- | -------------------- |
| kernelapp.   autoEnableDriversOnStartup    | 启动自动使能         | kernelapp.   saveModelOnTerminateModelling         | 退出编辑模式自动保存 |
| kernelapp.   saveModelOnTerminateOperating | 退出操作模式自动保存 | kernelapp.   updateRoutingTopologyOnPathLockChange | 路径锁定后更新拓扑图 |
| orderpool.   sweepInterval                 | 扫描间隔             | orderpool.   sweepAge                              | 订单保存时间         |
| rmikernelinterface.enable                  | 远程调用接口是否可用 | rmikernelinterface.useSsl                          | 是否加密             |
| controlcenter.language                     | 语言选择             | rmikernelinterface.   registryHost                 | 注册主机             |
| rmikernelinterface.   registryPort         | 注册端口号           |                                                    |                      |

 

### 9.2 Viewer 关键配置列表

| 字段                          | 含义             | 字段                         | 含义               |
| ----------------------------- | ---------------- | ---------------------------- | ------------------ |
| ignoreVehicleOrientationAngle | 忽略机器人朝向角 | ignoreVehiclePrecisePosition | 忽略机器人精确位置 |
| plantoverviewapp.initialMode  | 默认模式         | plantoverviewapp.language    | 语言选择           |

 

## 十、扩展插件

### 10.1 订单统计

![img](https://github.com/qunge12345/roboroute_users_guide/blob/master/pictures/01/clip_image095.png?raw=true)

 

订单统计提供整个场景中机器人、点位、订单的处理信息。

机器人数据分析：

| 字段       | 释义                             |
| ---------- | -------------------------------- |
| 名称       | 机器人名称                       |
| 运行时间   | 机器人运行时间总和               |
| 等待时间   | 机器人处理订单过程中等待时间总和 |
| 订单已处理 | 机器人处理完成的订单数量         |
| 充电时间   | 机器人充电时间总和               |

点位分析：

| 字段     | 释义                   |
| -------- | ---------------------- |
| 地标点   | 地标点位ID             |
| 占用时间 | 该点位被占用的时间总和 |

订单分析：

| 字段     | 释义                           |
| -------- | ------------------------------ |
| 名称     | 业务订单名称                   |
| 时间分配 | 订单预期时间                   |
| 处理时间 | 业务订单实际处理时间           |
| 成功     | 业务订单最终处理状态，成功与否 |
| 超时     | 订单实际完成时间与预期时间差值 |

 

### 10.2 随机订单测试

![img](https://github.com/qunge12345/roboroute_users_guide/blob/master/pictures/01/clip_image096.png?raw=true)

 

在测试环节可以选择自动生成订单功能来创建订单，选择生成订单的条件然后勾选最下方的生成业务订单，订单就会自动创建并添加到业务订单视图中。

| 参数                    | 释义                                                         |
| ----------------------- | ------------------------------------------------------------ |
| 仅创建一次              | 创建单次订单，仅生成一次                                     |
| 少于N要被处理的业务订单 | N是订单的数量，在订单列表中少于N个时会持续自动生成           |
| 间隔时间                | 两次自动生成业务订单的间隔时间                               |
| 随机业务订单            | 首个参数代表每次生成订单的个数，第二个代表每个业务订单包含的订单子任务数量 |
| 根据目的地创建业务订单  | 勾选后下方的添加新业务订单按钮可用                           |
| 添加新业务订单          | 选择截止时间和需要执行的机器人来生成业务订单                 |
| 新建订单子任务          | 选择目的地工作站以及所要执行的动作来生成订单子任务           |
| 打开                    | 打开已编辑好的订单配置表                                     |
| 保存                    | 将本次编辑作为模板保存至文件夹                               |

 

## 十一、关于

### 11.1 关于软件

RoboRoute 是上海仙知机器人科技有限公司（Seer Robotics，以下简称 仙知）开发的多机器人调度系统。  仙知整合 RoboRoute 系统、Roboshop Pro 软件，以及 SRC2000 系列控制器，可针对多种类、多数量移动机器人复杂操作与协同配合的场景，提供快速、专业的整厂解决方案，以此提升工厂的整体作业效率。

### 11.2 关键术语表

| 术语           | 释义       | 详细解释                           |
| -------------- | ---------- | ---------------------------------- |
| Model          | 场景       | 由smap转换成的XML文件              |
| TransportOrder | 业务订单   | 机器人执行的订单                   |
| DriverOrder    | 订单子任务 | 订单中的每一个单步任务             |
| Property       | 元属性     | 自定义属性                         |
| Vehicle        | 机器人     | 场景中的所有类型机器人统称         |
| OrderSequence  | 订单序列   | 多个业务订单可以组合成一个订单序列 |
| Point          | 节点       | 节点是地标点和停靠点的统称         |
| Halt   Point   | 地标点     | 标识为灰色圆点                     |
| Park   Point   | 停靠点     | 标识为蓝色圆点                     |

### 11.3 快捷键

| 操作               | 键                |
| ------------------ | ----------------- |
| 新建场景           | Ctrl   + N        |
| 导入场景           | Ctrl   + L        |
| 保存场景           | Ctrl   + S        |
| 场景另存为         | Ctrl   + Shift +S |
| 导入Kernel场景     | Alt   + K         |
| 将场景同步到Kernel | Alt   + P         |
| 派遣所有机器人     | Alt   +D          |
| 编辑模式           | Alt   + M         |
| 操作模式           | Alt   + O         |

### 11.4 修订历史

| 文件版本 | 发布时间 | 更新描述 | 软件版本      |
| -------- | -------- | -------- | ------------- |
|          |          |          | RoboRoute_1.0 |

### 11.5 Web API 链接

TODO

### 11.6 FAQ 链接

TODO

### 11.7 联系我们

网站: [*www.seer-robotics.com*](http://www.seer-robotics.com/)

地址: 上海市浦东新区金桥镇金领之都7号楼203室

邮箱: [*contact@seer-robotics.com*](mailto:contact@seer-robotics.com)

技术支持: [*support@seer-robotics.com*](mailto:support@seer-robotics.com)

商务合作: [*zhangsui@seer-robotics.com*](mailto:zhangsui@seer-robotics.com)

技术咨询: [*yys@seer-robotics.com*](mailto:yys@seer-robotics.com)

电话: 400-061-6660 / 086-021-61112205

### 11.8 版权声明

本手册会定期进行检查和修正，更新后的内容将出现在新版本中。本手册中的内容或信息如有变更，恕不另行通知。

安装、使用产品前请阅读本手册。

请保管好本手册，以便随时阅读与参考。

本手册所记载的内容，不排除有错误或遗漏的可能性，如对本手册中的内容有疑问，请与我司[*联系*](mailto:support@seer-robotics.com)。

 

 Seer Robotics 和 仙知 为上海仙知机器人科技有限公司的注册商标。

 

上海仙知机器人科技有限公司对 RoboRoute 软件保留所有权利。

 

上海仙知机器人科技有限公司对本文档内容保留所有权利，请勿重制或分发此文档。

 

Copyright © 2015 – 2018 Seer Robotics Co.，Ltd.