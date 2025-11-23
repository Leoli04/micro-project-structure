# micro-project-structure

这个项目是关于在搭建微服务的时候，如何处理项目结构

## 三种项目结构

### micro-one-module

这种是最简单的方式，和原来的单体结构类似，调用方根据swagger接口，自己定义远程调用的服务以及接口

### micro-two-module

这种是增加了一个契约包，调用方在使用的时候通过依赖契约包的方式调用

### micro-multi-module

这种结构复杂一些，类似六边形架构，结构更清晰。

> 六边形架构（Hexagonal Architecture） —— 也叫 端口与适配器架构（Ports and Adapters）



| 六边形概念                          | 对应模块/代码                     | 说明                                                         |
| ----------------------------------- | --------------------------------- | ------------------------------------------------------------ |
| **应用核心（Inside Hexagon）**      | `micro-core`                      | 包含实体、领域服务、**端口接口（Port）**                     |
| **输入端口（Primary Port）**        | `micro-contract`、`micro-service` | “别人怎么调我？”（如注册、查询用户）                         |
| **输出端口（Secondary Port）**      | `micro-core`中的repository包      | “我需要什么外部能力？”（如缓存、搜索）                       |
| **输入适配器（Primary Adapter）**   | `micro-service`                   | 将 HTTP/Feign 请求转换为对核心的调用                         |
| **输出适配器（Secondary Adapter）** | `micro-infra`                     | 实现端口接口，对接 Redis、ES、Kafka 等                       |
| **外部契约（API）**                 | `micro-contract`                  | 定义对外接口规范（DTO + Feign Client），属于输入适配器的一部分 |
