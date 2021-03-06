# Research On Multi-AGV Path Planning For Logictics Sorting Based On CBS Algorithm

## 1.摘要
  * 互联网+以及工业4.0
  * 两种基于CBS算法改进的并行算法:PCBS与它的增强型EPCBS。并行算法通过登记正在扩展的节点的代价值使得并行算法可以有条件选取扩展节点，最终求得问题的近似最优解；利用随机化的冲突选择策略，让结点之间找到解的概率尽可能相互独立，使得并行算法带来实质上的效率提升
  * 在其中加入了对环境中执行任务的Agent数量变化的考虑，针对该问题，本文基于CBS提出了一个增量搜索算法的LPCBS来求，并证明了其最优性。增量搜索通过复用CBS前一次搜索过程中产生的约束树实现了给“新到达”Agent规划路径的同时快速调整“在途中”Agent的路径。
  * 同时在LPCBS中，给出了CBS中约束树的一种新的实现，该实现节省了搜索过程中所需要的内存
  * Li等人为了使单个AGV路径更平滑，基于A\*算法改进，引入转弯因子，是的求出路径达到实际需求的最优，转弯次数最少
  * Su等人提出了最短时间路径规划的模型，同样基于A\*算法改进，求出节点无冲突、时间最短的路径，对多AGV而言，提出一种算法解决可能发生的边冲突
  * 在物流仓储环境中，对AGV而言，环境可能是半已知的，在行走过程中遇到障碍物，这时已经规划的路线就行不通，需要重新规划，杨璐等人提出了一种动态修正路径的A\*算法，使得算法可以利用已有信息，快速调整路径到新的最优解
  * Tai等人使用A\*算法作为离线的路径规划算法，在线安排时间窗时通过考虑冲突发生的所有情形动态地给AGV分配优先级进行时间窗重排得到无冲突的多AGV路径
  * Zheng等人在蚁群算法中引入反向学习法，结合粒子群算法调整蚁群算法中信息素的值，给多个AGV规划路径，最后利用博弈论构建动态避障模型解决AGV之间的冲突
  * 焦红艳将AGV运行场景栅格化之后，对场景建立了人工势场模型，结合一般冲突消解的办法给多个AGV规划平滑无冲突的路径
  * Liu等人在遗传算法的变异过程中引入启发式信息加大了每一轮迭代产生更好的解的几率，同时结合模拟退火算法加强了遗传算法的局部搜索能力
  * 苑光明等人为了AGV路径更平滑，在编码染色体时引入了转弯因素，同时改进了遗传算法，通过每一代动态的调整交叉、变异概率使得算法有了更快的收敛速度
  * Ryosuke等人利用遗传算法优化了固定导轨的路网设计，提高了零件加工的效率
  * Peihuang等人通过遗传算法给AGV生成若干条离线路径，然后再用在线的遗传算法给多个AGV分配真实路径，使得AGV之间无冲突且能按给定的任意速度移动
  * Davide将无人仓储中的多AGV路径规划问题建模成了一个颜色Petri网模型，利用Petri网的调度能力，成功给多个AGV规划了无冲突的路径，并进行了仿真实验
  * Zheng等人将无人仓储环境划分为多个区间，利用改进的Dijkstra算法离线生成多条候选路径，然后通过在线算法对多AGV路径进行时间窗的安排解决路径之间的冲突

