## Комманды npm, которые нам пригодятся :


`npm install npm@latest -g` - node установить последнюю версию:  
`npm update npm -g`  - обновить node  
`npm list --depth=0` - список установленных пакетов  
`npm outdated --depth=0` - список установленных пакетов требующих обновления  

`npm list` - список всех установленных пакетов  

`npm -g ls --depth=0` - список глобально установленных пакетов  
`npm outdated` - проверить, не устарели ли пакеты  
`npm update gulp` - обновление версий плагинов  
`npm init` - создать package.json  
`npm install package_name` - установить пакет (package_name - название нужного пакета)  
`npm install package_name --save-dev` - установить пакет и вносит запись о нем в package.jsonв секцию devDependencies  
`npm uninstall package_name` - удаление пакета  
`npm install` - установить все пакеты, перечисленные в package.json  
>Перед запуском в продакшн **npm shrinkwrap** - фиксируем версии пакетов,теперь **npm install** будет устанавливать именно их и вы будете уверены что все будет работать как надо  


### Сокращения
---
```
-v: --version
-g: --global
-S: --save
-D: --save-dev
-y: --yes
-n: --yes false
```
[установка Gulp](https://simplamarket.com/blog/ispolzovanie-gulp-chast-1---ustanovka)
**Заметки по терминалу**  
---  
`~/.gitconfig` - глобальный конфиг git  
  
`echo test.txt` - создаёт файл "test.txt"  
`test.txt echo change > test.txt` - добавляет слово change в файл test.txt  
`touch test.txt` - создать файл  
`mkdir block`  - создать папку 'block'  
`mkdir block/{1,2,3} ` -	создать папки 1,2 и 3 в папке 'block'  
`rm [путь/имя файла]` - удаляет файл  
		**создание проекта**
		**создаем конфигурации**
  
`.gitignore` - файл с списком игнорируемых файлов  
`git config --global user.name "Poliakh Roman"`  
`git config --global user.email "r.poliakh@gmail.com"`  
  
**запускаем в папке проекта**
`git init` - инициализация проекта  
`git config user.name "test User"`  
`git config user.email "test@litle.com"`  
		
		
### --- alias ---
---
`git config --global alias.st status` - __"git status"__  по ключу  __"git st"__  
  
`git config --global alias.unstage 'reset HEAD --'`  
`git reset HEAD -- fileA`  


### ---инидексация---

`git -a -m"[masage]"`  
`git add .` - индексирование  всех файлов  
`git add [имя файла]` - индексирование файла  
`git rm --cached [имя файла]` - исключить индексирование файла  
`git rm -r --cached [folder_name]` - удаление папки из индексирования  
  
`git commit -a -m"[masage]"` - коммит всех файлов без предварительной индексации (без add)  
`git commit -m"[masage]"` - добавить коммит  
`git commit --amend` - перезапись последнего коммита  
  
`git diff` - показывает проиндексированные изменения  
`git ls-files` - проиндексированные файлы  
`git diff --cached || git diff --staged` - покажет непроиндексированные изменения  
`git clean -f -d` - удаление всех неотслеживаемых файлов  
  
`git checkout --[имя файла]`- восстановить последний коммит  
`git checkout [хешкод]` - переход к коммиту  
  
`git help [key]` - отправка на страницу справки по ключику, например  "git help log"  

### --- логи ---

`git log` - просмотр истории коммитов  
`git log --pretty=format:"%h - %an, %ar : %s"` - вывод информации хешкод - имя атвора, когда сделано : комментарий  
`git log --pretty=oneline` - выводит коммиты строками  
`git log --pretty=oneline --author ="[имя юзера]"` - выводит коммиты строками  
`git log --pretty=format:'%h %ad | %s%d' --date=short` - клевый шаблон  
`git log --since=weeks` - лог за последние две недели  
`git log -p -2` - показать изменения последних двух коммитов  
`git log -p --word-diff ` - толком не понял что отобразить, что-то там с разницей в коментах по слову  
`git log --stat` - log c списком измененных вайлов  
  
	
### ---замена редактора для коммита---

`git config --global core.editor "'C:\Users\Roman\Downloads\emacs-26.1-x86_64\bin\emacs.exe' -multiInst -notabbar -nosession -noPlugin"`  
	
### ---ветки---
	
`git remote` - посмотреть удаленные ркпозитории  
`git remote -v` - посмотреть адрес репозитария  
`git remote add [сокращение] [url]` - добавление удаленного репозитория  
`git remote show` - инспеция  удаленного репозитория  
`git remote rename [oldName][newName]` - переименование удаленного репозитория  
`git remote rm [имя репа]` - удалить ссылку на ветку  
  
`git checkout -b [имя ветки]` - создание и переход в новую ветку  
`git branch [имя ветки]` - создание ветки  
`git branch` - просмоgit ыетр веток  
`git branch -v` - просмотр версии веток  
`git branch -d [имя ветки]` - удалить ветку  
`git git branch --merged || --no-merged` - позволяют осмотреть какие ветки слиты (или не слиты)  
`git checkout [имя ветки] ` - переход в ветку  
  
`git clone [url] -b [имя ветки]` - скпоирует нужную ветку  
`git clone -b [имя ветки] [url] .` - скопировать нужную ветку в текущую папку  
`git checkout -b  [имя ветки] origin/[имя ветки на реп]` - добавить нужную ветку  




`git clone -b [имя ветки] [url] .` - скопировать нужную ветку в текущую папку

`git checkout -b  [имя ветки] origin/[имя ветки на реп]` - добавить нужную ветку

### --- корзина ---

`git stash list` - отобразить список stash  
`git stash show` - показать последнее изменение  
`git stash apply` - показать последнее изменение  
`git stash drop` - удаляет последни stash  
`git stash clear` - удаляет все stash  
  
### --- плагин разрешения конфликтов---
  
`git config --global mergetool.kdiff3.cmd '"D:\\Program Files\\KDiff3\\kdifа3" $BASE $LOCAL $REMOTE -o $MERGED'` - подключение  плагина KDiff3 (предварительно установить в системе)  
		[Oтсюда(youtube)](https://youtu.be/xAKnRuYobdc?list=PLoonZ8wII66iUm84o7nadL-oqINzBLk5g&t=430)  
`git config --global merge.tool kdiff3` - указать чем программе разбирать конфликт  
`git mergetool` - для запуска kdiff3  
  
`git merge [имя ветки с которой объеденяемся]` - мерджим  
`git romote -v` - посмотреть версии репозиториев  
`git config --global push.default matching` - будет пушить те ветки которые уже есть в репозитории  
`git config --global push.default simple` - будет пушить только текущую ветку  
  
### ---возврат изменение---
`git reset --soft HEAD^` - отменит коммит но не изменения которые были сделаны  
`git reset HEAD  text.txt` - отмена индексирования  
>после сброса необходимо сделать   __git checkout[namefiles]__  для возврата состояния файла
>
`git revert --abort` - отмена отката  
		// редактор в консоли  
`vim [имя файлв для редактированя]` - для выхода набрать  :qa!  
  
`git mv [old name] [new name]` - переименование файла  
  
`git pull [remoteName] [branch]  --allow-unrelated-histories` - для слияние независимых веток одного проекта  


