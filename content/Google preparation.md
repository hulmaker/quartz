
- sorting
- binary search
- DFS, BFS
- min heap
- dynamic programming
- two pointers
- sliding window
- greedy algorithms
- prefix sum
- recursion
- trees - binary tree, avl tree
	- segment tree - for min/max/sum over segments
	- interval tree - for interval intersection at point
	- disjoint set union
	- tries
	- spanning tree
	
```python
def dijkstra(E, V, start, end):
	dist = {v: float('inf') for v in V} # distance from start
	pred = {v: None for v in V} # parent
	seen = {v: False for v in V}
	dist[start] = 0
	Q = [(0, start)] # priority queue: dist, vertex
	
	while Q:
		u = heappop(Q)  # closest node to start
		if seen[u]: continue
		if u == end: break
		for v in neighbor(u):
			alt = dist[u] + edge_size(u, v)
			if alt < dist[v]:
				dist[v] = alt
				pred[v] = u
				heappush(Q, (alt, v)) # with decrease_priority, no need for seen
		seen[u] = True
	return dist, prev


def bisect(arr, target):  
	l, r = 0, len(arr)-1
  
	while l <= r:  
		mid = (l + r) // 2  
		if arr[mid] == target:  
			return mid  
	    if arr[mid] < target:  
		    l = mid + 1  
	    else:  
			r = mid - 1  
	return r


 def edit_distance(word1: str, word2: str):
	m, n = len(word1), len(word2)
	dp = [[0] * (n + 1) for _ in range(m + 1)]

	for i in range(m + 1): # from "" it's just inserts
		dp[i][0] = i
	for j in range(n + 1):
		dp[0][j] = j

	for i in range(1, m + 1):
		for j in range(1, n + 1):
			if word1[i - 1] == word2[j - 1]:
				dp[i][j] = dp[i - 1][j - 1]
			else:
				dp[i][j] = 1 + min(
					dp[i - 1][j - 1],  # replace
					dp[i - 1][j],      # delete
					dp[i][j - 1],      # insert
				)

	return dp[m][n]
```


| **USPOŘÁDANÝ VÝBĚR**    |                                                           |
| ----------------------- | --------------------------------------------------------- |
| Variace bez opakovani   | <br>$V(n, k)=\frac{n!}{(n-k)!}$                           |
| Variace s opakovanim    | $V^*(n, k)=n^k$                                           |
| permutace bez opakovani | $P(n)=V(n, n)=n!$                                         |
| permutace s opakovanim  | $P^*(n, k) =\frac{n!}{n_{1}!\cdot n_{2}!\ldots . n_{k}!}$ |

| **NEUSPOŘÁDANÝ VÝBĚR**  |                                        |
| ----------------------- | -------------------------------------- |
| Kombinace bez opakování | $C(n, k) =\frac{n!}{(n-k)!k!}$         |
| Kombinace s opakováním  | $C^*(n, k) =\frac{(n+k-1)!}{(n-1)!k!}$ |

**Eulerova věta**:
$a^{\varphi(n)} \equiv 1 \quad(\bmod n)$, pro $\gcd(a, n) = 1$ kde $\varphi(n) :=$ počet nesoudělných čísel $\leq n$



## Questions
- Worst/best thing about working at google
- Compared to your previous working experiences, what stands out about google?
- How do you feel about people culture? Is it easy for you to get along?
- Are there any out-of-work activities?



# Coding questions
## Q1
- sachovnice jako string
- nemuzou se krizit
- validation process
- trim both sides
- pocitadlo - nahlanim a hazim je na hromadu

## Q2
- mam fer minci, chci s ni vygenerovat randint(a, b)
- given categorical distribution [(a, 0.1), (b, 0.5), (c, 0.4)] - get a,b,c with probability proportional to their weight (the weight don't have to be between 0-1)
## Q3
Given a list/array of Strings, find and group together all Strings that are "buddies" with one another. 
You may use any data structure of your choosing to return the grouping of buddies. 
Two Strings are "buddies" if they are the same length, and the characters are equal distance from each other. 
For example, "aaa" and "zzz" are buddies, but "aaa" would not be buddies with "abc".

abc | def --> buddies
aaa | zzz --> buddies
abc | deg -> not buddies
ab | ba -> buddies (cyclic set)
abc | yza -> buddies (cyclic set)