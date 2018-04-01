#summary Создание объекта "Конец уровня"

 # По логике разрабов, уровень 3 не рестартится при смерти жабы, пока не затронут чекпойнт трассы. Когда он затронут, в адрес $E5-E6 пишется поинтер на конфиг объектов, который потом в случае сметри жабы на байке пишется в $B7-B8. Мы умираем, не затронув чекпоинта, таким образом в $B7-B8 пишется #$00! СЛЕДОВАТЕЛЬНО, объекты начинают читаться прямо с начала РАМ. 
 # В начале каждого уровня идет загрузка начальных объектов, сначала во время лага грузятся жабы, потом сразу после лага точка рестарта, враги по очереди, и всё, поинтер не меняется пока в ходе уровня ему сам геймплей не прикажет. То есть при начале уровня он в течение нескольких кадров автоматически изменяется несколько раз подряд на длину дескриптора объектов (#$0B). 
 # Так как изначальное значение поинтера стало 0x00, то он переключается начиная с 0x0B (которое сразу же после обнуления вписывается, в ходе того же кадра, еще ДО ЛАГА) и далее по 0x16, 0x21, 0x2C и 0x37. 
 # Так уж сложилось, что в адреса $15 и $16 игра пишет значения джоев, чтобы регистрировать Tap'n'Hold. Субрутина перекидывает по 1 биту из соответствующего джоя в соответствующий адрес нулевой страницы посредством флага переноса и ROR/ROL, совершаемых по 8 раз. 
 # Много везения, и мы имеем поинтер указывающий игре на адрес $16 для чтения с него объектов, а в этом адресе у нас значение инпута 2 джоя, равное в данный кадр 0x7F. 
 # Игра начинает искать первый же пустой слот объекта. Первые 2 заняты жабами, третий занят байком, 4 свободен. В него и попадает ID=0x7F.

http://www.youtube.com/watch?v=bOweqz4cDlA