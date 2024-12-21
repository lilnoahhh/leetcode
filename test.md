step1
思考順にコメントを書いていく

headの末尾のnextが存在すればtrue、それ以外はfalseにしよう
Cみたいにアロー演算子使ってよかったっけ
```python
class Solution:
    def hasCycle(self, head: Optional[ListNode]) -> bool:
        fast = head
        slow = head

        while fast and fast.next:
            fast = fast.next.next
            slow = slow.next

            if fast == slow:
                return True
        
        return False
```
C言語と書き方が混ざった、かつ解法が思いつかなかったため答えを見た。

step2
読みやすくする＆他の人の解法を見る

人の話などを引用しているときは「」を使う。

h1rosakaさんのレポジトリを読む
この答えで用いられているアルゴリズムはフロイドの循環検出法
任意の数列に出現する循環を検出するアルゴリズム

今回の問題はこの知識が有無を問う問題？でもodaさんの話ではその場で思いつくことを期待していないものらしいから違うだろう
この問題は何を問いたかったんだろう（後で分かったがsetを扱えるか見る問題）

シングルトンとシングルトンパターンを初めて聞いたので調べる。
https://note.nkmk.me/python-none-usage/
（このサイトを読みながらh1rosakaさんのレポジトリを読みながら勉強を進める）

https://pep8-ja.readthedocs.io/ja/latest/#section-36
「None のようなシングルトンと比較をする場合は、常に is か is not を使うべきです。絶対に等値演算子を使わないでください。」（PEP8より）
「シングルトンは「一つしかないもの」くらいの意味です。シングルトンパターンはそれを作るための書き方です。」（odaさんのレビューより）

オーバーロードとは？
「プログラミングにおいては同じ名前の関数や演算子などを複数定義し、それを利用する際に引数などに応じて使い分けられる仕組みのこと。例えば、＋という演算子が数字同士では加算するのに対して、文字列同士では文字列の結合という結果を出力する。」（https://www.ntt-west.co.jp/business/glossary/words-00735.html）

「==, !=は特殊メソッド__eq__, __ne__でオーバーロード可能であり、自由にカスタマイズできる。」→__eq__,__ne__というもので==,!=どっちも表現できるということ？
ここら辺の論理はよく分からなかったがNoneに対して比較演算子を使うと思っていた挙動と違うふるまいすることあるから、とにかくPythonではNoneはis Noneかis not Noneで書く、と覚えておく。

それなら答えのコードwhile fast and fast.nextはwhile fast is None and fast.next is Noneと書いたほうがよさそう。

マルチスレッドとは、一つのコンピュータープログラムを実行する際に、アプリケーションのプロセス（タスク）を複数のスレッドに分けて並行処理する流れのことです。マルチスレッドの対義語はシングルスレッドで、ソースコードの上から順に一つの処理を行ないます。
スレッドとはCPUから見たプログラムの実行単位であり、プロセスの中に組み込まれているものです。マルチスレッドとは、複数のスレッドが一つのプロセス内で実行されることを表します。
（https://www.ntt-west.co.jp/business/glossary/words-00262.html）

h1rosakaさんのリポジトリに勉強すべき内容がまとまっていたので特にこれ以上はまとめない（めっちゃ勉強になります）

setって何だっけ？
集合を作るためのクラス

型コンストラクタとは、 それ自体が型であるが、別の型をくっつけて新たな型を作るものである。
型 [] は、型一つを包んでリストになる リストの型コンストラクタ であり、型 (,) は型二つを包んでタプルになる タプルの型コンストラクタ である。
同じように、 型 Either は型二つを包んで Either a b を作る Either の型コンストラクタ である。
一方、値としての [] は空リスト、値としての (,) はタプルのコンストラクタであることに注意する。
（https://qiita.com/rooooomania/items/e9d29c27abfe2aa9d8c6）

early returnについて調べたがCで同じことをやっとことがあるので大丈夫そう。

tk-hirom さんのレポジトリを読む（https://github.com/tk-hirom/Arai60/pull/1/commits/967ba6e39e0f6fd44a044778596f7dcd13ad0160）
「上の set を使ったコードが書けた場合、普通はできます。
上の set を使ったコードが書けなかった場合、一緒に働くことが困難です。
というわけで、set を使えるかを判定している出題です。」（odaさんの発言より）
あーsetを扱えることを見るための問題だったのか。今後もsetを使うのは重要っぽい
じゃあsetを使った解法で解き直すか

空間計算量って何だっけ
時間計算量は、アルゴリズムが問題を解決するために必要な計算ステップの数を示します。一方、空間計算量は、アルゴリズムが問題を解決するために必要なメモリの量を示します（https://qiita.com/_shun/items/8be65f63142a875c136d）
じゃあさっきのフロイドの循環検出法は
時間計算量O(n)
空間計算量O(1)？

「List の in の確認は、線形で舐めるので大きくなると遅くなります。」(odaさんより）

ハッシュテーブルの解説（https://qiita.com/tenten1010/items/da4084f937ad07e70164）

setを用いてinで探す処理は平均 O(1) で済む。ハッシュ値を計算し、それに対応するハッシュテーブル内の位置を直接参照すればいいから

以下の説明はh1rosakaのもの。分かりやすかったためここにも載せる。
- Nodeの数をNとする
    - STEP1
        - 時間計算量O(N^2)
            - whileのループ処理がN回で、1回の処理あたり、listのinだから1~N回つまり、N+2N+3N+...+N^2
            - ちなみにsetを使っていれば1回あたりが1に減ったので、O(N)で済んだ。
        - 空間計算量O(N)
            - checked_nodesの長さ分。
    - leetcodeの正解(ウサギとかめ)
        - 時間計算量O(N)
            - 輪っかがない時はN/2でfastがゴールにつく
            - 輪っかがある時で、一番fastが追いつくのが大変なのは全てのNode使って輪っかになっていた時で、その場合はN
        - 空間計算量O(1)
            - ループ処理はあるが、毎回上書きするので、Nに関係ない

```python 
if node is in visited:
```
と書いたらsyntax errorはきだした。whileと違ってifの中にisは使わない。

```python
class Solution:
    def hasCycle(self, head: Optional[ListNode]) -> bool:
        visited = set()
        node = head

        while node is not None:
            if node in visited:
                return True
            
            visited.add(node)
            node = node.next
        return False
```
この解法が良さそうなのでこれでstep3にいく。

step3 10分以内にエラーはかずに3回連続acceptさせる
1回目1分29秒
2回目1分6秒
3回目51秒

``` python
class Solution:
    def hasCycle(self, head: Optional[ListNode]) -> bool:
        visited = set()
        node = head

        while node is not None:
            if node in visited:
                return True
                
            visited.add(node)
            node = node.next

        return False
```
初手の発想として、循環の真偽判定はsetを用いて探索するという考え方で良いのだろうか？

