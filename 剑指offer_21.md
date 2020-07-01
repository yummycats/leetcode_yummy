## 调整数组顺序使奇数位于偶数前面

输入一个整数数组，实现一个函数来调整该数组中数字的顺序，使得所有奇数位于数组的前半部分，所有偶数位于数组的后半部分。

```
输入：nums = [1,2,3,4]
输出：[1,3,2,4] 
注：[3,1,2,4] 也是正确的答案之一。
```

提示：

1. 1 <= nums.length <= 50000
2. 1 <= nums[i] <= 10000

java
### 方法一：开辟另一个数组，两轮for循环
```
class Solution {
    public int[] exchange(int[] nums) {
        int len = nums.length;
        int index = 0;
        int[] res = new int [len];
        for(int i=0;i<len;i++){
            if(nums[i]%2!=0){
                res[index++] = nums[i];
            }
        }
        for(int i=0;i<len;i++){
            if(nums[i]%2==0){
                res[index++] = nums[i];
            }
        }
    return res;
        
    }
}
```
### 方法二： 双指针
```
class Solution {
    public int[] exchange(int[] nums) {
    int len = nums.length;
        if(nums==null || len==0) {
            return nums;
        }

        int left=0,right=len-1,temp ;
        
        while(left<right ){
            while(left<len && (nums[left] & 1)== 1 ){//如果遇到奇数，继续向右走，直到碰到偶数
                left++;
            }
            while(right>=0 && (nums[right] & 1)== 0){//如果遇到偶数，继续向左走，直到碰到奇数
                right--;
            }
            if(left<right){
                temp = nums[left];
                nums[left] = nums[right];
                nums[right] = temp;
            }          
        }        
return nums;     
    }
}
```