## 2.MAPF
  * MAPF问题已经被证明为NP-Complete
  * 一般的MAPF求解器可以分为集中式求解器和分布式求解器
  * 一类集中式的求解器将MAPF问题进一步建模，规约到另一种可以用标准求解器求解的问题
    * Yu 等人将 MAPF 问题规约到一个多商品流的整数规划（Integer Linear Programing，ILP）问题，基于不同的优化目标对问题进行了求得了最优解，并提出了一种启发式方法将问题分解为多个并行的整数规划求解使得求解速度更高效而不是求得最优解
    * Surynek 等人将 MAPF 问题规约到另一类标准问题——可满足性问题（Satisfiability Problem，SAP），并针对最小化完成时间和最小化路径代价和这两个优化目标分别进行了求解
  * 另一类集中式MAPF求解器是基于搜索的，最基本的搜索类求解器就是A\*算法了，A\*在求解MAPF问题的时候会发生状态空间的爆炸，不适应Agent数目多、场景大的问题
    * Standly等人提出了操作分解符(Operation Deconposition，OD)的方法和独立性检测方法(Independent Dectection，OD)
    * OD引入了中间状态和最终状态的概念，大大减少了A\*的分支因子，缓解了A\*的状态空间爆炸的问题，但是增加了算法的搜索深度，仍然无法适应大规模问题的求解
    * ID可以将一个大的MAPF问题分解为小的MAPF问题，提高求解效率
    * 增强的部分扩展A\*算法(Enhanced Patial-Expantion A\*, EPEA\*)是另一种A\*算法的改进，它的前身是用来求解单个Agent路径规划的PEA\*算法，它大大减少了搜索时所占用的内存，展示出了求解多Agent路劲规划的能力
    * M\*是一种基于A\*算法的改进，针对多Agent路径规划问题，动态的减少搜索维度，算法搜索时的分支因子随着冲突的增加而增加，能成功求解冲突概率不高的MAPF问题
  * Sharon等人提出了增加代价树搜索(Increasing Cost Tree Search, ICTS)算法和基于冲突的搜索(Conflict-Based Search, CBS)算法，是近几年专门用于求解MAPF问题的两种算法，他们都是二级搜索算法，算法的搜索分为上下两层
    * ICTS上层给每个Agent的路径代价分配一个值，下层搜索负责找到一个解使得每个Agent的路径代价等于上次指定的值
    * CBS算法下层搜索把MAPF问题视为多个单Agent路径规划问题，单Agent路径规划问题能在很短的时间内得到解；上层算法用来找到多个Agent路径之间的冲突，通过分裂节点的方式在下层搜索中添加约束条件解决发现的冲突，CBS在大地图、Agent路径耦合度不高的场景下展现出了优秀的求解效率
    * 基于CBS的搜索框架，改进的CBS(Improved Conflict-Based Search, ICBS)提出了主要冲突、半主要冲突、以及非主要冲突的概念，通过优先解决主要冲突以及半主要冲突加快了CBS的求解速度
    * 基于CBS主要冲突的概念，Felner等人在CBS上层的搜索加入启发式信息，从而将上层搜索从无信息的搜索变成了A\*搜索，进一步加快了CBS搜索速度
    * Barer等人基于CBS，在上下层搜索中将最优搜索改为了聚焦搜索(Focus Search)，得到增强型CBS算法(Enhanced Conflict-Based Search, ECBS)，可以求得具有可控近似比的MAPF问题的近似解，聚焦搜索充分利用了上层接之间的冲突信息，使下层更容易避免冲突
    * Cohen等人在MAPF问题的原始图中引入了高速路，在高速路上Agent智能单向行驶，改进后的算法下层搜索类似加权A\*算法，该算法也可以求得MAPF问题的近似解
  * 分布式求解器通常是近似最优的，这个领域一个杰出的算法是层次的协调A\*算法(Hierachy Cooperative A\*, HCA\*)，HCA\*被广泛应用到游戏以及工业控制领域。HCA\*通过一个个求解Agent的路径，使得已求得的Agent的路径上的点在时空图上为不可通过的障碍物，以此为基础进行下一个Agent的求解，HCA\*算法具有很高的求解效率，但是算法不具备完整性
    * HangMa等人提出了两种分布式算法，Token传递算法(Token Passing, TP)和Token传递和任务交换(Token Passing with Task Swaps)算法，这两种算法通过一块内存空间的共享进行协调，内存中可以发现其他Agent路径以便于下一个Agent路径规划
    * 另一种分布式求解器不是基于搜索的，而是基于规则定义的，Luna等人提出了Agent在移动时的两种规则，Push和Swap，
    
