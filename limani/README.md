# Protocol Documentation
<a name="top"></a>

## Table of Contents

- [limani/v1/calendar.proto](#limani_v1_calendar-proto)
    - [Calendar](#limani-v1-Calendar)
    - [CalendarCallerPermissions](#limani-v1-CalendarCallerPermissions)
  
- [limani/v1/calendar_api.proto](#limani_v1_calendar_api-proto)
    - [CreateCalendarRequest](#limani-v1-CreateCalendarRequest)
    - [GetCalendarRequest](#limani-v1-GetCalendarRequest)
    - [ListCalendarsRequest](#limani-v1-ListCalendarsRequest)
    - [ListCalendarsResponse](#limani-v1-ListCalendarsResponse)
  
- [limani/v1/todo.proto](#limani_v1_todo-proto)
    - [Todo](#limani-v1-Todo)
    - [TodoDateTime](#limani-v1-TodoDateTime)
  
    - [TodoStatus](#limani-v1-TodoStatus)
  
- [limani/v1/todo_api.proto](#limani_v1_todo_api-proto)
    - [CreateTodoRequest](#limani-v1-CreateTodoRequest)
    - [DeleteTodoRequest](#limani-v1-DeleteTodoRequest)
    - [GetTodoRequest](#limani-v1-GetTodoRequest)
    - [ListTodosRequest](#limani-v1-ListTodosRequest)
    - [ListTodosResponse](#limani-v1-ListTodosResponse)
    - [SetTodoStatusRequest](#limani-v1-SetTodoStatusRequest)
    - [UpdateTodoRequest](#limani-v1-UpdateTodoRequest)
  
- [limani/v1/todo_comment.proto](#limani_v1_todo_comment-proto)
    - [TodoComment](#limani-v1-TodoComment)
  
- [limani/v1/todo_comment_api.proto](#limani_v1_todo_comment_api-proto)
    - [CreateTodoCommentRequest](#limani-v1-CreateTodoCommentRequest)
    - [DeleteTodoCommentRequest](#limani-v1-DeleteTodoCommentRequest)
    - [ListTodoCommentsRequest](#limani-v1-ListTodoCommentsRequest)
    - [ListTodoCommentsResponse](#limani-v1-ListTodoCommentsResponse)
    - [UpdateTodoCommentRequest](#limani-v1-UpdateTodoCommentRequest)
  
- [limani/v1/todo_link.proto](#limani_v1_todo_link-proto)
    - [TodoLink](#limani-v1-TodoLink)
  
- [limani/v1/todo_link_api.proto](#limani_v1_todo_link_api-proto)
    - [CreateTodoLinkRequest](#limani-v1-CreateTodoLinkRequest)
    - [DeleteTodoLinkRequest](#limani-v1-DeleteTodoLinkRequest)
    - [ListTodoLinksRequest](#limani-v1-ListTodoLinksRequest)
    - [ListTodoLinksResponse](#limani-v1-ListTodoLinksResponse)
  
- [limani/v1/api.proto](#limani_v1_api-proto)
    - [CalendarService](#limani-v1-CalendarService)
    - [TodoService](#limani-v1-TodoService)
  
- [Scalar Value Types](#scalar-value-types)



<a name="limani_v1_calendar-proto"></a>
<p align="right"><a href="#top">Top</a></p>

## limani/v1/calendar.proto



<a name="limani-v1-Calendar"></a>

### Calendar
Calendar は Todo（VTODO）をまとめるカレンダー（タスクリスト）。
vitrina の準備会（organization）ごと、またはイベントごとに作る。


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| name | [string](#string) |  | リソース名（calendars/{id}）。 |
| scope | [string](#string) |  | 属する vitrina のリソース名（organizations/{id} または events/{id}）。 |
| display_name | [string](#string) |  | 表示名。 |
| color | [string](#string) |  | 表示色（#RRGGBB 形式）。未設定なら空。 |
| sync_token | [int64](#int64) |  | 書き込みのたびに増える連番。CalDAV の差分同期（RFC 6578）に使う。 |
| create_time | [google.protobuf.Timestamp](#google-protobuf-Timestamp) |  | 作成時刻。 |
| update_time | [google.protobuf.Timestamp](#google-protobuf-Timestamp) |  | 更新時刻。 |
| caller_permissions | [CalendarCallerPermissions](#limani-v1-CalendarCallerPermissions) |  | 呼び出し元がこのカレンダーに対して持つ権限。呼び出し側に依存する情報のため、 Calendar の一部としてキャッシュしてはならない。vitrina の Event.caller_permissions に対応する。 |






<a name="limani-v1-CalendarCallerPermissions"></a>

### CalendarCallerPermissions
CalendarCallerPermissions は、このカレンダーに対して呼び出し元（リクエストの認証主体）が
持つ権限を表す。権限は vitrina のロールで決まる（イベントのカレンダーはイベントの、
準備会のカレンダーは準備会の read / update 権限）。メンバーは Todo とカレンダーを読める。
can_update が false のメンバーは読むだけで、書き込み系の RPC は PERMISSION_DENIED になる。


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| can_update | [bool](#bool) |  | Todo の作成・更新・完了・削除、リンクの追加・解除ができるか （vitrina の event.update / organization.update に相当する権限を持つか）。 |





 

 

 

 



<a name="limani_v1_calendar_api-proto"></a>
<p align="right"><a href="#top">Top</a></p>

## limani/v1/calendar_api.proto



<a name="limani-v1-CreateCalendarRequest"></a>

### CreateCalendarRequest
CreateCalendarRequest はカレンダーを作る。呼び出し元が parent のメンバーで、かつ書き込み権限（event.update / organization.update 相当）を持つ必要がある。
読むだけのメンバーは PERMISSION_DENIED。


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| parent | [string](#string) |  | 親（organizations/{id} または events/{id}）。vitrina のリソース名。 |
| calendar | [Calendar](#limani-v1-Calendar) |  | 作るカレンダー。display_name は必須。name・scope・sync_token は無視する。 |






<a name="limani-v1-GetCalendarRequest"></a>

### GetCalendarRequest
GetCalendarRequest はカレンダーを取得する。
メンバーでない場合は NotFound を返す（存在を漏らさないため）。


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| name | [string](#string) |  | リソース名（calendars/{id}）。 |






<a name="limani-v1-ListCalendarsRequest"></a>

### ListCalendarsRequest
ListCalendarsRequest は呼び出し元がメンバーであるカレンダーを一覧する。

メンバーかどうかは vitrina の RoleAssignment で決まる。
準備会のカレンダーは、その準備会に何らかのロールを持つ人がメンバー。
イベントのカレンダーは、そのイベント、またはイベントを主催する準備会に
何らかのロールを持つ人がメンバー。


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| parent | [string](#string) |  | 絞り込み先の vitrina のリソース名（organizations/{id} または events/{id}）。 空なら絞り込まない。 |
| page_size | [int32](#int32) |  |  |
| page_token | [string](#string) |  |  |






<a name="limani-v1-ListCalendarsResponse"></a>

### ListCalendarsResponse



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| calendars | [Calendar](#limani-v1-Calendar) | repeated |  |
| next_page_token | [string](#string) |  |  |





 

 

 

 



<a name="limani_v1_todo-proto"></a>
<p align="right"><a href="#top">Top</a></p>

## limani/v1/todo.proto



<a name="limani-v1-Todo"></a>

### Todo
Todo は VTODO 1件。


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| name | [string](#string) |  | リソース名（calendars/{calendar}/todos/{todo}）。{todo} はサーバーが決める ID で、UID とは別。 UID は任意の文字列（URL や「/」を含むこともある）なので、リソース名には使わない。 {calendar} には、Todo が出ているカレンダー（TodoLink）のどれでも指定できる。 返す name は、問い合わせたカレンダーのもの（同じ Todo でも、カレンダーごとに name が違う）。 |
| uid | [string](#string) |  | iCalendar の UID。カレンダー内で一意（リンクされた Todo を含む）。作成時に省略するとサーバーが決める。 UID から Todo を探すときは ListTodos の uid で絞り込む。 |
| summary | [string](#string) |  | SUMMARY。必須。 |
| description | [string](#string) |  | DESCRIPTION。 |
| status | [TodoStatus](#limani-v1-TodoStatus) |  | STATUS。作成時に未指定なら NEEDS-ACTION。 |
| priority | [int32](#int32) |  | PRIORITY（0〜9。0 は未設定、1 が最も高い）。 |
| percent_complete | [int32](#int32) |  | PERCENT-COMPLETE（0〜100）。 |
| dtstart | [TodoDateTime](#limani-v1-TodoDateTime) |  | DTSTART。未設定なら省略。 |
| due | [TodoDateTime](#limani-v1-TodoDateTime) |  | DUE。未設定なら省略。dtstart より前にできず、dtstart と all_day をそろえる。 |
| completed_time | [google.protobuf.Timestamp](#google-protobuf-Timestamp) |  | COMPLETED。status が COMPLETED になると、未指定ならサーバーが現在時刻を入れる。 |
| categories | [string](#string) | repeated | CATEGORIES。 |
| parent_uid | [string](#string) |  | 親の Todo の UID（RELATED-TO;RELTYPE=PARENT）。 親は、書き込みに使ったカレンダーの中で UID から探す（Todo が出ているカレンダーごとに、親の Todo が出ているとは限らない。 親がそのカレンダーに出ていなければ、そのカレンダーからは親が見つからない）。 |
| assignees | [string](#string) | repeated | 担当者の kebab のユーザー ID（ATTENDEE として ics に出る）。 返すのは、Todo が出ているすべてのカレンダーのメンバーのうち、いまメンバーである人だけ。 |
| sequence | [int32](#int32) |  | SEQUENCE。更新のたびに増える。 |
| etag | [string](#string) |  | 楽観的排他制御のための値。CalDAV の ETag と同じ。 UpdateTodo で指定すると、保存されている値と違うときに ABORTED を返す。 |
| ics | [string](#string) |  | VCALENDAR 全文（RFC 5545）。 |
| create_time | [google.protobuf.Timestamp](#google-protobuf-Timestamp) |  | 作成時刻。 |
| update_time | [google.protobuf.Timestamp](#google-protobuf-Timestamp) |  | LAST-MODIFIED。 |
| calendars | [string](#string) | repeated | この Todo が出ているカレンダー（calendars/{id}）。1 つ以上ある。カレンダーの ID の昇順。 どのカレンダーで作った Todo かによる違いはない（Todo の同期は TodoLink で増減する）。 |






<a name="limani-v1-TodoDateTime"></a>

### TodoDateTime
TodoDateTime は DTSTART・DUE の値。日付（VALUE=DATE）と日時（VALUE=DATE-TIME）を区別する。


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| time | [google.protobuf.Timestamp](#google-protobuf-Timestamp) |  | all_day が false なら、その瞬間。 all_day が true なら、日付を UTC の 00:00:00 で表した値（例: 2026-11-03 は 2026-11-03T00:00:00Z）。 |
| all_day | [bool](#bool) |  | true なら日付のみ（VALUE=DATE）。tzid は使わない。 |
| tzid | [string](#string) |  | IANA のタイムゾーン名（例: Asia/Tokyo）。ics に TZID として出す。 空なら UTC（末尾が Z の日時）。all_day のときは無視する。 |





 


<a name="limani-v1-TodoStatus"></a>

### TodoStatus
TodoStatus は VTODO の STATUS（RFC 5545 3.8.1.11）。

| Name | Number | Description |
| ---- | ------ | ----------- |
| TODO_STATUS_UNSPECIFIED | 0 |  |
| TODO_STATUS_NEEDS_ACTION | 1 | NEEDS-ACTION |
| TODO_STATUS_IN_PROCESS | 2 | IN-PROCESS |
| TODO_STATUS_COMPLETED | 3 | COMPLETED |
| TODO_STATUS_CANCELLED | 4 | CANCELLED |


 

 

 



<a name="limani_v1_todo_api-proto"></a>
<p align="right"><a href="#top">Top</a></p>

## limani/v1/todo_api.proto



<a name="limani-v1-CreateTodoRequest"></a>

### CreateTodoRequest
CreateTodoRequest は Todo を作る。


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| parent | [string](#string) |  | 親（calendars/{id}）。 |
| todo | [Todo](#limani-v1-Todo) |  | 作る Todo。summary は必須。uid が空ならサーバーが決める。 name・sequence・etag・ics・create_time・update_time は無視する。 |






<a name="limani-v1-DeleteTodoRequest"></a>

### DeleteTodoRequest
DeleteTodoRequest は Todo を削除する。削除の記録（tombstone）を残す。

Todo が出ているすべてのカレンダーから消える（どのカレンダーのリソース名で指定しても同じ。
呼び出し元がそのカレンダーの書き込み権限を持つメンバーである必要がある）。
1 つのカレンダーから外すだけのときは DeleteTodoLink を使う。


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| name | [string](#string) |  | リソース名（calendars/{calendar}/todos/{todo}）。 |
| etag | [string](#string) |  | 指定すると、保存されている etag と違うときに ABORTED を返す。 |






<a name="limani-v1-GetTodoRequest"></a>

### GetTodoRequest
GetTodoRequest は Todo を取得する。


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| name | [string](#string) |  | リソース名（calendars/{calendar}/todos/{todo}）。 |






<a name="limani-v1-ListTodosRequest"></a>

### ListTodosRequest
ListTodosRequest はカレンダー内の Todo を一覧する。
TodoLink で同期されている Todo も含めて返す。


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| parent | [string](#string) |  | 親（calendars/{id}）。 |
| statuses | [TodoStatus](#limani-v1-TodoStatus) | repeated | 指定した status の Todo だけを返す。空なら絞り込まない。 |
| page_size | [int32](#int32) |  |  |
| page_token | [string](#string) |  |  |
| uid | [string](#string) |  | 指定した iCalendar の UID の Todo だけを返す（0件か1件）。空なら絞り込まない。 |






<a name="limani-v1-ListTodosResponse"></a>

### ListTodosResponse



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| todos | [Todo](#limani-v1-Todo) | repeated |  |
| next_page_token | [string](#string) |  |  |






<a name="limani-v1-SetTodoStatusRequest"></a>

### SetTodoStatusRequest
SetTodoStatusRequest は status だけを変える近道。

COMPLETED にすると completed_time に現在時刻を入れ、percent_complete を 100 にする。
COMPLETED から戻すと completed_time を消す。


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| name | [string](#string) |  | リソース名（calendars/{calendar}/todos/{todo}）。 |
| status | [TodoStatus](#limani-v1-TodoStatus) |  |  |
| etag | [string](#string) |  | 指定すると、保存されている etag と違うときに ABORTED を返す。 |






<a name="limani-v1-UpdateTodoRequest"></a>

### UpdateTodoRequest
UpdateTodoRequest は Todo を更新する。

todo.etag を指定すると、保存されている etag と違うときに ABORTED を返す。
空なら競合を検出しない。


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| todo | [Todo](#limani-v1-Todo) |  | 更新する Todo。name で対象を決める。Todo が出ているカレンダーのどの name でもよく、 どのカレンダーから更新しても、Todo が出ているすべてのカレンダーに反映される。 |
| update_mask | [google.protobuf.FieldMask](#google-protobuf-FieldMask) |  | 更新するフィールド。次のどれか: summary, description, status, priority, percent_complete, dtstart, due, completed_time, categories, parent_uid, assignees。 |





 

 

 

 



<a name="limani_v1_todo_comment-proto"></a>
<p align="right"><a href="#top">Top</a></p>

## limani/v1/todo_comment.proto



<a name="limani-v1-TodoComment"></a>

### TodoComment
TodoComment は、Todo に付けるコメント（GitHub の Issue のコメントのように、Todo について話し合うためのもの）。

コメントは Todo に属する。Todo と同じく、Todo が出ているすべてのカレンダー（TodoLink）で共有される
（どのカレンダーから書いても、Todo が出ているほかのカレンダーのメンバーに見える）。
Todo を削除すると、コメントもすべて消える。TodoLink を外してもコメントは消えない。

コメントは iCalendar（RFC 5545）には含まれない。Todo の ics・raw_ics には書かず、CalDAV にも出さない。
コメントを書く・直す・消すことで、Todo の etag・sequence・update_time、カレンダーの sync_token は変わらない。
CalDAV クライアントが書いた COMMENT プロパティは ics にそのまま残り、TodoComment とは無関係。


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| name | [string](#string) |  | リソース名（calendars/{calendar}/todos/{todo}/comments/{comment}）。{comment} はサーバーが決める ID。 {calendar}/{todo} には、Todo のリソース名と同じく、Todo が出ているカレンダーのどれでも指定できる。 返す name は、問い合わせたカレンダーのもの（同じコメントでも、カレンダーごとに name が違う）。 |
| body | [string](#string) |  | 本文（プレーンテキスト。改行を含められる）。 改行（CRLF・CR）は LF にそろえ、前後の空白・改行を取り除いて保存する。取り除いたあとが空なら INVALID_ARGUMENT。 必須で、10000 文字（Unicode のコードポイント）まで。制御文字（改行とタブを除く）は使えない。 |
| author | [string](#string) |  | 書いた人の kebab のユーザー ID（Todo.assignees と同じ形式）。 書いた人がカレンダーのメンバーから外れても、コメントは返る。 |
| author_display_name | [string](#string) |  | 書いた人の表示名。kebab のプロフィールの表示名（なければ username）を、書いた時刻（本文を直した時刻）に写したもの。 書いたときにプロフィールを取得できなかったときは空。直したときに取得できなかったときは、前の値のまま。 |
| author_image_url | [string](#string) |  | 書いた人のアイコンの URL。author_display_name と同じ時点の写し。ないときは空。 |
| create_time | [google.protobuf.Timestamp](#google-protobuf-Timestamp) |  | 作成時刻。 |
| update_time | [google.protobuf.Timestamp](#google-protobuf-Timestamp) |  | 本文を最後に直した時刻。直していなければ create_time と同じ。 |





 

 

 

 



<a name="limani_v1_todo_comment_api-proto"></a>
<p align="right"><a href="#top">Top</a></p>

## limani/v1/todo_comment_api.proto



<a name="limani-v1-CreateTodoCommentRequest"></a>

### CreateTodoCommentRequest
CreateTodoCommentRequest は、Todo にコメントを書く。

呼び出し元が parent のカレンダーのメンバーである必要がある。
1 つの Todo に付けられるコメントは 1000 件まで（超えると RESOURCE_EXHAUSTED）。


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| parent | [string](#string) |  | 親の Todo（calendars/{calendar}/todos/{todo}）。{calendar} は Todo が出ているカレンダーのどれでもよい。 |
| todo_comment | [TodoComment](#limani-v1-TodoComment) |  | 作るコメント。body は必須。name・author・author_display_name・author_image_url・create_time・update_time は無視する。 |






<a name="limani-v1-DeleteTodoCommentRequest"></a>

### DeleteTodoCommentRequest
DeleteTodoCommentRequest は、コメントを削除する（物理削除。記録は残さない）。

消せるのは書いた人だけ（それ以外のメンバーは PERMISSION_DENIED）。


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| name | [string](#string) |  | リソース名（calendars/{calendar}/todos/{todo}/comments/{comment}）。 |






<a name="limani-v1-ListTodoCommentsRequest"></a>

### ListTodoCommentsRequest
ListTodoCommentsRequest は、Todo のコメントを一覧する。

呼び出し元が parent のカレンダーのメンバーである必要がある。
書いた人がカレンダーのメンバーから外れていても、コメントは返る。


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| parent | [string](#string) |  | 親の Todo（calendars/{calendar}/todos/{todo}）。{calendar} は Todo が出ているカレンダーのどれでもよい。 |
| page_size | [int32](#int32) |  | 1 ページの件数。0 以下なら 50。200 を超える値は 200 にする。 |
| page_token | [string](#string) |  | 前の応答の next_page_token。空なら最初のページ。 |






<a name="limani-v1-ListTodoCommentsResponse"></a>

### ListTodoCommentsResponse



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| todo_comments | [TodoComment](#limani-v1-TodoComment) | repeated | 作成時刻の昇順（古いものが先。同じ時刻なら ID の昇順）。 |
| next_page_token | [string](#string) |  | 次のページがあるときの page_token。なければ空。 |






<a name="limani-v1-UpdateTodoCommentRequest"></a>

### UpdateTodoCommentRequest
UpdateTodoCommentRequest は、コメントの本文を直す。

直せるのは書いた人だけ（それ以外のメンバーは PERMISSION_DENIED）。


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| todo_comment | [TodoComment](#limani-v1-TodoComment) |  | 直すコメント。name で対象を決める。Todo が出ているカレンダーのどの name でもよい。 |
| update_mask | [google.protobuf.FieldMask](#google-protobuf-FieldMask) |  | 更新するフィールド。指定できるのは body だけ。空なら body を更新する。 |





 

 

 

 



<a name="limani_v1_todo_link-proto"></a>
<p align="right"><a href="#top">Top</a></p>

## limani/v1/todo_link.proto



<a name="limani-v1-TodoLink"></a>

### TodoLink
TodoLink は、Todo が表示されているカレンダーとの関係（イベント間の同期）。

Todo は 1 件だけ保存され、複数のカレンダーに出る（コピーはしない）。
どのカレンダーの一覧・CalDAV にも同じ Todo が出て、どのカレンダーから編集しても同じ Todo が更新される。
「持ち主のカレンダー」はない。Todo が出ているカレンダーは、すべて TodoLink で表される。
Todo を削除すると、すべてのカレンダーから消える。


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| name | [string](#string) |  | リソース名（calendars/{calendar}/todos/{todo}/links/{link}）。 {link} は表示先のカレンダーの ID（calendar の calendars/{id} の {id}）。 {calendar}/{todo} には、Todo のリソース名と同じく、Todo が出ているカレンダーのどれでも指定できる。 |
| calendar | [string](#string) |  | Todo を表示するカレンダー（calendars/{id}）。 |
| create_time | [google.protobuf.Timestamp](#google-protobuf-Timestamp) |  | Todo がこのカレンダーに出た時刻（Todo を作った時刻、またはリンクを作った時刻）。 |





 

 

 

 



<a name="limani_v1_todo_link_api-proto"></a>
<p align="right"><a href="#top">Top</a></p>

## limani/v1/todo_link_api.proto



<a name="limani-v1-CreateTodoLinkRequest"></a>

### CreateTodoLinkRequest
CreateTodoLinkRequest は、Todo をほかのカレンダーにもリンクする。

呼び出し元が、parent のカレンダーとリンク先のカレンダーの両方で書き込み権限を持つメンバーである必要がある。
リンク先のメンバーでなければ NOT_FOUND、書き込み権限がなければ PERMISSION_DENIED。
リンク先のカレンダーに同じ UID の Todo がすでにある場合と、Todo がすでにそのカレンダーに出ている場合は、
ALREADY_EXISTS を返す。
リンク先のカレンダーの CalDAV クライアントには、次の同期で Todo が現れる。


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| parent | [string](#string) |  | 親の Todo（calendars/{calendar}/todos/{todo}）。{calendar} は Todo が出ているカレンダーのどれでもよい。 |
| todo_link | [TodoLink](#limani-v1-TodoLink) |  | 作るリンク。calendar は必須（リンク先のカレンダー）。name・create_time は無視する。 |






<a name="limani-v1-DeleteTodoLinkRequest"></a>

### DeleteTodoLinkRequest
DeleteTodoLinkRequest は、Todo をカレンダーから外す（同期をやめる。リンクを削除する）。

呼び出し元が、name のカレンダー（{calendar}）と外すカレンダー（{link}）の両方で書き込み権限を持つメンバーである必要がある。
書き込み権限がなければ PERMISSION_DENIED。
外したカレンダーの CalDAV クライアントには、次の同期で Todo が削除として伝わる（削除の記録を残す）。
ほかのカレンダーには Todo が残る。Todo が出ているカレンダーが 1 つだけのときは外せない（FAILED_PRECONDITION）。
そのときは Todo を削除する。


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| name | [string](#string) |  | リソース名（calendars/{calendar}/todos/{todo}/links/{link}）。 |






<a name="limani-v1-ListTodoLinksRequest"></a>

### ListTodoLinksRequest
ListTodoLinksRequest は、Todo が出ているカレンダーを一覧する。
1 つの Todo は 50 のカレンダーまでなので、ページングはしない。

呼び出し元が parent のカレンダーのメンバーである必要がある。
ほかのカレンダーのメンバーでなくても、Todo が出ているカレンダーの ID は返る。


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| parent | [string](#string) |  | 親の Todo（calendars/{calendar}/todos/{todo}）。{calendar} は Todo が出ているカレンダーのどれでもよい。 |






<a name="limani-v1-ListTodoLinksResponse"></a>

### ListTodoLinksResponse



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| todo_links | [TodoLink](#limani-v1-TodoLink) | repeated | カレンダーの ID の昇順。 |





 

 

 

 



<a name="limani_v1_api-proto"></a>
<p align="right"><a href="#top">Top</a></p>

## limani/v1/api.proto


 

 

 


<a name="limani-v1-CalendarService"></a>

### CalendarService
CalendarService はカレンダー（タスクリスト）の API。
認証は kebab のアクセストークン（Authorization: Bearer）。

| Method Name | Request Type | Response Type | Description |
| ----------- | ------------ | ------------- | ------------|
| ListCalendars | [ListCalendarsRequest](#limani-v1-ListCalendarsRequest) | [ListCalendarsResponse](#limani-v1-ListCalendarsResponse) | 呼び出し元がメンバーであるカレンダーを一覧する。 |
| GetCalendar | [GetCalendarRequest](#limani-v1-GetCalendarRequest) | [Calendar](#limani-v1-Calendar) |  |
| CreateCalendar | [CreateCalendarRequest](#limani-v1-CreateCalendarRequest) | [Calendar](#limani-v1-Calendar) |  |


<a name="limani-v1-TodoService"></a>

### TodoService
TodoService は Todo（VTODO）の API。
認証は kebab のアクセストークン（Authorization: Bearer）。

| Method Name | Request Type | Response Type | Description |
| ----------- | ------------ | ------------- | ------------|
| ListTodos | [ListTodosRequest](#limani-v1-ListTodosRequest) | [ListTodosResponse](#limani-v1-ListTodosResponse) | カレンダーに出ている Todo を一覧する（TodoLink で同期されている Todo を含む）。 |
| GetTodo | [GetTodoRequest](#limani-v1-GetTodoRequest) | [Todo](#limani-v1-Todo) |  |
| CreateTodo | [CreateTodoRequest](#limani-v1-CreateTodoRequest) | [Todo](#limani-v1-Todo) |  |
| UpdateTodo | [UpdateTodoRequest](#limani-v1-UpdateTodoRequest) | [Todo](#limani-v1-Todo) |  |
| SetTodoStatus | [SetTodoStatusRequest](#limani-v1-SetTodoStatusRequest) | [Todo](#limani-v1-Todo) |  |
| DeleteTodo | [DeleteTodoRequest](#limani-v1-DeleteTodoRequest) | [.google.protobuf.Empty](#google-protobuf-Empty) | Todo を削除する。Todo が出ているすべてのカレンダーから消える（どのカレンダーのリソース名で呼んでも同じ）。 1 つのカレンダーから外すだけのときは DeleteTodoLink を使う。 |
| ListTodoLinks | [ListTodoLinksRequest](#limani-v1-ListTodoLinksRequest) | [ListTodoLinksResponse](#limani-v1-ListTodoLinksResponse) | Todo が出ているカレンダーを一覧する。 |
| CreateTodoLink | [CreateTodoLinkRequest](#limani-v1-CreateTodoLinkRequest) | [TodoLink](#limani-v1-TodoLink) | Todo をほかのカレンダーにもリンクする（イベント間の同期）。 |
| DeleteTodoLink | [DeleteTodoLinkRequest](#limani-v1-DeleteTodoLinkRequest) | [.google.protobuf.Empty](#google-protobuf-Empty) | Todo をカレンダーから外す（そのカレンダーとの同期をやめる）。最後の 1 つのカレンダーからは外せない。 |
| ListTodoComments | [ListTodoCommentsRequest](#limani-v1-ListTodoCommentsRequest) | [ListTodoCommentsResponse](#limani-v1-ListTodoCommentsResponse) | Todo のコメントを古い順に一覧する。コメントは Todo が出ているすべてのカレンダーで共有され、iCalendar・CalDAV には出ない。 |
| CreateTodoComment | [CreateTodoCommentRequest](#limani-v1-CreateTodoCommentRequest) | [TodoComment](#limani-v1-TodoComment) | Todo にコメントを書く。Todo の etag・sequence・update_time は変わらない。 |
| UpdateTodoComment | [UpdateTodoCommentRequest](#limani-v1-UpdateTodoCommentRequest) | [TodoComment](#limani-v1-TodoComment) | コメントの本文を直す。書いた人だけができる。 |
| DeleteTodoComment | [DeleteTodoCommentRequest](#limani-v1-DeleteTodoCommentRequest) | [.google.protobuf.Empty](#google-protobuf-Empty) | コメントを削除する。書いた人だけができる。 |

 



## Scalar Value Types

| .proto Type | Notes | C++ | Java | Python | Go | C# | PHP | Ruby |
| ----------- | ----- | --- | ---- | ------ | -- | -- | --- | ---- |
| <a name="double" /> double |  | double | double | float | float64 | double | float | Float |
| <a name="float" /> float |  | float | float | float | float32 | float | float | Float |
| <a name="int32" /> int32 | Uses variable-length encoding. Inefficient for encoding negative numbers – if your field is likely to have negative values, use sint32 instead. | int32 | int | int | int32 | int | integer | Bignum or Fixnum (as required) |
| <a name="int64" /> int64 | Uses variable-length encoding. Inefficient for encoding negative numbers – if your field is likely to have negative values, use sint64 instead. | int64 | long | int/long | int64 | long | integer/string | Bignum |
| <a name="uint32" /> uint32 | Uses variable-length encoding. | uint32 | int | int/long | uint32 | uint | integer | Bignum or Fixnum (as required) |
| <a name="uint64" /> uint64 | Uses variable-length encoding. | uint64 | long | int/long | uint64 | ulong | integer/string | Bignum or Fixnum (as required) |
| <a name="sint32" /> sint32 | Uses variable-length encoding. Signed int value. These more efficiently encode negative numbers than regular int32s. | int32 | int | int | int32 | int | integer | Bignum or Fixnum (as required) |
| <a name="sint64" /> sint64 | Uses variable-length encoding. Signed int value. These more efficiently encode negative numbers than regular int64s. | int64 | long | int/long | int64 | long | integer/string | Bignum |
| <a name="fixed32" /> fixed32 | Always four bytes. More efficient than uint32 if values are often greater than 2^28. | uint32 | int | int | uint32 | uint | integer | Bignum or Fixnum (as required) |
| <a name="fixed64" /> fixed64 | Always eight bytes. More efficient than uint64 if values are often greater than 2^56. | uint64 | long | int/long | uint64 | ulong | integer/string | Bignum |
| <a name="sfixed32" /> sfixed32 | Always four bytes. | int32 | int | int | int32 | int | integer | Bignum or Fixnum (as required) |
| <a name="sfixed64" /> sfixed64 | Always eight bytes. | int64 | long | int/long | int64 | long | integer/string | Bignum |
| <a name="bool" /> bool |  | bool | boolean | boolean | bool | bool | boolean | TrueClass/FalseClass |
| <a name="string" /> string | A string must always contain UTF-8 encoded or 7-bit ASCII text. | string | String | str/unicode | string | string | string | String (UTF-8) |
| <a name="bytes" /> bytes | May contain any arbitrary sequence of bytes. | string | ByteString | str | []byte | ByteString | string | String (ASCII-8BIT) |

