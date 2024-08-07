# Leetcode & GeeksforGeeks
<h3>Reverse Integer</h3>

    class Solution {
        public int reverse(int x) {
            int r1=0,rev=0;
            while(x!=0) {
                r1=x%10;
                
                x=x/10;
                if(rev>Integer.MAX_VALUE/10 || rev<Integer.MIN_VALUE/10) {
                    return 0;
                }
                rev=rev*10+r1;
            }
            return rev;
        }
    }
    
<h3>Double a Number Represented as a Linked List</h3>

    class Solution {
        public ListNode doubleIt(ListNode head) {
   
            ListNode start=null;
            head=reverseLL(head);
            int carry=0;
            int ans=0;
        
            while(head!=null){
                ans=carry+(head.val*2);
            
                int data=ans%10;
                ListNode newNode= new ListNode(data);
                if(start!=null){
                    newNode.next=start;
                }
                start=newNode;
        
                carry=ans/10;
                head=head.next;
            }
      
            while(carry!=0){
                int c=carry%10;
                carry/=10;
                ListNode newNode= new ListNode(c);
          
                  newNode.next=start;
                  start=newNode;
            }
            return start;
        }
    
         static ListNode reverseLL(ListNode pre){
       
            if(pre==null || pre.next==null){
               return pre;
            }
            ListNode curr=pre.next;
                pre.next=null;
                while(curr!=null){
                ListNode temp=curr.next;
                curr.next=pre;
                pre=curr;
                curr=temp;
               }
         return pre;
        }
    }
    
<h3>check if the linked list has a loop</h3>

    class Solution {
        public static boolean detectLoop(Node head){
            Node slow=head;
            Node fast=head;
            while(fast!=null && fast.next!=null){
                slow=slow.next;
                fast=fast.next.next;
                if(slow==fast){
                    return true;
                }
            }
            return false;
        }
    }
    
<h3>remove a loop in the linked list</h3>

    class Solution {
    
        public static void removeLoop(Node head){
        
            boolean cycle=false;
            Node slow=head;
            Node fast=head;
            Node pre=null;
            while(fast!=null && fast.next!=null){
                slow=slow.next;
                pre=fast.next;
                fast=fast.next.next;
                if(slow==fast){
                    cycle=true;
                    break;
                }
            }
            if(cycle){
                slow=head;
        
                while(slow!=fast){
                    slow=slow.next;
                    pre=fast;
                    fast=fast.next;
                }       
                pre.next=null;
            }
        }
    }
    
<h3>Kadane's Algorithm</h3>

    class Solution{
        
        long maxSubarraySum(int arr[], int n){
            long sum=0;
            long maxsum=Integer.MIN_VALUE;
            for(int i=0;i<n;i++){
                sum += arr[i];
                maxsum=Math.max(maxsum,sum);
                if(sum<0){
                    sum=0;
                }
            }
            return maxsum;
        }
    }

<h3>Index of an extra element</h3>

    class Solution {

        public int findExtra(int n, int arr1[], int arr2[]) {
            int low=0,high=n-1;
            while(low<high){
                int mid=(low+high)/2;
            
                if(arr1[mid]==arr2[mid]){
                    low=mid+1;
                }
                else if(arr1[mid]<arr2[mid]){    
                    if(mid>0 && arr1[mid]==arr2[mid-1]){
                         high=mid-1;
                    }
                    else {
                        return mid;
                    }
                }
            }
            return low;
        }
    }

<h3>Height checker</h3>
    class Solution {

        public int heightChecker(int[] heights) {
            int n=heights.length;
            int ans[]=new int[n];
            int arr[]=new int[100];
            for(int i=0;i<n;i++){
                arr[heights[i]-1] +=1;
            }
             for(int i=0,j=0;j<n;){
                if(arr[i]>0){
                    ans[j]=i+1;
                    arr[i] -=1;
                    j++;
                }
                else{
                    i++;
                }
            }
            int count=0;
             for(int i=0;i<n;i++){
                if(ans[i]!=heights[i]){
                    count++;
                }
            }
            return count;
        }
    }

