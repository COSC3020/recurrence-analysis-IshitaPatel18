[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-24ddc0f5d75046c5622901739e7c5dd533143b0c8e959d652212380cedb1ea36.svg)](https://classroom.github.com/a/OlW38W4k)
# Recurrence Analysis -- Mystery Function

Analyze the running time of the following recursive procedure as a function of
$n$ and find a tight big $O$ bound on the runtime for the function. You may
assume that each operation takes unit time. You do not need to provide a formal
proof, but you should show your work: at a minimum, show the recurrence relation
you derive for the runtime of the code, and then how you solved the recurrence
relation.

```javascript
function mystery(n) {
    if(n <= 1)
        return;
    else {
        mystery(n / 3);
        var count = 0;
        mystery(n / 3);
        for(var i = 0; i < n*n; i++) {
            for(var j = 0; j < n; j++) {
                for(var k = 0; k < n*n; k++) {
                    count = count + 1;
                }
            }
        }
        mystery(n / 3);
    }
}
```

Add your answer to this markdown file. [This
page](https://docs.github.com/en/get-started/writing-on-github/working-with-advanced-formatting/writing-mathematical-expressions)
might help with the notation for mathematical expressions.

My answer:

The if statement check takes constant steps, along with the var count = 0. The first and the third for loops iterate for $n^2$ because of the i < n* n and k < n*n. The second for loop iterates for n because of the j < n. The for loops are nested so their steps are multiplied to get $n * n^2 * n^2$ which equals $n^5$. Lastly, there are 3 recursive calls, which are dividing n by 3, which gives us 3T(n/3). Now to put it together and solve, where the constants are dropped because they aren't important asymptotically.

T(n) = 1 for n <= 1. This is our base/termination case. <br>
T(n) = 3T(n/3) + $n^5$ for n > 1; <br>

Now to calculate T(n/3) and sub it back in: <br>
T(n/3) = 3T(n/9) + $(n/3)^5$ <br>
T(n) = 3(3T(n/9) + $(n/3)^5$) + $n^5$ <br>
T(n) = 9T(n/9) + $3(n/3)^5$ + $n^5$ <br>

Now to calculate T(n/9) and sub it back in (This is just to establish a concrete pattern): <br>
T(n/9) = 3T(n/27) + $(n/9)^5$ <br>
T(n) = 9(3T(n/27) + $(n/9)^5$) + $3(n/3)^5$ + $n^5$ <br>
T(n) = 27T(n/27) + $9(n/9)^5$ + $3(n/3)^5$ + $n^5$ <br>

This can be simplified to: <br>
T(n) = T(n) = 27T(n/27) + $n^5/9^4$ + $n^5/3^4$ + $n^5$ <br>

This continues for each iteration until the base case is reached. <br>
The pattern seems to be: <br>
$T(n) = 3^i(n/3^i) + n^5/3^{4(i-1)} + n^5/3^{4(i-2)} + ... + n^5$ <br>

Since the base case must be achieved, i needs to be $log_3(n)$ to achieve T(1) <br>
So now we have: <br>
$T(n) = 3^{log_3(n)}T(n/3^{log_3(n)}) + n^5/3^{4log_3(n) - 4} + n^5/3^{4log_3(n) - 8} + ... + n^5$ <br>
$T(n) = nT(1) + n^5/(n^4 * 3^{-4}) + n^5/(n^4 * 3^{-8}) + ... + n^5$ <br>
$T(n) = n + 3^4 * n + 3^8 * n + ... + n^5$ <br>

At this point and considering the pattern, the lower order terms of n along with their constants can be dropped because asymptotically, $n^5$ is more important than the other terms as it will impact the runtime to the greatest extent. Therefore, the Big $O$ tight bound is $O(n^5)$.


