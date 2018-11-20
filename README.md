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
![image](https://github.com/ITE03050654/Git-/blob/master/master%26develop.png)
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
![image](https://github.com/ITE03050654/Git-/blob/master/create_feature_from_develop.PNG)
</br>
將已經開發完的功能合併到develop</br>
![image](https://github.com/ITE03050654/Git-/blob/master/Feature_merge_develop.PNG)
</br>
刪除原本的Feature</br>
![image](https://github.com/ITE03050654/Git-/blob/master/delect_feature.PNG)
</br>
合併Feature可能會遇到的問題</br>
![image](https://github.com/ITE03050654/Git-/blob/master/merge_problem.PNG)
</br>
上面是git請你提交一個內容來解釋為什麼這種合併是合理的</br>
解決辦法:</br>
1.按i進入insert模式，修改黃色合併訊息(可不修改)</br>
2.按esc，輸入:wq(儲存)</br>
一般的merge(右圖)無法像merge --no -ff一樣保存著修改的訊息，必須先手動查詢log，再撤銷Feature再比對前面的案例</br>
//
</br>
# Release分支</br>
Release分支也是由develop分出來，最後必須merge回develop和master兩個主支。</br>
命名慣例: release-* </br>
release分支是為了生產新版本做預備。也允許開發者對產品做最後的潤色(They allow for last-minute dotting of i’s and crossing t’s.)。另外release分支也可以用來修復依些小bug，和即將發布版本的元數據(版本號、建構日期等)，通過此分支develop分支將被清除，並接受新的大版本。release分支基本上就是反應develop對新版本的期望。</br>
由develop分出一個release分支，假設當前版本是1.15，並確定下個版本是1.2，所以分出來的release分支以1.2來取名。</br>
//建立release的分支圖片</br>
创建并切换到新分支后，我们 bump 了版本号。在这里，bump-version.sh 是一个虚拟出来的 shell 脚本，用来修改一些文件，使其能体现新版本。之后，新的版本被 commit 上去。</br>
release可能會存在一段時間，這段期間可能會在此分支上修正一些bug(而不是在develop上做修正)，並且嚴禁在該分支上添加大的 feature。release最後會被合併到develop和master裡，並等待下個大版本。</br></br>
合併到develop和master裡</br>
//合併到develop和master裡
</br>
而這些合併可以能會造成程式碼的衝突，解決衝突後再提交</br>
完成合併後release分支就可以刪除了</br>
//完成合併後release分支就可以刪除了
</br>
# Hotfix 分支</br>
Hotfix分支也是由master分出來，最後必須merge回develop和master兩個主支。</br>
命名慣例: hotfix-* </br>
hotfix分支非常類似於Release分支，因為它們也可用於準備新的生產版本，儘管是計劃外的。它們源於必須立即修正master上發布版本的不良狀態。當必須立即解決發布版本中的嚴重錯誤時，可以從發布版本版本的主分支上的相應標記(mark)修補程序分支。</br>