<h3>Sort an array of 0s,1s and 2s</h3>

    class Solution {

        public void sortColors(int[] nums) {
          int n=nums.length;
          int low=0;
          int mid=0;
          int high=n;
          int temp;
          while(mid<high){
              if(nums[mid]==2){
                high--;
                temp=nums[high];
                nums[high]=nums[mid];
                nums[mid]=temp;        
              }
              else if(nums[mid]==0){
                  temp=nums[mid];
                  nums[mid]=nums[low];
                  nums[low]=temp;
                  low++;
                  mid++;
              }
              else{           
                mid++;
              }
            }
        }
    }

<h3>Rotate matrix</h3>

    class Solution {

        public void rotate(int[][] matrix) {
            int n=matrix.length;

            for(int i=0;i<n;i++){
                for(int j=i;j<n;j++){
                    if(matrix[i][j] != matrix[j][i]){
                        int temp=matrix[i][j];
                        matrix[i][j]=matrix[j][i];
                        matrix[j][i]=temp;
                    }
                }
            }

            for(int i=0;i<n;i++){
                for(int j=0,k=n-1;j<k;j++,k--){
                    int temp=matrix[i][j];
                    matrix[i][j]=matrix[i][k];
                    matrix[i][k]=temp;
                }
            }
        }
    }

<h3>Minimum number of moves to seats everyone</h3>
    
    class Solution {

        public int minMovesToSeat(int[] seats, int[] students) {
            int sum=0;
            Arrays.sort(seats);
            Arrays.sort(students);
            for(int i=0;i<seats.length;i++){
                sum += Math.abs(students[i]-seats[i]);
            }
            return sum;
        }
    }

<h3>Padovan Sequence</h3>

    class Solution {

         public int padovanSequence(int n){
            if(n==0 || n==1 || n==2){
                return 1;
            }
            long prev=1;
            long prev2=1;
            long curr=1;
            long next=0;
        
            for(int i=3;i<=n;i++){
                next=(prev+prev2)%1000000007;
                prev2=prev;
                prev=curr;
                curr=next;
                next=0;
            }
             return (int)curr;
        }  
    }

<h3>Minimum Increment to Make Array Unique</h3>

    class Solution {
    
        public int minIncrementForUnique(int[] nums) {
            Arrays.sort(nums);
            int count=0;
            for(int i=0;i<nums.length-1;i++){
                int incre=0;
                incre = nums[i]-nums[i+1]+1;
            
                if(incre>=0){
                    nums[i+1] += incre;
                    count +=incre;
                }
            }
            return count;
        }
    }

<h3>Mobile Numeric Keypad</h3>

    class Solution {
    
        public long getCount(int n) {
            if (n == 1) {
                return 10; 
            }
            List<int[]> moves = new ArrayList<>();

            moves.add(new int[]{0, 8});
            moves.add(new int[]{1, 2, 4}); 
            moves.add(new int[]{2, 1, 3, 5}); 
            moves.add(new int[]{3, 2, 6}); 
            moves.add(new int[]{4, 1, 5, 7});
            moves.add(new int[]{5, 2, 4, 6, 8}); 
            moves.add(new int[]{6, 3, 5, 9}); 
            moves.add(new int[]{7, 4, 8}); 
            moves.add(new int[]{8, 5, 7, 9, 0});
            moves.add(new int[]{9, 6, 8}); 

            long[][] dp = new long[n][10];

            for (int i = 0; i <= 9; i++) {
                dp[0][i] = 1;
            }

            for (int len = 2; len <= n; len++) {
                for (int key = 0; key <= 9; key++) {
                    dp[len-1][key] = 0;
                    for (int nextKey : moves.get(key)) {
                        dp[len-1][key] += dp[len - 2][nextKey];
                    }
                }
            }

            long totalSequences = 0;
            for (int i = 0; i <= 9; i++) {
                totalSequences += dp[n-1][i];
            }

            return totalSequences;        
        }
    }

