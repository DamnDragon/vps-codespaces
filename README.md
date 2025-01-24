Lệnh cài đặt nha mấy má
wget -O bios64.bin "https://github.com/BlankOn/ovmf-blobs/raw/master/bios64.bin"
wget -O os.iso "https://drive.massgrave.dev/en_windows_10_iot_enterprise_ltsc_2019_x64_dvd_a1aa819f.iso"
sudo apt update
sudo apt install qemu-kvm -y
qemu-img create -f raw os.img 20G
sudo qemu-system-x86_64 -m 10G -cpu host -boot order=c -drive file=os.iso,media=cdrom -drive file=os.img,format=raw -device usb-ehci,id=usb,bus=pci.0,addr=0x4 -device usb-tablet -vnc :0 -smp cores=4 -device rtl8139,netdev=n0 -netdev user,id=n0 -vga qxl -accel kvm -bios bios64.bin
