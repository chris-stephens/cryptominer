## Building a Crypto-Currency Miner

### Background
I built a crypto-currency miner in late 2013 and was able to mine some LiteCoin which ended up having a small value at the time.  I decided to not mine BitCoin because the mining network difficulty had risen beyond being profitable for GPU hardware (only custom ASICs were profitable at the time).

In late 2017, I decided to get back into cryptocurrency and build another mining machine.  My 2013 experiment had 4 AMD GPU's that were very power-hungry, loud, and generated a ton of heat.  My goal this time was to build a condensed desktop miner that didn't generate too much noise or heat, so I decided to go with a single GPU setup and mini-ITX motherboard/case.  

### Parts List

- [EVGA GeForce GTX 1080 Ti Video Card](http://amzn.to/2qzImd3) - Amazing graphics card with NVidia chip.  Lower power and more efficient design.  Unfortunately, the most costly part of the build.
- [Thermaltake Core V1 Mini ITX Cube Case](http://amzn.to/2EkbcjM) - I wanted a sleek and clean case (as compared to the milk crate for my last build), so I went with this model.
- [BIOSTAR A68N-5545 AMD A8-5545 Motherboard/CPU](http://amzn.to/2m3hPiM) - I picked this motherboard/CPU combo because it was low cost and low power.  It includes a quad-core CPU and single PCIe x16 slot.
- [EVGA 750 GQ, 80+ GOLD 750W Power Supply](http://amzn.to/2D4ZQ3t) - The GPU required about 600W to be safe, so I went with this gold-efficiency PSU.
- [Samsung 850 EVO 500GB SSD](http://amzn.to/2D2CziG) - You could probably get by with a smaller drive, but this worked for me.  I wanted to make sure I had enough capacity to run a full BitCoin node in the future (~160GB right now).
- [Corsair Vengeance Blue 16 GB (2x8 GB) DDR3](http://amzn.to/2m6ii3M) - Another component that probably could have been cheaper.  I already had this, so I decided to use it.
- [Kill A Watt Electricity Usage Monitor](http://amzn.to/2CNkR51) - Optional eletrical outlet usage monitor.  This will allow you to calculate how much electricity your mining rig will use.

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

####


You can use the [editor on GitHub](https://github.com/chris-stephens/cryptominer/edit/master/index.md) to maintain and preview the content for your website in Markdown files.

Whenever you commit to this repository, GitHub Pages will run [Jekyll](https://jekyllrb.com/) to rebuild the pages in your site, from the content in your Markdown files.

### Markdown

Markdown is a lightweight and easy-to-use syntax for styling your writing. It includes conventions for

```markdown
Syntax highlighted code block

# Header 1
## Header 2
### Header 3

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```

For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/chris-stephens/cryptominer/settings). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://help.github.com/categories/github-pages-basics/) or [contact support](https://github.com/contact) and we’ll help you sort it out.
