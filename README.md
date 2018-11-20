# Git 
</br>
# 1. Comparing Workflows
Git Workflow是一種採取高效率且一致性的方式來完成工作，Git在用戶管理方面提供了很大的方便和靈活性，由於沒有一個關於Git交互管理的標準化流程，所以可以針對工作選擇使用適合的Git Workflow。首次推出Git Workflow的概念是在2010由Vincent Driessen分享的A successful Git branching model，且備受大家推崇。 Workflow不會添加超出功能分支(branch)工作時所需的任何新概念或命令。相反，它在不同的分支上皆有各自的特色，並定義它們應該如何以及在何時進行交互管理。
</br>
# Example
讓我們舉一個典型的小團隊如何使用此工作流程進行協作的示例。我們將看到兩位開發人員John和Mary如何處理不同的功能並通過集中存儲庫共享他們的貢獻。</br>
John開發他負責的功能</br>
![image](https://github.com/ITE03050654/Git-/blob/master/john.PNG)

John可以在自己(local)的repo裡，開發功能，並且可以多次的編輯、提交，而不用擔心會影響到已發布的版本或是中央的repo。</br>
</br>
Mary開發他負責的功能</br>
![image](https://github.com/ITE03050654/Git-/blob/master/mary.PNG)
Mary可以和John一樣在本地工作，並且不需要擔心John跟中央的repo，因為所有本地(local)的repo都是私有的。</br>
![image](https://github.com/ITE03050654/Git-/blob/master/john_push.PNG)
</br>
John完成他的工作並且上傳到中央的repo
</br>
![image](https://github.com/ITE03050654/Git-/blob/master/mary_push_error.PNG)
</br>
Mary也完成她的工作，並且想上傳，但是因為John已經先行上傳了，所以Mary必須pull origin的檔案，並與她自己的功能合併，然後再上傳一次。這可以防止覆蓋掉官方的版本
</br>
![image](https://github.com/ITE03050654/Git-/blob/master/rebase_code.PNG)
</br>
但是在pull的時候必須使用--rebase，雖然一般的pull一樣可以把中央repo裡的資料拉下來，但每當有人需要與中央repo同步時，你會遇到多餘的“合併提交”。對於此Workflow，最好還是重新生成而不是生成合併提交。
</br>
![image](https://github.com/ITE03050654/Git-/blob/master/rebase.PNG)
而--rebase會讓Mary從中央repo上pull下來的資料在原本資料的最前端在建立一個git的版本控制，也就是將John的提交紀錄放在Mary本地資料的最前端，而在rebase的過程中如果遇到衝突而暫停，Mary只需要自己排除衝突就好，不需要John的幫助，而在解決問題可以使用git status來查看問題的所在，並在解決後在git上輸入</br>
![image](https://github.com/ITE03050654/Git-/blob/master/rebase_continue.PNG)
</br>
接著Mary只要在push就可以把自己完成的功能也上傳到中央repo了
</br>
# 2. A successful Git branching model
原文 https://nvie.com/posts/a-successful-git-branching-model/</br>
![image](https://github.com/ITE03050654/Git-/blob/master/git_model.PNG)</br>



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
上面是git請你提交一個內容來解釋為什麼這種合併是合理的</br>https://github.com/ITE03050654/Git-/blob/master/feature.png
解決辦法:</br>
1.按i進入insert模式，修改黃色合併訊息(可不修改)</br>
2.按esc，輸入:wq(儲存)</br>
一般的merge(右圖)無法像merge --no -ff一樣保存著修改的訊息，必須先手動查詢log，再撤銷Feature再比對前面的案例</br>
![image](https://github.com/ITE03050654/Git-/blob/master/feature.png)
</br>
# Release分支
Release分支也是由develop分出來，最後必須merge回develop和master兩個主支。</br></br>
命名慣例: release-* </br></br>
release分支是為了生產新版本做預備。也允許開發者對產品做最後的潤色(They allow for last-minute dotting of i’s and crossing t’s.)。另外release分支也可以用來修復依些小bug，和即將發布版本的元數據(版本號、建構日期等)，通過此分支develop分支將被清除，並接受新的大版本。release分支基本上就是反應develop對新版本的期望。</br>
由develop分出一個release分支，假設當前版本是1.15，並確定下個版本是1.2，所以分出來的release分支以1.2來取名。</br>
![image](https://github.com/ITE03050654/Git-/blob/master/create_release.PNG)</br>
创建并切换到新分支后，我们 bump 了版本号。在这里，bump-version.sh 是一个虚拟出来的 shell 脚本，用来修改一些文件，使其能体现新版本。之后，新的版本被 commit 上去。</br>
release可能會存在一段時間，這段期間可能會在此分支上修正一些bug(而不是在develop上做修正)，並且嚴禁在該分支上添加大的 feature。release最後會被合併到develop和master裡，並等待下個大版本。</br></br>
合併到develop和master裡</br>
![image](https://github.com/ITE03050654/Git-/blob/master/release_merge.PNG)
</br>
![image](https://github.com/ITE03050654/Git-/blob/master/release_merge_develop.PNG)
</br>
而這些合併可以能會造成程式碼的衝突，解決衝突後再提交</br>
完成合併後release分支就可以刪除了</br>
![image](https://github.com/ITE03050654/Git-/blob/master/delect_release.PNG)
</br>
# Hotfix 分支
Hotfix分支也是由master分出來，最後必須merge回develop和master兩個主支。</br></br>
命名慣例: hotfix-* </br></br>
hotfix分支非常類似於Release分支，因為它們也可用於準備新的生產版本，儘管是計劃外的。它們源於必須立即修正master上發布版本的不良狀態。當必須立即解決發布版本中的嚴重錯誤時，可以從發布版本版本的主分支上的相應標記(mark)修補程序分支。</br>
![image](https://github.com/ITE03050654/Git-/blob/master/hotfix.png)
</br>
從master建立Hotfix分支</br>
![image](https://github.com/ITE03050654/Git-/blob/master/create_hotfix.PNG)
</br>
解決bug後合併至master和develop，以確保下個版本不會出現同樣的bug，並利用git tag標記版本號</br>
![image](https://github.com/ITE03050654/Git-/blob/master/hotfix_merge_master.PNG)
</br>
![image](https://github.com/ITE03050654/Git-/blob/master/hotfix_merge_develop.PNG)
</br>
最後刪除hotfix分支</br>
![image](https://github.com/ITE03050654/Git-/blob/master/delect_hotfix.PNG)
</br>
</br>
# 3.git原理</br>
當你在git init時，git會在目標資料夾內建立一個樹狀的資料夾</br>
![image](https://github.com/ITE03050654/Git-/blob/master/tree.PNG)
</br>
而.git/Objects下面一開始是空的，但你commit之後資料就會儲存一些文件和子目錄在該資料夾下面</br>
![image](https://github.com/ITE03050654/Git-/blob/master/tree_after.PNG)
</br>
</br>
git會為每個Object產生40個字元和(SHA-1)，前兩個字元當作目錄名稱，後面38個當作檔案名稱，包括git add 時產生的快照。</br>
![image](https://github.com/ITE03050654/Git-/blob/master/git_add.PNG)
</br>
↑為add之後會有blob Object分別指向的兩個檔案。</br>
</br>
當git commit後會有一個tree Object指向兩個blob Object來建立兩個blob的關聯性</br>
![image](https://github.com/ITE03050654/Git-/blob/master/tree_blob.PNG)
</br>
</br>
最後git會再創造一個commit Object來指向tree Object</br>
![image](https://github.com/ITE03050654/Git-/blob/master/tree_up.PNG)
</br>
</br>
假設5a92c1修改了檔案並加入暫存區(新增 //some code magic)，這裡可以看到git已經為他新增了快照(以便commit)</br>
![image](https://github.com/ITE03050654/Git-/blob/master/new_index_add.PNG)
</br>
</br>
commit之後會再出現一個新的tree Object指向新的blob Object，另一個blob Object沒變所以同樣指向同一個地方</br>
![image](https://github.com/ITE03050654/Git-/blob/master/new_index_commit.PNG)
</br>
</br>
最後會再產生一個commit Object同時指向前一個的commit Object和現在的tree Object</br>
![image](https://github.com/ITE03050654/Git-/blob/master/new_index_up.PNG)
</br>
</br>
所以現在我們知道git如何處理文件添加和編輯，唯一剩下的就是看它如何處理文件刪除：</br>
![image](https://github.com/ITE03050654/Git-/blob/master/new_index_delect.PNG) 
</br>
</br>
直接刪除tree Object的文件條目，讓tree Object不再指向它



