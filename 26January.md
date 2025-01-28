Problem Statement: Given a string s, rearrange the characters of s so that any two adjacent characters are not the same.

Return any possible rearrangement of s or return "" if not possible.

Platform: Leetcode

Approach:
Step 1: Count the frequency of each character.
Step 2: If the frequency of any character is more than (n + 1) / 2 where n is the length of the string, it's impossible to rearrange the string as required.
Step 3: Use a max-heap (priority queue) to store characters based on their frequencies, and then build the rearranged string by placing characters with the highest frequencies in alternating positions.
```
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
```
