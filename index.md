## Building a Crypto-Currency Miner

### Background
I built a crypto-currency miner in late 2013 and was able to mine some LiteCoin which ended up having a small value at the time.  I decided to not mine BitCoin because the mining network difficulty had risen beyond being profitable for GPU hardware (only custom ASICs were profitable at the time).

In late 2017, I decided to get back into cryptocurrency and build another mining machine.  My 2013 experiment had 4 AMD GPU's that were very power-hungry, loud, and generated a ton of heat ([pic](https://imgur.com/4yjGuHI).  My goal this time was to build a condensed desktop miner that didn't generate too much noise or heat, so I decided to go with a single GPU setup and mini-ITX motherboard/case.  

### Parts List

- [EVGA GeForce GTX 1080 Ti Video Card](http://amzn.to/2qzImd3) - Amazing graphics card with NVidia chip.  Lower power and more efficient design.  Unfortunately, the most costly part of the build.
- [Thermaltake Core V1 Mini ITX Cube Case](http://amzn.to/2EkbcjM) - I wanted a sleek and clean case (as compared to the milk crate for my last build), so I went with this model.
- [BIOSTAR A68N-5545 AMD A8-5545 Motherboard/CPU](http://amzn.to/2m3hPiM) - I picked this motherboard/CPU combo because it was low cost and low power.  It includes a quad-core CPU and single PCIe x16 slot.
- [EVGA 750 GQ, 80+ GOLD 750W Power Supply](http://amzn.to/2D4ZQ3t) - The GPU required about 600W to be safe, so I went with this gold-efficiency PSU.
- [Samsung 850 EVO 500GB SSD](http://amzn.to/2D2CziG) - You could probably get by with a smaller drive, but this worked for me.  I wanted to make sure I had enough capacity to run a full BitCoin node in the future (~160GB right now).
- [Corsair Vengeance Blue 16 GB (2x8 GB) DDR3](http://amzn.to/2m6ii3M) - Another component that probably could have been cheaper.  I already had this, so I decided to use it.
- [Kill A Watt Electricity Usage Monitor](http://amzn.to/2CNkR51) - Eletrical outlet usage monitor (optional).  This will allow you to calculate how much electricity your mining rig will use.

Total cost for me was about $960 since I already had the SSD and memory from an old project.  You could probably cut some costs with a cheaper power supply, however the $80 CPU/motherboard combination in the list above can't be beat.  Keep in mind that a powerful CPU isn't important, since the GPU will be doing most of the work.

### Build Process

#### Power On & BIOS Settings
Once you have all the parts, it's time to put it together.  If you aren't familiar with building a computer, do some quick research online or on Youtube.  Once everything is assembled, it's time to install the OS.  Keep in mind that some BIOS will not allow your onboard GPU to function with an add-on PCIe GPU installed, so if there is no output to your monitor be sure to use the add-on GPU (you can fine-tune the preference in the BIOS settings).  You will also want to configure the BIOS options to power on the system after an outage.  This will ensure that mining continues even if you are not around to start it up.

#### OS Selection
I would suggest going with a Windows OS for a mining machine, as the driver support is typically better than Linux.  Unfortunately, the downfall is that Windows 10 is bundled with a bunch of extra components.  You could try using Microsoft Server 2012 R2 or 2016, but I haven't tested that out yet.  **Make sure the OS is 64-bit.**

#### OS Configuration & Drivers
After installing the operating system, you'll want to configure the following:
- Setup your account to auto-login (run **Netplwiz** and uncheck the "_Users must enter a password to use this computer_" option).
- Install [Visual Studio 2017 Redistributable 2017 x64 Package](https://aka.ms/vs/15/release/VC_redist.x64.exe).
- Disable User Account Control
- Install the latest Windows Updates and System Drivers (download from Intel/AMD).
- Install the latest GPU Drivers [NVIDIA](http://www.nvidia.com/Download/index.aspx) or [AMD](http://support.amd.com/en-us/download).

### Mining Software Installation
Depending on what you want to mine, the steps may be a bit different here.

#### Monero
The first thing you need to do is setup a wallet address.  This can be done by downloading the [Monero Client](https://getmonero.org/downloads/) and taking note of your wallet receiving address.  You should also setup a password for your wallet and store it in a safe place.  I would suggest not installing the Monero Client on your mining machine (you want that system to be as minimalist as possible).

#### Pool Selection
After setting up a wallet address, you need to select a mining pool to use.  A mining pool allows multiple miners to pool their resources and computing power to more efficiently mine for cryptocurrency.  Because the difficulty of mining a single block generally exceeds what a single GPU can do on it's own, the only way to actually earn value is to join a pool.  I use [SupportXMR](https://supportxmr.com/) in this example, but may others are also available.  You do not need to create an account within the pool, as all payouts will come to your Monero Receiving address.

#### Mining Software
I would suggest using [xmr-stak](https://github.com/fireice-uk/xmr-stak).  You can download the [latest Windows release](https://github.com/fireice-uk/xmr-stak/releases) and place it in a folder on your mining machine's hard drive (like **C:\xmr-stak-win64**).  Launch a command prompt and run the binary from that folder (**xmr-stak.exe**).  You will be prompted with a few questions, which you should answer (example below, be sure to use your wallet address):

```
c:\xmr-stak-win64\xmr-stak.exe
Please enter:
- Currency: 'monero' or 'aeon'
monero
- Pool address: e.g. pool.usxmrpool.com:3333
de03.supportxmr.com:7777
- Username (wallet address or pool login):
42TZm91mijNa19ME7rNcH7LUYEUvEHQqHQHst3u3Xkv15ftNHEfefzPRXAvygdcCusST2jVNcWTrVZU8dfAMZSBB8UM4dNj
- Password (mostly empty or x):
x
- Does this pool port support TLS/SSL? Use no if unknown. (y/N)
N
- Do you want to use nicehash on this pool? (y/n)
n
- Do you want to use multiple pools? (y/n)
n
Configuration stored in file 'config.txt'
```

After entering this information, the mining client will start.  It will be stored in the configuration file at **C:\xmr-stak-win64\config.txt**.

### Troubleshooting & Tuning

#### GPU Configuration
Once you've started mining, you'll want to check the console output for any errors.  In my situation, I immediately encountered a **[CUDA ERROR]** which typically means that something is wrong with the GPU operation.  This can occur if your GPU is overclocked or the GPU mining parameters are incorrect.  I found that the _bfactor_ in my configuration was wrong, as it was automatically generated by the xmr-stak client.  I modified it to the following (**C:\xmr-stak-win64\nvidia.txt**):

```
"gpu_threads_conf" :
[
  // gpu: GeForce GTX 1080 Ti architecture: 61
  //      memory: 9312/11264 MiB
  //      smx: 28
  { "index" : 0,
    "threads" : 32, "blocks" : 84,
    "bfactor" : 8, "bsleep" :  25,
    "affine_to_cpu" : false, "sync_mode" : 3,
  },
],
```

Additional configurations for your specific card can be found here - https://www.xmrstak.com/.

#### Auto-Start
Your operating system should be set to auto-login after reboot, however the **xmr-stak** client will still need to start.  On Windows 10, this can be done by placing a shortcut to the executable in the **shell:startup** folder.  After doing so, reboot the machine to ensure it starts automatically.

### Payouts
Once you start using the **SupportXMR** mining pool, you can check the balance of your account on the [Dashboard](https://supportxmr.com/#/dashboard).  No login is required, you can simply paste your Monero wallet address into the bottom half of the page.  Once your **Total Due** reaches **0.03**, it will be automatically sent to your wallet.

You can create an account within the SupportXMR portal by changing your pool password in the **C:\xmr-stak-win64\config.txt** configuration file to "_MinerName:your@email.com_" (replace with your email address).  After mining for a few minutes, you will then be able to login and change your payout threshold.


[Link](url) and ![Image](src)
