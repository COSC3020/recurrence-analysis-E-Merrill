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

For $n \leq 1$:  $T(n) = 1$  

For $n > 1$:  $T(n) = 3 * T(\frac{n}{3}) + n^5$  

$T(n) = 3 * T(\frac{n}{3}) + n^5$  
$T(n) = 3 * (3 * T(\frac{n}{9}) + \frac{n^5}{3^5}) + n^5$  
$T(n) = 9 * T(\frac{n}{9}) + n^5 + \frac{n^5}{3^4}$  
$T(n) = 27 * T(\frac{n}{27}) + n^5 + \frac{n^5}{3^4} + \frac{n^5}{3^8}$  
$T(n) = 81 * T(\frac{n}{81}) + n^5 + \frac{n^5}{3^4} + \frac{n^5}{3^8} + \frac{n^5}{3^12}$  
$T(n) = 3^i * T(\frac{n}{3^i}) + \sum_{i=0}^{\infty} \frac{1}{3^{4i}} * n^5$  

Solving the geometric sum:  
$\sum_{i=0}^{\infty} \frac{1}{3^{4i}} * n^5 = \frac{n^5}{1 - \frac{1}{3^4}}$  
$\sum_{i=0}^{\infty} \frac{1}{3^{4i}} * n^5 = \frac{n^5}{\frac{81 - 1}{81}}$  
$\sum_{i=0}^{\infty} \frac{1}{3^{4i}} * n^5 = \frac{81n^5}{80}$  

$T(n) = 3^{log_3(n)} * T(\frac{n}{3^{log_3(n)}}) + \frac{81n^5}{80}$  
$T(n) = n * T(\frac{n}{n}) + \frac{81n^5}{80}$  
$T(n) = n * T(1) + \frac{81n^5}{80}$  
$T(n) = n + \frac{81n^5}{80}$  
The fastest growing term in the above equation has a complexity of n^5  
Thus, the final asymptotic complexity of T(n) is:  
$T(n) \in O(n^5)$    


I received a good amount of help from Gage Hepworth figuring out that I could use a geometric series.

I certify that I have listed all sources used to complete this exercise, including the use of any Large Language Models. All of the work is my own, except where stated otherwise. I am aware that plagiarism carries severe penalties and that if plagiarism is suspected, charges may be filed against me without prior notice.

