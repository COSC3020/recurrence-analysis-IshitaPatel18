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

The if statement check takes constant steps, along with the var count = 0. The first and the third for loops iterates for $n^2$ because of the i < n* n and k < n*n. The second for loop iterates for n because of the j < n. The for loops are nested so their steps are multiplied to get $n * n^2 * n^2$ which equals $n^5$. Lastly, there are 3 recursive calls, which are dividing n by 3, which gives us 3T(n/3). Now to put it together and solve.

$T(n) = 1 for n <= 1. This is our base/termination case$. <br>
$T(n) = 3T(n/3) + n^5$; <br>
Now to calculate T(n/3) and sub it back in: <br>
$T(n/3) = 3T(n/9) + (n/9)^5$ <br>
$T(n) = 3(3T(n/9) + (n/9)^5) + n^5$ <br>
T(n) = 9T(n/9)

