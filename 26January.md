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
