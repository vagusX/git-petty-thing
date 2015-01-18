##git-petty-thing

*  git rebase 
>背景
提交代码后，本次commit和服务器中的某些commit不在同一时间轴上，即：本次commit需要参入到服务器中的某些commit之间，这样会造成代码冲突，所以要做rebase
方法：现在的分支为<code>feature/mix</code>,在本分至上刚提交过一些commit，此时
>*	1.新建一个分支，并且代码和服务器中代码同步
    <code>git checkout origin/master -b temp</code>
  	<code>git push</code>
>* 2.回到<code>feature/mix</code>分支
	<code>git checkout feature/mix</code>
>* 3.开始rebase操作
	<code>git rebase temp</code>
>* 4.solve conflict 解决冲突后
	<code>git add .</code> //不需要<code>git commit</code>
    <code>git rebase --continue</code>
>* 5.因为提交有多个，所以会出现多次solve conflict操作，直至没有冲突
>* 6.此时重新提交代码，git push


* git 修改commit
>

1. 可以记住某个commit号
2. git rebase -i commit号
3. 会显示一个整理提交的界面，有很多参数，e。p。等等
4.将前面的参数改为e。则wq保存后，系统会自动让你重新修改commit内容
5.修改完成后，再git push for-*

*  git如何删除远程仓库的某次错误提交
>* git reset –mixed
>此为默认方式，不带任何参数的git reset，就是这种方式，它回退到某个版本，只保留源码，回退commit和stage信息
>* git reset –soft
>回退到某个版本， 只回退了commit的信息，不会恢复stage（如果还要提交，直接commit即可
>* git reset –hard
>彻底回退到某个版本， 本地的源码也会变为上一个版本的内容