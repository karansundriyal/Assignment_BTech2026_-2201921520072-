# Assignment_BTech2026_-2201921520072-
Problem Statement: Given a string s, rearrange the characters of s so that any two adjacent characters are not the same.

Return any possible rearrangement of s or return "" if not possible.

 

Example 1:

Input: s = "aab"
Output: "aba"
Example 2:

Input: s = "aaab"
Output: ""

Platform Use: Leetcode

Approach:
1. Count character frequencies using a hash map (unordered_map).
2. Use a max heap to always pick the character with the highest frequency.
3. Greedily construct the string by placing the most frequent character in the result and ensuring that adjacent characters are not the same.

Code:
class Solution {
public:
    string reorganizeString(string s) {
        unordered_map<char, int> freq;
        for (char c : s) {
            freq[c]++;
        }

        
        priority_queue<pair<int, char>> maxHeap;
        for (auto& entry : freq) {
            maxHeap.push({entry.second, entry.first});
        }

        
        string result = "";
        pair<int, char> prev = {0, '#'};  

        while (!maxHeap.empty()) {
            auto curr = maxHeap.top();
            maxHeap.pop();

            
            result += curr.second;

            
            if (prev.first > 0) {
                maxHeap.push(prev);
            }

            
            curr.first--;

            
            prev = curr;
        }

        
        return result.size() == s.size() ? result : "";
    
    }
};

Explanation:
1. Frequency Map:

We count the frequency of each character in the input string s using an unordered map (unordered_map<char, int>).

2. Max Heap:

We use a priority queue (max heap) to always select the character with the highest remaining frequency.
The priority queue stores pairs where the first element is the character's frequency, and the second element is the character itself.

3. Greedy String Construction:

We initialize a prev variable to keep track of the previous character and its frequency. We use this to ensure that we don't place the same character adjacent to itself.
At each step, we extract the most frequent character, add it to the result, and decrease its frequency.
If the frequency of the current character is greater than zero, we put it back into the heap.

4. Edge Case Handling:

If at any point, it becomes impossible to rearrange the string (e.g., a character has too high a frequency relative to the length of the string), we return an empty string.

5. Result Check:

After building the result, we check if its size matches the original string. If they match, we return the result. If not, we return an empty string because the rearrangement wasn't possible.
