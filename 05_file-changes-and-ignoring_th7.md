# Просмотр изменений. Игнорирование файлов  

__*Тема 7/8 (Просмотр изменений. Игнорирование файлов) Урок 1/4*__  

# Просматриваем изменения в файлах  

При работе с Git часто нужно узнать, что конкретно изменится или уже изменилось после того или иного коммита. Вот примеры таких ситуаций:  

- Вы собираетесь сделать коммит, но хотите проверить (или перепроверить), какие именно изменения в него попадут.  
- Вчера ваш коллега сделал коммит с сообщением `small fix` (англ. «небольшое исправление»), после чего тесты проекта начали «падать». Чтобы разобраться в ситуации, нужно посмотреть, что изменилось в этом коммите.  

Всё это позволяет делать команда `git diff` (от англ. *difference* — «отличие», «разница»). О её возможностях пойдёт речь в этом и следующем уроках.  

## Подготавливаем репозиторий  

Историю масштабных и неожиданных изменений как нельзя лучше иллюстрирует сказка «Теремок». Создайте вместе с нами следующий репозиторий.

```text
$ mkdir ~/dev/teremok
$ cd ~/dev/teremok
$ git init
# пропустим вывод git init, тут он не важен 
```

Добавьте файл `teremok.txt` и запишите в нём состояние теремка.  

```text
$ touch teremok.txt
# отредактируйте файл teremok.txt, добавьте в него строки:
# Теремок стоит, и в нём:
# никого нет
$ cat teremok.txt
Теремок стоит, и в нём:
никого нет 
```

Теперь выполните коммит.

```text
git add teremok.txt
git commit -m "Исходное состояние теремка" 
```

## Селим мышку-норушку  

Откройте и отредактируйте файл `teremok.txt`, чтобы вместо `никого нет` стало `Мышка-норушка`. Сохраните файл, но не делайте коммит. Затем воспользуйтесь командой `git status`, чтобы посмотреть, что происходит с файлами.  

Видно, что в теремке произошли какие-то изменения, но не видно, какие именно. Запустите `git diff`, чтобы выяснить детали. Эта команда сравнит последнюю закоммиченную версию файла `teremok.txt` с текущей (изменённой) версией.  

Самое важное `git diff` выводит в конце:  

- красный цвет строки `никого нет` значит, что эта строка была удалена;  
- зелёный цвет строки `Мышка-норушка` значит, что она была добавлена.  

Не все консоли умеют выводить цвета, поэтому строки помечаются не только цветом, но и знаком `-` или `+`. *Минус* — это удалённые строки, *плюс* — это добавленные.  

Коротко разберём остальные строки вывода команды:  

- Первые две строки (`diff --git a/... b/...` и `index 901da07..ac459e1 100644`) — это низкоуровневая техническая информация. Мы не будем на ней останавливаться.  
- Строки `--- a/teremok.txt` и `+++ b/teremok.txt` говорят, что дальше будет выведен результат сравнения файлов `a/teremok.txt` и `b/teremok.txt` — исходной и текущей версий.  
- Строка `@@ -1,2 +1,2 @@` сообщает, какие строки файла попали в сравнение. Выражение `1,2` (неважно, с плюсом или с минусом) говорит, что были использованы две строки, начиная с первой. Если бы было, например, написано `+15,7`, это значило бы, что в сравнении участвуют __7__ строк, начиная с __15-й__.  

Выражение со знаком минус (`-1,2`) относится к __«оригинальной»__ версии файла (`a/teremok.txt`), а со знаком плюс (`+1,2`) — к __«изменённой»__ (`b/teremok.txt`).  

> 💡 __Зачем вообще указывать, какие строки файла участвуют? Разве сравниваются не все строки?__  
    Указывается не то, какие строки сравнивались, а какие попали в вывод команды `git diff`. Это важно для больших файлов. Если, например, сравнить два файла по __1000__ строк, в которых отличается только __500-я__ строка, то `git diff` выведет порядка __10__ строк (что-нибудь вроде `@@ -495,10 +495,10 @@` — с 495-й по 505-ю). Иначе пришлось бы читать всю тысячу. 10 строк вместо одной нужно, чтобы было проще понять контекст изменения.  

