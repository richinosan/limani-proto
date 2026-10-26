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
  
- [limani/v1/todo_attachment.proto](#limani_v1_todo_attachment-proto)
    - [TodoAttachment](#limani-v1-TodoAttachment)
  
- [limani/v1/todo_attachment_api.proto](#limani_v1_todo_attachment_api-proto)
    - [CreateTodoAttachmentRequest](#limani-v1-CreateTodoAttachmentRequest)
    - [DeleteTodoAttachmentRequest](#limani-v1-DeleteTodoAttachmentRequest)
    - [GetTodoAttachmentRequest](#limani-v1-GetTodoAttachmentRequest)
    - [ListTodoAttachmentsRequest](#limani-v1-ListTodoAttachmentsRequest)
    - [ListTodoAttachmentsResponse](#limani-v1-ListTodoAttachmentsResponse)
  
- [limani/v1/todo_change_history.proto](#limani_v1_todo_change_history-proto)
    - [TodoChangeHistory](#limani-v1-TodoChangeHistory)
  
    - [TodoChangeSource](#limani-v1-TodoChangeSource)
    - [TodoChangeType](#limani-v1-TodoChangeType)
  
- [limani/v1/todo_change_history_api.proto](#limani_v1_todo_change_history_api-proto)
    - [ListTodoChangeHistoriesRequest](#limani-v1-ListTodoChangeHistoriesRequest)
    - [ListTodoChangeHistoriesResponse](#limani-v1-ListTodoChangeHistoriesResponse)
  
- [limani/v1/todo_comment.proto](#limani_v1_todo_comment-proto)
    - [TodoComment](#limani-v1-TodoComment)
    - [TodoCommentAnchor](#limani-v1-TodoCommentAnchor)
  
- [limani/v1/todo_comment_api.proto](#limani_v1_todo_comment_api-proto)
    - [CreateTodoCommentRequest](#limani-v1-CreateTodoCommentRequest)
    - [DeleteTodoCommentRequest](#limani-v1-DeleteTodoCommentRequest)
    - [ListTodoCommentsRequest](#limani-v1-ListTodoCommentsRequest)
    - [ListTodoCommentsResponse](#limani-v1-ListTodoCommentsResponse)
    - [PinTodoCommentRequest](#limani-v1-PinTodoCommentRequest)
    - [ResolveTodoCommentRequest](#limani-v1-ResolveTodoCommentRequest)
    - [UnpinTodoCommentRequest](#limani-v1-UnpinTodoCommentRequest)
    - [UnresolveTodoCommentRequest](#limani-v1-UnresolveTodoCommentRequest)
    - [UpdateTodoCommentRequest](#limani-v1-UpdateTodoCommentRequest)
  
- [limani/v1/todo_completion_ticket.proto](#limani_v1_todo_completion_ticket-proto)
    - [TodoCompletionTicket](#limani-v1-TodoCompletionTicket)
  
- [limani/v1/todo_completion_ticket_api.proto](#limani_v1_todo_completion_ticket_api-proto)
    - [CreateTodoCompletionTicketRequest](#limani-v1-CreateTodoCompletionTicketRequest)
    - [RedeemTodoCompletionTicketRequest](#limani-v1-RedeemTodoCompletionTicketRequest)
  
- [limani/v1/todo_link.proto](#limani_v1_todo_link-proto)
    - [TodoLink](#limani-v1-TodoLink)
  
- [limani/v1/todo_link_api.proto](#limani_v1_todo_link_api-proto)
    - [CreateTodoLinkRequest](#limani-v1-CreateTodoLinkRequest)
    - [DeleteTodoLinkRequest](#limani-v1-DeleteTodoLinkRequest)
    - [ListTodoLinksRequest](#limani-v1-ListTodoLinksRequest)
    - [ListTodoLinksResponse](#limani-v1-ListTodoLinksResponse)
  
- [limani/v1/api.proto](#limani_v1_api-proto)
    - [CalendarService](#limani-v1-CalendarService)
    - [TodoCompletionTicketService](#limani-v1-TodoCompletionTicketService)
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
| assignees | [string](#string) | repeated | 担当者の kebab のユーザー ID（ATTENDEE として ics に出る）。 返すのは、Todo が出ているすべてのカレンダーのメンバーのうち、いまメンバーである人だけ。 書き込み権限のない（閲覧のみの）メンバーも、UpdateTodo の update_mask に assignees だけを指定して、自分自身を担当者に足す・外すことはできる （ほかの人を足したり外したりすると PERMISSION_DENIED。UpdateTodoRequest の「閲覧のみのメンバーの自己申告」を参照）。 |
| sequence | [int32](#int32) |  | SEQUENCE。更新のたびに増える。 |
| etag | [string](#string) |  | 楽観的排他制御のための値。CalDAV の ETag と同じ。 UpdateTodo で指定すると、保存されている値と違うときに ABORTED を返す。 |
| ics | [string](#string) |  | VCALENDAR 全文（RFC 5545）。 |
| create_time | [google.protobuf.Timestamp](#google-protobuf-Timestamp) |  | 作成時刻。 |
| update_time | [google.protobuf.Timestamp](#google-protobuf-Timestamp) |  | LAST-MODIFIED。 |
| calendars | [string](#string) | repeated | この Todo が出ているカレンダー（calendars/{id}）。1 つ以上ある。カレンダーの ID の昇順。 どのカレンダーで作った Todo かによる違いはない（Todo の同期は TodoLink で増減する）。 |
| creator | [string](#string) |  | 作った人の kebab のユーザー ID（TodoComment.author と同じ形式）。 CalDAV で作った Todo は、アプリパスワードの持ち主。作った人がカレンダーのメンバーから外れていても返る。 表示名・アイコンは返さない。kebab の GetUser で引くこと。 |
| last_updater | [string](#string) |  | 最後に更新した人の kebab のユーザー ID（creator と同じ形式）。 UpdateTodo・SetTodoStatus・状態つきの CreateTodoComment・CalDAV の PUT で、中身（summary・description・status・priority・ percent_complete・dtstart・due・completed_time・categories・parent_uid・assignees・completed_assignees）が実際に変わったときだけ更新する （DTSTAMP・SEQUENCE だけが変わる再送では変わらない）。一度も更新されていなければ creator と同じ。 TodoChangeHistory の actor と対応する。 |
| completed_assignees | [string](#string) | repeated | 自分の分を完了にした担当者の kebab のユーザー ID（assignees の部分集合）。 担当者ごとの完了は、担当者それぞれの作業が終わったかを表す。assignees が 2 人以上いるとき、全員の分が完了になるまで status は COMPLETED にならない（全員の分がそろった時点で COMPLETED になる）。 担当者の分が完了なのは、その人が自分の分を完了にしたとき、または status が COMPLETED のとき （COMPLETED の Todo では assignees の全員が入る）。 assignees が 1 人以下のときは status に一致する（1 人なら、その人の分の完了 = Todo の完了）。 UpdateTodo の update_mask に completed_assignees を指定すると書ける（assignees にない人を含めると INVALID_ARGUMENT）。 書き込み権限のない（閲覧のみの）メンバーも、自分が担当者なら、自分の分だけは完了にする・取り消すことができる（UpdateTodoRequest を参照）。 |






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

担当者ごとの完了: Todo.assignees が 2 人以上いるとき、呼び出した人（行為者）によって意味が変わる。
UpdateTodo の status、状態つきの CreateTodoComment、RedeemTodoCompletionTicket（行為者は発行者）、CalDAV の PUT も同じ規則になる。

1. COMPLETED にする:
   - 担当者がいない: Todo を COMPLETED にする。
   - 行為者が担当者の一人: 行為者の分だけを完了にする（completed_assignees に入れる）。全員の分がそろえば Todo を
     COMPLETED にする（上の completed_time と percent_complete）。そろわなければ status は COMPLETED にならず、
     NEEDS_ACTION なら IN_PROCESS になる（応答の status は IN_PROCESS）。
   - 行為者が担当者でない: 管理者の操作とみなし、全員の分を完了にして Todo を COMPLETED にする。
2. COMPLETED から戻す:
   - 行為者が担当者の一人: 行為者の分だけを未完了に戻す。ほかの人の分は完了のまま。
   - 行為者が担当者でない: 全員の分を未完了に戻す。

担当者が 1 人だけの Todo は、その人の分の完了が Todo の完了になる（従来と同じ）。

閲覧のみのメンバーの自己申告: Todo の書き込み権限が要るが、書き込み権限のない（閲覧のみの）メンバーも、その Todo の担当者なら、
自分の分だけを完了にする（COMPLETED）・取り消す（COMPLETED から戻す。自分の分が完了しているとき）ことができる。
自分の分が最後なら Todo は COMPLETED になる。担当者でない、中止（CANCELLED）にする、自分の分の完了と関係なく Todo の状態だけを変える、
ほかの人の分が変わるときは PERMISSION_DENIED（何も変わらない）。状態つきの CreateTodoComment も同じ規則になる。


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
| update_mask | [google.protobuf.FieldMask](#google-protobuf-FieldMask) |  | 更新するフィールド。次のどれか: summary, description, status, priority, percent_complete, dtstart, due, completed_time, categories, parent_uid, assignees, completed_assignees。

completed_assignees は、担当者ごとの完了を直接書く。書き込み権限があれば、誰の分でも書ける （書き込み権限のない閲覧のみのメンバーは、自分が担当者のとき、自分の分だけ。下の「閲覧のみのメンバーの自己申告」） （assignees にない人を含めると INVALID_ARGUMENT。同じリクエストで assignees も変えるなら、変えたあとの assignees で確かめる）。 書いた結果、担当者の全員の分が完了になれば、Todo の status は COMPLETED になる （completed_time を入れ、percent_complete を 100 にする）。完了していない人が残っていれば、 COMPLETED だった Todo は IN_PROCESS に戻り（completed_time を消す）、NEEDS_ACTION だった Todo は IN_PROCESS になる。 status と同時に指定したときは、status の意味（「完了にする操作の行為者」の規則）より completed_assignees を優先する。

status を COMPLETED にしたときの意味は、SetTodoStatus の「担当者ごとの完了」を参照。

閲覧のみのメンバーの自己申告: 書き込み権限のない（閲覧のみの）メンバーが更新できるのは、次の 2 つだけ。 それ以外のフィールドを update_mask に含める、または ほかの人の担当者・ほかの人の分の完了を変えると PERMISSION_DENIED （書き込み権限のあるメンバーは、これまでどおり全部できる）。 - assignees: 自分自身を担当者に足す、または外す（今の担当者との差が自分だけ）。足すときの ATTENDEE の扱いは、書き込み権限のある人が足すときと同じ。 外すと、自分の分の完了も消える。外した結果、残る担当者の全員の分が完了していれば、Todo は COMPLETED になる（導かれる結果）。 - completed_assignees: 自分が担当者のとき、自分の分の完了にする・取り消す（今の完了している担当者との差が自分だけ）。 自分の分が最後なら Todo は COMPLETED になる（導かれる結果）。 同じリクエストに assignees と completed_assignees の両方を指定してもよい（どちらも自分の分だけに限られる）。 |





 

 

 

 



<a name="limani_v1_todo_attachment-proto"></a>
<p align="right"><a href="#top">Top</a></p>

## limani/v1/todo_attachment.proto



<a name="limani-v1-TodoAttachment"></a>

### TodoAttachment
TodoAttachment は、Todo に添付したファイル（コメントや説明に貼る画像、成果物など）。

添付は Todo に属する。Todo と同じく、Todo が出ているすべてのカレンダー（TodoLink）で共有される
（どのカレンダーから添付しても、Todo が出ているほかのカレンダーのメンバーに見える）。
Todo を削除すると、添付もすべて消える。TodoLink を外しても添付は消えない。

添付は iCalendar（RFC 5545）には含まれない。Todo の ics・raw_ics に ATTACH は書かず、CalDAV にも出さない。
添付を追加・削除することで、Todo の etag・sequence・update_time、カレンダーの sync_token は変わらない。

説明（Todo.description）やコメントの Markdown からは url で参照する。
中身は公開しない。読めるのは、メンバーに返した期限付きの署名付き URL（download_uri）だけ。


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| name | [string](#string) |  | リソース名（calendars/{calendar}/todos/{todo}/attachments/{attachment}）。{attachment} はサーバーが決める ULID。 {calendar}/{todo} には、Todo のリソース名と同じく、Todo が出ているカレンダーのどれでも指定できる。 返す name は、問い合わせたカレンダーのもの（同じ添付でも、カレンダーごとに name が違う）。 GetTodoAttachment では {calendar} に &#34;-&#34; を指定できる。Todo が出ているカレンダーのどれかのメンバーなら読める。 |
| filename | [string](#string) |  | ファイル名。必須で、255 文字（Unicode のコードポイント）まで。 制御文字・&#34;/&#34;・&#34;\&#34; は使えない（INVALID_ARGUMENT）。 |
| content_type | [string](#string) |  | MIME タイプ（小文字、パラメーターなし）。空なら application/octet-stream。 大文字は小文字にし、&#34;;&#34; 以降のパラメーターは取り除く。type/subtype の形でなければ application/octet-stream として保存する。 画像（image/png・image/jpeg・image/gif・image/webp）は、中身の先頭のバイトがその形式と合わなければ application/octet-stream として保存する。 |
| size_bytes | [int64](#int64) |  | ファイルの大きさ（バイト）。 |
| uploader | [string](#string) |  | アップロードした人の kebab のユーザー ID（Todo.assignees と同じ形式）。 アップロードした人がカレンダーのメンバーから外れても、添付は返る。 |
| create_time | [google.protobuf.Timestamp](#google-protobuf-Timestamp) |  | アップロードした時刻。 |
| url | [string](#string) |  | Markdown に書く URL（{APP_ORIGIN}/admin/attachments/{todo}/{attachment}）。 ログインが必要な limani の画面の URL で、画面はこの URL の添付を GetTodoAttachment で引き、download_uri で表示する。 {todo}・{attachment} はリソース名の Todo と添付の ID で、カレンダーによらず同じ。この URL では中身は読めない。 |
| download_uri | [string](#string) |  | 中身を読む、期限付きの署名付き URL（{APP_ORIGIN}/files/todos/{todo}/attachments/{attachment}?exp=...&amp;sig=...）。 ログイン（Bearer）なしで GET でき、署名と期限が合わなければ 403、添付が削除されていれば 404。 画像（image/png・image/jpeg・image/gif・image/webp）は inline、それ以外は application/octet-stream の attachment（ダウンロード）として返す。 同じ期間（15 分ごと）の中では同じ URL を返す（ブラウザのキャッシュが効く）。期限が過ぎたら、取り直す。 |
| download_expire_time | [google.protobuf.Timestamp](#google-protobuf-Timestamp) |  | download_uri の期限。発行から 15〜30 分後。 |





 

 

 

 



<a name="limani_v1_todo_attachment_api-proto"></a>
<p align="right"><a href="#top">Top</a></p>

## limani/v1/todo_attachment_api.proto



<a name="limani-v1-CreateTodoAttachmentRequest"></a>

### CreateTodoAttachmentRequest
CreateTodoAttachmentRequest は、Todo にファイルを添付する。

呼び出し元が parent のカレンダーのメンバーである必要がある（vitrina のロールが読み取りだけの人もできる。Todo の書き込み権限とは別）。
1 つの Todo に付けられる添付は 500 件まで（超えると RESOURCE_EXHAUSTED）。


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| parent | [string](#string) |  | 親の Todo（calendars/{calendar}/todos/{todo}）。{calendar} は Todo が出ているカレンダーのどれでもよい。 |
| todo_attachment | [TodoAttachment](#limani-v1-TodoAttachment) |  | 作る添付。filename は必須。content_type は任意。name・size_bytes・uploader・create_time・url は無視する。 |
| data | [bytes](#bytes) |  | ファイルの中身。1 バイト以上 10 MiB（10485760 バイト）まで（空・超過は INVALID_ARGUMENT）。 |






<a name="limani-v1-DeleteTodoAttachmentRequest"></a>

### DeleteTodoAttachmentRequest
DeleteTodoAttachmentRequest は、添付を削除する（物理削除。記録は残さない）。

消せるのはアップロードした人だけ（それ以外のメンバーは PERMISSION_DENIED）。
その添付を Markdown で参照している説明・コメントは、壊れた添付の表示になる。


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| name | [string](#string) |  | リソース名（calendars/{calendar}/todos/{todo}/attachments/{attachment}）。 |






<a name="limani-v1-GetTodoAttachmentRequest"></a>

### GetTodoAttachmentRequest
GetTodoAttachmentRequest は、添付を取得する（中身は download_uri から読む）。

呼び出し元が、Todo が出ているカレンダーのメンバーである必要がある。


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| name | [string](#string) |  | リソース名（calendars/{calendar}/todos/{todo}/attachments/{attachment}）。 {calendar} は Todo が出ているカレンダーのどれでもよい。&#34;-&#34; を指定すると、 Todo が出ているカレンダーのどれかのメンバーであれば読める（画面の URL は {calendar} を持たないため）。 &#34;-&#34; のときに返す name も &#34;-&#34; のまま。 |






<a name="limani-v1-ListTodoAttachmentsRequest"></a>

### ListTodoAttachmentsRequest
ListTodoAttachmentsRequest は、Todo の添付を一覧する（中身は含まない）。

呼び出し元が parent のカレンダーのメンバーである必要がある。
アップロードした人がカレンダーのメンバーから外れていても、添付は返る。


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| parent | [string](#string) |  | 親の Todo（calendars/{calendar}/todos/{todo}）。{calendar} は Todo が出ているカレンダーのどれでもよい。 |
| page_size | [int32](#int32) |  | 1 ページの件数。0 以下なら 50。200 を超える値は 200 にする。 |
| page_token | [string](#string) |  | 前の応答の next_page_token。空なら最初のページ。 |






<a name="limani-v1-ListTodoAttachmentsResponse"></a>

### ListTodoAttachmentsResponse



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| todo_attachments | [TodoAttachment](#limani-v1-TodoAttachment) | repeated | アップロード時刻の昇順（古いものが先。同じ時刻なら ID の昇順）。 |
| next_page_token | [string](#string) |  | 次のページがあるときの page_token。なければ空。 |





 

 

 

 



<a name="limani_v1_todo_change_history-proto"></a>
<p align="right"><a href="#top">Top</a></p>

## limani/v1/todo_change_history.proto



<a name="limani-v1-TodoChangeHistory"></a>

### TodoChangeHistory
TodoChangeHistory は、Todo の変更履歴の 1 件（変更のたびに、変更後の状態を丸ごと残す）。

履歴は Todo に属する。Todo と同じく、Todo が出ているすべてのカレンダー（TodoLink）で共有される。
Todo を削除すると、履歴もすべて消える（削除は履歴に残さない）。TodoLink の作成・削除は履歴に残さない。
コメント（TodoComment）・添付（TodoAttachment）の追加や削除も履歴に残さない。

中身（summary・description・status・priority・percent_complete・dtstart・due・completed_time・categories・
parent_uid・assignees・completed_assignees）が変わらない更新は、記録しない（CalDAV クライアントが DTSTAMP・SEQUENCE だけを変えて
PUT し直しても、履歴は増えない）。
変更の内容は、隣り合う履歴の snapshot を比べて求める（サーバーは差分を持たない）。
履歴を残し始める前に作られた Todo は、最も古い履歴が CREATE ではなく UPDATE になる。


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| name | [string](#string) |  | リソース名（calendars/{calendar}/todos/{todo}/changeHistories/{change_history}）。{change_history} はサーバーが決める ID。 {calendar}/{todo} には、Todo のリソース名と同じく、Todo が出ているカレンダーのどれでも指定できる。 返す name は、問い合わせたカレンダーのもの（同じ履歴でも、カレンダーごとに name が違う）。 |
| actor | [string](#string) |  | 変えた人の kebab のユーザー ID（TodoComment.author と同じ形式）。CalDAV からのときは、アプリパスワードの持ち主。 変えた人がカレンダーのメンバーから外れても返る。表示名・アイコンは返さない。kebab の GetUser で引くこと。 |
| change_type | [TodoChangeType](#limani-v1-TodoChangeType) |  | 変更の種類。 |
| source | [TodoChangeSource](#limani-v1-TodoChangeSource) |  | 変えた経路。 |
| snapshot | [Todo](#limani-v1-Todo) |  | 変更後の Todo。容量を抑えるため、ics・etag・calendars は空。name は問い合わせたカレンダーのもの。 sequence・create_time・update_time・creator・last_updater は、変更した時点の値。 変更の内容を知りたいときは、隣り合う履歴の snapshot の中身のフィールドを比べる。 |
| create_time | [google.protobuf.Timestamp](#google-protobuf-Timestamp) |  | 変更した時刻。 |
| comment | [string](#string) |  | この変更と同時に書かれたコメントのリソース名（calendars/{calendar}/todos/{todo}/comments/{comment}）。 CreateTodoCommentRequest.status で状態を変えたときだけ入る（GitHub の &#34;Close with comment&#34; の、状態の変更の側）。 画面は、このコメントが一覧にあれば、状態の変更を履歴の側では出さない（コメントが同じ出来事を示すため）。 コメントを削除しても、この値は残る（指すコメントはもうない）。コメントと同時でない変更は空。 {calendar} は、問い合わせたカレンダーのもの。 |





 


<a name="limani-v1-TodoChangeSource"></a>

### TodoChangeSource
TodoChangeSource は、Todo を変えた経路。

| Name | Number | Description |
| ---- | ------ | ----------- |
| TODO_CHANGE_SOURCE_UNSPECIFIED | 0 |  |
| TODO_CHANGE_SOURCE_API | 1 | Connect の API（limani の画面を含む）。 |
| TODO_CHANGE_SOURCE_CALDAV | 2 | CalDAV（iOS のリマインダー・Thunderbird・Tasks.org など）。 |



<a name="limani-v1-TodoChangeType"></a>

### TodoChangeType
TodoChangeType は、Todo の変更の種類。

| Name | Number | Description |
| ---- | ------ | ----------- |
| TODO_CHANGE_TYPE_UNSPECIFIED | 0 |  |
| TODO_CHANGE_TYPE_CREATE | 1 | Todo の作成。 |
| TODO_CHANGE_TYPE_UPDATE | 2 | Todo の更新。 |


 

 

 



<a name="limani_v1_todo_change_history_api-proto"></a>
<p align="right"><a href="#top">Top</a></p>

## limani/v1/todo_change_history_api.proto



<a name="limani-v1-ListTodoChangeHistoriesRequest"></a>

### ListTodoChangeHistoriesRequest
ListTodoChangeHistoriesRequest は、Todo の変更履歴を一覧する。

呼び出し元が parent のカレンダーのメンバーである必要がある（vitrina のロールが読み取りだけの人もできる）。
変えた人がカレンダーのメンバーから外れていても、履歴は返る。


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| parent | [string](#string) |  | 親の Todo（calendars/{calendar}/todos/{todo}）。{calendar} は Todo が出ているカレンダーのどれでもよい。 |
| page_size | [int32](#int32) |  | 1 ページの件数。0 以下なら 50。100 を超える値は 100 にする。 |
| page_token | [string](#string) |  | 前の応答の next_page_token。空なら最初のページ。 |






<a name="limani-v1-ListTodoChangeHistoriesResponse"></a>

### ListTodoChangeHistoriesResponse



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| todo_change_histories | [TodoChangeHistory](#limani-v1-TodoChangeHistory) | repeated | 変更した時刻の降順（新しいものが先。同じ時刻なら ID の降順）。 |
| next_page_token | [string](#string) |  | 次のページがあるときの page_token。なければ空。 |





 

 

 

 



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

コメントは、Todo の書き込み権限のあるメンバーが「ピン留め」できる（PinTodoComment・UnpinTodoComment）。
ピン留めしたコメントは、画面で Todo の上のほうに固定して見せるためのもの（大事な決定・連絡先・手順など）。
ピン留めは Todo に属する（Todo が出ているすべてのカレンダーで共有する）。コメントを消すと、ピン留めも消える。

コメントでは、Todo が出ているカレンダーのメンバーを「メンション」できる（GitHub の @username と同じ）。
本文に @username と書いたユーザーの kebab のユーザー ID を、書く側（クライアント）が mentions に入れて送る。
サーバーは本文（Markdown）を解釈してメンションを見つけることはしない。mentions に入った人は、
メンションされたことの通知（limani の NOTIFICATION_KIND_MENTIONED）を受け取る。

コメントには、ドキュメントの選択範囲に付ける「レビューコメント」がある（Google ドキュメントや Zenn のレビューのような使い方）。
ebi（ブログ記事）や pompe（SNS の投稿）が、記事・投稿の一部を選択して書いたコメントを、その作成タスクのコメントとして limani に保存する。
選択範囲は anchor（TodoCommentAnchor）に入れる。anchor のあるコメントが「レビューのスレッド」のルートになり、
それへの返信は reply_to でルートを指す（返信に anchor はない。スレッドは 1 段）。
limani は anchor を保存して返すだけで、ドキュメントの中身を解釈しない（URL を開いて範囲に戻るのはクライアントの仕事）。
スレッドは、ルートに「解決済み」の印（resolve_time・resolved_by。ResolveTodoComment・UnresolveTodoComment）を付けられる。
ルートのコメントを削除すると、その返信もすべて消える。
選択範囲を持たない、文書全体へのレビューコメントもある（GitHub の PR の「レビューとしてコメント」と同じ使い方）。
review を true にしたコメントは、anchor のあるコメントと同じく「レビューのスレッド」のルートになり、返信（reply_to）・解決・
ルート削除での返信の削除ができる。review のないコメントは、これまでどおり通常のコメントで、返信も解決もない。
レビューコメントの作成・返信・解決も、通常のコメントと同じく、Todo の etag・sequence・update_time、カレンダーの sync_token を変えない。


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| name | [string](#string) |  | リソース名（calendars/{calendar}/todos/{todo}/comments/{comment}）。{comment} はサーバーが決める ID。 {calendar}/{todo} には、Todo のリソース名と同じく、Todo が出ているカレンダーのどれでも指定できる。 返す name は、問い合わせたカレンダーのもの（同じコメントでも、カレンダーごとに name が違う）。 |
| body | [string](#string) |  | 本文。GitHub Flavored Markdown（GFM）として表示する。サーバーは Markdown を解釈せず、そのまま保存して返す （表示する側で HTML に変換し、サニタイズすること）。 改行（CRLF・CR）は LF にそろえ、前後の空白・改行を取り除いて保存する。取り除いたあとが空なら INVALID_ARGUMENT。 必須で、10000 文字（Unicode のコードポイント）まで。制御文字（改行とタブを除く）は使えない。 ただし CreateTodoCommentRequest.status を指定して書くときは、空にできる（出来事だけの記録になる）。 |
| author | [string](#string) |  | 書いた人の kebab のユーザー ID（Todo.assignees と同じ形式）。 書いた人がカレンダーのメンバーから外れても、コメントは返る。 |
| author_display_name | [string](#string) |  | 書いた人の表示名。kebab のプロフィールの表示名（なければ username）を、書いた時刻（本文を直した時刻）に写したもの。 書いたときにプロフィールを取得できなかったときは空。直したときに取得できなかったときは、前の値のまま。 |
| author_image_url | [string](#string) |  | 書いた人のアイコンの URL。author_display_name と同じ時点の写し。ないときは空。 |
| create_time | [google.protobuf.Timestamp](#google-protobuf-Timestamp) |  | 作成時刻。 |
| update_time | [google.protobuf.Timestamp](#google-protobuf-Timestamp) |  | 本文を最後に直した時刻。直していなければ create_time と同じ。 |
| status_change | [TodoStatus](#limani-v1-TodoStatus) |  | このコメントと同時に変えた Todo の状態（GitHub の &#34;Close with comment&#34;）。 CreateTodoCommentRequest.status を指定して書いたコメントだけ入る（COMPLETED なら完了、NEEDS_ACTION・IN_PROCESS なら再開など）。 状態を変えていないコメントは TODO_STATUS_UNSPECIFIED。本文を直しても変わらない。 画面はこれを「完了にした」「再開した」などの出来事として表示できる。 TODO_STATUS_COMPLETED のコメントは「完了報告」（成果物・エビデンス）として、画面で目立たせる。 担当者が 2 人以上いて、書いた人の分だけが完了になったとき（Todo は COMPLETED にならない）も、 このコメントの status_change は TODO_STATUS_COMPLETED で、書いた人の分の完了報告になる。 ListTodoCommentsRequest.status_change で完了報告だけを一覧できる。 |
| pin_time | [google.protobuf.Timestamp](#google-protobuf-Timestamp) |  | ピン留めした時刻。ピン留めされていなければ未設定。 PinTodoComment で入り、UnpinTodoComment で消える。すでにピン留めされているコメントにもう一度 PinTodoComment を呼んでも変わらない。 本文を直しても変わらない。ListTodoCommentsRequest.pinned_only でピン留めされたコメントだけを一覧できる。 |
| pinned_by | [string](#string) |  | ピン留めした人の kebab のユーザー ID（author と同じ形式）。ピン留めされていなければ空。 ピン留めした人がカレンダーのメンバーから外れても、そのまま返る。 |
| mentions | [string](#string) | repeated | 本文でメンションしたユーザーの kebab のユーザー ID（Todo.assignees と同じ形式）。OPTIONAL。 本文の @username に対応する ID を、クライアントが CreateTodoCommentRequest・UpdateTodoCommentRequest で設定する。 画面はこれを使って、本文の @username をメンションとして強調して見せられる。

サーバーは保存するときに次のように整える（エラーにせず、黙って落とす）。 - 前後の空白を取り除き、空の要素と重複を落とす。 - Todo が出ているカレンダー（TodoLink）のどれかのメンバーでない ID を落とす （メンバーでない人にはメンションの通知を送らない。存在しない ID・書式の違う文字列も同じ）。 - 書いた人本人は残す（ただし、本人には通知しない）。 空の要素と重複を除いた数が 50 を超えると INVALID_ARGUMENT（メンバーかどうかで落とす前の数。 「mentions は 50 人以内にしてください」。Todo.assignees と同じ上限）。 返す値は整えたあとのもので、指定した値より少ないことがある。順は指定した順ではなく、kebab のユーザー ID の昇順。

作成時（CreateTodoCommentRequest）は、指定したすべての人が（書いた人本人を除いて）メンションの通知を受け取る。 更新時（UpdateTodoCommentRequest）は、update_mask に mentions を含めたときだけ置き換わり（空なら全員外れる）、 通知を受け取るのは、直す前の mentions になかった人だけ（ほかの人には通知しない）。 一度メンションされた人は、その Todo の参加者になり、以降のコメントの通知（NOTIFICATION_KIND_COMMENTED）も受け取る。 メンションは Todo の etag・sequence・update_time、カレンダーの sync_token を変えず、iCalendar・CalDAV にも出ない。 CreateTodoCompletionTicket・RedeemTodoCompletionTicket で書くコメントでは、メンションできない（常に空）。 |
| anchor | [TodoCommentAnchor](#limani-v1-TodoCommentAnchor) |  | ドキュメント（ブログ記事・SNS の投稿など）の選択範囲。OPTIONAL・IMMUTABLE。 設定したコメントは「レビューコメント」で、レビューのスレッド（reply_to で返信がぶら下がる）のルートになる。 CreateTodoCommentRequest で設定したときだけ保存する。UpdateTodoCommentRequest では変えられない（指定しても無視する）。 選択範囲をずらしたいときは、コメントを消して書き直す。 中身は TodoCommentAnchor の検証に通ったものだけが入る（通らなければ INVALID_ARGUMENT）。返すときは検証・正規化したあとの値。 reply_to と同時に指定できない（返信に anchor はない）。CreateTodoCommentRequest.status とも同時に指定できない。 |
| reply_to | [string](#string) |  | このコメントが返信する、ルートのコメントのリソース名（calendars/{calendar}/todos/{todo}/comments/{comment}）。 OPTIONAL・IMMUTABLE。空なら返信ではない（通常のコメントか、レビューのスレッドのルート）。 CreateTodoCommentRequest で設定したときだけ保存する。UpdateTodoCommentRequest では変えられない（指定しても無視する）。

指定できるのは、同じ Todo の、レビューのスレッドのルート（anchor のある、または review が true の）コメントだけ。 {calendar} は Todo が出ているカレンダーのどれでもよい（name と同じ）。返す値は、name と同じく、問い合わせたカレンダーのもの。 - 返信先がない（消えた・{todo} のコメントがない）→ NOT_FOUND - 別の Todo のコメント → INVALID_ARGUMENT - レビューのスレッドのルートでない（anchor がなく review も false の）コメントへの返信、返信への返信（スレッドは 1 段）→ INVALID_ARGUMENT （通常のコメントへの返信は今のところ受け付けない。将来、受け付けるようにするかもしれない） - anchor・review と同時に指定する → INVALID_ARGUMENT（返信に anchor・review は付けない） - CreateTodoCommentRequest.status と同時に指定する → INVALID_ARGUMENT 返信にも本文（body）は必須で、mentions も付けられる。返信も 1 つの Todo に付けられるコメントの上限（1000 件）に数える。 解決済みのスレッドに返信すると、スレッドは未解決に戻る（resolve_time・resolved_by が消える。Google ドキュメントと同じ）。 返信にもピン留め（PinTodoComment）はできる（ルートと同じ。ピン留めの扱いは変わらない）。 ルートのコメントが消えると（DeleteTodoComment）、返信も消える。返信だけを消しても、ルートや、ほかの返信は消えない。 |
| resolve_time | [google.protobuf.Timestamp](#google-protobuf-Timestamp) |  | スレッドを解決済みにした時刻。レビューのスレッドのルート（anchor のある、または review が true の）コメントだけに入り、解決済みでなければ未設定（返信・通常のコメントも常に未設定）。 ResolveTodoComment で入り、UnresolveTodoComment、または解決済みのスレッドへの返信で消える。 すでに解決済みのスレッドにもう一度 ResolveTodoComment を呼んでも変わらない。 解決・解決の取り消しは、コメントの update_time（本文を直した時刻）を変えない。 |
| resolved_by | [string](#string) |  | スレッドを解決済みにした人の kebab のユーザー ID（author と同じ形式）。解決済みでなければ空。 解決した人がカレンダーのメンバーから外れても、そのまま返る。 |
| review | [bool](#bool) |  | 文書全体へのレビューコメント（選択範囲を持たないレビューコメント）なら true。OPTIONAL・IMMUTABLE。 true のコメントは、anchor のあるコメントと同じく「レビューのスレッド」のルートになる （reply_to で返信がぶら下がり、ResolveTodoComment・UnresolveTodoComment で解決でき、消すと返信も消える）。 返信（reply_to のあるコメント）に review は付けない（返信は reply_to だけ）。 CreateTodoCommentRequest で設定したときだけ保存する。UpdateTodoCommentRequest では変えられない（指定しても無視する）。 anchor・reply_to と同時に指定できない。CreateTodoCommentRequest.status とも同時に指定できない（INVALID_ARGUMENT）。 false（または省略）なら、review のコメントではない（通常のコメントか、anchor のあるルート、または返信）。 書き込み権限・通知・Todo の etag・sequence・update_time、カレンダーの sync_token は、anchor のあるレビューコメントと同じ。 ListTodoCommentsRequest.anchor_target で絞り込んだときには、review のコメントは返らない。 |






<a name="limani-v1-TodoCommentAnchor"></a>

### TodoCommentAnchor
TodoCommentAnchor は、レビューコメントが指す、ドキュメント（ブログ記事・SNS の投稿など）の選択範囲。

W3C Web Annotation Data Model の TextQuoteSelector（exact・prefix・suffix）を中心に、
位置のヒント（start・end）と、ドキュメントを開く URL（uri）、ドキュメントの識別子（target）を持つ。
limani はこれを不透明な値として保存して返す。検証（下記の長さ・文字・URL の形）以外には、中身を解釈しない
（ドキュメントが実際にあるか、exact が本当にその位置にあるかも確かめない）。

クライアントは、ドキュメントが編集されて位置がずれたあとでも、exact・prefix・suffix でドキュメントを検索して範囲を探し直す
（再アンカー）。start・end は探すときの「ヒント」でしかなく、正しいとは限らない。
行番号は、表示するときにクライアントが位置から求めるもので、保存しない。

文字数はすべて Unicode のコードポイントで数える（start・end だけは UTF-16 のコードユニット）。
文字列に使えない文字は、改行（LF）とタブを除く制御文字など（TodoComment.body と同じ）。ただし target・part・version・target_title は
改行とタブも使えない（1 行の識別子・題名として扱う）。


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| uri | [string](#string) |  | コメントの位置でドキュメントを開く URL（たとえば ebi の編集画面の URL）。必須。 limani の画面は、これをリンクとして見せる。 絶対 URL の https:// で始まるものだけ（開発用に、http://localhost と http://127.0.0.1 は http:// でもよい。ポートを付けてもよい）。 2048 文字以内で、空白・制御文字・ユーザー情報（user:password@）を含められない。違反は INVALID_ARGUMENT。 |
| target | [string](#string) |  | ドキュメントを識別する、クライアントが決める安定した ID（たとえば //ebi.kanade.party/blogs/123、 //pompe.kanade.party/posts/abc）。必須。 クライアントは、ドキュメントごとにコメントを絞り込むために使う（ListTodoCommentsRequest.anchor_target）。 512 文字以内で、制御文字（改行・タブを含む）は使えない。違反は INVALID_ARGUMENT。 |
| part | [string](#string) |  | ドキュメントの中の部分（たとえば pompe のスレッドの投稿の ID・番号）。OPTIONAL。 1 つのドキュメントが複数の部分からなるとき、start・end はこの部分の中の位置になる。空なら、ドキュメント全体。 256 文字以内で、制御文字は使えない。 |
| version | [string](#string) |  | コメントしたときの、ドキュメントの版（たとえば ebi の change_history_id）。OPTIONAL。 start・end は、この版のドキュメントの位置。空なら、版は不明。 256 文字以内で、制御文字は使えない。 |
| exact | [string](#string) |  | 選択した文字列そのもの（W3C Web Annotation の TextQuoteSelector の exact）。必須。 1 文字以上 2000 文字以内。改行（CRLF・CR）は LF にそろえて保存する。 前後の空白は取り除かない（空白も範囲の一部なので、そのまま保存する）。ただし、空・空白だけは INVALID_ARGUMENT。 制御文字（改行とタブを除く）は使えない。 |
| prefix | [string](#string) |  | exact の直前の文脈（TextQuoteSelector の prefix）。OPTIONAL。64 文字以内。再アンカーで同じ文字列を見分けるために使う。 改行は LF にそろえ、前後の空白は取り除かない。制御文字（改行とタブを除く）は使えない。 |
| suffix | [string](#string) |  | exact の直後の文脈（TextQuoteSelector の suffix）。OPTIONAL。64 文字以内。prefix と同じ扱い。 |
| start | [int32](#int32) |  | 位置のヒント: part（なければドキュメント全体）の中の、選択範囲の開始位置。OPTIONAL。 UTF-16 のコードユニットの数（JavaScript の文字列の添字）で、version のドキュメントで 0 から数える。 0 &lt;= start &lt;= end でなければ INVALID_ARGUMENT。 start と end がどちらも 0 のときは、位置のヒントがない（exact は空にできないので、実際の範囲では end が 0 より大きい）。 あくまでヒントで、ドキュメントが編集されていたら合わない。クライアントは exact・prefix・suffix で探し直すこと。 |
| end | [int32](#int32) |  | 位置のヒント: 選択範囲の終了位置（含まない）。start と同じ単位。OPTIONAL。 |
| target_title | [string](#string) |  | ドキュメントの題名（limani の画面で、どのドキュメントへのコメントかを見せるため）。OPTIONAL。 200 文字以内で、制御文字は使えない。コメントしたときの題名の写しで、後から変えても追従しない。 |





 

 

 

 



<a name="limani_v1_todo_comment_api-proto"></a>
<p align="right"><a href="#top">Top</a></p>

## limani/v1/todo_comment_api.proto



<a name="limani-v1-CreateTodoCommentRequest"></a>

### CreateTodoCommentRequest
CreateTodoCommentRequest は、Todo にコメントを書く。

呼び出し元が parent のカレンダーのメンバーである必要がある（vitrina のロールが読み取りだけの人もできる）。
1 つの Todo に付けられるコメントは 1000 件まで（超えると RESOURCE_EXHAUSTED。返信も 1 件に数える）。

todo_comment.anchor を指定すると、ドキュメントの選択範囲に付けるレビューコメント（レビューのスレッドのルート）になる。
todo_comment.review を true にすると、文書全体へのレビューコメント（選択範囲を持たない、レビューのスレッドのルート）になる。
todo_comment.reply_to を指定すると、そのルートへの返信になる（解決済みのスレッドに返信すると、未解決に戻る）。
anchor・review・reply_to は、どれも同時には指定できず、いずれも status と同時に指定できない（INVALID_ARGUMENT）。
書き込み権限は通常のコメントと同じ（メンバーならよい。読み取りだけのメンバーもレビューコメント・返信を書ける）。

status を指定すると、GitHub の &#34;Close with comment&#34; のように、Todo の状態を変えてからコメントを書く。
状態の変更は SetTodoStatus と同じ（COMPLETED にすると completed_time が入り percent_complete が 100 になる。
COMPLETED から別の状態に戻すと completed_time が消える）ので、Todo の etag・sequence・update_time と
カレンダーの sync_token が変わる（etag の確認はしない）。状態を変えるには Todo の書き込み権限が要り、
読み取りだけのメンバーは PERMISSION_DENIED になって、状態もコメントも書かれない。
ただし、読み取りだけのメンバーも、その Todo の担当者なら、COMPLETED（自分の分の完了）と、COMPLETED から戻す（自分の分の取り消し）
状態つきのコメントは書ける（中止や、自分の分以外が変わる状態の変更は PERMISSION_DENIED。SetTodoStatus の「閲覧のみのメンバーの自己申告」を参照）。
担当者がいるときの COMPLETED は、コメントを書いた人（行為者）の分の完了になり、全員の分がそろわなければ Todo は
COMPLETED にならない（SetTodoStatus の「担当者ごとの完了」を参照。コメントの status_change は COMPLETED のまま）。
状態を変えられなかったときは、コメントも書かない。


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| parent | [string](#string) |  | 親の Todo（calendars/{calendar}/todos/{todo}）。{calendar} は Todo が出ているカレンダーのどれでもよい。 |
| todo_comment | [TodoComment](#limani-v1-TodoComment) |  | 作るコメント。status を指定しないときは body が必須。mentions（メンションした人の kebab のユーザー ID）は任意。 mentions に入れた人（Todo が出ているカレンダーのメンバーだけ。それ以外は黙って落とす。50 人まで）は、書いた人本人を除いて、 メンションの通知を受け取る（メンションされた人には COMMENTED は送らない）。 anchor（選択範囲。TodoCommentAnchor の検証に通らなければ INVALID_ARGUMENT）と review（文書全体へのレビューコメント）と reply_to（返信先のルートのコメント）は任意。 name・author・author_display_name・author_image_url・create_time・update_time・status_change・pin_time・pinned_by・ resolve_time・resolved_by は無視する （書いたコメントはピン留めも解決もされていない。ピン留めは PinTodoComment、解決は ResolveTodoComment で行う）。 |
| status | [TodoStatus](#limani-v1-TodoStatus) |  | コメントと同時に変える Todo の状態。TODO_STATUS_UNSPECIFIED（または省略）なら状態は変えない。 指定したときは body を空にでき（出来事だけの記録になる）、書いたコメントの status_change にこの値が入る。 今の状態と同じでもよい（SetTodoStatus と同じく Todo は書き直され、コメントが status_change つきで書かれる）。 |






<a name="limani-v1-DeleteTodoCommentRequest"></a>

### DeleteTodoCommentRequest
DeleteTodoCommentRequest は、コメントを削除する（物理削除。記録は残さない）。

消せるのは書いた人だけ（それ以外のメンバーは PERMISSION_DENIED）。

レビューのスレッドのルート（anchor のある、または review のコメント）を消すと、その返信（reply_to がそのコメントを指すコメント）も
すべて消える（返信を書いた人でなくても、ルートを書いた人が消せる）。返信だけを消しても、ルートやほかの返信は消えない。


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| name | [string](#string) |  | リソース名（calendars/{calendar}/todos/{todo}/comments/{comment}）。 |






<a name="limani-v1-ListTodoCommentsRequest"></a>

### ListTodoCommentsRequest
ListTodoCommentsRequest は、Todo のコメントを一覧する。

呼び出し元が parent のカレンダーのメンバーである必要がある。
書いた人がカレンダーのメンバーから外れていても、コメントは返る。

レビューコメント（anchor のある、または review のコメント）と、その返信（reply_to のあるコメント）も、通常のコメントと一緒に返る（並び順も同じ）。
クライアントは、reply_to でルートの下に返信をまとめてスレッドを作り、TodoComment.anchor.target で
ドキュメントごとのコメントを絞る（サーバー側で絞るなら anchor_target）。
文書全体へのレビューコメント（review）だけを絞り込む指定はない。クライアントは anchor_target なしで全件を取り、review で分ける。


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| parent | [string](#string) |  | 親の Todo（calendars/{calendar}/todos/{todo}）。{calendar} は Todo が出ているカレンダーのどれでもよい。 |
| page_size | [int32](#int32) |  | 1 ページの件数。0 以下なら 50。200 を超える値は 200 にする。 |
| page_token | [string](#string) |  | 前の応答の next_page_token。空なら最初のページ。 |
| status_change | [TodoStatus](#limani-v1-TodoStatus) |  | 指定すると、TodoComment.status_change がこの値のコメントだけを返す（並び順・ページングは同じ）。 たとえば TODO_STATUS_COMPLETED を指定すると、完了報告だけを取り出せる。 TODO_STATUS_UNSPECIFIED（または省略）なら絞り込まない。 page_token は、同じ status_change で取得したときだけ使える（違う値で使うと INVALID_ARGUMENT）。 |
| pinned_only | [bool](#bool) |  | true なら、ピン留めされているコメント（TodoComment.pin_time が設定されているもの）だけを返す（並び順・ページングは同じ）。 false（または省略）なら絞り込まない。status_change と同時に指定すると、両方に合うものだけを返す。 page_token は、同じ status_change・pinned_only の組で取得したときだけ使える（違う値で使うと INVALID_ARGUMENT）。 |
| anchor_target | [string](#string) |  | 指定すると、レビューコメントのうち TodoComment.anchor.target がこの値と等しいルートのコメントと、そのルートへの返信 （TodoComment.reply_to がそのルートを指すコメント）だけを返す。anchor のない通常のコメントと、review のコメント（文書全体へのレビューコメント。anchor がない）は返さない。 並び順・ページングは同じ（作成時刻の昇順で、ルートと返信が混ざる）。 空（または省略）なら絞り込まない。status_change・pinned_only と同時に指定すると、すべてに合うものだけを返す （返信は、返信自身が status_change・pinned_only の条件に合うかで決まる）。 page_token は、同じ status_change・pinned_only・anchor_target の組で取得したときだけ使える（違う値で使うと INVALID_ARGUMENT）。 |






<a name="limani-v1-ListTodoCommentsResponse"></a>

### ListTodoCommentsResponse



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| todo_comments | [TodoComment](#limani-v1-TodoComment) | repeated | 作成時刻の昇順（古いものが先。同じ時刻なら ID の昇順）。 |
| next_page_token | [string](#string) |  | 次のページがあるときの page_token。なければ空。 |






<a name="limani-v1-PinTodoCommentRequest"></a>

### PinTodoCommentRequest
PinTodoCommentRequest は、コメントをピン留めする（Todo の上のほうに固定して見せるための印を付ける）。

呼び出し元が name のカレンダーの書き込み権限のあるメンバーである必要がある（読み取りだけのメンバーは PERMISSION_DENIED）。
誰が書いたコメントでもピン留めできる（書いた人でなくてもよい）。
すでにピン留めされているコメントには何もせず、今の値を返す（pin_time・pinned_by は変えない）。
1 つの Todo にピン留めできるコメントは 10 件まで（超えると RESOURCE_EXHAUSTED）。
ピン留めは、Todo の etag・sequence・update_time、カレンダーの sync_token、コメントの update_time を変えない。


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| name | [string](#string) |  | リソース名（calendars/{calendar}/todos/{todo}/comments/{comment}）。 |






<a name="limani-v1-ResolveTodoCommentRequest"></a>

### ResolveTodoCommentRequest
ResolveTodoCommentRequest は、レビューのスレッドを解決済みにする（Google ドキュメントの「解決」）。

呼び出し元が name のカレンダーのメンバーである必要がある（読み取りだけのメンバーもできる。書いた人でなくてもよい）。
対象にできるのは、レビューのスレッドのルート（anchor のある、または review のコメント）だけ（通常のコメント・返信は FAILED_PRECONDITION）。
すでに解決済みなら何もせず今の値を返す（resolve_time・resolved_by は最初のまま）。
解決は、Todo の etag・sequence・update_time、カレンダーの sync_token、コメントの update_time を変えない。通知も送らない。
解決済みのスレッドに返信を書くと、未解決に戻る。


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| name | [string](#string) |  | リソース名（calendars/{calendar}/todos/{todo}/comments/{comment}）。 |






<a name="limani-v1-UnpinTodoCommentRequest"></a>

### UnpinTodoCommentRequest
UnpinTodoCommentRequest は、コメントのピン留めを外す。

呼び出し元が name のカレンダーの書き込み権限のあるメンバーである必要がある（読み取りだけのメンバーは PERMISSION_DENIED）。
ピン留めした人でなくても外せる。ピン留めされていないコメントには何もせず、今の値を返す。
ピン留めを外しても、コメントは消えない。Todo の etag・sequence・update_time、カレンダーの sync_token、
コメントの update_time は変わらない。


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| name | [string](#string) |  | リソース名（calendars/{calendar}/todos/{todo}/comments/{comment}）。 |






<a name="limani-v1-UnresolveTodoCommentRequest"></a>

### UnresolveTodoCommentRequest
UnresolveTodoCommentRequest は、レビューのスレッドの解決済みを取り消す（未解決に戻す）。

呼び出し元が name のカレンダーのメンバーである必要がある（読み取りだけのメンバーもできる。解決した人でなくてもよい）。
対象にできるのは、レビューのスレッドのルート（anchor のある、または review のコメント）だけ（通常のコメント・返信は FAILED_PRECONDITION）。
解決済みでなければ何もせず今の値を返す。
Todo の etag・sequence・update_time、カレンダーの sync_token、コメントの update_time は変わらない。通知も送らない。


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| name | [string](#string) |  | リソース名（calendars/{calendar}/todos/{todo}/comments/{comment}）。 |






<a name="limani-v1-UpdateTodoCommentRequest"></a>

### UpdateTodoCommentRequest
UpdateTodoCommentRequest は、コメントの本文を直す。

直せるのは書いた人だけ（それ以外のメンバーは PERMISSION_DENIED）。


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| todo_comment | [TodoComment](#limani-v1-TodoComment) |  | 直すコメント。name で対象を決める。Todo が出ているカレンダーのどの name でもよい。 body・mentions 以外（author・create_time・update_time・status_change・pin_time・pinned_by・anchor・reply_to・review・resolve_time・resolved_by など）は無視する。 ピン留め・解決済みの印は本文を直しても変わらない。anchor・reply_to・review は作ったあとに変えられない。 |
| update_mask | [google.protobuf.FieldMask](#google-protobuf-FieldMask) |  | 更新するフィールド。指定できるのは body と mentions。空なら body だけを更新する（mentions は変えない）。 mentions を指定すると、メンションした人をそっくり置き換える（todo_comment.mentions が空なら、全員外す）。 新しくメンションされた人（直す前の mentions になかった人。書いた人本人を除く）だけがメンションの通知を受け取り、 外れた人・そのまま残った人・ほかの人には、通知を送らない。 body を指定しないときは、todo_comment.body は無視する（本文は変わらない）。 |





 

 

 

 



<a name="limani_v1_todo_completion_ticket-proto"></a>
<p align="right"><a href="#top">Top</a></p>

## limani/v1/todo_completion_ticket.proto



<a name="limani-v1-TodoCompletionTicket"></a>

### TodoCompletionTicket
TodoCompletionTicket は、あとで Todo を完了報告つきで完了にするための引換券（完了チケット）。

pompe の予約投稿のように、利用者の kebab のトークンを持たない無人の処理から Todo を完了にするために使う。
利用者がいるうち（投稿を保存したときなど）に、利用者のトークンで CreateTodoCompletionTicket を呼んで発行しておき、
あとで処理が終わったときに secret を RedeemTodoCompletionTicket に渡して引き換える。

引き換えると、Todo を COMPLETED にし、発行した人を書いた人として完了報告（status_change が COMPLETED のコメント）を書く。
発行した人が担当者の一人なら、その人の分の完了になる（全員の分がそろうまで Todo は COMPLETED にならない）。
1 枚のチケットで書ける完了報告は 1 件だけ。同じ Todo に何枚でも発行でき、それぞれが別の完了報告になる。
チケットは iCalendar・CalDAV には出ない。


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| name | [string](#string) |  | リソース名（calendars/{calendar}/todos/{todo}/completionTickets/{ticket}）。{ticket} はサーバーが決める ID。 {calendar} は、発行したときに指定したカレンダー。 |
| secret | [string](#string) |  | 引き換えに使う秘密の文字列。CreateTodoCompletionTicket の応答にだけ入る（サーバーはハッシュだけを保存する）。 持っている人は誰でも引き換えられるので、パスワードと同じく扱うこと。 |
| issuer | [string](#string) |  | 発行した人の kebab のユーザー ID。引き換えたときの完了報告は、この人が書いたことになる。 |
| create_time | [google.protobuf.Timestamp](#google-protobuf-Timestamp) |  | 発行した時刻。 |
| expire_time | [google.protobuf.Timestamp](#google-protobuf-Timestamp) |  | 有効期限。発行から 400 日。過ぎると引き換えられない。 |





 

 

 

 



<a name="limani_v1_todo_completion_ticket_api-proto"></a>
<p align="right"><a href="#top">Top</a></p>

## limani/v1/todo_completion_ticket_api.proto



<a name="limani-v1-CreateTodoCompletionTicketRequest"></a>

### CreateTodoCompletionTicketRequest
CreateTodoCompletionTicketRequest は、Todo の完了チケットを発行する。

認証は kebab のアクセストークン。呼び出し元が Todo の書き込み権限を持つ必要がある
（読み取りだけのメンバーは PERMISSION_DENIED、メンバーでなければ NOT_FOUND）。
ただし、読み取りだけのメンバーも、その Todo の担当者なら発行できる（レビューする人が自分の分を承認するため）。
そのチケットを引き換えると、完了になるのは発行した人の分だけ（SetTodoStatus の「閲覧のみのメンバーの自己申告」と同じ。
全員の分がそろうまで Todo は COMPLETED にならない）。
発行しても Todo は変わらない（etag・sequence・update_time、カレンダーの sync_token も変わらない）。
1 つの Todo に対して、引き換えていない有効なチケットは 1000 枚まで（超えると RESOURCE_EXHAUSTED）。


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| parent | [string](#string) |  | 親の Todo（calendars/{calendar}/todos/{todo}）。{calendar} は Todo が出ているカレンダーのどれでもよい。 |






<a name="limani-v1-RedeemTodoCompletionTicketRequest"></a>

### RedeemTodoCompletionTicketRequest
RedeemTodoCompletionTicketRequest は、完了チケットを引き換えて、Todo を完了報告つきで完了にする。

認証は secret だけで、kebab のトークンは要らない（付けても無視する）。
CreateTodoCommentRequest に status = TODO_STATUS_COMPLETED を付けて書いたのと同じになる
（すでに COMPLETED の Todo でもよい）。コメントの書いた人は、チケットを発行した人。
完了にする行為者もチケットを発行した人で、発行した人が Todo の担当者の一人なら、その人の分だけが完了になる
（全員の分がそろうまで Todo は COMPLETED にならない。SetTodoStatus の「担当者ごとの完了」を参照）。
表示名・アイコンは、発行したときに kebab のプロフィールから写したもの。

次の順に確かめる。

1. secret が違う・期限切れ・Todo が削除された: NOT_FOUND
2. 引き換え済み: 権限は確かめ直さず、最初に書いた完了報告を返して何もしない
   （応答を受け取れなかったときに再試行してよい）。その完了報告が削除されていれば FAILED_PRECONDITION。
3. 発行した人が、Todo が「今」出ているカレンダー（TodoLink）のどれかで、Todo の書き込み権限を持っていること
   （カレンダーのメンバーの写しで判定する）。発行したカレンダーとのリンクが外れていて、ほかのカレンダーでも
   書き込み権限がなくても、そのカレンダーのメンバーのままで Todo の担当者なら、発行した人の分だけを完了にする。
   どちらでもなければ PERMISSION_DENIED で、何も書かない。
4. Todo のコメントが上限（1000 件）に達していれば RESOURCE_EXHAUSTED で、何も書かない
   （チケットは引き換えていない扱いのまま残り、コメントが消されて枠が空けば、期限内なら引き換えられる）。

返す完了報告の name は、発行したカレンダーが今も Todo とリンクしていればそのカレンダーのもの、
外れていれば、今リンクしているカレンダーのうち ID がいちばん小さいもの（引き換え済みのチケットで再試行したときも同じ決め方）。


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| secret | [string](#string) |  | CreateTodoCompletionTicket が返した TodoCompletionTicket.secret。 |
| body | [string](#string) |  | 完了報告の本文（GitHub Flavored Markdown）。TodoComment.body と同じ規則で、空にはできない。 |





 

 

 

 



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


<a name="limani-v1-TodoCompletionTicketService"></a>

### TodoCompletionTicketService
TodoCompletionTicketService は、完了チケットを引き換える API。
認証はチケットの secret で、kebab のアクセストークンは要らない（利用者のいない無人の処理から呼ぶため）。

| Method Name | Request Type | Response Type | Description |
| ----------- | ------------ | ------------- | ------------|
| RedeemTodoCompletionTicket | [RedeemTodoCompletionTicketRequest](#limani-v1-RedeemTodoCompletionTicketRequest) | [TodoComment](#limani-v1-TodoComment) | 完了チケットを引き換えて、Todo を COMPLETED にし、発行した人の名前で完了報告を書く。 |


<a name="limani-v1-TodoService"></a>

### TodoService
TodoService は Todo（VTODO）の API。
認証は kebab のアクセストークン（Authorization: Bearer）。

| Method Name | Request Type | Response Type | Description |
| ----------- | ------------ | ------------- | ------------|
| ListTodos | [ListTodosRequest](#limani-v1-ListTodosRequest) | [ListTodosResponse](#limani-v1-ListTodosResponse) | カレンダーに出ている Todo を一覧する（TodoLink で同期されている Todo を含む）。 |
| GetTodo | [GetTodoRequest](#limani-v1-GetTodoRequest) | [Todo](#limani-v1-Todo) |  |
| CreateTodo | [CreateTodoRequest](#limani-v1-CreateTodoRequest) | [Todo](#limani-v1-Todo) |  |
| UpdateTodo | [UpdateTodoRequest](#limani-v1-UpdateTodoRequest) | [Todo](#limani-v1-Todo) | Todo を更新する。Todo の書き込み権限が要る。ただし、書き込み権限のない（閲覧のみの）メンバーも、その Todo の担当者なら、 update_mask が assignees・completed_assignees だけで、自分を担当者に足す・外す、自分の分の完了・取り消しだけを変えるときはできる。 |
| SetTodoStatus | [SetTodoStatusRequest](#limani-v1-SetTodoStatusRequest) | [Todo](#limani-v1-Todo) | Todo の状態だけを変える。Todo の書き込み権限が要る。ただし、閲覧のみのメンバーも、その Todo の担当者なら、COMPLETED にして 自分の分だけを完了にする・COMPLETED から戻して自分の分だけを取り消すことはできる（中止はできない）。 |
| DeleteTodo | [DeleteTodoRequest](#limani-v1-DeleteTodoRequest) | [.google.protobuf.Empty](#google-protobuf-Empty) | Todo を削除する。Todo が出ているすべてのカレンダーから消える（どのカレンダーのリソース名で呼んでも同じ）。 1 つのカレンダーから外すだけのときは DeleteTodoLink を使う。 |
| ListTodoLinks | [ListTodoLinksRequest](#limani-v1-ListTodoLinksRequest) | [ListTodoLinksResponse](#limani-v1-ListTodoLinksResponse) | Todo が出ているカレンダーを一覧する。 |
| CreateTodoLink | [CreateTodoLinkRequest](#limani-v1-CreateTodoLinkRequest) | [TodoLink](#limani-v1-TodoLink) | Todo をほかのカレンダーにもリンクする（イベント間の同期）。 |
| DeleteTodoLink | [DeleteTodoLinkRequest](#limani-v1-DeleteTodoLinkRequest) | [.google.protobuf.Empty](#google-protobuf-Empty) | Todo をカレンダーから外す（そのカレンダーとの同期をやめる）。最後の 1 つのカレンダーからは外せない。 |
| ListTodoComments | [ListTodoCommentsRequest](#limani-v1-ListTodoCommentsRequest) | [ListTodoCommentsResponse](#limani-v1-ListTodoCommentsResponse) | Todo のコメントを古い順に一覧する。コメントは Todo が出ているすべてのカレンダーで共有され、iCalendar・CalDAV には出ない。 レビューコメント（anchor のある、または review のコメント）とその返信（reply_to）も一緒に返る。 anchor_target でドキュメントごとに絞れる（review のコメントは、絞り込むと返らない）。 |
| CreateTodoComment | [CreateTodoCommentRequest](#limani-v1-CreateTodoCommentRequest) | [TodoComment](#limani-v1-TodoComment) | Todo にコメントを書く。Todo の etag・sequence・update_time は変わらない。 anchor を付けるとドキュメントの選択範囲へのレビューコメント、review を true にすると文書全体へのレビューコメント、 reply_to を付けるとそのコメントへの返信になる。 status を指定すると、コメントと同時に Todo の状態を変える（GitHub の &#34;Close with comment&#34;）。状態を変えるには書き込み権限が要る （閲覧のみのメンバーも、その Todo の担当者なら、自分の分の完了・取り消しだけはできる）。 |
| UpdateTodoComment | [UpdateTodoCommentRequest](#limani-v1-UpdateTodoCommentRequest) | [TodoComment](#limani-v1-TodoComment) | コメントの本文を直す。書いた人だけができる。 |
| DeleteTodoComment | [DeleteTodoCommentRequest](#limani-v1-DeleteTodoCommentRequest) | [.google.protobuf.Empty](#google-protobuf-Empty) | コメントを削除する。書いた人だけができる。レビューのスレッドのルート（anchor のある、または review のコメント）を消すと、その返信も消える。 |
| PinTodoComment | [PinTodoCommentRequest](#limani-v1-PinTodoCommentRequest) | [TodoComment](#limani-v1-TodoComment) | コメントをピン留めする。Todo の書き込み権限のあるメンバーなら、誰が書いたコメントでもできる。 すでにピン留めされていれば何もせず今の値を返す。1 つの Todo に 10 件まで。Todo の etag・sequence・update_time は変わらない。 |
| UnpinTodoComment | [UnpinTodoCommentRequest](#limani-v1-UnpinTodoCommentRequest) | [TodoComment](#limani-v1-TodoComment) | コメントのピン留めを外す。Todo の書き込み権限のあるメンバーならできる。ピン留めされていなければ何もせず今の値を返す。 |
| ResolveTodoComment | [ResolveTodoCommentRequest](#limani-v1-ResolveTodoCommentRequest) | [TodoComment](#limani-v1-TodoComment) | レビューのスレッド（anchor のある、または review のルートのコメント）を解決済みにする。カレンダーのメンバーなら誰でもできる（読み取りだけのロールも）。 すでに解決済みなら何もせず今の値を返す。Todo の etag・sequence・update_time、コメントの update_time は変わらない。 |
| UnresolveTodoComment | [UnresolveTodoCommentRequest](#limani-v1-UnresolveTodoCommentRequest) | [TodoComment](#limani-v1-TodoComment) | レビューのスレッドの解決済みを取り消す。カレンダーのメンバーなら誰でもできる。解決済みでなければ何もせず今の値を返す。 |
| CreateTodoAttachment | [CreateTodoAttachmentRequest](#limani-v1-CreateTodoAttachmentRequest) | [TodoAttachment](#limani-v1-TodoAttachment) | Todo にファイルを添付する。呼び出し元がカレンダーのメンバーならできる（読み取りだけのロールも）。Todo の etag・sequence・update_time は変わらない。 |
| ListTodoAttachments | [ListTodoAttachmentsRequest](#limani-v1-ListTodoAttachmentsRequest) | [ListTodoAttachmentsResponse](#limani-v1-ListTodoAttachmentsResponse) | Todo の添付を古い順に一覧する（中身は含まず、各添付の download_uri から読む）。添付は Todo が出ているすべてのカレンダーで共有され、iCalendar・CalDAV には出ない。 |
| GetTodoAttachment | [GetTodoAttachmentRequest](#limani-v1-GetTodoAttachmentRequest) | [TodoAttachment](#limani-v1-TodoAttachment) | 添付を取得する（中身は download_uri から読む）。name の {calendar} に &#34;-&#34; を指定できる。 |
| DeleteTodoAttachment | [DeleteTodoAttachmentRequest](#limani-v1-DeleteTodoAttachmentRequest) | [.google.protobuf.Empty](#google-protobuf-Empty) | 添付を削除する。アップロードした人だけができる。 |
| ListTodoChangeHistories | [ListTodoChangeHistoriesRequest](#limani-v1-ListTodoChangeHistoriesRequest) | [ListTodoChangeHistoriesResponse](#limani-v1-ListTodoChangeHistoriesResponse) | Todo の変更履歴を新しい順に一覧する。変更のたびに、変更後の Todo（snapshot）・変えた人・経路（API か CalDAV か）を残す。 履歴は Todo が出ているすべてのカレンダーで共有され、iCalendar・CalDAV には出ない。呼び出し元がカレンダーのメンバーならできる（読み取りだけのロールも）。 |
| CreateTodoCompletionTicket | [CreateTodoCompletionTicketRequest](#limani-v1-CreateTodoCompletionTicketRequest) | [TodoCompletionTicket](#limani-v1-TodoCompletionTicket) | Todo の完了チケットを発行する。あとで RedeemTodoCompletionTicket で、利用者のトークンなしに Todo を完了報告つきで完了にできる （pompe の予約投稿が投稿できたら完了にする、など）。Todo の書き込み権限が要る （閲覧のみのメンバーも、その Todo の担当者なら発行できる。引き換えで完了になるのはその人の分だけ）。 |

 



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