<h3>Majority Elemment</h3>

    class Solution {
    
        static int majorityElement(int a[], int size) {
            int e=-1;
            int count=0;
            for(int i=0;i<size;i++){
                if(count==0){
                    e=a[i];
                    count++;
                }
                else if(a[i]==e){
                    count++;
                }
                else{
                    count--;
                }   
            }
            count=0;
            for(int i=0;i<size;i++){
                if(a[i]==e){
                    count++;
                }
            }
            if(count>size/2){
                return e;
            }
            return -1;
        }
    }

<h3>Equilibrium Point</h3>

    class Solution {

        public static int equilibriumPoint(long arr[], int n) {
        
            long suml=arr[0];
            long sumr=arr[n-1];
            int i=0;
            int j=n-1;
            while(i<j){
                if(suml>sumr){
                    j--;
                    sumr=sumr+arr[j];
                }
                else if(suml<sumr){
                    i++;
                    suml=suml+arr[i];
                }
                else{
                    i++;
                    j--;
                    suml=suml+arr[i];
                    sumr=sumr+arr[j];
                }
            }
            if(suml==sumr){
                return i+1;
            }
            return -1;
        }
    }

<h3>Set matrix Zeroes</h3>

    class Solution {
    
        public void setZeroes(int[][] matrix) {
            int col=1;
            int n=matrix.length;
            int m=matrix[0].length;
            for(int i=0;i<n;i++){
                for(int j=0;j<m;j++){ 
                    if(matrix[i][j]==0){
                        if(j==0){
                            col=0;
                        }  
                        else{
                            matrix[i][0]=0;
                            matrix[0][j]=0;
                        }
                    }
                }    
            }

            for(int i=n-1;i>=0;i--){
                for(int j=m-1;j>0;j--){ 
                    if(matrix[0][j]==0 || matrix[i][0]==0){ 
                        matrix[i][j]=0;
                    }
                }    
            }

            if(col==0){
                for(int j=n-1;j>=0;j--){ 
                    matrix[j][0]=0;
                }
            }    
        }    
    }

<h3>Grumpy Bookstore Owner</h3>    

    class Solution {
        public int maxSatisfied(int[] customers, int[] grumpy, int minutes) {
            
            int n=customers.length;
            int total=0;
            int max=0;
            for(int i=0;i<n;i++){
                if(grumpy[i]==0){
                    total +=customers[i];
                }
            }
            int ans=total;
            int count=0;
        
            for(int i=0,j=0;i<n;i++){
                count++;
                if(grumpy[i]==1){
                    ans +=customers[i];
                }
                if(count==minutes){
                    max=Math.max(ans,max);
                    if(grumpy[j]==1){
                        ans -=customers[j];
                    }
                    j++;
                    count--;
                } 
            }
            return max;
        }
    }

<h3>Find the Minimum Area to Cover All Ones</h3>

    class Solution {
        
        public int minimumArea(int[][] grid) {
            int n=grid.length;
            int m=grid[0].length;
            int lft=m;
            int rgt=0;
            int up=n;
            int dwn=0;
        
            for(int i=0;i<n;i++){
                if(lft==1 && rgt==m){
                    break;
                }
                for(int j=0;j<m;j++){
                    if(grid[i][j]==1){
                        lft=Math.min(lft,j+1);
                        rgt=Math.max(rgt,j+1);
                    }
                }   
            }
             for(int i=0;i<m;i++){
                 if(up==1 && dwn==n){
                    break;
                }
                for(int j=0;j<n;j++){
                    if(grid[j][i]==1){
                        up=Math.min(up,j+1);
                        dwn=Math.max(dwn,j+1);
                    }
                }
            }
        
            int l=dwn-up+1;
            int w=rgt-lft+1;
            return l*w;
        }
    }

<h3>Minimum Operations to Make Binary Array Elements Equal to One </h3>

    class Solution {
        public int minOperations(int[] nums) {
        
            int count=0;
            for(int i=0;i<nums.length;i++){
                if(nums[i]==0 && i<nums.length-2){
                     count++;
                     nums[i]=1^nums[i];
                     nums[i+1]=1^nums[i+1];
                     nums[i+2]=1^nums[i+2];
                 }
            }   
        
            for(int i=0;i<nums.length;i++){
                if(nums[i]==0){
                    return -1;
                }
            }
            return count;
        }
    }

