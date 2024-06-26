# 第四阶段（最终阶段）报告

> ——programming-team-X-C-X  真是难取名队

## 实现的附加任务

> 本阶段及先前阶段均**完整记录了更新日志**，可以在仓库中查阅。
>
> 项目仓库地址：`https://github.com/programming-team-X-C-X/Surakarta-private`
>
> **所有功能均在第四阶段deadline之前完成**，之后仅进行了代码结构的修改优化、debug工作

1. 完善**AI**，采用 `minmax` 算法与 `alpha-beta` 剪枝
2. 实现移动棋子时的**动画**（包括绕外棋线）
3. 在重现对局中实现 `播放`,`暂停`,`上一步`,`下一步`,`到第_步` 等功能。
4. 重播对局时可以随时**介入**进行不一样的尝试，尝试后也可以还原并继续播放
5. 实现结束后客户端发送 `READY_OP` 表示准备再来一局
6. AI **线程**和图形界面线程独立，AI 托管可以随时关闭
7. AI **进度条**：在游戏界面显示正在计算的AI进度条，保证这个进度条线性增长
8. **多游戏模式**，接入本地AI，实现与电脑对战，增加游戏性

## 具体实现方法与分工

以下简介我们附加功能的实现方法。

由于大家均为从0开始学习Qt和项目的搭建，因此在分工中，我们根据各自对于项目的熟悉程度，各取所长，进行诸多功能的开发。

**本阶段的完成离不开小组中每一个人的努力。**

#### 完善AI

> 向禹、常皓飞

向禹完成 `minmax` 算法与剪枝的基本设计，常皓飞将其接入项目。

#### 棋子动画

> 常皓飞

**我们在第二阶段就已经实现了动画**，在先前的报告中进行了较为详细的解释，主要难点在于对棋子移动路径的合理记录，需要弃用 `Qpainter`，在此不过多赘述。

#### 重现对局

>肖俊皓

会对对局进行按`A1-A2`格式的记录，在重现对局时会通过此得到对应的所有的移动步，存储在`moves`中，同时记录下每一步对应的棋盘界面，存储在`boards`中。要重现对局只需加载对应步数的棋盘即可。

#### 再来一局

> 肖俊皓

在客户端游戏结束后会直接像服务端发送`leave_op`，并且弹出对应的结束框，点击再来一局之后，会关闭游戏窗口，并且跳转到联机的窗口，此时会保留之前的用户信息，可以再次点击准备进行再来一局。若点击返回主菜单则会直接返回到游戏的主窗口。

#### AI线程独立

> 常皓飞

采用多线程，将 `agent` 的计算移动到单独的线程 `aiThread` ，防止堵塞界面。

#### AI进度条

> 常皓飞

采用估算方式，利用AI第一层的搜索估算整体的情况数，这是一个比较快的过程；在每一次搜索到底并达到阈值之后更新progress。

经过验证，在大多数时间和情况下，都能够实现比较精确的估算。

## 遇到的问题与解决

1. 在与多线程的设计过程中，经常出现内存等一些细微的问题，debug需要大量耐心。
2. 最开始我们更多注重功能实现，并不注重类的结构与代码质量；最后提交之前，我们尽己所能对项目的代码结构进行了优化。

## 当前其他进度

最终阶段，已经没有其他任务了。

#### 我们通过点亮 `star` 表达对助教师兄工作与付出的衷心感谢！