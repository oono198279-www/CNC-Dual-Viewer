# CNC Dual Viewer

読み取り専用のCNCプログラム左右比較PWAです。MAIN/BACKの待合わせコードを検出し、対応行を自動整列します。外部CDNやCNCデータの送信処理は使用しません。

公開版: <https://oono198279-www.github.io/CNC-Dual-Viewer/>

> CNCプログラムはブラウザ内でのみ処理されます。ファイルへの書き込み機能や外部送信処理はありません。

## PWA

公開URLをEdge、Chrome、Safariで開き、ブラウザのインストール／ホーム画面追加機能から利用できます。インストール後はアプリシェルだけをキャッシュしてオフライン起動します。読み込んだCNCプログラム本文はCache StorageやlocalStorageへ保存しません。

Service Workerのキャッシュ対象は `index.html`、manifest、PWAアイコンだけです。更新時はキャッシュ名のバージョンが変わり、旧キャッシュを削除します。

## ローカル確認

File System Access APIによる更新まで確認する場合は、ローカルHTTPサーバー経由で開いてください。

```sh
python3 -m http.server 8000
```

EdgeまたはChromeで `http://localhost:8000/` を開き、`test-data/` の架空ファイルを使用します。実際の業務用プログラムは含まれていません。

## テストデータ

- `main-normal.nc` / `back-normal`: 正常照合、複数回コード、仮想行、末尾差
- `back-normal`: 拡張子なし、M5000部分一致防止
- `back-order-mismatch.prg`: 順序・コード不一致
- `back-count-mismatch.txt`: 件数不一致
- `shift-jis-sample.txt`: Shift_JIS（生成元は `shift-jis-source.txt`）
