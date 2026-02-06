# Edit Distance Solution

## Algorithm: Dynamic Programming

This solution implements the classic Edit Distance (Levenshtein Distance) algorithm using dynamic programming.

## Code

```java
class Solution {
public:
    int minDistance(string word1, string word2) {
        int m = (int)word1.size(), n = (int)word2.size();
        vector<int> dp(n + 1, 0);
        // dp[0..n] for i = 0
        for (int j = 0; j <= n; j++) dp[j] = j;
        for (int i = 1; i <= m; i++) {
            int prevDiag = dp[0]; // old dp[i-1][0]
            dp[0] = i;            // new dp[i][0]
            for (int j = 1; j <= n; j++) {
                int temp = dp[j]; // old dp[i-1][j]
                if (word1[i - 1] == word2[j - 1]) {
                    dp[j] = prevDiag; // dp[i-1][j-1]
                } else {
                    dp[j] = 1 + min({prevDiag, dp[j], dp[j - 1]});
                    // prevDiag: replace, dp[j]: delete, dp[j-1]: insert
                }
                prevDiag = temp;
            }
        }
        return dp[n];
    }
};
```