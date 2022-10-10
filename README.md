# Winget を導入する

## Winget とは

Winget とは、Microsoft 社が提供する純正のパッケージマネージャのこと。

通常、デスクトップアプリケーションのインストールは、インストーラを起動し、
インストーラの案内にしたがって、ボタンで順次、選択してインストール作業を進めていく。

対して、Winget は、コマンドを一度発行するだけで、アプリのインストール完了まで、すべて自動で行ってくれる。

そのため、インストール作業を早く行うことができ、手順の間違いも起きにくい。

## Winget のインストール

### Microsoft Store の起動

Windows キーを押して `microsoft store` で検索。Microsoft Store を起動する。

### 「アプリ インストーラ―」を入手

検索フォームに「app installer」と入力する。

![検索フォームに「app installer」と入力](./images/microsoft-store.png)

検索結果から、「アプリ インストーラー」を選択。

「入手」ボタンをクリックする。

### インストールできたかの確認

PowerShell を起動。次のコマンドを実行。

``` console
winget -v
```

`実行結果: `
``` console
v1.1.12653
```

## Winget の使い方

Winget は、アプリのインストールなどをスクリプトやバッチで一括して行う用途を想定しているため、コマンドラインで操作を行う。

Winget のコマンド書式は次の通り。

`winget.exe の書式`
``` console
winget ［＜サブコマンド＞］ ［＜サブコマンドオプション＞］
```

Winget は、引数を何も付けずに実行するとオンラインヘルプを表示する。サブコマンドが分からなくなったら、`winget` のみのコマンドを実行すればよい。

### Winget のサブコマンド

| サブコマンド  | 説明                                                   |
| :------------ | :----------------------------------------------------- |
| -v／--version | wingetのバージョンを表示                               |
| --info        | wingetの情報を表示                                     |
| install       | 指定されたパッケージをインストール                     |
| show          | パッケージに関する情報を表示                           |
| source        | パッケージのソースの管理                               |
| search        | アプリの基本情報を見つけて表示                         |
| list          | インストール済みパッケージを表示                       |
| upgrade       | 指定されたパッケージをアップグレード                   |
| uninstall     | 指定されたパッケージをアンインストール                 |
| hash          | インストーラーファイルをハッシュするヘルパー           |
| validate      | マニフェストファイルを検証                             |
| settings      | 設定（settings.josnファイル）を開く                    |
| features      | 試験的な機能の状態を表示                               |
| export        | インストールされているパッケージのリストをエクスポート |
| import        | ファイル中の全てのパッケージをインストール             |

### オプション指定について

`winget.exe` のサブコマンドは、それぞれ特有のオプション指定が必要になる。それをまとめると以下の表になる。

これらは、それぞれのサブコマンドで詳細な情報を指定するために使われる。
同じ意味を持つオプションは、原則同じオプションとなる。

例えば、パッケージ ID を指定する `--id` オプションは、`install` `show` `search` `list` `upgrade` の各サブコマンドで共通である。
サブコマンドの後ろにヘルプオプションを付けると、サブコマンドのオンラインヘルプが表示される。

#### winget.exe のサブコマンドとオプション

