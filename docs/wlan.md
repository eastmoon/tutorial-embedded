# Linux 環境下無線網路 ( WIFI、Wireless Fidelity ) 設定

## 確認網路與介面狀態

```
sudo ifconfig
```
> 顯示與設定網路網路與介面狀態

```
sudo iwconfig
```
> 顯示與設定無限網路連線狀態

在實務上 ```iwconfig``` 會出現無線網路狀態 ( wlan0 )，但 ```ifconfig``` 並未出現網路介面 ( wlan0 )，表示有功能但啟動

## 啟動無線網路

```
sudo ifconfig wlan0 up            // 啟動網路介面 wlan0
sudo ifconfig wlan0 down          // 關閉網路介面 wlan0
```
> 再實務上碰到 [SIOCSIFFLAGS: Operation not possible due to RF-kill](https://askubuntu.com/questions/62166) 錯誤時，多數表示網卡並沒正常啟動，可以據文獻說明操作設定後再啟動網卡

## 設定無線網路路由

+ [wpa_cli](https://linux.die.net/man/8/wpa_cli)
    - [wpa_supplicant及wpa_cli使用方法](https://segmentfault.com/a/1190000011579147)
    - [命令列設置無線網路](https://www.raspberrypi.com.tw/2152/setting-up-wifi-with-the-command-line/)

由文獻所示，無線網路操作共有兩種主要方式

+ ```iwconfig```，適用傳統無線網路設定
+ ```wpa_cli```，適用 WPA/WPA2 無線網路設定

由於常規無線網路節點為 WPA/WPA2 規格，此處以 ```wpa_cli``` 做操作記錄；文獻中修改 ```/etc/wpa_supplicant/wpa_supplicant.conf``` 的方式可以透過 ```wpa_cli``` 設定，因此並使用此方式。

實務上，在利用 ```wpa_cli``` 完成網路連線並啟用，系統會對網路節點連線並取得網址，倘若有連線但未取得網址，則可使用 [dhclient](https://linux.die.net/man/8/dhclient) 自介面向網路解點取得網址 ( DHCP )  

### 搜尋無線網路節點

```
wpa_cli -i wlan0 scan             // 搜尋網路節點
wpa_cli -i wlan0 scan_result      // 輸出搜尋結果
```

### 設定網路連線

假定 wifi 節點 ESSID 為 "NAME"、密碼為 "PSK"

```
wpa_cli -i wlan0 add_network      // 增加一個網路連線
```

+ 加密原則為 [WPA-PSK-CCMP+TKIP]、[WPA2-PSK-CCMP+TKIP]、[ESS]

```
wpa_cli -i wlan0 set_network 0 ssid '"NAME"'
wpa_cli -i wlan0 set_network 0 psk '"PSK"'
wpa_cli -i wlan0 enable_network 0
```

+ 加密原則為 [WEP]、[ESS]

```
wpa_cli -i wlan0 set_network 0 ssid '"NAME"'
wpa_cli -i wlan0 set_network 0 key_mgmt NONE
wpa_cli -i wlan0 set_network 0 wep_key0 '"PSK"'
wpa_cli -i wlan0 enable_network 0
```

+ 加密原則為 [ESS] 無加密狀態

```
$ wpa_cli -i wlan0 set_network 0 ssid '"NAME"'
$ wpa_cli -i wlan0 set_network 0 key_mgmt NONE
$ wpa_cli -i wlan0 enable_network 0
```

### 儲存網路連線設定

此指令執行後，會依據前述設定直接寫入 ```/etc/wpa_supplicant/wpa_supplicant.conf``` 檔案
```
wpa_cli -i wlan0 save_config
```

## 設定鍵盤模式 ( 非必要操作 )

基於指令需要，適度調整鍵盤設定以便於輸入指令

```
sudo sed -i 's/XKBLAYOUT="gb"/XKBLAYOUT="us"/' /etc/default/keyboard
```
> [The XKB Configuration Guide](https://www.x.org/releases/X11R7.5/doc/input/XKB-Config.html)

## 設定無線網路地區 ( 非必要操作 )

```
sudo sed -i 's/REGDOMAIN=/REGDOMAIN=TW/' /etc/default/crda
```
> [How to set country (region) for WiFi globally in Linux](https://unix.stackexchange.com/questions/629134)

## 參考

+ [How to Configure Wireless on Any Linux Desktop](https://www.linux.com/training-tutorials/how-configure-wireless-any-linux-desktop/)
+ [Ubuntu 網路設定 - iwlist, iwconfig 無線上網指令](http://note.drx.tw/2010/12/network-wireless.html)
+ [手動向DHCP Server取得IP－ dhclient](https://david50.pixnet.net/blog/post/27179542)
+ [Can you explain how to understand what the 'iwconfig' command displays in Ubuntu-9.04?](https://superuser.com/questions/42460)
    - [您能解釋一下如何理解在Ubuntu-9.04中’iwconfig’命令顯示什麽嗎？](https://ubuntuqa.com/zh-tw/article/8959.html)
