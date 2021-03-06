# Справочник по GIT
## Требования к именам коммитов
> Названия коммитов должны быть согласно: https://www.conventionalcommits.org/en/v1.0.0/

> Должен использоваться present tense ("add feature" not "added feature")

> Должен использоваться imperative mood ("move cursor to..." not "moves cursor to...")

## Примеры имен коммитов

> init: - используется для начала проекта/таска. Примеры:

```
init: start mentor-dashboard task
```

> feat: - это реализованная новая функциональность из технического задания (добавил поддержку зумирования, добавил footer, добавил карточку продукта). Примеры:

```
feat: add basic page layout
feat: implement search box 
feat: implement request to youtube API
```

> fix: - исправил ошибку в ранее реализованной функциональности. Примеры:

```
fix: implement correct loading data from youtube
fix: change layout for video items to fix bugs
```

> refactor: - новой функциональности не добавлял / поведения не менял. Файлы в другие места положил, удалил, добавил. Изменил форматирование кода. Примеры:

```
refactor: change structure of the project
refactor: rename vars for better readability
refactor: apply eslint
refactor: apply prettier
```

> docs: - используется при работе с документацией/readme проекта. Примеры:

```
docs: update readme with additional information
docs: update description of run() method
```

# Команды GIT. Ветки
## Создание и переключение
Посмотреть текущую ветку
```sh
	git branch
```

Посмотреть версию текущей ветку
```sh
	git branch -v
```

Создать новую ветку под названием "newBranch"
```sh
	git branch newBranch
```

Для переключения на новую ветку необходимо использовать:
```sh
	git checkout newBranch
```

Создать новую ветку и переключиться на нее:
```sh
	git checkout -b newBranch2
```

## Команда checkout при незакоммиченных изменениях

Для того, чтобы переключиться на master игнорируя все сделанные изменения в newBranch2.

```sh
	git checkout --force master
```

Также применяют для возрврата на рабочее состояние. Удалить все изменения и перейти к последней рабочей версии.
```sh
	git checkout -f HEAD
```


Сохранить все не закоммиченные изменения в истории.
```sh
	git stash
```
Далее можно переходит на Мастер. но если потом нужно будет вернуть закоммиченные изменения из истории.
можно использовать команду:
```sh
	git stash pop
```

## Создание новой ветки из последних коммитов, передвижение веток

Для того, чтобы вернуться на прежние версии Master
необходимо:

> 1. создать новую ветку FIX для сохранения в нее текущих изменений. 
```sh
	git branch fix
```

> 2. перейти наветку fix 
```sh
	git checkout fix
```

> 3. переходим на мастер с указанием места из истории.

```sh
	git branch -f master 54a4 - 'это название места куда необходимо переключиться'  
```
или

```sh
	git checkout -В master 54a4  
```

> 4. Если необходимо обратно вернуться в FIX

```sh
	git branch -f master fix  
```

## Состояние отделённой HEAD

 переместить HEAD в указанное состояние "1977" адрес из истории.
```sh
	git checkout 1977 
```


```sh
	git cherry-pick 1977 
```


## Восстановление предыдущих версий файлов

Восстановление предыдущих версий
```sh
	git checkout -название ссылки - название файла
	 git checkout master index.html
```

Сброс выбранного индекса файла на самый поздний индекс.
удаление предыдущих версий и возврат в текущее.
```sh
	git reset index.html
```

## Просмотр истории и старых версий

```sh
	git log
```

```sh
	git log --oneline
```
посмотреть историю ветки Master
```sh
	git log master --oneline
```
посмотреть историю ветки fix
```sh
	git log fix --oneline
```


посмотреть историю коммита
```sh
	git show -индекс коммита
```

посмотреть историю ветки на определенный шаг назад ~ 2
```sh
	git show HEAD~2
	git show @~2
	git show master~2
```

посмотреть историю файла  на определенный шаг назад ~
```sh
	git show @~:index.html
```

```sh
	git show :/название коммита
```

## Слияние перемоткой
переходим с ветки fix на мастер
```sh
	git checkout master
```

переносим все изменения с ветки  fix на ветку master. делаем слияние веток в одну.
```sh
	git merge fix
```
или
```sh
	git checkout -B master fix
```


В случае если необходимо обратно вернуть мастер на исходную
```sh
	cat .git/ORIG_HEAD
	git branch -f master ORIG_HEAD
```

переходим на мастер	
```sh
	git checkout master
```

## Удаление веток
для удаления ветки которая уже слита в Мастер, применяют команду:
```sh
	git branch -d fix
```

для удаления ветки которая не нужна
```sh
	git branch -D fix
```

Для отмены удаления ветки
```sh
	git branch fix -адрес-индекса
	git branch fix 'HEAD@{7}'
```

## Лог ссылок: reflog

```sh
	git reflog

	git reflog --date=iso
```

## Сборка мусора

```sh
	git gc

	git filter-branch

	git reflog expire --expire=now --all

	git gc --prune=now
```

## Теги, основные действия с тегами
создание тэга "v1.0.0" в коммите 54a4
```sh
	git tag v1.0.0 54a4
```
просмотр всех тэгов
```sh
	git tag
```
просмотр тэгов с содержанием 54a4
```sh
	git tag --contain 54a4
```

просмотр тэгов с сообщениями
```sh
	git tag -n
```

просмотр тэгов с сообщениями
```sh
	git tag --oneline v1.1.0
```

фильтр для просмотра тэгов с определенным названием
```sh
	git tag -n -l 'v1.1*'
```

просмотр аннотированных тэгов
```sh
	git show v1.1.0
```

## Использование тегов для экспорта с describe, archive
получить описание тэгов
```sh
	git describe 54a4
```

показать описание ближайшего тэга
```sh
	git describe
```

архивировать коммит
	git archive -o /tmp/v1.1.0-2-54a4.zip HEAD
```
