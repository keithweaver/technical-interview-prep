# This problem is to rotate a given array to the right by n steps.

This problem is to rotate a given array to the right by n steps.

For example:

Given [1, 2, 3] and n = 1, you should return [3, 1, 2]

Each step, the last element in the array is moved to the front of the array, and the rest are shifted right.

Another example:

Given [1, 2, 3, 4, 5] and n = 3, you should return [3, 4, 5, 1, 2]

# Potential further questions

What is the time complexity of your solution?

How about space?

Can you do this in-place?

# Answer

With this the first solution is probably just create a new array. Start at i = 0 + n then when at end of array do i - n or whatever. This would be O(n) b/c all values are evaluated but uses more memory b/c new array.

The better solution would be swapping the values. So if it's `n = 3`, you being at `i = 0` and you need to move that to `pos = i + n`. This would work for the second example. Given:

```
[1, 2, 3, 4, 5]

i = 0
n = 3
newPos = 3

[3, 2, 3, 1, 5]

i = 1
n = 3
[1, 2, 3, 4, 5]
```

But this work because that's not right.

Easier just follow the instructions:
Each step, the last element in the array is moved to the front of the array, and the rest are shifted right.

Make this a recursive function.

```
class Solution {
  public int[] arrayRotateHelper(int[] arr, int n) {
    // If n = 0, return arr
    // else, recursive call that returns array then
    //       rotate the last value to front.
    if (n < 1) {
      return arr;
    }
    return moveLastToFront(arrayRotateHelper(arr, n - 1));
  }

  public int[] moveLastToFront(int[] arr) {
    // Dont want to move the last value to the next pos
    // handle the move to front on second last.

    if (arr.length < 1) {
      return arr;
    }

    int nextValue = arr[0];

    for(int i = 0;i < arr.length - 1;i += 1) {
      if (i + 1 == arr.length - 1) {
        // meaning next value is last
        // move last value to front
        arr[0] = arr[arr.length - 1];
      }

      int temp = arr[i];
      arr[i] = nextValue;
      nextValue = temp;
    }
    return arr;
  }

  public String arrayRotate(int[] arr, int n) {
    return String.value(arrayHelper(arr, n));
  }
  public void testOne() {
    System.out.println(arrayRotate([1, 2, 3], 1));
  }
  public void testTwo() {
    System.out.println(arrayRotate([1, 2, 3, 4, 5], 3));
  }
}
```

This would be O(n^2) b/c it goes through each N and goes through every value on each n. Therefore n^2.

This is the bruteforce solution. Extra array is a better one and O(n). The replacement cycle is another solution. Using reverse is another solution.



Source:
- https://github.com/codingforinterviews/practice-problems/tree/master/array_rotate
- https://leetcode.com/problems/rotate-array/solution/
