# Настройка рабочего окружения
## Установка операционной системы
В качестве среды разработки используется операционная система Ubuntu-24.04. Установка ОС производится через интерактивную командную оболочку — Windows PowerShell.
Для запуска оболочки и установки ОС необходимо выполнить следующую последовательнось действий

- [x] нажать комбинацию клавиш  `WIN+X` и выбрать меню `Терминал`
- [x] проверить текущую версию `WSL`— `wsl --version`

``` pwsh-session title="PowerShell"
Версия WSL: 2.3.24.0
Версия ядра: 5.15.153.1-2
Версия WSLg: 1.0.65
Версия MSRDC: 1.2.5620
Версия Direct3D: 1.611.1-81528511
Версия DXCore: 10.0.26100.1-240331-1435.ge-release
Версия Windows: 10.0.22631.4460``
``` 

- [x] установить [ОС](https://learn.microsoft.com/ru-ru/windows/wsl/basic-commands#install)
- [ ] Vestibulum convallis sit amet nisi a tincidunt
    * [x] In hac habitasse platea dictumst
    * [x] In scelerisque nibh non dolor mollis congue sed et metus
    * [ ] Praesent sed risus massa
- [ ] Aenean pretium efficitur erat, donec pharetra, ligula non scelerisque

### Code copy button

<!-- md:version 9.0.0 -->
<!-- md:feature -->

Code blocks can automatically render a button on the right side to allow the
user to copy a code block's contents to the clipboard. Add the following to
`mkdocs.yml` to enable them globally:

``` yaml
theme:
  features:
    - content.code.copy
```


 
