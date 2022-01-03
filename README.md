# devops-netology
DevOps course in Netology, homework
-------------------------------------------
Домашнее задание к занятию "3.1. Работа в терминале, лекция 1"
1. Установите средство виртуализации Oracle VirtualBox.
+ Готово

2. Установите средство автоматизации Hashicorp Vagrant.
+ Готово

3. В вашем основном окружении подготовьте удобный для дальнейшей работы терминал.
+ Готово

4. С помощью базового файла конфигурации запустите Ubuntu 20.04 в VirtualBox посредством Vagrant
+ Готово

5. Ознакомьтесь с графическим интерфейсом VirtualBox, посмотрите как выглядит виртуальная машина, которую создал для вас Vagrant, какие аппаратные ресурсы ей выделены. Какие ресурсы выделены по-умолчанию
ОТВЕТ: 
	Параметры созданной виртуалки:
	Base mem:  1024MB
	Processors: 2
	VMDK virtual size: 64GB
	Video memory: 4MB
	OS: Ubuntu 20.04.3 LTS

6. Ознакомьтесь с возможностями конфигурации VirtualBox через Vagrantfile: документация. Как добавить оперативной памяти или ресурсов процессора виртуальной машине?
ОТВЕТ:
	Прописать в VagrantFile подобный цикл:
	config.vm.provider "virtualbox" do |vb|
  	vb.memory = "2048"
	vb.cpus = "4"
	end
7. Команда vagrant ssh из директории, в которой содержится Vagrantfile, позволит вам оказаться внутри виртуальной машины без каких-либо дополнительных настроек. Попрактикуйтесь в выполнении обсуждаемых команд в терминале Ubuntu.
ОТВЕТ:
	Проверил, авторизация ssh по ключу работает. Также проверил вход по ssh на 127.0.0.1 по порту (в моем случае 2222) пользователем vagrant/vagrant - работает.

8. Ознакомиться с разделами man bash, почитать о настройках самого bash:
   - какой переменной можно задать длину журнала history, и на какой строчке manual это описывается?
	ОТВЕТ: 
	HISTSIZE - количество команд, которые будут запомнены в журнале,
	HISTFILESIZE - максимальное количество строк файла журнала
 	Номер строки зависит от масштабирования окна ssh клиента у меня на экране, в моем случае строки 875 и 859
   - что делает директива ignoreboth в bash?
	ОТВЕТ: данная директива является краткой записью для применения директив ignorespace (в историю команд bash не запишутся команды, начинающихся с пробела) и ignoredups (в историю команд bash не запишутся предыдущие повторные команды). 

9. В каких сценариях использования применимы скобки {} и на какой строчке man bash это описано?
ОТВЕТ:
	- Скобки {} применяются при написании составных команд и используются для передачи команде списка значений. Значения списка переданные команде выполняются в текущем окружении.
	 { list; }
              list is simply executed in the current shell environment.  list must be terminated with a newline or
              semicolon.  This is known as a group command.  The return status is the exit status of  list.   Note
              that  unlike  the metacharacters ( and ), { and } are reserved words and must occur where a reserved
              word is permitted to be recognized.  Since they do not cause a word break, they  must  be  separated
              from list by whitespace or another shell metacharacter.
	

	- Описание применения {} начинается на строке 258 (в моем случае) 

10. С учётом ответа на предыдущий вопрос, как создать однократным вызовом touch 100000 файлов? Получится ли аналогичным образом создать 300000? Если нет, то почему?
ОТВЕТ: создать 10000 тысяч файлов можно командой touch {00001..10000}.txt

Создать 30000 тысяч файлов в моем случае получилось. А вот создать 200000 не вышло, т.к. получаем ошибку Argument list too long из-за того, что команда touch с переданным ей списочным параметром разворачивает этот список в одну строку с перечислением всех параметров. В какой-то момент длина этой строки вываливается за значение системной переменной  ARG_MAX (в моем случае имеет значение 2097152 bytes).

