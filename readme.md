# howto fix wireless drivers for Qualcomm Atheros QCA9377 on Lenovo Ideapad 320 running Debian9 Stretch

## get the debian stretch firmware binaries
```bash
wget http://ftp.br.debian.org/debian/pool/non-free/f/firmware-nonfree/firmware-atheros_20180825+dfsg-1_all.deb
dpkg -i firmware-atheros_20180825+dfsg-1_all.deb
```

This should create a directory /lib/firmware/ath10k containing all supported models for this driver

## clone this guys firmware and copy just his firmware-5.bin to the hw1.0 root
```bash
git clone https://github.com/kvalo/ath10k-firmware.git
cp ath10k-firmware/QCA9377/hw1.0/CNSS.TF.1.0/firmware-5.bin_CNSS.TF.1.0-00267-QCATFSWPZ-1 /lib/firmeware/ath10k/QCA9377/hw1.0/firmware-5.bin
```

## then copy the latest firmware-6.bin from the original QCA9377 into the hw1.0 root @ /lib/firmware/ath10k/QCA9377/hw1.0/firmware-6.bin
```bash
cp /lib/firmware/QCA9377/hw1.0/WLAN.TF.2.1/firmware-6.bin_WLAN.TF.2.1-00021-QCARMSWP-1 /lib/firmware/ath10k/QCA9377/hw1.0/firmware-6.bin
```

# OR

## you can just download my prepackaged version of the QCA9377 directory and copy it to /lib/firmware/ath10k/
```bash
mkdir /lib/firmware/ath10k
cd /lib/firmware/ath10k
wget https://github.com/charlmert/qca9377/raw/master/QCA9377.tar.gz
tar -xzvf QCA9377.tar.gz
rm -f QCA9377.tar.gz
```

# Reload the driver

# in one terminal watch dmesg output
dmesg -w | grep ath10k_pci

# in another terminal reload the driver

rmmod ath10k_pci
modprobe -v ath10k_pci
