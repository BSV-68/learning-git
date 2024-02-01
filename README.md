# Основы работы с GIT  

Яндекс Практикум  

---

## Инициализируем репозиторий (th2-lesson1.md)  

- Сделать папку репозиторием — `git init`  
- «Разгитить» папку, если что-то пошло не так, — `rm -rf .git`  
- Проверить состояние репозитория — `git status`  

---

## Добавляем файлы в репозиторий (th2-lesson2.md)  

- Подготовить файлы к сохранению — `git add`

> - Команда `git add <file-name>...` позволяет подготовить файл к сохранению.  
> - Команда `git add --all` подготовит к сохранению сразу все файлы.  
> - С помощью `git add .` можно добавить в репозиторий текущую папку со всеми файлами.  

---

## Делаем первый коммит (th2-lesson3.md)  

- Выполнить коммит — `git commit`  
- Ещё раз о разнице между `git add` и `git commit`  

---

## Просматриваем историю коммитов (th2-lesson4.md)  

- Просмотреть историю коммитов — `git log`  

---

## Что такое SSH. Генерируем SSH-ключ (th4-lesson1.md)  

- Что такое SSH  
- Проверка наличия SSH-ключа  
- Инструкция по генерации SSH-ключа  

---

## Привязываем SSH-ключ к GitHub (th4-lesson2.md)  

- Инструкция по связыванию SSH-ключа и GitHub-аккаунта  

---

## Связываем локальный и удалённый репозитории (th4-lesson3.md)  

- Привязать удалённый репозиторий к локальному — `git remote add`  
- Убедиться, что репозитории связаны, — `git remote -v`  

---

## Синхронизируем локальный и удалённый репозитории (th4-lesson4.md)  

- Основная ветка  
- Отправить изменения на удалённый репозиторий — `git push`  
- Работа с графическим интерфейсом GitHub  

__Теперь ваши изменения могут увидеть те, кому вы отправите *ссылку на проект*!__  

---

## Хеш — идентификатор коммита (th5-lesson1.md)  

- Что такое хеш. Хеширование коммитов  
- Хеш — основной идентификатор коммита  

---

## Исследуем лог (th5-lesson2.md)  

- Элементы описания коммита  
- Получить сокращённый лог — `git log --oneline`  

---

## HEAD — всему голова (th5-lesson3.md)  

- Файл HEAD  

---

## Статусы файлов в Git (th5-lesson4.md)  

- Статусы *untracked*/*tracked*, *staged* и *modified*  
- Про `staged` и `modified`  
- Типичный жизненный цикл файла в Git  

---

## Как читать `git status` (th5-lesson5.md)  

- Какие состояния показывает `git status`  
- Подготавливаем репозиторий  
- Типичные варианты вывода `git status`  

---

## Оформление сообщений к коммитам (th6-lesson1.md)  

- Зачем вообще писать сообщения  
- Стили оформления  
- Корпоративный  
- Conventional Commits  
- GitHub-стиль  

---

## Практическая работа №2. Дополняем шпаргалку (th6-lesson2.md)  

---
---
