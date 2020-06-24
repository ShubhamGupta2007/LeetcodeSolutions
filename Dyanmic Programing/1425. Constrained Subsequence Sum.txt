//using deque and sliding window approach

class Solution {
public:
    int constrainedSubsetSum(vector<int>& nums, int k) {
        vector<int>dp(nums.size());
	
        int ans=nums[0];
	dp[0]=nums[0];
        deque<pair<int,int>>q;
        q.push_back(make_pair(dp[0],0));
        for(int i=1;i<nums.size();i++)
        {
	    //shrink the window	
            while(!q.empty()&&i-q.front().second>k)
            {
                q.pop_front();
            }
            dp[i]=nums[i]+max(0,q.front().first);
            
	    //maintaining the heap
	    while(!q.empty()&&dp[i]>q.back().first)
            {
                q.pop_back();
            }
            q.push_back(make_pair(dp[i],i));
           // cout<<dp[i]<<" ";
            ans=max(ans,dp[i]);
        }
        return ans;
    }
};