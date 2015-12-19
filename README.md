# Hacker Scripts

_[真人真事](https://www.jitbit.com/alexblog/249-now-thats-what-i-call-a-hacker/)_ :

> xxx：我們的一位工程師離職了。那傢伙是個活在終端機世界的人，他熱愛 Vim，喜歡用純文字作圖，使用 Markdown 語法編寫 Wiki 文件。任何事情如果需要超過 90 秒來處理，他就會編寫腳本來自動化它。

> yyy：傳奇啊，這個傢伙！

> xxx：你會愛死他的，例如 ...

> xxx：`smack-my-bitch-up.sh` 臭婆娘腳本 - 自動傳一個簡訊給他老婆，告訴老婆會因工作晚回家，簡訊內容會從一個字串陣列裡隨機挑選。觸發的條件是如果晚上 9 點以後，主機上還有他登入的 SSH Session 在活動。

> xxx：`kumar-asshole.sh` 庫馬爾你這白吃腳本 - 搜尋信箱中來自 Kumar (一個資料庫客戶) 的信，檢查關鍵字如果有「救命啊」、「出事啦」、「不好意思」等，就會自動登入客戶的主機，將資料庫回復到上一次的備份點，然後回信：「沒事了，下次小心點。」

> xxx：`hangover.sh` 醉後大丈夫腳本 - (週一到週五的) 排程工作，自動發信「身體不舒服，在家休息」之類的，理由一樣是隨機從陣列挑選。觸發條件是如果晚上 8:45 之後，主機上沒有屬於他的 SSH Session (代表跑去喝酒了)。

> xxx：[奧斯卡最佳腳本獎] `fucking-coffee.sh` 該死的咖啡咧腳本 - (週一到週五，早上九點到下午六點，整點啟動) 靜數 17 秒，接著啟動一個 telnet 連線到公司的咖啡機 (我們也搞不清楚咖啡機是怎麼被接上網路的，還跑了個帶 TCP 服務的 Linux 系統) 並傳送了 sys brew (釀造) 這樣的指令，煮了一杯中杯拿鐵，並且靜候 24 秒再開始倒咖啡。而這個時間恰恰就是腳本超人從他的辦公桌走到咖啡機的時間！

> yyy：你個熊寶寶，這個我也要！

原始出處： http://bash.im/quote/436725 (俄文)   
歡迎任何語言的實做 (Python, Perl, Shell 等)

## 使用方式

設定環境變數：

```sh
# used in `smack-my-bitch-up` and `hangover` scripts
TWILIO_ACCOUNT_SID=ACxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
TWILIO_AUTH_TOKEN=yyyyyyyyyyyyyyyyyyyyyyyyyyyyyyy

# used in `kumar_asshole` script
GMAIL_USERNAME=admin@example.org
GMAIL_PASSWORD=password
```

## Cron jobs

設定各個腳本執行的排程：

```sh
# Runs `smack-my-bitch-up.sh` monday to friday at 9:20 pm.
20 21 * * 1-5 /path/to/scripts/smack-my-bitch-up.sh >> /path/to/smack-my-bitch-up.log 2>&1

# Runs `hangover.sh` monday to friday at 8:45 am.
45 8 * * 1-5 /path/to/scripts/hangover.sh >> /path/to/hangover.log 2>&1

# Runs `kumar-asshole.sh` every 10 minutes.
*/10 * * * * /path/to/scripts/kumar-asshole.sh

# Runs `fucking-coffee.sh` hourly from 9am to 6pm on weekdays.
0 9-18 * * 1-5 /path/to/scripts/fucking-coffee.sh
```

---
授權是 WTFPL ( http://www.wtfpl.net/ ) 隨便你他媽怎麼改協議。