11. В man bash поищите по /\[\[. Что делает конструкция [[ -d /tmp ]]
ОТВЕТ:
	Проверяется выполнение услова наличия директории (ключ -d) /tmp, возвращается 0 если директория есть и 1, если директории нет. Можно использовать данное выражение, например в скриптах вида if [[ -d /tmp]] then ... else ... fi

12. Основываясь на знаниях о просмотре текущих (например, PATH) и установке новых переменных; командах, которые мы рассматривали, добейтесь в выводе type -a bash в виртуальной машине наличия первым пунктом в списке:
bash is /tmp/new_path_directory/bash
bash is /usr/local/bin/bash
bash is /bin/bash
ОТВЕТ:
	vagrant@vagrant:/$ mkdir /tmp/new_path_directory
	vagrant@vagrant:/$ cp /bin/bash /tmp/new_path_directory
	vagrant@vagrant:/$ PATH=/tmp/new_path_directory/:$PATH
	vagrant@vagrant:/$ type -a bash
	bash is /tmp/new_path_directory/bash
	bash is /usr/local/bin/bash
	bash is /usr/bin/bash
	bash is /bin/bash

13. Чем отличается планирование команд с помощью batch и at?
ОТВЕТ:
at - команда запускается в переданное параметром команде время
batch - команда запускается во время снижения нагрузки на систему ниже 1.5

14. Завершите работу виртуальной машины чтобы не расходовать ресурсы компьютера и/или батарею ноутбука.
ОТВЕТ:
vagrant suspend


-------------------------------------------
Домашнее задание к занятию «2.4. Инструменты Git»
1. Найдите полный хеш и комментарий коммита, хеш которого начинается на aefea.
ОТВЕТ: 
	хеш: aefead2207ef7e2aa5dc81a34aedf0cad4c32545
	комментарий: Update CHANGELOG.md 
Как получил ответ:
	1.1. admin@devops:~/.git/terraform$ git log | grep aefea
		commit aefead2207ef7e2aa5dc81a34aedf0cad4c32545
		commit 8619f566bbd60bbae22baefea9a702e7778f8254
		commit 3593ea8b0aefea1b4b5e14010b4453917800723f
		commit 0196a0c2aefea6b85f495b0bbe32a855021f0a24
	Убедился, что есть один commit, начинающийся на aefea, отсюда же взял полный хэш aefead2207ef7e2aa5dc81a34aedf0cad4c32545 
	1.2. admin@devops:~/.git/terraform$ git show aefead2207ef7e2aa5dc81a34aedf0cad4c32545
		commit aefead2207ef7e2aa5dc81a34aedf0cad4c32545
		Author: Alisdair McDiarmid <alisdair@users.noreply.github.com>
		Date:   Thu Jun 18 10:29:58 2020 -0400
		
		    Update CHANGELOG.md
	Получил комментарий к коммиту "Update CHANGELOG.md"	

2. Какому тегу соответствует коммит 85024d3?
ОТВЕТ:
	tag: v0.12.23
Как получил ответ:
	2.1. admin@devops:~/.git/terraform$ git show 85024d3
		commit 85024d3100126de36331c6982bfaac02cdab9e76 (tag: v0.12.23)
		Author: tf-release-bot <terraform@hashicorp.com>
		Date:   Thu Mar 5 20:56:10 2020 +0000
		
		    v0.12.23
	В скобках приведено наименование тэга коммита.

3. Сколько родителей у коммита b8d720? Напишите их хеши.
ОТВЕТ:
	Родителей: 2
	Хеш первого родителя: 56cd7859e05c36c06b56d013b55a252d0bb7e158
	Хеш второго родителя: 9ea88f22fc6269854151c571162c5bcf958bee2b
Как получил ответ:
	3.1. admin@devops:~/.git/terraform$ git show b8d720
		commit b8d720f8340221f2146e4e4870bf2ee0bc48f2d5
		Merge: 56cd7859e 9ea88f22f
		Author: Chris Griggs <cgriggs@hashicorp.com>
		Date:   Tue Jan 21 17:45:48 2020 -0800
	Из вывода команды в строке Merge увидел, что коммит получен слиянием коммитов 56cd7859e и 9ea88f22f
	3.2. admin@devops:~/.git/terraform$ git show b8d720^1
		commit 56cd7859e05c36c06b56d013b55a252d0bb7e158
		Merge: 58dcac4b7 ffbcf5581
		Author: Chris Griggs <cgriggs@hashicorp.com>
		Date:   Mon Jan 13 13:19:09 2020 -0800
	Данной командой посмотрел хеш первого родителя - 56cd7859e05c36c06b56d013b55a252d0bb7e158
	3.3. admin@devops:~/.git/terraform$ git show b8d720^2
		commit 9ea88f22fc6269854151c571162c5bcf958bee2b
		Author: Chris Griggs <cgriggs@hashicorp.com>
		Date:   Tue Jan 21 17:08:06 2020 -0800
	Данной командой посмотрел хеш второго родителя - 9ea88f22fc6269854151c571162c5bcf958bee2b

4. Перечислите хеши и комментарии всех коммитов которые были сделаны между тегами v0.12.23 и v0.12.24.
ОТВЕТ:
	хеш:	  комментарий:
	b14b74c49 [Website] vmc provider links
	3f235065b Update CHANGELOG.md
	6ae64e247 registry: Fix panic when server is unreachable
	5c619ca1b website: Remove links to the getting started guide's old location
	06275647e Update CHANGELOG.md
	d5f9411f5 command: Fix bug when using terraform login on Windows
	4b6d06cc5 Update CHANGELOG.md
	dd01a3507 Update CHANGELOG.md
	225466bc3 Cleanup after v0.12.23 release
Как получил ответ:
	4.1. admin@devops:~/.git/terraform$ git log v0.12.23..v0.12.24 --oneline
		33ff1c03b (tag: v0.12.24) v0.12.24
		b14b74c49 [Website] vmc provider links
		3f235065b Update CHANGELOG.md
		6ae64e247 registry: Fix panic when server is unreachable
		5c619ca1b website: Remove links to the getting started guide's old location
		06275647e Update CHANGELOG.md
		d5f9411f5 command: Fix bug when using terraform login on Windows
		4b6d06cc5 Update CHANGELOG.md
		dd01a3507 Update CHANGELOG.md
		225466bc3 Cleanup after v0.12.23 release
	Данной командой получил список коммитов между тэгами v0.12.23 и v0.12.24 (коммит с тэгом v0.12.23 в вывод не включен)

5. Найдите коммит в котором была создана функция func providerSource, ее определение в коде выглядит так func providerSource(...) (вместо троеточего перечислены аргументы).
ОТВЕТ:
commit 8c928e83589d90a031f811fae52a81be7153e82f
Author: Martin Atkins <mart@degeneration.co.uk>
Date:   Thu Apr 2 18:04:39 2020 -0700

Как получил ответ:
	5.1. admin@devops:~/.git/terraform$ git grep --break --heading -n -e 'func providerSource'
		provider_source.go
		23:func providerSource(configs []*cliconfig.ProviderInstallation, services *disco.Disco) (getproviders.Source, tfdiags.Diagnostics) {
	
	Данной командой получил имя файла provider_source.go, в котором присутствует описание искомой функции
	
	5.2. admin@devops:~/.git/terraform$ git log -L :providerSource:provider_source.go 
		commit 5af1e6234ab6da412fb8637393c5a17a1b293663
		Author: Martin Atkins <mart@degeneration.co.uk>
		Date:   Tue Apr 21 16:28:59 2020 -0700
		diff --git a/provider_source.go b/provider_source.go
		--- a/provider_source.go
		+++ b/provider_source.go
		@@ -20,6 +23,15 @@
		-func providerSource(services *disco.Disco) getproviders.Source {

		commit 92d6a30bb4e8fbad0968a9915c6d90435a4a08f6
		Author: Martin Atkins <mart@degeneration.co.uk>
		Date:   Wed Apr 15 11:48:24 2020 -0700
		diff --git a/provider_source.go b/provider_source.go
		--- a/provider_source.go
		+++ b/provider_source.go
		@@ -19,5 +20,6 @@
		 func providerSource(services *disco.Disco) getproviders.Source {
		commit 8c928e83589d90a031f811fae52a81be7153e82f
		Author: Martin Atkins <mart@degeneration.co.uk>
		Date:   Thu Apr 2 18:04:39 2020 -0700
		+++ b/provider_source.go
		+func providerSource(services *disco.Disco) getproviders.Source {
	Данной командой получил список коммитов, в которых изменялась искомая функция(часть вывода команды удалена для сокращения). Из вывода команды нашел первое упоминание искомой функции: +func providerSource(services *disco.Disco) getproviders.Source в коммите 8c928e83589d90a031f811fae52a81be7153e82f от 2 апреля 2020 года

6. Найдите все коммиты в которых была изменена функция globalPluginDirs.
ОТВЕТ:
78b12205587fe839f10d946ea3fdc06719decb05
52dbf94834cb970b510f2fba853a5b49ad9b1a46
41ab0aef7a0fe030e84018973a64135b11abcd70
66ebff90cdfaa6938f26f908c7ebad8d547fea17
8364383c359a6b738a436d1b7745ccdce178df47 (здесь она впервые определена)

Как получил ответ:
	6.1. admin@devops:~/.git/terraform$ git grep --break --heading -n -e 'globalPluginDirs'
		commands.go
		88:             GlobalPluginDirs: globalPluginDirs(),
		430:    helperPlugins := pluginDiscovery.FindPlugins("credentials", globalPluginDirs())

		internal/command/cliconfig/config_unix.go
		34:             // FIXME: homeDir gets called from globalPluginDirs during init, before
		
		plugins.go
		12:// globalPluginDirs returns directories that should be searched for
		18:func globalPluginDirs() []string {
	Данной командой получил список файлов и номера строк, в которых упоминается искомая функция
	6.2. git log -L 88:commands.go, git log -L 430:commands.go, git log -L 12:plugins.go, git log -L 12:plugins.go
	Данными командами просмотрел файлы, в которых упоминалась искомая функция,  начиная с нужных номеров строк, чтобы убедиться что там именно определение функции, а не ее вызов
	6.3. admin@devops:~/.git/terraform$ git log -L :globalPluginDirs:plugins.go
	Данной командой просмотрел все коммиты с изменениями в данной функции (вывод функции не приведен, т.к. его слишком многоa
)
7. Кто автор функции synchronizedWriters?
ОТВЕТ:
commit 5ac311e2a91e381e2f52234668b49ba670aa0fe5
Author: Martin Atkins <mart@degeneration.co.uk>

Как получил ответ:
	7.1. admin@devops:~/.git/terraform$ git log -SsynchronizedWriters
		commit bdfea50cc85161dea41be0fe3381fd98731ff786
		Author: James Bardin <j.bardin@gmail.com>
		Date:   Mon Nov 30 18:02:04 2020 -0500
		
		commit fd4f7eb0b935e5a838810564fd549afe710ae19a
		Author: James Bardin <j.bardin@gmail.com>
		Date:   Wed Oct 21 13:06:23 2020 -0400
		
		commit 5ac311e2a91e381e2f52234668b49ba670aa0fe5
		Author: Martin Atkins <mart@degeneration.co.uk>
		Date:   Wed May 3 16:25:41 2017 -0700
	Данной командой нашел все коммиты, где упоминалась искомая функция
	7.2. Команадами git checkout по-очереди переключался по найденным коммитам
	7.3. В каждом коммите командой git grep --break --heading -n -e 'synchronizedWriters' нашел файлы, где упоминалась искомая функция
	7.4. admin@devops:~/.git/terraform$ git log -L :synchronizedWriters:synchronized_writers.go
		commit 5ac311e2a91e381e2f52234668b49ba670aa0fe5 (HEAD)
		Author: Martin Atkins <mart@degeneration.co.uk>
		Date:   Wed May 3 16:25:41 2017 -0700
		diff --git a/synchronized_writers.go b/synchronized_writers.go
		--- /dev/null
		+++ b/synchronized_writers.go
		@@ -0,0 +15,12 @@
		+func synchronizedWriters(targets ...io.Writer) []io.Writer {
		+       mutex := &sync.Mutex{}
		+       ret := make([]io.Writer, len(targets))
		+       for i, target := range targets {
		+               ret[i] = &synchronizedWriter{
		+                       Writer: target,
		+                       mutex:  mutex,
		+               }
		+       }
		+       return ret
		+}
		+
		Данной командой нашел коммит в котором впервые была инициализирована искомая функция, здесь же посмотрел автора коммита



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



