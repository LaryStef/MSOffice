## Пошаговая инструкция для установки Microsoft Office 365

1. #### Удалить с устройства установленный MS Office, если такой имеется

2. #### Скопировать репозиторий себе на устройство

git clone https://github.com/LaryStef/MSOffice.git

Внимение!!! **Путь до репозитория должен содержать только латиницу**

3. #### Открыть powershell **от имени админитратора!!!**

4. #### Узнать свой текущий GeoId

Get-WinHomeLocation

5. #### При большом желании сделать бэкап реестра в temp

reg export HKCU\SOFTWARE\Microsoft\Office\16.0\Common\Experiment $ENV:temp\Experiment.reg

reg export HKCU\SOFTWARE\Microsoft\Office\16.0\Common\ExperimentConfigs $ENV:temp\ExperimentConfigs.reg

reg export HKCU\SOFTWARE\Microsoft\Office\16.0\Common\ExperimentEcs $ENV:temp\ExperimentEcs.reg

6. #### Сменить геоайди на сша

Set-WinHomeLocation -GeoId 244

7. #### Поменять страну в реестре, если не вышло, не страшно(хз, надо ли на самом деле)

New-ItemProperty -Path HKCU:\Software\Microsoft\Office\16.0\Common\ExperimentConfigs\Ecs -Name CountryCode -Type String -Value 'std::wstring|US' -Force

8. #### Перейти в папку с установщиком(в powershell)

9. #### Запустить установщик с кастомной конфигурацией из репозитория. Данный конфиг содержит только excel, word и powerpoint. При желании можете создать свою конфигурацию в её на сайте майков https://config.office.com/deploymentsettings и заменить её

.\Setup.exe /configure o365_custom_configuration.xml

10. #### Вернуть старый гео при необходимости

Set-WinHomeLocation -GeoId $oldGeo
