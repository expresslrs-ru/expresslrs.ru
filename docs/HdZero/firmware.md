---
description: Прошивка очков/приемников/передатчиков
---

Для кооректной работы всего и вся в нашем непростом пути энтузиастов малосерийного опенсорса рекомендуется всегда обновлять все на последние прошивки.

## Где скачать прошивку?

[Сайт HdZero](https://www.hd-zero.com/document) - тут в разделе Firmware лежат архивы по дате, внутри архива прошивка для VTX+VRX+Очков

[GitHub](https://github.com/hd-zero) - тут немного иначе, есть отдельный репозиторий под [прошивки для передатчиков](https://github.com/hd-zero/hdzero-vtx) и [прошивки очков](https://github.com/hd-zero/hdzero-goggle)

Есть ли разница?

В основном нет, релизы на гитхабе имеют понятную нумерацию, а на сайте просто дату релиза. На деле же это идентичные файлы. Но на GitHub они появляются зачастую раньше, также можно тестить конкретные PullRequestы и быть на острие ножа актуальности.

## Прошивка очков

[Скачиваем с сайта](https://www.hd-zero.com/document) последний архив, открываем архив. Находим в архиве другой архив с названием `HDZEROGOGGLE_RevXXX.zip`, берем из него ТОЛЬКО ОДИН ФАЙЛ `HDZERO_GOGGLE-xx-xxx-x.x.xx-.bin` и закидываем в корень флешки очков.

Включаем очки и идем во вкладку `Firmware`, нажимаем кнопку `Update Google` и ждем окончания процесса. После этого перезагружаем очки.

## Прошивка приемников 

[Скачиваем с сайта](https://www.hd-zero.com/document) последний архив, открываем архив. Находим в архиве другой архив с названием либо `HDZeroVRX4_4SMA_RevXXX.zip` для приемника HdZero (с 4мя SMA антеннами), либо `SharkByteVRX_2SMA_RevXXX.zip` для приемника SharkByte (с 2мя белыми патчками и 2мя SMA).

Распаковываем содержимое архива на флешку приемника, включаем приемник, ждем окончание процесса, перезагружаем.

# Прошивка передатчиков

## Прошивка через очки

[Скачиваем с сайта](https://www.hd-zero.com/document) последний архив, открываем архив. 
Из архива берем другой архив в зависимости от типа передатчика, внутри архива забираем файл `HDZERO_TX.bin` и кладем в корень флешки.

Соединяем VTX с очками кабелем.

Включаем очки и идем во вкладку `Firmware` и нажимаем кнопку `Update VTX` дождитесь окончания прошивки.

Файл прошивки не удаляется с флешки очков, таким образом можно за раз прошить несколько одинаковых видеопередатчиков.

## Прошивка через приемник

[Скачиваем с сайта](https://www.hd-zero.com/document) последний архив, открываем архив. 
Из архива берем другой архив в зависимости от типа передатчика, внутри архива забираем файл `HDZERO_TX.bin` и кладем в корень флешки.

Соединяем VTX с приемником кабелем.

Включаем приемник и процесс прошивки начинается автоматически. После этого перезагружаем обоих.

После прошивки файл удаляется с флешки, если вам надо прошить несколько одинаковых передатчиков создайте в корне флешки пустой файл с названием `“DONOTREMOVE.txt`
