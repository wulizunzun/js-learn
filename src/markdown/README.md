# 练习

- gitFlow工作流

    - 说明：gitFlow 使用两个分支来记录项目开发的历史

    - `[master]` ：被视为稳定分支 
        - 用于打标签发布版本号
        - bug修复基于此分支 创建hotfix进行修改 完成则合并master、develop分支 然后新版本打tag

    - `[develop]` : 用于集成各种功能开发的分支
        - 功能开发完成后，在此分支创建release分支进行bug修复、文档生成和其他面向发布任务 完成后合并 master、develop分支
        
    
