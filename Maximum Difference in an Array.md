# Problem:

### You are given an array of integers and must compute the maximum difference between any item and any lower indexed smaller item for all the possible pairs, i.e., for a given array 'a', find the maximum value of a[j] - a[i] for all i, j where 0 ≤ i < j < n and a[i] < a[j]. If no item has a smaller item with a lower index, then return -1.   For example, given an array [1, 2, 6, 4], you would first compare 2 to the elements to its left. 1 is smaller, so calculate the difference 2 - 1 = 1. 6 is bigger than 2 and 1, so calculate the differences 4 and 5. 4 is only bigger than 2 and 1, and the differences are 2 and 3. The largest difference was 6 - 1 = 5.   Function Description Complete the function maxDifference in the editor below. The function must return an integer representing the maximum difference in a.   maxDifference has the following parameter(s):     a[a[0],a[1],...a[n-1]]:  an array of integers   Constraints 1 ≤ n ≤ 2 × 105 −106 ≤ a[i] ≤ 106 ∀ i ∈ [0, n − 1]


```sh
diff = []
   (0..(a.size-2)).each do |i|
     diff[i] = a[i+1] - a[i]
   end
   max = diff[0]
   (1..diff.size-1).each do |j|
     diff[j] += diff[j-1] if diff[j-1] > 0
     max = diff[j] if max < diff[j]
   end
   max
```
