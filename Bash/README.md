# Manual по Bash-скриптам (краткий список возможностей, пишу для себя самого)
* Объявление shell, для которого написан скрипт: `!#<path to interpreter>`  
(example: `!#/bin/bash`)
* Сделать файл исполняемым: `chmod +x ./<name of script>`  
(example: `chmod +x ./myscript`)
* Вывод: `echo <list of parameters to output>`  
(example: `echo "Hi"`, `echo ~/*`)
* Переменные среды: $<name>  
  (example: `$HOME`)
* Управляющий символ: `\`  
  (example: `\$`, `\\`)
* Создание переменных: `<name>=<value>`  
  (example: `name=Yarik`, `age=18`, `echo "$name is $age years old"`)
* Извлечение информации из вывода команд: `<name>=$(<command>)`  
  (example: `iam=$(whoami)`)
* Мат. операции: `<name>=$((a+b))`  
  (example: `sum=$((2+4*6))`)
* Конструкция if-then-elif-else-fi (if/then/elif/else/fi - все пишется на новой строке):  
  + `if [<expression>] then <solution> fi`  
  (example: `if grep $user /etc/passwd then echo "The user $user Exists" fi`)
  + `if [<expression>] then <solution> else <another solution> fi`
  + `if [<expression>] then <solution> elif [<another expression>] then <another solution> fi`
* Сравнение чисел:  
  + `-eq` is `==` (equal)
  + `-ge` is `>=` (greater-equal)
  + `-gt` is `>` (strictly greater)
  + `-le` is `<=` (less-equal)
  + `-lt` is `<` (strictly less)
  + `-ne` is `!=` (not equal)
* Сравнение строк:
  + `s1 = s2` -> `if (s1 == s2) return true;`
  + `s1 != s2` -> `if (s1 != s2) return true;`
  + `s1 \< s2` -> `if (s1 < s2) return true;`
  + `s1 \> s2` -> `if (s1 > s2) return true;`
  + `-n s1` -> `if (s1.length() > 0) return true;`
  + `-z s1` -> `if (s1.length() == 0) return true;`
  + Если сравнивается переменная, объявленная статичной строкой, ее надо дополнительно заключать в двойные кавычки  
  (example: `s1 = $USER s2 = "SmartOven" if [$s1 \< "$s2"]) then echo "OK" fi`)
  + Несостыковочка: команда `sort` считает, что A < a, оператор сравнения считает наоборот :/
* Работа с файлами:  
  + Существует ли файл: `-e <file>`
  + Существует ли файл и является ли он директорией: `-d <file>`
  + Существует ли файл, и является ли он обычным файлом: `-f <file>`
  + Существует ли файл, и доступен ли он для чтения: `-r <file>`
  + Существует ли файл, и доступен ли он для записи: `-w <file>`
  + Существует ли файл, и не является ли он пустым: `-s <file>`
  + Существует ли файл, и является ли он исполняемым: `-x <file>`
  + Новее ли <file1>, чем <file2>: `file1 -nt file2`
  + Старше ли <file1>, чем <file2>: `<file1> -ot <file2>`
  + Существует ли файл, и является ли его владельцем текущий пользователь: `-O <file>`
  + Сществует ли файл, и соответствует ли его идентификатор группы идентификатору группы текущего пользователя: `-G <file>`
* Separator (разделитель): изначально `bash` считает сепараторами пробел, табуляцию и перенос строки, но список сепараторов можно изменить, изменив переменную IFS: `IFS=$'\n'` или `IFS=:`
* Циклы:
  + Цикл может быть вложенным (похож на **Pascal**)
  + Существуют операции `break` и `continue`
  + В цикле можно перенаправить вывод (вместо консоли выводить в файл): для этого надо после `done` добавить `> <file>`  
  (example: `done > output.txt`)
* Цикл while:
  + Простой цикл bash: `while [<expression>] do <another expression> done`  
  (example: `var1=5 while [ $var1 -gt 0 ] do echo $var1 var1=$[ $var1 - 1 ] done`)
* Цикл for:
  + Простой цикл bash: `for <var> in <list> do <list of commands> done`  
  (simple example: `for var in first second third fourth fifth do echo The $var item done`)  
  (real example: `file="myfile" for var in $(cat $file) do echo " $var" done`)
  + С-подобный цикл: `for (( a = 1; a < 10; a++ ))`  
* Чтение параметров командной строки:  
  + bash назначает им имена `$1`, `$2`, ... (`$0` - название скрипта)  
    (example: `./myscript 10 25` -> `$0=./myscript` `$1=10` `$2=25`)
  + Количество параметров содержится в переменной `$#`
  + Все параметры разом можно захватить: `$*`=строка, содержащая все параметры или `$@`=список, содержащий все параметры
  + Последний параметр можно получить, написав `${!#}`
  + Если требуется больше 9 параметров, параметры начиная с 10-ого идут как `${10}`, `${11}`, ...
  + Если требуется обработать несколько параметров, разделенных пробелом, как один - надо изменить сепаратор
  + Пример проверки на существование параметра: `if [ -n "$1" ] then echo Hello $1. else echo "No parameters found. " fi`
  + Чтобы сдвинуть влево все параметры (каждый `i-ый` становится `(i-1)-ым`), используется команда `shift`, но говорят, что надо быть с ней поосторожнее
* `Case` в `bash`:  
  `case "$1" in  
  -a) echo "Found the -a option" ;;  
  -b) echo "Found the -b option" ;;  
  -c) echo "Found the -c option" ;;  
  *) echo "$1 is not an option" ;;  
  esac`
