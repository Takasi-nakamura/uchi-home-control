# uchi — スマートホーム

GitHub Pagesで公開できる、Home Assistant連携の日本語PWAです。ホーム、デバイス、シーン、接続設定を独立した画面で切り替えられます。

## GitHub Pagesで公開

1. このフォルダーの中身をGitHubリポジトリのルートへ配置してpushします。
2. GitHubリポジトリの **Settings → Pages** を開きます。
3. **Build and deployment → Deploy from a branch** を選び、公開ブランチと `/ (root)` を指定して保存します。
4. 表示された `https://<ユーザー名>.github.io/<リポジトリ名>/` を開きます。

アセットとPWAのパスは相対指定なので、ユーザーサイトとプロジェクトサイトのどちらでも使えます。ビルド手順やNode.jsは不要です。

## Home Assistantに接続

1. Home AssistantをHTTPSでアクセスできるようにします。
2. Home Assistantのプロフィールで長期アクセストークンを発行します。
3. PWAの「接続・設定」にHome AssistantのHTTPS URLとトークンを入力します。
4. 初回接続後、デバイス一覧から電源や明るさ、エアコンの設定温度、カーテン、シーンを操作できます。

GitHub PagesとHome Assistantは別オリジンです。Home Assistantの `configuration.yaml` で公開サイトのオリジンをCORS許可してください。

```yaml
http:
  cors_allowed_origins:
    - https://<ユーザー名>.github.io
```

Home Assistantを再起動した後、接続し直します。ブラウザーからHTTPのHome Assistantへ接続すると、HTTPSページのセキュリティ制限でブロックされます。

## Google Homeと併用

Home Assistant CloudまたはGoogle Assistant連携を設定すると、連携した機器を「OK Google」対応端末とこのPWAの両方から操作できます。このPWA自体がGoogle Homeの認証やデバイス共有を行うわけではなく、Home Assistantが両者をつなぎます。

## 対応操作

- `light`: オン・オフ、明るさ調節
- `switch`、`fan`、`input_boolean`、`humidifier`: オン・オフ
- `climate`: 電源、目標温度
- `cover`: 開閉
- `lock`: 施錠・解錠、`vacuum`: 掃除開始・ドックへ戻す
- `scene`: シーンの実行
- デバイス検索、種類・部屋での絞り込み、お気に入り登録

接続URLとトークン、お気に入りは利用中のブラウザーのローカルストレージに保存されます。トークンはこの端末からHome Assistantの操作ができる強い認証情報です。個人用リポジトリに含めたり、スクリーンショットや共有端末に残さないでください。アプリのソースコードやGitHub Pagesには保存しません。

## ローカルで表示

```powershell
python -m http.server 4173
```

その後 `http://localhost:4173/` を開きます。PWAとしてインストールする場合はHTTPSで配信してください。
