思考順に書いていく
誰かの発言の引用は「」でおこなう

step1
```python
class Solution:
    def detectCycle(self, head: Optional[ListNode]) -> Optional[ListNode]:
        visited = set()
        node = head

        while node is not None and node.next is not None:
            if node in visited:
                return node
            
            visited.add(node)
            node = node.next
        
        return -1

```
141. Linked List Cycleとの違いは循環を検出したら循環の開始位置を出力するところだけ？

step1のコードを走らせると以下のエラー文が出た。
Your returned value is not a ListNode type.


2 / 18 testcases passedなので全て間違っているわけではない。何か考えられていない条件がある？

https://www.youtube.com/watch?v=wzoNwa0eOm0
上の動画を見た。
解法2は私のとそこまで変わらないはず。。。と思っていたらreturnがNoneにしていた。
ためしに以下のコードを走らせるとaccept
```python
class Solution:
    def detectCycle(self, head: Optional[ListNode]) -> Optional[ListNode]:
        visited = set()
        node = head

        while node is not None and node.next is not None:
            if node in visited:
                return node
            
            visited.add(node)
            node = node.next
        
        return None
        
```
型アノテーションについて勉強すべきだな

間数アノテーションと型アノテーションは違う？→多分同じ

https://docs.python.org/ja/3.13/library/typing.html#module-typing（pythonのドキュメント）を読んだ
「Optional[X] は X | None (や Union[X, None]) と同等
これがデフォルト値を持つオプション引数とは同じ概念ではないということに注意してください。 デフォルト値を持つオプション引数はオプション引数であるために、型アノテーションに Optional 修飾子は必要ありません。 例えば次のようになります:
```python
def foo(arg: int = 0) -> None:
    ...
```
それとは逆に、 None という値が許されていることが明示されている場合は、引数がオプションであろうとなかろうと、 Optional を使うのが好ましいです。 例えば次のようになります:
```python
def foo(arg: Optional[int] = None) -> None:
    ...
```
バージョン 3.10 で変更: Optionalは X | None のように書けるようになった」

「オプション引数（省略可能な引数）とは、メソッドを呼び出すときにその引数の一部を省略できる機能である。」 
    (https://atmarkit.itmedia.co.jp/ait/articles/1706/07/news021.html)
    
「*argとは関数定義時に、引数を指定（まさにアスタリスクみたいなもの）しないことで、関数呼び出し時に後付けで設定したものを引数として使える。尚、必ずしもargである必要はなく、argument=引数のため、*argとなっているだけであり、*がその役割を果たす。」
    (https://tiero.jp/magazine/python-arg-kwarg/)

今までの話をまとめると、以下のコードの意味は引数headはListNodeの属性だがNoneも含む、返り値も同様という意味
def detectCycle(self, head: Optional[ListNode]) -> Optional[ListNode]:

そのため循環がない場合の返り値は-1ではなくNoneで返すべきだった

他の方たちのgitも見てみたが解法に大きな違いはないのでこの解法のままstep3に行く。
フロイドの循環検出法は前の問題で写経したのと、setを使うことをメインにすえてる問題なので今回はsetだけ書く

step3
1回目 1分5秒
2回目 42秒
3回目 36秒

```python
class Solution:
    def detectCycle(self, head: Optional[ListNode]) -> Optional[ListNode]:
        visited = set()
        node = head

        while node is not None and node.next is not None:
            if node in visited:
                return node
            
            visited.add(node)
            node = node.next
        
        return None
```

振り返ってみると前回の141. Linked List Cycleとあまり変わらない
おそらく型アノテーションの知識もプラスで問われているのでmediumになったのかな（141. Linked List Cycleはeasy)


