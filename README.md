# Identity-Aware Proxy(IAP)×GAEチュートリアル
## IAPとは？
- GAE等の前にGoogle認証をカンタンに挟むことが可能
## 実践
### デプロイ対象のコード(Python)の動作確認(省略可)
```
❯ pip install virtualenv
❯ git clone https://github.com/kawamou/iap-flask-sample.git
❯ cd cd iap-flask-sample
❯ virtualenv --python python3 ~/envs/iap-flask-sample
❯ source ~/envs/iap-flask-sample/bin/activate
❯ pip install -r requirements.txt
❯ python main.py
```
### GAEアプリ作成→デプロイ
```
# 現在のアカウント確認
❯ gcloud config list
# ログイン
❯ gcloud auth login
# アプリ作成
❯ gcloud app create
# デプロイ
❯ gcloud app deploy app.yaml \
    --project [YOUR_PROJECT_ID]
# 動作確認
❯ curl [YOUR_PROJECT_ID].appspot.com
```
### IAP設定
-  GCPコンソールに移動
- 「APIとサービス > OAuth同意画面」でGoogle認証の画面作成
- 「IAMと管理 > Identity-Aware Proxy」でIAPの設定
    - 作成したGAEにチェック→IAPをON
    - メンバーを追加→IAP-secured Web App Userのロールを設定 
- ブラウザから[YOUR_PROJECT_ID].appspot.comにアクセス
    - Google認証画面が立ち上がればOK(MFA等も設定済なら反映される)
### 参考
- コードはGCPのGAEチュートリアル(Python3.7)から
- IAPの設定
    - https://cloud.google.com/iap/docs/managing-access?hl=ja&_ga=2.47097647.-922872182.1586219953
