# [11] Container With Most Water (Medium)

[Container With Most Water - LeetCode](https://leetcode.com/problems/container-with-most-water/)

벽이 될 수 있는 막대 그래프와 같은 모양이 주어질 때, 가장 물을 많이 채울 수 있는 경우를 찾는 문제다.

고려했던 사항은 다음과 같다.

- 벽을 한개 선택하면 중간 벽은 무시된다.
- O(n^2)은 X

풀이 과정은 다음과 같다.

- l, r인덱스를 0, len(height) - 1로 시작한다.
    - 이 문제에서 넓은 빗물을 받으려면 가장 넓고, 가장 높은 벽을 선택해야 한다. 2가지 조건에 따라서 동적으로 물의 양이 정해지기 때문에 한가지 조건(넓게)를 최선의 조건으로 시작했다.
- l, r중에 낮은 벽을 가리키는 인덱스를 안쪽으로 모아준다.
    - 안쪽의 더 큰 벽을 이용해서 많은 물의 양을 받을 가능성이 있기 때문이다.
- 각 인덱스마다 answer의 값을 갱신한다.
- l, r이 만나면 반복을 중지한다.
    - l, r이 만났다면 그 이외의 경우는 처음에 가장 큰 넓이로 잡았고, 더 낮은 벽을 모아주었기 때문에 계산했던 물의 양보다 많을 경우가 없다.

> leetcode를 풀면 느끼는 거지만 Medium이 상당히 어렵게 느껴질 때가 있다. 이 문제도 코드는 간단하게 나왔지만 오랜 시간 고민하여 얻고, 얻고나서도 허탈했다. 다른 답안들을 보니 dp, two pointer이렇게 두가지 경우의 답안이 있는것 같았다. dp의 경우는 너무 어려워보여서 pass하고, two pointer의 경우는 나와 비슷하지만 좀더 최적화되어 있는것 같았다.(무조건 지금보다 높은 벽을 만날 때까지 모은다.) 여기서, two pointer는 정렬된 데이터를 이용할 때 좋다고 공부하였는데 아닌 경우에도 사용될 수 있는걸 깨달았다.
> 

```jsx
class Solution:
    def maxArea(self, height: List[int]) -> int:
        answer = 0
        l, r = 0, len(height) - 1
        while l < r:
            answer = max(answer, min(height[l], height[r]) * abs(l - r))
            if height[l] < height[r]:
                l += 1
            else:
                r -= 1
                
        return answer
```