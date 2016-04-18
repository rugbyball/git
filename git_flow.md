### 安裝 git-flow ###
sudo apt-get install git-flow  

### 在進行 git flow init 以前，要先將所有 commit 完成 ###
git flow init  
git add --all  
git commit -m "merge to Neil's branch"  
git push -u origin master  

### 初始化 git-flow ###
git flow init  
git branch  

### 建立 feature (不可有空格，可以 _ 取代空格) ###
git flow feature start "add change log"  
git flow feature start "add_change_log"  

### 完成 feature, merge 回 develop branch ###
git branch  
touch CHANGELOG.md  
git flow feature finish add_change_log  
git branch  
