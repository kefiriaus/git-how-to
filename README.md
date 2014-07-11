<h1>Git HowTo для CentOS</h1>

Описание самых основных моментов для начала работы с git

<h2>Установка имени и электронной почты</h2>
<pre>git config --global user.name "Your Name"
git config --global user.email "your_email@whatever.com"</pre>

<h2>Параметры установки окончаний строк</h2>
<pre>git config --global core.autocrlf input
git config --global core.safecrlf true</pre>

<h2>Создание репозитория</h2>
<pre>mkdir hello
cd hello
touch hello.html
git init</pre>

<h2>Добавление страницы в репозиторий</h2>
<pre>git add hello.html (Можно 'git add .' для добавление всех файлов каталога в репозиторий)
git commit -m "First Commit"</pre>

<h2>Проверка статуса репозитория</h2>
<pre>git status</pre>

<h2>Добавление изменений в репозиторий</h2>
<pre>git add hello.html
git status</pre>

<h2>Коммит изменений</h2>
<pre>
#переход к созданию комментария в редакторе
git commit
#вывод комментария в командной строке
git commit -m 'название коммита'

#изменение существующего коммита
git add hello.html
git commit --amend -m "Add an author/email comment"
</pre>

<h2>История изменений</h2>
<pre>#история изменений
git log

#однострочная история изменений
git log --pretty=oneline

#немного вариантов
git log --pretty=oneline --max-count=2
git log --pretty=oneline --since='5 minutes ago'
git log --pretty=oneline --until='5 minutes ago'
git log --pretty=oneline --author=<your name>
git log --pretty=oneline --all

#удобный вывод истории изменений
git log --pretty=format:"%h %ad | %s%d [%an]" --graph --date=short
</pre>

<h2>Алиасы и шорткаты для команд git в файле ~/.gitconfig</h2>
<pre>[alias]
  co = checkout
  ci = commit
  st = status
  br = branch
  hi = log --pretty=format:\"%h %ad | %s%d [%an]\" --graph --date=short
  type = cat-file -t
  dump = cat-file -p
</pre>
  
<h2>Алиасы для bash в файле ~/.bashrc</h2>
<pre>alias gs='git status '
alias ga='git add '
alias gb='git branch '
alias gc='git commit'
alias gd='git diff'
alias go='git checkout '
alias gk='gitk --all&'
alias gx='gitx --all'
alias gh='git hi'
alias gt='git tag'
alias ght='git hi master --all'
alias gtype='cat-file -t'
alias gdump='cat-file -p'</pre>

<h2>Переход/Возврат к комиту/тегу/ветке</h2>
<pre>git checkout [hash]|[tag]|[branchname]</pre>

<h2>Работа с тегами</h2>
<pre>#создание тега
git tag [tagname]

#переключение по тегу
git checkout [tagname]

#переключение по тегу к предыдущей версии
git checkout [tagname]^
#аналогично
git checkout [tagname]~1

#просмотр тегов
git tag

#просмотр тегов в логах
git hi master --all

#удаление тега
git tag -d [tagname]
</pre>

<h2>Отмена изменений для файла hello.html</h2>
<pre>#отмена изменений в рабочем каталоге
git checkout hello.html

#отмена проиндексированных изменений
git reset HEAD hello.html
git checkout hello.html

#отмена коммита в локальном репозитории
git revert HEAD --no-edit
</pre>

<h2>Удаление коммита</h2>
<pre>#для того чтобы коммит не удалился сборщиком мусора ему нужно установить tag
git tag oops

#сброс коммита
git reset --hard [tagname]|[hash]

#показ удаленного коммита с тегом
git hi --all
</pre>

<h2>Перемещение файла в пределах репозитория</h2>
Переместить файл hello.html в каталог lib
<pre>
#средствами git
mkdir lib
git mv hello.html lib

#средствами OS
mkdir lib
mv hello.html lib
git add lib/hello.html
git rm hello.html
</pre>

<h2>Создание ветки в репозитории</h2>
<pre>git checkout -b [branchname]</pre>

<h2>Слияние веток</h2>
<pre>
#без конфликта
git checkout dev
git merge master
git hi --all

#решение конфликта вручную
git checkout dev
git merge master
git hi --all
Auto-merging lib/hello.html
CONFLICT (content): Merge conflict in lib/hello.html
Automatic merge failed; fix conflicts and then commit the result.

#необходимо отредактировать файл
vim lib/hello.html
git add lib/hello.html
git commit -m "Merged master fixed conflict."    
</pre>

<h2>Преобразование</h2>
<pre>
#сброс ветки dev до слияния
git checkout dev
git hi
git reset --hard [hash]

#сброс ветки master до конфликта
git checkout master
git hi
git reset --hard [hash]
git hist --all
</pre>

<h2>Перебазирование (rebase вместо merge)</h2>
<pre>
git checkout dev
git rebase master
git hi
</pre>

<h3>Rebase VS Merge</h3>
Конечный результат перебазирования очень похож на результат слияния. Ветка dev в настоящее время содержит все свои изменения, а также все изменения ветки master. Однако, дерево коммитов значительно отличается. Дерево коммитов ветки dev было переписано таким образом, что ветка master является частью истории коммитов. Это делает цепь коммитов линейной и гораздо более читабельной.

<h4>Когда использовать rebase, а когда merge?</h4>
Не используйте rebase:
<ol>
  <li>Если ветка является публичной и расшаренной. Переписывание общих веток будет мешать работе других членов команды.</li>
  <li>Когда <i>важна точная история</i> коммитов ветки (так как команда rebase переписывает историю коммитов).</li>
</ol>

Учитывая приведенные выше рекомендации, я предпочитаю использовать rebase для кратковременных, локальных веток, а merge для веток в публичном репозитории.

<h2>Клонирование репозитория</h2>
<pre>
git clone hello cloned_hello
</pre>

<h2>Имена удаленных репозиториев</h2>
<pre>
git remote

#более подробно
git remote show origin
</pre>

<h2>Локальные и удаленные ветки</h2>
<pre>
#локальные
git branch

#локальные и удаленные
git branch -a
</pre>

<h2>Извлечение изменений из удаленного репозитория</h2>
<pre>
cd ../cloned_hello
git fetch
git hist --all

#слияние с локальным репозиторием
git merge origin/master

#или вместо fetch и merge
cd ../cloned_hello
git pull
git hist --all
</pre>

<h2>Добавление локальной ветки, отслеживающей изменения удаленной ветки</h2>
<pre>
git branch --track dev origin/dev
git branch -a
git hist --max-count=2
</pre>

<h2>Чистый репозиторий</h2>
<pre>git clone --bare hello hello.git</pre>

<h2>Добавление удаленного репозитория</h2>
<pre>
cd hello
git remote add shared ../hello.git
</pre>

<h2>Отправка изменений в удаленный репозиторий</h2>
<pre>
git checkout master
git add README
git commit -m "Added shared comment to readme"
git push shared master
</pre>

<h2>Извлечение изменений с удаленного репозитория</h2>
<pre>
cd ../cloned_hello
git remote add shared ../hello.git
git branch --track shared master
git pull shared master
cat README
</pre>

<h2>Запуск git сервера</h2>
<pre>
#из рабочей директории
git daemon --verbose --export-all --base-path=.
</pre>

<h2>Подключение к git серверу</h2>
<pre>
git clone git://localhost/hello.git network_hello
cd network_hello
ls
</pre>
