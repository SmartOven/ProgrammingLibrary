# Как писать Bash-скрипты (краткий спикок возможностей чисто для меня самого)
* Объявление shell, для которого написан скрипт: `!#<path to interpreter>`
* Сделать файл исполняемым: `chmod +x ./<name of script>`
* Вывод: `echo <list of parameters to output>` (example: `echo "Hi"`, `echo ~/*`)
* Переменные среды: $<name> (example: `$HOME`)
* Управляющий символ: `\` (example: `\$`, `\\`)
* Создание переменных: `<name>=<value>` (example: `name=Yarik`, `age=18`, `echo "$name is $age years old"`)
* Извлечение информации из вывода команд: `<name>=$(<command>)` (example: `iam=$(whoami)`)
* Мат. операции: `<name>=$((a+b))` (example: `sum=$((2+4*6))`)
* Конструкция if-then-else:  
  + `if <expression> then <solution> fi`  
  (example: `if grep $user /etc/passwd then echo "The user $user Exists" fi`)
  + `if <expression> then <solution> else <another solution> fi`  
  (example: `if grep $user /etc/passwd then echo "The user $user Exists" fi`)
