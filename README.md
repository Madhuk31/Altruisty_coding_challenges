# Altruisty_coding_challenges**

#**CODE_answer 1**
def find_single_numbers(arr):
    xor_result = 0
    for num in arr:
        xor_result ^= num
    rightmost_set_bit = xor_result & -xor_result

    num1, num2 = 0, 0
    for num in arr:
        if num & rightmost_set_bit:
            num1 ^= num
        else:
            num2 ^= num
    return sorted([num1, num2])
print(find_single_numbers([1, 2, 3, 2, 1, 4])) 
print(find_single_numbers([2, 1, 3, 2]))        

#**CODE_answer 2**
def word_break(n, s, dictionary):
    word_set = set(dictionary)
    dp = [False] * (len(s) + 1)
    dp[0] = True

    for i in range(1, len(s) + 1):
        for j in range(i):
            if dp[j] and s[j:i] in word_set:
                dp[i] = True
                break
    return 1 if dp[len(s)] else 0
n1 = 6
s1 = "ilike"
dictionary1 = ["i", "like", "sam", "sung", "samsung", "mobile"]
print(word_break(n1, s1, dictionary1))

n2 = 6
s2 = "ilikesamsung"
dictionary2 = ["i", "like", "sam", "sung", "samsung", "mobile"]
print(word_break(n2, s2, dictionary2)) 


#**CODE_answer 3**
from collections import deque

def find_stepping_numbers(N, M):
    result = []
    queue = deque()
    for i in range(10):
        queue.append(i)
    while queue:
        step_num = queue.popleft()
        if N <= step_num <= M:
            result.append(step_num)
        if step_num == 0 or step_num > M:
            continue
        last_digit = step_num % 10
        if last_digit > 0:
            next_step_num = step_num * 10 + (last_digit - 1)
            if next_step_num <= M:
                queue.append(next_step_num)
        if last_digit < 9:
            next_step_num = step_num * 10 + (last_digit + 1)
            if next_step_num <= M:
                queue.append(next_step_num)
    result.sort()
    
    return result
N, M = map(int, input().split())
stepping_numbers = find_stepping_numbers(N, M)
print(' '.join(map(str, stepping_numbers)))

#**CODE_answer 4**
def minimize_ticket_price(ticket_price, k):
    stack = []
    length = len(ticket_price)
    
    for digit in ticket_price:
        while k > 0 and stack and stack[-1] > digit:
            stack.pop()
            k -= 1
        stack.append(digit)
        stack.pop()
        k -= 1
    result = ''.join(stack)
    result = result.lstrip('0')    
    if not result:
        result = '0'
    
    return result
ticket_price = input().strip()
k = int(input().strip())

print(minimize_ticket_price(ticket_price, k))

#**CODE_answer 5**
def getMaxToys(prices, money):
    start = 0
    current_sum = 0
    max_length = 0

    for end in range(len(prices)):
        current_sum += prices[end]
        while current_sum > money:
            current_sum -= prices[start]
            start += 1
        max_length = max(max_length, end - start + 1)

    return max_length

prices = [1, 4, 5, 3, 2, 1, 6]
money = 6
print(getMaxToys(prices, money))  
