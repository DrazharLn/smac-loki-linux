# Installing Loki's port of Sid Meier's Alpha Centauri and Alien Crossfire

## Why?

There's really no good reason to. Get the windows version from GOG and run it in `wine`. That way you can use unofficial patches, too.

The text is rendered a bit nicer in the linux version.

## How?

1. Get the loki games CD or an iso of it
2. Mount it and run `setup.data/bin/Linux/x86/setup`
3. Try running the binaries `smac` and `smacx`. They're static and it's not impossible they'll *just work*. Can also try `qemu-i386 smac`. Didn't work for me (segfault without qemu; `Unable to initialize SDL: Not enough resources to create thread` with)
3. If it's not working yet or you want allegedly less bugs, get the 6.0a patch http://updates.lokigames.com/smac/
4. Run it with `smac-6.0a-x86.run --keep` because it won't find `loki-patch`. Then `cd smac-6.0a-x86; bin/Linux/x86/loki_patch patch.dat /path/to/smac/` to patch
5. Get the Loki compatibility libraries from http://www.improbability.net/loki/
6. Run with `LD_LIBRARY_PATH=/path/to/Loki_Compat /path/to/Loki_Compat/ld-linux.so.2 /path/to/smac/smacx.dynamic`
7. If you don't want it to steal the whole display use Xephyr (see launch script below)

## Caveats

Music isn't supported. The whining you might get from ALSA isn't about that.

IP multiplayer crashes the game. Hotseat/PBEM is fine.

Check Loki's FAQ: http://faqs.lokigames.com/smacfaq.html

## 6.0a patch changelog

New enhancements include:
 * Added Voice Over IP support (activated by the '\' key in-game)
 * Fixed system hang on some newer x86 processors.
 * Fixed colony pod instant win bug.
 * Fixed several floating point exceptions.
 * Fixed crash when using the Planetbuster.
 * Patrol waypoints are limited to 2 instead of 3 (fix memory corruption).
 * Movies now play when started with a key press.
 * Demo tutorial text no longer refers to the Windows start menu.

## Launch script

Adapted from a script on the lutris db. You'll probably want to change the paths.

```sh
#!/bin/bash

if [ ! -e /dev/dsp ]; then
    sudo modprobe snd-pcm-oss
fi
Xephyr :1 -screen 1024x768 -extension Composite -fullscreen -name "Alpha Centauri"&
xephyr_pid=$!
sleep 1

DISPLAY=:1 LD_LIBRARY_PATH=~/SMAC/Loki_Compat ~/SMAC/Loki_Compat/ld-linux.so.2 ~/SMAC/smac/smac.dynamic
kill -9 $xephyr_pid
```

## More SMACX!

You may also be interested in:

- [Scient's Unofficial Patch][scient]
- [The Alphacentauri2.info Wiki][ac2wiki]
- [The Alphacentauri2.info Forum][ac2forum]
- [Plotinus Redux's PRACX UI mod][pracx]
- [Thinker][thinker]
- [Yitzi's patch][yitzi]
- [bvanery's SMACX AI Growth mod][aigrowthmod]
- [The SMAC in SMAX project][smac-in-smax]

The patches are all for the windows version.

[ac2wiki]: http://alphacentauri2.info/wiki/
[ac2forum]: http://alphacentauri2.info/index.php?action=community
[pracx]: https://github.com/drazharln/pracx
[scient]: https://github.com/drazharln/scient-unofficial-smacx-patch
[thinker]: https://github.com/induktio/thinker
[yitzi]: http://alphacentauri2.info/wiki/Yitzi%27s_patch
[aigrowthmod]: http://alphacentauri2.info/index.php?topic=20959.0
[smac-in-smax]: https://github.com/drazharln/smac-in-smax
