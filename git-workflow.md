#FWT: Git Standart

##Workflow

####1. Устанавливаем [git flow](https://danielkummer.github.io/git-flow-cheatsheet/index.ru_RU.html)
* `git flow init` - все по умолчанию (жмем enter)
* Запушить 2 ветки: `master` и `develop`

####2. Начало работы над задачей
* Перейти на `develop`
* Создать feature - `git flow feature start [name]`
* Работать только в своей ветке `feature/[name]`

####3. Завершении работ над задачей
* Опубликовать ветку(если не сделали раньше) - `git flow feature publish`
* **Отправить на ревью:**
* Cоздать pull-request из своей `feature/[name]` в `develop`
* Работать с замечаниями по ревью (Если на проекте нет рецензента, то рецензент - вы сами)

####4. Переход в статус Готово
* Получить статус Одобрено по ревью
* Смержить `feature` в `develop` - `git flow feature finish`
* Запушить `develop` - `git push`
* Приступить к новой задаче - п.1

###TL;DR
```
git checkout develop
git flow feature start [name]
//commits...
git flow feature publish (or git push)
//create PR
git flow feature finish
git push
```

###FAQ
>В каких случаях создавать отдельную ветку feature?
* Под каждую отдельную задачу: 1 задача = 1 ветка.

>Что делать, если текущая задача ждет ревью, а хочется начать делать следующую?
1. Первое - самому просмотреть свой PR.
2. Второе - перейти на `develop` и начать делать новую задачу по тому же workflow.  
   **Нельзя:** начинать делать новую задачу в той же ветке  
   **Нельзя:** стартовать новую `feature` **НЕ** от `develop`

>Что делать, если все-таки начали работу над новой задачи из старой ветки?
```
git stash
git flow feature start <name> <from_which_branch>
git stash pop
```

###Время релиза
1. Перейти на `develop`
2. Создать ветку релиза - `git flow release start 1.0`  
   Название версии без префикса  
   Стандарт версионирования определяется на проекте(семвер, etc.)
4. Производите настройку для прода (например: `npm run prod`)
5. Закрываете релиз - `git flow release finish -m "desc"`  
   _desc_ - описание основных изменений, которые были выполнены в данном релизе
6. Пушите `develop` вместе с тэгами - `git push --tags`
7. Пушите master - `git checkout master && git push`

####Наименование веток
**Case:** kebab-case  
**Пример:** feature/nova-multisecelt

//TODO