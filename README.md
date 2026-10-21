# limani-proto

limani の public API contract を管理する repository です。

limani は、イベント単位・準備会単位のタスク管理サービスです。Todo は iCalendar（RFC 5545）の VTODO に対応します。
適切な権限を持つ別サービスとの連携用です。ConnectRPC の URL は private 実装と同一です（例: `/limani.v1.TodoService/ListTodos`）。

認証は kebab のアクセストークン（`Authorization: Bearer`）です。

## Packages

```text
limani.v1
```

`limani.v1` には `CalendarService`（カレンダーの参照・作成）と `TodoService`（Todo の参照・作成・更新・状態変更・削除）を含めます。
アプリパスワードなど画面専用の API は、limani の private proto にあり、ここには含めません。

## Layout

```text
limani/
  buf.gen.yaml
  limani/v1/*.proto
```

## ドキュメント

module 配下の `README.md` を `mise run docs` で生成します。

## 開発

```bash
mise run lint
mise run docs
mise run breaking
mise run check
```
