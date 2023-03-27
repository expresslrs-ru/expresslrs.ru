---
description: Инструкция по прошивке внешних ELRS передатчиков
---
!!! note "Примечание"
    Эта инструкция подходит для всех внешних ELRS передатчиков на 2.4Ghz/900Mhz, которые устанавливаются во внешний слот аппаратуры.

!!! danger "Ошибка Bad Size Given"
    Если вы впервые обновляете свой **передатчик** через WiFi с 2.х/1.x прошивки, на 3.x прошивку, для начала вам нужно прошить его на версию 2.5.2, после этого прошить специальную [Repartitioner](https://github.com/ExpressLRS/repartitioner) прошивку [скачать тут](https://github.com/ExpressLRS/repartitioner/releases/download/1.0/repartitioner.bin) (нажать правой кнопкой, сохранить как). Оно будет ругаться на Target Mismatch (не совпадение таргетов), просто жмите `Flash Anyway`. 
    Только после этого можно закидывать 3.х прошивку по WiFi, точка поднимется сама, в Lua заходить не надо. 
    
    Видео Бардвела можно глянуть [тут](https://www.youtube.com/watch?v=2kcRi1cHejM).

    Можно шиться без всех этих танцев с бубном просто по USB

## Прошивка по WiFi

- Device Category: 
    - Выбираем фирму вашего передатчика

- Device:
    - Выбираем модель вашего передатчика, например `HM ES24TX Pro Series 2400 TX` - для HappyModel PRO 

<figure markdown>
![via WiFi](/assets/images/Method_TX_WiFi.png)
<figcaption>Прошивка по WiFi</figcaption>
</figure>

!!! note "Примечание"
    Методы прошивки описанные ниже работают только в том случае, если ваши модули уже на 2.x прошивке. Для модулей на древних 1.х прошивках вам придется обновить его по USB.

### Метод через браузер

Выбрав правильный таргет и [Параметры сборки](/Manuals/FlashingOptions), cоберите кнопкой `Build` вашу прошивку через ExpressLRS Configurator.

<figure markdown>
![Build]
</figure>


После того как строчки в окне конфигуратора успешно пробегут, откроется проводник, где будет файл `Название_TX-<версия>.bin`.
Не закрывайте это окно, а сохраните этот файл в удобное место для последующей загрузки, например скиньте в сохраненки Telegram.

Следующий шаг потребует [Lua скрипт ELRS](https://github.com/ExpressLRS/ExpressLRS/blob/3.x.x-maintenance/src/lua/elrsV3.lua?raw=true) (правой кнопкой, сохранить как *.lua). Скачайте и закиньте на флешку аппы, в папку `/Scripts/Tools`.
Чтобы открыть скрипт на аппаратуре зажмите кпопку `SYS` и выберите `ExpressLRS`.

<figure markdown>
![Lua Script](/assets/images/lua1.jpg)
</figure>

<figure markdown>
![Lua Script T16](/assets/images/lua2.jpg)
</figure>

Если скрипт не открывается и висит на `Loading...`, проверь что в модели выставлен External CRSF.

![ExternalRF BW](/assets/images/txprep-bw-externalRF.jpg)

<figure markdown>
![Lua3](/assets/images/lua3.jpg)
</figure>

Выберите пункт `Wifi Connectivity` в скрипте, а потом нажмите `Enable Wifi`. Нажмите ОК еще раз, чтобы включить WiFI на передатчике. Подключитесь к сети `ExpressLRS TX` с паролем `expresslrs`.

<figure markdown>
![Lua3](/../assets/images/lua/wifi-bw.png)
</figure>

<figure markdown>
![WiFi Hotspot](/assets/images/WifiHotspotTX.png)
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

Выбрав правильный таргет и [Параметры сборки](/Manuals/FlashingOptions), cоберите кнопкой `Build` вашу прошивку через ExpressLRS Configurator.

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

Используя [Lua скрипт ELRS](https://github.com/ExpressLRS/ExpressLRS/blob/3.x.x-maintenance/src/lua/elrsV3.lua?raw=true) (правой кнопкой, сохранить как *.lua). Выберите `Wifi Connectivity` и включите WiFi кнопкой `Enable WiFi`. Если во время предыдущей прошивки вы прописали SSID своего домашнего WiFi или добавили его подключившись по `10.0.0.1`, то теперь модуль подключается к вашему роутеру, вместо раздачи точки.

<figure markdown>
![Lua3](/assets/images/lua/wifi-bw.png)
</figure>

Теперь ваше устройство будет видно внизу ExpressLRS Configurator, если выбран метод прошивки WiFi
<figure markdown>
![via WiFi](/assets/images/Method_TX_WiFi.png)
<figcaption>Прошивка по WiFi</figcaption>
</figure>

!!! note "Примечание"
    Иногда роутеры не присваивают устройствам dns имя (http://elrs_tx.local), если этот сайт не доступен вам придется сходить в амдинку вашего роутера и посмотреть какой ip получило устройство ExpressLRS, и вбить его вместо порта внизу ExpressLRS Configurator.

В ExpressLRS Configurator выбрав правильный таргет и [Параметры сборки](/Manuals/FlashingOptions), нажмите `Build and Flash` и прошейте передатчик. При успешной прошивке вы увидите результат как на картинке ниже:

<figure markdown>
![Build & Flash]
</figure>

<figure markdown>
![Wifi Update Log](/assets/images/WifiUpdateLog.png)
</figure>

Проверьте что версия внизу скрипта или на WiFi странице поменялась на ту что вы прошивали.

## Прошивка по USB/UART

- Device Category: 
    - Выбираем фирму вашего передатчика

- Device:
    - Выбираем модель вашего передатчика, например `HM ES24TX Pro Series 2400 TX` - для HappyModel PRO 

<figure markdown>
![via UART](/assets/images/Method_TX_UART.png)
<figcaption>Flashing via UART</figcaption>
</figure>

Если у вас модуль от HappyModel/BetaFPV перед прошивкой по USB нужно убедится что джамперы либо дип-свитчи стоят в правильном режиме для прошивки передатчика `Tx Module Flashing`:

??? info "Открыть картинки"
    <figure markdown>
    ![JumperFS](/assets/images/jumper-es24Micro.png)
    <figcaption>ES24TX Full Size, Non Pro</figcaption>
    </figure>

    <figure markdown>
    ![JumperLite](/assets/images/jumper-es24Lite.png)
    <figcaption>ES24TX Lite, for Jumper T-Lite</figcaption>
    </figure>

    <figure markdown>
    ![DipswitchSlim](/assets/images/dipswitch-es24slim.png)
    <figcaption>ES24TX Slim, Iron Man</figcaption>
    </figure>

    <figure markdown>
    ![DipswitchSlimPro](/assets/images/dipswitch-es24slimPro.png)
    <figcaption>ES24TX Slim Pro</figcaption>
    </figure>

    <figure markdown>
    ![DipswitchPro](/assets/images/dipswitch-Pro.png)
    <figcaption>ES24TX Pro 1W</figcaption>
    </figure>

     <figure markdown>
    <img class="center-img" src="https://user-images.githubusercontent.com/1081265/208266962-2e00a222-d44f-48b8-8ea0-e4a9a8433e64.png">
    <figcaption>BetaFpv</figcaption>
    </figure>


Воткните USB в передатчик. Убедитесь что у вас есть [драйвера на CP210x](https://www.silabs.com/developers/usb-to-uart-bridge-vcp-drivers) для Windows (Для Mac/Linux не нужно). Проверьте в диспетчере устройств что у устройства нет восклицательного знака и драйвера встали. Устройство должно называться CP210x и иметь номер COM-порта.


<figure markdown>
![CP210x Drivers](/assets/images/CP210xDriverDownload.png)
</figure>

В ExpressLRS Configurator выбрав правильный таргет и [Параметры сборки](/Manuals/FlashingOptions), нажмите `Build and Flash` и прошейте передатчик. Дождитесь окончания, при успешной прошивке будет надпись "Success"


<figure markdown>
![Build & Flash]
</figure>

Соберите модуль обратно, если вы его разбирали, вставьте в аппу запускайте LUA Script и проверяйте работоспособность, джамперы можно оставить так если вы не пользуетесь ELRS Backpack или даже не знаете что это такое.

[ExpressLRS Lua script]: https://github.com/ExpressLRS/ExpressLRS/blob/3.x.x-maintenance/src/lua/elrsV3.lua?raw=true
[Build]: /assets/images/Build.png
[Build & Flash]: /assets/images/BuildFlash.png
[Firmware Options]: ../firmware-options.md
[Radio Preparation]: tx-prep.md
