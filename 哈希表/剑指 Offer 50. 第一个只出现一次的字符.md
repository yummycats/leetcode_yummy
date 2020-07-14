# 剑指 Offer 50. 第一个只出现一次的字符
在字符串 s 中找出第一个只出现一次的字符。如果没有，返回一个单空格。 s 只包含小写字母。

示例:
```
s = "abaccdeff"
返回 "b"

s = "" 
返回 " "
 

限制：

0 <= s 的长度 <= 50000
```
# 方法：哈希表
```
class Solution {
    public char firstUniqChar(String s) {
        HashMap<Character,Integer> map  = new HashMap<>();
        int len = s.length();
        char res='a';

        if(len==0){
            return ' ';
        }else{
            //从后往前遍历，如果键（字符）对应的值为1，那么键赋值给res
            for(int i=0;i<len;i++){
                int count = map.getOrDefault(s.charAt(i),0)+1;
                map.put(s.charAt(i),count);

            }
            int i=0;
            while(i<len){
                if(map.get(s.charAt(i))==1){
                    break;
                } 
                i++;
            }
            if(i==len) {
                return ' ';
            }else{
                res = s.charAt(i);
            }
        }
        return res;
    }
}
```
# 方法二： 优化版：有序哈希表，第二次遍历 遍历的是去重后的哈希表，速度要更快，而且出现次数大于1的键它的值设置为false, 简化代码逻辑
```
class Solution {
    public char firstUniqChar(String s) {
        Map<Character, Boolean> dic = new LinkedHashMap<>();
        char[] sc = s.toCharArray();
        for(char c : sc)
            dic.put(c, !dic.containsKey(c));
        for(Map.Entry<Character, Boolean> d : dic.entrySet()){
           if(d.getValue()) return d.getKey();
        }
        return ' ';
    }
}

```

作者：jyd
链接：https://leetcode-cn.com/problems/di-yi-ge-zhi-chu-xian-yi-ci-de-zi-fu-lcof/solution/mian-shi-ti-50-di-yi-ge-zhi-chu-xian-yi-ci-de-zi-3/
