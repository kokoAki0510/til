# インストール手順
## 1.公式からpython3.9をインストール
## 2.インストール先に移動
~ % cd /usr/local/bin
## 3.インストール先にpthon3がいることを確認
bin % ls -l
## 4.pipコマンド使うようにインストール
python3 -m pip install pillow
## 5.pipのバージョン古いと怒られたので、
書いてあったコマンドコピペ
bin % /Library/Frameworks/Python.framework/Versions/3.9/bin/python3 -m pip install --upgrade pip

## ライブラリインストール
pip install requests
一応いけるかな。
path設定していないけど・・・どうしようかなー

@MacBook-Pro ~ % which python
/usr/bin/python
@MacBook-Pro ~ % which python3
/Library/Frameworks/Python.framework/Versions/3.9/bin/python3

そんなに頻度高くなさそうだから、Homebrewは使わなかった。
同じ感じがあったから、
（めんどくさくなったら）いつかパス設定する
https://tipstour.net/python3-install-on-mac#bash_profilePython3

## バージョン確認
@MacBook-Pro testPy % python -V
Python 2.7.16
@MacBook-Pro testPy % python3 -V
Python 3.9.0

# seleniumインストールまで
## ①python3.9インストール済み
MacBook-Pro ~ % which python
/usr/bin/python
MacBook-Pro ~ % which python3
/Library/Frameworks/Python.framework/Versions/3.9/bin/python3
MacBook-Pro testPy % python -V
Python 2.7.16
MacBook-Pro testPy % python3 -V
Python 3.9.0
## ②seleniumのインストール
MacBook-Pro ~ % pip -V
pip 20.2.4 from /Library/Frameworks/Python.framework/Versions/3.9/lib/python3.9/site-packages/pip (python 3.9)
MacBook-Pro ~ % pip install selenium
Collecting selenium
・・・
Successfully installed selenium-3.141.0
## ③ドライバーのインストール（Mac用）
https://www.inet-solutions.jp/technology/python-selenium/
ここを参考に、GoogleのChrome用WebDriverのサイトから取得
## ④py書いて、対象フォルダまで行って実行するもエラー
【sample.py】
from selenium import webdriver
driver = webdriver.Chrome("/Users/aXXXXXXXX/driver/chromedriver.exe")
driver.get("http://www.yahoo.co.jp")
以下、ターミナル
MacBook-Pro AppWork % cd testPy
MacBook-Pro testPy % python3 sample.py
・・・
selenium.common.exceptions.WebDriverException: Message: 'chromedriver.exe' executable needs to be in PATH.
・・・
## ⑤exeが実行できるようにセキュリティ確認＆パスの記述変更
【sample.py（変更箇所のみ）】
driver = webdriver.Chrome(executable_path="/Users/aXXXXXXXX/driver/chromedriver")
→再度、実行！！　できた！