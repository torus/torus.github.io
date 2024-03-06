---
title: Google Cloud Storage、Eventarc、Cloud Run の連携
---

WIP

[Cloud Storage イベントを Cloud Run に転送する  \|  Eventarc  \|  Google Cloud](https://cloud.google.com/eventarc/docs/run/route-trigger-cloud-storage?hl=ja#console)

- （必要に応じて）サービスアカウントを作る
- サービスアカウントに対して鍵を追加する
- サービスアカウントに対して適切な権限を付与するために、自分のアカウントに IAM で `resourcemanager.projects.setIamPolicy` という権限を追加する。
- この権限は「Project IAM 管理者 (roles/resourcemanager.projectIamAdmin)」というロールに含まれるらしい。


BigQuery でサービスアカウントがテーブルを作るには「bigquery.tables.create」の権限が必要。
この権限は BigQuery のデータセットごとに設定する。

### Eventarc と連携しない場合

Eventarc と連携せずに Cloud Run を実行する場合は「サービス」ではなく「ジョブ」を使う。
ジョブが実行されるときは HTTP サーバが不要なので、直接必要な関数を実行すれば良い。

[ジョブの作成  \|  Cloud Run のドキュメント  \|  Google Cloud](https://cloud.google.com/run/docs/create-jobs?hl=ja)
