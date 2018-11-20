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
//主支圖片
# 輔助分支
在主分支外我們會利用很多輔助分支來幫助團隊並行開發、預備新的發布，協助快速修復已經發布的版本，與主要分支不同的是這些輔助分支生命只有有限的生命，最終會被移除。</br></br>
我們可以能會用到的輔助分支有三種</br>
1.Feature 分支</br>
2.Release 分支</br>
3.Hotfix 分支</br>
</br>
# Feature 分支
Feature是從develop分支分出來的，最後也得合併回develop分支，命名並沒有特別的要求，分支命名除了 master , develop , release_* 和 hotfix-* 以外皆可任意命名。</br>
剛開始開發的時候，Feature的功能可能還不知道，但只要功能處於開發階段Feature分支就會存在，最後會合併回develop分支(以便將新的功能新增到即將發布的版本上)或被丟棄(開發的結果令人失望)。</br>
Feature通常只存在開發者的repo裡，而不會origin repo裡。</br></br>
從develop上建立一個feature分支來開發新功能</br>
//創建feature
</br>
將已經開發完的功能合併到develop</br>
//合併feature
</br>
刪除原本的Feature</br>
//刪除
</br>
合併Feature可能會遇到的問題</br>
//合併問題
</br>
上面是git請你提交一個內容來解釋為什麼這種合併是合理的</br>
解決辦法:</br>
1.按i進入insert模式，修改黃色合併訊息(可不修改)</br>
2.按esc，輸入:wq(儲存)</br>
