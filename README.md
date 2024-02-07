# Основы работы с GIT  

Яндекс Практикум  

---

## Командная строка  (00_terminal_th3.md)  

- Инструкция по установке для пользователей Windows;  
- Первый запуск Git Bash.  

## Первый коммит  (01_1st-commit_th2.md)  

### Инициализируем репозиторий  

- Сделать папку репозиторием — `git init`  
- «Разгитить» папку, если что-то пошло не так, — `rm -rf .git`  
- Проверить состояние репозитория — `git status`  

### Добавляем файлы в репозиторий  

- Подготовить файлы к сохранению — `git add`

> - Команда `git add <file-name>...` позволяет подготовить файл к сохранению.  
> - Команда `git add --all` подготовит к сохранению сразу все файлы.  
> - С помощью `git add .` можно добавить в репозиторий текущую папку со всеми файлами.  

### Делаем первый коммит  

- Выполнить коммит — `git commit`  
- Ещё раз о разнице между `git add` и `git commit`  

### Просматриваем историю коммитов  

- Просмотреть историю коммитов — `git log`  

---

## Синхронизация репозиториев  (02_GitHUB_th4.md)  

### Что такое SSH. Генерируем SSH-ключ  

- Что такое SSH  
- Проверка наличия SSH-ключа  
- Инструкция по генерации SSH-ключа  

### Привязываем SSH-ключ к GitHub  

- Инструкция по связыванию SSH-ключа и GitHub-аккаунта  

### Связываем локальный и удалённый репозитории  

- Привязать удалённый репозиторий к локальному — `git remote add`  
- Убедиться, что репозитории связаны, — `git remote -v`  

### Синхронизируем локальный и удалённый репозитории  

- Основная ветка  
- Отправить изменения на удалённый репозиторий — `git push`  
- Работа с графическим интерфейсом GitHub  

__Теперь ваши изменения могут увидеть те, кому вы отправите *ссылку на проект*!__  

---

## Навигация по коммитам  (03_Nav-through-commits_th5)  

### Хеш — идентификатор коммита  

- Что такое хеш. Хеширование коммитов  
- Хеш — основной идентификатор коммита  

### Исследуем лог  

- Элементы описания коммита  
- Получить сокращённый лог — `git log --oneline`  

### HEAD — всему голова  

- Файл HEAD  

### Статусы файлов в Git  

- Статусы *untracked*/*tracked*, *staged* и *modified*  
- Про `staged` и `modified`  
- Типичный жизненный цикл файла в Git  

### Как читать `git status`  

- Какие состояния показывает `git status`  
- Подготавливаем репозиторий  
- Типичные варианты вывода `git status`  

---

## Работа над ошибками в коммитах  (04_correct-err-in-commits_th6)  

### Оформление сообщений к коммитам  

- Зачем вообще писать сообщения  
- Стили оформления  
- Корпоративный  
- Conventional Commits  
- GitHub-стиль  

### Практическая работа №2. Дополняем шпаргалку  

- Подсказка: как сделать mermaid-схему  

### Как исправить коммит  

- Подготавливаем репозиторий
- Дополнить коммит новыми файлами — `git commit --amend --no-edit`  
- Изменить сообщение коммита — `git commit --amend -m "Новое сообщение"`  
- Случилось страшное: открылся редактор... :) .  

### Как откатиться назад, если «всё сломалось»  

- Выполнить unstage изменений — `git restore --staged <file>`  
- «Откатить» коммит — `git reset --hard <commit hash>`  
- «Откатить» изменения, которые не попали ни в __staging__, ни в коммит, — `git restore <file>`  

---

## Просмотр изменений. Игнорирование файлов  (05_file-changes-and-ignoring_th7)  

### Просматриваем изменения в файлах  

- Подготавливаем репозиторий (teremok)
- Селим мышку-норушку  
- Просматриваем изменения в `staging area`  

### Сопоставляем коммиты  

- Дописываем строку в файл  
- Селим всех остальных  
- Сравниваем коммиты  
- Порядок аргументов `git diff`  

### Игнорирование файлов в Git  

- Как заполнить `.gitignore`  
- Комментарий  
- Просто название файла  
- Звёздочка (`*`)  
- Вопросительный знак (`?`)  
- Квадратные скобки (`[…]`)  
- Слеш (`/`)  
- Парные звёздочки (`**`)  
- Восклицательный знак (`!`)  
- Пример файла `.gitignore`  
- `.gitignore` и `git status`  

---

## Копирование репозиториев  (06_copying-repositories_th1)  

### Клонируем репозиторий  

- Клонировать репозиторий — `git clone`  

### Выполняем Fork  

- Что такое Fork  
- Применяем Fork  
- Задание для самостоятельной работы  

### Практическая работа №1. Скачиваем репозиторий мечты  

- Совы и жаворонки  
- Что нужно сделать  

---

## Ветки: создание, навигация, сравнение  

- Зачем нужны ветки;  
- Просмотреть ветки проекта — `git branch`;  
- Дополняем ветку;  
- Создать ветку — `git branch <название_ветки>`;  
- Как назвать новую ветку;  
- Переключиться на другую ветку — `git checkout <название_ветки>`;  
- Создать ветку и сразу переключиться на неё — `git checkout -b <название_ветки>`;  
- На какой коммит указывает `bugfix/fix-branch`;  
- Сравнить ветки — `git diff <название_ветки1> <название_ветки2>`;  
- Суффикс навигации `~`.  

---

## Слияние и удаление веток  (08_Merging-and-deleting-branches_th4)  

### Объединяем и удаляем ветки  

- Выполнить слияние — `git merge <название_ветки>`;  
- Удалить ветку после объединения — `git branch -D <название_ветки>`;  
- Задание для самостоятельной работы.  

### Что такое конфликт  

- Знакомьтесь: конфликт;  
- Как разрешать конфликты: общие рекомендации.  

## Работа с ветками в удалённом репозитории  (09_Working-with-branches-on-GitHub_th5)  

- Отправить локальную ветку в удалённый репозиторий — `git push`  

### Создаём pull request  

- Создаём *pull request*  
- Из чего состоит *pull request* и чем он может обернуться  
- Делаем *pull request*  
- Забрать изменения из удалённого репозитория — `git pull`  

