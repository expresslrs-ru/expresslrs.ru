# Приемники
При выборе приемников для ExpressLRS есть два важных фактора:
 - Рабочая частота - должна быть такая же как и у передатчика - 2.4ГГц или 868/915 МГц. При этом выбор 868 или 915 - связан исключительно с антенной, идущей в комплекте. Сами приемники могут программно переключать частоту на необходимую.
 - Поддержка приемников со стороны разработчиков ExpressLRS - к сожалению некоторые производители не дают свои приемники на тестирование и подразумевают что они будут использоваться с прошивками для приемников других производителей. Разница в схемотехнике может приводить к тому, что разработчики, оптимизируя прошивку под оригинальный приемник, невольно поломают ее работоспособность на подобном "клоне".

 > Отдельно хотелось бы обратить внимание на то, что некоторые производители, умудряются выпускать откровенно косячные приемники. Какие-то косяки можно обойти программно и команда ExpressLRS пишет фиксы или это можно сделать паяльником, а какие-то - увы нет.

Так же приемники могут иметь дополнительный функционал:
 - Возможность прошивки по Wi-Fi - имеют большинство приемников, так как сделаны на основе управляющего контроллера ESP8285, который имеет встроенный радиомодуль. Не поддерживается приемниками на контроллерах STM32, таких как FrSky R9. При этом приемники на основе ESP - еще и дешевле, так как нехватки этих микроконтроллеров на рынке нет.
 - Встроенный PA+LNA (усилитель для режима передачи телеметрии и малошумящий усилитель для приема) - есть далеко не во всех приемниках. Его наличие полезно для полетов 10+ км. На более близких дистанциях он не обязателен.
 - Псевдодиверсити - две антенны, переключение между которыми осуществляется программно, анализируя качество сигнала по очереди на каждой из них. Анализ происходит с очень высокой частотой, по этому заявленный функционал работает отлично и может быть полезен. Приемников с настоящим диверсити (когда каждая антенна подключена к своему трансиверу и осуществляет прием всегда, без переключения, а контроллер, выбирает целый сигнал с того трансивера, на котором он есть) на данный момент нет.
 - ШИМ(PWM)-выходы - позволяет подключить приемник непосредственно к регуляторам и сервомашинкам, минуя полетный контроллер. Полезны для "бомжелетов", машинок, катеров.
 - Керамическая антенна - обладает меньшей чувствительностью, но жестко установлена на плате и имеет минимальные размеры. Такие приемники удобно использовать на тинивупах и других моделя, которые летают вблизи и имеют ограниченное пространство.

 


## 2.4 Ghz

### Matek

Качественные беспроблемные приемники с отличными характеристиками

|  OK   | Название         | Антенна | Телеметрия | Прочее |
|-----|------------------|----------|------------|----------|
| ✅ |  [ELRS‑R24‑D](http://www.mateksys.com/?portfolio=elrs-r24#tab-id-1)      | Диполь - 2шт.       | PA+LNA 22.5dbm | псевдодиверсити  |
| ✅ |  [ELRS‑R24‑S](http://www.mateksys.com/?portfolio=elrs-r24#tab-id-2)       | SMD (керамическая)  | PA+LNA 20dbm | - |
| ✅ |  [ELRS‑R24‑P](http://www.mateksys.com/?portfolio=elrs-r24-p)       | Диполь  | 12dbm | 6 ШИМ(PWM) выходов, 1 вход для датчика напряжения без делителя (макс 3v3, пока не поддерживается), может работать как обычный CRSF приемник |

### HappyModel

Качественные недорогие приемники. С  мая по октябрь 2021 года были выпущены партии, в которых использовался регулятор напряжения, не позволяющий приемникам нормально запускаться. Проблема  заключалась в том, что контроллеры при инициализации потребляли больший ток, чем ожидалось. Решена программно правильной инициализацией, и больше не актуальна. Приемники всех партий работают отлично.

|  OK   | Название         | Антенна | Телеметрия | Прочее |
|-----|------------------|----------|------------|----------|
| ✅ |  [EP1](https://www.happymodel.cn/index.php/2021/04/10/happymodel-2-4g-expresslrs-elrs-nano-series-receiver-module-pp-rx-ep1-rx-ep2-rx/)      | T-диполь       | 12dbm |  |
| ✅ |  [EP2](https://www.happymodel.cn/index.php/2021/04/10/happymodel-2-4g-expresslrs-elrs-nano-series-receiver-module-pp-rx-ep1-rx-ep2-rx/)       | SMD (керамическая)  | 12dbm |  |
| ✅ |  [EPW5](https://www.happymodel.cn/index.php/2021/12/29/happymodel-expresslrs-elrs-epw5-2-4ghz-5ch-pwm-rc-receiver-for-fixed-wing/)       | T-диполь  | 12dbm | 5 ШИМ(PWM) выходов, может работать как обычный CRSF приемник |
| ❌ |  [PP](https://www.happymodel.cn/index.php/2021/04/10/happymodel-2-4g-expresslrs-elrs-nano-series-receiver-module-pp-rx-ep1-rx-ep2-rx/)       | SMD (керамическая)  | 12dbm | На основе STM32, нет Wi-Fi, больше не выпускается |


### GepRC

Являются клонами BetaFPV, низкий контроль качества и сомнительная экономия

### JHEMCU

Замечены косячные, нерабочие партии, стоит избегать

### Китайские ноунеймы с таобао

Встречаются на авитах/олх, неизвестные таргеты прошивок, непонятно что
