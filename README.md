## セキュアプログラミングについて

### セキュアプログラミングの定義
 - 「"確実"に正しく動作するコード」を指す（「攻撃されないコード」ではない）
 - 正しく動作することがセキュアプログラミングの目的（セキュアプログラミング = 脆弱性対策ではない）
 - リスク＝【情報資産】×【脅威】×【脆弱性】
   - リスクは損害が発生する可能性であり、損害の発生を抑えるためにリスクを低くしようとする。
   - この式の考え方では【情報資産】、【脅威】、【脆弱性】のどれかが無くなればリスク無いことになり、損害が発生することはないことになる。
   - 【脅威】への適切な対処は【情報資産】の性質により異なる。

### セキュアプログラミングの主な項目
セキュアプログラミングには様々な項目が存在するが、直近の業務でも関わりのあった3項目と開発時に意識するべき事柄について記載する。

#### 不正な値を入力させない（入力ミスとは異なる）
```
誤操作を安全に処理する。誤操作・誤動作による障害が発生した場合でも常に安全側に制御するというフェイルセーフな考え方をする。
必要ないものを排除するのではなく、必要なものを許すという判断を基本とする。
これは禁止を基本とすることで、明示的許可されない限りはデフォルトとしてサービスを拒否すべきというものである。
```
 - 入力値チェックを念入りに行う必要がある。
 - (ex)エスケープ、バリデーション等を適用し出力を無害化する
	- ユーザー入力のテキストボックスにバリデーションチェックを適用し、必要な値のみ入力を許容させる
   	- 処理で実行するクエリにユーザーが入力した値を直接使用させない、など
 - 設計、実装、テストなどどのフェーズでも意識する必要がある

#### 権限を分離する
```
可能であれば、1 つの鍵で保護する仕組みより 2 つの鍵を使って保護する方が強固だし柔軟でもある。
理想的には、アクセスは複数の条件に基づいて行うべきである。そうすれば、一つの防御メカニズムが破られても完全なアクセスを許すことはない。
多層防御（Defense in depth）や責務の分離（Separation of duty）につながる原則である。
```
 - (ex)公開鍵、秘密鍵の認証や多要素認証を用いる
	 - OTPの導入や生体認証も有効

#### 単純で小さな設計を心がける
```
仕組みを単純に。 システムは小さく単純明快に設計する。
「KISS」の原則" Keep it short and simple”または”keep it simple, stupid”である。
メカニズムが経済的であること。 システムは小さく単純に素直に設計すべきである。
大きく複雑なものは間違いやすく、それ故に経済的でなくなる。
```
 - (ex)複雑な機能について、いくつかの単純な機能に分割出来ないか検討する
	- 複雑な構造であるが故に想定外の挙動が起こり、それ自体が脆弱性となる可能性がある
	- 機能自体が必要なものであるかも検討する
 - (ex)ライブラリで実装可能なものは利用を検討する(※1)
	 - 利用しているツールやライブラリ等にも脆弱性のリスクが存在している可能性があるため、開発元や信頼出来るソースからインシデント情報などを確認すること。
	 - Log4jなどの幅広いプロジェクトで利用されているライブラリにも脆弱性は存在する。

## 参考
セキュアコーディング - JPCERT  
https://www.jpcert.or.jp/securecoding/  
IPA セキュア・プログラミング講座 - IPA  
https://www.ipa.go.jp/security/awareness/vendor/programming/
5分で解るセキュアコーディング - Yasuo Ohgaki  
https://www.slideshare.net/yohgaki/5-77628242  

(※1)  
Apache Log4jの任意のコード実行の脆弱性（CVE-2021-44228）に関する注意喚起 - JPCERT  
https://www.jpcert.or.jp/at/2021/at210050.html  
https://www.jpcert.or.jp/newsflash/2021122401.html  

