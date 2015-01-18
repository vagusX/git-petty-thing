##git-petty-thing

*  git rebase 
>背景
提交代码后，本次commit和服务器中的某些commit不在同一时间轴上，即：本次commit需要参入到服务器中的某些commit之间，这样会造成代码冲突，所以要做rebase


* git 修改commit
>1

*  git如何删除远程仓库的某次错误提交
>* git reset –mixed
>此为默认方式，不带任何参数的git reset，就是这种方式，它回退到某个版本，只保留源码，回退commit和stage信息
>* git reset –soft
>回退到某个版本， 只回退了commit的信息，不会恢复stage（如果还要提交，直接commit即可
>* git reset –hard
>彻底回退到某个版本， 本地的源码也会变为上一个版本的内容
