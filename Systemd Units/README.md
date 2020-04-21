# Systemd Units
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
(example: Description="Socket reader")  
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
* **Before=**
* **After=**
* **OnFailure=**
* **PropagatesReloadTo=**
* **ReloadPropagatedFrom=**
* **JoinsNamespaceOf=**
* **RequiresMountsFor=**
* **OnFailureJobMode=**
* **IgnoreOnIsolate=**
* **StopWhenUnneeded=**
* **RefuseManualStart=**
* **RefuseManualStop=**
* **AllowIsolate=**
* **DefaultDependencies=**
* **CollectMode=**
* **FailureAction=**
* **SuccessAction=**
* **FailureActionExitStatus=**
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
