# eigo-pwa

論文英語プリントの、スマホの採点画面。設計の正本は Obsidian Vault の `20_Projects/英語学習2026.md`「論文英語プリント」。
PC 側（紙のデータ・紙の生成・復習の選び方）は非公開リポジトリ `eigo-print`。

## 方針
- 紙で解き、□に書いた番号をここで押して採点する。**その場で ○× を出し**、× の問だけの「直し」の欄を足して、全部 ○ になるまで続ける（公文どおり）。技術士の答え入力（○× を出さない）とはここが違う。
- 開始・終了の時刻と、知らなかった語（紙で丸を付けた語）もここで入れる。
- **このリポジトリは公開**。問題文・原文・ヒントは入れない（画面のコードと Firebase の公開設定だけ）。

## データ（Firestore・プロジェクト `gijutsushi-pwa` を技術士と共用）
- `users/{uid}/eigo/{紙のid}` … PC（`eigo_sync.py push`）が `id`・`no`・`title`・`sub`・`items`・`sections`・`key`・`order` を置く。この画面が `start`・`end`・`unknown`・`rounds`・`doneAt`・`updatedAt` を足す。
- `users/{uid}/meta/eigo` … ログインの印。

ルールは技術士と同じ（`users/{uid}/**` を本人だけ読み書き）なので、Firebase 側の設定は増やしていない。

## 見本モード
`?demo` を付けて開くと、保存しない見本で動く（答えは全部 ①）。

## 配信（GitHub Pages）
- 公開URL `https://ykhandyssi-prog.github.io/eigo-pwa/`
- SW はネットワーク優先で即反映（必要なら `sw.js` の `CACHE` 版数を上げる）。同じオリジンのほかの PWA のキャッシュには触らない（接頭辞 `eg-` だけ消す）
