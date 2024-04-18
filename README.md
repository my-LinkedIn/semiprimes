# SEMIPRIMES

Testing the Waters with Semiprime Numbers... thanks to this [LinkedIn Post](https://www.linkedin.com/feed/update/urn:li:activity:7186515424790888448?utm_source=share&utm_medium=member_desktop).

## D Source code

```d
import std.stdio: writeln, writefln;
import std.range;
import std.algorithm;

/// Used the OEIS convention
/// Refer to https://oeis.org/A001358
/// Semiprimes (or biprimes): products of two primes.

bool isA001358(ulong n) pure nothrow @safe {
    if (n < 4)
        return false;

    ulong factorCount = 0;
    
    for (ulong i = 2; i * i <= n && factorCount < 3; ++i) {
        while (n % i == 0) {
            ++factorCount;
            n /= i;
        }
    }
    
    if (n > 1)
        ++factorCount;
    
    return factorCount == 2;
}

void main() {    
    const N = 100uL;
    auto immutable semiprimes = iota(N+1).filter!isA001358.array;
    
    writeln;
    semiprimes.writeln;
    
    writefln("\nSum of the 1st %s semiprime = %d", N, semiprimes.sum);
    
}

```

## Output

```text
[4, 6, 9, 10, 14, 15, 21, 22, 25, 26, 33, 34, 35, 38, 39, 46, 49, 51, 55, 57, 58, 62, 65, 69, 74, 77, 82, 85, 86, 87, 91, 93, 94, 95]

Sum of the 1st 100 semiprime = 1707
```

## References

[A001358 Sequence](https://oeis.org/A001358)
