# Idea设置方式
## Deault Settings（默认全局设置）

## 

# Idea常用设置
## 默认设置
### 设置本地MAVEN仓库的默认位置
> Idea的默认的本地MAVEN仓库是在C:\Users\${用户名}\.m2\repository目录下，但是大家一般不习惯放C盘，那就需要修改默认的设置 

进入如下设置路径
`Deault Settings-Appearence & Behavior-Path Varibles`
修改其中的MAVEN_REPOSITORY为你所需的路径
如
`E:\Dev\maven_repository`

------------
### 修改默认的MAVEN settings 文件路径
进入如下设置路径
`Deault Settings-Build, Execution, Deployment-Build Tools-Maven`
修改其中的
`User settings file:`
为我们真实的路径，如
`E:\Dev\apache-maven-3.5.2\conf\settings.xml`
