# Character with longest consecutive repetition

Copy from CodeWars.com

For a given string s find the character c (or C) with longest consecutive repetition and return:

Object[]{c, l};
where l (or L) is the length of the repetition. If there are two or more characters with the same l return the first in order of appearance.

For empty string return:

Object[]{"", 0}


# My Solution:

```java
import java.util.*;
import java.util.LinkedList;

public class Solution {
    public static Object[] longestRepetition(String s) {
      if (s.equals("")) return new Object[]{"", 0};
      
      LinkedList<String> list = new LinkedList<String>();
        char[] chars = s.toCharArray();
        StringBuilder currentString = new StringBuilder();
        char lastChar = chars[0];
        char currentChar = ' ';
        int currentSize = 0;
        int biggestSize = 0;
      
        // currentString is equal to the first char in string
        for (int i = 0; i < chars.length; i++) {
            currentChar = chars[i];
            // if current char is equal to last char
            if (currentChar == lastChar) {
                // add char to currentString
                currentString.append(currentChar);
                // increment currentSize  +1
                lastChar = currentChar;
                currentSize++;
            } else {
                lastChar = currentChar;
                // ELSE if current char is different from last string
                // if currentSize > biggestSize
                if (currentSize > biggestSize){
                    list.addFirst(currentString.toString());
                    biggestSize = currentSize;
                }
                // add string on front list
                // else add to the last
                else {
                    list.addLast(currentString.toString());
                }
                currentString = new StringBuilder();
                // set biggestSize to currentSize
                // set currentSize to 0
                currentSize = 0;
                // add current char to currentString, and increment currentSize +1
                currentString.append(currentChar);
                currentSize++;
            }
            if (i == chars.length -1 & currentSize > biggestSize) list.addFirst(currentString.toString());
        }
      return new Object[]{""+list.get(0).charAt(0), list.get(0).length()};
     }
}
```
