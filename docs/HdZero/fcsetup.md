---
description: Настройка полетника для HdZero
--- 
## Пайка передатчика

Паяем на свободный Uart: TX на RX, RX на TX. Провод SmartAudio не паяем, он не актуален и не нужен.

<figure markdown>
![wiring](https://oscarliang.com/wp-content/uploads/2022/07/hdzero-vtx-fc-wiring-connection-diagram-uart-tx-rx.jpg)
</figure>

## Betaflight

Прошиваем полетник на `4.4.x`, так как только с этой версии появляется MSPVTX и Smartaudio over MSP.

Заходим во вкладку `Presets` и набираем в поиске hdzero

<figure markdown>
![preset](/../assets/images/hdzero/preset1.png)
</figure>

Внутри пресета выбираем:
1) Тип вашего видеопередатчика
2) Uart на который вы припаяли видеопередатчик 

<figure markdown>
![preset](/../assets/images/hdzero/preset2.png)
</figure>

Нажимаешь кнопку `Pick`, потом `Save and Reebot`

Настраиваем OSD по вкусу на вкладке OSD и собственно все.

Теперь VTXом можно управлять по Smartaudio также как аналоговым передатчиком, переключать  мощность, питмод и тд. 