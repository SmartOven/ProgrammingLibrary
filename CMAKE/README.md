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
if(expr1) # necessarily
    statement1
elseif(expr2) # optional
    statement2
else() # optional, no expression available
    statement3
endif() necessarily
```
* `EQUAL` -- `==`, `STREQUAL` -- `== for strings`
* `GREATER` -- `>`
* `LESS` -- `<`

Цикл while:
```cmake
while(${name} operator value)
    statement
endwhile()
```
(example:
```cmake
set(name 7)
while(${name} GREATER 5)
    set(name 4)
endwhile()
```
)
For each цикл:
```cmake
foreach(name 1 2 3 4 5)
    message(${name})
endforeach()
```
(example:
```cmake
foreach(name 1 2 3 4 5)
    message(${name})
endforeach()
```
)
