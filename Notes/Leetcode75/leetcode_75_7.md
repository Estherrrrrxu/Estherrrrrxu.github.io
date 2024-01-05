# Queue

## [933. Number of Recent Calls](https://leetcode.com/problems/number-of-recent-calls/)

**Question** Implement `RecentCounter` class which counts the number of recent requests within a certain time frame. Initializes the counter with zero recent requests. Calls `ping(int t)` where `t` is the current timestamp (in milliseconds) and returns the number of requests that has happened in the past `3000` milliseconds (including the current call). Multiple calls to `ping` may happen before a call to `current` returns.

**Solution** Use a queue like a sliding window. Append the current timestamp to the queue. Then, pop the queue until the first element is within the time frame. Time complexity is `O(1)` and space complexity is `O(1)`.

## [649. Dota2 Senate](https://leetcode.com/problems/dota2-senate/)

**Question** Given a string `senate` represent each senator's party beloing to `R` or `D`. In each round, each senator either bans another senator or announces victory if all left senators are all belong to the same party. Output the winner party as `Radiant` or `Dire`.

**Solution** The best strategy is to ban the next closest opponent. Taking two arrays `r_ind` and `d_ind` to track the index of `R` and `D` senators. Then, use a queue to track the order of banning. A simplified version is to retreat `senate` as a queue, and use a counter to track the available senator for each party. Time complexity is `O(n)` and space complexity is `O(n)`.

```python
def predictPartyVictory(self, senate: str) -> str:
    # Eligible Senators of each party
    r_count = senate.count('R')
    d_count = len(senate) - r_count

    # Floating Ban Count
    # It tracks the number of bans that are applied to corresponding party
    # If the count is 0, means the current senator is eligible to vote
    d_floating_ban = 0
    r_floating_ban = 0

    # Queue of Senators can vote
    q = deque(senate)

    # While any party has eligible Senators
    while r_count and d_count:

        # Get the current senator to vote
        curr = q.popleft()

        if curr == 'D':
            # if not eligible
            if d_floating_ban:
                d_floating_ban -= 1 # decrease floating ban amount
                d_count -= 1 # decrease left senator amount
            # if eligible
            else:
                r_floating_ban += 1 # ban opponent
                q.append('D') # push back to voting queue
        else:
            if r_floating_ban:
                r_floating_ban -= 1
                r_count -= 1
            else:
                d_floating_ban += 1
                q.append('R')

    # Return the party with eligible Senators
    return 'Radiant' if r_count else 'Dire'
```

**Solution alternative** Use Greedy algorithm or binary search. Time complexity is `O(n^2)` and space complexity is `O(n)`.