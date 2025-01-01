# Short-Circuit Evaluation

**Short-circuiting is a programming concept in which the compiler skips the execution of sub-expressions in a logical expression.**

The compiler does not evaluate the contents of an expression until it is necessary.

<br/>

For Example,

```c++
int main() {
    int x = 1; //true
    
    if(x || ++x) {
        cout << x;
    }
    return 0;
}
```

```tex
1
```

The value of the first sub-expression,  x = true, is true.
So the value of the second sub-expression does not affect the value of the expression and hence the **compiler skips checking** it. 
Therefore the value of x **is not incremented.**

<br/>

참고

https://www.geeksforgeeks.org/short-circuit-evaluation-in-programming/
