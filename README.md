# Инструкция по оптимизации minecraft сервера
24.06.21, релиз: 1.0. Здесь могут быть ошибки. Если нашли - обратитесь ко мне в discord: cubelius#0988. За остальной помощью можете тоже обращаться ко мне, если что, могу помочь :)

Эта инструкция поможет максимально оптимизировать minecraft сервер и устранить лаги. После того как вы прочитаете всё до конца и сделаете всё то, что было рекомендовано мною - ваш сервер в 99% случаев будет работать намного лучше и производительнее.

## TPS 

TPS это Ticks per Second, количество тактов в секунду. Чем больше TPS - тем лучше. Если идёт большая нагрузка, консоль выведет такое сообщение: Can't keep up! Is the server overloaded?.. Это первый звоночек, что ваш сервер нуждается в оптимизации/повышении мощности. Причины могут быть разными, начиная от скачивания "якобы оптимизирующих" плагинов, заканчивая действиями игроков.

Нормальные показатели это 19.8-20.0 TPS, на этой отметке держаться большинство серверов. Чтобы посмотреть TPS, нужно написать команду: **/tps**.

## Тайминги
Если у вас низкий TPS, необходимо написать такие команды: **/timings on**, ждём 2-3 часа, **/timings paste**. После этого вы получите ссылку и попадёте на сайт, где сможете посмотреть, что нагружает сервер. Пролистав чуть ниже, вы увидите таблицу, где сможете определить, из-за чего опускается TPS. Если самому ничего не понятно и причины лагов не удаётся определить - напишите в какой-нибудь форум, вам обязательно помогут. Как по мне, лучше, чем minecraft-inside форума нет, так что вы смело можете рассказать о своей проблеме там. Кстати, на картинке ниже сервер страдает из-за лагов от большого кол-ва мобов.

