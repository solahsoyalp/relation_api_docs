# APIドキュメント

このドキュメントでは、各APIの概要、エンドポイント、および認証方法について説明します。

## 目次
1. [認証](#認証)
2. [アクセス制限（レートリミット）](#アクセス制限レートリミット)
3. [文字コード](#文字コード)
4. [基本エンドポイント](#基本エンドポイント)
5. [エラーレスポンス](#エラーレスポンス)
6. [APIリスト](#apiリスト)
   - [コンタクト (customer)](#コンタクト-customer)
   - [アドレス帳 (customer_group)](#アドレス帳-customer_group)
   - [チケット (ticket)](#チケット-ticket)
   - [チャット](#チャット)
   - [受信箱 (message_box)](#受信箱-message_box)
   - [保留理由 (pending_reason)](#保留理由-pending_reason)
   - [ユーザー (user)](#ユーザー-user)
   - [チケット分類 (case_category)](#チケット分類-case_category)
   - [ラベル (label)](#ラベル-label)
   - [バッジ (badge)](#バッジ-badge)
   - [送信メール設定 (mail_account)](#送信メール設定-mail_account)
   - [メール (mail)](#メール-mail)
   - [テンプレート (template)](#テンプレート-template)
   - [コメント (comment)](#コメント-comment)
   - [添付ファイル](#添付ファイル)
   - [更新履歴](#更新履歴)

## 認証
すべてのAPIの利用にはアクセストークンが必要です。Re:lationのシステム設定画面からAPIトークンを発行し、リクエスト時に `Authorization` ヘッダに `Bearer <ACCESS_TOKEN>` をセットしてください。

```
curl \
  -H 'Authorization: Bearer <ACCESS_TOKEN>' \
  https://*.relationapp.jp/..
```

## アクセス制限（レートリミット）
API の利用には1分あたり60回のリクエスト制限があります。

| ヘッダ | 内容 |
|--------|------|
| X-RateLimit-Limit | 期間内（1分）でリクエストできる最大回数 |
| X-RateLimit-Remaining | アクセス可能な残り回数 |
| X-RateLimit-Reset | アクセス数がリセットされる時刻（UNIX時間） |

## 文字コード
リクエストおよびレスポンスの文字コードは `UTF-8` を使用します。

## 基本エンドポイント
APIの基本エンドポイントは以下の形式です。
```
https://<subdomain>.relationapp.jp/api/v2/<message_box_id>/
```
| パラメータ | 説明 |
|------------|------|
| subdomain | ご利用のサブドメイン |
| message_box_id | 受信箱ID（数字） |

## エラーレスポンス
| HTTP ステータスコード | エラー内容 |
|----------------|----------------------------------|
| 400 | パラメータに誤りがある |
| 401 | アクセストークンが存在しない、または無効 |
| 403 | レートリミットを超過 |
| 404 | リソースまたはエンドポイントが存在しない |
| 415 | 無効なフォーマット（Content-type に application/json が指定されていない） |
| 500 | サーバーエラー |
| 503 | メンテナンス中 |

## APIリスト

### [コンタクト (customer)](contact_api.md)
顧客情報の検索、登録、更新、削除を行います。

### [アドレス帳 (customer_group)](customer_group_api.md)
顧客グループの管理を行います。

### [チケット (ticket)](ticket_api.md)
サポートチケットの管理を行います。

### [チャット](chat_api.md)
チャットメッセージの取得を行います。

### [受信箱 (message_box)](message_box_api.md)
受信箱の管理を行います。

### [保留理由 (pending_reason)](pending_reason_api.md)
保留理由の取得を行います。

### [ユーザー (user)](user_api.md)
ユーザー情報の取得を行います。

### [チケット分類 (case_category)](case_category_api.md)
チケットの分類を管理します。

### [ラベル (label)](label_api.md)
ラベルを管理します。

### [バッジ (badge)](badge_api.md)
バッジ一覧取得

### [送信メール設定 (mail_account)](mail_account_api.md)
送信メール設定

### [メール (mail)](mail_api.md)
メール送信

### [テンプレート (template)](template_api.md)
テンプレート一覧取得
テンプレート検索

### [コメント (comment)](comment_api.md)
コメント

### [添付ファイル](attachment_api.md)
添付ファイルの取得を行います。

# 更新履歴

| 日付       | 変更内容 |
|------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 2022/12/22 | 送信メール設定一覧を取得できるようになりました。 |
| 2023/02/02 | チャネル項目に Yahoo!ショッピングを追加 |
| 2023/02/16 | アドレス帳ID版のコンタクト系API（登録・更新・削除・取得）を追加しました。<br>旧（受信箱ID版）API でパラメータ名にぶれがあったもの（`email_addresses` と `addresses`）を、上記アドレス帳ID版APIでは `emails` に統一しました。<br>アドレス帳ID版のバッジAPIを追加しました。 |
| 2023/03/30 | アドレス帳ID版のコンタクト系API（登録・更新・取得）に以下の項目を追加しました。<br>・アーカイブメールアドレス<br>・アーカイブ電話番号 |
| 2023/03/30 | 以下のAPIについて、「リソースまたはエンドポイントが存在しない」場合でも、ドキュメントと異なり、HTTP ステータスコード `404` ではなく `400` を返していたため、修正しました。<br>・更新 (`system_id1` をキーに)(アドレス帳ID版)<br>・更新 (`email` をキーに)(アドレス帳ID版)<br>・取得 (`system_id1` をキーに)(アドレス帳ID版)<br>・取得 (`email` をキーに)(アドレス帳ID版)<br>・削除 (`system_id1` をキーに)(アドレス帳ID版)<br>・削除 (`email` をキーに)(アドレス帳ID版) |
| 2023/09/01 | 以下のAPIを追加しました。<br>・チケットAPI（更新）<br>・メールAPI（送信・返信） |
| 2023/09/05 | 以下のAPIを廃止に伴い削除しました。<br>・旧（受信箱ID版）コンタクト系API（登録・更新・削除・取得）<br>・旧（受信箱ID版）バッジAPI（取得） |
| 2023/09/08 | テンプレート一覧取得APIを追加しました。 |
| 2023/09/15 | 以下のAPIに機能を追加しました。<br>・チケット検索の条件にラベルを追加<br>・チケット1件取得の結果にコメントと添付ファイルを追加<br>以下のAPIを追加しました。<br>・添付ファイルAPI（メッセージ添付ファイルダウンロードURL発行） |
| 2023/10/26 | 種別（チャネル）の記述に SMS、通話メモを追記しました。 |
| 2023/11/09 | テンプレート検索APIを追加しました。 |
| 2023/11/30 | ユーザー一覧取得APIに以下を追加しました。<br>・メールアドレス<br>・テナント管理者かどうか<br>・多要素認証が有効になっているかどうか<br>チケット分類一覧取得APIに「アーカイブされているかどうか」を追加しました。 |
| 2024/01/18 | ユーザー一覧取得APIに最終アクセス日時を追加しました。 |
| 2024/03/04 | 以下のAPIを追加しました。<br>・チケット分類登録・更新API<br>・ラベル登録・更新API<br>・コメント作成API<br>・アドレス帳一覧取得API<br>受信箱一覧取得APIのレスポンスに、アドレス帳IDを追加しました。 |
| 2024/04/11 | チケット更新APIのリクエストに、スヌーズ復帰時に通知するユーザのメンション名を追加しました。 |
| 2024/04/26 | チケット検索APIのレスポンスに「保留理由ID」を追加しました。<br>チケット1件取得APIのレスポンスに「保留理由ID」と「メールの `Reply-To:`」を追加しました。 |
| 2024/05/09 | チケット検索APIのリクエストに「保留理由ID」を追加しました。 |
| 2024/05/23 | ChatPlus、Yahoo!のチャット取得APIを追加しました。 |
| 2024/05/30 | R-Messe、Lineのチャット取得APIを追加しました。 |
| 2024/06/13 | 以下のAPIについて、リクエストに担当者のメンション名を追加しました。<br>・コンタクト登録<br>・コンタクト更新 (`system_id1` をキーに)<br>・コンタクト更新 (`email` をキーに) |
| 2024/06/27 | 応対メモ作成APIのリクエストの `operator` を必須項目から任意項目に変更しました。 |
| 2024/09/02 | メール下書き作成APIを追加しました。 |
| 2024/09/12 | コンタクト検索APIを追加しました。 |

---

## ライセンス
このドキュメントは [https://developer.ingage.jp/](https://developer.ingage.jp/) をマークダウンファイルに変更したものです。全ての権利は **株式会社インゲージ** に帰属します。

以上がAPIの概要です。詳細は各APIのエンドポイントを参照してください。