## Просматриваем изменения в `staging area`  

Подготовьте мышку-норушку к коммиту, но пока не выполняйте его.  

```text
git add teremok.txt 
```

Вам наверняка знакома ситуация: вы выключили плиту и утюг, но вернулись проверить, всё ли точно в порядке. Сделайте что-то похожее с вашими изменениями: перепроверьте, что всё на месте.  

```text
$ git diff
# команда не выведет ничего! 
```

Не волнуйтесь: изменения не потерялись. Просто по умолчанию команда `git diff` не показывает изменения в `staged`-файлах — только в `modified`.  
Чтобы всё-таки просмотреть изменения в `staged`, нужно использовать флаг `--staged`: `git diff --staged`.  

Все хорошо, изменения на месте! Было `никого нет`, а стало `Мышка-норушка`. Сделайте коммит.  

```text
git commit -m "Поселить мышку-норушку" 
```

Теперь вы можете просматривать изменения в файлах. Если коротко:  

- Команда `git diff` сравнит последнюю закоммиченную версию файла с той, что находится в состоянии `modified`.  
- Команда `git diff --staged` покажет изменения в `staged`-файлах относительно последних закоммиченных версий.

---

__*Тема 7/8 (Просмотр изменений. Игнорирование файлов) Урок 2/4*__  

# Сопоставляем коммиты  

В этом уроке вы допишете сказку «Теремок», а также научитесь сопоставлять коммиты. Если вдруг на каком-то этапе работы возникнет проблема, это поможет разобраться, что конкретно изменилось в одном коммите по сравнению с другим.  

## Дописываем строку в файл  

Чтобы продолжить сказку, вам нужно будет дописывать новые строки в конец файла `teremok.txt`. Для этого подходит команда `echo` (англ. «эхо»). Разберём её.  

Сама по себе эта команда просто выводит в консоль то, что ей передали в качестве параметра.

```text
$ echo "Привет!"
Привет! 
```

Но если скомбинировать `echo` с символами перенаправления вывода `>>` (два знака «больше»), то всё, что должно было попасть на экран, вместо этого будет записано в файл.  

```text
$ cat file.txt
Первая строка файла

$ echo "Вторая строка файла" >> file.txt
$ cat file.txt
Первая строка файла
Вторая строка файла 
```

Оператор `>>` — это возможность командной строки (__Bash__). Его можно использовать не только с `echo`, но и с любой другой командой, которая выводит что-то на экран.  

Одинарный символ `>` тоже перенаправит вывод команды в файл, но перед этим сотрёт содержимое файла, то есть перезапишет файл целиком.  

```text
$ cat file.txt
Первая строка файла
$ echo "Новая строка" > file.txt
$ cat file.txt
Новая строка
```

Обратите внимание, что после использования символа `>` `Первая строка файла` исчезла.  

## Селим всех остальных  

Вернёмся к сказке. Сделайте по коммиту для каждого нового персонажа. Используйте команду `echo` или дописывайте строки вручную в любом текстовом редакторе.  

```text
$ echo "Лягушка-квакушка" >> teremok.txt
$ git add teremok.txt
$ git commit -m "Поселить лягушку-квакушку"
# пропускаем вывод команды commit

$ echo "Зайчик-побегайчик" >> teremok.txt
$ git add teremok.txt
$ git commit -m "Поселить зайчика-побегайчика"

$ echo "Лисичка-сестричка" >> teremok.txt
$ git add teremok.txt
$ git commit -m "Поселить лисичку-сестричку"

$ echo "Волчок -- серый бочок" >> teremok.txt
$ git add teremok.txt
$ git commit -m "Поселить волчка -- серого бочка"

# Пришла очередь медведя косолапого.
# Как известно, конструкция теремка не была рассчитана на массу медведя
# и теремок развалился.
# Обратите внимание на одинарный символ >
$ echo "Теремок развален" > teremok.txt
$ git add teremok.txt
$ git commit -m "Попытаться поселить медведя косолапого" 
```

