##git-petty-thing

* ####git rebase
>背景
提交代码后，本次commit和服务器中的某些commit不在同一时间轴上，即：本次commit需要参入到服务器中的某些commit之间，这样会造成代码冲突，所以要做rebase
方法：现在的分支为<code>feature/mix</code>,在本分至上刚提交过一些commit，此时
>*	1.新建一个分支，并且代码和服务器中代码同步
    <pre><code>git checkout origin/master -b temp</code></pre>
    <pre><code>git push</code></pre>
>* 2.回到feature/mix分支
	<pre><code>git checkout feature/mix</code></pre>
>* 3.开始rebase操作
    <pre><code>git rebase temp</code></pre>
>* 4.solve conflict 解决冲突后,
    <pre><code>git add .</code></pre>
    <pre><code>git rebase --continue</code></pre>
    <pre>注意，在以上<code>git add .</code>之后是不需要<code>git commit</code>的</pre>
>* 5.因为提交有多个，所以会出现多次solve conflict操作，直至没有冲突
>* 6.此时重新提交代码，
    <pre><code>git push</code></pre>


* ####git 合并数次commit
>*	1.<code>git log</code>查看你需要合并的几条commit的<code>hax_num</code>
	
```
    commit 5db46f...
	Author: me
	Date:   Sun Jan 18 14:10:46 2015 +0800

	    fix the github-markdown layouts

	commit cdedf...
	Author: me 
	Date:   Sun Jan 18 14:02:10 2015 +0800

	    sort it
```

>*	2.<code>git rebase -i hax_num</code>,此处hax_num是属于几条commit中最早的那一条commit的

```
	pick d0ccecd remove ##
	pick b677a3c add reset methods
	pick ba1ce29 remove ##
	pick cdedf66 sort it
	pick 5db46fd fix the github-markdown layouts

	#  p, pick = use commit
	#  r, reword = use commit, but edit the commit message
	#  e, edit = use commit, but stop for amending
	#  s, squash = use commit, but meld into previous commit
	#  f, fixup = like "squash", but discard this commit's log message
	#  x, exec = run command (the rest of the line) using shell
```
>*  3.将第一条commit的<code>pick</code>保留，其他要合并的commit的<code>pick</code>改为<code>squash</code>，然后退出
如果出现冲突，就solve conflict，
再次查看<code>git log</code>发现

```
	commit dad35...
	Author: me 
	Date:   Sun Jan 18 13:29:37 2015 +0800

	    remove ##
	    
	    add reset methods
	    
	    remove ##
	    
	    sort it
	    
	    fix the github-markdown layouts
```

>*  4.<code>git push</code>

* ####git 修改某次commit
>* 1.<code>git rebase -i </code>
>* 2.将要修改的commit的pick改成edit
>* 3.<code>git commit -amend</code>
>* 4.修改<code>commit</code>内容，保存并退出
>* 5.<code>git rebase --continue</code>
>* 6.<code>git log</code>查看是否修改生效（可选）

* ####删除分支
>删除本地分支
><code>git branch -d feature/xxx</code>
>** **
>删除远程分支
><code>git branch -d feature/xxx</code>先删除本地分支
><code>git push origin :feature/xxx</code>再将该空分支推送到远程，即可删除

* ####commit
>* <code>git add .</code>
>* <code>git commit -m 'merge feature into master'</code>
>* <code>git push</code>

* ####git merge 合并feature/xxx分支到master上
>* 1.<code>git checkout master</code>
>* 2.<code>git merge feature/xxx</code>
>* 3.<code>commit</code>
>* 4.删除<code>feature/xxx</code>分支


* ####git stash
>* 1.<code>git stash</code>暂存修改内容
>* 2.<code>git stash pop</code>从git栈中读取最近一次的stash内容，并从stash list中移除
>* 3.<code>git stash list</code>显示git栈中所有stash版本
>* 4.<code>git stash clear</code>清除git栈
>* 5.<code>git stash pop stash@{1}</code> 与 <code>git stash apply stash@{1}</code> 后者不会从stash list中移除stash@{1}

* ####git如何删除远程仓库的某次错误提交
>* <code>git reset –mixed</code>
>此为默认方式，不带任何参数的git reset，就是这种方式，它回退到某个版本，只保留源码，回退commit和stage信息
>* <code>git reset –soft</code>
>回退到某个版本， 只回退了commit的信息，不会恢复stage（如果还要提交，直接commit即可
>* <code>git reset –hard</code>
>彻底回退到某个版本， 本地的源码也会变为上一个版本的内容
