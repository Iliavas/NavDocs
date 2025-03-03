# GENERAL

В проекте есть 2 главных сцены:
* `MainMenu` - сцена главного меню
* `MapBase` - сцена где будет прогружаться карта

Также в проекте есть несколько побочных сцен (папка `AdditiveScenes`):
* `OnCreateScene` - сцена ввода имени карты
* `InputTarget` - сцена для ввода точки куда нужно пройти пользователю
* `InputCurrentPos` - сцена для ввода точки где находится пользователь

в проекте присутсвует папка `Resources` ([почитать про смысл этой папки в движке можно здесь](https://docs.unity3d.com/ScriptReference/Resources.html))
в ней присутствуют следующие папки:
* `AdditionalGraphics` - в этой папке находятся элементы которые я не смог причислить ни к одной из следующих папок (в данный момент там есть 1 элемент
    префаб точки поворота при калибровки гироскопа)
* `ObjectsUsedInMap` - в этой папке находятся все объекты которые используются в карте напрямую (а также их имена используются напрямую в коде так что менять их         нельзя). В этой папке находится:
    * `edge` - префаб который используется как часть пути (прямая линия между 2 точками) вместе все префабы с именем `edge` формируют граф по которому может                перемещаться пользователь
    * `PathToDest` - префаб который показывает путь пользователю от точки где он находится до точки куда ему надо пройти
    * `Point` - префаб точки на карте
    * `TailComp` - префаб который исполбзуется для отрисовки пройденного пути пользователя
    * `user` - префаб пользователя
* `UI` - в этой папке находятся элементы интерфейса которые используется в проекте и появляется на сцене в Runtime. В этой папке находится:
    * `Button` - префаб кнопки который используется при отображении имен карт в главном меню
    * `CalibrationGyroscope` - префаб калибровки для гироскопа
    * `LoadMap` - префаб кнопки на сцене `MapBase` для обновления карты
    * `PointCreation` - input поле для создания кнопки
    * `SaveMap` - кнопка для создания карты

# Scene Explanation

### Важное замечание
при желании отредактировать какую-либо сцену нельзя удалять существующие на сцене объекты или изменять их теги, но можно менять их свойства

## MainMenu
Изначально на сцене присутствуют 2 объекта (имеется ввиду объекты которые будут использованы в Runtime) `Main camera` и кнопка для создания карты. 
На объекте `Main camera` изначально весит скрипт `StartApp` который отрабатывает один раз за запуск приложения - при запуске. Вся его суть заключается в том,
чтобы отпаристь директорию `Application.persistentDataPath+"/binaries"` в которой хранятся бинарники всех карт, и для каждой карты создать кнопку для её (карты) загрузки.

## InputCurrentPosition
На эту сцену можно попасть путем нажатия кнопок закрузки карты из `MainMenu`
На сцене 2 "живых" объекта: Input поле для ввода имени точки рядом с которой находится пользователь и кнопка завершения этого действия.

## InputTarget
Эта сцена аналогична сцене `InputCurrentPosition` за одним исключением: на этой сцене пользователь вводит значение точки куда он хочет попасть. Хочу заметить, что
на сцене присутсвует кнопка `DevMode` которая пропускает эту сцену и запускает сцену `MapBase` без построения маршрута, во время билда приложения для пользователя
эта кнопка должна быть удалена

## OnCreateScene
На сцене присутствует 2 объекта: Input поле для ввода имени новой карты и кнопка для создания пустой карты с именем полученном из Input'а.


## MapBase 
Эта сцена прогрузки карты на ней будут происходить все основные действия пользователя. На карте присутствует 2 кнопки для создания новой точки и для сохрания карты (естественно при финальном билде эти кнопки надо будет удалить).
Также на сцене присутствует компонент `MainCamera` на котором висит большинство скриптов, связанных с обработкой чего-либо и менеджментом впринципе 
(об этом в документации дальше)

### MapBaseWorking
Если вы хотите создать красивый продукт, то с этой сценой придется много работать, и конкретно этот абзац документации посвящен получению всех (или почти всех)
данных которые могут быть полезны при создании навигатора.
Изначально сцена `MapBase` может загрузить карту, отобразить ее в Runtime, и построить маршрут из одной точки в другую
