## Personal OpenWrt OPKG Server
Install/upgrade paket openclash/passwall/ssr+/modeminfo dll dg mudah. instal paket tinggal opkg update && opkg install atau lewat luci di menu software.

Repository ini mendukung arsitektur dibawah ini:

```
aarch64_cortex-a53
aarch64_cortex-a72
aarch64_generic
arm_cortex-a7_neon-vfpv4
i386_pentium4
mipsel_24kc
x86_64
```

## Cara Pakai
Cara pakai dan instalasi repository ini, dapat menggunakan 2 cara yaitu
- [Menggunakan LuCI](#menggunakan-luci)
- [Menggunakan Terminal](#menggunakan-terminal) seperti JuiceSSH/Termius/Termux


### Menggunakan LuCI

  1. Masuk IP LuCI (contoh: 192.168.1.1), Login, Buka **System -> Software -> Configuration**
  
  2. Tambahkan tanda # (pagar) di depan baris ```option check_signature```, contoh dibawah ini
  
      ubah tulisan dibawah ini
      
      ```
      option check_signature
      ```
      
      menjadi seperti ini
      
      ```
      # option check_signature
      ```

  3. Pada bagian custom feeds tambahkan list dibawah ini

      ```
      src/gz custom_generic https://raw.githubusercontent.com/lrdrdn/my-opkg-repo/main/generic
      src/gz custom_arch https://raw.githubusercontent.com/lrdrdn/my-opkg-repo/main/arm_cortex-a7_neon-vfpv4
      ```

      ubah **arm_cortex-a7_neon-vfpv4** dan sesuaikan arsitektur CPU router OpenWrt kalian

      ![](https://raw.githubusercontent.com/lrdrdn/my-opkg-repo/main/preview/preview1.gif)
 
### Menggunakan Terminal
  1. Gunakan salah satu rekomendasi aplikasi Terminal dibawah ini
      - Terminal TTYD (Paket OpenWrt)
      - JuiceSSH
      - Termius
      - Termux
   
   
      > Catatan: Pengguna dapat menggunakan aplikasi terminal selain yang disebutkan diatas
  
  2. Copy paste dibawah di terminal, otomatis akan menyesuaikan tipe arsitektur cpu router
      
      ```
      sed -i 's/option check_signature/# option check_signature/g' /etc/opkg.conf
      echo "src/gz custom_generic https://raw.githubusercontent.com/lrdrdn/my-opkg-repo/main/generic" >> /etc/opkg/customfeeds.conf
      echo "src/gz custom_arch https://raw.githubusercontent.com/lrdrdn/my-opkg-repo/main/$(cat /etc/os-release | grep OPENWRT_ARCH | awk -F '"' '{print $2}')" >> /etc/opkg/customfeeds.conf
      ```

      > Catatan: untuk firmware OpenWrt 19.07 masih ada yg harus install manual seperti `kcptun-client`, `xray-core` dan `libcap-bin`.
    
      ![](https://raw.githubusercontent.com/lrdrdn/my-opkg-repo/main/preview/preview2.gif)
    
