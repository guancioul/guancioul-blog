---
title: "Algorithm"
categories:
  - Blog
tags:
  - Post Formats
  - readability
  - standard
published: false
---

## 自定義的sort
一般的sort都是從小排到大，如果是二維陣列要以後面的值排序要怎麼做

### Code
{% highlight cpp %}
// 第一種方式，額外寫一個function
// 這個寫法是如果string的長度不同時，會先將長度由小排到大，長度相同時，才會依照字母的順序排
bool comp(string a, string b){
    if (a.size() != b.size()) return a.size() < b.size();
        return a < b;
}
int main(){
    vector<string> vec = {"asdasgsa", "qwhsaf", "abc", "cba"};
    sort(vec.begin(), vec.end(), comp);
    for(auto s:vec) cout << s << "\n";
    return 0;
}
//abc
//cba
//qwhsaf
//asdasgsa

//第二種方式，直接把comp寫在sort裡面
// 這個寫法是二維矩陣中，排序第二個位置的值，由大排到小
int main(){
    vector<vector<int>> boxTypes = { {5,10}, {2,5}, {4,7}, {3,9} };
    sort(boxTypes.begin(),boxTypes.end(),[](vector<int> &first, vector<int> &second){
        return first[1]>second[1];
    });
    for(auto box:boxTypes) cout << box[0] << " " << box[1] << "\n";
    return 0;
}
{% endhighlight %}

## 反轉數字
有一個數字123，要怎麼把他反過來變成321<br>
210變成12<br>
等等<br>

### Solution
先設一個變數reverse等於0<br>
123%10後，會餘3<br>
reverse乘上10倍後，加上前面的餘數，會變成3<br>
再把123/10，會等於12<br>
<br>
再做一次<br>
12%10=2<br>
3*10+2=32<br>
12/10=1<br>
<br>
1%10=1<br>
32*10+1=321<br>
1/10=0<br>
最後因為值等於0所以跳出這個迴圈<br>

### Code
{% highlight cpp %}
int main(){
    vector<int> vec = {123, 210};
    for(auto v:vec){
        int reverse = 0;
        while(v!=0){
            int remainder = v%10;
            reverse = reverse*10 + remainder;
            v /= 10;
        }
        cout << reverse << "\n";
    }
    return 0;
}
{% endhighlight %}