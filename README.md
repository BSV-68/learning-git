. . . <br>   
## Инициализируем репозиторий  

В этом уроке покажем, как инициализировать Git-репозиторий и проверить, что всё прошло успешно.  
## Сделать папку репозиторием — '''git init'''  
Чтобы Git начал отслеживать изменения в проекте, папку с файлами этого проекта нужно сделать Git-репозиторием (от англ. repository — «хранилище»). Для этого следует переместиться в неё и ввести команду git init (от англ. initialize — «инициализировать»).  
Например, создайте папку first-project и сделайте её Git-репозиторием: перейдите в неё с помощью команды cd и выполните git init.  

`$ cd ~/dev/first-project` #-перешли в нужную папку  

`$ git init` #-создали репозиторий  
Вы можете создать папку в любом месте на компьютере. Но в этом случае не забывайте менять в наших примерах путь ~/dev/first-project на тот, который ведёт к вашей папке. Помните, что не рекомендуется создавать репозиторий Git внутри другого Git-репозитория. Это может вызывать проблемы с отслеживанием изменений.  
В некоторых случаях при инициализации репозитория Git может показать объёмное сообщение, которое начинается со слов Using 'master' as the name…. Не пугайтесь: это не ошибка. Пока это сообщение не имеет большого значения.  
> 💡 Почему появляется такое сообщение?  
> В зависимости от настроек Git может назвать начальную ветку или main, или master. Сообщение появится в том случае, если ветка по умолчанию будет > называться *master*.  
После волны протестов Black Lives Matter многие проекты стали отказываться от терминологии, которая может оскорбить темнокожих людей. Слово *master* можно перевести как «хозяин», поэтому сейчас рекомендуется называть основную ветку *main* (англ. «главная»).  
Подробнее о том, что такое ветки и как с ними работать, мы расскажем в дальнейшем.  
Также git init выведет сообщение вида Initialized empty Git repository in <*ваша папка с проектом*>/.git/ (англ. «инициализирован пустой Git-репозиторий в <*ваша папка*>/.git/»). В подпапке .git Git будет хранить всю служебную информацию.  

Команда `git init` — одна из редко применяемых, ведь репозиторий создаётся один раз, а пользоваться им можно сколько угодно долго.  
«Разгитить» папку, если что-то пошло не так, — rm -rf .git  
Если вы случайно сделали Git-репозиторием не ту папку, её можно «разгитить». Для этого нужно удалить скрытую подпапку .git.  
`$ cd <папка с репозиторием>` # перешли в папку  

`$ rm -rf .git` # удалили подпапку .git  
Разберём подробнее, что такое `-rf`:  
ключ `-r` (от англ. recursive — «рекурсивно») позволяет удалять папки вместе с их содержимым;  
ключ `-f` (от англ. force — «заставить») избавит вас от вопросов вроде «Вы точно хотите удалить этот файл? А этот? И этот тоже?».  
