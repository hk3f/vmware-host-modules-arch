For arch linux aur package vmware-workstation, after linux kernel updated vmware-worksation package has to be reinstalled  again to prevent vmmon module error.
To shorten the reinstall time, the vmmon&vmnet module could be extracted and build a standalone module updated package.
How to use:
1) Exctract vmmon.tar and vmnet.tar from vmware-workstation bundle file. It should be stored in vmware-vmx/lib/modules/source.
2) Place them in src folder.
3) Run makepkg
4) Use sudo pacman -U vmware-module-update-xxxxxx.pkg.tar.zst when needed.
