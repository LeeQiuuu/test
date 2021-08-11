## Git常用命令



# Git常用命令

[TOC]

## 修订历史记录

| 日期     | 版本 | 说明     | 作者   |
| -------- | ---- | -------- | ------ |
| 2020/7/1 | V1.0 | 初始版本 | 李治健 |
|          |      |          |        |
|          |      |          |        |

------

## 初始化本地仓库（远程仓库克隆）

$$ 适用于远程仓库已创建好仓库，且本地没有创建本地仓库，将远程仓库直接克隆到本地。 $$

- 克隆mater主分支

  ```
  git clone [url]
  例：git clone http://172.16.0.101:3000/jmax/jmq_app_android.git
  ```

- 克隆master分支某个提交

  ```
  git checkout -b branchname <commitId>
  
  例：git checkout -b master e4e7330eebf291324c60a31cc2ead4ea60c1b70e
  ```

------

## 初始化本地仓库（完全初始化重建模式）

$$ 适用于远程仓库已创建好仓库，且本地没有创建本地仓库，先创建本地仓库，之后再将远程仓库进行关联。 $$

- 初始化Git仓库

  ```
  git init
  ```

- 关联远程仓库

  ```
  git remote add origin http://172.16.0.101:3000/jmax/jmq_app_android.git
  ```

- 同步远程仓库

  master为Git远程仓库的主分支，仓库可能有多个分支，比如开发dev，测试test；如果需要拉哪个分支，则写对应的名称，后面的命令同理。

  ```
  git pull
  或
  git pull origin master
  ```

- 添加本地文件

  添加本地文件，注意最后是一个点，意思是将你本地修改了的文件添加到暂存区：

  ```
  git add .
  ```

- 提交日志信息

  ```
  git commit -m “首次提交”
  ```

- 推送至远程仓库

  ```
  git push
  或
  git push origin master
  ```

- ~~强推至远程仓库(禁用)~~

  ```
  git push origin HEAD --force
  ```

## 更换仓库地址

```
git remote set-url origin [url]
```

------

## 拉取所有分支

```
git branch -r | grep -v '\->' | while read remote; do git branch --track "${remote#origin/}" "$remote"; done
git fetch --all
git pull --all
```

------

## 强制拉取并覆盖本地代码

```
git fetch --all
git reset --hard origin/master
git pull
```

## 修改本地仓库关联的远程仓库地址

- 查看仓库关联的地址

  ```
  git remote -v
  ```

- 切换地址

  ```
  git remote set-url origin [url]
  ```

## 代码回撤

- 未提交至远程仓库的回撤

  ```
  git reset --soft HEAD^
  ```

  > --soft 不删除工作空间的改动代码 ，撤销commit，不撤销 git add file
  >
  > --hard 删除工作空间的改动代码，撤销commit且撤销add
  >
  > HEAD^ 表示上一个版本，即上一次的commit，可写成HEAD~1，1标识commit的次数；

- 撤销远程仓库代码

  ```
  git reset --hard HEAD^
  
  git push origin master --force
  ```

- 没有commit的回撤，即操作了add

  ```
  git reset HEAD^
  ```

- 回退某个文件到工作区

  ```
  git reset head filename 或 git reset filename
  ```

- 修改提交的commit注释

  ```
  git commit --amend
  ```

## 修改用户名和邮箱

- 修改名称：git config user.name "username"
- 修改邮箱：git config user.email "email"
- 全局修改名称：git config --global user.name "username"
- 全局修改邮箱：git config --global user.email "email"

## 添加Tag标签

$$ Tag的意义在于对不同时期的代码进行版本区分及进行标记，方便后期维护及查找代码。 $$

- 添加本地标签

  ```
  git tag 1.0.0
  ```

- 提交标签

  ```
  git push --tag
  ```

- 删除本地标签

  ```
  git tag -d 1.0.0
  ```

- 删除远程标签

  ```
  git push origin :refs/tags/1.0.0
  ```

------

## 切换分支

- 查看所有分支

  ```
  git branch -a	
  ```

- 捡出分支 checkout远程的dev分支，在本地起名为dev分支，并切换到本地的dev分支：

  ```
  git checkout -b dev origin/dev
  ```

- 切回分支 切换回dev分支，并开始开发：

  ```
  git checkout dev
  ```

------

## 子分支同步Master

```
git checkout master
git pull
git checkout dev
git merge master
若有冲突：解决冲突之后： git add & git commit 
git push dev
```

## 子分支合并到Master（现有分支）

```
git checkout dev
git add .
git commit -m "..."
git checkout master
git merge dev
若有冲突：解决冲突之后：git add & git commit
git push
```

------

## 合并分支(创建临时分支)

