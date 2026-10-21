## プロジェクト

limani の public API contract（protobuf）を管理する repository。実装は dai3no-me/limani にある。作業を始める前に [README.md](./README.md) を読むこと。

## 言語

ドキュメント・コメント・コミットメッセージは日本語で書く。コード上の識別子は英語。

## ルール

- proto は `limani/limani/v1/` に置く。package は `limani.v1`
- `buf lint`（STANDARD。例外は `buf.yaml` を参照）を通す
- リソース名は AIP 形式にする（例: `calendars/{id}/todos/{uid}`）
- breaking change を安易に行わない。`mise run breaking` で確かめる
- proto を編集したら `mise run docs` を実行し、`limani/README.md` の差分をコミットする
- private API（アプリパスワードなど）はここに置かない。dai3no-me/limani の `proto/` に置く
- 利用側（dai3no-me/limani）は、この repository を `pkg/gen/buf` で取得して TypeScript を生成する