Если сейчас выполнить команду `git log --oneline`, получится примерно следующее:  

```text
$ git log --oneline
48fe3dc (HEAD -> master) Попытаться поселить медведя косолапого
318ebdb Поселить волчка -- серого бочка
470c115 Поселить лисичку-сестричку
e4ede9c Поселить зайчика-побегайчика
31cf9b3 Поселить лягушку-квакушку
d7d797a Поселить мышку-норушку
1c29af6 Исходное состояние теремка 
```

Обратите внимание: у вас могут быть другие хеши, потому что они зависят в том числе от автора и времени, когда был сделан коммит.  

## Сравниваем коммиты  

Теперь, когда сказка рассказана и у вас есть история коммитов, попробуйте сравнить состояния файла `teremok.txt` между коммитами.  
Например, чтобы получить максимально сокращённую версию сказки, можно сравнить состояние файлов на момент первого коммита (у нас это `1c29af6`) и последнего (у нас `48fe3dc`). __Ваши хеши могут отличаться__.  

Передайте команде `git diff` хеши обоих коммитов. Состояние файлов на момент первого переданного коммита будет сравниваться с состоянием файлов на момент второго.  

Вместо `48fe3dc` можно было использовать `HEAD`: `git diff 1c29af6 HEAD`, потому что `HEAD` указывает на последний коммит.  

Если коротко, это сказка о том, как теремок был и его не стало. А теперь попробуйте узнать, кто подселялся между __лягушкой-квакушкой__ и __волчком — серым бочком__. Используйте соответствующие хеши коммитов.

Подселились: __зайчик-побегайчик__, __лисичка-сестричка__ и __волчок — серый бочок__. Чёрные строки без знаков `+` или `-` — это «контекст», его `git diff` выводит только для того, чтобы стало понятно, что находится рядом с изменёнными (зелёными и красными) строками.  

## Порядок аргументов `git diff`  

По сути команда `git diff A B` выводит список инструкций: как превратить состояние `A` в состояние `B`. Если поменять `A` и `B` местами (`git diff B A`), то и инструкции будут обратные: как превратить `B` в `A`. При этом все зелёные строки станут красными, и наоборот.  
Попробуйте `git diff <конец сказки> <начало>`. Вместо `HEAD` (конец сказки) можно также передать хеш.  

Готово! Всё равно, как если бы мы рассказали историю задом наперёд.
Вот и сказке конец, а кто с нами коммитил — молодец!

---
> `git log --oneline` показывает первые несколько символов хеша и сообщение коммита.  
>Этой командой можно воспользоваться, когда не нужен полный хеш.  
> `git diff --staged` показывает, что изменилось в проиндексированных файлах.  
>Ключ `--staged` говорит системе, что нужно смотреть изменения, которые были добавлены в `staged`.  
> `git diff a9928ab 11bada1` покажет различия коммитов с хешами `a9928ab` и `11bada1`.  
>В зависимости от того, в каком порядке переданы коммиты, это будут или внесённые правки, или информация о том, что нужно «откатить».  

---

__*Тема 7/8 (Просмотр изменений. Игнорирование файлов) Урок 3/4*__  

# Игнорирование файлов в Git  

Часто бывает так, что в папке-репозитории есть файлы, для которых не нужно хранить историю изменений. Например:

- macOS иногда создаёт скрытый файл `.DS_Store` для хранения настроек папки. К вашему проекту он, скорее всего, никакого отношения не имеет.  
- В Git не принято коммитить результаты компиляции исходного кода, то есть получившиеся исполняемые файлы.  
- Среды разработки (вроде *IntelliJ IDEA*) могут создавать папку с вашими личными настройками проекта. Если добавить её в репозиторий, то среда разработки других участников проекта может загрузить ваши настройки и начать вести себя странно.  

Чтобы Git игнорировал такие файлы и не пытался добавить их в репозиторий, нужно создать файл `.gitignore` (от англ. *ignore* — «игнорировать») и записать в него названия игнорируемых файлов. В этом уроке разберём, как это сделать.  

