# Git

## 版本控制系統 Git 精要
- Ref : http://ihower.tw/git/


/******************************************************************************/
開始 - 初次設定Git
/******************************************************************************/
初次設定Git
現在讀者的系統已安裝了Git，讀者可能想要做一些客製化的動作。 讀者應只需要做這些工作一次。 這些設定在更新版本時會被保留下來。 
讀者可藉由再度執行命令的方式再度修改這些設定。

Git附帶名為git config的工具，允許讀者取得及設定組態參數，可用來決定Git外觀及運作。 

這些參數可存放在以下三個地方：
檔案 /etc/gitconfig： 
    包含給該系統所有使用者的儲存庫使用的數值。 只要讀者傳遞 --system 參數給 git config，它就會讀取或者寫入參數到這個檔案
檔案 ~/.gitconfig： 
    給讀者自己的帳號使用。 傳遞 --global 參數給 git config，它就會讀取或者寫入參數到這個檔案。
儲存庫內的設定檔，也就是 .git/config： 
    僅給所在的儲存庫使用。 每個階級的設定會覆寫上一層的。 因此，git/config內的設定值的優先權高過/etc/config。
在Windows系統，Git在$HOME目錄(對大部份使用者來說是C:\Documents and Settings\$USER)內尋找.gitconfig。 
它也會尋找/etc/gitconfig，只不過它是相對於Msys根目錄，取決於讀者當初在Windows系統執行Git的安裝程式時安裝的目的地。

設定識別資料
讀者安裝Git後首先應該做的事是指定使用者名稱及電子郵件帳號。 這一點非常重要，因為每次Git提交會使用這些資訊，而且提交後不能再被修改：

$ git config --global user.name "John Doe"
$ git config --global user.email johndoe@example.com
再說一次，若讀者有指定 --global 參數，只需要做這工作一次。 因為在此系統，不論Git做任何事都會採用此資訊。 
若讀者想指定不同的名字或電子郵件給特定的專案， 只需要在該專案目錄內執行此命令，並確定未加上 --global 參數。

指定編輯器
現在讀者的識別資料已設定完畢，讀者可設定預設的文書編輯器，當Git需要讀者輸入訊息時會叫用它。 
預設情況下，Git會使用系統預設的編輯器，一般來說是Vi或Vim。 若讀者想指定不同的編輯器，例如：Emacs。可執行下列指令：

$ git config --global core.editor emacs
指定合併工具
另外一個對讀者來說有用的選項是設定解決合併失敗時，讀者慣用的合併工具。 假設讀者想使用vimdiff：

$ git config --global merge.tool vimdiff
Git能接受kdiff3、tkdiff、meld、xxdiff、emerge、vimdiff、gvimdiff、ecmerge及opendiff做為合併工具。 讀者可設定自訂的工具。 詳情參考第七章。

檢查讀者的設定
若讀者想確認設定值，可使用 git config --list 命令列出所有Git能找到的設定值：
$ git config --list
user.name=Scott Chacon
user.email=schacon@gmail.com
color.status=auto
color.branch=auto
color.interactive=auto
color.diff=auto
...
讀者可能會看到同一個設定名稱出現多次，因為Git從不同的檔案讀到同一個設定名稱（例如：/etc/gitconfig及~/.gitconfig）。 在這情況下，Git會使用最後一個設定名稱的設定值。

使用者也可以下列命令 git config 設定名稱，檢視Git認為該設定名稱的設定值：
$ git config user.name
Scott Chacon


/******************************************************************************/
Git 初學筆記 - 指令操作教學             from: http://blog.longwin.com.tw/2009/05/git-learn-initial-command-2009/
/******************************************************************************/
Git 是分散式的版本控制系統, 從架設、簡易操作、設定, 此篇主要是整理 基本操作、遠端操作 等.

註: Git 的範圍太廣了, 把這篇當作是初學入門就好了. 
注意事項
由 project/.git/config 可知: (若有更多, 亦可由此得知)
origin(remote) 是 Repository 的版本
master(branch) 是 local 端, 正在修改的版本

平常沒事不要去動到 origin, 如果動到, 可用 git reset --hard 回覆到沒修改的狀態.

Git 新增檔案
git add . # 將資料先暫存到 staging area, add 之後再新增的資料, 於此次 commit 不會含在裡面.
git add filename
git add modify-file # 修改過的檔案, 也要 add. (不然 commit 要加上 -a 的參數)
git add -u # 只加修改過的檔案, 新增的檔案不加入.
git add -i # 進入互動模式

Git 刪除檔案
git rm filename

Git 修改檔名、搬移目錄
git mv filename new-filename

Git status 看目前的狀態
git status # 看目前檔案的狀態

Git Commit
git commit
git commit -m 'commit message'
git commit -a -m 'commit -message' # 將所有修改過得檔案都 commit, 但是 新增的檔案 還是得要先 add.
git commit -a -v # -v 可以看到檔案哪些內容有被更改, -a 把所有修改的檔案都 commit

Git 產生新的 branch
git branch # 列出目前有多少 branch
git branch new-branch # 產生新的 branch (名稱: new-branch), 若沒有特別指定, 會由目前所在的 branch / master 直接複製一份.
git branch new-branch master # 由 master 產生新的 branch(new-branch)
git branch new-branch v1 # 由 tag(v1) 產生新的 branch(new-branch)
git branch -d new-branch # 刪除 new-branch
git branch -D new-branch # 強制刪除 new-branch
git checkout -b new-branch test # 產生新的 branch, 並同時切換過去 new-branch
# 與 remote repository 有關
git branch -r # 列出所有 Repository branch
git branch -a # 列出所有 branch

Git checkout 切換 branch
git checkout branch-name # 切換到 branch-name
git checkout master # 切換到 master
git checkout -b new-branch master # 從 master 建立新的 new-branch, 並同時切換過去 new-branch
git checkout -b newbranch # 由現在的環境為基礎, 建立新的 branch
git checkout -b newbranch origin # 於 origin 的基礎, 建立新的 branch
git checkout filename # 還原檔案到 Repository 狀態
git checkout HEAD . # 將所有檔案都 checkout 出來(最後一次 commit 的版本), 注意, 若有修改的檔案都會被還原到上一版. (git checkout -f 亦可)
git checkout xxxx . # 將所有檔案都 checkout 出來(xxxx commit 的版本, xxxx 是 commit 的編號前四碼), 注意, 若有修改的檔案都會被還原到上一版.
git checkout -- * # 恢復到上一次 Commit 的狀態(* 改成檔名, 就可以只恢復那個檔案)

