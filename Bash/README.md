# Как писать Bash-скрипты (краткий спикок возможностей чисто для меня самого)
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
  + Если сравнивается переменная, объявленная статичной строкой, ее надо дополнительно заключать в двойные кавычки  
  (example: `s1 = $USER s2 = "SmartOven" if [$s1 \< "$s2"]) then echo "OK" fi`)
  + `s1 = s2` -> `if (s1 == s2) return true;`
  + `s1 != s2` -> `if (s1 != s2) return true;`
  + `s1 \< s2` -> `if (s1 < s2) return true;`
  + `s1 \> s2` -> `if (s1 > s2) return true;`
  + `-n s1` -> `if (s1.length() > 0) return true;`
  + `-z s1` -> `if (s1.length() == 0) return true;`