- 创建临时分支 将master分支作为temp分支：

  ```
  git fetch origin master:temp
  ```

- 切换分支

  ```
  git branch temp
  ```

- 将temp分支和本地分支合并

  ```
  git merge temp
  ```

- 删除分支（禁用）

  ```
  git branch -d temp
  ```

------

## 撤销本地提交

- 查看本地提交信息

  ```
  git show
  ```

- 撤销某次提交(仅取消Commit信息，不还原代码，软撤销)

  ```
   git reset --soft HEAD^ 
   或 
   git reset --soft HEAD~1		//1表示撤销几次，如果是2则会连续撤销2次commit
  ```

- 撤销某次提交(不仅取消Commit信息，而且还原代码，硬撤销)

  ```
  git reset --hard HEAD^
  ```

- 回到到某个提交

  ```
   git reset --hard commit_id		// commit_id为对应commit的sha码
  ```

- 修改提交信息

  ```
  git commit --amend
  ```

------

## 支持大于50/100M文件上传

git config http.postBuffer 524288000 git config -l

------

## 取消文件跟踪

- 取消某个文件的跟踪(不删除本地文件) git rm --cached file_name.txt
- ~~取消某个文件的跟踪(删除本地文件，禁用)~~ git rm --f file_name.txt
- 取消所有文件的跟踪(不删除本地文件) git rm -r --cached .
- ~~取消所有文件的跟踪(删除本地文件，禁用)~~ git rm -r –f .

------

## Git老仓库迁移至新仓库

- 使用git remote set-url origin [url]切换远程仓库；
- 查看本地关联的地址：git remote -v，如果仓库地址没有切换，直接编辑.git/config中的url换成新仓库地址；
- 推本地代码送新的远程仓库：git push -u origin master；
- 如果出现错误，忽略及同步远程仓库历史关联：git pull origin master --allow-unrelated-histories
- 再次：git push -u origin master

------

## SVN仓库迁移至Git仓库

- 提交本地代码并推送至SVN仓库；

- 在SVN本地仓库同级目录(即.svn隐藏文件夹同目录)下，新建GitProject文件夹，执行以下命令(svn仓库地址需要更换成对应SVN远程仓库的地址)，里面的对应个人SVN账号：

  ```
  svn log 远程SVN仓库地址 -q | awk -F '|' '/^r/ {sub("^ ", "", $2); sub(" $", "", $2); print $2"="$2" <"$2"@iconcox.com>"}' | sort -u > ./users.txt
  ```

- 编辑user.txt，把=后面的姓名改成对应的名称(即=号后面的名称需要换成git账号名称)，比如`lizhijian=lizhijian<lizhijian@jimilab.com>`，修改成`lizhijian=zhijian.li<lizhijian@jimilab.com>`

- 执行拷贝svn代码命令：

  ```
  git svn clone 远程SVN仓库地址 --no-metadata --authors-file=users.txt GitProject
  ```

- 新建或拷贝忽略文件配置文件.gitignore在GitProjec下(若是新建文件，则需要写如忽略文件配置中的配置内容)；

- 进入GitProject文件夹，执行推送命令：

  ```
  git push -u origin master
  ```

- 若提示推送失败，执行忽略Git仓库历史记录命令，之后再执行第5步：

  ```
  git pull origin master --allow-unrelated-histories
  ```

------

## 游离合并

```
git branch temp
git checkout master	//master为当前开发分支，若为dev则改为dev，下面同样
git merge temp
git status
git push origin master
git branch -d temp
```

------

## 多子仓库模式拉取及提交

- 初始化克隆仓库(递归的方式克隆整个项目)

  ```
  git clone <repository> --recursive
  ```

- 添加子模块

  ```
  git submodule add <repository> <仓库存放本地的path>
  ```

- 初始化子模块

  ```
  git submodule init
  ```

- 更新子模块

  ```
  git submodule update
  ```

- 拉取所有子模块

  ```
  git submodule foreach git pull
  或
  git submodule foreach git pull origin master
  ```

- 推送所有子模块

  ```
  git submodule foreach git push origin master
  ```

- 删除子模块

  - 删除.gitsubmodule里相关部分；
  - 删除.git/config 文件里相关字段；
  - 删除子仓库目录；<https://github.com/JimiPlatform/JMSmartFTPUtils.git>
  - 执行：git rm --cached <本地路径>

## 移除大文件之后无法Push的问题

```
git filter-branch --force --index-filter 'git rm -rf --cached --ignore-unmatch JimiVideoPlayer_iOS/JimiVideoPlayer_iOS/JimiVideoPlayer/Lib/FFmpeg-iOS/lib.zip' --prune-empty --tag-name-filter cat -- --all
```

