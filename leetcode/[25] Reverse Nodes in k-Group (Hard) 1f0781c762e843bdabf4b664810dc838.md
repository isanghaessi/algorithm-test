# [25] Reverse Nodes in k-Group (Hard)

[Reverse Nodes in k-Group - LeetCode](https://leetcode.com/problems/reverse-nodes-in-k-group/)

SLL에서 k개씩 노드를 뒤집은 SLL을 반환하는 문제이다.

고려한 사항들은 다음과 같다.

- 노드의 value만 바꾸지 말고 노드 자체를 이동시킬 것

풀이 과정은 다음과 같다.

- left, right 2개의 포인터를 사용한다.
- left는 k개를 묶은 그룹의 앞, right는 k개를 묶은 그룹 뒤 노드를 가리킨다.
    - left는 head앞에 빈 노드를 만들어서 head를 가리키게 한다.
    - right는 left.next부터 시작해서 k번째 다음 노드로 이동한다.
- stack을 이용해서 right가 다녀간 노드를 담는다.
- k개가 다 담긴 상황이면,
    - stack에서 꺼내면서 left.next를 업데이트 해준다.
- k개가 다 담기지 않았다면(k개의 그룹이 형성되지 않는 마지막 반복문),
    - 그대로 내비둬야하므로 break

> SLL을 3개의 포인터로 뒤집는 문제와 유사했다. 2개의 런너를 사용해서 풀이할 수 있었으며, stack을 이용해서 거꾸로 데이터들을 담을 수 있었다.
> 

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def reverseKGroup(self, head: Optional[ListNode], k: int) -> Optional[ListNode]:
        answer = left = ListNode(0, head)
        while left:
            right = left.next
            stack = []
            isK = True
            for _ in range(k):
                if not right:
                    isK = False
                    
                    break
                stack.append(right)
                right = right.next
            if not isK:
                
                break
            else:
                while len(stack) > 0:
                    left.next = stack.pop()
                    left = left.next
                left.next = right
                
        return answer.next
```