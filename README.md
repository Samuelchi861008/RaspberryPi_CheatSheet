# Raspberry Pi CheatSheet

## 目錄
[機體資訊](#機體資訊) 

[必備項目](#必備項目) 

[機體構造](#機體構造) 

[腳位圖](#腳位圖)  

[將作業系統載入記憶卡](#將作業系統載入記憶卡)  

[安裝](#安裝)

[首次設定](#首次設定)  

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
  
  * 更新所有套件資料  
  ```$ sudo apt-get update```
  
  * 升級所有套件資料  
  ```$ sudo apt-get upgrade```  
  
  * 清除所有更新時下載的暫存安裝檔案  
  ```$ sudo apt-get clean```
