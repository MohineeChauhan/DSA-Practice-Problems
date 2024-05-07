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
