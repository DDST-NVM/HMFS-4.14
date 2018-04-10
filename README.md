# Introduction

We are now working to transport hm(v)fs codes from linux kernel 3.11.0 to 4.14 (Fedora 27). 

The integration procedure falls into three steps:

1. Debug **hmfs** codes on linux 4.14;
   - Fix all the bugs before building `hmfs.ko` in local machine; [Checked]
   - Build `hmfs.ko` successfully in local machine; [Checked]
   - Build `hmfs.ko` successfully in AEP machine. [ToBeDone]
2. Test **hmfs** codes on AEP machine; [ToBeDone]
   - Test basic commands (successfully);
   - Test complicated commands and dataset.
3. Run **demo** codes on AEP machine. [ToBeDone]
   - Certify the application and explanation; (e.g., filebench? Redis?)
   - Run applications successfully.

## NOTICE

Generally `hmfs/` module does not need to modify kernel codes.

However, to solve the error of **'init-mm' module undefined** error, we add a simple line in `/mm/init-mm.c` as follows:

`
EXPORT_SYMBOL(init-mm);
`

User-mode methods are being considered and developed.

(To be added...)


## How to Use

```
git clone https://github.com/DDST-NVM/HMFS-4.14.git
cd HMFS-4.14/
make mrproper
make menuconfig (save and exit; by the way, make localmodconfig can also work properly)
make -jN (N is the number of threads to use)
sudo make modules_install
sudo make install
sudo reboot
[Choose new kernel during boot]
uname -r (See if it is the correct kernel after system booting up)
cd HMFS-4.14/fs/hmfs/
make clean
make
sudo insmod hmfs.ko
```


