> The translation may contain mistakes. Is the translation inaccurate? Write to me! - contact me in discord (Cubelius#0988).
# Instructions for minecraft server optimization

This tutorial will help you optimize your minecraft server and eliminate lags as much as possible. After you read all the way to the end and do all that was recommended by me - your server in 99% of cases will work much better and more productive.

#### How to find the problem
A normal TPS is 19.8-20.0. This is the position most Minecraft servers stick to. If you notice things starting to slow down and your players start complaining about problems, type ``/tps`` and see if the server is really lagging. Also, the console may show a warning: Can't keep up! Is the server overloaded? If this happens, take action right away.

### Timings
If you have a low TPS, write the following commands: ``/timings on``, wait a few hours, ``/timings paste``. After that you will get a link and get to a site where you can see what is stressing the server. If you scroll a little further down, you will see a table where you can determine what is causing the TPS to drop. If you yourself do not understand anything and can not determine the cause of the lag - write to some forum, you will definitely help.

### RAM and CPU usage

You have clogged RAM, and the processor is loaded under 80+% at low load? You need to increase the capacity of your server, because the lack of cores or GB of RAM is what's causing you problems.

### Plugins

Never install plugins that claim to optimize your server or plugins that change the way the world is generated. ClearLagg and the like create blatant lags, and you can expect CPU load problems from EpicWorldGenerator. I won't even mention the paid React, it's just a shame. The load of this plugin should be measured in cores, not in percentages. Also, you should be wary of LockLogin, CoreProtect, high values of playholder updates (put them on 60-100 ticks), several plugins per chat.

Links to plugins that really optimize the server: [ServerBooster](https://www.spigotmc.org/resources/%E2%9C%85must-have%E2%9C%85-serverbooster-%E2%9A%A1optimize-your-server-anti-lag-fps-boost-multilanguage%E2%9A%A1.72184/), [Chunky (map loading)](https://www.spigotmc.org/resources/chunky.81534/), [MFM](https://www.spigotmc.org/resources/mob-farm-manager-supports-1-7-10-up-to-1-17-hopper-support.15127/).

Plugins that automatically save the world - demolish. Multiverse Core replace with Bungecord - a system that allows you to link multiple servers with each other. Also, you can only download plugins from these sites: [spigotmc.org](https://www.spigotmc.org/), [dev.bukkit.org](https://dev.bukkit.org/). Got caught on BlackSpigot? Get out of that cursed place right away. You won't be able to download anything good from there.

![Screenshot_351](https://user-images.githubusercontent.com/74359983/123166286-eac96600-d47d-11eb-99a3-0ee7f00e96f2.png)

Regarding server builds - I have a negative attitude towards them. Better not be lazy and create your own compilation, because in it you will understand much better than the one who built someone else. There are often viruses in compilations. To see if your build has viruses, download [this is the kernel you put in the plugins folder] (https://www.spigotmc.org/resources/spigot-anti-malware-detects-over-300-malicious-plugins.64982/). It detects viruses in all .jar files. 

I advise you not to clog your server with too many plugins. The more plugins - the greater the load on the server. Add as many plugins, so that your players was pleasant to play on the server. Agree, when you see the text in front of you in the bossbar, scorboard, in automatic messages in chat, and even more inscriptions over the entire screen, the desire to leave this shit goes up to 100%. Believe me, if you remove all unnecessary information for the average player, he will be much more pleasant to play. Administrative plugins that are used once in a while - take down, various add-ons that few people will use - take down, unnecessary plugins just delete.

### Kernel
I recommend using [Airplane](https://github.com/TECHNOVE/Airplane) for 1.16-1.17.x. For 1.12 and below - Spigot. **Do not use** [Bukkit](https://getbukkit.org/), [Spigot](https://getbukkit.org/), [Paper](https://papermc.io/downloads) or other unknown kernels.

### Configuration

#### server.properties

**view-distance** - chunk loading distance. If you have a lot of players on the server and lags occur because of the chunks - lower this parameter to 4-5 chunks. 6 chunks is quite enough for vanilla survival.

````java
view-distance=6
````

#### bukkit.yml
**spawn-limits** - parameter, which is responsible for changing the number of mobs per player. These limits apply only to animals or monsters in loaded chunks. If you don't need bats - set it to 0.

````yaml
monsters: 25, animals: 8, water-animals: 2, water-ambient: 1, ambient: 1
````
**period-in-ticks** - the less, the faster the server will unload empty chunks. If you have more than 60 people playing on your server, it is advisable to lower this parameter to 350.

````yaml
period-in-ticks: 400
````

**autosave** - If the server has an HDD drive, you will have to suffer lags due to automatic saving. You must have an SSD for the server to work properly. Raise the value to 12000 for a comfortable game. By the way, if you have a plugin for autosave world - remove it, use this parameter, it is no worse.

````yaml
autosave: 12000
````

#### spigot.yml
**save-user-cache-on-stop-only** - This parameter disables the permanent saving of user data. If your server crashes, user data will not be saved. It is advisable to restart your server every 48-72 hours to prevent losses. **Change this parameter at your own risk!

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

#### paper.yml

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

### Map loading

To avoid clogging up your disk too quickly, you can load your map with the [Chunky] plugin (https://www.spigotmc.org/resources/chunky.81534/). It's completely free. After you add the plugin to your plugins folder, restart your server and announce technical work for a few hours to your players. Stand at map zero coordinates and enter these commands in turn: `/chunky center`, `/chunky radius 6000`, `/chunky start`. Done! Now you have to wait from one to 8 hours for the plugin to load the 6000 blocks that we set in the second command. It is desirable to limit your world to 6000 blocks. Believe me, this number of blocks will be enough for everyone to enjoy playing. If you still need to increase the size of the map to higher values - instead of 6000 write your number.

After loading the map you need to restart the server. The load on the processor will be reduced, and the consumption of RAM from the map is now completely gone.

### Anticheat

Almost every anticheat plugin is cheesy and consumes too many resources, but [Vulkan](https://www.spigotmc.org/resources/vulcan-advanced-cheat-detection-1-7-1-16-5.83626/) is not like that at all. It's the best anticheat in my opinion, productive and powerful, which makes "bugs" **very rarely.












