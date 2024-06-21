# mohinee
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

    
