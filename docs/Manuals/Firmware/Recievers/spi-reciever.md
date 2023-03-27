---
description: Инструкция по прошивке SPI приемников
---

!!! note "Поддерживаемые пакетрейты"
    D(D250, D500), F(F500, F1000) и Full Res(100Hz Full Res, 333Hz Full Res) режимы (пакет рейты) не поддерживаются SPI приемниками, и аппаратура в этом режиме не сможет сбиндится с SPI приемником.

На вупах часто стоят полётники с SPI приёмниками. Их не нужно прошивать отдельно, их прошивка уже содержится в самой прошивке Betaflight.

!!! info "Примечание"
    ExpressLRS конфигуратор не понадобится для прошивки SPI приемника.

Betaflight 4.3.x работает только с ELRS 2.x.x передатчиками

Betaflight 4.4.x работает только с ELRS 3.x.x передатчиками

Не забывайте, что при апгрейде с 4.3 на 4.4 слетают настройки полетника, перед обновлением делайте бекап с помощью CLI. Напишите в CLI команду `diff all` и нажмите save to file. После прошивки зайдите в CLI нажмите load file и выберите ранее сохраненый файл. При переходе с 4.3 на 4.4 в CLI могут появится ошибки в связи с отсуствием некоторых параметров, не пугаемся пишем save и жмем enter, возможно дважды.

Для прошивки переходим в [Betaflight Configurator](https://github.com/betaflight/betaflight-configurator/releases), во вкладку `Update Firmware` и выбираем нужную вам прошивку (4.3 или 4.4), таргет  вашего полетника определите сами, но он должен содержать слово SX1280. Также вам скорее всего понадобятся драйвера STM32DFU, [скачать тут](https://github.com/expresslrs-ru/expresslrs-ru.github.io/raw/main/docs/assets/files/STM32-DFU.zip).

После прошивки и восстановления ваших настроек перейдите на вкладку Radio и установите приемник в режим `SPI Reciever` с протоколом `ExpressLRS`.

<figure markdown>
![BF settings](/assets/images/SPIReceiverSetup.png)
</figure>

## Бинд SPI приемников

Есть два способа бинда, о них ниже

### С помощью кнопок

Вы можете перевести приемник в режим бинда несколькими способами:

- Кнопкой "Bind" на вкладке приемник в Betaflight.
- Физической кнопкой bind на полетнике
- Командой `bind rx` в CLI.

Когда вы перевели приемник в режим бинда, в Lua скрипте ELRS на аппаратуре также нажмите BIND. Приемник с передатчиком должны соединится. Нажмите save или пропишите save в CLI.

**Порядок важен, сначала переводите в бинд приемник, потом передатчик**

Видео:

<figure markdown>
<iframe width="560" height="315" src="https://www.youtube.com/embed/U2sxqx2oT4k" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</figure>

### Бинд фразой

#### Генератор UID из бинд фразы

Фраза:

<div class="bp-wrapper">
  <input class="md-input bp-input" type="text" placeholder="expresslrs" />
</div>

!!! info "Не обновляется?"
    Если поле не работает обновите страницу и подождите минутку, оно может обновлятьяся не мгновенно.

Ваш UID
```
```

#### Установка бинд фразы на полетник
Перейдите в CLI и вставьте команду ниже
```
```

<script type="text/javascript" src="https://raw.githubusercontent.com/expresslrs-ru/expresslrs-ru.github.io/main/docs/assets/javascripts/crypto-js.js"></script>
<script type="text/javascript">
  window.addEventListener("load", (event) => {
    initBindingPhraseGen();
  });
</script>

Начиная с версии Betaflight Configurator 10.9.0 фразу можно вбивать прямо в бетафлае, на вкладке приемник для этого появилось соответсвующее поле. Введите вашу фразу и нажмите `Save and Reboot`.

!!! note "Поддерживаемые пакетрейты"
    D(D250, D500), F(F500, F1000) и Full Res(100Hz Full Res, 333Hz Full Res) режимы (пакет рейты) не поддерживаются SPI приемниками, и аппаратура в этом режиме не сможет сбиндится с SPI приемником.