Git diff
git diff master # 與 Master 有哪些資料不同
git diff --cached # 比較 staging area 跟本來的 Repository
git diff tag1 tag2 # tag1, 與 tag2 的 diff
git diff tag1:file1 tag2:file2 # tag1, 與 tag2 的 file1, file2 的 diff
git diff # 比較 目前位置 與 staging area
git diff --cached # 比較 staging area 與 Repository 差異
git diff HEAD # 比較目前位置 與 Repository 差別
git diff new-branch # 比較目前位置 與 branch(new-branch) 的差別
git diff --stat

Git Tag
git tag v1 ebff # log 是 commit ebff810c461ad1924fc422fd1d01db23d858773b 的內容, 設定簡短好記得 Tag: v1
git tag 中文 ebff # tag 也可以下中文, 任何文字都可以
git tag -d 中文 # 把 tag=中文 刪掉

Git log
git log # 將所有 log 秀出
git log --all # 秀出所有的 log (含 branch)
git log -p # 將所有 log 和修改過得檔案內容列出
git log -p filename # 將此檔案的 commit log 和 修改檔案內容差異部份列出
git log --name-only # 列出此次 log 有哪些檔案被修改
git log --stat --summary # 查每個版本間的更動檔案和行數
git log filename # 這個檔案的所有 log
git log directory # 這個目錄的所有 log
git log -S'foo()' # log 裡面有 foo() 這字串的.
git log --no-merges # 不要秀出 merge 的 log
git log --since="2 weeks ago" # 最後這 2週的 log
git log --pretty=oneline # 秀 log 的方式
git log --pretty=short # 秀 log 的方式
git log --pretty=format:'%h was %an, %ar, message: %s'
git log --pretty=format:'%h : %s' --graph # 會有簡單的文字圖形化, 分支等.
git log --pretty=format:'%h : %s' --topo-order --graph # 依照主分支排序
git log --pretty=format:'%h : %s' --date-order --graph # 依照時間排序

Git show
git show ebff # 查 log 是 commit ebff810c461ad1924fc422fd1d01db23d858773b 的內容
git show v1 # 查 tag:v1 的修改內容
git show v1:test.txt # 查 tag:v1 的 test.txt 檔案修改內容
git show HEAD # 此版本修改的資料
git show HEAD^ # 前一版修改的資料
git show HEAD^^ # 前前一版修改的資料
git show HEAD~4 # 前前前前一版修改的資料

Git reset 還原
git reset --hard HEAD # 還原到最前面
git reset --hard HEAD~3
git reset --soft HEAD~3
git reset HEAD filename # 從 staging area 狀態回到 unstaging 或 untracked (檔案內容並不會改變)

Git grep
git grep "te" v1 # 查 v1 是否有 "te" 的字串
git grep "te" # 查現在版本是否有 "te" 的字串

Git stash 暫存
git stash # 丟進暫存區
git stash list # 列出所有暫存區的資料
git stash pop # 取出最新的一筆, 並移除.
git stash apply # 取出最新的一筆 stash 暫存資料. 但是 stash 資料不移除
git stash clear # 把 stash 都清掉

Git merge 合併
git merge
git merge master
git merge new-branch
下述轉載自: ihower 的 Git 版本控制系統(2) 開 branch 分支和操作遠端 repo.x
    Straight merge 預設的合併模式，會有全部的被合併的 branch commits 記錄加上一個 merge-commit，看線圖會有兩條 Parents 線，並保留所有 commit log。
    Squashed commit 壓縮成只有一個 merge-commit，不會有被合併的 log。SVN 的 merge 即是如此。
    cherry-pick 只合併指定的 commit
    rebase 變更 branch 的分支點：找到要合併的兩個 branch 的共同的祖先，然後先只用要被 merge 的 branch 來 commit 一遍，然後再用目前 branch 再 commit 上去。
    這方式僅適合還沒分享給別人的 local branch，因為等於砍掉重練 commit log。

    指令操作
    git merge <branch_name> # 合併另一個 branch，若沒有 conflict 衝突會直接 commit。若需要解決衝突則會再多一個 commit。
    git merge --squash <branch_name> # 將另一個 branch 的 commit 合併為一筆，特別適合需要做實驗的 fixes bug 或 new feature，最後只留結果。
    合併完不會幫你先 commit。
    git cherry-pick 321d76f # 只合併特定其中一個 commit。如果要合併多個，可以加上 -n 指令就不會先幫你 commit，這樣可以多 pick幾個要合併的 commit，
    最後再 git commit 即可。

Git blame
git blame filename # 關於此檔案的所有 commit 紀錄

Git 還原已被刪除的檔案
git ls-files -d # 查看已刪除的檔案
git ls-files -d | xargs git checkout -- # 將已刪除的檔案還原

Git 維護
git gc # 整理前和整理後的差異, 可由: git count-objects 看到.
git fsck --full

Git revert 資料還原
git revert HEAD # 回到前一次 commit 的狀態
git revert HEAD^ # 回到前前一次 commit 的狀態
git reset HEAD filename # 從 staging area 狀態回到 unstaging 或 untracked (檔案內容並不會改變)
git checkout filename # 從 unstaging 狀態回到最初 Repository 的檔案(檔案內容變回修改前)

Git Rollback 還原到上一版
git reset --soft HEAD^
編輯 + git add filename
git commit -m 'rollback'

以下與 遠端 Repository 相關
Git remote 維護遠端檔案

git remote
git remote add new-branch http://git.example.com.tw/project.git # 增加遠端 Repository 的 branch(origin -> project)
git remote show # 秀出現在有多少 Repository
git remote rm new-branch # 刪掉

git branch -r # 列出所有 Repository branch
抓取 / 切換 Repository 的 branch

git fetch origin
git checkout --track -b reps-branch origin/reps-branch # 抓取 reps-branch, 並將此 branch 建立於 local 的 reps-branch
刪除 Repository 的 branch

git push origin :heads/reps-branch


/******************************************************************************/
Git 基礎工作流程
/******************************************************************************/
使用 Git 來管理版本時的基礎作業流程：
建立一個共享的版本庫。
將遠端主機上的版本庫複製一份至本機。
修改本機的工作複本，然後提交。
將提交的檔案推送至遠端主機的版本庫。

