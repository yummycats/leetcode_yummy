# 378. 有序矩阵中第K小的元素
给定一个 n x n 矩阵，其中每行和每列元素均按升序排序，找到矩阵中第 k 小的元素。
请注意，它是排序后的第 k 小元素，而不是第 k 个不同的元素。

 

####  示例：

matrix = [
   [ 1,  5,  9],
   [10, 11, 13],
   [12, 13, 15]
],
k = 8,

返回 13。
 

#### 提示：
你可以假设 k 的值永远是有效的，1 ≤ k ≤ n2 

## 方法一：归并排序（运用PriorityQueue数据结构）

#### 思路：
1. 首先将第一列的元素进队，以数组的形式new int[]{matrix[i][0], i, 0}
2. 将最小值出队，并将最小值右边（如果有）的数进队
3. 重复k次
```
class Solution {
    public int kthSmallest(int[][] matrix, int k) {
        PriorityQueue<int[]> pq = new PriorityQueue<int[]>(new Comparator<int[]>() {
            public int compare(int[] a, int[] b) {
                return a[0] - b[0];
            }
        });
        int n = matrix.length;
        for (int i = 0; i < n; i++) {
            pq.offer(new int[]{matrix[i][0], i, 0});//把数值和坐标当作一个数组存储在优先队列的一项中，比较时，比较的是矩阵对应坐标的数值
        //这句话是把矩阵的第一列，存储在优先队列中
        }
        for (int i = 0; i <k - 1; i++) {
            int[] now = pq.poll();//获取并移除队列的头，最小值出队
            // System.out.println(now[0]+","+now[1]+","+now[2]);
            if (now[2] != n - 1) {//如果列在范围内，那么右侧的第一个数进队
                pq.offer(new int[]{matrix[now[1]][now[2] + 1], now[1], now[2] + 1});
            }
        }
        return pq.poll()[0];
    }
}

```
