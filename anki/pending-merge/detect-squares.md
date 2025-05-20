Q:: =============================================
The problem statement specifies that squares must have "all sides parallel to the x-axis and y-axis." What does this imply about the orientation of the squares we are looking for?
A) Squares can be of any size.
B) Squares must have vertices with integer coordinates.
C) Squares cannot be rotated; their sides must be perfectly horizontal and vertical.
D) Squares must involve the origin (0,0) as one of their vertices.
A:: =============================================
Answer: C
Explanation: The condition "all sides parallel to the x-axis and y-axis" means the squares are "axis-aligned." This excludes squares that are tilted or rotated relative to the coordinate axes. For example, a square formed by points (0,1), (1,0), (2,1), (1,2) is a valid geometric square, but its sides are not parallel to the axes, so it would not be counted.

Q:: =============================================
Consider the `count(point)` operation. If you have `N` points already stored, and for a given `query_point`, you decide to check every possible combination of three *other* distinct points from the stored `N` points to see if they form a square with the `query_point`, what would be the time complexity of a single `count` call?
A) O(N)
B) O(N^2)
C) O(N^3)
D) O(N * log N)
A:: =============================================
Answer: C
Explanation: To choose 3 points from N stored points, there are roughly N * (N-1) * (N-2) / (3*2*1) combinations, which is O(N^3). For each combination, you'd perform some checks. This approach is generally too slow for typical constraints on N.

Q:: =============================================
If a `query_point = (x1, y1)` and another `stored_point = (x2, y2)` are to form the two endpoints of a diagonal of an *axis-aligned* square, which of the following conditions must be true?
A) `x1 == x2` AND `y1 == y2` (the points are identical).
B) `abs(x1 - x2) == abs(y1 - y2)` AND `x1 != x2` AND `y1 != y2`.
C) `x1 == x2` OR `y1 == y2` (the points lie on the same horizontal or vertical line).
D) The distance between `(x1,y1)` and `(x2,y2)` must be an integer.
A:: =============================================
Answer: B
Explanation: For an axis-aligned square, the width and height must be equal. If `(x1, y1)` and `(x2, y2)` are diagonal, then the absolute difference in their x-coordinates (`abs(x1 - x2)`) is the side length, and the absolute difference in their y-coordinates (`abs(y1 - y2)`) is also the side length. Thus, these must be equal. Also, for a valid square with area, the side length must be non-zero, so `x1 != x2` (which also implies `y1 != y2` since their absolute differences are equal and non-zero).

Q:: =============================================
Given a query point `P1 = (x1, y1)` and another point `P2 = (x2, y2)`. If these two points are assumed to be diagonally opposite vertices of an axis-aligned square, what are the coordinates of the other two vertices, `P3` and `P4`?
A) `P3 = (x1, x2)` and `P4 = (y1, y2)`
B) `P3 = (x1, y2)` and `P4 = (x2, y1)`
C) `P3 = ((x1+x2)/2, y1)` and `P4 = (x1, (y1+y2)/2)`
D) `P3 = (x2, y2)` and `P4 = (x1, y1)` (this just lists the same points)
A:: =============================================
Answer: B
Explanation: For an axis-aligned square, if `(x1, y1)` and `(x2, y2)` are diagonal corners, the other two corners will share x-coordinates with one point and y-coordinates with the other. Thus, the other two points are `(x1, y2)` and `(x2, y1)`.

Q:: =============================================
To efficiently implement the `add(point)` operation, aiming for O(1) average time complexity, and to correctly handle the fact that "Duplicate points are allowed and should be treated as separate points," what information is crucial to maintain for each unique coordinate pair `(x,y)` that is added?
A) Only a flag indicating that this coordinate pair has been seen at least once.
B) A list of all points added so far, in the order they were added.
C) The frequency or count of how many times each unique coordinate pair `(x,y)` has been added.
D) The timestamp of when each unique coordinate pair was last added.
A:: =============================================
Answer: C
Explanation: Since duplicate points contribute to forming different squares (e.g., if point A is added twice, it can be used as two distinct points), we need to know how many times each specific coordinate pair `(x,y)` has been added. Storing its frequency allows us to account for this in the `count` method.

