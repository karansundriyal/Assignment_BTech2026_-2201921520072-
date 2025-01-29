Problem: Given a valid parentheses string s, return the nesting depth of s. The nesting depth is the maximum number of nested parentheses.

 Platform: Leetcode

 ```
#include <iostream>
#include <string>
#include <algorithm>
using namespace std;

class Solution {
public:
    
    int maxDepth(string s) {
        int currentDepth = 0;  
        int maxDepth = 0;      

        
        for (char ch : s) {
            if (ch == '(') {
                currentDepth++;  
                maxDepth = max(maxDepth, currentDepth);  
            }
            else if (ch == ')') {
                currentDepth--;  
            }
        }

        return maxDepth;  
    }
};

int main() {
    
    Solution solution;

    string s1 = "(1+(2*3)+((8)/4))+1";
    string s2 = "(1)+((2))+(((3)))";
    string s3 = "()";
    
    
    cout << "Max depth of s1: " << solution.maxDepth(s1) << endl;
    cout << "Max depth of s2: " << solution.maxDepth(s2) << endl;
    cout << "Max depth of s3: " << solution.maxDepth(s3) << endl;

    return 0;
}

```
Explanation:
1. Class Solution:
The class Solution has a public method maxDepth that calculates the maximum nesting depth of a valid parentheses string.
The method maxDepth takes the string s as an argument and iterates over each character of the string.

2. Nesting Depth Calculation:
We use two variables: currentDepth (to track the current depth) and maxDepth (to store the maximum depth encountered).
For every '(' character, we increment the currentDepth and also update maxDepth to ensure we are keeping track of the maximum depth.
For every ')' character, we simply decrement currentDepth.

3. Main Function:
We create an object solution of the Solution class.
Then we test the maxDepth method on different strings and print the results.
