python'''
#step1、思考順にコメントを書いていく
#headの末尾のnextが存在すればtrue、それ以外はfalseにしよう
#Cみたいにアロー演算子使ってよかったけ

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
#C言語と書き方が混ざった、かつ解法が思いつかなかったため答えを見た。

'''
