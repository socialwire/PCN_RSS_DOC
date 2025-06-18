# 連携RSS仕様書 \[2025.06.18\]

<br>

## 変更履歴

- 2025.06.18 : カテゴリ情報の配信に対応
- 2025.06.05 : RSSのパラメータにgtm\_idを追加

<br>

## はじめに

本RSS仕様書は作成途中のものとなり、実際の運用時に多少の変更が入いることがございます。

概要の把握としてご参照ください。

<br>

## RSS URL

以下のURLにて貴社専用の記事を配信させていただきます。

```
https://pcn-api.cowriter.jp/v1/rss?media={メディアID}&gtm_id={gtm_id}&limit=10&no_gtm=false
```

`メディアID`, `gtm_id` は、連携開始時にお伝えいたします。

`limit` は取得する件数となります。

`no_gtm` を `true` にセットすると、RSS内のGoogle Tag Manager のタグが入らなくなります。別途、`monolab:gtm_id` の値で追加していただくか、弊社のGA4 の測定IDをお渡ししますので、貴社GTMに追加をお願いいたします。

<br>

## RSS詳細

<br>

### 不使用要素

- channel.title
- channel.link
- channel.description
- channel.language
- channel.atom:link
- channel.item.link

<br>

<br>

### 使用要素

- channel.lastBuildDate : RSSの最終更新日
- channel.item.title: 記事のタイトル
- channel.item.description: サマリー。meta description にご使用くださし。
- channel.item.pubDate: 記事公開日
- channel.item.guid: この記事を表すユニークな値です。記事の更新、削除時にご利用ください。
- channel.item.monolab:eyecatchUrl: この記事のアイキャッチ用画像
- channel.item.monolab:deleted: 記事が削除されると、”true”$00A0 となりますので、貴社CMSでも削除をお願いいたします。
- channel.item.monolab:modDate: 最終更新日
- channel.item.content:encoded: 記事の本文（HTML形式）
- channel.item.monolab:markdown:$00A0記事の本文（マークダウン形式）
- channel.item.monolab:gtm\_id: Google Tag Manager の ID
- channel.item.enclosure: この記事のアイキャッチ用画像（channel.item.monolab:eyecatchUrlと同じ内容が常に入ります）

<br>

### カテゴリ情報

記事のカテゴリ情報を以下の要素で配信いたします：

- channel.item.monolab:category1: 大カテゴリ名
- channel.item.monolab:category2: 中カテゴリ名
- channel.item.monolab:category3: 小カテゴリ名
- channel.item.category: 標準RSS要素でのカテゴリ名

**カテゴリ構造について：**
- 3階層のカテゴリ構造を採用しています
- category1 > category2 > category3 の順で階層が深くなります
- カテゴリが設定されていない場合、該当要素は空になります

<br>

### 新規・更新・削除

- pubDate >=$00A0modDate の場合、新規記事（更新がない記事）となります
- 前回の取り込み時の modDate < 現在の$00A0modDate の場合、更新記事となります。貴社CMS上でも更新をお願いいたします。※前回の取り込み時の modDateを貴社のCMSにも保持してください。
- deletedが true の場合、削除記事となります。貴社CMSにおいても非公開化、あるいは、削除をお願いいたします。

<br>

### 画像の取り扱い

- RSS内に含まれる画像は、記事配布用となります。RSS読み込み時、貴社サーバーへの保存をお願いいたします。

<br>

## 具体例:

