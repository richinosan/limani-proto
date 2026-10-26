# limani-proto

limani の public API contract を管理する repository です。

limani は、イベント単位・準備会単位のタスク管理サービスです。Todo は iCalendar（RFC 5545）の VTODO に対応します。
適切な権限を持つ別サービスとの連携用です。ConnectRPC の URL は private 実装と同一です（例: `/limani.v1.TodoService/ListTodos`）。

認証は kebab のアクセストークン（`Authorization: Bearer`）です。
ただし `TodoCompletionTicketService` だけは例外で、kebab のトークンは要らず、リクエストに入れる完了チケットの secret で認証します（利用者のいない無人の処理から呼ぶため）。

## Packages

```text
limani.v1
```

`limani.v1` には `CalendarService`（カレンダーの参照・作成）と `TodoService`（Todo の参照・作成・更新・状態変更・削除と、Todo をほかのカレンダーにも出すリンク（イベント間の同期）の参照・作成・削除と、Todo へのコメント（`TodoComment`。iCalendar・CalDAV には含まれない）の参照・作成・更新・削除・ピン留め（`PinTodoComment`・`UnpinTodoComment`。書き込み権限のあるメンバーが 1 つの Todo に 10 件まで留められる）と、ドキュメントの選択範囲へのレビューコメント（`TodoComment.anchor`。文書全体へのレビューコメントは `TodoComment.review`・返信 `reply_to`・スレッドの解決 `ResolveTodoComment`・`UnresolveTodoComment`）と、Todo の変更履歴（`TodoChangeHistory`。作った人・最後に更新した人と、変更のたびの変更後の状態。CalDAV からの更新も記録する）の参照と、完了チケット（`TodoCompletionTicket`）の発行）と `TodoCompletionTicketService`（完了チケットを引き換えて、Todo を完了報告つきで完了にする）を含めます。
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
