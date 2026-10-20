# Protocol Documentation
<a name="top"></a>

## Table of Contents

- [limani/v1/calendar.proto](#limani_v1_calendar-proto)
    - [Calendar](#limani-v1-Calendar)
  
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





 

 

 

 



<a name="limani_v1_calendar_api-proto"></a>
<p align="right"><a href="#top">Top</a></p>

## limani/v1/calendar_api.proto



<a name="limani-v1-CreateCalendarRequest"></a>

### CreateCalendarRequest
CreateCalendarRequest はカレンダーを作る。呼び出し元が parent のメンバーである必要がある。


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
| name | [string](#string) |  | リソース名（calendars/{id}/todos/{uid}）。 |
| uid | [string](#string) |  | iCalendar の UID。カレンダー内で一意。作成時に省略するとサーバーが決める。 |
| summary | [string](#string) |  | SUMMARY。必須。 |
| description | [string](#string) |  | DESCRIPTION。 |
| status | [TodoStatus](#limani-v1-TodoStatus) |  | STATUS。作成時に未指定なら NEEDS-ACTION。 |
| priority | [int32](#int32) |  | PRIORITY（0〜9。0 は未設定、1 が最も高い）。 |
| percent_complete | [int32](#int32) |  | PERCENT-COMPLETE（0〜100）。 |
| dtstart | [TodoDateTime](#limani-v1-TodoDateTime) |  | DTSTART。未設定なら省略。 |
| due | [TodoDateTime](#limani-v1-TodoDateTime) |  | DUE。未設定なら省略。dtstart より前にできず、dtstart と all_day をそろえる。 |
| completed_time | [google.protobuf.Timestamp](#google-protobuf-Timestamp) |  | COMPLETED。status が COMPLETED になると、未指定ならサーバーが現在時刻を入れる。 |
| categories | [string](#string) | repeated | CATEGORIES。 |
| parent_uid | [string](#string) |  | 親の Todo の UID（RELATED-TO;RELTYPE=PARENT）。 |
| assignees | [string](#string) | repeated | 担当者の kebab のユーザー ID（ATTENDEE として ics に出る）。 |
| sequence | [int32](#int32) |  | SEQUENCE。更新のたびに増える。 |
| etag | [string](#string) |  | 楽観的排他制御のための値。CalDAV の ETag と同じ。 UpdateTodo で指定すると、保存されている値と違うときに ABORTED を返す。 |
| ics | [string](#string) |  | VCALENDAR 全文（RFC 5545）。 |
| create_time | [google.protobuf.Timestamp](#google-protobuf-Timestamp) |  | 作成時刻。 |
| update_time | [google.protobuf.Timestamp](#google-protobuf-Timestamp) |  | LAST-MODIFIED。 |






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


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| name | [string](#string) |  | リソース名（calendars/{id}/todos/{uid}）。 |
| etag | [string](#string) |  | 指定すると、保存されている etag と違うときに ABORTED を返す。 |






<a name="limani-v1-GetTodoRequest"></a>

### GetTodoRequest
GetTodoRequest は Todo を取得する。


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| name | [string](#string) |  | リソース名（calendars/{id}/todos/{uid}）。 |






<a name="limani-v1-ListTodosRequest"></a>

### ListTodosRequest
ListTodosRequest はカレンダー内の Todo を一覧する。


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| parent | [string](#string) |  | 親（calendars/{id}）。 |
| statuses | [TodoStatus](#limani-v1-TodoStatus) | repeated | 指定した status の Todo だけを返す。空なら絞り込まない。 |
| page_size | [int32](#int32) |  |  |
| page_token | [string](#string) |  |  |






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
| name | [string](#string) |  | リソース名（calendars/{id}/todos/{uid}）。 |
| status | [TodoStatus](#limani-v1-TodoStatus) |  |  |
| etag | [string](#string) |  | 指定すると、保存されている etag と違うときに ABORTED を返す。 |






<a name="limani-v1-UpdateTodoRequest"></a>

### UpdateTodoRequest
UpdateTodoRequest は Todo を更新する。

todo.etag を指定すると、保存されている etag と違うときに ABORTED を返す。
空なら競合を検出しない。


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| todo | [Todo](#limani-v1-Todo) |  | 更新する Todo。name で対象を決める。 |
| update_mask | [google.protobuf.FieldMask](#google-protobuf-FieldMask) |  | 更新するフィールド。次のどれか: summary, description, status, priority, percent_complete, dtstart, due, completed_time, categories, parent_uid, assignees。 |





 

 

 

 



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
| ListTodos | [ListTodosRequest](#limani-v1-ListTodosRequest) | [ListTodosResponse](#limani-v1-ListTodosResponse) |  |
| GetTodo | [GetTodoRequest](#limani-v1-GetTodoRequest) | [Todo](#limani-v1-Todo) |  |
| CreateTodo | [CreateTodoRequest](#limani-v1-CreateTodoRequest) | [Todo](#limani-v1-Todo) |  |
| UpdateTodo | [UpdateTodoRequest](#limani-v1-UpdateTodoRequest) | [Todo](#limani-v1-Todo) |  |
| SetTodoStatus | [SetTodoStatusRequest](#limani-v1-SetTodoStatusRequest) | [Todo](#limani-v1-Todo) |  |
| DeleteTodo | [DeleteTodoRequest](#limani-v1-DeleteTodoRequest) | [.google.protobuf.Empty](#google-protobuf-Empty) |  |

 



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

