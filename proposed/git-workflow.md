# FWT: Git Standart

## Workflow

#### 1. Устанавливаем [git flow](https://danielkummer.github.io/git-flow-cheatsheet/index.ru_RU.html)
* `git flow init -d` - все настройки по умолчанию
* Запушить 2 ветки: `master` и `develop`

#### 2. Начало работы над задачей
* Создать feature - `git flow feature start [name]`
* Работать только в своей ветке `feature/[name]`

#### 3. Завершении работ над задачей
* Опубликовать ветку _(если не сделали раньше)_ - `git flow publish`
* **Отправить на ревью:**
    * Создать pull-request из своей `feature/[name]` в `develop`
    * Работать с замечаниями по ревью 
    * Если на проекте нет рецензента, то рецензент - вы сами

#### 4. Переход в статус Готово
* Получить статус Одобрено по ревью
* Смержить `feature` в `develop` - `git flow feature finish`
    * Просто `git flow finish`, если находитесь на нужной ветке `feature`
* Запушить `develop` - `git push`
* Приступить к новой задаче - п.2

### TL;DR
```
git flow feature start [name]
// commits...
git flow publish
// create PR
git flow finish
git push
```

### FAQ
>В каких случаях создавать отдельную ветку feature?
* Под каждую отдельную задачу: 1 задача = 1 ветка.

>Что делать, если текущая задача ждет ревью, а хочется начать делать следующую?
1. Самому просмотреть свой PR.
2. Перейти на `develop` и начать делать новую задачу по тому же workflow.  
   **Нельзя:** начинать делать новую задачу в той же ветке  
   
>Что делать, если все-таки начали работу над новой задачи из старой ветки?
```
git stash
git flow feature start <name> <from_which_branch>
git stash pop
```

### Время релиза
1. Перейти на `develop`
2. Создать ветку релиза - `git flow release start 1.0`  
   * Название версии без префикса  
   * Стандарт версионирования определяется на проекте(семвер, etc.)
4. Произвести настройку для прода (например: `npm run prod`)
5. Закрыть релиз - `git flow release finish -m "desc"`  
   * _desc_ - описание основных изменений, которые были выполнены в данном релизе
6. Запушить `develop` вместе с тэгами - `git push --tags`
7. Запушить master - `git checkout master && git push`

## Наименование веток
**Case:** kebab-case  
**Пример:** `feature/nova-select`

> TODO
- [ ] Branch names
- [ ] Commit messages
