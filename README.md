# Git flow instruction
## Git flow theory
Теоретическое описание работы с ветками

ru: https://guides.github.com/introduction/flow/

eng: https://habr.com/ru/post/346066/

## Git commands
Book with all details: https://git-scm.com/book/en/v2

You can always type "git command_name --help" for detailed explanation of the command.


### Проверка состояния
|   |   |
| - | - |
| `git status` | Выводит ветку в который ты находишься, что добавлено в индекс и что готово к коммиту. |
| `git log -N` | Показать последние N коммитов в данной ветке. |

### Работа с текущими изменениями
Все изменения происходят внутри какой-то выбранной ветки

|   |   |
| - | - |
|`git add path/to/directory/filename` | Добавить в индекс файл с путем path/to/directory/filename.|
|`git add .` | Добавить в индекс все файлы из текущей директории (частный случай предыдущего).|
|`git commit -m "commit message"` | Перенести все изменения из индекса в новый коммит с данным коммит сообщением. Коммит добавляется как новая вершина в текущую ветку.|
|`git push` | Отправить все коммиты из текущей ветки сделанные локально в удаленный репозиторий, если удаленной ветки с таким именем нет, нужно использовать команду "git push origin my-new-branch-name" (origin - обозначение удаленного репозитория).|

### Работа с ветками
master - Имя основной ветки. Там всегда должна находится стабильная последняя версия проекта.
При смене ветки и переходе к другому коммиту происходит изменение файлов в файловой системе.

|   |   |
| - | - |
|`git branch` | Показать все локальные (т.е. на текущей машине) ветки.|
|`git branch -a`  | Показать все ветки, в том числе в удаленном репозитории.|
|`git branch new-branch-name` | Создать новую ветку с именем new-branch-name. последним коммитом в ветке new-branch-name  становится последний коммит в той ветке, из который она была создана.|
|`git checkout branch-name` | Перейти на ветку с именем branch-name.|
|`git branch -d branch-name` | Удалить локальную ветку с именем branch-name.|
|`git push origin --delete branch-name` | Удалить ветку с именем branch-name в удаленном репозитории.|

### Еще полезное

`HEAD` - Alias для указания на последний коммит в данной ветке

`HEAD~N` - Alias для указания на N-ый коммит с конца в данной ветке

Далее везде вместо commit_name можно использовать как имя коммита, так и HEAD~N

|   |   |
| - | - |
|`git reset HEAD` | Можно использовать после неверного git add, чтобы очистить индекс|
|`git reset --soft commit_name` | Перейти на коммит с именем commit_name, при этом физически файлы на диске останутся без изменений|
|`git reset --hard commit_name` | Перейти на коммит с именем commit_name, при этом физически файлы на диске откатятся на состояние commit_name|
|`git diff commit_name_1 commit_name_2` | Показать разницу между commit_name_1 и commit_name_2|


## Основной сценарий работы
Клонируем репозиторий: `git clone repository_address` (1 раз для репозитория)

Создаем и переходим на эту ветку: `git checkout -b feature/feature-name`

Для каждого отдельного изменения которое хочется внести

   - Вносим нужные изменения
   
   - `git add filename1 filename2 filenameN`
   
   - `git commit -m "message"`
   
Тестируем изменения

Отправляем изменения в удаленный репозиторий: `git push origin feature/feature-name`

В интерфейсе делаем пул реквест

Дорабатываем ветку по комментариям: изменение -> `git add` -> `git commit` -> `git push`

Ревьюеры подтверждают слияние, происходит merge ветки branch-name в master.

Далее можно перейти в мастер: `git checkout master`
