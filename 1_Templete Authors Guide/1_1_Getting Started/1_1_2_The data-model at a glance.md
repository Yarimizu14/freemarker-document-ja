これまで、`data-model`は基本的に木（ツリー構造）になっている事をみてきました。この木構造は、時として複雑で深いものになることがあります。

````
(root)
  |
  +- animals
  |   |
  |   +- mouse
  |   |   |   
  |   |   +- size = "small"
  |   |   |   
  |   |   +- price = 50
  |   |
  |   +- elephant
  |   |   |   
  |   |   +- size = "large"
  |   |   |   
  |   |   +- price = 5000
  |   |
  |   +- python
  |       |   
  |       +- size = "medium"
  |       |   
  |       +- price = 4999
  |
  +- test = "It is a test"
  |
  +- whatnot
      |
      +- because = "don't know"  

````

変数は、ディレクトリのようになっており、**hases（ハッシュ）**と呼ばれます。（例ではroot,animals,mouse,elephant,python,whatnot）
そして、ハッシュは、名前を参照する事で他の変数（subvariablesと呼びます）を保持することができます。（例では、"animals","mouse", "price"）

もし、ハッシュ内の変数をテンプレートで使いたいときは、rootからのパスをドット区切りで指定します。mouseのpriceにアクセスするためには、rootからanimals、mouse、priceと指定し、`animals.mouse.price`と記述します。この記述を`${...}`で囲むと、この変数をFreeMarkerテンプレートで書き出す事を意味します。

そしてもうヒトッツ、重要な変数の種類があります。**sequence**です。
sequenceはhashと似ていますが、sequenceはsequenceが保持する値に名前を持ちません。代わりに、それらの値に順番を付けて保持し、インデックスでアクセスする事が出来ます。たとえば、この`data-model`では、`animals`と`whatnot.fruits`がsequenceになっています。

````
(root)
  |
  +- animals
  |   |
  |   +- (1st)
  |   |   |
  |   |   +- name = "mouse"
  |   |   |
  |   |   +- size = "small"
  |   |   |
  |   |   +- price = 50
  |   |
  |   +- (2nd)
  |   |   |
  |   |   +- name = "elephant"
  |   |   |
  |   |   +- size = "large"
  |   |   |
  |   |   +- price = 5000
  |   |
  |   +- (3rd)
  |       |
  |       +- name = "python"
  |       |
  |       +- size = "medium"
  |       |
  |       +- price = 4999
  |
  +- whatnot
      |
      +- fruits
          |
          +- (1st) = "orange"
          |
          +- (2nd) = "banana"  
````

sequence内の変数にアクセスするためには、スクエアブランケットでインデックスを指定します。インデックスは、０から始まり、最初の値は０、２番目の値は１という風に続きます。そのため、最初のanimalの値を得たいときには`animals[0].name`、`whatnot.fruits`の２番目の値（文字列"banana"）を得たいときには`whatnot.fruits[1]`と書きます。

スカラ値はさらに以下のカテゴリに分類されます。

* **String**：テキスト、上の例の"m"、"o"、"u"、"s"、“e”のように文字の列と扱われることもある。上の例では、`name`,`size`も文字列である。

* **Number**：これは上の例の`price`のような数値の値です。FreeMarkerでは、文字列の"50"と数値の50は違うものです。前者はただの二つの文字の連続であり（人間が読みやすい形式になったもの（？））、後者は計算が可能な数値の値になっています。

* **Date/Time**：日付・年月日や時です。動物が捕まった日付や、お店が開店する時間などです。

* **Boolean**：trueまたはfalseを持ちます。例えば、`animal`が持つ`protected`という変数では、その動物が保護されているか否かを保持する事が出来ます。

###まとめ

* `data-model`は木構造で表されます。

* スカラ値は単独の値を保持します。その値は、string、number、data/time、booleanのいずれかを取ります。

* Hashesは、一意の名前と関連づけられる他の値を保持するコンテナーです。

* Sequenceは、順序付けられた値を保持するコンテナーです。Sequenceに保持された値は、０から始まるインデクスを通して取り出されます。







