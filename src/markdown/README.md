# 练习
* gitFlow工作流

    - 说明：gitFlow 使用两个分支来记录项目开发的历史

        - `[main]` ：被视为稳定分支 新版本打tag
        - `[develop]` : 用于集成各种功能开发的分支
        - `[feature]` : 新功能开发 基于develop分支创建
        - `[release]` : 预发布分支 基于feature分支创建 进行发布前bug修复、文档生成和其他面向发布任务 完成后合并 main、develop分支
        - `[hotfix]`  : 热更 基于main分支创建 用于修改项目遗留BUG修复并同步main、develop分支
        

* git tag

    - 说明：记录标签格式（x,y,z）正整数

        - `[x]` : 主版本号（不兼容改动 例如：重构、改版）
        - `[y]` : 次版本号（新增功能及需求变动）
        - `[z]` : 修订号（bug修复）
        

* Git Commit 提交规范（基于angular）

    - 说明：统一团队Git Commit日志标准，便于后续代码 review 和版本发布进行bug修复、文档生成和其他面向发布任务 完成后合并 main、develop分支

        - 提交信息格式 :
            - `<type>(<scope>):<subject>`
            - 空一行
            - `<body>`
            - 空一行
            - `<footer> `

            - 其中，header是必须的，body和footer可以省略 不管是哪一个部分，任何一行不超过72个字符（或100个字符）

            * `[Header]` : 部分只有一行，包括三个字段：type（必需）、scope（可选）和subject（必需）
                - `[type]` :
                    - `[feat]` ：新功能
                    - `[fix]`  ：修复BUG
                    - `[docs]` ：修改文档、比如README
                    - `[style]`：修改空格、缩进、逗号、样式等，不改变逻辑
                    - `[refactor]` ：代码重构，没有附加新功能或修复BUG
                    - `[text]` ：测试用例，包括单元测试，集成测试
                    - `[chore]` ：改变构建流程，或者增加依赖库、工具
                    - `[revert]` ：回滚到某个版本
                    - `[perf]` ：优化相关，性能提升、体验
                    

                - `[scope]` : 用于说明 commit 影响的范围，比如数据层、控制层、视图层等等，视项目不同而不同

                - `[subject]` : 用于是 commit 目的的简短描述，不超过50个字符 以动词开头,首字母小写,末尾不要标点 (ps:可写中文~~~)

            * `[body]` : 是对本次 commit 的详细描述，可以分成多行

            * `[footer]` : 如果当前代码与上一个版本不兼容，则 Footer 部分以BREAKING CHANGE开头，后面是对变动的描述、以及变动理由和迁移方法。
                - BREAKING CHANGE:xxxxxxx
                    - before:
                        xxxxx

                    - after:
                        xxxxx

        - 案例：
            - 新增一条 Commit 记录
                - git commit -m 'docs(README.md): 修改文档 新增Git Commit 提交规范'
            

            - 搜索跟README.md 文件相关的历史记录
                - git log HEAD --grep docs(README.md)
        

    