> [https://pcn-api.cowriter.jp/v1/rss?media=MONOLAB&gtm\_id=GTM-TZSPQCNDlimit=10&no\_gtm=false](https://pcn-api.cowriter.jp/v1/rss?media=MONOLAB&gtm_id=GTM-TZSPQCNDlimit=10&no_gtm=false "https://pcn-api.cowriter.jp/v1/rss?media=MONOLAB&gtm_id=GTM-TZSPQCNDlimit=10&no_gtm=false")  

より実際のデータを取得可能です。

<br>

```
<?xml version="1.0" ?>
  <rss xmlns:content="http://purl.org/rss/1.0/modules/content/" xmlns:atom="http://www.w3.org/2005/Atom" xmlns:monolab="http://pcn.cowriter.jp/rss/ns/1.0" version="2.0">
    <channel>
      <title>MONOLAB</title>
      <link>https://pcn-strapi.cowriter.jp/blog/MONOLAB</link>
      <description>MONOLAB用フィード</description>
      <language>ja-jp</language>
      <lastBuildDate>Thu, 22 May 2025 09:44:27 +0000</lastBuildDate>
      <atom:link href="https://pcn-strapi.cowriter.jp/api/rss/MONOLAB" rel="self" type="application/rss+xml"/>
      <item>
        <title>東京駅騒然！ミニオン東京ばな奈、ついに上陸$D83C$DF4C【期間限定】</title>
        <link>https://pcn-strapi.cowriter.jp/blog/MONOLAB/65</link>
        <description>「バナーナ！」の声が聞こえてきそう？ 関西で240万個売れた「東京ばな奈 ミニオン」がついに東京駅にやってくる！ 約2ヶ月の期間限定。この記事では、どこで買えるのか、どんな味がするのか、徹底的にご紹介します。今すぐチェックして、東京駅でミニオンたちを見つけよう！
</description>
        <pubDate>Tue, 06 May 2025 15:00:00 +0000</pubDate>
        <guid isPermaLink="false">MONOLAB-65</guid>
        <category>グルメ・食品</category>
        <monolab:eyecatchUrl>https://minio.monolab.tokyo/monolab/images/2310/319443aa-f5ab-4aec-82eb-caf9429f3476.webp</monolab:eyecatchUrl>
        <monolab:deleted>true</monolab:deleted>
        <monolab:category1>ライフスタイル</monolab:category1>
        <monolab:category2>食べ物・飲み物</monolab:category2>
        <monolab:category3>グルメ・食品</monolab:category3>
        <monolab:markdown>## 『東京ばな奈 ミニオン』が東京に初上陸！期間限定でミニオンたちをゲットしよう

ついに、あの**東京ばな奈 ミニオン** が東京にやってきます！$D83C$DF4C$D83C$DF4C$D83C$DF4C
2025年5月15日(木)から約2ヶ月間の期間限定で、JR東京駅 HANAGATAYAグランスタ東京中央通路店催事場にて先行販売されるんです。
以前から気になっていた方も、初めて知った方も、この機会を逃す手はありませんよ！

### 関西で大人気だった『東京ばな奈 ミニオン』、ついに東京へ！

![『東京ばな奈 ミニオン』が東京に初上陸！約2ヶ月間の期間限定販売](https://minio.monolab.tokyo/monolab/images/2310/5eb91adb-b2da-46ce-8ea8-d20d044b37bf.webp)

2022年に登場し、関西で240万個以上も売れたという**『東京ばな奈 ミニオン「見ぃつけたっ」 濃厚バナナカスタード味』** 。
「東京ばな奈」なのに東京で買えなかった、あの幻の商品がついに東京に上陸です！
これはもう、ミニオン好き、バナナ好き、そして東京ばな奈ファンにとっては見逃せないビッグニュースですよね。
約2ヶ月の期間限定なので、急いでゲットしに行きましょう！

### バナナ愛が炸裂！濃厚バナナカスタード味

![累計販売240万個超え！『東京ばな奈 ミニオン』が東京に初上陸？！](https://minio.monolab.tokyo/monolab/images/2310/80a9b43b-f0d4-4f88-a32b-744dc5f4b252.webp)
![バナナが大好きなミニオンのための、“濃厚バナナカスタード味”](https://minio.monolab.tokyo/monolab/images/2310/d79fc6ad-9324-4fb7-9d3d-fa07b94c102c.webp)

ミニオンといえば、やっぱりバナナ！$D83C$DF4C
**『東京ばな奈 ミニオン』** は、そんなミニオンたちのために、バナナカスタードの中のバナナを20％も増量しているんです。
想像してみてください、口に入れた瞬間に広がる濃厚なバナナの風味…！
これはもう、ミニオンと一緒に「バナーナ！」って叫びたくなっちゃいますね。

### どのミニオンに出会える？全5種類のデザイン

![どのミニオンに出会えるかな？表情豊かなデザインは全5種類！](https://minio.monolab.tokyo/monolab/images/2310/a335d388-f173-4e5c-932f-225376b2ff06.webp)

ふわふわのスポンジケーキには、**ボブ、スチュアート、ケビン、カール、オットー** 、5種類のミニオンたちが描かれています。
どのミニオンに出会えるかは、箱を開けるまでのお楽しみ！
全部集めたくなっちゃいますよね。
（※1箱にすべてのお菓子の絵柄が揃わない場合があるとのことなので、ご注意ください。）

### 商品情報と購入方法


*   **商品名:** 東京ばな奈 ミニオン「見ぃつけたっ」 濃厚バナナカスタード味
*   **価格:**
    *   4個入 税込842円(本体価格780円)
    *   8個入 税込1,512円(本体価格1,400円)

このクオリティでこの価格なら、コスパも悪くないと思います！
ちょっとしたお土産にもぴったりですよね。

**購入方法**

*   **先行販売:** 2025年5月15日(木)～5月21日(水) JR東京駅構内 HANAGATAYA グランスタ東京中央通路店催事場
    *   先行販売で購入すると、オリジナルステッカーがもらえます！（数量限定）
*   **通常販売:** 2025年5月22日(木)～7月末ごろまで
    *   東京ばな奈s(JR東京駅 八重洲地下中央改札外)
    *   東京ばな奈スタジオ 1F-STUDIO 大丸東京店
    *   その他、東京駅、品川駅、羽田空港、成田空港など

私は先行販売でステッカーをゲットしたいので、初日にJR東京駅にダッシュする予定です！$D83C$DFC3$200D♀$FE0F$D83D$DCA8

### 期間限定！スマホのオリジナル壁紙もプレゼント

![【初登場】スマートフォンのオリジナル壁紙を期間限定プレゼント！](https://minio.monolab.tokyo/monolab/images/2310/aa52f197-06e9-4907-acfb-e517f329309c.webp)

2025年5月8日(木)$301C5月21日(水)の期間限定で、『東京ばな奈 ミニオン』のパッケージとお揃いの、スマートフォンオリジナル壁紙が公式HPでダウンロードできます。
これは嬉しいサプライズ！
早速ダウンロードして、スマホもミニオン仕様にしちゃいましょう！
[公式HPはこちら](https://www.tokyobanana.jp/products/banana_minion.html)

### 株式会社グレープストーン について

**東京ばな奈ワールド** を展開する株式会社グレープストーンは、1991年に“新しい時代の東京みやげ”として誕$2F63した『東京ばな奈』から始まったスイーツブランドです。
長年愛されている東京土産の定番ですよね。
バナナのおいしさにこだわったスイーツは、日本国内だけでなく海外からの旅行客にも人気があります。
[東京ばな奈ワールド公式HP](https://www.tokyobanana.jp/)

### まとめ


『東京ばな奈 ミニオン』の東京初上陸は、ミニオンファン、東京ばな奈ファンにとって、絶対に**見逃せない** イベントです！
期間限定なので、早めにゲットして、濃厚なバナナカスタード味と可愛いミニオンデザインを楽しんでくださいね。
私も今から楽しみで仕方ありません！
東京駅でミニオンたちに会えるのを楽しみにしています！$D83C$DF4C$D83D$DC9B

</monolab:markdown>
        <monolab:modDate>Thu, 08 May 2025 09:32:33 +0000</monolab:modDate>
        <monolab:gtm_id>GTM-TZSPQCND</monolab:gtm_id>
        <content:encoded>&lt;![CDATA[&lt;h2&gt;『東京ばな奈 ミニオン』が東京に初上陸！期間限定でミニオンたちをゲットしよう&lt;/h2&gt;
&lt;p&gt;ついに、あの&lt;strong&gt;東京ばな奈 ミニオン&lt;/strong&gt; が東京にやってきます！$D83C$DF4C$D83C$DF4C$D83C$DF4C
2025年5月15日(木)から約2ヶ月間の期間限定で、JR東京駅 HANAGATAYAグランスタ東京中央通路店催事場にて先行販売されるんです。
以前から気になっていた方も、初めて知った方も、この機会を逃す手はありませんよ！&lt;/p&gt;
&lt;h3&gt;関西で大人気だった『東京ばな奈 ミニオン』、ついに東京へ！&lt;/h3&gt;
&lt;p&gt;&lt;img alt=&quot;『東京ばな奈 ミニオン』が東京に初上陸！約2ヶ月間の期間限定販売&quot; src=&quot;https://minio.monolab.tokyo/monolab/images/2310/5eb91adb-b2da-46ce-8ea8-d20d044b37bf.webp&quot; /&gt;&lt;/p&gt;
&lt;p&gt;2022年に登場し、関西で240万個以上も売れたという&lt;strong&gt;『東京ばな奈 ミニオン「見ぃつけたっ」 濃厚バナナカスタード味』&lt;/strong&gt; 。
「東京ばな奈」なのに東京で買えなかった、あの幻の商品がついに東京に上陸です！
これはもう、ミニオン好き、バナナ好き、そして東京ばな奈ファンにとっては見逃せないビッグニュースですよね。
約2ヶ月の期間限定なので、急いでゲットしに行きましょう！&lt;/p&gt;
&lt;h3&gt;バナナ愛が炸裂！濃厚バナナカスタード味&lt;/h3&gt;
&lt;p&gt;&lt;img alt=&quot;累計販売240万個超え！『東京ばな奈 ミニオン』が東京に初上陸？！&quot; src=&quot;https://minio.monolab.tokyo/monolab/images/2310/80a9b43b-f0d4-4f88-a32b-744dc5f4b252.webp&quot; /&gt;
&lt;img alt=&quot;バナナが大好きなミニオンのための、“濃厚バナナカスタード味”&quot; src=&quot;https://minio.monolab.tokyo/monolab/images/2310/d79fc6ad-9324-4fb7-9d3d-fa07b94c102c.webp&quot; /&gt;&lt;/p&gt;
&lt;p&gt;ミニオンといえば、やっぱりバナナ！$D83C$DF4C
&lt;strong&gt;『東京ばな奈 ミニオン』&lt;/strong&gt; は、そんなミニオンたちのために、バナナカスタードの中のバナナを20％も増量しているんです。
想像してみてください、口に入れた瞬間に広がる濃厚なバナナの風味…！
これはもう、ミニオンと一緒に「バナーナ！」って叫びたくなっちゃいますね。&lt;/p&gt;
&lt;h3&gt;どのミニオンに出会える？全5種類のデザイン&lt;/h3&gt;
&lt;p&gt;&lt;img alt=&quot;どのミニオンに出会えるかな？表情豊かなデザインは全5種類！&quot; src=&quot;https://minio.monolab.tokyo/monolab/images/2310/a335d388-f173-4e5c-932f-225376b2ff06.webp&quot; /&gt;&lt;/p&gt;
&lt;p&gt;ふわふわのスポンジケーキには、&lt;strong&gt;ボブ、スチュアート、ケビン、カール、オットー&lt;/strong&gt; 、5種類のミニオンたちが描かれています。
どのミニオンに出会えるかは、箱を開けるまでのお楽しみ！
全部集めたくなっちゃいますよね。
（※1箱にすべてのお菓子の絵柄が揃わない場合があるとのことなので、ご注意ください。）&lt;/p&gt;
&lt;h3&gt;商品情報と購入方法&lt;/h3&gt;
&lt;ul&gt;
&lt;li&gt;&lt;strong&gt;商品名:&lt;/strong&gt; 東京ばな奈 ミニオン「見ぃつけたっ」 濃厚バナナカスタード味&lt;/li&gt;
&lt;li&gt;&lt;strong&gt;価格:&lt;/strong&gt;&lt;ul&gt;
&lt;li&gt;4個入 税込842円(本体価格780円)&lt;/li&gt;
&lt;li&gt;8個入 税込1,512円(本体価格1,400円)&lt;/li&gt;
&lt;/ul&gt;
&lt;/li&gt;
&lt;/ul&gt;
&lt;p&gt;このクオリティでこの価格なら、コスパも悪くないと思います！
ちょっとしたお土産にもぴったりですよね。&lt;/p&gt;
&lt;p&gt;&lt;strong&gt;購入方法&lt;/strong&gt;&lt;/p&gt;
&lt;ul&gt;
&lt;li&gt;&lt;strong&gt;先行販売:&lt;/strong&gt; 2025年5月15日(木)～5月21日(水) JR東京駅構内 HANAGATAYA グランスタ東京中央通路店催事場&lt;ul&gt;
&lt;li&gt;先行販売で購入すると、オリジナルステッカーがもらえます！（数量限定）&lt;/li&gt;
&lt;/ul&gt;
&lt;/li&gt;
&lt;li&gt;&lt;strong&gt;通常販売:&lt;/strong&gt; 2025年5月22日(木)～7月末ごろまで&lt;ul&gt;
&lt;li&gt;東京ばな奈s(JR東京駅 八重洲地下中央改札外)&lt;/li&gt;
&lt;li&gt;東京ばな奈スタジオ 1F-STUDIO 大丸東京店&lt;/li&gt;
&lt;li&gt;その他、東京駅、品川駅、羽田空港、成田空港など&lt;/li&gt;
&lt;/ul&gt;
&lt;/li&gt;
&lt;/ul&gt;
&lt;p&gt;私は先行販売でステッカーをゲットしたいので、初日にJR東京駅にダッシュする予定です！$D83C$DFC3$200D♀$FE0F$D83D$DCA8&lt;/p&gt;
&lt;h3&gt;期間限定！スマホのオリジナル壁紙もプレゼント&lt;/h3&gt;
&lt;p&gt;&lt;img alt=&quot;【初登場】スマートフォンのオリジナル壁紙を期間限定プレゼント！&quot; src=&quot;https://minio.monolab.tokyo/monolab/images/2310/aa52f197-06e9-4907-acfb-e517f329309c.webp&quot; /&gt;&lt;/p&gt;
&lt;p&gt;2025年5月8日(木)$301C5月21日(水)の期間限定で、『東京ばな奈 ミニオン』のパッケージとお揃いの、スマートフォンオリジナル壁紙が公式HPでダウンロードできます。
これは嬉しいサプライズ！
早速ダウンロードして、スマホもミニオン仕様にしちゃいましょう！
&lt;a href=&quot;https://www.tokyobanana.jp/products/banana_minion.html&quot;&gt;公式HPはこちら&lt;/a&gt;&lt;/p&gt;
&lt;h3&gt;株式会社グレープストーン について&lt;/h3&gt;
&lt;p&gt;&lt;strong&gt;東京ばな奈ワールド&lt;/strong&gt; を展開する株式会社グレープストーンは、1991年に“新しい時代の東京みやげ”として誕$2F63した『東京ばな奈』から始まったスイーツブランドです。
長年愛されている東京土産の定番ですよね。
バナナのおいしさにこだわったスイーツは、日本国内だけでなく海外からの旅行客にも人気があります。
&lt;a href=&quot;https://www.tokyobanana.jp/&quot;&gt;東京ばな奈ワールド公式HP&lt;/a&gt;&lt;/p&gt;
&lt;h3&gt;まとめ&lt;/h3&gt;
&lt;p&gt;『東京ばな奈 ミニオン』の東京初上陸は、ミニオンファン、東京ばな奈ファンにとって、絶対に&lt;strong&gt;見逃せない&lt;/strong&gt; イベントです！
期間限定なので、早めにゲットして、濃厚なバナナカスタード味と可愛いミニオンデザインを楽しんでくださいね。
私も今から楽しみで仕方ありません！
東京駅でミニオンたちに会えるのを楽しみにしています！$D83C$DF4C$D83D$DC9B&lt;/p&gt;

&lt;!-- Google Tag Manager --&gt;
&lt;script&gt;(function(w,d,s,l,i){w[l]=w[l]||[];w[l].push({'gtm.start':
new Date().getTime(),event:'gtm.js'});var f=d.getElementsByTagName(s)[0],
j=d.createElement(s),dl=l!='dataLayer'?'&amp;l='+l:'';j.async=true;j.src=
'https://www.googletagmanager.com/gtm.js?id='+i+dl;f.parentNode.insertBefore(j,f);
})(window,document,'script','dataLayer','GTM-TZSPQCND');&lt;/script&gt;
&lt;!-- End Google Tag Manager --&gt;
&lt;!-- Google Tag Manager (noscript) --&gt;
&lt;noscript&gt;&lt;iframe src=&quot;https://www.googletagmanager.com/ns.html?id=GTM-TZSPQCND&quot;
height=&quot;0&quot; width=&quot;0&quot; style=&quot;display:none;visibility:hidden&quot;&gt;&lt;/iframe&gt;&lt;/noscript&gt;
&lt;!-- End Google Tag Manager (noscript) --&gt;
]]&gt;</content:encoded>
        <enclosure url="https://minio.monolab.tokyo/monolab/images/2310/319443aa-f5ab-4aec-82eb-caf9429f3476.webp" type="image/webp" length="0"/>
      </item>
    </channel>
  </rss>
```
