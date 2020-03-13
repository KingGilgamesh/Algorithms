1. The KMP algorithm

+ Suffix
  Given a string S[0,...,m-1], the substring s[i,m-1](0 <= i <= m-1) is a suffix of S.  
+ Partial Match Table next[q]
  + next[q] = max{k:k < q and P[0,k] is a suffix of P[0,q]};
  + PMT: for every position in the string, a corresponding longest match is recorded;
  + relations between next[q] and PMT: by right shifting the PMT by 1 position and adding -1 at the first position, PMT is converted to next[q].
  
next[q] array(or PMT) is the key in KMP algorithm. Assume we have computed next[q-1] = k-1(which means P[0,k-1] is a suffix of P[0,q-1]), next we want to compute next[q] = k(find the longest match substring), if P[k] = P[q], then P[0,k] is a suffix of P[0,q], and all of P[0,k]'s substring are suffixes of P[0,q], and continue to check until P[k'] != P[q'], when this happens, recursively call q = next[q].

Simple illustration: Assume we have a string P[0,1,2,3,4,5] = "ababac", P[0,1] is a suffix of P[0,1,2,3], where k = 1, q = 3(by index or length doesn't matter, here k denotes the index of the last matched element). Next we compare P[k = k+1](a) with P[q = q + 1](a),still match, and repeated until encounter c, when we have to go back to next[5] = 0. 

* Java
```java
public class KMP{
    public static void main(String[] args){
         String str = "abababdafdasabcfdfeaba";
        String pattern = "abc";
        int[] nextTable = KMP.next(pattern);
        int idx = KMP.KMP(str, pattern, nextTable);
        System.out.println(idx);
    }

    public static int[] next(String pattern){
        int k = -1;//k is used to find the longest substring match
        int[] next = new tne[pattern/length()];

        for(int q = 0; q < pattern.length(); q++){
            while(k >= 0 && pattern.charAt(k) != pattern.charAt(q))k = next[k];
        }
        if(P[k + 1] == P[q])
    }
}
```