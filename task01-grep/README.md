# Grep (`task01-grep`)

## Содержание
1. [Содержание](#содержание)
1. [Задание](#задание)
1. [Требования к корректности решения](#требования-к-корректности-решения)
    1. [Разумная попытка](#разумная-попытка)
    1. [Блокирующее](#блокирующее)
    1. [Режимы поиска](#режимы-поиска)
    1. [Режимы вывода](#режимы-вывода)
    1. [Прочие требования](#прочие-требования)
1. [Сдача задания](#сдача-задания)
    1. [Процесс](#процесс)
    1. [Сроки](#сроки)
    1. [Система оценки](#система-оценки)

## Задание
Реализуйте в процедурном стиле на языке Python 3 утилиту [`grep`](https://ru.wikipedia.org/wiki/Grep),
поддерживающую флаги `-E` и `-c`.
Эта утилита ищет в стандартном вводе или наборе файлов строчки с заданной подстрокой
и выводит их на экран.

Также вам требуется реализовать white-box юнит-тесты и интеграционные тесты.

Для разогрева вам даны файлы `grep.py` и `test_grep.py`, демонстрирующие
основы синтаксиса языка Python, точный формат ввода и вывода, а также
использования полезных библиотек, которые пригодятся вам в задании.

Это задание состоит из двух итераций. Сейчас здесь описана только первая.
На второй итерации задания вам потребуется добавить другие флаги,
изменяющие как способ поиска строчек, так и формат вывода.
На данный момент эти флаги вам неизвестны; рекомендуется сделать
понятный и расширяемый код, чтобы было проще выполнять вторую итерацию.

## Требования к корректности решения
### Разумная попытка
Преподаватели в некоторых группах могут требовать сделать "разумную попытку" к определённому сроку.
Под этим понимается:

1. Все присланные файлы не имеют синтаксических ошибок.
1. Предоставленные в задании тесты проходят без их изменений при запуске команды `pytest`.

### Блокирующее
Если хотя бы одно из следующих требований не выполняется, вы можете получить не более 30% баллов за задание:

1. Попытка является "разумной" (смотри выше).
1. Команда `flake8 --max-line-length=100` (с установленными `pep8-naming` или `flake8-quotes`) не выдаёт ошибок ни в одном из файлов.
1. Команда `pylint --max-line-length=100 --disable=invalid-name,missing-docstring,global-statement,too-many-lines,R --enable=simplifiable-if-statement,redefined-variable-type` не выдаёт ошибок ни в одном из файлов.
   Это требование можно ослабить, если вы предоставите практику пример, где это команда выдаёт неразумную, на ваш взгляд, рекомендацию.
1. Команда `mypy --ignore-missing-imports` не выдаёт ошибок ни в одном из файлов.
1. Все ваши тесты запускаются командой `pytest` и проходят под Windows, Linux и Mac (используйте `/` вместо `\` для разделения папок в путях, а в Python можно использовать `pathlib`).
1. Каждая содержательная команда в коде (не обработка ошибки и не вызов `main(sys.argv[1:])` должна вызываться
   хотя бы в одном тесте (неважно, юнит- или интеграционном).
   Проверяйте при помощи `pytest-cov`.
1. Должны быть указаны типы всех параметров всех функций (кроме параметров тестов `test_*`) и типы их возвращаемых значений для команды `mypy`.
1. Для каждой процедуры должен быть написан хотя бы один нетривиальный юнит-тест.
1. В качестве shebang в Python используется `#!/usr/bin/env python3`.
1. В неисполняемых файлах shebang отсутствует.

### Режимы поиска
Команда `./grep.py [-c] <needle> [<file> [<file>...]]` ищет в перечисленных файлах (или стандартном вводе, если файлов нет)
подстрочку `<needle>`.

В режиме `./grep.py [-c] -E <needle> [<file> [<file>...]]` утилита трактует `<needle>` как регулярное выражение:
вместо `needle in line` для подстроки используйте `re.search(needle, line)` (смотри предоставленный пример).
Например, строка `h*i?` не является подстрокой `ahhhe`, однако регулярное выражение `h*i?`
принимает строку `hh`, являющуюся подстрокой `ahhhe`.

### Режимы вывода
По умолчанию на экран выводятся все найденные строчки.

Если файлов больше одного, то на экран выводится не просто строчка `<line>`, а ещё и имя файла: `<file>:<line>`.

Ключ `-c` подавляет весь стандартный вывод утилиты и вместо этого выводит количество
найденных строк.
Если файлов при этом больше одного, то на экран вместо суммарного количества строк
выводится количество строк отдельно для каждого файла в формате `<file>:<count>`.

### Прочие требования
* Гарантируется, что все пути относительные.
* Выводите пути без изменений, даже если их можно "упростить".
* Выводите строчки в том же порядке, в котором они идут в файлах.
* Выводите ответы для файлов в том же порядке, в котором они были переданы в качестве параметров.
* В частности, один файл может быть передан несколько раз, тогда его надо выводить несколько раз.

## Сдача задания
### Процесс
Решением задачи являются два файла: `grep.py` с основным кодом решения и `test_grep.py`
с юнит- и интеграционными тестами.
Не разрешается прикладывать другие файлы.

Попытка сдачи — прислать эти два файла практику своей группы на email с CSCWiki
с префиксом темы письма `[hse] [pb] [task01-grep]`.
Ответ практик направит по почте.
Вы можете исправлять своё решение сколько угодно раз.

В каждой группе независимо устанавливаются дополнительные возможности сдать
(например, через Telegram), уточняйте правила у своего преподавателя.

Если вы сдаёте с нарушением процесса (например, не на тот email или с неверной
темой), то ваша посылка может быть не проверена, пока вы не исправите формат.

### Сроки
Задание выдано 07.11.2019 (четверг).

Срок сдачи — **15.11.2019 (пятница) 22:59 по Москве**.

В некоторых группах к сроку сдачи требуется лишь сделать посылку,
а доделывать можно потом без последствий; в некоторых может требоваться
исправить все замечания до срока сдачи.
Уточняйте правила у своего преподавателя.

## Система оценки
Задание оценивается в 10 баллов (за две итерации), из них 4 вы получаете за корректность,
4 за стиль кода и тестов, и ещё 2 за субъективное качестве тестов.

Если вы вообще не выполните вторую итерацию, вы можете получить за задание
не более 5 баллов из 10 возможных.

В каждой группе независимо устанавливаются баллы за посылки, сделанные
после срока сдачи, за частичное выполнение задания, за выполненную
первую итерацию без второй.
Уточняйте правила у своего преподавателя.