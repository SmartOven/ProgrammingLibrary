# Как писать Bash-скрипты (краткий спикок возможностей чисто для меня самого)
* Объявление shell, для которого написан скрипт: `!#<path to interpreter>`
* Сделать файл исполняемым: `chmod +x ./<name of script>`
* Вывод: `echo <list of parameters to output>` (example: `echo "Hi"`, `echo ~/*`)
* Переменные среды: $<name> (example: `$HOME`)
* Управляющий символ: `\` (example: `\$`, `\\`)
* Создание переменных: `<name>=<value>` (example: `name=Yarik`, `age=18`, `echo "$name is $age years old"`)
* Извлечение информации из вывода команд: `<name>=$(<command>)` (example: `iam=$(whoami)`)
* Мат. операции: `<name>=$((a+b))` (example: `sum=$((2+4*6))`)
* Конструкция if-then-elif-else-fi (if/then/elif/else/fi - все пишется на новой строке):  
  + `if <expression> then <solution> fi`  
  (example: `if grep $user /etc/passwd then echo "The user $user Exists" fi`)
  + `if <expression> then <solution> else <another solution> fi`  
  (example: `if grep $user /etc/passwd then echo "The user $user Exists" fi`)
  + `if <expression> then <solution> elif <another expression> then <another solution> fi`  
  (example: `if grep $user /etc/passwd then echo "$user Exists" elif ls /home then echo "doesn’t exist but there is a dirunder /home" fi`)