## Как заполнить `.gitignore`  

С точки зрения Git `.gitignore` — это обычный текстовый файл. Его добавляют в корень репозитория и тоже коммитят.  
В простейшем случае в `.gitignore` указывают все файлы, которые нужно игнорировать (по одному имени на строку). Но часто удобнее использовать __шаблоны__. Шаблон, или правило, — это способ указать сразу на несколько файлов с однотипными названиями.  

> 💡 Правила из `.gitignore` применяются только к новым (`untracked`) файлам. Если файл уже попал в `staging area` или в коммит, то правила на него не распространяются.  

Разберём подробнее формат файла `.gitignore`, какие в нём могут встречаться строки и как выглядят шаблоны.  

## Комментарий  

Если строка начинается с `#`, то это __комментарий__, и `.gitignore` не будет его учитывать.

```text
# вот так можно писать комментарии;
# они ничего не значат для .gitignore,
# но они могут быть полезны, чтобы понять, зачем было добавлено то или иное правило 
```

## Просто название файла  

Допустим, нужно, чтобы Git игнорировал все файлы `.DS_Store`. Для этого достаточно добавить в `.gitignore` строку с названием файла.  

```text
# для macOS
.DS_Store 
```

В таком случае Git будет игнорировать файлы с именем `.DS_Store`, причём не только в корне репозитория, но и во всех вложенных папках.  

## Звёздочка (`*`)  

Символ звёздочки (`*`) соответствует любой строке, включая пустую. Если такой символ используется в шаблоне в `.gitignore`, значит, файл будет проигнорирован вне зависимости от того, что будет на месте звёздочки.  

```text
# игнорировать все файлы, которые заканчиваются на .jpeg
*.jpeg

# игнорировать все файлы "tmp" во всех подпапках папки docs
docs/*/tmp 
```

Теперь Git будет игнорировать все файлы, которые заканчиваются на `.jpeg` — пригодится тем, кто не любит картинки. А также все временные файлы `tmp` (от англ. *temporary* — «временный») в подпапках папки `docs`. Например, Git проигнорирует файл `docs/current/tmp`.  

> 💡 Если задать правило, которое состоит только из звёздочки, Git будет игнорировать все файлы. Это происходит потому, что под звёздочку подходит любое имя файла.  

```text
# странное, но возможное правило
# "игнорировать все файлы"
* 
```

## Вопросительный знак (`?`)  

Вопросительный знак `?` соответствует одному любому символу.  

```text
file?.txt
```

Если сохранить такую запись в `.gitignore`, то будут проигнорированы, например, файлы `fileA.txt` и `file1.txt`. А вот файл `file12.txt` не будет проигнорирован, потому что в его названии два символа после `file`, а не один.  

## Квадратные скобки (`[…]`)  

Квадратные скобки, как и вопросительный знак, соответствуют одному символу. При этом символ не любой, а только из списка, который указан в скобках.  

```text
# игнорировать файлы file0.txt, file1.txt и file2.txt
# при этом не игнорировать file3.txt, file4.txt, ...
file[0-2].txt 
```

В скобках можно либо перечислить символы (`[abc]`), либо задать диапазон (`[a-z]`).  

## Слеш (`/`)  

Косая черта, или слеш (`/`), указывает на каталоги. Если шаблон в `.gitignore` начинается со слеша, то Git проигнорирует файлы или каталоги только в корневой директории.  

```text
# игнорировать todo.txt в корне репозитория
/todo.txt

# для сравнения: spam.txt будет игнорироваться во всех папках
spam.txt 
```

Теперь файл `todo.txt` в корневом каталоге будет проигнорирован. При этом, например, файл `subdir/todo.txt` по-прежнему отслеживается.  
Если шаблон заканчивается слешем, то правило применится только к папке.  

```text
# игнорировать папку build
build/ 
```

Обратите внимание: если `build` — это папка, то она будет проигнорирована. Если `build` — обычный файл, то он не подпадёт под правило и не будет игнорироваться.  

## Парные звёздочки (`**`)  

