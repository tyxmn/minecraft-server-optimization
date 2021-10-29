> The translation may contain mistakes. Is the translation inaccurate? Write to me! - contact me in discord (Cubelius#0988).
![mso](https://user-images.githubusercontent.com/74359983/139340373-ced4a416-e216-452b-823d-1b260fa131ad.png)

Lags in Minecraft server, what to do? - Believe me, this is the most popular question that almost every newcomer to servers in this wonderful
game. Do not worry, because you have already taken the first step to solving this problem. Read the entire repository carefully and follow my recommendations step by step.

## Warning

This article is based on 1.17.1 with vanilla kernels. If you have mods, I don't think you have found a suitable guide. Also, please note
that the results of stability and correct operation of the server after optimization may vary from case to case. If you're sure that I made a mistake
or something is missing here - please open the problem in the Issues section.

## Start

### TPS
TPS is an abbreviation for Ticks per Second. The higher the value, the better the performance of the server. On average this value
19.8 to 20.0. You can type in `/tps` and look at the numbers. Are your TPS numbers below 19.5? The server is sluggish.

### Server.jar
The choice of server.jar (kernel) is a very important thing when building your server. The kernel has a direct influence on the performance of the server. At the moment there are several kernels that I recommend using, but there are also some that you should absolutely avoid.

I recommend:
- [Airplane](https://airplane.gg) - a stable and quite popular kernel, gaining momentum among servers. Supported by experienced developers, patches are made very quickly. Fork Paper.
- [Patina](https://github.com/PatinaMC/Patina) - a new, high-quality kernel. My tests lasted about 14 days and one conclusion can be made - this thing is very fast, but I don't have much confidence in this kernel as it is only being developed and has recently come to light.
- [Purpur](https://purpur.pl3x.net/downloads/) - the kernel is time tested. Good opinion from many server administrators, but it will eat more RAM than the above kernels.
- [Paper](https://papermc.io/) - a fork of Spigot. The most popular kernel in the world.

*For enthusiasts: SSSPigot. You can find more details on the Internet. It is the most productive kernel in the world, but it is paid.

Not recommended:
- [Yatopia](https://github.com/YatopiaMC/Yatopia) - [it's a complete failure in the whole history of kernels in Minecraft](https://github.com/KennyTV/list-of-shame). By the way, the core is no longer supported and has been abandoned.
- [Sugarcane](https://github.com/SugarcaneMC/Sugarcane) - Yatopia 2.0. Although it is under development, it contains Yatopia patches.
- [Bukkit/Spigot](https://getbukkit.org/) - these kernels are obsolete. They are strictly forbidden to use (unless you're a masochist, of course).
- Sponge (for mods and **sponge-plugins**) - in my personal opinion - complete crap. First of all there is no stability at all, and secondly there is a limitation in plugins: you can only put
Secondly, there is a limitation for plugins: only plugins for this kernel can be installed, although there is a Magma kernel that can support both plugins and mods at the same time.

*Please beware of other kernels! In 99.99% of cases these are scams. Your server and its data may be affected.

### Adding a garbage collector

A garbage collector is a must for every server, because Java really likes to eat RAM, but it cleans it badly. 

If you have regular hosting you should put ``-XX:+UseSerialGC`` at the startup prompt. According to my tests, this builder turns out to be better than the one used in [Aikar's flags](https://mcflags.emc.gs).
````yaml
java -Xmx2G -Xms16G -XX:+UseSerialGC -jar airplane.jar nogui 
````
If you have a VDS -
[this builder](https://github.com/hilltty/hilltty-flags) will really help you out! You should read the article before using it.
````yaml
java -jar -server -Xms6G -Xmx6G -XX:+UseLargePages -XX:LargePageSizeInBytes=2M -XX:+UnlockExperimentalVMOptions -XX:+UseShenandoahGC -XX:ShenandoahGCMode=iu -XX:+UseNUMA -XX:+AlwaysPreTouch -XX:-UseBiasedLocking -XX:+DisableExplicitGC -Dfile. encoding=UTF-8 airplane.jar --nogui
````

### Map pregen

Load the map with the [Chunky] plugin(https://www.spigotmc.org/resources/chunky.81534/). Stand at map zero coordinates and enter these commands alternately: `/chunky center`, `/chunky radius 6000`, `/chunky start`. Done! Now you have to wait a while for the plugin to load the 6000 blocks we set in the second command. It is desirable to limit your world to 6-10 thousand blocks. Believe me, this number of blocks will be enough for everyone to enjoy playing. If you need to increase the size of the map to higher values - instead of 6000 write your own number.

There is another plugin for map loading - [WorldBorder](https://www.spigotmc.org/resources/worldborder.60905/), if you need.

#### Plugins

Never install plugins that claim to optimize your server or plugins that change the world generation. ClearLagg and the like create **blinding lags**, and you can expect CPU load problems from EpicWorldGenerator and Iris. I won't even mention the paid React plugin because **it's just a shame**. You should measure this plugin's load in cores, not in percentages.

Links to plugins which really optimize server: [ServerBooster] (https://www.spigotmc.org/resources/%E2%9C%85must-have%E2%9C%85-serverbooster-%E2%9A%A1optimize-your-server-anti-lag-fps-boost-multilanguage%E2%9A%A1.72184/), [MFM] (https://www.spigotmc.org/resources/mob-farm-manager-supports-1-7-10-up-to-1-17-hopper-support.15127/).

Plugins that automatically save the world - demolish. Multiverse Core replace with Bungecord - a system that allows you to link multiple servers with each other. Also, download plugins **only from these sites**: [spigotmc.org](https://www.spigotmc.org/), [dev.bukkit.org](https://dev.bukkit.org/). Please don't look for resources elsewhere.

*And one more thing: I advise you not to clog your server with too many plugins. The more plugins, the greater the load on the server. Add as many plugins as your players will enjoy playing. Agree, when you see a text in the bossbar, scorboard, automatic messages in the chat, and even more inscriptions over the whole screen, the desire to leave the server increases to 100%, right? Administrative plugins, which are used once in a while - take down, various add-ons, which few people will use - take down, unnecessary plugins simply delete.*

## Configurations

There may be changes and additions in new versions of the article!

## [server.properties](https://minecraft.fandom.com/wiki/Server.properties)

**view-distance** - chunk loading distance. If you have a lot of players on the server and lags occur because of the chunks - lower this parameter to 4-5 chunks. 6 chunks is quite enough for vanilla survival.

````java
view-distance=6
````

### [bukkit.yml](https://bukkit.fandom.com/wiki/Bukkit.yml)
**spawn-limits** is a parameter that is responsible for changing the number of mobs per player. These limits only apply to animals or monsters in loaded chunks. If you don't need bats - set it to 0.

````yaml
monsters: 25, animals: 8, water-animals: 2, water-ambient: 1, ambient: 1
````

**period-in-ticks** - the less, the faster the server will unload empty chunks. If your server has more than 60 players, it is advisable to lower this parameter to 350.

````yaml
period-in-ticks: 400
````

**autosave** - If the server has an HDD drive, you will have to suffer lags due to automatic saving. You must have an SSD for the server to work properly. Raise the value to 12000 for a comfortable game. By the way, if you have a plugin for autosave world - remove it, use this parameter, it is no worse.

````yaml
autosave: 12000
````

### [spigot.yml](https://www.spigotmc.org/wiki/spigot-configuration/)
**save-user-cache-on-stop-only** - this parameter disables the permanent saving of user data. If your server crashes, user data will not be saved. It is advisable to restart your server every 48-72 hours to prevent losses. **Change this parameter at your own risk!

````yaml
save-user-cache-on-stop-only: true
````

**entity-activation-range** is a group of parameters that regulates how close animals and mobs must be to you to activate your AI. The numbers denote the distance in blocks. If you leave the "AI activation zone" - the mobs won't move. If you go back up, they'll turn on their AI. That's how it all works.

````yaml
animals: 16
monsters: 24
raiders: 48
misc: 8
````

**mob-spawn-range** - this parameter adjusts the spawn radius of mobs near you. The value should be one less than the number of chunks you set.

````yaml
mob-spawn-range: 5
````

### [paper.yml](https://gist.github.com/aikar/7e5978cfb22bb404f87a0dedac849358)

**max-auto-save-chunks-per-tick** - the parameter slows down the frequency of saving chunks. Don't set it lower than 12, otherwise some chunks might not be saved at all.

````yaml
max-auto-save-chunks-per-tick: 12
````

**mob-spawner-tick-rate** - ticks of the mob triggered by the spawner. **Do not raise the value higher.

````yaml
mob-spawner-tick-rate: 2
````

**prevent-moving-into-unloaded-chunks** - if the player somehow got into an unloaded chunk - he will constantly fall down (into the void), and when the server loads the chunks, it can play a cruel joke with him by not teleporting the player back. The player can simply die in the void. To prevent this from happening, you need to turn this option on.

````yaml
prevent-moving-into-unloaded-chunks: true
````

**armor-stands-tick** - by disabling this parameter the server will not check armor stands.

````yaml
armor-stands-tick: false
````

## Conclusion

After you have done everything that was written in this article - check the stability and performance of the server. Is it freezing? To do this you will need to write these commands: `/mspt`, `/tps`. If after starting the server passed 5-10 minutes and the maximum number in mspt does not exceed 150.0, and TPS varies around 19.8-20.0 - great, you optimized your server. Congratulations!

#### The server keeps lagging. What to do?

Chances are you either did something wrong or you missed some point in the article. If the server is still lagging even after optimization, it's time to think about money, because you need to buy more power. Check out another one of my articles: https://github.com/cubelius/minecraft-server-create. Maybe you have 1 core and 30 players online? :D

![1](https://user-images.githubusercontent.com/74359983/139352191-22411c4e-5aa1-4aaa-85a9-e73a32788ad9.png)
