---
description: Маленький диверсити передатчик из приемника
---
Это инструкция по переделке ESP32 (True Diversity) приемника в миниатюрный диверсити передатчик. Который удобно встраивается в аппы типо Tango 2.

Мощность передачи будет 50мвт, вполне достаточно для вупов и прочих полетов на мелкашах дома и в парках.

!!! danger "Внимание"
    Все действия вы делаете на свой страх и риск. Не забудьте использовать понижайку, так как без нее  приемник может сгореть.

## Что нам понадобится:

- Приемник [HappyModel EP1 Dual](https://rcsearch.ru/-c41393) желательно TXCO версии, либо BetaFPV Super-D (не проверенно мной)
- Понижайка до 5v, например [Matek](https://rcsearch.ru/-c1602)

!!! note "Другие приемнники"
    Так как мы подключаем наш передатчик(приемник) по S.Port (HalfDuplex по одному проводу), то нам подойдут только ESP32 приемники (EP1 DUAL/SuperD), приемники на ESP8285 не умеют в HalfDuplex и годятся только для встройки вместо мультипротокольного модуля, по полноценному RX/TX 

## Подключение 

У меня есть видео по встройке такого приемника в Tango 2, но процесс прошивки там не актуален. Смотрите только часть с пайкой и подключением, постараюсь переделать видео, когда появится время:
<figure markdown>
<iframe width="560" height="315" src="https://www.youtube.com/embed/2cn96u_nlnw" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</figure> 

<figure markdown>
![BF settings](/assets/images/ep1_dual_tx.jpg)
<figcaption>Схема подключения</figcaption>
</figure>

<figure markdown>
![BF settings](/assets/images/ep1_dual_tx2.jpg){ width="400" }
<figcaption>Мой пример</figcaption>
</figure>

Паяем и подключаем по схеме, и втыкаем в аппаратуру. Не забудьте включить External модуль в настройках модели, чтобы на приемник (передатчик) пошло питание.

## Прошивка

!!! danger "Внимание"
    Процесс прошивки в видео на YouTube не актуален, так как по какой-то причине на новых прошивках (> 3.0.1) приемник перестает поднимать вайфай и не дает себя настроить, следуйте инструкции ниже.

Я собрал готовую кастомную прошивку, в которой уже все настроено и работает, но нужно будет прописать свою фразу на WiFI странице, после прошивки.

[Скачать прошивку](https://github.com/expresslrs-ru/expresslrs-ru.github.io/raw/main/docs/assets/files/EP1_DUAL_TX_nophrase_master.bin){ .md-button .md-button--primary } Сборка из master ветки 01.04.2023, без bind фразы

Скачиваем ``*.bin`` файл и прошиваем обычным способом на WiFi странице приемника.

В процессе прошивки ругнется на несовпадение таргета, это нормально, соглашаемся и прошиваем.

После успешной прошивки, открываем Lua Scrips ELRS и убеждаемся что у нас все работает.

<figure markdown>
![BF settings](/assets/images/ep1_dual_tx3.jpg){ width="600" }
</figure>
<figure markdown>
![BF settings](/assets/images/ep1_dual_tx4.jpg){ width="600" }
</figure>

Включаем в скрипте WiFi, подключаемся, выставляем свою фразу и летаем.

Если что-то не получилось и пошло не так, всегда можно прошить приемник обратно, по USB-UART.

Если остались вопросы переходите в телеграм и спрашивайте

[Telegram чатик](https://t.me/expresslrs_rus){ .md-button .md-button--primary } 