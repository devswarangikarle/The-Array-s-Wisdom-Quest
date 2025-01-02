# The-Array-s-Wisdom-Quest

In the ancient realm of Numeria, the High Council of Elders has presented you with a unique challenge. You are given a magical array of N distinct numbers, each holding a secret power. To unlock the ultimate knowledge of Numeria, you must decipher the array’s wisdom by finding the sum of the smallest element in every possible subarray (a continuous sequence) within the array. Each subarray reveals a hidden truth, and only by calculating the sum of these smallest elements will you unveil the full power of the array.
Your quest is to compute this mystical sum and prove your worth to the Council.

def sum_of_minimums(n, arr):
    # Arrays to store indices of the Previous and Next Smaller Elements
    prev_smaller = [-1] * n
    next_smaller = [n] * n

    # Monotonic stack to compute PSE
    stack = []
    for i in range(n):
        while stack and arr[stack[-1]] > arr[i]:
            stack.pop()
        prev_smaller[i] = stack[-1] if stack else -1
        stack.append(i)

    # Monotonic stack to compute NSE
    stack = []
    for i in range(n - 1, -1, -1):
        while stack and arr[stack[-1]] >= arr[i]:
            stack.pop()
        next_smaller[i] = stack[-1] if stack else n
        stack.append(i)

    # Compute the sum of minimums
    result = 0
    for i in range(n):
        left_count = i - prev_smaller[i]
        right_count = next_smaller[i] - i
        result += arr[i] * left_count * right_count

    return result

# Input Handling
n = int(input())
arr = list(map(int, input().split()))
print(sum_of_minimums(n, arr))