以下是範例：
1. 建立一個共享的版本庫
cd d:/GitRepos/Projects/MyProjectA
git init --bare

2. 將遠端主機上的版本庫複製一份至本機
git clone http://my-server:8080/Projects/MyProjectA

如果你的 Git 伺服器支援 https:// 協定，則複製版本庫的指令會類似這樣：
git clone https://my-server/Projects/MyProjectA

若以 https:// 協定複製版本庫時出現錯誤：
error: SSL certificate problem, verify that the CA cert is OK. Details:
error:14090086:SSL routines:SSL3_GET_SERVER_CERTIFICATE:certificate verify faile
d while accessing https://localhost/Projects/test/info/refs
fatal: HTTP request failed

可嘗試以下列指令解決：
git config --global http.sslverify  false

此外，你也可以在複製時直接指定帳號密碼，例如：
git clone https://michael:guesswhat@my-server/Projects/MyProjectA
如果這個「遠端主機」就是你目前工作的本機，亦即要在同一台機器上複製出另一個版本庫，則可以用 file:// 協定。例如：
git clone file://d:/GitRepos/Projects/MyProjectA
沒有加 file:// 或者寫 file:///（三個斜線）也可以。

3. 修改本機的工作複本，然後提交
git add .
git commit -m "提交時的說明文字"
此動作可能會執行許多次，端看你覺得何時要將所有已提交的檔案推送至遠端主機的版本庫。

4. 將提交的檔案推送至遠端主機的版本庫
git push origin master
其中的 push 代表要將變更推送至遠端伺服器；origin 代表此 local 版本庫在遠端伺服器的來源，你可以從 local 版本庫的 .git\config 檔案中找到這個遠端的 "origin"；最後的參數 master 則代表 master 分支。
所以上述指令的意思，以比較精確的解釋來說，就是：將本機的 master 分支的所有變更推送至遠端主機的 master 分支。
如果沒有指定 master 分支，只寫這樣：
git push origin
則表示要將本機的所有分支的變更推送至遠端主機的對應分支。
若要將本機的變更推送至遠端版本庫的其他分支，例如 feature101，就可以輸入指令：
git push origin feature101
其他開發人員如果要取得最新的檔案，可以在自己的 local 版本庫的目錄之下執行 git pull 命令。
以上大概就是最簡單、最基礎的 git 作業流程。
============
呼∼總算把所有的 Subversion 版本庫移轉成 Git 了。


/******************************************************************************/
Git 情境劇
/******************************************************************************/
這篇主要是給自己做個記錄，因為 Git 指令實在太多了…
Git 教學(1)：Git的基本使用
Git 教學(2)：Git Branch 的操作與基本工作流程
Git 情境劇：告訴你使用 Git 時什麼情況該下什麼指令

如何安裝 Git
Mac : 安裝 Homebrew : brew install git
Linux(Debian) : apt-get install git-core
Linux(Fedora) : yum install git-core
Windows : 下載安裝 msysGit