<table>
  <tr>
    <td id="null">サブコマンド</td>
    <td id="null">オプション</td>
    <td id="null">省略表記</td>
    <td id="null">動作</td>
  </tr>
  <tr>
    <td rowspan="15" id="null">install</td>
    <td id="null">--query 文字列</td>
    <td id="null">-q</td>
    <td id="null">ID、名前、モニカー（別名）、タグでの文字列部分一致検索（オプション省略可）</td>
  </tr>
  <tr>
    <td id="null">--manifest パス</td>
    <td id="null">-m</td>
    <td id="null">パッケージのマニフェストのパス</td>
  </tr>
  <tr>
    <td id="null">--id 文字列</td>
    <td id="null"></td>
    <td id="null">IDで結果をフィルター処理</td>
  </tr>
  <tr>
    <td id="null">--name 文字列</td>
    <td id="null"></td>
    <td id="null">名前で結果をフィルター処理</td>
  </tr>
  <tr>
    <td id="null">--moniker 文字列</td>
    <td id="null"></td>
    <td id="null">モニカーで結果をフィルター処理</td>
  </tr>
  <tr>
    <td id="null">--version バージョン</td>
    <td id="null">-v</td>
    <td id="null">指定されたバージョンを使用する。デフォルトは最新バージョン</td>
  </tr>
  <tr>
    <td id="null">--source winget|msstore</td>
    <td id="null">-s</td>
    <td id="null">指定されたソースを使用してパッケージを検索</td>
  </tr>
  <tr>
    <td id="null">--exact</td>
    <td id="null">-e</td>
    <td id="null">完全一致を使用してパッケージを検索</td>
  </tr>
  <tr>
    <td id="null">--interactive</td>
    <td id="null">-i</td>
    <td id="null">対話式のインストール（ユーザーの入力が必要になる場合がある）</td>
  </tr>
  <tr>
    <td id="null">--silent</td>
    <td id="null">-h</td>
    <td id="null">サイレントインストールを要求</td>
  </tr>
  <tr>
    <td id="null">--log＜パス＞</td>
    <td id="null">-o</td>
    <td id="null">ログの場所（サポートされている場合）</td>
  </tr>
  <tr>
    <td id="null">--override＜引数＞</td>
    <td id="null"></td>
    <td id="null">インストーラーに渡される引数を上書き</td>
  </tr>
  <tr>
    <td id="null">--location＜パス＞</td>
    <td id="null">-l</td>
    <td id="null">インストール先（サポートされている場合）</td>
  </tr>
  <tr>
    <td id="null">--force</td>
    <td id="null"></td>
    <td id="null">ハッシュのチェックがエラーでも強行</td>
  </tr>
  <tr>
    <td id="null">--help</td>
    <td id="null">-?</td>
    <td id="null">サブコマンドのヘルプ表示</td>
  </tr>
  <tr>
    <td rowspan="10" id="null">show</td>
    <td id="null">--query＜文字列＞</td>
    <td id="null">-q</td>
    <td id="null">ID、名前、モニカー、タグでの文字列部分一致検索（オプション省略可）</td>
  </tr>
  <tr>
    <td id="null">--manifest＜パス＞</td>
    <td id="null">-m</td>
    <td id="null">パッケージのマニフェストのパス</td>
  </tr>
  <tr>
    <td id="null">--id＜文字列＞</td>
    <td id="null"></td>
    <td id="null">ID で結果をフィルター処理</td>
  </tr>
  <tr>
    <td id="null">--name＜文字列＞</td>
    <td id="null"></td>
    <td id="null">名前で結果をフィルター処理</td>
  </tr>
  <tr>
    <td id="null">--moniker＜文字列＞</td>
    <td id="null"></td>
    <td id="null">モニカーで結果をフィルター処理</td>
  </tr>
  <tr>
    <td id="null">--version＜バージョン＞</td>
    <td id="null">-v</td>
    <td id="null">指定されたバージョンを使用する。デフォルトは最新バージョン</td>
  </tr>
  <tr>
    <td id="null">--source winget|msstore</td>
    <td id="null">-s</td>
    <td id="null">指定されたソースを使用してパッケージを検索</td>
  </tr>
  <tr>
    <td id="null">--exact</td>
    <td id="null">-e</td>
    <td id="null">完全一致を使用してパッケージを検索</td>
  </tr>
  <tr>
    <td id="null">--versions</td>
    <td id="null"></td>
    <td id="null">パッケージの利用可能なバージョンを表示</td>
  </tr>
  <tr>
    <td id="null">-?,--help</td>
    <td id="null"></td>
    <td id="null">サブコマンドのヘルプ表示</td>
  </tr>
  <tr>
    <td rowspan="6" id="null">source</td>
    <td id="null">add</td>
    <td id="null"></td>
    <td id="null">新しいソースを追加。オプションあり（詳細は-?で表示）</td>
  </tr>
  <tr>
    <td id="null">list</td>
    <td id="null"></td>
    <td id="null">現在のソースを一覧表示。オプションあり（詳細は-?で表示）</td>
  </tr>
  <tr>
    <td id="null">update</td>
    <td id="null"></td>
    <td id="null">現在のソースを更新。オプションあり（詳細は-?で表示）</td>
  </tr>
  <tr>
    <td id="null">remove</td>
    <td id="null"></td>
    <td id="null">現在のソースを削除。オプションあり（詳細は-?で表示）</td>
  </tr>
  <tr>
    <td id="null">reset</td>
    <td id="null"></td>
    <td id="null">ソースをリセット。オプションあり（詳細は-?で表示）</td>
  </tr>
  <tr>
    <td id="null">--help</td>
    <td id="null">-?</td>
    <td id="null">サブコマンドのヘルプ表示</td>
  </tr>
  <tr>
    <td rowspan="10" id="null">search</td>
    <td id="null">--query＜文字列＞</td>
    <td id="null">-q</td>
    <td id="null">ID、名前、モニカー、タグでの文字列部分一致検索（オプション省略可）</td>
  </tr>
  <tr>
    <td id="null">--id＜文字列＞</td>
    <td id="null"></td>
    <td id="null">IDで結果をフィルター処理</td>
  </tr>
  <tr>
    <td id="null">--name＜文字列＞</td>
    <td id="null"></td>
    <td id="null">名前で結果をフィルター処理</td>
  </tr>
  <tr>
    <td id="null">--moniker＜文字列＞</td>
    <td id="null"></td>
    <td id="null">モニカーで結果をフィルター処理</td>
  </tr>
  <tr>
    <td id="null">--tag＜文字列＞</td>
    <td id="null"></td>
    <td id="null">タグで結果をフィルター処理</td>
  </tr>
  <tr>
    <td id="null">--command</td>
    <td id="null"></td>
    <td id="null">コマンドによる結果のフィルター処理</td>
  </tr>
  <tr>
    <td id="null">--source winget|msstore</td>
    <td id="null">-s</td>
    <td id="null">指定されたソースを使用してパッケージを検索</td>
  </tr>
  <tr>
    <td id="null">--count＜数値＞</td>
    <td id="null">-n</td>
    <td id="null">指定した数以下の結果を表示</td>
  </tr>
  <tr>
    <td id="null">--exact</td>
    <td id="null">-e</td>
    <td id="null">完全一致を使用してパッケージを検索</td>
  </tr>
  <tr>
    <td id="null">--help</td>
    <td id="null">-?</td>
    <td id="null">サブコマンドのヘルプ表示</td>
  </tr>
  <tr>
    <td rowspan="10" id="null">list</td>
    <td id="null">--query＜文字列＞</td>
    <td id="null">-q</td>
    <td id="null">ID、名前、モニカー、タグでの文字列部分一致検索（オプション省略可）</td>
  </tr>
  <tr>
    <td id="null">--id＜文字列＞</td>
    <td id="null"></td>
    <td id="null">IDで結果をフィルター処理</td>
  </tr>
  <tr>
    <td id="null">--name＜文字列＞</td>
    <td id="null"></td>
    <td id="null">名前で結果をフィルター処理</td>
  </tr>
  <tr>
    <td id="null">--moniker＜文字列＞</td>
    <td id="null"></td>
    <td id="null">モニカーで結果をフィルター処理</td>
  </tr>
  <tr>
    <td id="null">--tag＜文字列＞</td>
    <td id="null"></td>
    <td id="null">タグで結果をフィルター処理</td>
  </tr>
  <tr>
    <td id="null">--command＜文字列＞</td>
    <td id="null"></td>
    <td id="null">コマンドによる結果のフィルター処理</td>
  </tr>
  <tr>
    <td id="null">--source winget|msstore</td>
    <td id="null">-s</td>
    <td id="null">指定されたソースを使用してパッケージを検索</td>
  </tr>
  <tr>
    <td id="null">--count＜数値＞</td>
    <td id="null">-n</td>
    <td id="null">指定した数以下の結果を表示</td>
  </tr>
  <tr>
    <td id="null">--exact</td>
    <td id="null">-e</td>
    <td id="null">完全一致を使用してパッケージを検索</td>
  </tr>
  <tr>
    <td id="null">--help</td>
    <td id="null">-?</td>
    <td id="null">サブコマンドのヘルプ表示</td>
  </tr>
  <tr>
    <td rowspan="16" id="null">upgrade</td>
    <td id="null">--query＜文字列＞</td>
    <td id="null">-q</td>
    <td id="null">ID、名前、モニカー、タグでの文字列部分一致検索（オプション省略可）</td>
  </tr>
  <tr>
    <td id="null">--manifest＜パス＞</td>
    <td id="null">-m</td>
    <td id="null">パッケージのマニフェストのパス</td>
  </tr>
  <tr>
    <td id="null">--id＜文字列＞</td>
    <td id="null"></td>
    <td id="null">IDで結果をフィルター処理</td>
  </tr>
  <tr>
    <td id="null">--name＜文字列＞</td>
    <td id="null"></td>
    <td id="null">名前で結果をフィルター処理</td>
  </tr>
  <tr>
    <td id="null">--moniker＜文字列＞</td>
    <td id="null"></td>
    <td id="null">モニカーで結果をフィルター処理</td>
  </tr>
  <tr>
    <td id="null">--version＜バージョン＞</td>
    <td id="null">-v</td>
    <td id="null">指定されたバージョンを使用する。デフォルトは最新バージョン</td>
  </tr>
  <tr>
    <td id="null">--source winget|msstore</td>
    <td id="null">-s</td>
    <td id="null">指定されたソースを使用してパッケージを検索</td>
  </tr>
  <tr>
    <td id="null">--exact</td>
    <td id="null">-e</td>
    <td id="null">完全一致を使用してパッケージを検索</td>
  </tr>
  <tr>
    <td id="null">--interactive</td>
    <td id="null">-i</td>
    <td id="null">対話式のインストール（ユーザーの入力が必要になる場合がある）</td>
  </tr>
  <tr>
    <td id="null">--silent</td>
    <td id="null">-h</td>
    <td id="null">サイレント インストールを要求</td>
  </tr>
  <tr>
    <td id="null">--log＜パス＞</td>
    <td id="null">-o</td>
    <td id="null">ログの場所 （サポートされている場合）</td>
  </tr>
  <tr>
    <td id="null">--override＜引数＞</td>
    <td id="null"></td>
    <td id="null">インストーラーに渡される引数を上書き</td>
  </tr>
  <tr>
    <td id="null">--location＜パス＞</td>
    <td id="null">-l</td>
    <td id="null">インストール先 （サポートされている場合）</td>
  </tr>
  <tr>
    <td id="null">--force</td>
    <td id="null"></td>
    <td id="null">ハッシュのチェックがエラーでも強行</td>
  </tr>
  <tr>
    <td id="null">--all</td>
    <td id="null"></td>
    <td id="null">インストール済みの全パッケージを最新版に更新する</td>
  </tr>
  <tr>
    <td id="null">--help</td>
    <td id="null">-?</td>
    <td id="null">サブコマンドのヘルプ表示</td>
  </tr>
  <tr>
    <td rowspan="3" id="null">hash</td>
    <td id="null">--file</td>
    <td id="null">-f</td>
    <td id="null">ハッシュするファイル</td>
  </tr>
  <tr>
    <td id="null">--msix</td>
    <td id="null">-m</td>
    <td id="null">入力ファイルをmsixとして扱う</td>
  </tr>
  <tr>
    <td id="null">--help</td>
    <td id="null">-?</td>
    <td id="null">サブコマンドのヘルプ表示</td>
  </tr>
  <tr>
    <td rowspan="2" id="null">validate</td>
    <td id="null">--manifest＜パス＞</td>
    <td id="null">-m</td>
    <td id="null">検証対象のマニフェストのパス</td>
  </tr>
  <tr>
    <td id="null">--help</td>
    <td id="null">-?</td>
    <td id="null">サブコマンドのヘルプ表示</td>
  </tr>
  <tr>
    <td id="null">settings</td>
    <td id="null">--help</td>
    <td id="null">-?</td>
    <td id="null">サブコマンドのヘルプ表示</td>
  </tr>
  <tr>
    <td id="null">features</td>
    <td id="null">--help</td>
    <td id="null">-?</td>
    <td id="null">サブコマンドのヘルプ表示</td>
  </tr>
  <tr>
    <td rowspan="2" id="null">experimental</td>
    <td id="null">--arg</td>
    <td id="null"></td>
    <td id="null">デモを目的とした試験的引数</td>
  </tr>
  <tr>
    <td id="null">--help</td>
    <td id="null">-?</td>
    <td id="null">サブコマンドのヘルプ表示</td>
  </tr>
