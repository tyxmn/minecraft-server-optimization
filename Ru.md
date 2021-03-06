![mso](https://user-images.githubusercontent.com/74359983/139340373-ced4a416-e216-452b-823d-1b260fa131ad.png)

Лаги в майнкрафт сервере, что делать? — поверьте, это самый популярный вопрос, который возникает практически у каждого новичка в сфере серверов в этой замечательной
игре. Не переживайте, так как вы уже сделали первый шаг к решению данной проблемы. Читайте весь репозиторий внимательно и выполняйте мои рекомендации постепенно.

## Предупреждение

Эта статья основана на версии 1.17.1 с ванильными ядрами. Если у вас моды — я не думаю, что вы нашли подходящее руководство. Также, обратите внимание на
то, что результаты стабильности и корректной работоспособности сервера после оптимизации может отличатся в разных случаях. Если вы уверены, что я допустил ошибку
или тут чего-то нехватает - пожалуйста, откройте проблему в разделе Issues.

## Начало

### TPS
TPS — сокращение от Ticks per Second — это число тактов за секунду. Чем выше данный показатель, тем большая производительность сервера. В среднем это значение
варьируется от 19.8 до 20.0. Вы можете прописать ```/tps``` и посмотреть на цифры. У вас ниже 19.5 TPS? Сервер подлагивает.

### Server.jar
Выбор ядра — очень важная вещь при сборке вашего сервера. Ядро напрямую влиет на производительность сервера. На данный момент существуют несколько ядер, которые я рекомендую использовать, но есть и те, от которых вам категорически нужно отказаться.

Рекомендую:
- [Airplane](https://airplane.gg) — стабильное и довольно популярное ядро, набирающее обороты среди серверов. Поддерживается опытными разработчиками, патчи делают очень быстро. Форк Paper.
- [Patina](https://github.com/PatinaMC/Patina) — новое, качественное ядро. Мои тесты длились около 14 дней и можно сделать один вывод - эта штука очень быстрая, но у меня нет особого доверия к этому ядру, так как оно только разрабатывается и недавно появилось на свет.
- [Purpur](https://purpur.pl3x.net/downloads/) — ядро проверено временем. Хорошее мнение со стороны многих администраторов серверов, но оперативной памяти будет кушать больше, чем вышеперечисленные ядра.
- [Paper](https://papermc.io/) — форк Spigot. Самое популярное ядро в мире.

*Для энтузиастов: SSSPigot. Подробности вы можете узнать в интернете. Это самое производительное ядро в мире, но платное.*

Нерекомендую:
- [Yatopia](https://github.com/YatopiaMC/Yatopia) — [это полный провал во всей истории ядер в Minecraft](https://github.com/KennyTV/list-of-shame). Кстати, ядро больше не поддерживается и было заброшено.
- [Sugarcane](https://github.com/SugarcaneMC/Sugarcane) — Yatopia 2.0. Хоть оно и разрабатывается, но соддержит патчи от Yatopia.
- [Bukkit/Spigot](https://getbukkit.org/) — эти ядра морально устарели. Их использовать категорически запрещено (если вы не мазохист, конечно же).
- Sponge (для модов и **sponge-плагинов**) — лично моё мнение — полное дерьмо. Во-первых стабильности никакой нет, а во-вторых ограничение в плагинах: можно ставить
только плагины для этого ядра, хотя есть ядро Magma, которое может поддерживать и плагины и моды одновременно.
- Mohist - крайне нестабильное ядро (ещё и [опасное](https://essentialsx.net/do-not-use-mohist.html)).

*Пожалуйста, остерегайтесь других ядер! В 99.99% случаев это скам. Ваш сервер и его данные могут пострадать.*

### Добавление сборщика мусора

Сборщик мусора обязательно должен стоять в каждом сервере, так как Java очень любит кушать оперативную память, но очищает её плохо. 

Если у вас обычный хостинг, вам нужно вставить ```-XX:+UseSerialGC``` в строку запуска. По моим тестам, этот сборщик оказывается лучше, чем тот, который применён в [флагах Aikar'а](https://mcflags.emc.gs).
````yaml
java -Xmx2G -Xms16G -XX:+UseSerialGC -jar airplane.jar nogui 
````
Если у вас VDS -
[этот сборщик](https://github.com/hilltty/hilltty-flags) вас нереально выручит! Перед использованием нужно прочитать статью.
````yaml
java -jar -server -Xms6G -Xmx6G -XX:+UseLargePages -XX:LargePageSizeInBytes=2M -XX:+UnlockExperimentalVMOptions -XX:+UseShenandoahGC -XX:ShenandoahGCMode=iu -XX:+UseNUMA -XX:+AlwaysPreTouch -XX:-UseBiasedLocking -XX:+DisableExplicitGC -Dfile.encoding=UTF-8 airplane.jar --nogui
````

### Прогрузка карты

Прогрузите карту с помощью плагина [Chunky](https://www.spigotmc.org/resources/chunky.81534/). Станьте на нулевые координаты карты и введите эти команды поочерёдно: `/chunky center`, `/chunky radius 6000`, `/chunky start`. Готово! Теперь вам нужно подождать некоторое время, пока плагин прогрузит 6000 блоков, которые мы задали во второй команде. Желательно ограничить свой мир до 6-10 тыс. блоков. Поверьте, такого количества блоков будет вполне достаточно, чтобы всем было приятно играть. Если нужно увеличить размер карты до более высоких значений — вместо 6000 напишите своё число.

Есть и другой плагин для прогрузки карты — [WorldBorder](https://www.spigotmc.org/resources/worldborder.60905/), если вам надо.

### Плагины

Никогда не ставьте плагины, которые заявляют, что они оптимизируют ваш сервер или плагины, которые изменяют генерацию мира. ClearLagg и ему подобные создают **вопиющие лаги**, а от EpicWorldGenerator и Iris можно ожидать проблем с нагрузкой процессора. Про платный React даже упоминать не буду, потому что **это просто позор**. Измерять нагрузку этого плагина нужно не в процентах, а в ядрах.

Ссылки на плагины, которые действительно оптимизируют сервер: [ServerBooster](https://www.spigotmc.org/resources/%E2%9C%85must-have%E2%9C%85-serverbooster-%E2%9A%A1optimize-your-server-anti-lag-fps-boost-multilanguage%E2%9A%A1.72184/), [MFM](https://www.spigotmc.org/resources/mob-farm-manager-supports-1-7-10-up-to-1-17-hopper-support.15127/).

Плагины, автоматически сохраняющие мир — сносите. Multiverse Core замените на Bungecord — систему, которая позволяет связывать несколько серверов между собой. Скачивать плагины можно **только с этих сайтов**: [spigotmc.org](https://www.spigotmc.org/), [dev.bukkit.org](https://dev.bukkit.org/). Также, можете рассмотреть [Songoda](https://songoda.com/) и [MC-Market](https://www.mc-market.org/). Не ищите ресурсы в других местах.

*Советую не засорять свой сервер изрядным количеством плагинов. Чем больше плагинов, тем больше нагрузка на сервер. Добавьте столько плагинов, чтобы вашим игрокам было приятно играть. Администрационные плагины, которые используются невероятно редко — можно снести. Различные дополнения, которыми мало кто будет пользоваться — снести. Мусорные плагины только ухудшают ваш сервер.*

## Конфигурации

### [server.properties](https://minecraft.fandom.com/wiki/Server.properties)

**view-distance** - дистанция прогрузки чанков. Если на сервере много игроков и лаги происходят из-за чанков - снижайте этот параметр до 4-5 чанков. 6 чанков вполне достаточно для ванильного выживания.

````java
view-distance=6
````

### [bukkit.yml](https://bukkit.fandom.com/wiki/Bukkit.yml)
**spawn-limits** - параметр, который отвечает за изменение количества мобов на одного игрока. Эти ограничения применяются только к животным или монстрам в загруженных чанках.

````yaml
monsters: 30
animals: 6
water-animals: 2
water-ambient: 2
water-underground-creature: 2
ambient: 1
````

**period-in-ticks** - чем меньше, тем быстрее сервер будет выгружать пустые чанки. Если на вашем сервере играет больше 60 человек, желательно опустить этот параметр до 350.

````yaml
period-in-ticks: 400
````

**autosave** - если у сервера стоит HDD накопитель, вам придётся страдать от лагов из-за автоматического сохранения. Вы должны иметь SSD накопитель для нормальной работы сервера. Поднимите значение до 12000 для комфортной игры. Кстати, если у вас стоит плагин на автосохранение мира - удалите его, используйте этот параметр, он ничем не хуже.

````yaml
autosave: 12000
````

### [spigot.yml](https://www.spigotmc.org/wiki/spigot-configuration/)
**save-user-cache-on-stop-only** - этот параметр отключает постоянное сохранение пользовательских данных. Если ваш сервер аварийно выключиться, пользовательские данные не будут сохранены. Желательно перезагружать свой сервер раз в 48-72 часа, чтобы предотвратить потери. **Изменяйте этот параметр на свой страх и риск!**

````yaml
save-user-cache-on-stop-only: true
````

**entity-activation-range** - это группа параметров, которая регулирует, насколько близко животные и мобы должны находиться к вам, чтобы активировать свой ИИ. Числа обозначают расстояние в блоках. Если вы выйдите из "зоны активации ИИ" - мобы не будут двигаться, подойдёте обратно - включат свой ИИ. Вот так это всё и работает.

````yaml
animals: 16
monsters: 24
raiders: 48
misc: 8
````

**mob-spawn-range** - этот параметр регулирует радиус спавна мобов возле вас. Значение должно быть на единицу меньше от кол-ва чанков, которое вы выставили.

````yaml
mob-spawn-range: 5
````

### [paper.yml](https://gist.github.com/aikar/7e5978cfb22bb404f87a0dedac849358)

**max-auto-save-chunks-per-tick** - параметр замедляет частоту сохранения чанков. Не опускайте значение ниже 12, иначе некоторые чанки могут не сохраниться вообще.

````yaml
max-auto-save-chunks-per-tick: 12
````

**mob-spawner-tick-rate** - тики моба, вызванного спавнером. **Не поднимайте значение выше.**

````yaml
mob-spawner-tick-rate: 2
````

**prevent-moving-into-unloaded-chunks** - если игрок каким-то образом попал в незагруженный чанк - он постоянно будет проваливаться вниз (в пустоту), а когда сервер прогрузит чанки, он может с ним сыграть в злую шутку, не телепортировав игрока обратно. Игрок может просто умереть в пустоте. Чтобы такого не произошло, нужно включить данный параметр.

````yaml
prevent-moving-into-unloaded-chunks: true
````

**armor-stands-tick** - выключив данный параметр, сервер не будет проверять стенды для брони.

````yaml
armor-stands-tick: false
````

## Заключение

После того, как вы проделали всё, что было написано в данной статье — проверьте стабильность и производительность сервера. Не лагает ли он? Для этого вам необходимо прописать эти команды: `/mspt`, `/tps`. Если после запуска сервера прошло 5-10 минут и максимальная цифра в mspt не превышает 150.0, а TPS варьируется в районе 19.8-20.0 — отлично, вы оптимизировали свой сервер. Поздравляю!

### Сервер продолжает лагать. Что делать?

Скорее всего, вы либо что-то неправильно сделали, либо пропустили какой-то пункт из статьи. Если сервер продолжает лагать даже после оптимизации — время задуматься о деньгах, ибо вам нужно покупать больше мощностей. Посмотрите ещё одну мою статью: https://github.com/cubelius/minecraft-server-create. Может, у вас 1 ядро и 30 игроков онлайна? :D

![1](https://user-images.githubusercontent.com/74359983/139352191-22411c4e-5aa1-4aaa-85a9-e73a32788ad9.png)




