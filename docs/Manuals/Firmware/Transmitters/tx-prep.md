---
description: Инструкция по первичной настройки аппаратуры под работу с ELRS
---

## Прошивка аппаратуры

ExpressLRS для работы требует протокол CRSFShot. Этот протокол поддерживается начиная с [OpenTX-2.3.12](https://www.open-tx.org/2021/06/14/opentx-2.3.12).

Но проще и лучше всего перейти на прошивку [EdgeTX](https://github.com/EdgeTX/edgetx/releases). Так как OpenTX перестал нормально развиваться. Также EdgeTX помогает старинным аппам типо QX7 и X9 поддерживать высокие рейты юарта через onebit хак, без пайки инвертора.

Самый простой способ прошивки EdgeTX это прошивка через сайт EdgeTX Buddy.
[Переходим по ссылке](https://buddy.edgetx.org/#/flash), втыкаем __выключенную__ аппаратуру в usb. И прошиваем. Далее обновляем содержимое флешки на этом же сайте.

Для прошивки необходимы драйвера [STM32DFU (скачать)](https://github.com/expresslrs-ru/expresslrs-ru.github.io/raw/main/docs/assets/files/STM32-DFU.zip)

## Настройка апппаратуры

### Скорость юарта Baud Rate

Baud Rate это скорость с которой Передатчик общается с аппаратурой. Измеряется в битах в секунд. Обычно имеет значение 115200bps and 400000bps.

Установка более высоких скоростей позволяет аппе быстрее общаться с ELRS модуем, снижая общую задержку и ускоряя работу LUA скрипта. Но не каждая аппаратура поддерживает высокие скорости (В основном проблема только на древних Frsky QX7/X9)

Поменять скорость можно в настройках аппаратуры, на странице Hardware (попасть туда можно зажав кнопку SYS). На прошивках начиная с EdgeTX 2.7.0 скорость меняется в настройках самой модели для внешних передатчиков, скорость для внутренних передатчиков все еще выставляется в Hardware.

<figure markdown>
![Baudrate](/assets/images/txprep-clr-hardware.jpg)
<figcaption>Baudrate на цветных аппах</figcaption>
</figure>

<figure markdown>
![Baud Rate](https://fpvfrenzy.com/wp-content/uploads/2017/11/baud-rate.jpg)
<figcaption>Baudrate на чб аппах</figcaption>
</figure>

Скорость передачи в 500Hz треует как минимум 400k Baud Rate.

1000Hz требует установку скорости свыше 400k.

Древние аппы Frsky такие как QX7, X9D, X10/S, и X12 требуют установки [Резистор Мода](https://blog.seidel-philipp.de/fixed-inverter-mod-for-tbs-crossfire-and-frsky-qx7/) либо OneBit хака в EdgeTX. Чтобы установить режим OneBit перейдите на вкладку Hardware в аппаратуре и уставновите Sample mode в OneBit, а Baud Rate в 400k или выше.

!!! info "Инфо"
    Если установлен BaudRate 115200, 250Hz будет максимально доступной скоростью линка.

Если вы наблюдаете проблемы с постоянной потерей и восстановлением телеметрии даже вблизи, возможно ваша аппа не тянет установленный высокий BaudRate, опустите его ниже или верните 400k и проблемы должны уйти.

### ADC Фильтр

ADC Фильтр на вкладке HardWare в OpenTX (либо в модели на EdgeTX) нужно отключать, так как он накладывает лишнюю фильтрацию и задержку на пакеты управления и только мешает.

Допустимо оствлять включенный ADC Фильтр для PWM приемников, так как у вас нет полетного контроллера, который и занимается сглаживанием сигнала.

## Настройка модели

### Протокол

!!! Примечание
    Если вы используете внешний передатчик, убедитесь что настройка встроенного (Internal RF) стоит в положении **OFF** (выключен).

    Если вы используете встроенный ELRS передатчик, то наоборот External RF = OFF, Internal RF = CRSF

ExpressLRS использует протокол **CRSF** для общенния между вашей аппаратурой и передатчиком. Вам нужно установить этот протокол в настройках модели аппаратуры, для внешнего либо внутреннего модуля (External RF/Internal RF):

<figure markdown>
![ExternalRF](/assets/images/txprep-bw-externalRF.jpg)
</figure>

<figure markdown>
![ExternalRF](/assets/images/txprep-clr-externalRF.jpg)
</figure>

Для аппаратур с внутренним(встроенным) ELRS передатчиком вам нужно установить настройку **Internal RF** в положение **CRSF** на странице настройки модели. Если же вы видите только **MULTI**, то надо сходить на вкладку Hardware (зажать SYS) и поменять **Internal RF** c **MULTI** на **CRSF**.

<figure markdown>
![InternalRF BW](/assets/images/txprep-bw-internalRF.jpg)
</figure>

<figure markdown>
![InternalRF Color](/assets/images/txprep-clr-internalRF.jpg)
</figure>

### Тумблеры и AUX каналы

По умолчанию созданнная в аппаратуре модель не имеет выведенных тумблеров в миксах. Только 4 оси стиков. Поэтому если в Betaflight/iNav у вас не работают тумблеры, вам нужно их назначить каналам на вкладке Mixes в настройках модели аппаратуры.

<figure markdown>
![mixes BW](/assets/images/txprep-bw-mixes.jpg)
</figure>

<figure markdown>
![mixes Color](/assets/images/txprep-clr-mixes.jpg)
</figure>

Выберите необходимый канал, зажмите кнопку выбора и нажмите Edit. Выберите Source и назначьте нужный вам тумблер для данного канада.
**ВАЖНО ПОМНИТЬ ЧТО ДЛЯ АРМА В ELRS НУЖННО ИСПОЛЬЗОВАТЬ ТОЛЬКО AUX1 (5Й КАНАЛ) И НИКАКОЙ ДРУГОЙ.**

<figure markdown>
![mixesAux BW](/assets/images/txprep-bw-mixAux.jpg)
</figure>

<figure markdown>
![mixesAux Color](/assets/images/txprep-clr-mixAux.jpg)
</figure>

**Теперь ваша аппаратура настроена, и можно переходить к инструкциям по прошивке ELRS модулей**