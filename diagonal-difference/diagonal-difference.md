# Diagonal Difference

Given a square matrix, calculate the absolute difference between the sums of its diagonals.

For example, the square matrix `arr` is shown below:

```
1 2 3
4 5 6
9 8 9
```

The left-to-right diagonal = `1 + 5 + 9 = 15`. The right to left diagonal = `3 + 5 + 9 = 17`. Their absolute difference is `|15 - 17| = 2`.

### My Approach

I started by defining the initial values that I wanted to make an absolute value from. The leftDiagonal, and the rightDiagonal. I then tried looping them and got close to the solution.

```js
function diagonalDifference(arr) {
  let leftDiagonal = 0;
  let rightDiagonal = 0;

  for (let i = 0; i < arr.length; i++) {
    leftDiagonal += arr[i][i];
    rightDiagonal += arr[i][i + i + 2];
  }
  return Math.abs(leftDiagonal - rightDiagonal);
}
```

This result didnt work. I tried isolating the solution and found out that the right diagonal was getting an `NaN` return value. I knew something was wrong but at this point I didn't know why this wouldn't work. Reason being is that I thought both instances of `i` would've incremented normally. However this wasn't happening, so I asked ChatGPT what the issue could've been:

> In a 3x3 matrix, the indices of the elements on the right diagonal are (0,2), (1,1), and (2,0). As you can see, the sum of the row and column indices for each element on the right diagonal is always 2 (in a 0-indexed system). The way you're calculating the column index for the right diagonal (i + i + 2) doesn't reflect this pattern.

I was thinking the entire array was an `array.length` of 9, instead of three separate arrays. When I realized this I tried the following solution:

```js
function diagonalDifference(arr) {
  let leftDiagonal = 0;
  let rightDiagonal = 0;

  for (let i = 0; i < arr.length; i++) {
    leftDiagonal += arr[i][i];
    rightDiagonal += arr[i][array.length - i - 1];
  }
  return Math.abs(leftDiagonal - rightDiagonal);
}
```

This way, whenever `rightDiagonal` incremented, I was always going to get `[0][3 - 0 - 1 = 2]`, `[1][3 - 1 - 1 = 1]`, and `[2][3 - 2 - 1 = 0]`, which, lo and behold, adhered to the correct pattern that GPT desribed. This is because the array really looks like `[[1, 2, 3][4, 5, 6][7, 8, 9]] instead of [1, 2, 3, 4, 5, 6, 7, 8, 9]. After I realized this structure. It made it really easy to recognize this type of problem. This best thing with this solution is that it matches any size matrix, whether it be a 3x3 square or a 9x9. So, this doesn't brute force the problem. 

### What did I learn?

- Analyze the structure of the problem. Even in the problem it said that `arr` is a return value of `arr[i][j]`. Now in the future whenever I see problems that involve array matrices, I can figure that the structure of the arrays will problem be of a similar array value as previously mentioned. By not recognizing this structure, I was getting `NaN` when trying to solve the problem and getting frustrated. Now, this is just another pattern and problem solving technique in my arsenal. This is also the first time I used double-incremented array values, so I will take the experience of figuring out this solution and implementing it into future problems where `i` is being incremented across multiple arrays.