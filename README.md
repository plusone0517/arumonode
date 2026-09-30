# あるもので — APP05

食材・残量・人数から12種類の基本レシピと不足分を探す家庭向けWebアプリ。

## できること

- 食材写真を端末内で解析し、候補を確認・修正して登録。現在の自動認識対象はブロッコリー、にんじん、りんご、バナナ、オレンジの5種類。候補の見落とし・誤認識があるため必ず本人確認。写真から分量は推定しません。
- 27種類の食材・調味料を手動登録、可食部分の分量を編集。空欄は不明として明示。
- 1〜6人分の材料計算、買い足しなし候補・あと1品まで・料理分類の絞り込み。
- 不足分の買い物メモ、購入チェック、レシピのお気に入り、調理手順のチェック。
- 避けたい原材料の目安・個別食材による除外。
- IndexedDBによる同一ブラウザー内保存。JSONバックアップと追加読み込み。

## 現在の範囲

レシピは編集済みの12種類から検索します。自由生成、栄養計算、病気に応じた食事指導、サプリ比較・購入は含みません。アレルギー設定は製品表示や混入の確認を代替しません。食材の鮮度・安全性は写真判定しません。写真はメモリー内のみで扱い、保存・外部送信しません。TensorFlow.js / COCO-SSDのモデルデータは初回にGoogleのモデル配信元から取得します。通信・機種により使えない場合は手動入力に切り替えられます。

サンプル食材は在庫に混ぜずお試し表示。買い足しメモへの追加は都度追加し、買ったチェックでは在庫を自動変更しません。分量不明は不足量に含めず「分量未確認」と表示します。水と下ゆで用の湯は別途用意。利用者間・端末間のクラウド同期はありません。

## 開発・配布

`source.zip` に編集用ソースを同梱。Node 22以降とpnpmで依存関係をインストールし、`node scripts/build-portable.mjs ./portable-build/index.html` で画像・CSS・JavaScriptを埋め込んだ単一HTMLを生成します。公開サイトはGitHub Pagesのmainブランチのルートを使用します。生成HTMLのみでレシピ・保存機能が動作し、写真解析時だけモデル取得通信が必要です。

主なファイル: app/page.tsx、app/globals.css、lib/recipes.ts、lib/storage.ts、lib/detect.ts。レシピを増やす際は材料ID・分量・調理手順・原材料タグを整合させてください。写真はAIで作成した盛りつけイメージです。

## 確認

10ケースの在庫・残量・人数・除外判定、全12レシピの食材IDと手順を確認。写真入力、候補の追加・修正、保存と再読み込み、買い足し、モバイル表示をブラウザーで検証。

食品加熱の参考: 厚生労働省「家庭での食中毒予防」
https://www.mhlw.go.jp/stf/seisakunitsuite/bunya/kenkou_iryou/shokuhin/syokuchu/01_00008.html

写真判定: TensorFlow.js 4.22.0 / @tensorflow-models/coco-ssd 2.2.3 (Apache-2.0)
https://github.com/tensorflow/tfjs-models/tree/master/coco-ssd

Built with React, Vite, Tailwind CSS, Radix UI / Base UI and Lucide. Dependencies retain their upstream licenses.
