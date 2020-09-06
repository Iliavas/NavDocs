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
      * `CalibrationGyroscope` - 
