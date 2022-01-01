# devops-netology
DevOps course in Netology, homework
new line for the task 7
Будут проигнорированы файлы из подпапки terraform, подподающие под ограничения вложенного в папку terraform файла .gitignore:
-локальные папки terraform
-файлы с "расщирением" tfstate и содержащие в имени tfstate
-файлы логов падений crash.log
-файлы с "расширеним" tfvars, содержащие явки и пароли и тому подобные секретные данные, не относящиеся к версионируемым объектам
-файлы переопределений локальных ресурсов
-файлы с настройками CLI 
+one line to the fix branch
-------------------------------------------
Домашнее задание к занятию «2.3. Ветвления в Git»
Здравствуйте! 
Не очень понятно в каком виде необходимо предоставить решение задачи, поэтому приложу историю команд (история терминала не очень сохранилась, т.к. перетёрлась man'ами)
Также приложу ссылку на Network graph своего репозитория:
https://github.com/zhukovga/devops-netology/network
На графе видно, что домашку делал со второго раза, т.к. вначале пропустил моменты с пушами и немного запутался с репозиторями, т.к. с прошлой домашки остались подключенными репозитории bitbucket и gitlab. 

  967  git push --set-upstream origin main
  968  git status
  969  git checkout main
  970  git status
  971  ls
  972  cd branching/
  973  ls
  974  vi merge.sh
  975  vi rebase.sh
  976  git commit -m "prepare for merge and rebase"
  977  git add .
  978  git commit -m "prepare for merge and rebase"
  979  git push origin main
  980  git checkout -b git-merge
  981  vi merge.sh
  982  git add .
  983  git commit -m "merge: @ instead *"
  984  git push origin main
  985  vi merge.sh
  986  git add .
  987  git commit "merge: use shift"
  988  git commit -m "merge: use shift"
  989  git push origin main
  990  git status
  991  vi merge.sh
  992  git commit -m "merge: @ instead *"
  993  git add .
  994  git commit -m "merge: @ instead *"
  995  git push origin git-merge
  996  vi merge.sh
  997  git add .
  998  git commit -m "merge: use shift"
  999  git push origin git-merge
 1000  git checkout main
 1001  vi rebase.sh
 1002  git add .
 1003  git push origin main
 1004  git add .
 1005  git commit -m "changed rebase.sh first time with ====="
 1006  git push origin main
 1007  git log
 1008  git checkout 7c2e9fdcbb1c0d4201592fa3c342373f18598576
 1009  ls
 1010  git checkout -b git-rebase
 1011  vi rebase.sh
 1012  git add .
 1013  git commit -m "git-rebase"
 1014  git push origin git-rebase
 1015  git status
 1016  git commit -m "git-rebase 1"
 1017  vi rebase.sh
 1018  git add .
 1019  git commit -m "git-rebase 2"
 1020  git push origin git-rebase
 1021  git push --force origin git-rebase
 1022  git status
 1023  git checkout main
 1024  git merge git-merge
 1025  git push
 1026  git checkout git-rebase
 1027  git rebase -i main
 1028  vi rebase.sh
 1029  git rebase -i main
 1030  git rebase -i main --abort
 1031  git rebase --abort
 1032  git rebase -i main
 1033  vi rebase.sh
 1034  git add rebase.sh
 1035  git rebase --continue
 1036  git rebase --abort
 1037  git rebase -i main
 1038  vi rebase.sh
 1039  git add rebase.sh
 1040  vi rebase.sh
 1041  git rebase --continue
 1042  vi rebase.sh
 1043  git add rebase.sh
 1044  git rebase --continue
 1045  git push -u origin git-rebase
 1046  git push -u origin git-rebase -f
 1047  git checkout main
 1048  git merge git-rebase
 1049  git push



