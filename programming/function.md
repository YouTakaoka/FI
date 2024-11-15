このページでは，関数の概念についてまとめる。

# 関数とは
**関数**とは，「一連の処理のまとまりに名前を付けたもの」と理解すればよい。

たとえば，「オムレツを作る」という一つのタスクを考えよう。
このタスクは，「卵を割る」とか「砂糖を入れて混ぜる」，「焼く」などのいくつかの工程に分解できるはずである。
これを，次のように書いてみよう:

```php
○オムレツを作る
    卵を割る
    砂糖を入れて混ぜる
    焼く
    盛り付ける
```

これで，一連の工程に「オムレツを作る」という名前がついた。
我々は，意識せずとも日常的にこのようなことをやっているはずである。
例えば，誰かにオムレツを焼いてくれるよう頼むとき，一々「卵を割って，砂糖を入れて，…」などと指示するだろうか？
単に「オムレツを作って」と頼めば，オムレツの作り方を知っている相手ならそのような工程を勝手にやってくれるはずである。

プログラミングにおいて，この「オムレツを作る」といったタスクが「関数」に相当する。

# 関数定義
とは言っても，相手がオムレツの作り方を知らないこともあるだろう。
その場合には，上のようにして「オムレツを作る」工程の「手順書」を作成して相手に渡す必要がある。
然らば，上のような「手順書」のことをプログラミングでは**関数定義**という。

## 書式（擬似言語）
擬似言語における，関数定義の書式を見てみよう:

```php
○関数名()
    // 処理
```

先程のオムレツの例では簡単のために省略したが，関数名の後ろに`()`が来ることに注意しよう。
この括弧は後ほど重要な意味を持つが，今はとりあえず「関数であることを明示するための記号」ぐらいに思ってよい。

簡単な例を示そう。
次の関数`judge_3_is_even_or_odd`は，「3が偶数かどうか」を判定するものである（"even"/"odd"はそれぞれ「偶数の」/「奇数の」という意味の形容詞）。無論，そんなことを判定するのにプログラムの力を借りる必要は無いが，最初の例はなるべく簡単な方がいいであろうし，後ほどこれを発展させてより複雑な関数を作っていくための基礎でもある。

```php
○judge_3_is_even_or_odd()
    // 3 が偶数かどうかを判定する。
    // 偶数なら"偶数"，奇数なら"奇数"と出力する。
    if (3 を 2 で割った余りが 0 に等しい)
        "偶数"を出力
    else
        "奇数"を出力
```

これで，仮にプログラマが「3が偶数かどうか」をすぐに思い出せなくても，そのことを一々考える必要が無くなったわけだ。
勿論これだけでは大したことに思えないであろうが，後に引数や戻り値の概念と組み合わさったとき，関数概念の真の威力が実感できるだろう。

## 書式（Python）
同じことを，Pythonでやるとどうなるか見てみよう。
まず，書式は次のようになる:

```python
def 関数名():
    # 処理
```

今度は`()`の後ろに`:`が必要なのに注意しよう。
キーワード`def`は，「定義(definition)」の頭から取ったものである。

先程，擬似言語の例で出てきた関数`judge_3_is_even_or_odd`を，Pythonで書き直してみよう:

```python
def judge_3_is_even_or_odd():
    # 3 が偶数かどうかを判定する。
    # 偶数なら"偶数"，奇数なら"奇数"と出力する。
    if 3 % 2 == 0:
        print("偶数")
    else:
        print("奇数")
```

# 関数呼び出し
一度オムレツの作り方を教えたなら，その相手に「オムレツを作って」と命令できるようになる。
そのように「命令」することを，プログラムの言葉では「関数を呼び出す」と表現する。

## 書式
関数呼び出しの書式は，擬似言語でもPythonでも共通で，次のようにする:

```php
関数名()
```

例えば，先程の例で定義した関数`judge_3_is_even_or_odd`を呼び出したければ，呼び出したい箇所で

```php
judge_3_is_even_or_odd()
```

と書けばよい。

## 例(Python)
Pythonが擬似言語と違うのは，Pythonのプログラムは実際に動かして確かめることができる点だ。
試しに，先程の関数`judge_3_is_even_or_odd`を呼び出してみよう。
上のPythonコードに，少し行を書き足し次のようにする:

```python
# 関数定義
def judge_3_is_even_or_odd():
    # 3 が偶数かどうかを判定する。
    # 偶数なら"偶数"，奇数なら"奇数"と出力する。
    if 3 % 2 == 0:
        print("偶数")
    else:
        print("奇数")

judge_3_is_even_or_odd() # 関数呼び出し
```

