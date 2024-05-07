# mohinee
<br>
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

<br>
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
