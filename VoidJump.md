# Прыжок из бездны

Когда высота персонажа на экране равна 255, можно нажать Прыжок и выпрыгнуть из ямы. В БТДД можно зажимать турбо Прыжок, чтобы задержаться на месте и потом уже выпрыгнуть. Можно делать гипер-прыжок.

Однако, высота на экране не считается напрямую. Она складывается из высоты над тенью и высоты тени на экране.
```
if ($493 - $475) > 255, then die
```

Скорость падения превосходит 1 пиксель за кадр, поэтому попасть в нужную позицию высоты можно не всегда. В игре есть несколько мест, с которых при обычном беге можно сбежать и попасть в 255. Но в основном падение перса не совпадает с этой точкой, например если он 1 раз уже выпрыгнул из ямы и летит в нее второй раз. Здесь приходится менять длительность прыжка. Если же это например потолок над ямой, то можно нажать Влево+Вправо на кадр или несколько, чтобы при спрыгивании попасть в эту позицию.

http://www.youtube.com/watch?v=9EEbQld_nSs