Функция парных звёздочек (`**`) похожа на функцию одинарной (`*`). Отличие в том, как они работают с вложенными папками. Двойная звёздочка может соответствовать __любому количеству__ таких папок (в том числе нулю). Одинарная может соответствовать только __одной__.  

```text
# игнорировать файлы "docs/current/tmp", "docs/old/tmp",
# а также "docs/old/saved/a/b/c/d/tmp"
# и даже "docs/tmp", потому что ноль вложенных папок тоже подходит
docs/**/tmp

# игнорировать только "docs/current/tmp" и "docs/old/tmp"
# файл "docs/old/saved/a/b/c/d/tmp" не попадает в правило
docs/*/tmp 
```

> 💡 Для двойной звёздочки верно то же самое, что и для одной: если задать правило `**`, то будут проигнорированы все файлы.  

## Восклицательный знак (`!`)  

Любое правило в файле `.gitignore` можно инвертировать с помощью восклицательного знака (`!`).  

```text
# игнорировать все JPEG-файлы
*.jpeg

# но только не мем с Doge
!doge.jpeg 
```

Теперь файл `doge.jpeg` будет отслеживаться, хотя остальные `jpeg`-файлы будут проигнорированы. Такие правила удобны для добавления исключений из других правил `.gitignore`.  

## Пример файла `.gitignore`  

Содержание `.gitignore` может быть таким.  

```text
# игнорировать все файлы в каталоге build
build/

# игнорировать все .log файлы
*.log

# не игнорировать *.log файлы в examples
# потому что это пример для документации
!examples/**/*.log 
```

## `.gitignore` и `git status`  

Игнорируемые файлы не отображаются в выводе команды `git status`, иначе они бы засоряли вывод.  
Если всё же нужно отобразить все игнорируемые файлы, то это можно сделать с помощью ключа `--ignored`: `git status --ignored`. В таком случае в выводе `git status` появится раздел `Ignored files`.  

На скриншотах ниже видно, как меняется вывод команды `git status` без ключа и с ним.  

- ![Scr1](pics/T7-L3_pic1.jpg)  
- ![Scr2](pics/T7-L3_pic2.jpg)  
- ![Scr3](pics/T7-L3_pic3.jpg)  

> 💡 Обратите внимание: сам файл `.gitignore` не отображается в выводе только потому, что мы его предварительно закоммитили.  

---

*Перед вами настроенный `.gitignore`. Изучите его и разделите файлы на те, которые Git будет отслеживать, и те, которые он проигнорирует*.

```text
*.log
!debug.log
/debug.bar
log[0-7].foo
logs/**/debug.log 
```

### Будет отслеживать  

```text
debug.log
logs/debug.bar
logSeven.foo
log8.foo
```

### Проигнорирует  

```text
logs/monday/pm/debug.log
log5.foo
debug.bar
foo.log
```

---

### *Задание для самостоятельной работы*  

Многие научные статьи оформляют с помощью *TeX*. Этот инструмент принимает на вход файлы с расширением `.tex` и выдаёт в качестве результата красиво оформленный `.pdf`. Но есть подвох: в процессе работы *TeX* также создаёт много временных файлов с расширениями вроде `.aux`, `.lof`, `.lot` и так далее.  

Составьте файл `.gitignore` так, чтобы Git игнорировал все файлы, кроме `.tex` и `.pdf`. Вы можете свериться с авторским решением, но сначала рекомендуем попробовать выполнить задание самостоятельно.

```text
# *** Авторское решение: 

# игнорировать все файлы
**

# кроме .tex и .pdf
!**.tex
!**.pdf 
```

Игнорирование файлов — механизм, который нельзя игнорировать. Вот что важно помнить:

- Если нужно, чтобы Git игнорировал какие-то файлы, стоит составить файл .gitignore.  
- Посмотреть, что игнорируется, можно с помощью команды `git status --ignored`.  
- Сам файл `.gitignore` — это обычный файл в репозитории. Его тоже стоит закоммитить.  
- Шаблонов много, но их легко найти в интернете вместе с примерами использования.  

---