<h3>Left Rotate Matrix K Times</h3>

    class Solution {
    
        int[][] rotateMatrix(int k, int mat[][]) {
        // code here
            k=k%mat[0].length;
            rotate(0,k-1,mat);
            rotate(k,mat[0].length-1,mat);
            rotate(0,mat[0].length-1,mat);
            return mat;
        }
    
        void rotate(int s,int e,int[][] mat){
            while(s<e){
                for(int i=0;i<mat.length;i++){
                    int temp=mat[i][s];
                    mat[i][s]=mat[i][e];
                    mat[i][e]=temp;
                }
                s++;
                e--;
            }
        }
    }

<h3>3 Sum</h3>

    class Solution {
    
        public List<List<Integer>> threeSum(int[] nums) {
            Arrays.sort(nums);
            List<List<Integer>> mainlist=new ArrayList<>();
            int sum;

            for(int i=0;i<nums.length-1;i++){
                while( i>0 && i<nums.length && nums[i]==nums[i-1]){
                    i++;
                }
                int j=i+1;
                int k=nums.length-1;
             
                while(j<k){
                    sum=nums[i]+nums[j]+nums[k];
                    if(sum==0){
                        mainlist.add(new ArrayList<>());
                        mainlist.get(mainlist.size()-1).add(nums[i]);
                        mainlist.get(mainlist.size()-1).add(nums[j]);
                        mainlist.get(mainlist.size()-1).add(nums[k]);
                        j++;
                        
                        while(nums[j]==nums[j-1] && j<k){
                            j++;
                        }
                        k--;
                        while(nums[k]==nums[k+1] && j<k){
                            k--;
                        }        
                    }
                    else if(sum<0){
                        j++;
                    }
                    else {
                        k--;         
                    }
                }
            }   
            return mainlist; 
        }
    }

<h3>Merge Intervals</h3>

    class Solution {
    
    public int[][] merge(int[][] intervals) {

        Arrays.sort(intervals,Comparator.comparingDouble(o->o[0]));
        int n=intervals.length;
        List<int[]> ans=new ArrayList<>();

        ans.add(intervals[0]);
        for(int i=1;i<n;i++){
            int end=ans.get(ans.size()-1)[1];
            if(intervals[i][0]<=end){
                ans.get(ans.size()-1)[1]=Math.max(intervals[i][1],end);
            }
            else{
                ans.add(intervals[i]);
            }
        }
        int arr[][]=new int[ans.size()][2];
        for(int i=0;i<ans.size();i++){
                arr[i]=ans.get(i);
        }
        return arr;
    }
    }

<h3>Trapping Rain Water</h3>

    class Solution{
    
    // arr: input array
    // n: size of array
    // Function to find the trapped water between the blocks.
    static long trappingWater(int arr[], int n) { 
        // Your code here
        int left[]=new int[n];
        int right[]=new int[n];
        left[0]=arr[0];
        right[n-1]=arr[n-1];
        
        for(int i=1;i<n;i++){
           left[i]=Math.max(arr[i],left[i-1]);
        }
        
        for(int i=n-2;i>=0;i--){
           right[i]=Math.max(arr[i],right[i+1]);
        }
        
        long maxwater=0;
        for(int i=0;i<n;i++){
            long lvl=Math.min(right[i],left[i]);
            maxwater+=lvl-arr[i];
        }
        return maxwater;
    } 
    }

<h3>4 Sum</h3>

    class Solution {
    
    public List<List<Integer>> fourSum(int[] nums, int target) {
        Arrays.sort(nums);
        int n=nums.length;
        List<List<Integer>> ans=new ArrayList<>();

        for(int i=0;i<n;i++){
            if(i>0 && nums[i]==nums[i-1]){
                continue;
            }
            for(int j=i+1;j<n;j++){
                if(j>i+1 && nums[j]==nums[j-1]){
                    continue;
                }
                int k=j+1;
                int l=n-1;
                while(k<l){
                    long sum=(long)nums[i]+(long)nums[j]+(long)nums[k]+(long)nums[l];
                    if(sum==target){
                        ans.add(new ArrayList<>());
                        ans.get(ans.size()-1).add(nums[i]);
                        ans.get(ans.size()-1).add(nums[j]);
                        ans.get(ans.size()-1).add(nums[k]);
                        ans.get(ans.size()-1).add(nums[l]);
                        k++;
                        l--;
                        while(k<l && nums[k]==nums[k-1]){
                            k++;
                        }
                        while(k<l && nums[l+1]==nums[l]){
                            l--;
                        }
                    }
                    else if(sum>target){
                        l--;
                    }
                    else{
                        k++;
                    }
                }
            }
        }
        return ans;
    }
    }

