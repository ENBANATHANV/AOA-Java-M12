
# EX 2E Pattern Matching using KMP Algorithm.
## DATE: 15/02/2026
## AIM:
To write a Java program for the following constraints.
Longest Palindromic Substring
Given a string s, return the longest palindromic substring in s.
using Manacher's Algorithm

## Algorithm
1. Transform the string by inserting # between characters (e.g., "babad" → #b#a#b#a#d#) to handle odd/even palindromes uniformly.
2. Create an array palindromeRadii[] to store the palindrome radius at each index and initialize center = 0, radius = 0.
3. Scan each position i in the transformed string and compute its mirror index using mirror = 2 * center - i.
4. If i is within the current right boundary radius, initialize palindromeRadii[i] = min(radius - i, palindromeRadii[mirror]).
5. Expand around index i while characters match on both sides and update the radius length for that center. If the palindrome expands beyond the current boundary,
   update center and radius.
6. After scanning all positions, find the index with the maximum radius, convert it back to the corresponding start index in the original string, and return the
   substring. 

## Program:
```
/*
Program to implement Reverse a String
Developed by: ENBANATHAN V
Register Number: 212224220027 
*/
import java.util.Scanner;

public class Solution {
    public String longestPalindrome(String s) {
        //Type code here...
        if(s==null||s.length()==0)
        {
            return "";
        }
        String changed = process(s);
        int n =changed.length();
        int[] arr = new int[n];
        int cen =0,rig=0;
        for(int i=1;i<n-1;i++){
            int mir = 2*cen-i;
            if(i<rig){
                arr[i]=Math.min(rig-i,arr[mir]);
            }
            while(changed.charAt(i-arr[i]-1)==changed.charAt(i+arr[i]+1))
            {
                arr[i]++;
            }
            if(i+arr[i]>rig)
            {
                cen=i;
                rig = i+arr[i];
            }
        }
        int max=0;
        int check =0;
        for(int i=1;i<n-1;i++)
        {
            if(arr[i]>max){
                max=arr[i];
                check=i;
            }
        }
        int start = (check- max)/2;
        return s.substring(start,start+max);
    }
    private static String process(String a){
        StringBuilder val = new StringBuilder("^");
        for(char c: a.toCharArray()){
            val.append("#").append(c);
        }
        val.append("#$");
        return val.toString();
    }
    // Main method for user input
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
   
        String input = scanner.nextLine();

        Solution sol = new Solution();
        String result = sol.longestPalindrome(input);

        System.out.println("Longest Palindromic Substring: " + result);
        scanner.close();
    }
}

```

## Output:
<img width="830" height="200" alt="image" src="https://github.com/user-attachments/assets/f099eb85-cc22-4466-ae9a-44833bd58539" />



## Result:
The program successfully implemented and the expected output is verified.
