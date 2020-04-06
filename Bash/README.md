# Как писать Bash-скрипты (краткий спикок возможностей чисто для меня самого)
* Объявление shell, для которого написан скрипт: `!#<path to interpreter>`
* Сделать файл исполняемым: `chmod +x ./<name of script>`
* Вывод: `echo <list of parameters to output>` (example: `echo "Hi"`, `echo ~/*`)
* Переменные среды: $<name> (example: `$HOME`)
* Управляющий символ: `\` (example: `\$`, `\\`)
* Создание переменных: `<name>=<value>` (example: `name=Yarik`, `age=18`, `echo "$name is $age years old"`)
* Извлечение информации из вывода команд: `<name>=\`<command>\``
