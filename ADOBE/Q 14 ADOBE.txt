static int MOD=1e9+7;
class Solution {
public:
    int peopleAwareOfSecret(int n, int delay, int forget) {
        vector<long> memo(n+1,1);    // Each day contributes at least to 1 person kowing the secret.
        memo[0]=0;  // End case
        for(int i=1;i<=n;i++)
            for(int j=delay;j<forget;j++) // Number of people that the secret will be forwarded to
                if(i-j>=0)
                    memo[i]=(memo[i]+memo[i-j])%MOD;    // Same as our recursion relation.
        return (memo[n]-memo[n-forget]+MOD)%MOD;  // Subtract the people who found out by the `n-forget` day as observed.
    }
};