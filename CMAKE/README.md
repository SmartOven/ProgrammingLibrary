# Manual по CMAKE
> **CMake** — это открытый и кросс-платформенный набор утилит, предназначенных для автоматизации тестирования, компиляции и создания пакетов проектов на C/C++

Команды в **CMAKE** подобны функциям, но при передаче списка аргументов в них сепаратором является не `,`, а ` `(пробел)
Вывод данных в консоль:
* `message(arg1 arg2)` - выводит сообщение в консоль

Комментарии:
* `# put you text here` - начинается с символа `#`, заканчивается на этой же строке

Переменные:
* `set(name value)` - создание переменной и задания ей значения
* `unset(name)` - удаление переменной
* `${name}` - использование значения переменной
(example: `message("Value of the X: " ${x})`)
* `option(optional_var "variable description" standard_value)`

Условные операторы:
```cmake
if(expr1)
    statement1
elseif(expr2)
    statement2
else() # no expression available
    statement3
endif() 
```
* `EQUAL` -- `==`
* `GREATER` -- `>`
* `LESS` -- `<`
