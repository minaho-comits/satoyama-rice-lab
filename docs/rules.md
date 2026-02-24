\#「今回の学び」テンプレ



現象：



期待：



実際：



原因：（要素にクラスが付いてる場所 / セレクタ不一致 など）



検証：（DevToolsで見たルール、取り消し線の有無）



修正：



再発防止ルール（1行）：







20260224

\## 事例：Hero CTAが効かなかった件



\#現象：

.c-btn { display: inline-block; } を書いたが、効いてるか分からなかった。



\#期待：

ボタンの表示形式が変更されるはず。



\#実際：

Dev Toolsでc-btn に取り消し線。

.wp-block-button > .wp-block-button 側のdisplayが適用されていた。



\#原因：

c-btnが.wp-block-button(外箱)についていたが、

CSSは .wp-block-button\_\_link.c-btn(リンク側)前提で書いていた。

→セレクタ不一致。



\#検証：

DevTools→Filterにdisplayと入力。

適用されているCSSと取り消し線を確認。



\#修正：



@media (max-width: 600px) {

  .p-hero #hero-cta .wp-block-button\_\_link {

    display: block;

    width: 100%;

  }

}



再発防止ルール（1行）：

「まずHTML構造を見て、クラスが付いている“正確な要素”を確認する。」



Devツール Filterの「入力ワード」チートシート

Filterは「探したいプロパティ名」か「クラス名」を入れるのが基本。



よく使う入力

\*display

\*width

\*margin

\*padding

\*font-size

\* text-align

\* background

\* border

\* gap

\* flex

\* position

\* overflow



コツ：まず display / width / marginあたりを入れると「当たってる/負けてる」が分かりやすい





\#\*\* 次回以降の迷わない判断ルール\*\*



\*\*c- (部品) \*\*は「箱or本体」に付ける。

\*\*p-(ページ部分) \*\*は"範囲限定(スコープ)"のために使う

・効いてるか分からない時は、見た目で判断しない

→DevToolで「取り消し線」「適用元ファイル」を見る



・変化ゼロの原因はだいたい3つ

 1. セレクタ不一致

 2. 読み込み/キャッシュ

 3. @media条件外



\## CSSが効かない時のデバッグ順



1\. HTMLでクラス付与位置を確認

2\. DevToolsでFilter検索（display / width など）

3\. 取り消し線があるか確認

4\. 強制的に差が出る値（width:100%など）を当てる

5\. @mediaを一旦外して確認

6\. 最後にスコープを限定する

