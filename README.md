# Git

# 1. A successful Git branching model
原文 https://nvie.com/posts/a-successful-git-branching-model/
![image](https://github.com/ITE03050654/Git-/blob/master/git_model.PNG)

 A successful Git branching model 是作者  gitflow 在所2010年所撰寫的，是一篇關於git分支(branch)的使用方法和心得。
 
 # 主要分支
 1.master</br></br>
 2.develop
 
master/origin作為主要分支的其中之一，它的head永遠指向一個可以發布的狀態（production-ready state)。</br></br>
develop/origin為另一個主要分支，其head永遠指向下一版最新發布的改動。</br>
</br>
當develop開發到一個穩定且可以發布的狀態，應該把所有的改動合併(merge)到master分支上並標記版本號，所以每次合併到master上面，就會生成一個可以發布的新版本，每當master上有commit時，可以利用git hook的腳本自動建立並推送到伺服器(master/origin)。</br></br>

# 輔助分支
在主分支外我們會利用很多輔助分支來幫助團隊並行開發、預備新的發布，協助快速修復已經發布的版本，與主要分支不同的是這些輔助分支生命只有有限的生命，最終會被移除。</br></br>
我們可以能會用到的輔助分支有三種
1.Feature 分支</br>
2.Release 分支</br>
3.Hotfix 分支</br>
