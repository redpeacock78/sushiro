# README

## 🍣What is 'sushiro'?🍣
このコマンド'sushiro'(以下sushiro)は回転寿司チェーン店"スシロー"のメニューをランダムに表示するコマンドです。

~~作ろうと思ったきっかけがこのツイート https://twitter.com/gamun/status/1068470182551597056 だなんて言えやしない…~~

## 🍣How to Install🍣
- ### Mac
    sushiroはHomebrewでのインストールができます。
    ```console
    $ brew tap redpeacock78/sushiro
    $ brew install sushiro
    ```
- ### Linux
    Linuxでは以下のようにすることをお勧めします。
    ```console
    $ git clone https://github.com/redpeacock78/sushiro
    $ cd "cloneしたディレクトリ"
    $ sudo install -m 0755 sushiro /usr/local/bin/sushiro
    ```
    なおアップデート方法は、
    ```console
    $ cd "cloneしたディレクトリ"
    $ git pull
    $ sudo install -m 0755 sushiro /usr/local/bin/sushiro
    ```
    をお勧めします。

## 🍣Overview of 'sushiro'🍣
susiroには以下のオプションがあります。
- ### -l [NUMBER]
    指定された数だけメニューをランダムに表示します。(デフォルトではランダムに一つ表示します。)
    ```console
    $ sushiro -l 
    たっぷりりんごのキャラメルパフェ
    
    $ sushiro -l 5
    天然えびの食べ比べ(生・漬け)
    炭焼き豚の蒲焼き
    手巻き納豆
    カニ風サラダ
    鯛だし塩ラーメン
    ```
- ### -p [MENU_NAME]
    指定された名前に対応するメニューのメニュー名と価格(外税表示)を表示します。(指定がなければ全てのメニューと価格を表示します。)
    ```console
    $ sushiro -p ぶり
    寒ぶり 100円+税
    大とろぶり 150円+税
    炙りぶりしゃぶ 150円+税
    ぶりの卵の炊いたんのせ 150円+税
    ```
- ### -k [MENU_NAME]
    指定された名前に対応するメニューのメニュー名とカロリー(kcal)を表示します。(指定がなければ全てのメニューとカロリーを表示します。)
    ```console
    $ sushiro -k ビール
    生ビール　グラス 100gあたり47kcal
    生ビール　ジョッキ 100gあたり47kcal
    ```
- ### -a
    全てのメニュー名を表示します。(全158種)
- ### -f
    www.akindo-sushiro.co.jp からメニューを取得します。(メニューは/usr/local/share/sushiro_cacheに保存されます,)

