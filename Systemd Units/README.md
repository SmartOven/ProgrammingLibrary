# Systemd Units
###### *Дополнительную информацию можно получить в источниках, указанных в самом низу*
**Systemd** - инструмент для управления сервером с момента загрузки.  
**Units** - файлы, которые запускаются **systemd** (условия запуска, остановки и прочее описывается в самом юните)  

Юниты делятся на:
* Службы (.service)  
* Точки монтирования (.mount)  
* Устройства (.device)  
* Сокеты (.socket)

Сам юнит делится на три секции:
* \[Unit\]
* \[Service\]
* \[Install\]

Каждая секция содержит переменные (блоки), на которые будет ссылаться **systemd**
Списки обязательных переменных для каждой секции будет добавлен позже
Списки возможных переменных для каждой секции находятся ниже

Секция **\[Unit\]**:
* **Description=**"Название вашего юнита"  
Сюда помещается название вашего юнита (латиницей)  
Оно будет использовано **systemd** в некоторых случаях: например, чтобы записать в лог-файл ошибку  
* **Documentation=**"Ссылка на документацию к юниту"  
Должна содержать ссылку на документацию к этому юниту  
Возможные варианты ссылки: "http://", "https://", "file:", "info:", "man:"  
[Мануал о том, как писать мануалы](http://man7.org/linux/man-pages/man7/uri.7.html) (хаха, каламбур)  
* **Wants=** 1.service 2.socket 3.mount  
Содердит список юнитов, которые запустятся параллельно с этим юнитом  
Работает это так: запустили данный юнит -> запустили все юниты из списка -> смотрим, получилось ли  
Если при запуске юнитов из списка произошла ошибка - данный юнит все равно запустится  
Переменных **Wants=** может быть несколько  
* **Requires=** 1.service 2.socket 3.mount  
Содердит список юнитов, которые запустятся параллельно с этим юнитом  
Работает так же, как и **Wants=**, но  
Если при запуске юнитов из списка произошла ошибка - данный юнит сразу обратится к переменной **After=**, а затем завершит свое выполнение  
  > Лучшей практикой является использование **Wants=** вместо **Requires=**, чтобы не вылетать с ошибкой, а сохранять данные о них, не завершая исполнения юнита  
* **Requisite=** 1.service 2.socket 3.mount  
Работает так же, как и **Requires=**, но  
Если при запуске юнитов из списка произошла ошибка - данный юнит сразу завершится  
* **BindsTo=** - что-то похожее на **Requires**, см. [документацию](https://www.freedesktop.org/software/systemd/man/systemd.unit.html#BindsTo=)  
* **PartOf=** - что-то похожее на **Requires**, см. [документацию](https://www.freedesktop.org/software/systemd/man/systemd.unit.html#PartOf=)  
* **Conflicts=** 1.service 2.socket 3.mount  
При запуске данного юнита все юниты из списка **Conflicts=**, которые в данный момент активны (запущены и работают) будут остановлены  
Для корректной работы данного блока должны быть объявлены блоки **Before=** и **After=**  
Также стоит учитывать, что в блоки **Requires=** и **Conflicts=** не стоит пихать одинаковые юниты, в противном случае работа данного юнита завершится с ошибкой  
* **Before=** 1.service 2.socket 3.mount  
Если юнит (`a` из списка **Before=** и данный юнит) запускаются, то сначала запустится данный юнит, а потом уже юнит `a`  
Для юнитов типа `.devise` данный блок пропускается и не имеет никакого эффекта на них  
Переменных **Before=** может быть несколько  
* **After=** 1.service 2.socket 3.mount  
Если юнит (`a` из списка **After=** и данный юнит) запускаются, то сначала запустится юнит `a`, а потом уже данный юнит  
Переменных **After=** может быть несколько  
* **OnFailure=** 1.service 2.socket 3.mount  
Список юнитов, которые будут запущены, если/когда данный юнит крашнется (перейдет в состояние `failed`)  
Если юнит содержит блок **Restart=** - в состояние `failed` он перейдет только, когда достигнет лимит перезапусков  
* **PropagatesReloadTo=** - см. [документацию](https://www.freedesktop.org/software/systemd/man/systemd.unit.html#PropagatesReloadTo=)  
* **ReloadPropagatedFrom=** - см. [документацию](https://www.freedesktop.org/software/systemd/man/systemd.unit.html#PropagatesReloadTo=)  
* **JoinsNamespaceOf=** 1.service 2.socket 3.mount  
Параметр действует только на юниты типа `.service`
Присоединяет пространства имен юнитов из списка к данному юниту  
Этот параметр действует только в том случае, если (**PrivateNetwork=** или **NetworkNamespacePath=**) и/или **PrivateTmp=** объявлены для обоих юнитов: (тот, который присоединяют) и (тот, к которому присоединяют)  
* **RequiresMountsFor=** path1 path2 path3  
Автоматически добавляет в **Requires=** и **After=** все `.mount` юниты, которые нужно подключить, чтобы иметь доступ ко всем путям из данного списка  
Актуально только для `.mount` юнитов с меткой `noauto`, все с меткой `auto` будут поключены и без использования данного блока  
* **OnFailureJobMode=** string_value  
Задает способ запуска юнитам, которые будут запущены в блоке **OnFailure=**
Блок должен иметь одно из значений:  
\["fail", "replace", "replace-irreversibly", "isolate", "flush", "ignore-dependencies", "ignore-requirements"\]  
Если такого блока в юните нет, его дефолтное значение - "replce".  
Описание каждого значения есть в [документации](https://www.freedesktop.org/software/systemd/man/systemctl.html#--job-mode=)
* **IgnoreOnIsolate=** bool_value  
Принимает булевое значение. `true` - этот юнит не будет остановлен во время изоляции другого юнита.  
Дефолтное значение - `false`  
* **StopWhenUnneeded=** bool_value  
Принимает булевое значение. `true` - этот юнит будет остановлен когда перестанет быть нужным.  
Дефолтное значение - `false` 
* **RefuseManualStart=** - если `true` - его можно запустить только из другого юнита.  
* **RefuseManualStop=** - если `true` - его можно остановить только из другого юнита.  
* **AllowIsolate=** - если `true` - его можно изолировать командой `systemctl isolate`. Лучше оставить `false` (дефолт)  
* **DefaultDependencies=** - лучше не трогать (изначально `yes`).  
* **CollectMode=** - либо `inactive`, либо `inactive-or-failed`. Как-то меняет работу `garbage collector`
* **FailureAction=** string_value  
Блок должен иметь одно из значений:  
\[none, reboot, reboot-force, reboot-immediate, poweroff, poweroff-force, poweroff-immediate, exit, exit-force\]
В режиме пользователя доступны только: \[none, exit, exit-force\]
Задает действие, выполняемое после остановки юнита (юнит выдал ошибку и остановился)
* **SuccessAction=** string_value  
Блок должен иметь одно из значений:  
\[none, reboot, reboot-force, reboot-immediate, poweroff, poweroff-force, poweroff-immediate, exit, exit-force\]  
В режиме пользователя доступны только: \[none, exit, exit-force\]  
Задает действие, выполняемое после успешного выполнения юнита  
* **FailureActionExitStatus=** int_value  
Блок должен иметь значение в диапазоне от 0 до 255.  
Значение используется для передачи `exit status` после выполнения **FailureAction=**  
Используется только если **FailureAction=** установлен на `exit` или `exit-force`
* **SuccessActionExitStatus=**
* **JobTimeoutSec=**
* **JobRunningTimeoutSec=**
* **JobTimeoutAction=**
* **JobTimeoutRebootArgument=**
* **StartLimitIntervalSec=**\<interval\>
* **StartLimitBurst=**\<burst\>
* **StartLimitAction=**
* **RebootArgument=**
* **SourcePath=**
* Conditions и Asserts блоки:  
Блоки дополнительных условий запуска юнита  
Не рассматриваются в этом мануале, так как их очень много и, возможно, они редко используются

Секция \[Service\]:
* будет рассмотрена позже

Секция \[Install\]:
* **Alias=**
* **WantedBy=**
* **RequiredBy=**
* **Also=**
* **DefaultInstance=**

Полезные ссылки:
* [Документация по юнитам](https://www.freedesktop.org/software/systemd/man/systemd.unit.html)
* [systemd - ArchWiki](https://wiki.archlinux.org/index.php/Systemd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9))
* [Введение в systemctl](https://community.vscale.io/hc/ru/community/posts/211805669-%D0%92%D0%B2%D0%B5%D0%B4%D0%B5%D0%BD%D0%B8%D0%B5-%D0%B2-systemd-%D0%A1%D0%B5%D1%80%D0%B2%D0%B8%D1%81%D1%8B-%D1%8E%D0%BD%D0%B8%D1%82%D1%8B)
