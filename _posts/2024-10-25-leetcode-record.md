---
title: "LeetCode Record"
toc: true
categories: 
    - Algorithm
tags: 
    - Algorithm
    - Leetcode
---

# LeetCode 75
## Array / String
### 345. Reverse Vowels of a String
* Easy
* 2024-10-25
* C++
* Runtime 0ms Beats 100.00%
* Memory 9.39MB Beats 79.14%
{: .notice--info}

Note
: * 被LeetCode 75歸類在 Array/String, 但我是用two pointer來處理
: * 用 unordered_set 結果runtime更高

<b>Solution</b>
{% capture code %}
{% highlight cpp linenos %}
class Solution {
public:
    char vowelArray[5] = {'a', 'e', 'i', 'o', 'u'};

    string reverseVowels(string s) {
        int first = 0, end = s.size();
        while (first < end) {
            while (!checkIsVowel(s[first]) && first < end)
                first++;
            while (!checkIsVowel(s[end]) && first < end)
                end--;
            swap(s[first], s[end]);
            first++;
            end--;
        }

        return s;
    }

    bool checkIsVowel(char c) {
        for(int i=0; i<5; i++) {
            if(c == vowelArray[i] || c+32 == vowelArray[i]) {
                return true;
            }
        }
        return false;
    }
}
{% endhighlight %}
{% endcapture %}
{% include collapsible_code.html title="cpp solution" content=code %}

### 151. reverse-words-in-a-string
* Medium
* 2024-10-29
* C++
* Runtime 3ms Beats 45.45%
* Memory 9MB Beats 73.07%
{: .notice--info}

Note
: * 這題是用follow-up的方式來解
: * 先把頭尾的空白去掉，然後把整個字串reverse，再把每個word reverse
: * 中間遇到超過2個以上的空白用erase來處理

<b>Solution</b>
{% capture code %}
{% highlight cpp linenos %}
class Solution {
public:
    string reverseWords(string s) {
        // Follow-up
        trim(s);

        // Reverse all the words
        reverse(s.begin(), s.end());
        s += ' ';

        int word_start = 0;
        int space_start = 0;
        bool isWordStart = 1;
        // Reverse each word
        for (int i=0; i<s.length(); i++) {
            // Word Start
            if (s[i] != ' ') {
                if (!isWordStart) {
                    int erase_len = i-space_start-1;
                    if (erase_len >= 1) {
                        s.erase(space_start+1, erase_len);
                        i = i - erase_len;
                    }
                    word_start = i;
                    isWordStart = 1;
                }
            } else {
                if (isWordStart) {
                    // Reverse Word
                    reverse(s.begin() + word_start, s.begin() + i);
                    space_start = i;
                    isWordStart = 0;
                }
            }
        }
        s.pop_back();

        return s;
   }

void trim(string& str) {
    auto is_space = [](unsigned char ch) { return isspace(ch); };

    string::iterator start = find_if_not(str.begin(), str.end(), is_space);

    string::iterator end = find_if_not(str.rbegin(), str.rend(), is_space).base();

    if (start >= end) {
        str.clear();
        return;
    }

    str = string(start, end);
}
};
{% endhighlight %}
{% endcapture %}
{% include collapsible_code.html title="cpp solution" content=code %}

