## Personal OpenWrt OPKG Server
Install/upgrade paket openclash/passwall/ssr+/modeminfo dll dg mudah. instal paket tinggal opkg update && opkg install atau lewat luci di menu software.

### Cara Pakai
- **Menggunakan LuCI**

  system-software-configure opkg
  
  disable option check_signature, tambahkan tanda # (pagar) didepan option check_signature & bagian custom feeds tambahkan list dibawah ini

  ```
  src/gz custom_generic https://raw.githubusercontent.com/lrdrdn/my-opkg-repo/main/generic
  src/gz custom_arch https://raw.githubusercontent.com/lrdrdn/my-opkg-repo/main/arm_cortex-a7_neon-vfpv4
  ```

  ubah **arm_cortex-a7_neon-vfpv4** dan sesuaikan arsitektur CPU router OpenWrt kalian

  ![](https://raw.githubusercontent.com/lrdrdn/my-opkg-repo/main/preview/preview1.gif)
 
# 
- **Menggunakan Terminal/JuiceSSH/Termius/Termux**
  
  Copy paste dibawah di terminal, otomatis akan menyesuaikan tipe arc cpu router
  
  ```
  sed -i 's/option check_signature/# option check_signature/g' /etc/opkg.conf
  echo "src/gz custom_generic https://raw.githubusercontent.com/lrdrdn/my-opkg-repo/main/generic" >> /etc/opkg/customfeeds.conf
  echo "src/gz custom_arch https://raw.githubusercontent.com/lrdrdn/my-opkg-repo/main/$(cat /etc/os-release | grep OPENWRT_ARCH | awk -F '"' '{print $2}')" >> /etc/opkg/customfeeds.conf
  ```
  ![](https://raw.githubusercontent.com/lrdrdn/my-opkg-repo/main/preview/preview2.gif)
> note: untuk fw 19.07 masih ada yg harus install manual seperti kcptun-client, xray-core & libcap-bin.
