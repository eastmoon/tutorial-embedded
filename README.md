# 嵌入式系統 ( Embedded System )

此專案主要記錄各類嵌入式系統的教學與使用文獻，並撰寫與設計相關自動化腳本。

## Raspberry Pi 3

### 裝置規格

+ [Raspberry Pi 3 Model B+](https://static.raspberrypi.org/files/product-briefs/Raspberry-Pi-Model-Bplus-Product-Brief.pdf)
    - ARM Cortex-A53
    - SDRAM 1G
    - 4 x USB 2.0、Gigabit Ethernet、IEEE 802.11 Wireless LAN、Bluetooth 4.2
+ HDD：[microSD 16G+](https://www.raspberrypi.com/documentation/computers/getting-started.html#sd-cards)
    - for Raspberry Pi Zero, 1 and 2，microSD must be 256G or less
    - for Raspberry Pi 3 to new version，2，microSD do not have this limitation
+ Power：USB Micro 5v / 2A
+ Input：USB keyboard、USB Mouse
+ Output：HDMI

### 作業系統

嵌入式系統安裝的作業系統為 Linux，開發者可以透過印象檔燒入至 microSD 中，並安裝至嵌入式設備。

+ [Installing the Operating System](https://github.com/raspberrypi/documentation/blob/develop/documentation/asciidoc/computers/getting-started/installing-from-an-image.adoc)
    - 自 [Raspberry Pi OS](https://www.raspberrypi.com/software/) 下載對應作業系統 ( Windows、MacOS、Linux ) 的 Raspberry Pi Imager
    - 連結 SD 卡讀取器並放置 SD 卡在其中
    - 開啟 Raspberry Pi Imager 並自清單中選擇需要的作業系統
    - 選擇映像檔安裝的 SD 卡
    - 確認妳的選項並點擊寫入 ( Write button ) 來開始對 SD 卡寫入資料
    - 寫入完成後，將 SD 卡取出並放置於 Raspberry Pi 的 SD 卡槽
    - 啟動 Raspberry Pi
    - 登入帳號 Raspberry Pi OS 預設帳號 ```pi```，密碼 ```raspberry```

+ [Pi-gen](https://github.com/RPi-Distro/pi-gen) a tool used to create Raspberry Pi OS images.
    - [Create your own custom Raspberry Pi image](https://opensource.com/article/21/7/custom-raspberry-pi-image)

+ [設定 Raspberry Pi](https://www.raspberrypi.com/documentation/computers/configuration.html)
    - [設定 raspi-config](http://korewa72.blogspot.com/2018/08/raspi-config-raspberry-pi-3b.html)

+ [無線網路裝置設定](./docs/wlan.md)

## NVIDIA Jetson NANO

### 裝置規格

+ [NVIDIA Jetson NANO](https://elinux.org/Jetson_Nano)、[Spec Document](https://developer.download.nvidia.com/assets/embedded/secure/jetson/Nano/docs/NV_Jetson_Nano_Developer_Kit_User_Guide.pdf?5oddmTH4mRABebvgkzlp8nhAsGJDSTrlRGeY5NTB16Wj59jjcduh0-v1Y2CHE0NIm1FObRt6dC9HWWSwhLD0MZ9UJrXQtV6YGdC1daRjcbEuWYyQv7d62jBeQIj5mTYlDIZyeBGFANsdOyphz5m74d27nTHggm40WBdERJIXL601GEXheXMrFj0iGpbC7UiM19Q&t=eyJscyI6ImdzZW8iLCJsc2QiOiJodHRwczpcL1wvd3d3Lmdvb2dsZS5jb21cLyJ9)
    - Quad-core ARM A57 64-bit CPU、128-Core Maxwell GPU
    - DDR4 4G
    - 4 x USB 3.0、Gigabit Ethernet、Bluetooth 4.2
+ HDD：microSD 16G+
+ Power：USB Micro 5v / 2A
+ Input：USB keyboard、USB Mouse、USB Wireless networking adapter
+ Ouput：HDMI 2.0、DisplayPort

## 參考

+ [Raspberry Pi Foundation](https://www.raspberrypi.org/)
    - [Raspberry Pi 台灣樹莓派](https://www.raspberrypi.com.tw/)
