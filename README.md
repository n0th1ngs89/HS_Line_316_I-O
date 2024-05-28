# Документация проекта
## Авторы
1. Досаев Максим
2. Иванов Даниил
3. Шварц Максим
4. Умнова Екатерина

## Описание опставленной задачи
Необходимо организовать передачу входных и выходных данных между Sorting station PLC, Proccesing station PLC и Handling and packing station PLC. Так же поднять OPC сервер на Handling and packing station PLC для дальнейшего его использования командами отвечающими за разработку логики и SCADA системы.

## Ссылка на проект
[HS Line 316](https://drive.google.com/drive/folders/10Y2lL00LheItdtCxrIDzM5lAGOLko-ze?usp=sharing)

## Архитектура
ПЛК взаимодействут друг с другом благодаря стандарту Profinet 
![изображение](https://github.com/n0th1ngs89/HS_Line_316_I-O/assets/146949002/05848d01-be59-402f-ab1c-b9a10d6a265b)


## Возникшие сложности:
#### Ошибка и вылет при компиляции программы ПЛК с OPC UA server
При работа с данной установкой, нам надо было поднять OPC сервер на Handling and packing station PLC для того, чтобы команды которые отвечают за логику и SCADA систему могли с ними взаимодействовать. При попытке 
загрузки конфигруации с OPC сервером на ПЛК на Windows 10 и 11 мы с толкнулись с проблемой, что у нас вылетала программа Tia Portal при шифровании данных. Изначально я думал что проблема в моем компьюетере, поэтому мы попыталсиь загрузить конфигурацию с другого ноутбука, но тщетно. Так же предпринимали попытки запустить repair программы Tia Portal, но это тоже не помогло. В итоге мы поставили Tia Portal на компьютер в 316 кабинете на котором стоит Windows 7 и у нас все заработало и получилось загрузить конфигурацию. В общем с этой проблемой мы провозились более 5 часов.
## Таблица входных и выходных тэгов

### Proccesing station PLC
<table>
  <tr>
    <td>Тэги</td>
    <td>Описание</td>
    <td>Адрес</td>
  </tr>
  <tr>
    <th colspan="3">Входы</th>
  </tr>
  
  <tr>
    <td>processing_input_1_workpiece_detected</td>
    <td>шайба на определении цвета</td>
    <td>I0.1</td>
  </tr>
<tr>
    <td>processing_input_2_workpiece_silver</td>
    <td>датчик для серебристой шайбы</td>
    <td>I0.2</td>
  </tr>
  <tr>
    <td>processing_input_5_carousel_init</td>
    <td>поворот карусели на 45 градусов</td>
    <td>I0.5</td>
  </tr>
  <tr>
    <td>processing_input_6_hole_detected</td>
    <td>дырка сверху шайбы</td>
    <td>I0.6</td>
  </tr>
  
  <tr>
    <td>processing_input_7_workpiece_not_black</td>
    <td>датчик для красной и серебристой шайбы</td>
    <td>I0.7</td>
  </tr>
  <tr>
    <th colspan="3">Выходы</th>
  </tr>
  <tr>
    <td>processing_output_0_drill</td>
    <td>включить дрель</td>
    <td>Q0.0</td>
  </tr>
<tr>
    <td>processing_output_1_rotate_carousel</td>
    <td>включить вращение карусели</td>
    <td>Q0.1</td>
  </tr>
  <tr>
    <td>processing_output_2_drill_down</td>
    <td>опустить дрель</td>
    <td>Q0.2</td>
  </tr>
  <tr>
    <td>processing_output_3_drill_up</td>
    <td>поднять дрель</td>
    <td>Q0.3</td>
  </tr>
  
  <tr>
    <td>processing_output_4_fix_workpiece</td>
    <td>зафиксировать шайбу</td>
    <td>Q0.4</td>
  </tr>
<tr>
    <td>processing_output_5_detect_hole/td>
    <td>опустить определитель дырки</td>
    <td>Q0.5</td>
  </tr>
</table>

### Handling and packing station PLC

<table>
  <tr>
    <td>Тэги</td>
    <td>Описание</td>
    <td>Адрес</td>
  </tr>
  <tr>
    <th colspan="3">Входы</th>
  </tr>
  
  <tr>
    <td>handling_input_0_workpiece_pushed</td>
    <td>шайба выдвинута</td>
    <td>I0.0</td>
  </tr>
<tr>
    <td>handling_input_1_grippe_at_right</td>
    <td>гриппер в крайнем правом положении</td>
    <td>I0.1</td>
  </tr>
  <tr>
    <td>handling_input_2_gripper_at_start </td>
    <td>гриппер в начальном положении</td>
    <td>I0.2</td>
  </tr>
  <tr>
    <td>handling_input_3_gripper_down_pack_lvl</td>
    <td>гриппер над упаковщиком</td>
    <td>I0.3</td>
  </tr>
  
  <tr>
    <td>packing_input_7_pack_turned_on</td>
    <td>упаковщик включен</td>
    <td>I0.7</td>
  </tr>
  <tr>
    <th colspan="3">Выходы</th>
  </tr>
  <tr>
    <td>handling_output_0_to_green</td>
    <td>зеленый цвет светофора</td>
    <td>Q0.0</td>
  </tr>
  <tr>
    <td>handling_output_1_to_yellow</td>
    <td>желтый цвет светофора</td>
    <td>Q0.1</td>
  </tr>
<tr>
    <td>handling_output_2_to_red</td>
    <td>красный цвет светофора</td>
    <td>Q0.2</td>
  </tr>
  <tr>
    <td>handling_output_3_gripper_to_right</td>
    <td>движение гриппера вправо</td>
    <td>Q0.3</td>
  </tr>
  <tr>
    <td>handling_output_4_gripper_to_left</td>
    <td>движение гриппера влево</td>
    <td>Q0.4</td>
  </tr>
  
  <tr>
    <td>handling_output_5_gripper_to_down</td>
    <td>переключатель движения гриппера вниз</td>
    <td>Q0.5</td>
  </tr>
<tr>
    <td>handling_output_6_gripper_to_open</td>
    <td>переключатель открытия клешни гриппера</td>
    <td>Q0.6</td>
  </tr>
  <tr>
    <td>handling_output_7_gripper_push_workpiece</td>
    <td>вытолкнуть шайбу</td>
    <td>Q0.6</td>
  </tr>
<tr>
    <td>packing_output_4_push_box</td>
    <td>вытолкнуть коробку</td>
    <td>Q0.4</td>
  </tr>
  <tr>
    <td>packing_output_5_fix_box_upper_side</td>
    <td>зафиксировать верхнюю часть коробки</td>
    <td>Q0.5</td>
  </tr>
  <tr>
    <td>packing_output_6_fix_box_tongue/td>
    <td>зафиксировать язычок коробки</td>
    <td>Q0.6</td>
  </tr>
  
  <tr>
    <td>packing_output_7_pack_box</td>
    <td>упаковать коробку</td>
    <td>Q0.7</td>
  </tr>
</table>

### Sorting station PLC
<table >
  <tr>
    <td>Тэги</td>
    <td>Описание</td>
    <td>Адрес</td>
  </tr>
  <tr>
    <th colspan="3">Входы</th>
  </tr>
  
  <tr>
    <td>sorting_input_3_box_on_conveyor</td>
    <td>коробка на конвейере</td>
    <td>I0.3</td>
  </tr>
<tr>
    <td>sorting_input_4_box_is_down</td>
    <td>коробка упала в желоб со своим цветом</td>
    <td>I0.4</td>
  </tr>
  <tr>
    <th colspan="3">Выходы</th>
  </tr>
  <tr>
    <td>sorting_output_0_move_conveyor_right </td>
    <td>включить движение конвейера вправо</td>
    <td>Q0.0</td>
  </tr>
<tr>
    <td>sorting_output_1_move_conveyor_left</td>
    <td>включить движение конвейера влево</td>
    <td>Q0.1</td>
  </tr>
  <tr>
    <td>sorting_output_2_push_silver_workpiece</td>
    <td>толкатель для серебристой шайбы</td>
    <td>Q0.2</td>
  </tr>
  <tr>
    <td>sorting_output_3_push_red_workpiece</td>
    <td>толкатель для красной шайбы</td>
    <td>Q0.3</td>
  </tr>
</table>


## Передача и сбор данных на ПЛК
### Передача данных
Передачу данных была реализованна с помощью блока PUT в Tia Portal
![изображение](https://github.com/n0th1ngs89/HS_Line_316_I-O/assets/146949002/6581da98-b933-4021-b081-be2306663c30)

### Сбор данных
Сбор данных был реализован с помощью блока GET в Tia Portal

![изображение](https://github.com/n0th1ngs89/HS_Line_316_I-O/assets/146949002/b206100b-15a7-44b3-8e9e-9ef3aa4cb85b)

