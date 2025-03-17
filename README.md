[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/wek6H0xj)
# Jump Game
class Solution {
public:
    bool canJump(vector<int>& nums) {
        int maxReach = 0; // Farthest index we can reach
        
        for (int i = 0; i < nums.size(); i++) {
            if (i > maxReach) return false; // If we can't reach this index, return false
            maxReach = max(maxReach, i + nums[i]); // Update the farthest reachable index
            if (maxReach >= nums.size() - 1) return true; // If we can reach the last index, return true
        }
        
        return false;
    }
};
# Unique Paths
class Solution {
public:
    int uniquePaths(int m, int n) {
        vector<vector<int>> dp(m, vector<int>(n, 1)); // Initialize all cells with 1
        
        for (int i = 1; i < m; i++) {
            for (int j = 1; j < n; j++) {
                dp[i][j] = dp[i - 1][j] + dp[i][j - 1]; // Sum of top and left cells
            }
        }
        
        return dp[m - 1][n - 1]; // Bottom-right cell
    }
};
# Coin Change
class Solution {
public:
    int coinChange(vector<int>& coins, int amount) {
        vector<int> dp(amount + 1, amount + 1); // Fill with a large number
        dp[0] = 0; // Base case: 0 coins for amount 0

        for (int coin : coins) { // Iterate through each coin
            for (int j = coin; j <= amount; j++) { // Check all amounts >= coin
                dp[j] = min(dp[j], dp[j - coin] + 1); // Take the minimum
            }
        }

        return dp[amount] == amount + 1 ? -1 : dp[amount];
    }
};
# Longest Increasing Subsequence
class Solution {
public:
    int lengthOfLIS(vector<int>& nums) {
        int n = nums.size();
        if (n == 0) return 0;

        vector<int> dp(n, 1); // Initialize DP array with 1
        int maxLIS = 1; // Track the maximum LIS found

        for (int i = 1; i < n; i++) {
            for (int j = 0; j < i; j++) {
                if (nums[i] > nums[j]) {
                    dp[i] = max(dp[i], dp[j] + 1);
                }
            }
            maxLIS = max(maxLIS, dp[i]);
        }

        return maxLIS;
    }
};
# Maximum Product Subarray
class Solution {
public:
    int maxProduct(vector<int>& nums) {
        if (nums.empty()) return 0;

        int maxProd = nums[0]; // Stores the final maximum product
        int minProd = nums[0]; // Stores the minimum product (for negative numbers)
        int result = nums[0];  // Stores the overall maximum

        for (int i = 1; i < nums.size(); i++) {
            if (nums[i] < 0) swap(maxProd, minProd); // Swap because multiplying by a negative flips the min/max

            maxProd = max(nums[i], maxProd * nums[i]); // Max product at this index
            minProd = min(nums[i], minProd * nums[i]); // Min product at this index

            result = max(result, maxProd); // Update the final result
        }

        return result;
    }
};
# Decode Ways
class Solution {
public:
    int numDecodings(string s) {
        if (s.empty() || s[0] == '0') return 0; // If first character is '0', return 0

        int n = s.size();
        vector<int> dp(n + 1, 0);
        dp[0] = 1; // Base case: Empty string has 1 way
        dp[1] = s[0] != '0' ? 1 : 0; // First character is valid or not

        for (int i = 2; i <= n; i++) {
            // Single digit decoding (if valid)
            if (s[i-1] != '0') {
                dp[i] += dp[i-1];
            }
            // Two-digit decoding (if valid 10-26)
            int twoDigit = stoi(s.substr(i-2, 2));
            if (twoDigit >= 10 && twoDigit <= 26) {
                dp[i] += dp[i-2];
            }
        }

        return dp[n];
    }
};
# Perfect Squares
class Solution {
public:
    int numSquares(int n) {
        vector<int> dp(n + 1, INT_MAX);
        dp[0] = 0; // Base case: sum of 0 requires 0 numbers

        for (int i = 1; i <= n; i++) {
            for (int j = 1; j * j <= i; j++) {
                dp[i] = min(dp[i], dp[i - j * j] + 1);
            }
        }

        return dp[n];
    }
};
# Word Break
#include <vector>
#include <string>
#include <unordered_set>

class Solution {
public:
    bool wordBreak(string s, vector<string>& wordDict) {
        unordered_set<string> wordSet(wordDict.begin(), wordDict.end());
        int n = s.size();
        vector<bool> dp(n + 1, false);
        dp[0] = true;

        for (int i = 1; i <= n; i++) {
            for (int j = 0; j < i; j++) {
                if (dp[j] && wordSet.find(s.substr(j, i - j)) != wordSet.end()) {
                    dp[i] = true;
                    break;
                }
            }
        }

        return dp[n];
    }
};