<h3>Count Inversions</h3>

    class Solution {
    
    // arr[]: Input Array
    // N : Size of the Array arr[]
    // Function to count inversions in the array.
    static long inversionCount(long arr[], int n) {
        // Your Code Here
        return merge(0,n-1,arr);
    }
    
    static long merge(int start,int end,long arr[]){
        long count=0;
        if(start<end){
            int mid=start+(end-start)/2;
            count += merge(start,mid,arr);
            count += merge(mid+1,end,arr);
            count += merging(start,mid,end,arr);
        }
        return count;
    }
    
    static long merging(int start,int mid,int end,long arr[]){
        int left=start;
        int rgt=mid+1;
        long count=0;
        ArrayList<Long> a=new ArrayList<>();

        while(left<=mid && rgt<=end){
            
            if(arr[left]>arr[rgt]){
               a.add(arr[rgt]);
                rgt++;
                count +=mid-left+1;
            }
            else{
               a.add(arr[left]);
               left++;
            }
        }
        
        while(left<=mid ){
            a.add(arr[left]);
            left++;
            // count +=mid-left+1;
        }
        while(rgt<=end){
            a.add(arr[rgt]);
              rgt++;
        }
        
        for(int i=0;i<a.size();i++){
            arr[i+start]=a.get(i);
        }
        return count;
    }
    }

<h3>Find Minimum in Rotated Sorted Array</h3>

    class Solution {
    
    public int findMin(int[] nums) {
        int n=nums.length;
        int low=0;
        int high=n-1;
        int ans = Integer.MAX_VALUE;
        while (low <= high) {
            int mid = (low + high) / 2;

            if (nums[low] <= nums[high]) {
                ans = Math.min(ans, nums[low]);
                break;
            }
            if (nums[low] <=nums[mid]) {
                ans = Math.min(ans,nums[low]);
                low = mid + 1;
            } else { 
                ans = Math.min(ans,nums[mid]);
                high = mid - 1;
            }
        }
        return ans;
    }
    }

<h3>Merge Nodes in Between Zeros</h3>

    class Solution {

    public ListNode mergeNodes(ListNode head) {
        ListNode start=head.next;
        ListNode ptr=head;
        int sum=0;
        while(start!=null){
            if(start.val!=0){
                sum +=start.val;
                start=start.next;
            }
            else{
                ptr.val=sum;
                if(start.next!=null){
                    ptr=ptr.next;
                }
                else{
                    ptr.next=null;
                }
                sum=0;
                start=start.next;
            }
        }
        return head;
    }
    }

<h3>Koko Eating Bananas</h3>

    class Solution {
    public int minEatingSpeed(int[] piles, int h) {
        int n=piles.length;
        int max=piles[0];
        for(int i=1;i<n;i++){
            max=Math.max(max,piles[i]);
        }
        int low=1;
        int high=max;
        while(low<=high){
            int mid=low+(high-low)/2;
             
            double total=0;
            for(int i=0;i<n;i++){
                total=total+Math.ceil((double)piles[i]/(double)mid);
            }

            if(total<=h){
                high=mid-1;
            }
            else{
                low=mid+1;
            }
        }
        return low;
    }
    }

