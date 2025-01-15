## Пошаговая инструкция к установке Microsoft Office 365

1. #### Скопировать репозиторий себе на устройство

git clone https://github.com/LaryStef/MSOffice.git

Внимение!!! **Путь до репозитория должен содержать только латиницу**

2. #### Открыть powershell **от имени админитратора!!!**

3. #### При желании сделать бэкап реестра в temp

reg export HKCU\SOFTWARE\Microsoft\Office\16.0\Common\Experiment $ENV:temp\Experiment.reg

reg export HKCU\SOFTWARE\Microsoft\Office\16.0\Common\ExperimentConfigs $ENV:temp\ExperimentConfigs.reg

reg export HKCU\SOFTWARE\Microsoft\Office\16.0\Common\ExperimentEcs $ENV:temp\ExperimentEcs.reg

4. #### Сменить геоайди на сша

Set-WinHomeLocation -GeoId 244

5. #### Поменять страну в реестре, если не вышло, не страшно(хз, надо ли на самом деле)

New-ItemProperty -Path HKCU:\Software\Microsoft\Office\16.0\Common\ExperimentConfigs\Ecs -Name CountryCode -Type String -Value 'std::wstring|US' -Force

6. #### Удалить с устройства установленный MS Office, если такой имеется

7. #### Перейти в папку с установщиком

8. #### Pапустить установщик с кастомной конфигурацией. Данный конфиг содержит excel, word и powerpoint. При желании можете создать свою конфигурацию и заменить в папке(https://config.office.com/deploymentsettings).

.\Setup.exe /configure o365_custom_configuration.xml

9. #### Вернуть старый гео при необходимости

Set-WinHomeLocation -GeoId $oldGeo