如何設定 Git
Mac : Set Up Git on Mac (https://help.github.com/articles/set-up-git/)
Linux : Set Up Git on Linux (https://help.github.com/articles/set-up-git/)
Windows : Set up Git on Windows (https://help.github.com/articles/set-up-git/)

如何開始一個 Git Respository
在專案底下
. 使用 git init 開始一個新的 Git repo.
. 使用 git clone 複製一個專案

如何將檔案加入 Stage
. 使用 git add 將想要的檔案加入 Stage.
. git add . 會將所有編修過的檔案加入 Stage (新增但還沒 Commit 過的檔案並不會加入)

如何將檔案從 Stage 中移除(取消add)
git reset HEAD 檔案名稱

如何將檔案提交(commit)
. 使用 git commit會將 Stage 狀態的檔案做 Commit 動作
. git commit -m "commit訊息" 可以略過編輯器直接輸入 commit 訊息完成提交。
. git commit -am "commit訊息" 等同於先git add .後略過編輯器提交 commit。

如何修改/取消上一次的 commit
. git commit --amend 修改上一次的 commit 訊息。
. git commit --amend 檔案1 檔案2... 將檔案1、檔案2加入上一次的 commit。
. git reset HEAD^ --soft 取消剛剛的 commit，但保留修改過的檔案。
. git reset HEAD^ --hard 取消剛剛的 commit，回到再上一次 commit的 乾淨狀態。

分支基本操作(branch)
. git branch 列出所有本地端的 branch。
. git branch -r 列出所有遠端的 branch。
. git branch -a 列出所有本地及遠端的 branch。
. git branch "branch名稱" 建立一個新的 branch。
. git checkout -b "branch名稱" 建立一個新的 branch 並切換到該 branch。
. git branch branch名稱 起始點 以起始點作為基準建立一個新的 branch，起始點可以是一個 tag，branch 或是 commit。
. git branch --track branch名稱 遠端branch 建立一個 tracking 遠端 branch 的 branch，這樣以後 push/pull都會直接對應到該遠端的branch。
. git branch --set-upstream branch 遠端branch 將一個已存在的 branch 設定成 tracking 遠端的branch。
. git branch -d "branch 名稱" 刪除 branch。
. git -r -d 遠端branch 刪除一個 tracking 的遠端 branch，例如git branch -r -d wycats/master
. git push repository名稱 :遠端branch 刪除一個 repository 的 branch，通常用在刪除遠端的 branch，例如git push origin :old_branch_to_be_deleted。
. git checkout branch名稱 切換到另一個 branch(所有修改過程會被保留)。

遠端操作(remote)
. git remote add remote名稱 remote網址 加入一個 remote repository，例如 git remote add github git://github.com/gogojimmy/test.git
. git push remote名稱 :branch名稱 刪除遠端 branch，例如 git push origin :somebranch。
. git pull remote名稱 branch名稱 下載一個遠端的 branch 併合併(注意是下載遠端的 branch 合併到目前本地端所在的 branch)。
. git push 類似於 pull 操作，將本地端的 branch 上傳到遠端。

合併操作(merge)
. git merge branch名稱 合併指定的 branch 到目前的 branch。
. git merge branch名稱 --no-commit 合併指定的 branch 到目前的 branch 但是不會產生合併的 commit。
. git cherry-pick SHA 將某一個 commit 的內容合併到目前 branch，指定 commit 是使用該 commit 的 SHA 值，例如 git cherry-pick 7300a6130d9447e18a931e898b64eefedea19544。

暫存操作(stash)
. git stash 將目前所做的修改都暫存起來。
. git stash apply 取出最新一次的暫存。
. git stash pop 取出最新一次的暫存並將他從暫存清單中移除。
. git stash list 顯示出所有的暫存清單。
. git stash clear 清除所有暫存。

常見問題：
. 我的 code 改爛了我想全部重來，我要如何快速回到乾淨的目錄?
  . git reset --hard 這指令會清除所有與最近一次 commit 不同的修改。
. merge 過程中發生 confict 我想放棄 merge，要如何取消 merge？
  . 一樣使用 git reset --hard 可以取消這次的 merge。
. 如何取消這次的 merge 回到 merge 前的狀態?
  . git reset --hard ORIG_HEAD 這指令會取消最近一次成功的 merge 以及所有你在這次 merge 後所做的修改。
. 如何回復單獨檔案到原本 commit 的狀態?
  . git checkout 檔案名稱 這指令會將已經被修改過的檔案回復到最近一次 commit 的樣子。


/******************************************************************************/
Git 教學(1) : Git 的基本使用            http://gogojimmy.net/2012/01/17/how-to-use-git-1-git-basic/
/******************************************************************************/
Git 教學(1)：Git的基本使用
Git 教學(2)：Git Branch 的操作與基本工作流程
Git 情境劇：告訴你使用 Git 時什麼情況該下什麼指令
前言
Git 是一套分散式的版本控制系統，版本控制是一個開發團隊中不可或缺的工具，Git 最強大的一個特點就是可以無窮無盡的開 branch 
(分支)，好處就是今天不論是修 Bug ，開發新功能，或是研究 feature 都非常的方便，學 Git 到現在大概三個月的時間讓我體會到
"Git 用的好，產品開發沒煩惱!!"，搭配 Github (一個以 Git 作為基礎的程式碼社群服務，上面有非常多的資源)使用更是天下無敵，
團隊開發怎麼能少的了用 Git 呢！！！！
坦白說 Git 還是需要一些時間去學習， Workflow 對於使用 Git 有非常大的影響，一個好的 Workflow 會更幫助你學會如何去操作 
Git 及培養好的團隊開發技巧，因此這篇就是要來幫助剛學習 Git 的人如何快速上手 Git 及一個開發的 Workflow ，以下是給完全沒接觸過的新手的入門文，如果你想要快速的瞭解基本操作，你可以直接看這裡。

安裝Git
網路上已經有很多教學了，善用 Google 我相信你可以找到非常多的資源，的我建議可以參考 Github 上的教學(請先建立一個 Github 的帳號，因為他會連 Github 的設定一起設定完成)：
Mac setup git
Windows setup git
Linux setup git
若你想看中文的推薦你 Git 的權威教材 Pro Git。
Git 也有很多的 GUI 工具，免費的像是 GITX、 SourceTree、SmartGit (我沒用過但是是2011評價最好的 Git GUI)，付費的像是 Tower 都是不錯的選擇，但我會建議先從基本的 Git 指令開始學習，當你對基本的指令熟悉後再去使用各種不同的 GUI 就會更加的得心應手了！

設定你的Git
在每一次的 Git commit (提交，我們稍後會提到) 都會記錄作者的訊息像是 name 及 email ，因此我們使用下面的指令來設定：
$ git config --global user.name "Jimmy Kuo"
$ git config --global user.email "jimmy@gogojimmy.net"
加上 --global 表示是全域的設定。你可以使用 git config --list 這個指令來看你的 Git 設定內容：
$ git config --list
    user.name=Jimmy Kuo
    user.email=jimmy@gogojimmy.net
或是其實 Git 的設定檔是儲存在你的家目錄的.gitconfig 隱藏檔中，你可以使用編輯器將他打開
$ cat ~/.gitconfig
    [user]
        name = Jimmy Kuo
        email = jimmy@gogojimmy.net
使用終端機來操作 Git 常會讓人覺得一直打指令很繁瑣，因此 Git 也有提供 alias 的功能，例如你可以將 git status 縮寫為 git st，git checkout 縮寫為 git co 等，你只要這樣設定：
$ git config --global alias.st status
這樣一來只要打 git st 就等同於打 git status 了。

空白對有些語言是有影響的(像是Ruby)，因此我們會希望 Git 去忽略空白的變化，這時候你需要在你的設定加入：
$ git config --global apply.whitespace nowarn
如此一來 Git 對於空白的變化便會忽略不計。

Git 預設輸出是沒有顏色的，我們可以讓他在輸出時加上顏色讓我們更容易閱讀：
$ git config --global color.ui true
開始使用Git (init, clone)

要開始使用 Git 你必須先建立一個 Git 的 Repository，你可以把它想做是一個資料庫的意思，有兩種方法可以建立一個 Git 的 Repository：

自己建立一個新的 Repository
例如我現在有個叫做 Animal 專案資料夾，我現在想要開始使用 Git 開始管理，因此我先將目錄切換到 Animal 底下後輸入git init
$ git init
Initialized empty Git repository in /Users/Jimmy/Projects/Animal/.git/
這時你就會看到 Git 告訴你說已經在這邊建立好一個新的 Git Repository。

Clone(複製)別人的 Repository
例如我們在 Github 上面看到人家的程式碼想要抓下來自己修改，或是團隊中別人的程式碼，這時候他們通常會有一個 Git 的檔案位置像是在 Github 的話你就會看到像下面的地方可以讓你複製 git 的 clone 位置：
git clone
將他複製起來後到你的目錄下輸入 git clone
$ git clone https://gogojimmy@github.com/gogojimmy/Animal.git
如此便會將這個 Git Repository下載到我們的資料夾， git clone 預設會將下載的 git 存成一樣檔名的資料夾，如果你要更改成別的名稱的話只需要在網址後面加上你想要更改的名稱即可，像是：
$ git clone https://gogojimmy@github.com/gogojimmy/Animal.git monkey
這樣子下載下來的 Repository 的名稱就會從原本的 Animal 變成 monkey 了。

Git的基本功(status, add, commit, log, .gitignore)
在一個 Git 的 Repository 中你可以輸入git status來檢查目前 Git 的狀態
$ git status
# On branch master
#
# Initial commit
#
nothing to commit (create/copy files and use "git add" to track)
這代表目前是一個乾淨的目錄狀態，沒有未被追蹤或是被修改的檔案， On branch master 表示你目前正在名為 master 的 branch 上，等等會再說明 branch 的功用。
我們現在在這個目錄新增一個 test 檔案後，再使用git status 來查看：
$ git status
# On branch master
#
# Initial commit
#
# Untracked files:
#   (use "git add ..." to include in what will be committed)
#
#   test.rb
nothing added to commit but untracked files present (use "git add" to track)
這時候你會看到我剛剛新增的 test.rb 檔案變成在 Untracked files (未被追蹤的檔案)，表示過去在這個 Git Repository 中從未有這支檔案，是一支未被追蹤的檔案，
我們要把這個檔案讓 Git 能夠追蹤的話，我們使用 git add 這個指令來把它加入追蹤：
$ git add test.rb
$ git status
# On branch master
#
# Initial commit
#
# Changes to be committed:
#   (use "git rm --cached ..." to unstage)
#
#   new file:   test.rb
#
你可以看到原本 test.rb 還在 Untracked files 中，經過我們使用 git add test.rb 後他就變成了 Changes to commit，通常我們稱這個狀態叫做 stage ，修改過但還沒使用 git add 的檔案稱為 unstage 。
Tips: 一次加入全部的檔案
如果你一次修改了很多檔案，懶得一個一個輸入 git add 的話，你可以輸入 git add . 這會幫你將所有剛剛修改過或新增加的檔案一次 Add 進 stage 狀態，
但強烈不推薦這樣的作法，這樣的方法雖然方便但很容易會不小心加入一些其他不必要的檔案，一個正確的觀念是你必須隨時都很清楚你的檔案狀態，因此最好是手動將你確定要加入的檔案使用 git add 來加入，
有一個更好的作法是使用互動模式 git add -i ，在互動模式下你可以方便的選擇你要加入的檔案，或是移除剛剛不小心加入的檔案 (revert)。

已經在 stage 狀態的檔案的下一步就是準備提交( commit )，commit 是寫程式時一個很重要的動作，一個 commit 在 Git 中就是一個節點，這些 commit 的節點就是未來你可以回朔及追蹤的參考，
你可以想像就像是電玩遊戲時的存檔，每一個 commit 就是一次存檔，讓我們未來在需要的時候都可以回到這些存檔時的狀態。因此我們將剛剛做的修改提交：
$ git commit
此時你會看到畫面跳到你在 git 中設定的編輯器畫面：
#
# Please enter the commit message for your changes. Lines starting
# with '#' will be ignored, and an empty message aborts the commit.
# On branch master
#
# Initial commit
#
# Changes to be committed:
#  (use "git rm --cached …" to unstage)
#
#       new file: test.rb
#
這個視窗中最上面的空行是要給你寫下你這次 commit 的訊息，例如在這裡寫下 "Add test.rb file to test git function" 來表示這一次提交的目的，
強烈建議在 commit 的時候要盡量清楚表達這次 commit 的內容為何，因為這會讓你未來要回頭看 code 的時候能讓你快速的找到你想要找的內容，也能對團隊中其他成員瞭解你在做什麼。

在 commit 完後會顯出出你這次 commit 的更動：
[master 5f76371] add ignore files
 2 files changed, 8 insertions(+), 0 deletions(-)
 create mode 100644 .gitignore
 create mode 100644 test.rb
如果你覺得每次這樣跳出編輯器很麻煩，你也可以在 commit 時加上 -m 的參數來快速提交：

$ git commit -m "Add test.rb to test git function"
若使用 -am 的話還能將所有未被 add 的檔案一併 add 進來( 更新：如果是第一次新增還沒有被 add 的檔案是不會一起加入的，只有之前已經被 add 過 commit 的檔案才會被加入 )，
但就像前面所說這樣的作法並不推薦，你應該清楚的加入你應該加入的檔案就好：

$ git commit -am "Add test.rb to test git function"

若使用 -v 的話會列出更動的紀錄：
# Please enter the commit message for your changes. Lines starting
# with '#' will be ignored, and an empty message aborts the commit.
# On branch master
# Changes to be committed:
#   (use "git reset HEAD ..." to unstage)
#
#   new file:   .gitignore
#   new file:   test.rb
#
diff --git a/.gitignore b/.gitignore
new file mode 100644
index 0000000..61521a9
--- /dev/null
+++ b/.gitignore
@@ -0,0 +1,3 @@
+.DS_Store
+*.swp
+log/*.log
diff --git a/test.rb b/test.rb
new file mode 100644
index 0000000..23df1c1
--- /dev/null
+++ b/test.rb
@@ -0,0 +1,5 @@
+class Test
+  def test
+    puts "This is a test file"
+  end
+end
加號(+)代表增加的部份，減號(–)代表刪除的部份。

我們可以使用 git log 的指令查看過去 commit 的紀錄：
$ git log
5f76371 - (HEAD, master) add ignore files (3 minutes ago) 
4ca268d - (origin/master) First commit (33 minutes ago) 
前面的亂碼代表的是當次 commit 的版號，後面的是 commit 的訊息、時間以及 commit的作者，你可以使用 --stat 參數看到更詳盡的訊息：

$ git log --stat
5f76371 - (HEAD, master) add ignore files (7 minutes ago) 
 .gitignore |    3 +++
 test.rb    |    5 +++++
 2 files changed, 8 insertions(+), 0 deletions(-)

4ca268d - (origin/master) First commit (37 minutes ago) 
 lib/animal.rb       |    5 +++++
 spec/animal_spec.rb |    5 +++++
 2 files changed, 10 insertions(+), 0 deletions(-)
如果你想看到檔案更詳細的變更內容，你可以加上 -p 的參數：

$ git log -p
5f76371 - (HEAD, master) add ignore files (8 minutes ago) 
diff --git a/.gitignore b/.gitignore
new file mode 100644
index 0000000..61521a9
--- /dev/null
+++ b/.gitignore
@@ -0,0 +1,3 @@
+.DS_Store
+*.swp
+log/*.log
diff --git a/test.rb b/test.rb
new file mode 100644
index 0000000..23df1c1
--- /dev/null
+++ b/test.rb
@@ -0,0 +1,5 @@
+class Test
+  def test
+    puts "This is a test file"
+  end
+end

因此我們稍微做一下流程的整理：
修改檔案 => 加入 stage (git add) => 提交( git commit )=> 繼續修改其他檔案

Tips: commit 的最佳時機？ 什麼時候該 commit ?
什麼時候才是 commit 的最好時機並沒有一個定論，大部分人會告訴你通常你完成了一個階段性的小工作就做一次的 commit ，我的感覺是當你想要記錄目前的狀態的時候就是你 commit 的最佳時機，
例如說剛完成某個page，某個任務需求而你想要做個記錄的時候。
有些檔案我們不希望加入版本控制的追蹤，例如說Database的schema或是一些log檔，這時候你可以將他們加入 .gitignore 中來讓 Git 忽略他們，使用編輯器來打開你的 .gitignore 檔案。
$ vim .gitignore
在這邊假設我想將 Mac 自動產生的.DS_Store， vim 的 swp 暫存檔及 log 檔忽略，我便分行加入：
.DS_Store
*.swp
log/*.log
如此一來便會將這些檔案從git追蹤忽略了。
Tips: 被加入 gitignore 的檔案一樣出現在 status 中？
有時候你會發現即時你將檔案加入了 .gitignore 卻一樣會出現在 Git 的追蹤狀態中，這是由於你想要忽略的檔案之前已經被 Git 追蹤了，因此你現在想要讓 Git 忽略他的話只能先將他刪除然後再 commit 一次，
再來這支檔案再出現就不會再追蹤這支檔案了。


/******************************************************************************/
簡易git server架設教學 (用Ubuntu linux)
/******************************************************************************/
1. 安裝git
sudo apt-get install git-core

2. 在server端建立放置所有projects的目錄
我的習慣是放在 /var/git
cd /var
sudo mkdir git

3. 在server端建立project
步驟3,5,6是 每開一個新project就要做一遍 的，假設現在我開了一個專案叫new_project
cd /var/git
sudo mkdir new_project.git
# 如果是第二次新增project，記得也要改該資料夾的群組跟權限，相關步驟在step 4有寫
cd new_project.git
sudo git --bare init

4. 建立git的群組
因為我放在/var之下，這邊要root權限，當你用你的帳號pull東西上去時，會爆權限不足。
但是把他改成權限全開的話(chmod 777 ...)又很危險。所以我開一個git的群組，讓會傳東西的人加到這個群組。
sudo groupadd git
sudo usermod -a -G git your_login # your_login改成你自己的帳號。
# 下面這兩行，在每次新增新project時要對新的資料夾補做
sudo chgrp -R git /var/git
sudo chmod g+rwx -R /var/git
在local端，假設我的project資料夾是/path/to/your/projects/new_project

5. 初始化git
cd /path/to/your/projects/new_project
git init

6. 把我們遠端的repository加到git remote
`git remote add origin ssh://your_login@your.host/var/git/new_project.git/`
這邊的路徑要注意，別打成 ssh://your_login@your.host:/var/git/new_project.git，否則會爆以下錯誤：
ssh: Could not resolve hostname : Name or service not known
fatal: The remote end hung up unexpectedly

7. 把我們local的程式碼丟上去：(每次commit的例行步驟)
git add .
git commit -m '註解'
git push origin master

常用git指令小筆記：
git add 檔案名稱 #加到本次commit
git add -i #加檔案的互動介面
git status # 看準備要commit的檔案
git grep 關鍵字 # 在專案中搜尋關鍵字
git diff # 看本次變動
git log # 看log
git rm 檔案名稱 # 從準備要commit的檔案清單中去除，加-f參數強制刪除
git remote # 會列出來remote列表。總之就是git remote add new_remote ssh://... 。新增以後，打這個指令就會出現new_remote。名稱可以自己取，但如果需求單純的話，一般都習慣取作origin。

如果你懶得每次要一直打密碼，可以參考SSH免密碼登入


/******************************************************************************/
[Coding] repo & git 的使用方法
/******************************************************************************/
什麼是Repo和Git？
Git是所謂的分散式版本控管系統，網路上可以查到很多相關資料，請善用Google，在此就只貼上維基百科的說明。
要先知道，Android本身是一個大的work space，裡面包含非常多的git repository。
為了方便管理這些git repository，Repo就是背負著這個責任所發明出來的。
Repo是由Google用Python script所寫出來，專門用來使用Git的一套script，主要是用來下載、管理Android下所有的git repository。
Repo: 
使用Repo就大部分按照以下的格式
repo COMMAND OPTIONS

1、獲取相關幫助：
repo help COMMAND
例如：repo help init，就可以取得repo init的其他用法

2、repo init -u URL
用來在目前目錄安裝下載整個Android repository，會下建立一個".repo"的目錄。
-u參數用來指定一個URL，從這個URL中獲取repository的manifest文件。
例如：repo init -u git://android.git.kernel.org/platform/manifest.git，獲取的manifest文件放在.repo目錄中，命名為manifest.xml。
這個文件的內容其實就是Android work space下所有被git管理的git repository的列表！
如果你有仔細看，可以發現到.repo/manifests是個被git管理的repository，裡面放著所有的manifest文件 (*.xml)。而透過參數的設定，則可以指定要使用哪個manifest文件，甚至是該文件的不同branch。
-m：用來選擇獲取 repository 中的某一個特定的 manifest 文件。如果不具體指定，那麼表示為預設的 manifest 文件 (default.xml)
repo init -u git://android.git.kernel.org/platform/manifest.git -m dalvik-plus.xml
-b：用來指定某個manifest 分支。
repo init -u git://android.git.kernel.org/platform/manifest.git -b release-1.0

3、repo sync [PROJECT_LIST]
下載最新文件，更新成功後，文件會和遠端server中的代碼是一樣的。 可以指定需要更新的project ， 如果不指定任何參數，則會同步整個所有的project。

4、repo upload [PROJECT_LIST]
上傳修改的代碼 ，如果你的代碼有所修改，那麼在運行 repo sync 的時候，會提示你上傳修改的代碼。所有修改的代碼分支會上傳到 Gerrit，Gerrit 收到上傳的代碼，會轉換為一個改動，從而可以讓人們來review 修改的代碼。

5、repo diff [PROJECT_LIST]
顯示尚未commit的改動差異

6、repo download target revision
下載指定的修改版本， 例如:  repo download platform/frameworks/base 1241 ，就是下載修改版本為 1241 的代碼。

7、repo start new_branch_name [PROJECT_LIST]
在指定的project中建立新的branch，並且切換到該branch上。

--all：代表指定所有的git projects

8、repo prune [PROJECT_LIST]
刪除已經merge好的project。

9、repo forall [PROJECT_LIST] -c COMMAND
針對指定的project執行所帶入的git command，例如：repo forall -c git reset --hard HEAD 就會將所有project中的改動全部都清掉。

10、repo status
顯示所有project的狀態

Git:
1. 把遠端的git project抓下來放在local
git clone [REMOTE_PROJECT_URL]

2. 之前有提到的，任何的改動都需要建立在branch之上，所以就得建立local branch
git branch [BRANCH_NAME]

如果local branch需要track遠端的branch，那就在後面加上remote branch
git branch [BRANCH_NAME] [REMOTE_BRANCH]

要知道有哪些remote branch，可以透過git branch -a，會列出所有(local和remote)的branch。
git branch -a
舉例來說：
$ git branch -a
* local_branch
  remotes/arm7/master
$ git branch local_branch_test remotes/arm7/master

3. 切換local branch
git checkout [BRANCH_NAME]

4. 列出所有的改動
git status

5. 把改動的檔案先放上modified list
git add [FILE_NAME]
 or 
git add [DIR_NAME]

6. 把modified list中的檔案，退掉改動
git checkout [FILE_NAME]
 or
git checkout [DIR_NAME]

7. 把所有project中的所有改動都退掉
git reset --hard HEAD

8. 將modified list中的改動一起commit到local branch
git commit

9. 將local branch上已經commit的改動退掉 (改動還留著)
git reset --soft HEAD^

10. 把commit的改動，放到remote branch
git push [REMOTE_PROJECT_URL] HEAD:refs/to/[REMOTE_BRANCH_NAME]

要怎麼知道remote branch name呢？
可以透過git remote show [REMOTE]，例如下面的例子中的branch name就是master：
$ git remote
mips
$ git remote show mips
* remote mips
  Fetch URL: [REMOTE_PROJECT_URL]
  Push  URL: [REMOTE_PROJECT_URL]
  HEAD branch: master
  Remote branch:
    master tracked
  Local branch configured for 'git pull':
    local_branch merges with remote master


/******************************************************************************/
Ubuntu Linux 上安裝並設定私有 git server 筆記
/******************************************************************************/
因為工作需要，我必須要在 Ubuntu 上架設一個私有的 git server , 以下是筆記

事先準備：
灌好 Ubuntu 的實體機器或 VM （我是用 Ubuntu Server 14.04 LTS）
安裝 Ubuntu 時選 sshd server 或是由 apt-get 安裝 ssh 

步驟：
若想用最新的 git 版本（建議），可先加入 ppa 再安裝
$ sudo add-apt-repository ppa:git-core/ppa
$ sudo apt-get update
$ sudo install git git-core

確認 git 版本的方法
$ git --version

在 server 端建立 project
$ cd /var/git （目錄位置可以自己決定）
$ sudo mkdir new_project.git
$ cd new_project.git
$ sudo git --bare init
 
如果要用 ssh 存取，每一個可以用來存取的帳號必須為這台 linux 的帳號（用 web 就不一定要用了，這個其他文章再提），為了方便我們可以建立一個群組，把要存取 git 的人加入。

sudo groupadd git
sudo usermod -a -G git [你的id] ＃id 改自己的帳號
# 修改 owner 跟權限，每次開專案時都要做
sudo chgrp -R git /var/git 
sudo chown g+rwx -R /var/git
回到 local 端，我們要 clone 一個 git 的 repository 下來改，語法如下
git clone ssh://[你的帳號]@[server ip or name]:/var/git/new_proejct.git
將帳號, server ip 換成自己的。
系統會問你密碼，填入密碼，就可以把 repository clone 下來，之後就跟一般 git 操作一樣，修改->commit->push



/******************************************************************************/
[Coding] repo & git 的使用方法
/******************************************************************************/
最近開始，由於公司規劃往Android方向靠攏，學習Android上所採用Repo和Git作為版本控制的工具就變成無法避免的課題。

什麼是Repo和Git？
Git是所謂的分散式版本控管系統，網路上可以查到很多相關資料，請善用Google，在此就只貼上維基百科的說明。

要先知道，Android本身是一個大的work space，裡面包含非常多的git repository。為了方便管理這些git repository，Repo就是背負著這個責任所發明出來的。Repo是由Google用Python script所寫出來，專門用來使用Git的一套script，主要是用來下載、管理Android下所有的git repository。
Repo: 
使用Repo就大部分按照以下的格式
repo COMMAND OPTIONS

1、獲取相關幫助：
repo help COMMAND
例如：repo help init，就可以取得repo init的其他用法

2、repo init -u URL
用來在目前目錄安裝下載整個Android repository，會下建立一個".repo"的目錄。-u參數用來指定一個URL，從這個URL中獲取repository的manifest文件。
例如：repo init -u git://android.git.kernel.org/platform/manifest.git，獲取的manifest文件放在.repo目錄中，命名為manifest.xml。這個文件的內容其實就是Android work space下所有被git管理的git repository的列表！

如果你有仔細看，可以發現到.repo/manifests是個被git管理的repository，裡面放著所有的manifest文件 (*.xml)。而透過參數的設定，則可以指定要使用哪個manifest文件，甚至是該文件的不同branch。

-m：用來選擇獲取 repository 中的某一個特定的 manifest 文件。如果不具體指定，那麼表示為預設的 manifest 文件 (default.xml)
repo init -u git://android.git.kernel.org/platform/manifest.git -m dalvik-plus.xml

-b：用來指定某個manifest 分支。
repo init -u git://android.git.kernel.org/platform/manifest.git -b release-1.0

3、repo sync [PROJECT_LIST]
下載最新文件，更新成功後，文件會和遠端server中的代碼是一樣的。 可以指定需要更新的project ， 如果不指定任何參數，則會同步整個所有的project。

4、repo upload [PROJECT_LIST]
上傳修改的代碼 ，如果你的代碼有所修改，那麼在運行 repo sync 的時候，會提示你上傳修改的代碼。所有修改的代碼分支會上傳到 Gerrit，Gerrit 收到上傳的代碼，會轉換為一個改動，從而可以讓人們來review 修改的代碼。

5、repo diff [PROJECT_LIST]
顯示尚未commit的改動差異

6、repo download target revision
下載指定的修改版本， 例如:  repo download platform/frameworks/base 1241 ，就是下載修改版本為 1241 的代碼。

7、repo start new_branch_name [PROJECT_LIST]
在指定的project中建立新的branch，並且切換到該branch上。

--all：代表指定所有的git projects

8、repo prune [PROJECT_LIST]
刪除已經merge好的project。

9、repo forall [PROJECT_LIST] -c COMMAND
針對指定的project執行所帶入的git command，例如：repo forall -c git reset --hard HEAD 就會將所有project中的改動全部都清掉。

10、repo status
顯示所有project的狀態

Git:
1. 把遠端的git project抓下來放在local
git clone [REMOTE_PROJECT_URL]

2. 之前有提到的，任何的改動都需要建立在branch之上，所以就得建立local branch
git branch [BRANCH_NAME]

如果local branch需要track遠端的branch，那就在後面加上remote branch
git branch [BRANCH_NAME] [REMOTE_BRANCH]

要知道有哪些remote branch，可以透過git branch -a，會列出所有(local和remote)的branch。
git branch -a
舉例來說：
$ git branch -a

* local_branch

  remotes/arm7/master

$ git branch local_branch_test remotes/arm7/master

3. 切換local branch
git checkout [BRANCH_NAME]

4. 列出所有的改動
git status

5. 把改動的檔案先放上modified list
git add [FILE_NAME]

 or 

git add [DIR_NAME]

6. 把modified list中的檔案，退掉改動
git checkout [FILE_NAME]

 or

git checkout [DIR_NAME]

7. 把所有project中的所有改動都退掉
git reset --hard HEAD

8. 將modified list中的改動一起commit到local branch
git commit

9. 將local branch上已經commit的改動退掉 (改動還留著)
git reset --soft HEAD^

10. 把commit的改動，放到remote branch
git push [REMOTE_PROJECT_URL] HEAD:refs/to/[REMOTE_BRANCH_NAME]

要怎麼知道remote branch name呢？
可以透過git remote show [REMOTE]，例如下面的例子中的branch name就是master：
$ git remote
mips
$ git remote show mips
* remote mips
  Fetch URL: [REMOTE_PROJECT_URL]
  Push  URL: [REMOTE_PROJECT_URL]
  HEAD branch: master
  Remote branch:
    master tracked
  Local branch configured for 'git pull':
    local_branch merges with remote master


/******************************************************************************/
.gitignore example
/******************************************************************************/
https://github.com/github/gitignore


/******************************************************************************/
[Git] 工作上常使用到的git指令
分享: facebook PLURK twitter  


@可以看某個git check point的詳細紀錄 
git log -p -l 2afeedb08454260516db332d70e661c3ae35e216 

@git 退版 
git checkout -b GoogleReader 2afeedb08454260516db332d70e661c3ae35e216 
說明:新增一個GoogleReader的branch並還原到後面commit point的時間版本 

@建立git push rule的範本 
git config commit.template ~/git-template 

＠建立新的branch 
git branch 'branch name' 
Ex. git branch working; //建立一個名字為working的branch 

@刪除branch 
git branch -D 

@只加修改過的檔案, 新增的檔案不加入 
git add -u


@個人資料設定
git config --global user.name "First Last" /* 設定使用者名稱 */
git config --global user.email "user@example.com" /* 設定使用者電子郵件 */

@設定commit的template

1.使用指令方式設定
$ git config --global commit.template $HOME/.git-template
$ git commit

2.可以直接在.gitconfig裡設定
[commit]
template = /home/frank/.git-template

@git log 使用方式
1.查看最近2次的提交歷史紀錄
git log -2

2.在該資料夾下看誰在git server上更改過的歷史紀錄
git log .


3.查看file1文件的提交紀錄 
git log filename

4.查看送交更改過檔案，計算每個檔案中被更改的行數
git log --stat


@git init 的方式
1.在初始化git過程時最好使用 git init  --bare而不要使用：git init
由於初始化的git目錄中，存在一些其它與git本地相關的文件或是目錄，導致無法push code。

--bare
在不加--bare所init完的結果，會是在目前的working目錄下建立.git目錄，並把上述的git相關檔案放在.git目錄裡。
加了--bare的話，則是不建.git目錄，而把裡面的檔案直接放在目前目錄下。
適合在沒有修改檔案或開發的機器上，ex GIT server。
好處是只要maintain git repository，project的資料只存在repository中，不需要再複製一份最新的版本出來，會省點空間。

2.上傳檔案
git push origin master 

@設定指令的縮寫
git config --global alias.st status

@git reset使用方式
使用git reset有兩種情況

1. git reset --soft HEAD^
只會撤銷上一個commit，通常用在少加或加錯檔案，此時可以打此指令，在重新git add和git commit。

2.git reset --hard HEAD^
不只撤銷commit，連commit裡列表修改過檔案，都會還原成未修改的狀態，所以要謹慎使用。

3. git commit --amend
此指令通常用在commit log寫錯時，可以打此指令，修改commit log後，再上傳。


@重新命名git branch
假設現在有兩個 branch， master 跟 old-branch ，目前在 master ，
想要把 old-branch 的名字改成 new-branch 的話，請輸入
git branch -m old-branch new-branch

如果現在已經在 old-branch ，想要直接把名字改成 new-branch 的話，就輸入：
git branch -m new-branch


@當repo sync遇到衝突時

如下所示，會列出下面的訊息
warning: squelched 1295 whitespace errors
warning: 1300 lines add whitespace errors.
Falling back to patching base and 3-way merge...
Auto-merging Android.mk
CONFLICT (content): Merge conflict in Android.mk
Recorded preimage for 'Android.mk'
Failed to merge in the changes.
Patch failed at 0001 Symptom : [UI framework]
When you have resolved this problem run "git rebase --continue".
If you would prefer to skip this patch, instead run "git rebase --skip".
To restore the original branch and stop rebasing run "git rebase --abort".

表示Gaia.mk遇到衝突，需要手動修改

解法：
切資料夾到gaiaframework
1.打開Android.mk，搜尋===的字串，手動修改衝突
2.修改完後，執行git add。
3.接著打 git rebase --continue，系統會幫忙處理更改過的commit。

@將code上傳到Gerrit的步驟

1.到各個要上code的branch，進行git add --> git commit
2.先repo sync確保已抓到最新的code
3.打repo upload
4.把#註解到的branch給去掉
5.upload成功。
6.到Gerrit上增加reviewer。


/******************************************************************************/
/******************************************************************************/
/******************************************************************************/

De++eR
