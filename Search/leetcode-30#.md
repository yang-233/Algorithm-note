# LeetCode 30. Substring with Concatenation of All Words	 [link](https://leetcode.com/problems/substring-with-concatenation-of-all-words/)

## Problem description:

> You are given a string, **s**, and a list of words, **words**, that are all of the same length. Find all starting indices of substring(s) in **s** that is a concatenation of each word in **words** exactly once and without any intervening characters.

## Example:

```
Input:
  s = "barfoothefoobarman",
  words = ["foo","bar"]
Output: [0,9]
Explanation: Substrings starting at index 0 and 9 are "barfoor" and "foobar" respectively.
The output order does not matter, returning [9,0] is fine too.

Input:
  s = "wordgoodgoodgoodbestword",
  words = ["word","good","best","word"]
Output: []
```

## Solution:

### Tags:

#### *[Search](https://github.com/yang-233/Algorithm-note/tree/master/Search)*

### How to do:

> Use the sliding window approach.

### Code:

```c++
class Solution {
public:
    unordered_map<string, int> countFrequency(const vector<string> &words) {
        unordered_map<string, int> freq;
        for(auto i: words) {//count the frequency of the words
            if(freq.find(i) == freq.end())
                freq[i] = 1;
            else
                ++freq[i];
        }
        return freq;
    }
    vector<int> findSubstring(string s, vector<string>& words) {
        vector<int> res;
        if(s.empty() || words.empty())
            return res;
        int wordLen = words[0].length(),
            wordNum = words.size(),
            sLen = s.length();
        unordered_map<string, int> freq = countFrequency(words);//frequency
        for(int i = 0; i < wordLen; ++i) {//loop the length of words
            unordered_map<string, int> cur;
            for(int l = i, r = i, count = 0; r + wordLen <= sLen; r += wordLen) {
                string word = s.substr(r, wordLen);
                if(freq.find(word) == freq.end()){//the word is not in words
                    cur.clear();
                    count = 0;
                    l = r + wordLen;
                } else {
                    if(cur.find(word) == cur.end())
                        cur[word] = 1;
                    else
                        ++cur[word];
                    ++count;
                    if(cur[word] > freq[word]) {
                        for(int j = l;; j += wordLen){
                            string temp = s.substr(j, wordLen);
                            --cur[temp];
                            --count;
                            if(temp == word) {
                                l = j + wordLen;
                                break;
                            }
                        }
                    }
                   if(count == wordNum)
                        res.push_back(l);

                }
            }
        };
        return res;
    }
};
```

### Time complexity:

#### *O (n\*len(word))*

### Space complexity:

#### *O(m)*s

