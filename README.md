# Экран параметров железа ПК
* [Описание проекта](#chapter-0)
* [Папки проекта](#chapter-1)
* [Используемые библиотеки](#chapter-2)
* [Схема подключения](#chapter-3)
* [Анализ использования памяти](#chapter-4)

### Версии прошивки
- m3.0 (первая которую решил выложить)
  - все настройки перенесены из программы в скетч (есть выбор источника настроек)
  - если запрещено получать настройки с ПК то LED и вентилятор работает по температурепературе
  - добавлено управление яркостью экрана и LED через фоторезистр
  - добавлены библитеки "GyverTimer" и "GyverButton"
  - удержание любой кнопки 2 сек. переводит на начальный экран
  - если присвоить значение 0 пинам отвечающим за те или иные функции (BTN2, LED_GP_PIN, LED_CP_PIN, LED_R, LED_G, LED_B, FAN_PIN, SENSOR_PIN, BACKLIGHT), то они будут отключены при компиляции скетча
  - добавлена настройка выбора источника данных для адресных светодиодов макс. мин. с компьютера или разные для ЦП и ГП из скетча
  - настройка LED brighness переработана и изменяет яркость дисплея адресной и обычной ленты в пределах минимума и максимума обозначенных в настройках скетча
  - добавлена настройка для отключения построения графиков (PLOT)
  - добавлена настройка (MICRO) для переключения используемых библиотек (микро версии AlexGyver или стандартные)
  - при использовании стандартной библиотеки датчика DS18B20 используется паразитное питание, при использовании микро нормальное питание и отдельные пины для каждого датчика
  - если SENSOR_PIN2 = 0 то отображается только один датчик
- m3.1
  - немного кастомизации (можно выбрать вариант полосы "загрузки")
- m3.2
  - добавлена плавность изменения цвета при режиме по температуре
  - изменен алгоритм отображения цвета Manual COLOR (0 выкл, 1-7 яркие цвета, 8 радуга, 9 огонь, 10-1000 по радуге (с фиолетовым!))

<a id="chapter-0"></a>
## Описание проекта
За основу взяты проекты:
  - ["ЭКРАН С ПАРАМЕТРАМИ ЖЕЛЕЗА ПК С РЕОБАСОМ И ПОДСВЕТКОЙ"](https://alexgyver.ru/pcdisplay/) v. 1.6
  - ["МОДДИНГ ПК С LED И ARDUINO"](https://alexgyver.ru/pcdisplay_v2/) v. 1.0

<a id="chapter-1"></a>
## Папки проекта
- **libraries** - библиотеки проекта. Заменить имеющиеся версии
- **firmware** - прошивка для Arduino, файл в папке открыть в Arduino IDE
- **HardwareMonitor** - программа, необходимая для работы устройства
- **schemes** - наглядная схема

<a id="chapter-2"></a>
## Используемые библиотеки
* [FastLED](https://github.com/FastLED/FastLED) v. 3.3.3
* [LiquidCrystal_I2C](https://github.com/marcoschwartz/LiquidCrystal_I2C) v. 1.1.4
* [TimerOne](https://github.com/PaulStoffregen/TimerOne) v. 1.1
* [DallasTemperature](https://github.com/milesburton/Arduino-Temperature-Control-Library) v. 3.9.0
* [OneWire](https://github.com/PaulStoffregen/OneWire) v. 2.3.5
* [GyverButton](https://github.com/AlexGyver/GyverLibs) v. 3.5
* [GyverTimer](https://github.com/AlexGyver/GyverLibs) v. 3.2
* [microWire](https://github.com/AlexGyver/GyverLibs) v. 2.1
* [microLiquidCrystal_I2C](https://github.com/AlexGyver/GyverLibs) v. 1.1
* [microDS18B20](https://github.com/AlexGyver/GyverLibs) v. 2.2

<a id="chapter-3"></a>
## Схема подключения
![SCHEME](https://github.com/MalfurionST/PCdisplay/blob/master/schemes/PCdisplay.png)

<a id="chapter-4"></a>
## Анализ использования памяти

Функция         | Arduino | GyverCore | Разница, Flash 
----------------|---------|-----------|---------------
millis	      	| 26      | 24	      | 2
micros		      | 24	    | 20	      | 4
pinMode         | 114     | 24        | 90             
digitalWrite    | 200     | 24        | 176            
digitalRead     | 190     | 24        | 166           
analogWrite     | 406     | 48        | 358            
analogRead      | 32      | 72        | -40            
analogReference | 0       | 22        | -22            
attachInterrupt | 212     | 180       | 32             
detachInterrupt | 198     | 150       | 48         
tone      	    | 1410    | 740       | 670       
Serial begin    | 1028    | 166       | 862            
print long      | 1094    | 326       | 768            
print string    | 2100    | 1484      | 616            
print float     | 2021    | 446       | 1575           
parseInt        | 1030    | 214       | 816            
readString      | 2334    | 1594      | 740            
parseFloat      | 1070    | 246       | 824   
