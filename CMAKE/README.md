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
foreach(name list_of_values)
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
Также цикл foreach может быть выполнен с использованием `RANGE`
* `RANGE start end step` - `end` - обязателен, `start` и `step` - опциональны  
Дефолтные значения: `start` = 0, `step` = 1
(example: `RANGE 5` # 0 1 2 3 4 5)
(example: `RANGE 2 5` # 2 3 4 5)
(example: `RANGE 2 15 4` # 2 6 10 14)

Функции и макросы:
```cmake
function(func_name arg1 arg2 arg3)
    message(${arg1} " " ${arg2} " " ${arg3})
endfunction()
func_name(12 89 225) # вызов функции
```
```cmake
macro(mac_name arg1 arg2 arg3)
    message(${arg1} " "  ${arg2} " " ${arg3})
endmacro()
func_name(Hello, Ilon Musk) # вызов макроса
```
Отличие **макросов** от **функций**: переменные в функциях локальные, а в макросах - глобальные
