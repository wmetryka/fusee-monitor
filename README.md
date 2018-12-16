# Fusée Gelée

```
                                      *     .--.
                                           / /  `
                          +               | |
                                 '         \ \__,
                             *          +   '--'  *
                                 +   /\
                    +              .'  '.   *
                           *      /======\      +
                                 ;:.  _   ;
                                 |:. (_)  |
                                 |:.  _   |
                       +         |:. (_)  |          *
                                 ;:.      ;
                               .' \:.    / `.
                              / .-'':._.'`-. \
                              |/    /||\    \|
                            _..--"""````"""--.._
                      _.-'``                    ``'-._
                __             __                   _   __
               / _|           /_/                  | | /_/
              | |_ _   _ ___  ___  ___    __ _  ___| | ___  ___
              |  _| | | / __|/ _ \/ _ \  / _` |/ _ \ |/ _ \/ _ \
              | | | |_| \__ \  __/  __/ | (_| |  __/ |  __/  __/
              |_|  \__,_|___/\___|\___|  \__, |\___|_|\___|\___|
                                          __/ |
                                          |___/
```

## Fusée Launcher

The Fusée Launcher is a proof-of-concept arbitrary code loader for a variety
of Tegra processors, which takes advantage of CVE-2018-6242 ("Fusée Gelée")
to gain arbitrary code execution and load small payloads over USB.

The vulnerability is documented in the 'report' subfolder; more details and
guides are to follow! Stay tuned...

## Fusée Monitor

The Fusée uses the original Fusée Launcher with the use of the `pyudev` library to monitor USB devices on a Linux machine and automatically inject the files into the switch when it's found.

### Use Instructions
The main launcher is "monitor-launcher.py". Only Linux is natively supported (due to udev being Linux exclusive), with the primary idea behind this software being devices like RaspberryPi running the script constantly, injecting the payload in a matter of seconds by just plugging in your device.

Invoke the launcher with the desired payload as an argument, e.g. `sudo python ./fusee-monitor.py payload.bin`. Connect a Nintendo Switch in recovery mode via USB. The inejction will happen as soon as it's detected.

To use this script automatically on each boot, use `sudo crontab -e` and add `@reboot PYTHONPATH=/_yourglobalpath_/python3.6/site-packages _yourglobalpath_/python3 /_yourglobalpath_/fusee-launcher-master/fusee-monitor.py /_yourglobalpath_/fusee-primary.bin` to the end of the file. Make sure all of your paths are global in order for crontab to run them. Make sure you ran crontab as sudo, otherwise the script will fail. 

Linux systems currently require either that the Tegra device be connected to an XHCI controller (used with blue USB 3 ports) or that the user has patched their EHCI driver. 

### Credits            
Fusée Gelée (CVE-2018-6242) was discovered and implemented by Kate Temkin (@ktemkin);
its launcher is developed and maintained by Mikaela Szekely (@Qyriad) and Kate Temkin (@ktemkin).

Credit goes to:

  * Qyriad -- maintainership and expansion of the code
  * SciresM, motezazer -- guidance and support  
  * hedgeberg, andeor  -- dumping the Jetson bootROM
  * TuxSH -- help with a first pass of bootROM RE
  * the ReSwitched team

Love / greetings to:

  * Levi / lasersquid
  * Aurora Wright
  * f916253
  * MassExplosion213 

CVE-2018-6242 was also independently discovered by fail0verflow member 
shuffle2 as the "shofEL2" vulnerability-- so that's awesome, too.
jestemkioskiem - provided the pyudev functionality
