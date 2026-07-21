
git clone https://git.yoctoproject.org/poky
cd poky
git checkout dunfell
less meta-poky/conf/distro/poky.conf

git clone https://github.com/agherzan/meta-raspberrypi.git
cd meta-raspberrypi/
git checkout dunfell 

cd ..
git clone https://git.openembedded.org/meta-openembedded
cd meta-openembedded/
git checkout dunfell