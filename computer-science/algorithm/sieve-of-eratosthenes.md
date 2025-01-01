# Sieve of Eratosthenes



### Algorithm for finding all `prime numbers` up to any given limit. (**Big O of n log n**)

<img src="https://dryuc24b85zbr.cloudfront.net/tes/resources/12713107/image?width=500&height=500&version=1659266726359" alt="image" style="zoom:100%;" />

```c++
#include <iostream>
#include <vector>
#include <cmath>

using namespace std;

/* 9-1. 소수 찾기 */

vector<int> sieveOfEratosthenes(int n) {
    vector<bool> isPrime(n+1, true);
    isPrime[0] = isPrime[1] = false; //0,1 은 false

    for(int i = 2 ; i < sqrt(n) ; i++) {  // number larger than n^2 would have already been marked by a smaller factor
        if(isPrime[i]) { // initally all true
            for(int j = i*i ; j <= n ; j +=i) { // start frmo i*i bc all smaller multiples would have been marked by smaller primes
                isPrime[j] = false;
            }
        }
    }

    vector<int> primeNumbers;

    for(int i = 2 ; i <= n ; i++) {
        if(isPrime[i]) {
            primeNumbers.push_back(i);
        }
    }

    return primeNumbers;
}

int main() {
    int num;
    cin >> num;

    vector<int> primes = sieveOfEratosthenes(num);

    for (int prime : primes) {
        cout << prime << " ";
    }
    cout << endl;

    return 0;
}
```