## 🍣How to play🍣
__基本的になんでもあり!!!!__
- 使用例
    - メニュー数が知りたい時
    ```console
    $ echo-sd --center スシローのメニューは$(grep "" -c <(sushiro -a))種類！
    ＿人人人人人人人人人人人人人人人人人＿
    ＞　スシローのメニューは158種類！ 　＜
    ￣Y^Y^Y^Y^Y^Y^Y^Y^Y^Y^Y^Y^Y^Y^Y^Y^Y^￣
    ```
    - 共食い願望
    ```console
    $ cowsay $(sushiro -a | grep 牛 | shuf -n 1)食べたい
     ______________________________________ 
    < 牛すき焼きにぎり食べたい >
     -------------------------------------- 
            \   ^__^
             \  (oo)\_______
                (__)\       )\/\
                    ||----w |
                    ||     ||
    ```
    - ランダムなメニューでnグラム
    ```console
    $ (i=$(sushiro -l);seq $[${#i}+1] | sed -z "s/[0-9]*\n/$i/g;s/\(.\{$[${#i}+1]\}\)/\1\n/g")
    軍艦ねぎまぐろ軍
    艦ねぎまぐろ軍艦
    ねぎまぐろ軍艦ね
    ぎまぐろ軍艦ねぎ
    まぐろ軍艦ねぎま
    ぐろ軍艦ねぎまぐ
    ろ軍艦ねぎまぐろ
    ```
    - リアルな牛に
    ```console
    $ sushiro -a | grep 牛 | sed "s/牛/$(emspect :ox: -f '%C')/g"
    🐂塩カルビ
    🐂すき焼きにぎり
    ```
    - "プリパラ"じゃなくて"将太の寿司"だった…？
    ```console
    $ rubipara episode 1 | sed "s/       .*$/    $(sushiro -l)/" 
    第01話	天然インド鮪7貫盛り
    ```
    - 1日の終わりに生ビールをジョッキで頼む小学生
    ```console
    $ rubipara kashikoma $(sushiro -a | grep 生 | grep '.........' | grep '　')
    
    
                     ／^v ＼
                   _{ / |-.(`_￣}__
            _人_  〃⌒ ﾝ'八{   ｀ノト､`ヽ
            `Ｙ´  {l／ / /    / Ｖﾉ } ﾉ    (     生ビール　ジョッキ      )
              ,-ｍ彡-ｧ Ｌﾒ､_彡ｲ } }＜く   O
             / _Uヽ⊂ﾆ{J:}  '⌒Ｖ  {  l| o
           ／  r‐='V(｢`¨,  r=≪,/ { .ﾉﾉ
          /   /_xヘ 人 丶-  _彡ｲ ∧〉
          (  ノ¨ﾌ’  ｀^> ‐ｧｧ ＜¨ﾌｲ
           --＝〉_丶/ﾉ { 彡' '|           Everyone loves Pripara!
               ^  '7^ O〉|’ ,丿
    ＿＿＿＿ ___ __ _{’O 乙,_r[_ __ ___ __________________________
    ```
    - 寿司なのかプリキュアなのか
    ```console
    $ cure echo -q | sed "s/キュア.*/キュア$(sushiro -l )！/"
    みんなの思いを守るために
    心をひとつに！
    思いよ届け！キュアいくら！
    ```
    - 一句読んでみた
    ```console
    $ echo-sd --tanzaku $(sushiro -l) 集めて早し 最上川 $(faker-cli -L ja -n lastName | sed 's/"//g')
    ┏━━━-┷-━━━┓
    ┃ 高　最　集　ホ ┃
    ┃ 橋　上　め　ッ ┃
    ┃　　 川　て　ト ┃
    ┃　　　　 早　コ ┃
    ┃　　　　 し　｜ ┃
    ┃　　　　　　 ヒ ┃
    ┃　　　　　　 ｜ ┃
    ┗━━━━━━━━┛
    ```
    - 松屋とコラボメニュー開発
    ```console
    $ yes "(sushiro -l;matsuya) | sed -z 's/\n//'" | head -n 5 | sh
    あん肝カルビ丼
    煮あなご肉カレーうどん（関西風だし）
    レモンサワープレミアムおろしポン酢牛焼肉膳
    生えびオリジナルハンバーグセット
    シーサラダ担々うどん（プレミアム牛肉使用）
    ```
    - 寿司屋の大将気分で
    ```console
    $ echo へいおまち！;echo-sd --center $(sushiro -l)
   へいおまち！
    ＿人人人人人人人＿
    ＞　炙り上穴子　＜
    ￣Y^Y^Y^Y^Y^Y^Y^￣
    ```
    - 名前がダジャレのメニュー
    ```console
    $ sushiro -a | dajarep -d 
    炙りぶりしゃぶ[ブリ]
    ```
     - スシローでわらしべ長者
    ```console
    $ echo-sd --stress $(sushiro -l 5)
    秋の贅沢　安納芋メルバ
           ↘
         えびバジルチーズ
            ↙
      えびかにみそ巻
            ↘
          活ほっき貝
            ↙
     ＿人人人人人人人人＿
     ＞　たこの唐揚げ　＜
     ￣Y^Y^Y^Y^Y^Y^Y^Y^￣
    ```
    - 松屋とダジャレコラボメニュー開発
    ```console
    $ yes "(sushiro -l;matsuya) | sed -z 's/\n//'" | head -n 100 | sh | dajarep -d
    活〆煮穴子一本にぎり肉きつねうどん　ミニプレミアム牛ミニうどん　ミニ生姜焼チゲカルビ丼セットセット[ショウ]
    いくら旨辛ネギたっぷりネギ塩豚バラ生姜焼定食[ショウ]
    活〆有頭大海老とろたまうどん（プレミアム牛肉使用）　ミニプレミアムキムチチゲカルビ焼定食セット[タマ]
    北海道ミルクレープたっぷりネギたっぷりネギ塩豚バラ生姜焼定食[ショウ]
    なんこつ唐揚げ鉄皿旨辛ネギたっぷりネギ塩豚カルビ焼膳（プレミアム牛肉使用）　ミニプレミアム膳　ミニライスセットセット[ショウ]
    熟成肉の炙りサーロイン肉カレーうどん生姜焼定食[ショウ]
    炙りぶりしゃぶキムチチゲカルビ焼定食[ブリ]
    ```
