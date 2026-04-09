# who-is-yamashu

やましゅう（山本周）の自己紹介Q&Aページ。神山まるごと高専 2年生向け。

**GitHub Pages URL:** https://yamashu00.github.io/who-is-yamashu/

---

## 質問のストレージ設定（Google Apps Script）

学生が送った質問を Google スプレッドシートに自動で蓄積する設定。

### 1. スプレッドシートを作る

1. Google スプレッドシートを新規作成
2. シート名はそのまま（Sheet1）でOK
3. 1行目に見出しを入れる:
   - A1: `timestamp`
   - B1: `question`

### 2. Apps Script を書く

1. スプレッドシートのメニュー → **拡張機能 → Apps Script**
2. 以下のコードを貼り付けて保存:

```javascript
function doPost(e) {
  const sheet = SpreadsheetApp.getActiveSpreadsheet().getActiveSheet();
  const data  = JSON.parse(e.postData.contents);
  sheet.appendRow([data.timestamp, data.question]);
  return ContentService.createTextOutput('ok');
}
```

### 3. Web アプリとしてデプロイ

1. **デプロイ → 新しいデプロイ**
2. 種類: **ウェブアプリ**
3. 次のユーザーとして実行: **自分（自分のメールアドレス）**
4. アクセスできるユーザー: **全員**
5. **デプロイ** → URLをコピー

### 4. index.html に URL を貼る

`index.html` の以下の行を書き換える:

```js
// 変更前
const GAS_URL = 'YOUR_GAS_WEB_APP_URL';

// 変更後（例）
const GAS_URL = 'https://script.google.com/macros/s/XXXXXXXXX/exec';
```

---

## GitHub Pages の有効化

1. リポジトリの **Settings → Pages**
2. Source: **Deploy from a branch**
3. Branch: **main** / **(root)**
4. Save → しばらくすると `https://yamashu00.github.io/who-is-yamashu/` が公開される

---

## Q&A を追加・更新したいとき

`index.html` の該当セクションのカードを複製・編集するだけ。

```html
<div class="card" onclick="toggle(this)">
  <div class="card-q">
    <span class="card-q-text">質問テキスト</span>
    <span class="card-icon">+</span>
  </div>
  <div class="card-body">
    <div class="card-body-inner">回答テキスト</div>
  </div>
</div>
```