![Screenshot_296](https://user-images.githubusercontent.com/74359983/123190649-9e475000-d4a8-11eb-9504-26e5ddb77af3.png)

## Оперативная память, флаги

Для комфортной игры в 40 человек, вам понадобится 6 Гб ОЗУ. Прибавляйте приблизительно 60 Мб на одного игрока. Также, вам нужно постравить hilltty-flags при запуске сервера. Нажмите [сюда](https://github.com/hilltty/hilltty-flags/blob/main/russian-lang.md) для просмотра флагов. Это сборщик мусора, построенный на алгоритме Shenandoah. Этот алгоритм намного лучше, чем тот, который применяется в флагах Айкара.

Рекомендуемое количество игроков и плагинов на определённое количество Гб ОЗУ и количества ядер. 

**Не рекомендую** использовать сервер, у которого меньше 4-ёх Гб ОЗУ. Для адекватной работы 1.17 нужно как минимум 2 ГБ ОЗУ (с нулевым онлайном).

```
04 Гб ОЗУ, 2 ядра: до 25 игроков, 20 плагинов.
06 Гб ОЗУ, 3 ядра: до 40 игроков, 30 плагинов.
08 Гб ОЗУ, 4 ядра: до 60 игроков, 45 плагинов.
12 Гб ОЗУ, 5 ядер: до 80 игроков, 50 плагинов.
```

## Плагины

Никогда не ставьте плагины, которые заявляют, что они оптимизируют ваш сервер или плагины, которые изменяют генерацию мира. ClearLagg и ему подобные создают вопиющие лаги, а от EpicWorldGenerator можно ожидать проблем с нагрузкой CPU. Про платный React даже упоминать не буду, это просто позор. Измерять нагрузку этого плагина нужно не в процентах, а в ядрах.

Ссылки на плагины, которые действительно оптимизируют сервер: [ServerBooster](https://www.spigotmc.org/resources/%E2%9C%85must-have%E2%9C%85-serverbooster-%E2%9A%A1optimize-your-server-anti-lag-fps-boost-multilanguage%E2%9A%A1.72184/), [Chunky (прогрузка карты)](https://www.spigotmc.org/resources/chunky.81534/), [MFM](https://www.spigotmc.org/resources/mob-farm-manager-supports-1-7-10-up-to-1-17-hopper-support.15127/).

Плагины, автоматически сохраняющие мир - сносите. Multiverse Core, и не дай Бог MultiWorld ставьте только в том случае, если вы уверены, что вам действительно нужно несколько миров. Каждый мир потребляет ~100 МБ ОЗУ при нулевом онлайне. Замените этот плагин на Bungecord - систему, которая позволяет связывать несколько серверов между собой. Все сервера, которым нужно несколько миров уже давным-давно используют эту систему.

Касаемо CoreProtect - ставьте на своё усмотрение, но учтите, что даже с оптимизируемым конфигом с онлайном 100+ человек за месяц база данных будет забита на 70-100 ГБ. Вам действительно это нужно? Подумайте сами. Кстати, иногда бывает такое, что у этого плагина ложиться база данных, если это произойдёт, вы будете наслаждаться 0.60 TPS. 

Также, скачивать плагины можно только с этих сайтов: [spigotmc.org](https://www.spigotmc.org/), [dev.bukkit.org](https://dev.bukkit.org/). Попали на BlackSpigot? Срочно выходите с этого проклятого места. Ничего хорошего оттуда вы точно не скачаете.

![Screenshot_351](https://user-images.githubusercontent.com/74359983/123166286-eac96600-d47d-11eb-99a3-0ee7f00e96f2.png)

Касаемо сборок серверов - к ним я отношусь негативно. Лучше не поленитесь и создайте собственную сборку, потому что в ней вы будете разбираться намного лучше, чем в той, который собрал кто-то другой. В сборках частенько присутствуют вирусы. Чтобы посмотреть, есть ли вирусы в вашей сборке, скачайте [это ядро, которое нужно закинуть в папку plugins](https://www.spigotmc.org/resources/spigot-anti-malware-detects-over-300-malicious-plugins.64982/). Он распознаёт вирусы во всех .jar файлах. 

Советую не засорять свой сервер изрядным количеством плагинов. Чем больше плагинов - тем больше нагрузка на сервер. Добавьте столько плагинов, чтобы вашим игрокам было приятно играть на сервере. Согласитесь, когда вы видите перед собою текст в боссбаре, скорборде, в автоматических сообщениях в чате, а уж тем более надписи на весь экран, желание уйти с этого говна возрастает до 100%. Поверьте, если вы уберёте всю ненужную для обычного игрока информацию, ему будет намного приятнее играть. Администрационные плагины, которые используются раз в никогда - снести, различные дополнения, которыми мало кто будет пользоваться - снести, ненужные плагины просто удаляйте.

## Ядро

Самые популярные форки, которыми можно пользоваться на данный момент: [Paper](https://papermc.io/downloads#Paper-1.17), [Purpur](https://purpur.pl3x.net/downloads/#1.17), [Tuinity](https://ci.codemc.io/job/Spottedleaf/job/Tuinity/), [Airplane](https://github.com/TECHNOVE/Airplane). Я не рекомендую использовать Bukkit и Spigot, так как это пережитки прошлого, которые имеют много проблем. В Paper исправлено много багов и сделано много патчей, с производительностью всё прекрасно. 

## Оптимизированные конфиги

### server.properties

**view-distance** - дистанция прогрузки чанков. Если на сервере много игроков и лаги происходят из-за чанков - снижайте этот параметр до 4-5 чанков. 6 чанков вполне достаточно для ванильного выживания.

````java
view-distance: 6
````

**network-compression-threshold** - этот параметр отвечает за ограничение размера пакета.

````java
network-compression-threshold: 512
````

### bukkit.yml
**spawn-limits** - параметр, который отвечает за изменение количества мобов на одного игрока. Эти ограничения применяются только к животным или монстрам в загруженных чанках. Если вам не нужны летучие мыши - ambient ставьте на 0.

````java
monsters: 30, animals: 10, water-animals: 3, water-ambient: 1, ambient: 1
````

**period-in-ticks** - чем меньше, тем быстрее сервер будет выгружать пустые чанки. Если на вашем сервере играет больше 60 человек, желательно опустить этот параметр до 350.

````java
period-in-ticks: 450
````

**autosave** - если у сервера стоит HDD накопитель, вам придётся страдать от лагов из-за автоматического сохранения. Вы должны иметь SSD накопитель для нормальной работы сервера. Поднимите значение до 12000 для комфортной игры. Кстати, если у вас стоит плагин на автосохранение мира - удалите его, используйте этот параметр, он ничем не хуже.

````java
autosave: 12000
````

### spigot.yml
**save-user-cache-on-stop-only** - этот параметр отключает постоянное сохранение пользовательских данных. Если ваш сервер аварийно выключиться, пользовательские данные не будут сохранены. Желательно перезагружать свой сервер раз в 48-72 часа, чтобы предотвратить потери. Изменяйте этот параметр на свой страх и риск!

````java
save-user-cache-on-stop-only: true
````

**entity-activation-range** - это группа параметров, которая регулирует, насколько близко животные и мобы должны находиться к вам, чтобы активировать свой ИИ. Числа обозначают расстояние в блоках. Если вы выйдите из "зоны активации ИИ" - мобы не будут двигаться, подойдёте обратно - включат свой ИИ. Вот так это всё и работает.

````java
animals: 16
monsters: 24
raiders: 48
misc: 8
````

**merge-radius** - радиус слияния блоков и опыта в кучку. Не повышайте рекомендуемые параметры. Вы же не хотите, чтобы ваши игроки сделали вашу личку вот [такой](https://www.youtube.com/watch?v=zGl796352RI), когда они обнаружат, что их драгоценные алмазы сгорели в лаве?

````java
item: 4.0
exp: 6.0
````

**max-tick-time** - не используйте этот параметр. Значение 1000 отключает его.

````java
max-tick-time: 1000
````

**mob-spawn-range** - этот параметр регулирует радиус спавна мобов возле вас.

````java
mob-spawn-range: 6
````

**arrow-despawn-rate** - стрелы, выпущенные игроками, будут удаляться быстрее, если вы поставите рекомендуемое значение - 300 (15 секунд).

````java
arrow-despawn-rate: 300
````

### Paper.yml

**max-auto-save-chunks-per-tick** - параметр замедляет частоту сохранения чанков. Не опускайте значение ниже 12, иначе некоторые чанки могут не сохраниться вообще. У вас играют меньше 20 игроков? Ставьте 8. Это предел.

````java
max-auto-save-chunks-per-tick: 12
````

**mob-spawner-tick-rate** - тики моба-спавнера. Не поднимайте значение выше.

````java
mob-spawner-tick-rate: 2
````

**disable-chest-cat-protections** - даже котейки вредят серверу, падлы :3 Этот параметр необходимо отключить, потому что по умолчанию сервер постоянно проверяет сундуки, чтобы увидеть, сидит ли на нём котейка.

````java
disable-chest-cat-protections: true
````

**prevent-moving-into-unloaded-chunks** - если игрок каким-то образом попал в незагруженный чанк - он постоянно будет проваливаться вниз (в пустоту), а когда сервер прогрузит чанки, он может с ним сыграть в злую шутку, не телепортировав игрока обратно. Игрок может просто умереть в пустоте. Чтобы такого не произошло, нужно включить данный параметр.

````java
prevent-moving-into-unloaded-chunks: true
````

**armor-stands-tick** - выключив данный параметр, сервер не будет проверять стенды для брони.

````java
armor-stands-tick: false
````

## Прогрузка карты

Чтобы не засорять свой диск слишком быстро, вы можете прогрузить свою карту с помощью плагина [Chunky](https://www.spigotmc.org/resources/chunky.81534/). Он абсолютно бесплатный. После того как вы добавите плагин в папку plugins, перезагрузите сервер и объявите технические работы на несколько часов своим игрокам. Станьте на нулевые координаты карты и введите эти команды поочерёдно: **/chunky center**, **/chunky radius 6000**, **/chunky start**. Готово! Теперь вам нужно подождать от одного до 8-и часов, пока плагин прогрузит 6000 блоков, которые мы задали во второй команде. Желательно ограничить свой мир до 6000 блоков. Поверьте, такого количества блоков будет вполне достаточно, чтобы всем было приятно играть. Если всё же нужно увеличить размер карты до более высоких значений - вместо 6000 напишите своё число.

После прогрузки карты нужно перезапустить сервер. Нагрузка на процессор снизится, а потребление ОЗУ от карты теперь полностью исчезло! Как же круто, когда столь большие проблемы решаются так просто, не правда ли?

## Античит

Практически каждый плагин-античит убогий и потребляет слишком много ресурсов, но [Vulkan](https://www.spigotmc.org/resources/vulcan-advanced-cheat-detection-1-7-1-16-5.83626/) совсем не такой. Это лучший античит по моему мнению, который производительный, да и к тому же очень мощный!

![Screenshot_352](https://user-images.githubusercontent.com/74359983/123166626-4ac00c80-d47e-11eb-8fe5-8637209ad668.png)

## Датапаки

Датапаки связанные с мобами/генерацией лучше не использовать, потому что они плохо влияют на производительность. Датапаки лучше заменить **плагинами**.

## Моды

Любой minecraft мод любит много жрать. Если у вас несколько простеньких модов - лагать не будет, 6 Гб ОЗУ и 3 ядра для 15-20 человек будет вполне достаточно, но если это большие сборки модификаций или несколько масштабных модов, вам придётся покупать мощный сервер. Кстати, для модов нужно скачивать совершенно другие ядра.










