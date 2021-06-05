# idlerpg-patches

## Bot Source Patches

To apply the patches to the bot source:

1. copy patch file(s) to bot source directory
2. go to bot source directory
3. for each patch file run patch -p1 < irpgbot.v3.1.2+xyz.patch (with xyz replaced appropriately)
4. restart the bot

Some other patches for nice features may be found at http://vayanla.no-ip.com/idle/patch.php.
### irpgbot.v3.1.2+autologin

Author: Markus John [johm@quyo.de]

Automatically logs in any re-joining players if they didn't change their nick, ident and host since quitting.

###irpgbot.v3.1.2+config

Author: Christian Schuster [blackout@s2000.ws]

This small patch prevents the bot from complaining about undefined values when some configurations options are empty. This is the case if there is nothing but whitespace after the name of the option in the configuration file.

###irpgbot.v3.1.2+ha

Author: Christian Schuster [blackout@s2000.ws]

Another small patch to catch the rare case of an undefined user name to be handled by the bot. This may happen when someone tries to execute a privileged command immediately after bot startup.

###irpgbot.v3.1.2+ipv6

Author: Markus John [johm@quyo.de]

This patch adds IPv6 support to the bot. If you'd like to find out more about IPv6, visit http://www.ipv6.org/.

###irpgbot.v3.1.2+itemlevel

Author: Christian Schuster [blackout@s2000.ws]

This one fixes some warnings when string to integer conversion is called for a non-numeric argument (levels of unique items). The desired result, but without the warnings, is now achieved by separating the tag from the numeric level.

###irpgbot.v3.1.2+johm+chschu

Authors: Markus John [johm@quyo.de], Christian Schuster [blackout@s2000.ws]

This is the patch containing all changes made to the bot. It consists of

* irpgbot.v3.1.2+autologin
* irpgbot.v3.1.2+config
* irpgbot.v3.1.2+ha
* irpgbot.v3.1.2+ipv6
* irpgbot.v3.1.2+johm+chschu
* irpgbot.v3.1.2+mapitems+itemlevel
* irpgbot.v3.1.2+nick
* irpgbot.v3.1.2+reloadquest
* irpgbot.v3.1.2+skew
* irpgbot.v3.1.2+teambattle
* irpgbot.v3.1.2+ttl
* irpgbot.v3.1.2+voice
* irpgbot.v3.1.2+war

You'd probably prefer to apply the smaller patches one after another if you made changes to the bot. They have a much higher chance of being applied correctly despite your changes.

### irpgbot.v3.1.2+mapitems+itemlevel

Author: Christian Schuster [blackout@s2000.ws]

This patch contains one of the major changes made to the bot. It introduces items lying on the map. When players are levelling, the unneeded (new or old) item is dropped and its level is slowly decreased. The speed of this process may be adjusted in the configuration file. There may be more than one item at the same spot, and a player reaching that spot keeps the best items from his inventory and the ones lying around. Unique items lose their magic if their level falls below the minimum level of that unique item type.

This patch includes irpgbot.v3.1.2+itemlevel due to unavoidable dependencies.

### irpgbot.v3.1.2+nick

Author: Christian Schuster [blackout@s2000.ws]

This patch fixes the nick bug. A nick change resulting in a shorter or longer new nick caused the nick!ident@host of the user to break.

### irpgbot.v3.1.2+reloadquest

Author: Christian Schuster [blackout@s2000.ws]

This patch lets the bot reload the running quest after restart. If all four questers are online when the bot comes back, the quest continues normally. The host mask, ident and nick of the questers are not compared to the pre-restart values.

### irpgbot.v3.1.2+skew

Authors: Markus John [johm@quyo.de], Christian Schuster [blackout@s2000.ws]

This patch fixes a timer bug. If there is much to do during execution, there may be cycles running longer than $opts{self_clock}. As a result some equality checks fail and the corresponding events are not triggered properly.

### irpgbot.v3.1.2+teambattle

Author: Christian Schuster [blackout@s2000.ws]

This patch adds localized team battles to the bot. A random point on the map is chosen, and the six closest players are determined. The "batte arena" is then split into two sectors with three players each. The two resulting teams battle each other as usual.

### irpgbot.v3.1.2+ttl

Author: Markus John [johm@quyo.de]

This patch adds two functions for TTL calculations, namely the normal TTL and the penalty times. This makes changes to the TTL calculation a lot easier.

### irpgbot.v3.1.2+voice

Author: Christian Schuster [blackout@s2000.ws]

This patch contains a small fix to the voice-on-login code. The bot sent out less nicks than voice flags, resulting in some warnings.

### irpgbot.v3.1.2+war

Author: Christian Schuster [blackout@s2000.ws]

This patch introduces a new kind of event called "war" occurring roughly every 10 days. The map is split into four quadrants and the item values of all players in each quadrant are summed up. Then each quadrant challenges both of its direct neighbors according to the rules of normal challenges. If a quadrant defeats both neighbors, the TTL of every player in that quadrant is halved. If it loses both challenges, TTLs are doubled. If none of the above cases occur, i.e. the quadrant loses against one neighbor and defeats the other, the TTLs are kept as they are.

You'll probably hate that thing if you lose a war shortly after reaching level 50, but if you want to mix up the rankings a bit, this is your patch of choice.

## Site Source Patches

To apply the patches to the site source:

1. copy patch file(s) to site source directory
2. go to site source directory
3. for each patch file run patch -p1 < irpgsite.v0.5+xyz.patch (with xyz replaced appropriately)

### irpgsite.v0.5+mapitems+fgets

Author: Christian Schuster [blackout@s2000.ws]

This patch contains the code to display items on the map if you applied the irpgbot.v3.1.2+mapitem+itemlevel patch to the bot source. There were also some other calls to fgets lacking the second parameter needed for older PHPs.
