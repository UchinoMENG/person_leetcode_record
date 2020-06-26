#### [剑指 Offer 33. 二叉搜索树的后序遍历序列](https://leetcode-cn.com/problems/er-cha-sou-suo-shu-de-hou-xu-bian-li-xu-lie-lcof/)

1. 题目：

   ![image-20200627060031015](https://i.loli.net/2020/06/27/oN96lMDib5hLTrU.png)

2. 分析：

   1. 首先后序遍历的结果是：左子树：右子树：根
   2. 而二叉搜索树的结果是：左子树<根<右子树
   3. 虽然这样也不是很好理解，但是现在就是存在这样的一个解法
   4. 首先在数组中找到根节点，然后从左依次遍历找到第一个大于根节点的位置，这个位置其实是右子树的开始部分，然后由于右子树全部大于根节点，然后找到第一个小于等于根节点的位置，如果此位置和根的位置相同，则为true，然后递归进行检查即可。

3. 代码

   ```java
   class Solution {
       public boolean verifyPostorder(int[] postorder) {
           return dfs(postorder,0,postorder.length-1);
       }
       public boolean dfs(int[] postorder,int left,int right){
           if(left>=right){
               return true;
           }
           int ll = left;
           int base = postorder[right];
           while(postorder[left]<base){
               left++;
           }
           int cha = left;
           while(postorder[left]>base){
               left++;
           }
           return left==right&&dfs(postorder,ll,cha-1)&&dfs(postorder,cha,right-1);
       }
   }
   ```

   