プログラムが正しく動いたなら，コンソールに`奇数`と表示されるはずである。

動かしてみれば分かるが，**関数定義だけだとPythonは何もしてくれない**（試しに，関数呼び出しの行の頭に`#`を付けてコメントアウトしてみて欲しい）。
これは考えてみれば当たり前のことで，**オムレツの作り方を教えただけで，実際に「オムレツを作って」と言わなければ相手が何もしてくれないのと同じ**である。

## 関数を呼び出した際の処理の流れ
プログラム内で関数を呼び出したとき，処理がどのように流れていくのか，初学者にはわかりづらいところがある。
ここでは，2つの理解の仕方を紹介しよう:

1. プログラムの「置き換え」と考える（少し不正確）
2. 処理が関数の中に「入る」と考える（正確）

再び，先程のオムレツの例で考えよう。
上で書いた「手順書」を，擬似言語の関数っぽい書き方で書き直すと次のようになる:

```php
○オムレツを作る()
    卵を割る()
    砂糖を入れて混ぜる()
    焼く()
    盛り付ける()
```

ここで，上の`焼く()`という工程自体も実はそれなりに複雑かもしれない。
例えば，

```php
○焼く()
    フライパンに油をひく()
    弱火で温める()
    溶いた卵を流し込む()
    箸で30秒間かき回す()
    巻く()
```

みたいなこともあり得る。
これはつまり，上記の「オムレツを作る」手順書が，次の「省略版」であることを意味する:

```php
○オムレツを作る()
    卵を割る()
    砂糖を入れて混ぜる()

    // ここから「焼く」工程
    フライパンに油をひく()
    弱火で温める()
    溶いた卵を流し込む()
    箸で30秒間かき回す()
    巻く()
    // 「焼く」の終わり

    盛り付ける()
```

この例を見れば，上の1番目，つまり"プログラムの「置き換え」と考える"が理解できるのではないだろうか。
つまり，関数呼び出しがあるプログラムの流れは，関数呼び出しの部分をそっくりそのまま，関数定義の中身で置き換えてしまったものと同じである，という考え方である。
これは上でも書いた通り少し不正確な理解の仕方ではあるが，最初のイメージを掴むのには便利であろう。

例えば，次のようなPythonコードを理解するのに有用である:

```python
judge_3_is_even_or_odd()
print("こんにちは！")
judge_3_is_even_or_odd()
```

なお，関数`judge_3_is_even_or_odd`の定義は上で書いた通りなので省略した。
このPythonコードを実行すると，次のような出力が得られるはずだ:

```
奇数
こんにちは！
奇数
```

何故このような順番で出力されるかは，上でやったように，コード中の関数呼び出し部分をそのまま定義で「置き換えて」みれば分かる。
つまり，上のコードは次と等価だ:

```python
# 関数`judge_3_is_even_or_odd`の定義の中身
# --- ここから ---
if 3 % 2 == 0:
    print("偶数")
else:
    print("奇数")
# --- ここまで ---

print("こんにちは！")

# 関数`judge_3_is_even_or_odd`の定義の中身
# --- ここから ---
if 3 % 2 == 0:
    print("偶数")
else:
    print("奇数")
# --- ここまで ---
```

読みやすいように，コメントは適宜補った。

もう一つの考え方，"処理が関数の中に「入る」と考える"はより正確だが，少し難解である。
再びオムレツの例を用いるならば，上の`焼く`という工程はすべて，フライパンの上で行われる作業である。
`焼く`工程が始まった途端，作業場所がフライパンに移る。
ただし，それも最終的には元の調理場に戻ってくる前提でのことだ。
処理が関数の中に「入る」とは，このように「作業場所が一旦移る」（ただし，終わったら元の場所に戻ってくる）イメージである。

より明示的に書くなら，次のような流れになる:

1. 関数が呼び出される
2. 処理の流れが関数定義の内部に移る
3. 関数定義内部の処理が一通り実行される
4. 終わったら，関数の「呼び出し元」に処理が戻る
5. そこから再び処理が流れ始める

再び，先程のPythonコードで考えてみよう:

```python
judge_3_is_even_or_odd() # 関数呼び出し(1)
print("こんにちは！")
judge_3_is_even_or_odd() # 関数呼び出し(2)
```

ただし今度は区別しやすいように，関数呼び出しにコメントで番号を振った。
これを実行したときの流れは，次のようになる:

