# fish-redux 的演进史

fish-redux 是一个不断演进的框架，甚至是在不断的回炉重造，在这个过程中

<img src="https://img.alicdn.com/tfs/TB1aeJELpzqK1RjSZFCXXbbxVXa-1794-938.png" width="897px" height="469px">

-   1. 第一个版本是基于社区内的 flutter_redux 进行的改造，核心是提供了 UI 代码的组件化，当然问题也非常明显，针对复杂的业务场景，往往业务逻辑很多，无法做到逻辑代码的分治和复用。

-   2. 第二个版本针对第一个版本的问题，做出了比较重大的修改，解决了 UI 代码和逻辑代码的分治问题，但设计上打破了 redux 的原则，丢失了 Redux 的精华。

-   3. 在第三个版本进行重构时，我们确立了整体的架构原则与分层要求，一方面按照 reduxjs 的代码进行了 flutter 侧的 redux 实现，将 redux 完整保留下来。另一方面针对组件化的问题，提供了 redux 之上的 component 的封装，并创新的通过这一层的架构设计提供了业务代码分治的能力。第三版 完成了 Redux， Component 两层的设计，其中包含了 Connector，Dependencies，Context 等重要概念。

    -   3.1 解决集中和分治的矛盾的核心在于 [Connector](what's-connector.md)
    -   3.2 这一层的组件的分治是面向通用设计的。通过在 [Dependencies](dependencies-cn.md) 配置 slots，得到了可插拔的组件系统。

-   4. 在第三个版本 Redux & Component 之外，提供了面向 ListView 场景的分治设计 Adapter。
    -   4.1 解决 "Big-Cell" 问题
        > 以假设的一个业务场景为例，其中有个"Big-Cell":留言（有非常多行）。如果我们将"留言"以 Component 形态来组装，就会使得"留言"成为一个非常巨大的 Widget，极大影响整体的 FPS。所以我们需要将这个"留言"拆的更细一点。
        > 两种方式
        >
        > 1. 将每一行都拆解为一个 Component
        >    我们将得到性能的提升，但是这样的拆分下，每一行的 Component 仅仅有展示的能力而失去了大部分的逻辑的能力，主要的"留言"的逻辑部分都会上升到 ListView 本身，导致"留言"失去了做为独立模块纯在的能力。
        > 2. 将"留言"这个"Big-Cell"
    -   4.2 解决逻辑的独立性
        > 以闲鱼的详情业务场景为例，其中有两个"Big-Cell":留言和推荐。如果我们将留言和推荐以 Component 形态来组装，就会使得留言和推荐成为两个非常巨大的 Widget，极大的影响了页面的 FPS。
    -   4.3
        > 以闲鱼的详情业务场景为例，其中有两个"Big-Cell":留言和推荐。如果我们将留言和推荐以 Component 形态来组装，就会使得留言和推荐成为两个非常巨大的 Widget，极大的影响了页面的 FPS。

> 目前，fish redux 已经在闲鱼线上稳定运行，未来，期待 fish redux 给社区带来更多的输入。
