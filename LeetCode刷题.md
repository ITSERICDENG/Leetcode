

## Leetcode189 旋转数组（Rotate Array）

给定一个数组，将数组中的元素向右移动 k 个位置，其中 k 是非负数。
**示例1：**
>**输入:** [1,2,3,4,5,6,7] 和 k = 3
**输出:** [5,6,7,1,2,3,4]
**解释:**
向右旋转 1 步: [7,1,2,3,4,5,6]
向右旋转 2 步: [6,7,1,2,3,4,5]
向右旋转 3 步: [5,6,7,1,2,3,4]

**示例2：**
>**输入:** [-1,-100,3,99] 和 k = 2
**输出:** [3,99,-1,-100]
**解释:**
向右旋转 1 步: [99,-1,-100,3]
向右旋转 2 步: [3,99,-1,-100]

**思路1：**
采取反转数组来实现。分别反转前n-k个数和后k个数，最后整体反转整个数组。
时间复杂度o(n),空间复杂度o(1)。
JAVA实现：
```
class Solution {
    public void rotate(int[] nums, int k) {
        int n = nums.length;
        k = k%n;
        if(nums.length==0||k==0)
            return;
        reverse(nums,0,n-k-1);
        reverse(nums,n-k,n-1);
        reverse(nums,0,n-1);
    }
    public static void reverse(int[] nums,int start,int end){
        while(start<end){
            int temp = nums[start];
            nums[start++] = nums[end];
            nums[end--] = temp;
        }
    }
}
```

**思路2：**
通过不停的交换数组来实现，每个K长度为一块，交换完毕后，已交换的不动，从后面继续重新交换。
时间复杂度o(n),空间复杂度o(1)。
JAVA实现
```
class Solution {
    public void rotate(int[] nums, int k) {
        int n = nums.length;
        k = k%n;
        if(nums.length==0||k==0)
            return;
        int start = 0;
        while(n!=0&&(k%=n)!=0){
            for(int i=0;i<k;i++){
                int temp = nums[n+i-k+start];
                nums[n+i-k+start] = nums[i+start];
                nums[i+start] = temp;
            }
            n -= k;
            start += k;
        }
    }
}
```

## LeetCode217 存在重复

给定一个整数数组，判断是否存在重复元素。
如果任何值在数组中出现至少两次，函数返回 true。如果数组中每个元素都不相同，则返回 false。
**示例1：**
>**输入:** [1,2,3,1]
**输出:** true

**示例2：**
>**输入:** [1,2,3,4]
**输出:** false

**示例3：**
>**输入:** [1,1,1,3,3,4,3,2,4,2]
**输出:** true

**思路1：**
先排序数组，再比较相邻两个数是否相同。
时间复杂度o(n)+排序复杂度,空间复杂度o(1)。
JAVA实现：
```
class Solution {
    public boolean containsDuplicate(int[] nums) {
        Arrays.sort(nums);
        for(int i=1;i<nums.length;i++){
            if(nums[i]==nums[i-1])
                return true;
        }
        return false;
    }
}
```

## LeetCode136 只出现一次的数字

给定一个非空整数数组，除了某个元素只出现一次以外，其余每个元素均出现两次。找出那个只出现了一次的元素。
说明：
你的算法应该具有线性时间复杂度。 你可以不使用额外空间来实现吗？
**示例1：**
>**输入:** [2,2,1]
**输出:** 1

**示例2：**
>**输入:** [4,1,2,1,2]
**输出:** 4

**思路1：**
利用异或的思想。相同的数异或得0,0与任何数异或得其本身。因此将数组内所有数全部异或就可得到只出现一次的数。
时间复杂度o(n),空间复杂度o(1)。
JAVA实现：
```
class Solution {
    public int singleNumber(int[] nums) {
        int num = nums[0];
        for(int i=1;i<nums.length;i++)
            num^=nums[i];
        return num;
    }
}
```

## LeetCode350 两个数组的交集Ⅱ

给定两个数组，写一个方法来计算它们的交集。
**例如：**
>给定 nums1 = [1, 2, 2, 1], nums2 = [2, 2], 返回 [2, 2].

**思路1：**
将两个数组排序，依次从索引0开始比较，相同就加入输出数组，大的就索引加一。
时间复杂度o(n)+排序复杂度,空间复杂度o(1)。
JAVA实现：
```
class Solution {
    public int[] intersect(int[] nums1, int[] nums2) {
        Arrays.sort(nums1);
        Arrays.sort(nums2);
        int[] res = new int[nums1.length < nums2.length ? nums1.length : nums2.length];
        int i = 0, j = 0, k = 0;
        while (i < nums1.length && j < nums2.length) {
            if (nums1[i] == nums2[j]) {
                res[k++] = nums1[i];
                i++;
                j++;
            } else if (nums1[i] < nums2[j]) {
                i++;
            } else {
                j++;
            }
        }
        return Arrays.copyOfRange(res, 0, k);
    }
}
```
