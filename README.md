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
class Solution
{
    
    public static void removeLoop(Node head){
        // code here
        // remove the loop without losing any nodes
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

    // arr: input array
    // n: size of array
    //Function to find the sum of contiguous subarray with maximum sum
    
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
