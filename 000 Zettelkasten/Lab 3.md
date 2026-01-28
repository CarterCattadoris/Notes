###### Lab 3: Raspberry Pi OS
###### Group Members: Carter Cattadoris, Lucas Le, Jon-Micheal Gonzalez

##### All checkpoints verified on Jan 28
---
##### Jan 28, 2:00-2:15PM

command 1:
```
kmsprint
Connector 0 (33) HDMI-A-1 (connected)
  Encoder 0 (32) TMDS
    Crtc 2 (92) 1920x1080@60.00 148.500 1920/88/44/148/+ 1080/4/5/36/+ 60 (60.00) P|D 
      Plane 2 (81) fb-id: 682 (crtcs: 2) 0,0 1920x1080 -> 0,0 1920x1080 (XR24 AR24 AB24 XB24 RG16 BG16 AR15 XR15 RG24 BG24 YU16 YV16 YU24 YV24 YU12 YV12 NV12 NV21 NV16 NV61 P030 XR30 AR30 AB30 XB30 RGB8 BGR8 XR12 AR12 XB12 AB12 BX12 BA12 RX12 RA12 P010 P012 P016 S010 S012 S016)
        FB 682 1920x1080 XR24
      Plane 54 (655) fb-id: 685 (crtcs: 2) 0,0 64x64 -> 1777,-2 64x64 (XR24 AR24 AB24 XB24 RG16 BG16 AR15 XR15 RG24 BG24 YU16 YV16 YU24 YV24 YU12 YV12 NV12 NV21 NV16 NV61 P030 XR30 AR30 AB30 XB30 RGB8 BGR8 XR12 AR12 XB12 AB12 BX12 BA12 RX12 RA12 P010 P012 P016 S010 S012 S016)
        FB 685 64x64 AR24
Connector 1 (42) HDMI-A-2 (disconnected)
  Encoder 1 (41) TMDS
```

command 2: 
```
vcgencmd measure_volts core
volt=0.7200V
```

command 3: 
```
vcgencmd measure_temp pmic
temp=44.0'C
```

command 4: 
```
sudo vclog --msg
165171.367: *** Restart logging
165178.176: board: boardrev c04170 otp c04170
165190.745: Initial voltage 800000 temp 30685
165391.324: avs_2712: AVS pred 9124 912400 temp 30136
165394.930: vpred 912 mV +0
165399.136: over-voltage idle: 0 avs: 152400 delta: 0 (0x00000000)
166030.803: FB framebuffer_swap 1
166032.672: Select resolution HDMI0/2 hotplug 1 max_mode 2
166052.066: HDMI0 edid block 0 offset 0
166054.447: 00ffffffffffff005a632ede01010101
166060.120: 0b1c010380341d782e2cc5a45650a128
166065.793: 0f5054bfef80b300a940a9c095009040
166071.466: 818081408100023a801871382d40582c
166077.138: 450009252100001e000000ff00545654
166082.811: 3138313141313831300a000000fd0032
166088.484: 4b0f5213000a202020202020000000fc
166094.157: 0056583234353220536572696573014d
166112.344: HDMI0 edid block 1 offset 128
166114.903: 020328f1559005040302070608090e0f
166120.575: 1f1413121115161d1e0123097f078301
166126.248: 000065030c001000023a801871382d40
166131.921: 582c450009252100001e011d8018711c
166137.594: 1620582c250009252100009e011d0072
166143.267: 51d01e206e28550009252100001e8c0a
166148.940: d08a20e02d10103e9600092521000018
166154.613: 0000000000000000000000000000003c
166160.305: HDMI0: best-mode 2 (limit 2) 1920x1080 60 Hz CEA modes fec37fe0000000000000000000000000 extensions 1
166171.897: Select resolution HDMI1/2 hotplug 0 max_mode 2
166178.813: FB0 disp 0 max-fb 2 1920x1080 stride 3840 base 0x3f800000
169369.887: initramfs (initramfs_2712) loaded to 0x2de78000 (size 0x1187a6c)
169375.574: dtb_file 'bcm2712-rpi-5-b.dtb'
169515.367: dtparam: audio=on
169523.996: Unknown dtparam 'audio' - ignored
169614.145: Loaded overlay 'vc4-kms-v3d-pi5'
169791.170: Read command line from file 'cmdline.txt':
169797.674: 'console=serial0,115200 console=tty1 root=PARTUUID=9fae0b7a-02 rootfstype=ext4 fsck.repair=yes rootwait quiet splash plymouth.ignore-serial-consoles cfg80211.ieee80211_regdom=US'
170019.783: RPM 5276, max RPM 5276
173016.350: Device tree loaded to 0x2de64400 (size 0x13b1d)
173085.834: BSC_A no ACK
173087.061: BSC_A no ACK
173090.997: BSC_A no ACK
173116.935: BSC_B no ACK
173118.161: BSC_B no ACK
173122.087: BSC_B no ACK
173147.897: Starting OS 173147 ms
173153.593: 00000040: -> 00000480
173155.447: 00000030: -> 00100080
173160.159: 00000034: -> 00100080
173164.872: 00000038: -> 00100080
173169.585: 0000003c: -> 00100080
173265.523: sdram: sdram refresh 2081->8324 (1)
233193.317: initial_turbo of 60 deactivated
283194.539: sdram: sdram refresh 2081->4162 (2)
284194.971: sdram: sdram refresh 2081->8324 (1)
286195.923: sdram: sdram refresh 2081->4162 (2)
```

command 5: 
```
vcgencmd get_throttled
throttled=0x0
```

---
##### Jan 28, 2:15-2:30PM
Open a code editor (I used vscode)

use subprocess.run to run terminal commands. The syntax is as follows:
```
subprocess.run(['first word', 'second word', '...'], optional flag 1, optional flag 2)
```
the output is returned as a string with a newline character, so for the best formatting use .strip() to remove this

```
import subprocess

  
temp = subprocess.run(['vcgencmd', 'measure_temp'], capture_output=True, text=True)

voltage = subprocess.run(['vcgencmd', 'measure_volts', 'sdram_c'], capture_output=True, text=True)

  

print(temp.stdout.strip())

print(voltage.stdout.strip())
```

---
##### Jan 28, 2:30-2:45PM

key nano keybinds:
in terminal, run nano <filepath> to edit your desired file, then:

ctrl+G - display all keybinds and their functions
ctrl+X - exit nano
ctrl+O - write (save) the current buffer
ctrl+K - cut the current line your cursor is on
ctrl+U - paste
ctrl+F - search your file