1. 「関数呼び出し(1)」で，`judge_3_is_even_or_odd`が呼び出される
1. 処理が，関数`judge_3_is_even_or_odd`の定義の内部に移る
1. `judge_3_is_even_or_odd`の定義内部の処理が一通り実行される（その結果，「奇数」が出力される）
1. 関数の呼び出し元，すなわち「関数呼び出し(1)」のところに処理が戻る
1. そこから処理が再開する
1. `print`関数により"こんにちは！"が出力される
1. 「関数呼び出し(2)」で，再び`judge_3_is_even_or_odd`が呼び出される
1. 処理が，関数`judge_3_is_even_or_odd`の定義の内部に移り，再度「奇数」が出力される
1. 関数の呼び出し元，すなわち「関数呼び出し(2)」のところに処理が戻る
1. プログラム終了

関数内部の処理を実行するとき，定義の最後まで進んだら自動的に関数を抜けて呼び出し元に戻るという認識は見落としがちである。
今回のように簡単な関数であれば上記のようなトレースは容易いが，引数や戻り値を持つ関数になってくると難しくなってくるので，今回のような「準備運動」は大切である。

# 引数
先程は「オムレツを作る」というタスクを考えたが，今度は「たい焼きを焼く」というタスクについて考えてみよう。
ただし，たい焼きの中身は「あんこ」，「カスタードクリーム」，「モッツァレラチーズ」の3種があるとする。
この場合，工程は「中身」という1つの「変数」を持つことになる:

```php
○たい焼きを焼く(「中身」)
    生地を作る
    生地を鉄板に流し込む
    「中身」を入れる
    さらに生地を流し込む
    焼く
```

こんな具合だろうか。
「中身」が何かは事前に決まっていない（＝変数である）以上，それに何かしら「名前」を持たせておかねば工程を記述できない。

このように，「事前に値が決まっておらず，関数が呼び出されたときに値が決まる」変数を**引数**という。
関数は，先程の例のように引数を取らないこともできるし，また複数個の引数を取ることもできる。

## 書式（擬似言語）
擬似言語において，1つ以上の引数を取る関数の定義は次のように書かれる:

```php
○関数名(型1: 引数名1, 型2: 引数名2, …)
    // 処理
```

また，呼び出しは:

```php
関数名(引数1, 引数2, …)
```

例として，先程の`judge_3_is_even_or_odd`を，一つの引数を取る形に書き換えてみよう:

```php
○judge_even_or_odd(整数型: n)
    // n が偶数かどうかを判定する。
    // 偶数なら"偶数"，奇数なら"奇数"と出力する。
    if (n を 2 で割った余りが 0 に等しい)
        "偶数"を出力
    else
        "奇数"を出力
```

今度は，判定される整数が`3`のように固定した数でなくなったことに注目したい。
これが何を意味するだろうか？
「呼び出し側」が，そこに好きな数を「代入」できるということだ！

```php
judge_even_or_odd(3) // "奇数"と出力
judge_even_or_odd(4) // "偶数"と出力
```

これで以前よりは大分，実生活の役に立ちそうな気がしてきただろう。

なお，上記の関数定義において`n`という文字を使ったことには何の意味もない。
これは定義内で「偶数か奇数かを判定すべき対象」に付けられた名前でしかないから，別に他の文字でも良かったし，関数定義の「外側」の住人にとっては意味のない名前だ。

## 書式(Python)
引数がある場合の関数定義の書式は，Pythonだと次のようになる:

```python
def 関数名(引数名1: 型1, 引数名2: 型2, …):
    # 処理
```

擬似言語とは，引数名と型の順番が逆であることに注意しよう。

呼び出しの書式は擬似言語と同じである:

```python
関数名(引数1, 引数2, …)
```

再び例として，上で擬似言語で書いた関数`judge_even_or_odd`を，Pythonで定義してみよう:

```python
def judge_even_or_odd(n: int)
    # n が偶数かどうかを判定する。
    # 偶数なら"偶数"，奇数なら"奇数"と出力する。
    if n % 2 == 0:
        print("偶数")
    else:
        print("奇数")
```

これを呼び出した結果も勿論同じである:

```python
judge_even_or_odd(3) # "奇数"と出力
judge_even_or_odd(4) # "偶数"と出力
```

## 組み込み関数
なお，上のコードにも出てきたPythonの`print()`も一種の関数である。
関数`print()`は一つの文字列を引数として取り，その受け取った文字列をコンソールに出力する（厳密に言うと複数の引数を取ることもできる（オーバーロード））。

このように，プログラマが定義しなくても使える関数というのがある。
これらは，Pythonに予め用意されているものだから**組み込み関数**と呼ばれる。

# 戻り値

戻り値のない関数のことを，**手続き**とも言う。

# まとめ

# 再帰関数
