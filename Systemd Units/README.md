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

Секция **\[Unit\]**  
(самые важные выделены жирным шрифтом):
* **Description=**"Название вашего юнита"  
(example: Description="Message Collector Bot")
* Documentation=""
* Wants=
* Requires=
* Requisite=
* BindsTo=
* PartOf=
* Conflicts=
* Before=
* After=
* OnFailure=
* PropagatesReloadTo=
* ReloadPropagatedFrom=
* JoinsNamespaceOf=
* RequiresMountsFor=
* OnFailureJobMode=
* IgnoreOnIsolate=
* StopWhenUnneeded=
* RefuseManualStart=
* RefuseManualStop=
* AllowIsolate=
* DefaultDependencies=
* CollectMode=
* FailureAction=
* SuccessAction=
* FailureActionExitStatus=
* SuccessActionExitStatus=
* JobTimeoutSec=
* JobRunningTimeoutSec=
* JobTimeoutAction=
* JobTimeoutRebootArgument=
* StartLimitIntervalSec=\<interval\>
* StartLimitBurst=\<burst\>
* StartLimitAction=
* RebootArgument=
* SourcePath=
