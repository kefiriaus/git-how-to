git-howto для CentOS
====================

Установка имени и электронной почты
git config --global user.name "Your Name"
git config --global user.email "your_email@whatever.com"

Параметры установки окончаний строк
git config --global core.autocrlf input
git config --global core.safecrlf true

Создание репозитория
mkdir hello
cd hello
touch hello.html
git init

Добавление страницы в репозиторий
git add hello.html (Можно 'git add .' для добавление всех файлов каталога в репозиторий)
git commit -m "First Commit"

Проверка статуса репозитория
git status

Добавление изменений в репозиторий
git add hello.html
git status

Коммит изменений
git commit = переход к созданию комментария в редакторе
-m = вывод комментария в командной строке

История изменений
git log

Однострочная история изменений
git log --pretty=oneline

немного вариантов
git log --pretty=oneline --max-count=2
git log --pretty=oneline --since='5 minutes ago'
git log --pretty=oneline --until='5 minutes ago'
git log --pretty=oneline --author=<your name>
git log --pretty=oneline --all

Удобный вывод истории изменений
git log --pretty=format:"%h %ad | %s%d [%an]" --graph --date=short

Алиасы и шорткаты для команд git в файле ~/.gitconfig
[alias]
  co = checkout
  ci = commit
  st = status
  br = branch
  hi = log --pretty=format:\"%h %ad | %s%d [%an]\" --graph --date=short
  type = cat-file -t
  dump = cat-file -p
  
Алиасы для bash в файле ~/.bashrc
alias gs='git status '
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
alias gdump='cat-file -p'

Переход/Возврат к комиту/тегу/ветке
git checkout коммит|тег|ветка




