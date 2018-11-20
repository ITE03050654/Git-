# Git

# 1. A successful Git branching model
原文 https://nvie.com/posts/a-successful-git-branching-model/
![image](https://github.com/ITE03050654/Git-/blob/master/git_model.PNG)

 A successful Git branching model 是作者  gitflow 在所2010年所撰寫的，是一篇關於git分支(branch)的使用方法和心得
 
 # 主要分支
 1.master</br>
 2.develop
 
master/origin作為主要分支的其中之一，它的head永遠指向一個可以發布的狀態（production-ready state)</br>
develop/origin為另一個主要分支，其head永遠指向下一版最新發布的改動</br>
</br>
當develop開發到一個穩定且可以發布的狀態，應該把所有的改動合併(merge)到master分支上並標記版本號</br>
所以每次合併到master上面，就會生成一個可以發布的新版本，每當master上有commit時，可以利用git hook的腳本自動建立並推送到伺服器(master/origin)

