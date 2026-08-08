# Spring 实战 (第 6 版) 中文翻译

> ⚠️ **项目已完结，不再更新**

本项目是《Spring in Action (6th Edition)》的社区中文翻译，基于 Manning 出版社的 MEAP 版本。

**强烈推荐购买正版：** https://www.manning.com/books/spring-in-action-sixth-edition

---

## 项目历程

- **2021年**：启动翻译，基于 MEAP v7 版本
- **2022年1月**：收到人民邮电出版社编辑邮件，要求关闭项目（版权原因）
- **2022年1月28日**：项目正式关闭
- **2025年8月**：使用 AI 对全部 18 章翻译质量进行优化，修复错别字、重复字、术语不一致、生硬直译等问题

## 翻译内容

共 **18 章**，全部完成：

| 章节 | 中文标题 |
| :--- | :--- |
| 1 | Spring 入门 |
| 2 | 开发 Web 应用程序 |
| 3 | 处理数据 |
| 4 | 处理非关系型数据 |
| 5 | Spring 安全 |
| 6 | 使用配置属性 |
| 7 | 创建 REST 服务 |
| 8 | 保护 REST 服务 |
| 9 | 发送异步消息 |
| 10 | 集成 Spring |
| 11 | Reactor 介绍 |
| 12 | 开发响应式 API |
| 13 | 响应式持久化数据 |
| 14 | 使用 RSocket |
| 15 | 使用 Spring Boot Actuator |
| 16 | 管理 Spring |
| 17 | 使用 JMX 监控 Spring |
| 18 | 部署 Spring |

## 项目结构

```
spring-in-action-v6-translate/
├── cn-translate/                    # 中文翻译
│   ├── Chapter-01/ ~ Chapter-18/    # 各章节
│   ├── assets/                      # 书中图片
│   ├── SUMMARY.md                   # 目录
│   └── Welcome.md
├── Spring_in_Action_Sixth_Edition_v7.pdf   # 原版 PDF
└── spring-in-action-v6-source-code.zip     # 源代码
```

## 翻译规范

- 读者称谓统一使用 **`您`**
- 代码块标注语言类型（`java`、`yaml`、`xml`、`bash`）
- 图片引用路径指向 `cn-translate/assets/`

## AI 优化记录

2025年8月，使用 AI 对全部翻译进行了质量优化，主要包括：

| 优化类型 | 示例 |
|---------|------|
| 错别字修复 | Subcriber→Subscriber、Actuaotr→Actuator |
| 重复字修复 | 的的、被被、在在 等 |
| 术语统一 | 依赖项注入→依赖注入、你→您、web→Web |
| 生硬直译 | Chapter-11 整章重写 |
| 语序优化 | 多处调整为自然中文表达 |

共修改 **36 个文件**，涵盖全部 18 章。

## 相关项目

- 《云原生 Spring 实战》翻译：https://github.com/LeonLi0102/cloud-native-spring-in-action-translate

## 免责声明

本翻译仅供学习交流使用，请支持正版图书。

---

*项目始于 2021，终于 2025。感谢所有贡献者。*
