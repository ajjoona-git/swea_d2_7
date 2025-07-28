# 4834. [파이썬 S/W 문제해결 기본] 1일차 - 숫자 카드 D2

## 문제

```
0에서 9까지 숫자가 적힌 N장의 카드가 주어진다.

가장 많은 카드에 적힌 숫자와 카드가 몇 장인지 출력하는 프로그램을 만드시오. 
카드 장수가 같을 때는 적힌 숫자가 큰 쪽을 출력한다.

 

[입력]
 

첫 줄에 테스트 케이스 개수 T가 주어진다.  ( 1 ≤ T ≤ 50 )

다음 줄부터 테스트케이스의 첫 줄에 카드 장수 N이 주어진다. ( 5 ≤ N ≤ 100 )

다음 줄에 N개의 숫자 ai가 여백없이 주어진다. (0으로 시작할 수도 있다.)  ( 0 ≤ ai ≤ 9 ) 

 

[출력]
 

각 줄마다 "#T" (T는 테스트 케이스 번호)를 출력한 뒤, 
가장 많은 카드의 숫자와 장 수를 차례로 출력한다.
```

## 전략

```python
T = int(input())  # 테스트 케이스 개수

for test_case in range(1, T+1):
    N = int(input())  # 카드 장수
    cards = input()  # 카드 숫자가 여백없이 주어진다.(str)
    
    # cards 에서 숫자 하나씩 순회하면서
    # card_list 에 카운트를 저장한다.
    # 이때 card_list의 인덱스가 카드의 숫자를, 값이 카운트를 의미한다.
    card_list = [0] * 10
    for card in cards:
        card_number = int(card)
        card_list[card_number] += 1
    
    # card_list에서 값이 가장 큰 인덱스(=가장 많은 카드의 숫자)
    max_count_number = -1
    max_count = 0
    for i in range(9, -1, -1):
        if card_list[i] > max_count:
            max_count_number = i
            max_count = card_list[i]
    
    print(f'#{test_case} {max_count_number} {max_count}')
```

### 수정한 거

```python
    # card_list에서 값이 가장 큰 인덱스(=가장 많은 카드의 숫자)
    max_count_number = 10
    for i in range(9, -1, -1):
        if card_list[i] > card_list[max_count_number]:
            max_count_number = i
```

리스트 범위 밖의 숫자로 초기화하고 max값을 갱신하려고 했으나,

맨 처음 순회할 때 card_list[max_count_number]가 지정되지 않는 문제가 발생함.

⇒ max_count 변수를 추가해서 숫자와 카운트를 각각 저장함.