------

## .gitignore忽略文件配置

$$ .gitignore是Git对整个仓库文件需要忽略上传的一个配置文件，默认每个仓库都应该具备。配置可以为如下内容（已包含Xcode、AS、RN的需要忽略的文件） $$

```
# Xcode
#
# gitignore contributors: remember to update Global/Xcode.gitignore, Objective-C.gitignore & Swift.gitignore

## User settings
xcuserdata/

## compatibility with Xcode 8 and earlier (ignoring not required starting Xcode 9)
*.xcscmblueprint
*.xccheckout

## compatibility with Xcode 3 and earlier (ignoring not required starting Xcode 4)
build/
DerivedData/
*.moved-aside
*.pbxuser
!default.pbxuser
*.mode1v3
!default.mode1v3
*.mode2v3
!default.mode2v3
*.perspectivev3
!default.perspectivev3
*.xcuserstate

## Obj-C/Swift specific
*.hmap

## App packaging
*.ipa
*.dSYM.zip
*.dSYM

# CocoaPods
#
# We recommend against adding the Pods directory to your .gitignore. However
# you should judge for yourself, the pros and cons are mentioned at:
# https://guides.cocoapods.org/using/using-cocoapods.html#should-i-check-the-pods-directory-into-source-control
#
Pods/
Podfile.lock
*.xcworkspace

# Carthage
#
# Add this line if you want to avoid checking in source code from Carthage dependencies.
Carthage/Checkouts

Carthage/Build/

# fastlane
#
# It is recommended to not store the screenshots in the git repo.
# Instead, use fastlane to re-generate the screenshots whenever they are needed.
# For more information about the recommended setup visit:
# https://docs.fastlane.tools/best-practices/source-control/#source-control

fastlane/report.xml
fastlane/Preview.html
fastlane/screenshots/**/*.png
fastlane/test_output

# Code Injection
#
# After new code Injection tools there's a generated folder /iOSInjectionProject
# https://github.com/johnno1962/injectionforxcode

iOSInjectionProject/
.DS_Store
*/.DS_Store

# Xcode
#
# gitignore contributors: remember to update Global/Xcode.gitignore, Objective-C.gitignore & Swift.gitignore

## User settings
xcuserdata/

## compatibility with Xcode 8 and earlier (ignoring not required starting Xcode 9)
*.xcscmblueprint
*.xccheckout

## Obj-C/Swift specific
*.hmap

## App packaging
*.ipa
*.dSYM.zip
*.dSYM

## Playgrounds
timeline.xctimeline
playground.xcworkspace

# Swift Package Manager
#
# Add this line if you want to avoid checking in source code from Swift Package Manager dependencies.
Packages/
Package.pins
Package.resolved
#
# Xcode automatically generates this directory with a .xcworkspacedata file and xcuserdata
# hence it is not needed unless you have added a package configuration file to your project
.swiftpm

.build/
iOSInjectionProject/
.DS_Store

# Built application files
*.apk
*.aar
*.ap_
*.aab

# Files for the ART/Dalvik VM
*.dex

# Java class files
*.class

# Generated files
bin/
gen/
out/
#  Uncomment the following line in case you need and you don't have the release build type files in your app
# release/

# Gradle files
.gradle/
build/

# Local configuration file (sdk path, etc)
local.properties

# Proguard folder generated by Eclipse
proguard/

# Log Files
*.log

# Android Studio Navigation editor temp files
.navigation/

# Android Studio captures folder
captures/

# IntelliJ
*.iml
.idea/
.idea/workspace.xml
.idea/tasks.xml
.idea/gradle.xml
.idea/assetWizardSettings.xml
.idea/dictionaries
.idea/libraries
# Android Studio 3 in .gitignore file.
.idea/caches
.idea/modules.xml
# Comment next line if keeping position of elements in Navigation Editor is relevant for you
.idea/navEditor.xml

# Keystore files
# Uncomment the following lines if you do not want to check your keystore files in.
#*.jks
#*.keystore

# External native build folder generated in Android Studio 2.2 and later
.externalNativeBuild
.cxx/

# Google Services (e.g. APIs or Firebase)
# google-services.json

# Freeline
freeline.py
freeline/
freeline_project_description.json

# fastlane
fastlane/report.xml
fastlane/Preview.html
fastlane/screenshots
fastlane/test_output
fastlane/readme.md

# Version control
vcs.xml

# lint
lint/intermediates/
lint/generated/
lint/outputs/
lint/tmp/
# lint/reports/

# Other
libs_export/
.DS_Store
*/.DS_Store

node_modules
yarn.lock
bundles
yarn-error.log
*.jsbundle
.DS_Store
*/.DS_Store
```