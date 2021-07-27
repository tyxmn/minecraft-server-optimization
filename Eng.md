> The translation may contain mistakes. Is the translation inaccurate? Write to me! - contact me in discord (Cubelius#0988).
## Instruction for minecraft server optimization

This tutorial will help you maximally optimize minecraft server and eliminate lag. After you read all the way through and do all that was recommended by me - your server in 99% of cases will run much better and more efficiently.

## How to find a problem

Normal TPS is 19.8-20.0 which is where most servers should be. If you notice that things start to slow down, type `/tps` and check if the server is really lagging. Also, the console may give a warning: Can't keep up! Is the server overloaded? If this happens, don't wait, just go straight to the action.

## Timings

If you have a low TPS, you can write the following commands: `/timings on`, wait a few hours, `/timings paste`. After that you will get a link and go to a site where you can see what is stressing the server. If you swipe a little lower, you will see a table where you can determine what is causing the TPS to drop. If you do not understand yourself and the cause of lag can not determine - write to any forum, you will help.

## RAM

For a comfortable game with 40 players, you need 6 GB. I recommend putting [Aikars flags](https://aikar.co/2018/07/02/tuning-the-jvm-g1gc-garbage-collector-flags-for-minecraft/), which reduce RAM consumption. In addition to these flags, you need to put [this plugin](https://www.spigotmc.org/resources/garbage-collector.26902/).

```
04 GB RAM, 2 cores: up to 25 players, 20 plugins.
06 GB RAM, 3 cores: up to 40 players, 30 plugins.
08 GB RAM, 4 cores: up to 60 players, 45 plugins.
12 GB RAM, 5 cores: up to 80 players, 50 plugins.
```

## Plugins

Never install plugins that claim to optimize your server or plugins that change the world generation. ClearLagg and the like create blatant lags, and you can expect CPU load problems from EpicWorldGenerator. I won't even mention the paid React, it's just a shame. The load of this plugin should be measured in cores, not in percentages. Also, you should be wary of LockLogin, CoreProtect, high values of placeholders updates (put them on 60-100 ticks), several plugins per chat.

Links to plugins that really optimize the server: [ServerBooster](https://www.spigotmc.org/resources/%E2%9C%85must-have%E2%9C%85-serverbooster-%E2%9A%A1optimize-your-server-anti-lag-fps-boost-multilanguage%E2%9A%A1.72184/), [Chunky (map pregen)](https://www.spigotmc.org/resources/chunky.81534/), [MFM](https://www.spigotmc.org/resources/mob-farm-manager-supports-1-7-10-up-to-1-17-hopper-support.15127/).

Plugins that automatically save the world - demolish. Multiverse Core replace with Bungecord - a system that allows you to link multiple servers with each other. Also, you can only download plugins from these sites: [spigotmc.org](https://www.spigotmc.org/), [dev.bukkit.org](https://dev.bukkit.org/). Got caught on BlackSpigot? Get out of that cursed place immediately. You will definitely not download anything good from there.

![Screenshot_351](https://user-images.githubusercontent.com/74359983/123166286-eac96600-d47d-11eb-99a3-0ee7f00e96f2.png)

Regarding server builds - I have a negative attitude towards them. Better not be lazy and create your own compilation, because in it you will understand much better than the one who collected someone else. There are often viruses in compilations. To see if your build has viruses, [download this kernel and put it in the plugins folder](https://www.spigotmc.org/resources/spigot-anti-malware-detects-over-300-malicious-plugins.64982/). It detects viruses in all .jar files.

I advise you not to clog your server with too many plugins. The more plugins, the greater the load on the server. Add as many plugins, so that your players was pleasant to play on the server. Agree, when you see the text in front of you in the bossbar, scorboard, in automatic messages in chat, and even more inscriptions over the entire screen, the desire to leave this shit goes up to 100%. Believe me, if you remove all unnecessary information for the average player, he will be much more pleasant to play. Administrative plugins that are used once in a while - take down, various add-ons, which few people will use - take down, unnecessary plugins just delete.

## Server.jar

I recommend using [Airplane](https://github.com/TECHNOVE/Airplane) for 1.16-1.17.x. For 1.12 and below - Spigot. **Do not use** [Bukkit](https://getbukkit.org/), [Spigot](https://getbukkit.org/), [Paper](https://papermc.io/downloads), [Yatopia](https://github.com/YatopiaMC) & [Sugarcane](https://github.com/SugarcaneMC/Sugarcane). Tuinity and Purpur aren't bad either, you can use those .jars.

## Configs

### server.properties

**view-distance** - chunk loading distance. If the server has a lot of players and lags occur because of the chunks - reduce this parameter to 4-5 chunks. 6 chunks is enough for vanilla survival.

````java
view-distance=6
````

### bukkit.yml
**spawn-limits** - parameter, which is responsible for changing the number of mobs per player. These limits apply only to animals or monsters in loaded chunks. If you don't want bats, set it to 0.

````yaml
monsters: 25, animals: 8, water-animals: 2, water-ambient: 1, ambient: 1
````

**period-in-ticks** - the smaller, the faster the server will unload the empty chunks. If your server is played by more than 60 people, it is advisable to lower this parameter to 350.

````yaml
period-in-ticks: 400
````

**autosave** - if the server has an HDD drive, you will have to suffer from lags due to automatic saving. You must have an SSD in order for your server to work properly. Raise it to 12000 to play the game comfortably. By the way, if you have autosave plugin - remove it, use this parameter, it is no worse.

````yaml
autosave: 12000
````

### spigot.yml
**save-user-cache-on-stop-only** - this parameter disables permanent saving of user data. If your server crashes, user data will not be saved. It is advisable to restart your server every 48-72 hours to prevent losses. **Change this parameter at your own risk!**

````yaml
save-user-cache-on-stop-only: true
````

**entity-activation-range** - is a group of parameters that regulates how close animals and mobs must be to you to activate your AI. The numbers denote the distance in blocks. If you leave the "AI activation zone" - the mobs won't move. If you go back up, they'll turn on their AI. That's how it all works.

````yaml
animals: 16
monsters: 24
raiders: 48
misc: 8
````

**mob-spawn-range** - this parameter adjusts the spawn radius of the mobs near you. The value should be one less than the number of chunks you set.

````yaml
mob-spawn-range: 5
````

### paper.yml

**max-auto-save-chunks-per-tick** - the parameter slows down the frequency of saving chunks. Don't set it lower than 12, otherwise some chunks might not be saved at all.

````yaml
max-auto-save-chunks-per-tick: 12
````

**mob-spawner-tick-rate** - the ticks of the mob triggered by the spawner. **Don't set it any higher.**

````yaml
mob-spawner-tick-rate: 2
````

**prevent-moving-into-unloaded-chunks** - if the player somehow got into an unloaded chunk - he will constantly fall down (into the void), and when the server loads the chunks, it can play a cruel joke with him, not teleporting the player back. The player can simply die in the void. You can enable this option to prevent this from happening.

````yaml
prevent-moving-into-unloaded-chunks: true
````

**armor-stands-tick** - by turning off this parameter, the server will not check the armor stands.

````yaml
armor-stands-tick: false
````

## Map pregen

To avoid clogging up your disk too quickly, you can load your map with the [Chunky](https://www.spigotmc.org/resources/chunky.81534/) plugin. It's completely free. After you add the plugin to your plugins folder, restart your server and announce technical work for a few hours to your players. Stand at map zero coordinates and enter these commands in turn: `/chunky center`, `/chunky radius 6000`, `/chunky start`. Done! Now you need to wait from one to 8 hours for the plugin to load 6000 blocks, which we set in the second command. It is desirable to limit your world to 6000 blocks. Believe me, this number of blocks will be enough for everyone to enjoy playing. If you still need to increase the size of the map to higher values - instead of 6000 write your number.

After loading the map you need to restart the server. CPU load will be reduced, and the consumption of RAM from the map is now completely gone.

## Anticheat

Almost every anticheat plugin is cheesy and consumes too many resources, but [Vulkan](https://www.spigotmc.org/resources/vulcan-advanced-cheat-detection-1-7-1-16-5.83626/) is not like that. This is the best anticheat in my opinion, productive and powerful, which makes "bugs" **very rarely.**
