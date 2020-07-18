# Raspberry Pi CheatSheet

## 目錄
[機體資訊](#機體資訊) 

[必備項目](#必備項目) 

[機體構造](#機體構造) 

[腳位圖](#腳位圖)  

[將作業系統載入記憶卡](#將作業系統載入記憶卡)  

[安裝](#安裝)

[首次設定](#首次設定)  

[設定遠端連線](#設定遠端連線)

[軟體安裝或設定](#軟體安裝或設定)

[常用指令](#常用指令)


## 機體資訊
  * 型號 : Raspberry Pi 4B
  * Ram : 4G (同款有 2G 與 8G 可供選擇)

## 必備項目
  * 主機體
  * 64G Micro SD記憶卡 (注意是 Micro SD)
  * Type-C 變壓器 (建議購置原廠)
  * 保護機體外殼 (建議含風扇和散熱片，因為 Pi 4B 較容易發燙)
  * HDMI(母) 轉 Micro HDMI(公) 轉接頭
  * Micro SD記憶卡讀卡器
  * 鍵盤、滑鼠
  * 其他依據自己應用需求採購感應器與線材
  
  採購參考網頁：https://www.eclife.com.tw/led/0703300039/1401100001/160309001


## 機體構造 
![image](https://github.com/Samuelchi861008/RaspberryPi_CheatSheet/blob/master/Model%20Overview.png)


## 腳位圖
![image](https://github.com/Samuelchi861008/RaspberryPi_CheatSheet/blob/master/%E8%85%B3%E4%BD%8D%E5%9C%96.png)


## 將作業系統載入記憶卡 
以 MacOS 作為示範
  * 下載官方作業系統檔案
    * 分為三種版本(附帶圖形化介面和建議軟體、圖形化介面、單純指令介面)，擇一下載 zip
    * https://www.raspberrypi.org/downloads/raspbian/
  * 安裝 p7zip
    * ```$ brew install p7zip```
  * 解壓縮 (解壓縮後將會產生相同檔名的img檔)
    * ```$ 7z x [檔案路徑]```
  * 將 Micro SD 記憶卡插入讀卡機並插入電腦
  * 查詢 Micro SD 記憶卡的硬碟代號
    * ```$ diskutil list ```
    * 將可看到電腦所有硬碟代號 (範例：/dev/disk2)
  * Micro SD 記憶卡進行格式化
    * ```$ diskutil eraseDisk FAT32 RPI [Micro SD 的硬碟代號]```
    * 範例：```$ diskutil eraseDisk FAT32 RPI /dev/disk2```
  * 卸載
    * ```$ diskutil unmountDisk [Micro SD 的硬碟代號]```
    * 範例：```$ diskutil unmountDisk /dev/disk2```
  * 將作業系統寫入 Micro SD 記憶卡
    * ```$ sudo dd bs=1m if=[img 檔案路徑] of=[Micro SD 的硬碟代號]```
    * 範例：```$ sudo dd bs=1m if=xxxx.img of=/dev/disk2```
    * 下指令以後可能會需要等5~10分鐘，等待出現文字訊息則為載入完畢，並非當機
  * 再次卸載
    * ```$ diskutil unmountDisk [Micro SD 的硬碟代號]```
    * 範例：```$ diskutil unmountDisk /dev/disk2```
  * 拔出讀卡機，取出 Micro SD 記憶卡


## 安裝
  * 將散熱片確實貼上 Raspberry Pi
  * 將安裝完作業系統的 Micro SD 記憶卡插入至 Raspberry Pi
  * 將盒子與風扇組裝完成，並將 Raspberry Pi 放至盒子中
  * 將鍵盤滑鼠接上 USB 連接阜
  * 將 HDMI 接上轉接頭後插入 Micro HDMI 連接阜，HDMI 需接上一個外接螢幕
  * 若要使用網路線也可插入網路線 (內建有 Wi-Fi，故請自行選擇)
  * 最後再將電源接上，則會自動開機

## 首次設定
  * 首先，會看到歡迎頁面，點擊『Next』即可
  * 『Set Country』頁面
    * Country : Taiwan
    * Language : Chinese
    * Timezone : Taipei
    * 勾選『Use US Keyboard』
  * 『Change Password』修改預設密碼頁面
    * 輸入新密碼，並再次輸入一次進行驗證
    * 假設不想設定可直接按『Next』跳過，而預設帳號為『pi』、預設密碼為『raspberry』
  * 『Set Up Screen』頁面
    * 假設螢幕過大，則畫面將不會填滿整個螢幕，想要填滿則勾選下方選項即可
  * 『Select Wireless Network』頁面
    * 選擇一個可用 Wi-Fi 並輸入密碼連線即可
  * 『Update Software』頁面，直接點擊『Next』將軟體更新至最新，需等待10~15分鐘
    * 過程中可能會進入休眠狀態，動一動滑鼠即可恢復
    * 最後等待 『Restart』按鈕出現，並點擊重啟即可完成更新
  * 重啟後，開啟『終端機』，修改 root 密碼
    * ```$ sudo passwd root```
    * 輸入新密碼，並再次輸入一次進行驗證
  * 使用右鍵點擊右上角鍵盤符號，選擇『configureFcitx』進行中英文輸入鍵盤快捷鍵設定
  * 點擊左上角莓果圖案，在『偏好設定』中找到『Raspberry Pi 設定』
    * 點擊『介面』標籤頁，將『攝影機』、『SSH』、『VNC』、『遠端GPIO』啟用
    * 會要求再次重啟，點擊重啟即可

## 設定遠端連線
遠端連線分為兩種模式，VNC (遠端桌面) 與 SSH (遠端指令介面)
  * VNC 連線
    * 先前往 VNC 官網註冊帳號  
    https://www.realvnc.com/
    * 點擊 Raspberry Pi 右上角 VNC 圖案，並利用註冊的帳密找到登入頁面進行登入
      * 登入時，請記得選擇家用，則為永遠免費
    * 自己電腦或手機請下載 VNC Viewer，登入後則會看到 Raspberry Pi 裝置，即可遠端連線使用  
    https://www.realvnc.com/en/connect/download/viewer/
    * 以上方式可不需與 Raspberry Pi 同網段
  * SSH 連線 (內網連線)
    * 需與 Raspberry Pi 相同網段
    * 先在 Raspberry Pi 透過 ifconfig 查看 IP 位置 (範例: 192.168.x.x)
    * 在自己電腦與手機打開『終端機』，輸入  
    ```$ ssh pi@192.168.x.x```
    * 輸入密碼後即可登入 (首次登入會需要先輸入 yes or no)
  * SSH 連線 (外網連線)
    * 可不需與 Raspberry Pi 相同網段，且 Raspberry Pi 可以連接 Wi-Fi
    * 首先，先從中華電信申請固定IP  
    http://service.hinet.net/2004/adslstaticip_query.php
    * 將自己電腦先與 Raspberry Pi 連接網段 (也就是連結相同網路分享器)
    * 透過自己電腦瀏覽器進入網路分享器，開啟設定頁面
    * 將網路分享器以先前申請的固定IP進行設定，將網路分享器固定IP
    * 在網路分享器內找到 Raspberry Pi 內網 IP，並以 DHCP 設定固定內網 IP
    * 在網路分享器內設定『連接阜轉發』至 Raspberry Pi 內網 IP 的 22 port
    * 內部可固定 22 port，但外部 port 建議自定義更換
    * 以 SSH 外部連線後，輸入  
    ```$ ssh pi@中華電信申請的固定IP -p 自定義的port```
    * 若出現『WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED!』錯誤訊息，輸入```$ ssh-keygen -R 中華電信申請的固定IP```，再重新連線。


## 軟體安裝或設定
  * Visual Studio Code (簡稱：VS code)
    * 本方式安裝並非官方提供方式，因為官方並未針對ARM架構之CPU裝置提供載點，因此國外人士針對開源程式碼進行修改後，修改成適合ARM架構的軟體，並提供下載，整體與官方版本功能皆相同。
    * 首先，開啟『終端機』切換成管理員權限  
    ```$ sudo -s```
    * 安裝 VS code  
    ```# . <( wget -O - https://code.headmelted.com/installers/apt.sh )```
    * 切換回一般使用者模式  
    ```# exit```
    * 開啟 VS code (若不想使用指令開啟，可從應用程式選單選擇或是將項目釘選到桌面或工具列)  
    ```$ code-oss```

  * Git 初始設定
    * 預設已安裝好 Git，因此直接進行設定即可
    * 首先，確認是否已設定過(若沒有設定過將不會顯示出任何文字，若設定過則不需要再設定)  
    ```$ git config list```
    * 設定使用者名稱  
    ```$ git config --global user.name "你的名字"```
    * 設定使用者信箱  
    ```$ git config --global user.email "你的信箱"```
  
  * 程式語言
    * 內建已安裝完畢 Python2(版本2.7.16) 與 Python3(版本3.7.3)
    * 內建已安裝完畢 gcc/g++ (版本8.3)


## 常用指令
以下指令應在 Raspberry Pi 執行
  
  * 查看 CPU 溫度  
  ```$ vcgencmd measure_temp```
  
  * 查看已開啟的 Port  
  ```$ sudo netstat -tulpn```
  
  * 查看 SD 卡空閒狀況  
  ```$ df -h```
  
  * 查看 USB 連接的硬體  
  ```$ lsusb```

  * 查看硬體詳細資訊  
  ```$ sudo apt-get install lshw``` (首次需先安裝)  
  ```$ lshw```

  * 查看目前網路資訊  
  ```$ iwconfig wlan0```
  
  * 更新所有套件資料  
  ```$ sudo apt-get update```
  
  * 升級所有套件資料  
  ```$ sudo apt-get upgrade```  
  
  * 清除所有更新時下載的暫存安裝檔案  
  ```$ sudo apt-get clean```

  * 進行系統設定  
  ```$ sudo raspi-config```

  * 立即關機  
  ```$ sudo shutdown -h now```