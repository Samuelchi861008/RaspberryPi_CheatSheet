# Raspberry Pi CheatSheet

## 目錄
[機體資訊](#機體資訊) 

[必備項目](#必備項目) 

[機體構造](#機體構造) 

[腳位圖](#腳位圖)  

[將作業系統載入記憶卡](#將作業系統載入記憶卡)


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
  * 其他依據自己應用需求採購感應器與線材
  
  採購參考網頁：https://www.eclife.com.tw/led/0703300039/1401100001/160309001


## 機體構造 
![image](https://github.com/Samuelchi861008/RaspberryPi_CheatSheet/blob/master/Model%20Overview.png)


## 腳位圖
![image](https://github.com/Samuelchi861008/RaspberryPi_CheatSheet/blob/master/%E8%85%B3%E4%BD%8D%E5%9C%96.png)


## 將作業系統載入記憶卡 
以 MacOS 作為示範
  * 下載官方作業系統檔案
    * 分為三種版本(附帶圖形化介面和建議軟體、單純圖形化介面、單純指令介面)，擇一下載 zip
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
