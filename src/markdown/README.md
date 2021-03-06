# 练习
* gitFlow工作流

    - 说明：gitFlow 使用两个分支来记录项目开发的历史

        - `[main]` ：被视为稳定分支 新版本打tag

        - `[develop]` : 用于集成各种功能开发的分支

        - `[feature]` : 新功能开发 基于develop分支创建

        - `[release]` : 预发布分支 基于feature分支创建 进行发布前bug修复、文档生成和其他面向发布任务 完成后合并 main、develop分支

        - `[hotfix]`  : 热更 基于main分支创建 用于修改项目遗留BUG修复并同步main、develop分支

        

        

* Git Commit 提交规范（基于angular）

    - 说明：统一团队Git Commit日志标准，便于后续代码 review 和版本发布进行bug修复、文档生成和其他面向发布任务 完成后合并 main、develop分支

        - 提交类型限制：
            - `[feat]` ：新功能
            - `[fix]`  ：修复BUG
            - `[docs]` ：修改文档、比如README
            - `[style]`：修改空格、缩进、逗号、样式等，不改变逻辑
            - `[refactor]` ：代码重构，没有附加新功能或修复BUG
            - `[text]` ：测试用例，包括单元测试，集成测试
            - `[chore]` ：改变构建流程，或者增加依赖库、工具
            - `[revert]` ：回滚到某个版本
            - `[perf]` ：优化相关，性能提升、体验

        - 提交信息格式
            - 标题 : 首字母不大写 末尾不要标点
            - 主题内容 ：正常描述
            

        - 案例：
            - 新增一条 Commit 记录
                - git commit -m 'docs(README.md): 修改文档 新增Git Commit 提交规范'
            

            - 搜索跟README.md 文件相关的历史记录
                - git log HEAD --grep docs(README.md)

        

    
