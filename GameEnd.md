# Вызов конца игры.

1) Из [сбитого поинтера конфигов объектов](LevelEnd) читается строчка с нулевым ID, у которого оказывается координата `X=#$C8`.

2) Объекты с ID #1 и #2 это объекты игроков. Они всегда привязаны к слотам 0 и 1. (из типа объекта вычитается 1)

3) Нулевого объекта в нормальных условиях нету. Из-за этого нулевой при чтении считается тоже игроком. (всё что меньше ID=3). И получается 0-1=`$FF` - объект слот `$FF`.

4) Далее проверяется наличие жизней-седречек (проверка не кончились ли жизни)- в нормальных условиях это адреса 11 и 12. Со слотом сбитом на `$FF` получается = `$110`. Число в этом адресе должно быть положительное. (иначе не загрузится)

5) Далее читается конфиг и при чтении X от этого объекта (числа `#$C8`) оно попадает в `$3FD+$FF=$4FC`. `$3FD=Objects_Xpos_L`, `$FF` - номер слота. `$4FС` оказывается адресом `Objects_HitID`: (что-то связанное с анимацией)

6) При обработке их грузится поинтер для этого удара, анимации которого не существует. Из других данных получается поинтер на `$2207`.  (ппу дата чтоли)

7) Из него начинает читаться анимация - `#$FE, #$90, #$18`

8) Чуть позже идет обработка анимации. `#$FE` считывается и делается andi с `#$1F`. Это должно указывать на требуемый для
анимации код, но поинтеров там всего 22 (`$16`), то есть меньше. Опять грузится 'левый' поинтер (число `$75BD` с адреса рома `$DB76`).

9) Для выполнения анимации должен прыгнуть по это поинтеру то есть попадает `JMP $75BD`.
Совершенно левое место - какое-то баттери бак-ап рам или ворк рам. В ней все залито числом `$6F`.(на картидже не знаю - в фцеух так).

10) На этой команде проц не виснет и едет дальше пока не доедет до `$8000`.

11) Там идет обычный джамп. В результате которого видимо попадает на функцию концовки.
```asm
    $8000:6C 13 00  JMP ($0013) = $8045                                            A:06 X:45 Y:06 S:FA 
    $8045:4C 24 AC  JMP $AC24       
```
`$45`=69, 69/3 - 23-ая функция в банке 6. (в каждом банке вначале таблицы идут из джампов- а они по 3байта) 