</table>

## アプリの検索

``` console
winget search chrome
```

`実行結果: `
``` console
名前                       ID                         バージョン    一致            ソース
-------------------------------------------------------------------------------------------
Streamer to Chromecast     9MTTSZ74DBRS               Unknown                       msstore
Google Chrome              Google.Chrome              95.0.4638.69  Moniker: chrome winget
Google Chrome Dev          Google.Chrome.Dev          97.0.4681.0   Command: chrome winget
Google Chrome Beta         Google.Chrome.Beta         96.0.4664.35  Command: chrome winget
Stack                      stack.stack                3.32.0        Tag: chrome     winget
Brave                      BraveSoftware.BraveBrowser 95.1.31.88    Tag: Chrome     winget
Chrome Remote Desktop Host Google.ChromeRemoteDesktop 94.0.4606.27  Tag: chrome     winget
Ginger Chrome              Saxo_Broko.GingerChrome    93.0.4529.0                   winget
115浏览器                  115.115Chrome              25.0.0.3                      winget
360极速浏览器              360.360Chrome              13.0.2256.0                   winget
Chromium Installer         macchrome.winchrome        89.0.4389.114                 winget
Google Chrome Canary       Google.Chrome.Canary       97.0.4690.0                   winget
```

## アプリのインストール

