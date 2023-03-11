---
description: Инструкция по прошивке встроенных ELRS передатчиков
---
!!! danger "Ошибка Bad Size Given"
    Если вы впервые обновляете свой **передатчик** через WiFi с 2.х/1.x прошивки, на 3.x прошивку, для начала вам нужно прошить его на версию 2.5.2, после этого прошить специальную [Repartitioner](https://github.com/ExpressLRS/repartitioner) прошивку [скачать тут](https://github.com/ExpressLRS/repartitioner/releases/download/1.0/repartitioner.bin) (нажать правой кнопкой, сохранить как). Оно будет ругаться на Target Mismatch (не совпадение таргетов), просто жмите `Flash Anyway`. 
    Только после этого можно закидывать 3.х прошивку по WiFi, точка поднимется сама, в Lua заходить не надо. 
    
    Видео Бардвела можно глянуть [тут](https://www.youtube.com/watch?v=2kcRi1cHejM).

    Можно шиться без всех этих танцев с бубном просто по USB

## Прошивка через EdgeTX Passthrough

!!! danger "Jumper T-PRO"
    Чтобы прошить Jumper T-PRO по USB (через Edgetx) нужны определенные телодвижения, см. [Проблемы Jumper T-Pro (todo)](https://todo)

Перед прошивкой убедитесь что у вас последняя версия EdgeTX, [подробнее о прошивке EdgeTX читайте тут (todo)](todo)

Также убедитесь что у вас ExpressLRS версия аппаратуры, а не Multi модуль.

Проверьте что на 6й странице настроек в аппаратуре (`Hardware`), в пункте `Serial Port` параметр `USB-VCP` равен `CLI`

В настройках Модели на аппаратуре выберите `Internal RF` = `CRSF`

Включите аппаратуру и подключите USB кабель в нужный порт (у аппаратур Radiomaster это верхний). Выберите опцию `USB Serial(Debug)` или `USB Serial(VCP)` в появившемся на аппаратуре окне.

<figure markdown>
![usb picture](/../assets/images/tx-internalUSBPlugged.jpg)
</figure>

<figure markdown>
![Debug option](/../assets/images/tx-internalSerialDebug.jpg)
</figure>

!!! tip "Важно"
    Внимательно читайте этот шаг, частые проблемы с прошивкой этим методом связанно именно с ним.

Если ваш ПК на Windows убедитесь что в Диспетчере Устройств аппаратура определилась как **STMicroelectronics Virtual COM Port**.

<figure markdown>
![Device Manager](/../assets/images/DeviceMngr.png)
</figure>

Если нет, и вы видите желтый восклицательный знак на логотипе рядом с названием устройства, то вам необходимо [установить драйвера (кликабельно)](https://www.st.com/en/development-tools/stsw-stm32102.html). Распакуйте архив, и запустите `VCP_V1.5.0_Setup_W7_x64_64bits`.

В ExpressLRS конфигураторе выберите нужную вам версию и правильный тип устройства, а также метод прошивки `EdgeTXPassthrough`

<figure markdown>
![via EdgeTX Passthrough](/../assets/images/Method_intTX_EdgeTXPassthrough.png)
<figcaption>Прошивка через EdgeTX</figcaption>
</figure>

В ExpressLRS Configurator выбрав правильный таргет и [Параметры сборки](/Manuals/FlashingOptions), нажмите `Build and Flash` и прошейте передатчик. Дождитесь окончания, при успешной прошивке будет надпись "Success"

<figure markdown>
![Build & Flash]
</figure>

Отключите USB кабель и запустите LUA Script, проверьте работоспособность и версию прошивки.

<figure markdown>
![Lua Running](/../assets/images/tx-internalLuaCheck.jpg)
</figure>

## Прошивка по WiFi

<figure markdown>
![via WiFi](/../assets/images/Method_intTX_WiFi.png)
<figcaption>Flashing via WiFi</figcaption>
</figure>

### Метод через браузер 

Выбрав правильный таргет и [Параметры сборки](/Manuals/FlashingOptions.md), cоберите кнопкой `Build` вашу прошивку через ExpressLRS Configurator.

<figure markdown>
![Build]
</figure>

После того как строчки в окне конфигуратора успешно пробегут, откроется проводник, где будет файл `Название_TX-<версия>.bin`.
Не закрывайте это окно, а сохраните этот файл в удобное место для последующей загрузки, например скиньте в сохраненки Telegram.

Следующий шаг потребует [Lua скрипт ELRS](https://github.com/ExpressLRS/ExpressLRS/blob/3.x.x-maintenance/src/lua/elrsV3.lua?raw=true) (правой кнопкой, сохранить как *.lua). Скачайте и закиньте на флешку аппы, в папку `/Scripts/Tools`.
Чтобы открыть скрипт на аппаратуре зажмите кпопку `SYS` и выберите `ExpressLRS`.

<figure markdown>
![Lua Script](/../assets/images/lua1.jpg)
</figure>

Если скрипт не открывается и висит на `Loading...`, проверь что в модели выставлен Internal CRSF.

<figure markdown>
![InternalRF BW](/../assets/images/txprep-bw-internalRF.jpg)
</figure>

Выберите пункт `Wifi Connectivity` в скрипте, а потом нажмите `Enable Wifi`. Нажмите ОК еще раз, чтобы включить WiFI на передатчике. Подключитесь к сети `ExpressLRS TX` с паролем `expresslrs`.

<figure markdown>
![Lua3](/../assets/images/lua/wifi-bw.png)
</figure>

<figure markdown>
![WiFi Hotspot](/../assets/images/WifiHotspotTX.png)
</figure>

Откройте браузер и перейдите на http://10.0.0.1/, откроется красивый сайт где вам нужна будет кнопка `Choose File`, выберите ранее полученный из конфигуратора файл `Название_TX-<версия>.bin` и нажмите `Update`.

После того как файл загрузится появится зеленое окно подтверждения что все хорошо, либо ошибка. Если ругается на таргет, убедитесь что он верный и нажмите `Flash Anyway`
Проверьте что версия внизу скрипта или на WiFi странице поменялась на ту что вы прошивали.

<figure markdown>
![Firmware Update](/../assets/images/web-firmwareupdate.png)
</figure>

<figure markdown>
![Update Success](/../assets/images/web-firmwareupdateSuccess.png)
</figure>

### Метод через домашнюю сеть и браузер

Выбрав правильный таргет и [Параметры сборки](../../../../Manuals/FlashingOptions.md), cоберите кнопкой `Build` вашу прошивку через ExpressLRS Configurator.

<figure markdown>
![Build]
</figure>

После того как строчки в окне конфигуратора успешно пробегут, откроется проводник, где будет файл `Название_TX-<версия>.bin`.
Не закрывайте это окно, а сохраните этот файл в удобное место для последующей загрузки, например скиньте в сохраненки Telegram.

Используя [Lua скрипт ELRS](https://github.com/ExpressLRS/ExpressLRS/blob/3.x.x-maintenance/src/lua/elrsV3.lua?raw=true) (правой кнопкой, сохранить как *.lua). Выберите `Wifi Connectivity` и включите WiFi кнопкой `Enable WiFi`. Если во время предыдущей прошивки вы прописали SSID своего домашнего WiFi или добавили его подключившись по `10.0.0.1`, то теперь модуль подключается к вашему роутеру, вместо раздачи точки.

<figure markdown>
![Lua3](/../assets/images/lua/wifi-bw.png)
</figure>

!!! danger "Внимание"
    После того как вы подключите свой TX/RX модуль к домашней WiFi сети он всегда будет подключаться к вашему роутеру. Он не будет создавать привычную WiFi точку, пока видит ваш домашний WiFi. Если вы не можете найти устройство в локальной сети, выключите роутер и подключитесь первым методом, далее уберите домашнюю WiFi сеть.

Используя браузер, перейдите по ссылке http://elrs_tx.local и вы попадете на WiFi страницу модуля. Найдите пункт Firmware Update, как показано ниже:

<figure markdown>
![Firmware Update](/assets/images/web-firmwareupdate.png)
</figure>

!!! note "Примечание"
    Иногда роутеры не присваивают устройствам dns имя (http://elrs_tx.local), если этот сайт не доступен вам придется сходить в амдинку вашего роутера и посмотреть какой ip получило устройство ExpressLRS, и перейти по этому ip.

Выберите ранее полученный из конфигуратора файл `Название_TX-<версия>.bin` и нажмите `Update`.

После того как файл загрузится появится зеленое окно подтверждения что все хорошо, либо ошибка. Если ругается на таргет, убедитесь что он верный и нажмите `Flash Anyway`
Проверьте что версия внизу скрипта или на WiFi странице поменялась на ту что вы прошивали.

<figure markdown>
![Update Success](/../assets/images/web-firmwareupdateSuccess.png)
</figure>

### Метод через домашнюю сеть и конфигуратор

Using the [ExpressLRS Lua script] (right-click, save as), select `Wifi Connectivity` then choose `Enable WiFi` and if you have flashed your Tx Module with your Home WiFi Network details or have set it in the Join Network section of the Update Page, it will connect to the network automatically.

<figure markdown>
![Lua3](/assets/images/lua/wifi-bw.png)
</figure>

Теперь ваше устройство будет видно внизу ExpressLRS Configurator, если выбран метод прошивки WiFi
<figure markdown>
![via WiFi](/assets/images/Method_TX_WiFi.png)
<figcaption>Прошивка по WiFi</figcaption>
</figure>

Using the ExpressLRS Configurator, select the correct Target and set your [Firmware Options]. Click **Build and Flash** and wait for the compile process to complete. 

<figure markdown>
![Build & Flash]
</figure>

!!! note "Примечание"
    Иногда роутеры не присваивают устройствам dns имя (http://elrs_tx.local), если этот сайт не доступен вам придется сходить в амдинку вашего роутера и посмотреть какой ip получило устройство ExpressLRS, и вбить его вместо порта внизу ExpressLRS Configurator.

В ExpressLRS Configurator выбрав правильный таргет и [Параметры сборки](../../../../Manuals/FlashingOptions.md), нажмите `Build and Flash` и прошейте передатчик. При успешной прошивке вы увидите результат как на картинке ниже:

<figure markdown>
![Build & Flash]
</figure>

<figure markdown>
![Wifi Update Log](/assets/images/WifiUpdateLog.png)
</figure>

Проверьте что версия внизу скрипта или на WiFi странице поменялась на ту что вы прошивали.

[ExpressLRS Lua script]: https://github.com/ExpressLRS/ExpressLRS/blob/3.x.x-maintenance/src/lua/elrsV3.lua?raw=true
[Build]: /../assets/images/Build.png
[Build & Flash]: /../assets/images/BuildFlash.png
[Firmware Options]: tx-prep.md