Q:: =============================================
During the `count(query_point)` operation, you'll need to quickly determine if certain other coordinate pairs (potential vertices of a square) have been added previously, and if so, how many times. Which data structure generally provides the fastest average time complexity for looking up the count/frequency of a given point `(x,y)`?
A) A simple list or array of all points added, requiring a linear scan.
B) A balanced binary search tree storing unique points, allowing O(log N) lookup.
C) A hash map (or dictionary) where keys are point coordinates (e.g., a tuple `(x,y)` or a string `x#y`) and values are their frequencies.
D) A 2D array `grid[x][y]` if coordinates are bounded and small, storing frequencies.
A:: =============================================
Answer: C
Explanation: A hash map provides, on average, O(1) time complexity for lookups, insertions, and deletions. This is ideal for quickly checking the existence and frequency of points. While a 2D array (option D) can also offer O(1) lookup if coordinates are small and bounded (like 0-1000 here), a hash map is more general and often preferred for flexibility if coordinate ranges were larger or less predictable. For this problem's specific constraints, D is plausible, but C is a more canonical and flexible approach for point frequency tracking. The question asks for "fastest average time complexity" generally, which points to hash maps.

Q:: =============================================
When trying to count squares for a `query_point = (qx, qy)`, suppose you iterate through all *stored* unique points `(px, py)`. If `(qx, qy)` and `(px, py)` can form a diagonal of a square (meaning `abs(qx-px) == abs(qy-py) > 0`), you then identify the other two potential vertices: `V1 = (qx, py)` and `V2 = (px, qy)`. If `count(P)` gives the number of times point `P` has been added, how do you calculate the number of new squares formed using the specific `(px, py)` chosen, along with `V1` and `V2`?
A) `count((px, py)) + count(V1) + count(V2)`
B) `1` if `count((px, py)) > 0`, `count(V1) > 0`, and `count(V2) > 0`, else `0`.
C) `count((px, py)) * count(V1) * count(V2)`
D) `min(count((px, py)), count(V1), count(V2))`
A:: =============================================
Answer: C
Explanation: The query point is given (implicitly, count 1 for itself in this context). For each *choice* of the diagonally opposite point `(px, py)`, we need one instance of `V1` and one instance of `V2`. The number of ways to pick an instance of `(px, py)` is `count((px, py))`. The number of ways to pick an instance of `V1` is `count(V1)`, and for `V2` is `count(V2)`. Since these choices are independent for forming this specific square configuration, we multiply their counts. If any of these points are not present (i.e., their count is 0), the product will correctly be 0.

Q:: =============================================
The problem constraints state `0 <= x, y <= 1000`. How could this constraint potentially simplify the choice of data structure for storing point frequencies, compared to a scenario with arbitrary or very large coordinate values?
A) It makes sorting points by coordinate values more efficient.
B) It allows the use of a direct-access 2D array (e.g., `int_array[1001][1001]`) to store frequencies, offering O(1) worst-case access.
C) It significantly reduces the number of possible squares, making brute-force faster.
D) It has no significant impact; a hash map remains the only practical choice.
A:: =============================================
Answer: B
Explanation: With coordinates bounded to a relatively small range like 0-1000, one could use a 2D array (e.g., `counts[1001][1001]`) to store the frequency of each point `(x,y)` at `counts[x][y]`. This offers true O(1) time for add and lookup. However, it requires O(MAX_COORD^2) space, which is `1001*1001` (about 1 million integers) in this case. If `MAX_COORD` were much larger, this would be impractical. A hash map is more space-efficient if the number of actual points is much smaller than `MAX_COORD^2`. The constraints make a 2D array a *possible* alternative to a hash map for this specific problem.

Q:: =============================================
In designing the `count(query_point)` method, a common strategy involves iterating through your collection of stored points. To identify potential squares involving the `query_point`, which geometric role is most efficient for a `stored_point` to play relative to the `query_point` to easily determine the other two vertices of an axis-aligned square?
A) The `stored_point` forms a horizontal or vertical side with the `query_point`.
B) The `stored_point` is identical to the `query_point` (if duplicates are allowed).
C) The `stored_point` is diagonally opposite to the `query_point`.
D) The `stored_point` is the one closest to the `query_point`.
A:: =============================================
Answer: C
Explanation: If a `stored_point` is assumed to be diagonally opposite the `query_point` in an axis-aligned square, the coordinates of the other two vertices are immediately determined: `(query_point.x, stored_point.y)` and `(stored_point.x, query_point.y)`. This makes checking for the existence of these other two points straightforward. Other relationships would require more complex logic to find the remaining vertices.