``` console
winget install  -e --id Google.Chrome
```

## アプリのアンインストール

``` console
winget uninstall Google.Chrome
```

## インストールされているアプリの情報を取得

### 対象アプリを指定して

``` console
winget list chrome
```

`実行結果: `
``` console
名前          ID            バージョン   ソース
------------------------------------------------
Google Chrome Google.Chrome 95.0.4638.69 winget
```

### すべてのアプリを表示

``` console
winget list
```

## インストールされているアプリのエクスポート

``` console
winget export -o ./my-winget-packages.json
```

## JSON ファイルから指定アプリをインポート

``` console
winget import -i ./my-winget-packages.json
```

## インポート/エクスポートのファイル形式

``` json
{
	"$schema": "https://aka.ms/winget-packages.schema.2.0.json",
	"CreationDate": "2021-11-05T22:03:33.775-00:00",
	"Sources": [
		{
			"Packages": [
				{
					"PackageIdentifier": "Canonical.Ubuntu.2004"
				},
				{
					"PackageIdentifier": "Discord.Discord"
				},
				{
					"PackageIdentifier": "Docker.DockerDesktop"
				},
				{
					"PackageIdentifier": "Git.Git"
				},
				{
					"PackageIdentifier": "LINE.LINE"
				},
				{
					"PackageIdentifier": "Microsoft.WindowsTerminal"
				},
				{
					"PackageIdentifier": "WinMerge.WinMerge"
				},
				{
					"PackageIdentifier": "SlackTechnologies.Slack"
				},
				{
					"PackageIdentifier": "Zoom.Zoom"
				},
				{
					"PackageIdentifier": "Microsoft.OpenJDK.11"
				},
				{
					"PackageIdentifier": "Google.Chrome"
				}
			],
			"SourceDetails": {
				"Argument": "https://winget.azureedge.net/cache",
				"Identifier": "Microsoft.Winget.Source_8wekyb3d8bbwe",
				"Name": "winget",
				"Type": "Microsoft.PreIndexed.Package"
			}
		}
	],
	"WinGetVersion": "1.1.12653"
}
```