## 3.多Agent路径规划问题模型
  * A\*算法是启发式搜索算法的先驱:
    * g(n)表示从起始状态S到状态N的观测代价
    * h(n)表示从状态N到目标状态G的估计代价
    * A\*算法使用OPEN来存放待探测的状态，每次从OPEN中选出一个f值最小的进行扩展，将后继状态添加到OPEN中去，而将扩展过的状态标记为CLOSED
    * 每一个状态是一个m元组，代表m个Agent的状态；在4-连通的网格内，每个Agent可以采取的行动的数量为b=5，则对于任意一种状态的扩展得到的后继状态可能有m·b种，即A\*算法呈现指数级增长m，带来状态空间爆炸
  * CBS通过分层搜索的手段，解决了直接在原始状态空间搜索的状态空间爆炸的问题
  
### 3.1.基于冲突的搜索算法

## 4.多Agent路径规划解决方案
  * 并行基于冲突的搜索算法PCBS，增强型基于冲突的搜索ECBS，从而得到EPCBS
  * 生命期的基于冲突的搜索算法LPCBS
  
### 4.1.并行的基于冲突的搜素算法
  * 假设：CBS算法中OPEN中的每一个节点的解有效的概率p是一个常数，节点直接相互独立
  
### 4.2.增强并行基于冲突的搜索算法
  * ECBS之所以可以求得近似最优解，来源于它在CBS搜索框架的上下层采用聚焦搜索(Focus Search)技术。
  * CBS算法在扩展节点时，若发现节点的解有冲突，则会依据冲突创建两个子节点，并对这两个子节点添加新的约束条件用底层搜索重新规划，重新规划的路径是依据新的约束条件下的最优解。这种算法具有一定的盲目性，仅仅是处理了已经发现的“看得见”的冲突，因此解的路径有可能再次与解中的其他Agent路径发生冲突
  * 在搜索时只考虑现有约束而忽略了其他Agent的路径，基于这样一个事实，在知道其他Agent的路径上的所有位置的情况下，下层单Agent路径规划搜索算法可以把这一点作为启发式信息，在搜索过程中就尽量避免与其他路径发生冲突
  * 采用聚焦搜索策略，A\*在待扩展节点的一个子集中选出一个更不容易发生冲突的节点，从而减轻CBS上层搜索解决冲突的负担
  * ECBS下层使用聚焦搜索的A\*算法
  * 引入评价函数h(s)，表示状态s上发生冲突的Agent个数
  * 引入评价函数H(N)，表示N.Solution中发生冲突的元素的个数
  
### 4.3.动态多Agent路径规划问题与求解
  * 静态问题假设所有的Agent是同时出发的，而动态问题区分Agent是“在途中”，即A中的Agent，还是“新到达”，即A'中的Agent。
  * 在已有一批规划好路径的Agent基础上给另一批Agent规划路径
  * 我们需要算法可以在给A'中的Agent规划的同时有必要的调整A中Agent的路径
  
### 4.4.增量搜索：生命期的基于冲突的搜索算法
  * 每次规划的搜索过程都是基于上一次搜索时产生的信息的搜索，即为增量搜索
  * 相关性：如果两个约束，它们对应着相同的元素和时间，但是对应不同的Agent，那么我们说这两个约束是相关的
  * 时间一致性：N.SOlution(ts) = li(ts)，扩展一个时间一致的约束树节点得到的两个子节点仍然是时间一致的
  * LPCBS的基本思想是，保存给A规划路径中产生的约束树，在下一次给A'规划路径时基于该约束树继续搜索，节省了重新给A规划路径的时间
  * 过期节点，即节点N是时间不一致的
  * 过期约束，当A'在ts时刻到达，对于OPEN中的任意一个节点的任意一个约束c=(ai, s, t)，t<ts，我们称这个约束为过期约束
  * 当前问题：正在任意一个时刻，环境的状态反应着所有Agent在该时刻的位置，我们把当前时刻ts所有Agent从当前位置l(ts)到目的位置di构成的一个静态问题称之为当前问题
  * **消除时间不一致的节点的算法**
  * **清理过期约束的算法**
  * **LPCBS算法**
  
## 5.实验结果分析
    

  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
