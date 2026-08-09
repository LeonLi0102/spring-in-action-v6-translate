# Spring 实战 (第 6 版) 中文翻译

![](cn-translate/assets/cover.png)

> ⚠️ **项目已完结，不再更新**

本项目是《Spring in Action (6th Edition)》的社区中文翻译，基于 Manning 出版社的**正式版本**。

**强烈推荐购买正版：** https://www.manning.com/books/spring-in-action-sixth-edition

---

## 项目历程

- **2021年**：启动翻译，基于 MEAP 版本
- **2022年1月**：收到人民邮电出版社编辑邮件，要求关闭项目（版权原因）
- **2022年1月28日**：项目正式关闭
- **2026年8月**：使用 AI 对全部 18 章翻译质量进行优化，修复错别字、重复字、术语不一致、生硬直译等问题
- **2026年8月**：基于正式版 PDF 校验，修正章节结构差异，补翻附录

## 翻译内容

共 **18 章 + 附录**，全部完成：

| 部分 | 章节 | 中文标题 |
| :--- | :--- | :--- |
| **Part 1: 基础 Spring** | 1 | Spring 入门 |
| | 2 | 开发 Web 应用程序 |
| | 3 | 处理数据 |
| | 4 | 处理非关系型数据 |
| | 5 | Spring 安全 |
| | 6 | 使用配置属性 |
| **Part 2: 集成 Spring** | 7 | 创建 REST 服务 |
| | 8 | 保护 REST 服务 |
| | 9 | 发送异步消息 |
| | 10 | 集成 Spring |
| **Part 3: 响应式 Spring** | 11 | Reactor 介绍 |
| | 12 | 开发响应式 API |
| | 13 | 响应式持久化数据 |
| | 14 | 使用 RSocket |
| **Part 4: 部署 Spring** | 15 | 使用 Spring Boot Actuator |
| | 16 | 管理 Spring |
| | 17 | 使用 JMX 监控 Spring |
| | 18 | 部署 Spring |
| **附录** | A | 引导 Spring 应用程序 |

## 项目结构

```
spring-in-action-v6-translate/
├── cn-translate/                    # 中文翻译
│   ├── Chapter-01/ ~ Chapter-18/    # 各章节
│   ├── Appendix/                    # 附录
│   ├── assets/                      # 书中图片
│   ├── SUMMARY.md                   # 目录
│   └── README.md
├── raw/                             # 提取的原文
├── Spring_in_Action_Sixth_Edition.pdf       # 正式版 PDF
├── Spring_in_Action_Sixth_Edition_v7.pdf    # MEAP 版 PDF
└── spring-in-action-v6-source-code.zip      # 源代码
```

## 翻译规范

- 读者称谓统一使用 **`您`**
- 代码块标注语言类型（`java`、`yaml`、`xml`、`bash`）
- 图片引用路径指向 `cn-translate/assets/`
- 中英文之间添加空格（如 `Spring Boot` 而不是 `SpringBoot`）

## 质量检查

翻译完成后，进行了全面的质量检查：

| 检查项 | 状态 |
|--------|------|
| 内容完整性 | ✅ 每章行数合理（500-1400行） |
| 术语一致性 | ✅ 关键术语统一 |
| 重复字检查 | ✅ 无重复字 |
| 常见错字 | ✅ 无"其它"等错字 |
| 中英文空格 | ✅ 全部规范 |
| 代码块闭合 | ✅ 全部正确 |
| 图片引用 | ✅ 路径正确 |
| 章节结构 | ✅ 与正式版一致 |

## AI 优化记录

2026年8月，使用 AI 对全部翻译进行了质量优化，主要包括：

| 优化类型 | 示例 |
|---------|------|
| 错别字修复 | Subcriber→Subscriber、Actuaotr→Actuator |
| 重复字修复 | 的的、被被、在在 等 |
| 术语统一 | 依赖项注入→依赖注入、你→您、web→Web |
| 生硬直译 | Chapter-11 整章重写 |
| 语序优化 | 多处调整为自然中文表达 |

共修改 **36+ 个文件**，涵盖全部 18 章 + 附录。

## 在线阅读

**GitBook：** https://leonli0102.github.io/spring-in-action-v6/

## 相关项目

- 《云原生 Spring 实战》翻译：https://github.com/LeonLi0102/cloud-native-spring-in-action-translate

## 免责声明

本翻译仅供学习交流使用，请支持正版图书。

---

*项目始于 2021，终于 2026。感谢所有贡献者。*
