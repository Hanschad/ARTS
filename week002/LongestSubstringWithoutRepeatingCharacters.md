# Longest Substring Without Repeating Characters

## 题目

Given a string, find the length of the longest substring without repeating characters.

Example 1:

    Input: "abcabcbb"
    Output: 3
    Explanation: The answer is "abc", with the length of 3. 

Example 2:

    Input: "bbbbb"
    Output: 1
    Explanation: The answer is "b", with the length of 1.

Example 3:

    Input: "pwwkew"
    Output: 3
    Explanation: The answer is "wke", with the length of 3. 
                Note that the answer must be a substring, "pwke" is a subsequence and not a substring.

## 解题思路

1. 要记录之前出现过的字符
2. 维护一个滑块类型的结构来计算不重复字符的区间

## 解答

- 方法一：用hashmap记录字符串字符与位置的映射

```java
public int lengthOfLongestSubstring(String s) {
    int res = 0;

    HashMap<Character, Integer> map = new HashMap<>();

    int left = 0;
    for (int i = 0; i < s.length(); i++) {
        if (map.containsKey(s.charAt(i))){
            left = Math.max(left, map.get(s.charAt(i))+1);
        }
        map.put(s.charAt(i), i);
        res = Math.max(res, i - left + 1);
    }

    return res;
}
```

- 方法二：直接用一个256长度的大小的整形数组记录字符的位置，字符串的字符转成ASCII码代表数组的pos

```java
public int lengthOfLongestSubstring(String s) {
    int res = 0;

    int[] map = new int[256];
    Arrays.fill(map, -1);
    int left = -1;

    for (int i = 0; i < s.length(); i++) {
        left = Math.max(left, map[s.charAt(i)]);
        map[s.charAt(i)] = i;
        res = Math.max(res, i-left);
    }

    return res;
}
```