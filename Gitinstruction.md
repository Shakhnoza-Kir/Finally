# Инструкция для работы с GIT

## Что такое Git?
Git - это одна из реализаций распределенных систем контроля версий, имющая как локальная, так и удаленные репозитории. Является самой популярной реализацией систем контроля версий в мире. 

## Подготовка репозитория.

Для создания репозитория необходимо выполнить команду *git init в папке репозиторием и у вас создастся репозиторий (появится скрытая папка .git)

## Создание коммитов. 

### Git add
Для добавления изменений в коммит используется команда *git add. Чтобы использовать команду *git add напишите git add <имя файла>.

### Просмотр состояния репозитория 
Для того, чтобы посмотреть состояния репозитория используется команда *git status. Для этого необходимо в папке с репозиторием написать *git status и вы увидите были ли изменения в файлах или их не было.

### Создание коммитов

Для того чтобы создать коммит (сохранение) необходимо выполнить команду *git commit. Выполняется она так: git commit -m <название выполненной команды>


## Клонирование существующего репозитория.

При работе в команде, разрабатываемые проекты часто размещают на сервере. Это один из самых распространенных сценариев. При этом, нужно получить копию проекта последней версии на свой компьютер, чтобы далее вносить в него свой вклад.

В качестве примера мы будем рассматривать проект, который создан на ресурсе https://github.com/ . После регистрации на сайте и подтверждения по e-mail нужно создать новый репозиторий *create a new repository.

### Тип репозитория:

публичный (public) – доступ открыт для любого пользователя, однако права на редактирование выдает владелец проекта;

приватный/скрытый (private) — проект виден только владельцу, другие участники добавляются вручную.

При этом, работаем с командой *git clone. 

*git clone https://github.com/<название ссылки>.


## Сохранение снимков и просмотр статуса проекта.

Сразу после клонирования все файлы проекта будут отслеживаемыми. Отредактировав их, индексируется (stage) и фиксируется (commit) правки, и так для каждой версии проекта.

При этом нужно внимательно следить, чтобы вспомогательные файлы, особенно объемные, оставались вне контроля версий. Если по недосмотру добавить их в коммит и отправить на сервер — вероятнее всего, ваши правки придется частично откатывать.

Проверить состояние файлов в рабочем каталоге можно командой git status. После клонирования консоль выведет примерно такую информацию:

On branch master
Your branch is up to date with ‘origin/master’.

nothing to commit, working tree clean

Для удаления ненужных файлов из репозитория можно использовать команду git rm <file-name>. Файл также пропадет из рабочего каталога. Выполнить коммит необходимо и в этом случае; до тех пор структура проекта не изменится.

## Файл .gitignore

В рабочий каталог могут попадать файлы, которые не хотелось отправлять на сервер. Это и документы с экспериментами или образцами, и автоматически генерируемые части проекта, актуальные только на нашем компьютере. Git может полностью игнорировать их, если создать в рабочем каталоге файл с названием .gitignore и внести в него все имена ненужных файлов и папок.

## Управление удаленными репозиториями.

Просмотреть список текущих онлайн-репозиториев можно командой git remote. Добавить другие — с помощью команды git remote add <shortname> <url>, например:


>git remote add myDemo https://github.com/DanZDev2/DemoApp
>git remote
myDemo
origin

## Отправка изменений в удаленный репозиторий (Push).

Команда для отправки изменений на сервер такова: git push <remote-name> <branch-name>. Если ваша ветка называется master, то команда для отправки коммитов станет такой:

> git push origin master
Она сработает, если у вас есть права на запись на том сервере, откуда вы клонировали проект. Также предполагается, что другие участники команды за это время не обновляли репозиторий.

## Получение изменений из репозитория (Pull).

Самый простой и быстрый способ получить изменения с сервера — выполнить команду git pull, которая извлечет (fetch) данные с сервера и попытается встроить/объединить (merge) их с вашей локальной версией проекта. На этом этапе могут возникать конфликты версий, когда несколько человек поработали над одними и теми же файлами в проекте и сохранили свои изменения. Избежать этого можно, если изолировать части проекта, поручив работу над одной частью только одному человеку. Разумеется, на практике это не всегда выполнимо, поэтому в Git есть инструменты для разрешения конфликтов версий. 

## Создание веток и переключение между ними.

Создадим две дополнительные ветки Dev и Test (например, одна может пригодиться для процесса разработки, а другая — для запуска в тестирование). Введем команду git branch <branch-name> дважды с разными аргументами: 

>git branch Dev
>git branch Test
Ветки созданы, но мы по-прежнему работаем в master. Для переключения на другую нужно выполнить git checkout <branch-name>:

>git checkout Dev

## Слияние веток (merge).

Работа над проектами часто ведется в несколько этапов, им могут соответствовать ветки (в нашем примере Dev → Test → master). Отдельные ветки могут создаваться для срочного исправления багов, быстрого добавления временных функций, для делегирования части работы другому отделу и т. д. Предположим, что нужно применить изменения из ветки Dev, внеся их в master. Перейдем в master и выполним команду git merge <source-branch>:

>git merge Dev

Изменения успешно перенесены. В наших упрощенных условиях команда завершилась без ошибок, не найдя конфликтов в файлах. Если же над общими участками какого-либо файла успели поработать несколько человек, с этим нужно разбираться вручную. При возникновении ошибок Git помечает общие части файлов из разных веток и сообщает о конфликте.git log

## Заключение.

Мы рассмотрели, как устанавливать и настраивать Git в различных ОС, создавать новые и клонировать существующие репозитории, получать и отправлять новые версии проекта, а также ознакомились с базовыми концепциями ведения веток.

Этой информации обычно хватает для повседневных задач, связанных с хранением рабочих проектов.

Главная отличительная черта Git состоит в подходе к обработке данных. Каждый раз при сохранении данных проекта (коммите) система фиксирует состояние файла (делает снимок) и создает ссылку на этот снимок. Последующие изменения отражаются через ссылки на более ранние версии файла. Нет необходимости снова сохранять файл целиком. К тому же, основываясь на контрольных hash-суммах, система снимков обеспечивает целостность всей истории изменений. На практике это означает, что невозможно (либо крайне трудно) полностью удалить данные из рабочего каталога и утратить к ним любой доступ. В большинстве случаев данные можно восстановить из ранней версии проекта.

Таким образом, систему контроля версий в Git проще всего представлять как поток снимков (сохраненных состояний проекта).

