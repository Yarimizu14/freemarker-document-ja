最も簡潔なテンプレートはHTMLファイルであり（またはテキストファイル、FreeMarkerはHTMLに限られたものではありません）、FreeMarkerはHTMLをそのままクライアントに送信します。

しかし、ページを動的にしたい場合、FreeMarkerの特別なパーツをHTMLに挿入する必要があります。

* **`${…}`**：FreeMarkerが波括弧（curly brancket）内を実際の値に置き換え出力します。

* **FTL tags**（for FreeMarker Template Language Tags）：FTLタグはHTMLタグに似ていますが、FTLタグはFreeMarkerへの指示であり、出力されません。FTLタグは、`#`で始まります（少し進んだ話ですが、ユーザーが定義したFTLタグは`#`の代わりに`@`で始まります）。

* **コメント**：コメントはHTMLと似ていますが、`<#--`と`-->`で区切られます。これらの区切りと区切り内で囲まれた全てのものは、FreeMarkerにより無視され、出力されません。

FTLタグ、インターポレーション、コメント以外のものは全て、静的なテキストとして考えられ、そのまま出力されます。

FTLタグと共に参照されるものは、**directive**と呼ばれます。これは、HTMLタグと（例：<table>と</table>）とHTMLタグと一緒に参照するHTMLエレメント（例：table）の関係と似ています（この違いが分からない場合、"FTLタグ"と“ディレクティブ”は同意語と扱って下さい）。

####ディレクティブの例

FreeMarkerには多くのディレクティブがありますが、ここでは、３つのよく使われるディレクティブを概観します。

#####if文

if文では、条件的にテンプレートの箇所をスキップする事が出来ます。例えば、[始めの例で](http://freemarker.org/docs/dgui_quickstart_basics.html#example.first)、他の人を除き上司であるBig Joeに挨拶をしたい場合、

````
<html>
<head>
  <title>Welcome!</title>
</head>
<body>
  <h1>
    Welcome ${user}<#if user == "Big Joe">, our beloved leader</#if>!
  </h1>
  <p>Our latest product:
  <a href="${latestProduct.url}">${latestProduct.name}</a>!
</body>
</html>
````
ここでは、変数`user`が"Big Joe"と等しい場合のみ'', our beloved leader''が表示されるようにしています。一般的に、条件*condition*がfalseの場合、`<#if condition>`と`</#if>`の間で囲まれたものはスキップされます。