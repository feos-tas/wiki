#summary Цепляние за пушку в 3

=В нормальных условиях=

Стрелка и пушка не должны существовать одновременно.

Пушка грузится в 8 слот при появлении. До нее в этом слоте была капсула с веревками. Когда стрелка срывается с  места, после того как герои перепрыгнули и отпустили веревки - капсуле ставится флаг 1 в адрес $5A9. Это последний атрибут в РАМ объектов, он используется для РАЗНЫХ переменных. Когда в этом адресе капсула получает 1, она отпускает скроллинг экрана, а стрелка, которая и пишет туда эту единицу, улетает. По задумке разрабов - стрелка (ID = 0х58 в 7 слоте) улетает и слот очищается, как и 8-й, в котором капсула. И потом в первый свободный слот грузится пушка.

=При глюке=

Пушка уже выехала, а стрелка еще есть на экране. Стрелка думает, что в 8 слоте капсула, и надо сказать ей мол "я улетаю, отвязывай экран", и пишет еденицу в атрибут объекта в 8 слоте. А там уже пушка! И для пушки это означает, какой персонаж на ней висит! 1 - первый игрок, 2 - второй игрок. И вот, когда стрелка еще висит на экране, а персонаж запрыгивает на пушку, ей пишется его номер. В этот момент стрелка решает, что ей пора, и если у пушки прописано 2 (на пушке висит второй перс), она СИЛОЙ вписывает туда 1 (в ходе какогото еще глюка) и улетает восвояси.

Глюк готов - пушка думает что на ней висит первый игрок, поэтому она не скидывает с себя ВТОРОГО. Отцепиться можно если нажать вниз.

Потом камера умирает, но не сбрасывает с себя 2 перса. У него так и остается 88 в атрибуте МЕНЯ НЕСУТ. То есть всякий объект, рождающийся в 8 слоте будет тащить его на себе. Следующие 2 пушки являются последним шансом для 2 игрока. Если он после того как услышит звук своей смерти и увидит обнуление ХП нажмет ВНИЗ, он отцепится от ДРУГОЙ пушки и воскреснет. Если же будет жать удар - его невидимый стпрайт изобьет вторую пушки и навсегда потеряет возможность вернуться к жизни, так как дальше яма и он не сможет выкинуть веревку.

http://www.youtube.com/watch?v=e3f_TYS1ARA