<h3>Capacity To Ship Packages Within D Days</h3>

    class Solution {
    public int shipWithinDays(int[] weights, int days) {
        int n=weights.length;
        int low=0;
        int high=0;
        for(int i=0;i<n;i++){
            low=Math.max(low,weights[i]);
            high += weights[i];
        }
        while(low<=high){
            int mid=low+(high-low)/2;
            int sum=0;
            int count=1;
            for(int i=0;i<n;i++){
                if(sum+weights[i]<=mid){
                    sum +=weights[i];
                }
                else{
                    count++;
                    sum=weights[i];
                }
            }
            if(count<=days){
                high=mid-1;
            }
            else{
                low=mid+1;
            }
        }
        return low;
    }
    }

<h3>Find the Smallest Divisor Given a Threshold</h3>

    class Solution {
    public int smallestDivisor(int[] nums, int threshold) {
        int n=nums.length;
        int high=0;
        for(int i=0;i<n;i++){
            high=Math.max(high,nums[i]);
        }
        int low=1;
        while(low<=high){
            int mid=low+(high-low)/2;
            double count=0;
            for(int i=0;i<n;i++){
                count += Math.ceil((double)nums[i]/(double)mid);
            }
            if(count<=threshold){
                high=mid-1;
            }
            else{
                low=mid+1;
            }
        }
        return low;
    }
    }

<h3>K-th Element of Two Arrays</h3>

    class Solution {
    public long kthElement( int arr1[], int arr2[], int n, int m, int k) {
        if(n>m){
            return kthElement(arr2,arr1,m,n,k);
        }
        int low=Math.max(0,k-m);
        int high=Math.min(n,k);

        while(low<=high){
            int mid1=low+(high-low)/2;
            int mid2=Math.abs(k-mid1);
            
            int l1=Integer.MIN_VALUE;
            int l2=Integer.MIN_VALUE;
            int r1=Integer.MAX_VALUE;
            int r2=Integer.MAX_VALUE;
            
            if(mid1<n) r1=arr1[mid1];
            if(mid2<m) r2=arr2[mid2];
            if(mid1-1>=0) l1=arr1[mid1-1];
            if(mid2-1>=0) l2=arr2[mid2-1];
            
            if(l2<=r1 && l1<=r2){
                return Math.max(l1,l2);
            }
            if(l2>r1){
                low=mid1+1;
            }
            else{
                high=mid1-1;
            }
        }
        return 0;
    }
    }

<h3>Subarray with given XOR</h3>

    public class Solution {
    
    public int solve(ArrayList<Integer> A, int B) {
        int count=0;
        int n=A.size();
        Map<Integer,Integer> hm=new HashMap<>();
        hm.put(0,1);
        int xor=0;
        for(int i=0;i<n;i++){
            xor ^=A.get(i);
            int rem=xor^B;
            if(hm.containsKey(rem)){
                count+=hm.get(rem);
            }
                hm.put(xor,hm.getOrDefault(xor,0)+1);
        }
        return count;
    }
    }

<h3>0 - 1 Knapsack Problem</h3>

    class Solution {
    
    //Function to return max value that can be put in knapsack of capacity W.
    static int knapSack(int W, int wt[], int val[], int n) { 
         // your code here 
         int arr[][]=new int[val.length+1][W+1];
         
         for(int i=0;i<arr.length;i++){
            arr[i][0]=0;
         }
         
         for(int j=0;j<arr[0].length;j++){
            arr[0][j]=0;
         }
         
         for(int i=1;i<arr.length;i++){
             for(int j=1;j<arr[0].length;j++){
                if(j>=wt[i-1]){
                    arr[i][j]=Math.max(val[i-1]+arr[i-1][j-wt[i-1]],arr[i-1][j]);
                }
                else{
                    arr[i][j]=arr[i-1][j];
                }
            }
        }
        return arr[arr.length-1][arr[0].length-1];
    } 
    }

<h3>Reverse a Stack</h3>

    class Solution{
    
    static void reverse(Stack<Integer> s){
    
        // add your code here
        if(!s.isEmpty()){
            int x=s.pop();
            reverse(s);
            pushBack(s,x);
        }
    }
    static void pushBack(Stack<Integer> s,int x){
        if(s.isEmpty()){
            s.push(x);
        }
        else{
            int temp =s.pop();
            pushBack(s,x);
            s.push(temp);
        }
    }
    }
