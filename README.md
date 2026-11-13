# 留学費用シミュレーター（公開用）

セブ島留学バディー（cebu-buddy.com）の記事に埋め込む、費用シミュレーターです。`index.html` 1ファイルで動きます。
このフォルダは、公開用のGitHubリポジトリです（社内のデータは、入っていません）。

## 1. 公開する（最初の1回）
1. GitHubで、新しいリポジトリを作る（New repository）。名前は、例: `simulator`。**Public** を選ぶ。
2. このフォルダで、リモートを登録して、push する。
   ```bash
   git remote add origin https://github.com/（ユーザー名）/simulator.git
   git push -u origin main
   ```
3. GitHubのリポジトリの Settings → Pages → Source を「Deploy from a branch」、Branch を `main`・`/ (root)` にして Save。
4. 数分後、公開URLができる: `https://（ユーザー名）.github.io/simulator/`

## 2. WPの記事に貼る
### 2-1. 高さを自動で合わせるスクリプト（サイトに1回だけ）
テーマの「カスタムHTML」を入れられる場所（フッターなど）か、どれか1つの記事のカスタムHTMLに、1回だけ貼ります。

```html
<script>
window.addEventListener("message", function (e) {
  if (!e.data || e.data.type !== "sim-height") return;
  document.querySelectorAll("iframe.cb-sim").forEach(function (f) {
    if (f.contentWindow === e.source) f.style.height = e.data.height + "px";
  });
});
</script>
```

### 2-2. 記事に、iframeを貼る（記事ごと）
記事の「カスタムHTML」ブロックに、次の1行を貼ります。`school=` の値だけ、記事の学校に変えます。

```html
<iframe class="cb-sim" src="https://（ユーザー名）.github.io/simulator/?school=CIA" style="width:100%;border:0;height:720px" loading="lazy" title="留学費用シミュレーター"></iframe>
```

- `school=` を付けないと、学校の選択から始まります。
- `?school=GLC&course=gps&room=mtw&weeks=10` のように、コース・部屋・週数も、決めておけます（学校の下の項目は、あとから選べます）。

### 2-3. 本番の前に確認する
1. 下書きの固定ページを作り、カスタムHTMLにiframeを貼って、プレビューで表示を確認する。
2. 表示されない・枠の高さが合わないときは、WPのセキュリティ設定か、外注先のWEB制作の方に確認する。
3. 確認が済んでから、記事に貼る。

## 3. 料金を改定したとき（記事は、触りません）
1. 見積作成ツールの料金を直す。
2. 作成スクリプトで、`index.html` を作り直す（Claudeに頼めば実行します）。
3. このフォルダで、コミットして push する。GitHub Pagesが、自動で反映する。全部の記事に、同時に反映されます。

## 4. 仕様の要点
- 成人1名の単身留学の金額です。長期割引は、学校のルールのとおり。ウェブ限定の5%割引は、「授業料および寮費」から長期割引を引いた額にかけます（入学金などは対象外）。
- キャンペーン、繁忙期（ピークシーズン）の追加料金、オプション、空港ピックアップは、含みません。
- 為替: USD建ての学校は、過去1週間の最安値（Frankfurter API）。固定レートの学校は学校の固定レート。円建ての学校は為替なし。取得できないときは、金額を出しません。
- お客様の個人情報は、集めません。最後に選んだ条件は、お客様のブラウザ内にだけ、覚えます。

## 5. 学校のキー（`?school=` に入れる値）
| キー | 学校 |
|---|---|
| `AJ` | A&J e-Edu Academy |
| `BCEBU` | B'Cebu |
| `APIBECI_EOP` | BECI EOPキャンパス |
| `APIBECI_CITY` | BECI シティキャンパス |
| `APIBECI_SPARTA` | BECI スパルタキャンパス |
| `COCO` | Boracay Coco English Academy |
| `BRILLIANT` | Brilliant Cebu English Academy |
| `CBEA` | CBEA |
| `CBOA` | Cebu Blue Ocean Academy |
| `CELLA_PREMIUM` | CELLA Premium Campus |
| `CELLA_UNI` | CELLA Uni Sparta Campus |
| `CG_BANILAD` | CG Academy（Banilad キャンパス） |
| `CG_SPARTA` | CG Academy（スパルタキャンパス） |
| `CIA` | CIA（Cebu International Academy） |
| `CIEC` | CIEC |
| `CIP` | CIP English Academy |
| `WE_DORM` | CLARK WE ACADEMY |
| `WE_NR` | CLARK WE ACADEMY（RESIDENCE） |
| `CLC` | CLC（Campus Language Center） |
| `CPI` | CPI（Cebu Pelis Institute） |
| `CWA` | Curious World Academy |
| `EROOM` | E-Room Language Center |
| `EG` | EG ACADEMY |
| `EF1` | English Fella1 |
| `EF2` | English Fella2 |
| `EV` | EV Academy |
| `EVLM` | EV Academy La Mer |
| `FEGC` | First English Global College |
| `GENIUS` | Genius English |
| `GLC` | GLC（Global Language Cebu） |
| `IBREEZE_MAIN` | I.BREEZE Mainキャンパス |
| `IBREEZE_PRIME` | I.BREEZE Primeキャンパス |
| `IMS` | IMS（IMS Academy CEBU） |
| `JIC_CHALLENGER` | JICチャレンジャー校 |
| `JIC_PREMIUM` | JICプレミアム校 |
| `MERISE` | MeRISE |
| `MK` | MK EDUCATION |
| `MONOL_SPARTA` | MONOL スパルタキャンパス |
| `MONOL_MAIN` | MONOL メインキャンパス |
| `PHILINTER` | Philinter |
| `PILA` | PILA education |
| `PINES` | PINES International Academy |
| `SMEAG_CAPITAL` | SMEAG Capital |
| `SMEAG_ENCANTO` | SMEAG Encanto（個人留学） |
| `STARGATE` | Stargate |
| `TALK` | Talk Academy |
| `TARGET` | TARGET |
| `WALES` | WALES |
| `WE_ILOILO` | WE Academy ILOILO |
| `WINNING` | Winning English |
