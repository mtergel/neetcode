```cpp
// Problem: https://www.lintcode.com/problem/659/
// Time O(N)
// Space O(N)

class Solution {
public:
    /*
     * @param strs: a list of strings
     * @return: encodes a list of strings to a single string.
     */
    string encode(vector<string> &strs) {
        // write your code here
        string res = "";
        
        // length + delimiter
        // 4#
        for (int i = 0; i < strs.size(); i++)
        {
            res += to_string(strs[i].size()) + "#" + strs[i];
        }

        return res;
    }

    /*
     * @param str: A string
     * @return: dcodes a single string to a list of strings
     */
    vector<string> decode(string &str) {
        // write your code here
        vector<string> res;
        int i = 0, j = 0;
        int len = 0;

        while (i < str.size())
        {
            j = i;
            while (str[j] != '#')
            {
                len = len * 10 + (str[j] - '0');
                j++;
            }
            // len = atoi(str.substr(i, j))

            res.push_back(str.substr(j + 1, len));
            i = j + 1 + len;
            len = 0;
        }
        
        return res;
    }
};
```