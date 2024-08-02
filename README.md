# 最高の避暑地はどこ？

<div align="right">
朝日新聞デジタル企画報道部　小宮山亮磨  <br>
@ryomakom  <br>
2024/8/23  </div>



「最高の避暑地はどこにある？100年分の気象庁データから探ってみた」という記事を、「ウィズニュース」に[掲載しました](https://)。気象庁が気温などを観測している全国1300カ所超の観測所のうち、1924年以降の、つまり過去100年分のデータがあるところをみつけて、それぞれで8月の気温がどのように変化してきたかを調べた、というものです。

データは[jmastatsというライブラリ](https://uribo.quarto.pub/jmastats_heatmap/)を使い、気象庁のサイトから取得しました。以下のコードにあるとおり、まず全観測所に対して1924年のデータを要求し、この時点から観測を続けている77の観測所を特定。で、その77観測所から、1924～2023年について、各年の8月のデータを取得する、という手続きをとりました。

jmastatsは気象庁のサイトに負荷をかけすぎないよう、データを1個とるごとに7秒の間隔を空けるので、全部をとるには丸一日近くかかりました。自分でスクレーピングのコードをかけば短縮はできますが、いろんな意味でお薦めはしません。

というわけで、データを取得し、また100年間での気温変化と、2023年までの直近5年間の気温を表として出力するためのコードは、以下の通りです。


<table>
 <thead>
  <tr>
   <th style="text-align:left;"> area </th>
   <th style="text-align:left;"> station_name </th>
   <th style="text-align:right;"> station_no </th>
   <th style="text-align:left;"> block_no </th>
   <th style="text-align:right;"> change </th>
   <th style="text-align:right;"> p.value </th>
   <th style="text-align:right;"> latest_average </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:left;"> 上川 </td>
   <td style="text-align:left;"> 旭川 </td>
   <td style="text-align:right;"> 12442 </td>
   <td style="text-align:left;"> 47407 </td>
   <td style="text-align:right;"> 0.5637254 </td>
   <td style="text-align:right;"> 0.2756023 </td>
   <td style="text-align:right;"> 22.16774 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 留萌 </td>
   <td style="text-align:left;"> 羽幌 </td>
   <td style="text-align:right;"> 13181 </td>
   <td style="text-align:left;"> 47404 </td>
   <td style="text-align:right;"> 0.8434560 </td>
   <td style="text-align:right;"> 0.0853716 </td>
   <td style="text-align:right;"> 21.94323 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 石狩 </td>
   <td style="text-align:left;"> 札幌 </td>
   <td style="text-align:right;"> 14163 </td>
   <td style="text-align:left;"> 47412 </td>
   <td style="text-align:right;"> 1.4899180 </td>
   <td style="text-align:right;"> 0.0034970 </td>
   <td style="text-align:right;"> 23.63032 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 後志 </td>
   <td style="text-align:left;"> 寿都 </td>
   <td style="text-align:right;"> 16252 </td>
   <td style="text-align:left;"> 47421 </td>
   <td style="text-align:right;"> 0.0684030 </td>
   <td style="text-align:right;"> 0.8844625 </td>
   <td style="text-align:right;"> 22.28323 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 網走・北見・紋別 </td>
   <td style="text-align:left;"> 網走 </td>
   <td style="text-align:right;"> 17341 </td>
   <td style="text-align:left;"> 47409 </td>
   <td style="text-align:right;"> 0.4368050 </td>
   <td style="text-align:right;"> 0.4746105 </td>
   <td style="text-align:right;"> 20.50516 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 根室 </td>
   <td style="text-align:left;"> 根室 </td>
   <td style="text-align:right;"> 18273 </td>
   <td style="text-align:left;"> 47420 </td>
   <td style="text-align:right;"> 0.2212305 </td>
   <td style="text-align:right;"> 0.6871794 </td>
   <td style="text-align:right;"> 18.56387 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 釧路 </td>
   <td style="text-align:left;"> 釧路 </td>
   <td style="text-align:right;"> 19432 </td>
   <td style="text-align:left;"> 47418 </td>
   <td style="text-align:right;"> 0.6921673 </td>
   <td style="text-align:right;"> 0.1581773 </td>
   <td style="text-align:right;"> 19.54323 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 十勝 </td>
   <td style="text-align:left;"> 帯広 </td>
   <td style="text-align:right;"> 20432 </td>
   <td style="text-align:left;"> 47417 </td>
   <td style="text-align:right;"> 0.4942714 </td>
   <td style="text-align:right;"> 0.3481288 </td>
   <td style="text-align:right;"> 21.33226 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 胆振 </td>
   <td style="text-align:left;"> 室蘭 </td>
   <td style="text-align:right;"> 21323 </td>
   <td style="text-align:left;"> 47423 </td>
   <td style="text-align:right;"> -0.3841391 </td>
   <td style="text-align:right;"> 0.4237865 </td>
   <td style="text-align:right;"> 21.83290 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 渡島 </td>
   <td style="text-align:left;"> 函館 </td>
   <td style="text-align:right;"> 23232 </td>
   <td style="text-align:left;"> 47430 </td>
   <td style="text-align:right;"> 0.7070391 </td>
   <td style="text-align:right;"> 0.1478292 </td>
   <td style="text-align:right;"> 23.40710 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 青森 </td>
   <td style="text-align:left;"> 青森 </td>
   <td style="text-align:right;"> 31312 </td>
   <td style="text-align:left;"> 47575 </td>
   <td style="text-align:right;"> 1.2824211 </td>
   <td style="text-align:right;"> 0.0094141 </td>
   <td style="text-align:right;"> 25.03032 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 秋田 </td>
   <td style="text-align:left;"> 秋田 </td>
   <td style="text-align:right;"> 32402 </td>
   <td style="text-align:left;"> 47582 </td>
   <td style="text-align:right;"> 1.5865141 </td>
   <td style="text-align:right;"> 0.0005063 </td>
   <td style="text-align:right;"> 26.64194 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 岩手 </td>
   <td style="text-align:left;"> 盛岡 </td>
   <td style="text-align:right;"> 33431 </td>
   <td style="text-align:left;"> 47584 </td>
   <td style="text-align:right;"> 1.0883211 </td>
   <td style="text-align:right;"> 0.0208526 </td>
   <td style="text-align:right;"> 25.13935 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 岩手 </td>
   <td style="text-align:left;"> 宮古 </td>
   <td style="text-align:right;"> 33472 </td>
   <td style="text-align:left;"> 47585 </td>
   <td style="text-align:right;"> -0.2438354 </td>
   <td style="text-align:right;"> 0.6340998 </td>
   <td style="text-align:right;"> 23.89806 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 宮城 </td>
   <td style="text-align:left;"> 石巻 </td>
   <td style="text-align:right;"> 34292 </td>
   <td style="text-align:left;"> 47592 </td>
   <td style="text-align:right;"> 0.1760866 </td>
   <td style="text-align:right;"> 0.6896097 </td>
   <td style="text-align:right;"> 25.24323 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 山形 </td>
   <td style="text-align:left;"> 山形 </td>
   <td style="text-align:right;"> 35426 </td>
   <td style="text-align:left;"> 47588 </td>
   <td style="text-align:right;"> 1.2779091 </td>
   <td style="text-align:right;"> 0.0038522 </td>
   <td style="text-align:right;"> 26.63935 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 福島 </td>
   <td style="text-align:left;"> 福島 </td>
   <td style="text-align:right;"> 36127 </td>
   <td style="text-align:left;"> 47595 </td>
   <td style="text-align:right;"> 1.1776139 </td>
   <td style="text-align:right;"> 0.0138159 </td>
   <td style="text-align:right;"> 27.04839 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 福島 </td>
   <td style="text-align:left;"> 小名浜 </td>
   <td style="text-align:right;"> 36846 </td>
   <td style="text-align:left;"> 47598 </td>
   <td style="text-align:right;"> 1.3012478 </td>
   <td style="text-align:right;"> 0.0003748 </td>
   <td style="text-align:right;"> 25.91226 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 茨城 </td>
   <td style="text-align:left;"> 水戸 </td>
   <td style="text-align:right;"> 40201 </td>
   <td style="text-align:left;"> 47629 </td>
   <td style="text-align:right;"> 1.6618739 </td>
   <td style="text-align:right;"> 0.0000495 </td>
   <td style="text-align:right;"> 27.20258 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 茨城 </td>
   <td style="text-align:left;"> つくば </td>
   <td style="text-align:right;"> 40336 </td>
   <td style="text-align:left;"> 47646 </td>
   <td style="text-align:right;"> 1.8747344 </td>
   <td style="text-align:right;"> 0.0000011 </td>
   <td style="text-align:right;"> 27.33871 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 栃木 </td>
   <td style="text-align:left;"> 宇都宮 </td>
   <td style="text-align:right;"> 41277 </td>
   <td style="text-align:left;"> 47615 </td>
   <td style="text-align:right;"> 1.9878536 </td>
   <td style="text-align:right;"> 0.0000003 </td>
   <td style="text-align:right;"> 27.38258 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 群馬 </td>
   <td style="text-align:left;"> 前橋 </td>
   <td style="text-align:right;"> 42251 </td>
   <td style="text-align:left;"> 47624 </td>
   <td style="text-align:right;"> 2.5925476 </td>
   <td style="text-align:right;"> 0.0000000 </td>
   <td style="text-align:right;"> 28.38194 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 埼玉 </td>
   <td style="text-align:left;"> 熊谷 </td>
   <td style="text-align:right;"> 43056 </td>
   <td style="text-align:left;"> 47626 </td>
   <td style="text-align:right;"> 2.5583326 </td>
   <td style="text-align:right;"> 0.0000000 </td>
   <td style="text-align:right;"> 28.61032 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 東京 </td>
   <td style="text-align:left;"> 東京 </td>
   <td style="text-align:right;"> 44132 </td>
   <td style="text-align:left;"> 47662 </td>
   <td style="text-align:right;"> 1.8846046 </td>
   <td style="text-align:right;"> 0.0000013 </td>
   <td style="text-align:right;"> 28.32000 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 東京 </td>
   <td style="text-align:left;"> 八丈島 </td>
   <td style="text-align:right;"> 44263 </td>
   <td style="text-align:left;"> 47678 </td>
   <td style="text-align:right;"> 0.3614549 </td>
   <td style="text-align:right;"> 0.0620210 </td>
   <td style="text-align:right;"> 27.07032 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 千葉 </td>
   <td style="text-align:left;"> 銚子 </td>
   <td style="text-align:right;"> 45147 </td>
   <td style="text-align:left;"> 47648 </td>
   <td style="text-align:right;"> 1.1712939 </td>
   <td style="text-align:right;"> 0.0006486 </td>
   <td style="text-align:right;"> 26.66516 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 千葉 </td>
   <td style="text-align:left;"> 勝浦 </td>
   <td style="text-align:right;"> 45371 </td>
   <td style="text-align:left;"> 47674 </td>
   <td style="text-align:right;"> 1.1340495 </td>
   <td style="text-align:right;"> 0.0000942 </td>
   <td style="text-align:right;"> 26.76323 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 神奈川 </td>
   <td style="text-align:left;"> 横浜 </td>
   <td style="text-align:right;"> 46106 </td>
   <td style="text-align:left;"> 47670 </td>
   <td style="text-align:right;"> 2.0101700 </td>
   <td style="text-align:right;"> 0.0000000 </td>
   <td style="text-align:right;"> 28.33871 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 長野 </td>
   <td style="text-align:left;"> 長野 </td>
   <td style="text-align:right;"> 48156 </td>
   <td style="text-align:left;"> 47610 </td>
   <td style="text-align:right;"> 1.4194032 </td>
   <td style="text-align:right;"> 0.0000667 </td>
   <td style="text-align:right;"> 26.66000 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 長野 </td>
   <td style="text-align:left;"> 松本 </td>
   <td style="text-align:right;"> 48361 </td>
   <td style="text-align:left;"> 47618 </td>
   <td style="text-align:right;"> 2.2020867 </td>
   <td style="text-align:right;"> 0.0000000 </td>
   <td style="text-align:right;"> 26.18710 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 長野 </td>
   <td style="text-align:left;"> 飯田 </td>
   <td style="text-align:right;"> 48767 </td>
   <td style="text-align:left;"> 47637 </td>
   <td style="text-align:right;"> 1.4703522 </td>
   <td style="text-align:right;"> 0.0000003 </td>
   <td style="text-align:right;"> 25.91806 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 山梨 </td>
   <td style="text-align:left;"> 甲府 </td>
   <td style="text-align:right;"> 49142 </td>
   <td style="text-align:left;"> 47638 </td>
   <td style="text-align:right;"> 2.2732209 </td>
   <td style="text-align:right;"> 0.0000000 </td>
   <td style="text-align:right;"> 27.93548 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 静岡 </td>
   <td style="text-align:left;"> 浜松 </td>
   <td style="text-align:right;"> 50456 </td>
   <td style="text-align:left;"> 47654 </td>
   <td style="text-align:right;"> 2.2748120 </td>
   <td style="text-align:right;"> 0.0000000 </td>
   <td style="text-align:right;"> 28.42774 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 愛知 </td>
   <td style="text-align:left;"> 名古屋 </td>
   <td style="text-align:right;"> 51106 </td>
   <td style="text-align:left;"> 47636 </td>
   <td style="text-align:right;"> 2.5927954 </td>
   <td style="text-align:right;"> 0.0000000 </td>
   <td style="text-align:right;"> 29.01032 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 岐阜 </td>
   <td style="text-align:left;"> 高山 </td>
   <td style="text-align:right;"> 52146 </td>
   <td style="text-align:left;"> 47617 </td>
   <td style="text-align:right;"> 1.9818724 </td>
   <td style="text-align:right;"> 0.0000000 </td>
   <td style="text-align:right;"> 25.22000 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 岐阜 </td>
   <td style="text-align:left;"> 岐阜 </td>
   <td style="text-align:right;"> 52586 </td>
   <td style="text-align:left;"> 47632 </td>
   <td style="text-align:right;"> 2.5902674 </td>
   <td style="text-align:right;"> 0.0000000 </td>
   <td style="text-align:right;"> 29.05871 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 三重 </td>
   <td style="text-align:left;"> 津 </td>
   <td style="text-align:right;"> 53133 </td>
   <td style="text-align:left;"> 47651 </td>
   <td style="text-align:right;"> 2.0704199 </td>
   <td style="text-align:right;"> 0.0000000 </td>
   <td style="text-align:right;"> 28.62903 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 新潟 </td>
   <td style="text-align:left;"> 相川 </td>
   <td style="text-align:right;"> 54157 </td>
   <td style="text-align:left;"> 47602 </td>
   <td style="text-align:right;"> 0.7710384 </td>
   <td style="text-align:right;"> 0.0779116 </td>
   <td style="text-align:right;"> 27.25871 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 新潟 </td>
   <td style="text-align:left;"> 新潟 </td>
   <td style="text-align:right;"> 54232 </td>
   <td style="text-align:left;"> 47604 </td>
   <td style="text-align:right;"> 1.3095884 </td>
   <td style="text-align:right;"> 0.0018013 </td>
   <td style="text-align:right;"> 27.81548 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 新潟 </td>
   <td style="text-align:left;"> 高田 </td>
   <td style="text-align:right;"> 54651 </td>
   <td style="text-align:left;"> 47612 </td>
   <td style="text-align:right;"> 1.2081995 </td>
   <td style="text-align:right;"> 0.0016722 </td>
   <td style="text-align:right;"> 27.71097 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 富山 </td>
   <td style="text-align:left;"> 伏木 </td>
   <td style="text-align:right;"> 55091 </td>
   <td style="text-align:left;"> 47606 </td>
   <td style="text-align:right;"> 1.1408980 </td>
   <td style="text-align:right;"> 0.0023074 </td>
   <td style="text-align:right;"> 27.86903 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 石川 </td>
   <td style="text-align:left;"> 金沢 </td>
   <td style="text-align:right;"> 56227 </td>
   <td style="text-align:left;"> 47605 </td>
   <td style="text-align:right;"> 2.3515248 </td>
   <td style="text-align:right;"> 0.0000000 </td>
   <td style="text-align:right;"> 28.52065 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 福井 </td>
   <td style="text-align:left;"> 福井 </td>
   <td style="text-align:right;"> 57066 </td>
   <td style="text-align:left;"> 47616 </td>
   <td style="text-align:right;"> 1.7844184 </td>
   <td style="text-align:right;"> 0.0000012 </td>
   <td style="text-align:right;"> 28.45677 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 福井 </td>
   <td style="text-align:left;"> 敦賀 </td>
   <td style="text-align:right;"> 57248 </td>
   <td style="text-align:left;"> 47631 </td>
   <td style="text-align:right;"> 2.2495650 </td>
   <td style="text-align:right;"> 0.0000000 </td>
   <td style="text-align:right;"> 28.66194 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 滋賀 </td>
   <td style="text-align:left;"> 彦根 </td>
   <td style="text-align:right;"> 60131 </td>
   <td style="text-align:left;"> 47761 </td>
   <td style="text-align:right;"> 2.0092351 </td>
   <td style="text-align:right;"> 0.0000000 </td>
   <td style="text-align:right;"> 28.42581 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 京都 </td>
   <td style="text-align:left;"> 京都 </td>
   <td style="text-align:right;"> 61286 </td>
   <td style="text-align:left;"> 47759 </td>
   <td style="text-align:right;"> 2.6269562 </td>
   <td style="text-align:right;"> 0.0000000 </td>
   <td style="text-align:right;"> 29.37032 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 大阪 </td>
   <td style="text-align:left;"> 大阪 </td>
   <td style="text-align:right;"> 62078 </td>
   <td style="text-align:left;"> 47772 </td>
   <td style="text-align:right;"> 2.0441063 </td>
   <td style="text-align:right;"> 0.0000000 </td>
   <td style="text-align:right;"> 29.46710 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 兵庫 </td>
   <td style="text-align:left;"> 豊岡 </td>
   <td style="text-align:right;"> 63051 </td>
   <td style="text-align:left;"> 47747 </td>
   <td style="text-align:right;"> 1.7497343 </td>
   <td style="text-align:right;"> 0.0000016 </td>
   <td style="text-align:right;"> 28.20000 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 兵庫 </td>
   <td style="text-align:left;"> 神戸 </td>
   <td style="text-align:right;"> 63518 </td>
   <td style="text-align:left;"> 47770 </td>
   <td style="text-align:right;"> 2.0132805 </td>
   <td style="text-align:right;"> 0.0000000 </td>
   <td style="text-align:right;"> 29.10194 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 兵庫 </td>
   <td style="text-align:left;"> 洲本 </td>
   <td style="text-align:right;"> 63571 </td>
   <td style="text-align:left;"> 47776 </td>
   <td style="text-align:right;"> 0.8830599 </td>
   <td style="text-align:right;"> 0.0035705 </td>
   <td style="text-align:right;"> 28.12774 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 和歌山 </td>
   <td style="text-align:left;"> 和歌山 </td>
   <td style="text-align:right;"> 65042 </td>
   <td style="text-align:left;"> 47777 </td>
   <td style="text-align:right;"> 2.1574616 </td>
   <td style="text-align:right;"> 0.0000000 </td>
   <td style="text-align:right;"> 28.88000 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 和歌山 </td>
   <td style="text-align:left;"> 潮岬 </td>
   <td style="text-align:right;"> 65356 </td>
   <td style="text-align:left;"> 47778 </td>
   <td style="text-align:right;"> 1.1908888 </td>
   <td style="text-align:right;"> 0.0000002 </td>
   <td style="text-align:right;"> 27.41419 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 岡山 </td>
   <td style="text-align:left;"> 岡山 </td>
   <td style="text-align:right;"> 66408 </td>
   <td style="text-align:left;"> 47768 </td>
   <td style="text-align:right;"> 2.2340118 </td>
   <td style="text-align:right;"> 0.0000000 </td>
   <td style="text-align:right;"> 28.77419 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 広島 </td>
   <td style="text-align:left;"> 広島 </td>
   <td style="text-align:right;"> 67437 </td>
   <td style="text-align:left;"> 47765 </td>
   <td style="text-align:right;"> 2.4071601 </td>
   <td style="text-align:right;"> 0.0000000 </td>
   <td style="text-align:right;"> 29.00581 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 広島 </td>
   <td style="text-align:left;"> 呉 </td>
   <td style="text-align:right;"> 67511 </td>
   <td style="text-align:left;"> 47766 </td>
   <td style="text-align:right;"> 0.8781299 </td>
   <td style="text-align:right;"> 0.0042014 </td>
   <td style="text-align:right;"> 28.41226 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 島根 </td>
   <td style="text-align:left;"> 浜田 </td>
   <td style="text-align:right;"> 68376 </td>
   <td style="text-align:left;"> 47755 </td>
   <td style="text-align:right;"> 1.3901571 </td>
   <td style="text-align:right;"> 0.0001484 </td>
   <td style="text-align:right;"> 27.66839 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 鳥取 </td>
   <td style="text-align:left;"> 境 </td>
   <td style="text-align:right;"> 69006 </td>
   <td style="text-align:left;"> 47742 </td>
   <td style="text-align:right;"> 1.3942317 </td>
   <td style="text-align:right;"> 0.0002963 </td>
   <td style="text-align:right;"> 28.26839 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 徳島 </td>
   <td style="text-align:left;"> 徳島 </td>
   <td style="text-align:right;"> 71106 </td>
   <td style="text-align:left;"> 47895 </td>
   <td style="text-align:right;"> 2.2615596 </td>
   <td style="text-align:right;"> 0.0000000 </td>
   <td style="text-align:right;"> 28.54129 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 香川 </td>
   <td style="text-align:left;"> 多度津 </td>
   <td style="text-align:right;"> 72111 </td>
   <td style="text-align:left;"> 47890 </td>
   <td style="text-align:right;"> 1.7405302 </td>
   <td style="text-align:right;"> 0.0000001 </td>
   <td style="text-align:right;"> 28.88129 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 愛媛 </td>
   <td style="text-align:left;"> 松山 </td>
   <td style="text-align:right;"> 73166 </td>
   <td style="text-align:left;"> 47887 </td>
   <td style="text-align:right;"> 2.1886569 </td>
   <td style="text-align:right;"> 0.0000000 </td>
   <td style="text-align:right;"> 28.63097 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 愛媛 </td>
   <td style="text-align:left;"> 宇和島 </td>
   <td style="text-align:right;"> 73442 </td>
   <td style="text-align:left;"> 47892 </td>
   <td style="text-align:right;"> 1.3867445 </td>
   <td style="text-align:right;"> 0.0000044 </td>
   <td style="text-align:right;"> 28.12065 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 高知 </td>
   <td style="text-align:left;"> 高知 </td>
   <td style="text-align:right;"> 74182 </td>
   <td style="text-align:left;"> 47893 </td>
   <td style="text-align:right;"> 2.1795399 </td>
   <td style="text-align:right;"> 0.0000000 </td>
   <td style="text-align:right;"> 28.26065 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 高知 </td>
   <td style="text-align:left;"> 室戸岬 </td>
   <td style="text-align:right;"> 74372 </td>
   <td style="text-align:left;"> 47899 </td>
   <td style="text-align:right;"> 0.8908955 </td>
   <td style="text-align:right;"> 0.0000623 </td>
   <td style="text-align:right;"> 26.64903 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 山口 </td>
   <td style="text-align:left;"> 下関 </td>
   <td style="text-align:right;"> 81428 </td>
   <td style="text-align:left;"> 47762 </td>
   <td style="text-align:right;"> 2.0352841 </td>
   <td style="text-align:right;"> 0.0000000 </td>
   <td style="text-align:right;"> 28.37419 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 福岡 </td>
   <td style="text-align:left;"> 福岡 </td>
   <td style="text-align:right;"> 82182 </td>
   <td style="text-align:left;"> 47807 </td>
   <td style="text-align:right;"> 2.5130707 </td>
   <td style="text-align:right;"> 0.0000000 </td>
   <td style="text-align:right;"> 29.04516 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 大分 </td>
   <td style="text-align:left;"> 大分 </td>
   <td style="text-align:right;"> 83216 </td>
   <td style="text-align:left;"> 47815 </td>
   <td style="text-align:right;"> 2.4702186 </td>
   <td style="text-align:right;"> 0.0000000 </td>
   <td style="text-align:right;"> 28.21419 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 長崎 </td>
   <td style="text-align:left;"> 厳原 </td>
   <td style="text-align:right;"> 84072 </td>
   <td style="text-align:left;"> 47800 </td>
   <td style="text-align:right;"> 1.0788130 </td>
   <td style="text-align:right;"> 0.0038859 </td>
   <td style="text-align:right;"> 27.49935 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 長崎 </td>
   <td style="text-align:left;"> 長崎 </td>
   <td style="text-align:right;"> 84496 </td>
   <td style="text-align:left;"> 47817 </td>
   <td style="text-align:right;"> 2.1847372 </td>
   <td style="text-align:right;"> 0.0000000 </td>
   <td style="text-align:right;"> 28.30581 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 長崎 </td>
   <td style="text-align:left;"> 雲仙岳 </td>
   <td style="text-align:right;"> 84519 </td>
   <td style="text-align:left;"> 47818 </td>
   <td style="text-align:right;"> 2.2979279 </td>
   <td style="text-align:right;"> 0.0000000 </td>
   <td style="text-align:right;"> 23.61097 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 佐賀 </td>
   <td style="text-align:left;"> 佐賀 </td>
   <td style="text-align:right;"> 85142 </td>
   <td style="text-align:left;"> 47813 </td>
   <td style="text-align:right;"> 1.8387019 </td>
   <td style="text-align:right;"> 0.0000000 </td>
   <td style="text-align:right;"> 28.69226 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 熊本 </td>
   <td style="text-align:left;"> 熊本 </td>
   <td style="text-align:right;"> 86141 </td>
   <td style="text-align:left;"> 47819 </td>
   <td style="text-align:right;"> 1.9892551 </td>
   <td style="text-align:right;"> 0.0000000 </td>
   <td style="text-align:right;"> 28.55290 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 宮崎 </td>
   <td style="text-align:left;"> 宮崎 </td>
   <td style="text-align:right;"> 87376 </td>
   <td style="text-align:left;"> 47830 </td>
   <td style="text-align:right;"> 1.5552936 </td>
   <td style="text-align:right;"> 0.0000000 </td>
   <td style="text-align:right;"> 28.15484 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 鹿児島 </td>
   <td style="text-align:left;"> 鹿児島 </td>
   <td style="text-align:right;"> 88317 </td>
   <td style="text-align:left;"> 47827 </td>
   <td style="text-align:right;"> 2.3438499 </td>
   <td style="text-align:right;"> 0.0000000 </td>
   <td style="text-align:right;"> 29.09548 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 鹿児島 </td>
   <td style="text-align:left;"> 枕崎 </td>
   <td style="text-align:right;"> 88466 </td>
   <td style="text-align:left;"> 47831 </td>
   <td style="text-align:right;"> 1.7005275 </td>
   <td style="text-align:right;"> 0.0000000 </td>
   <td style="text-align:right;"> 28.22452 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 鹿児島 </td>
   <td style="text-align:left;"> 名瀬 </td>
   <td style="text-align:right;"> 88836 </td>
   <td style="text-align:left;"> 47909 </td>
   <td style="text-align:right;"> 1.2296403 </td>
   <td style="text-align:right;"> 0.0000000 </td>
   <td style="text-align:right;"> 28.57484 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 沖縄 </td>
   <td style="text-align:left;"> 那覇 </td>
   <td style="text-align:right;"> 91197 </td>
   <td style="text-align:left;"> 47936 </td>
   <td style="text-align:right;"> 2.0567158 </td>
   <td style="text-align:right;"> 0.0000000 </td>
   <td style="text-align:right;"> 29.14839 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 沖縄 </td>
   <td style="text-align:left;"> 石垣島 </td>
   <td style="text-align:right;"> 94081 </td>
   <td style="text-align:left;"> 47918 </td>
   <td style="text-align:right;"> 1.6548842 </td>
   <td style="text-align:right;"> 0.0000000 </td>
   <td style="text-align:right;"> 29.71032 </td>
  </tr>
</tbody>
</table>
