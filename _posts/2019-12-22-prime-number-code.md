---
layout: post
title: "Finding Prime Numbers in Java, Python, and Ruby"
categories: [Java, Python, Ruby, Performance]
---

I'm planning a series of blog posts about performance in Java, Python, and Ruby (where by "performance" I mean how fast programs in each language run), and how tweaks to code affect speed.

Each of those posts focus on code for finding prime numbers. Instead of duplicating that code in each upcoming post, I'll post it once here and refer to it from the other posts.

A few notes on this code:

+ In case your math is rusty: prime numbers are numbers that are only cleanly divisible by themselves and 1. For example, 5 is a prime number because the only numbers you can multiply together to get 5 are 1 x 5. In contrast, 30 is not prime because 2 x 15, 3 x 10, and 5 x 6 all give you 30.
+ The Java, Python, and Ruby programs in this post all use the same algorithm for finding prime numbers. This isn't the most efficient algorithm, but it's short, easy to understand, and easy to implement in code.
+ Just like prose, code can be written with different levels of care, in different styles. These 3 programs are written in a style that most experienced programmers would consider reasonably clean and idiomatic. Real-world programs--even high-profile products created and sold by large, respected companies--are often messier less stylistically pure, even if they work correctly.
+ All 3 programs give the same output. If we ask them to find 1000 prime numbers, the output will look like this (but with different elapsed time):

  ```console
  finding 1000 primes
  last prime: 7919
  elapsed: 0.024 seconds
  ```


## Java

If you're not familiar with Java, this code probably won't make a ton of sense. That's OK: Java isn't the most user-friendly language around for beginners.

```java
import java.util.ArrayList;
import java.util.List;

public class Primes {

    public static void main(String[] args) {
        final long primeCount = Long.parseLong(args[0]);
        Primes myPrimes = new Primes();
        myPrimes.findPrimes(primeCount);
    }

    private void findPrimes(final long primeCount) {
        final long startMillis = System.currentTimeMillis();
        
        System.out.println("finding " + primeCount + " primes");
        List<Long> primes = new ArrayList<>();
        primes.add(2L);
        long candidate = 3L;
        while (primes.size() < primeCount) {
            if (isPrime(candidate)) primes.add(candidate);
            candidate += 2L;
        }

        final long elapsedMillis = 
            System.currentTimeMillis() - startMillis;
        System.out.println("last prime: " + 
            primes.get(primes.size() - 1));
        System.out.println("elapsed: " + 
            elapsedMillis / 1000.0 + " seconds");
    }

    private boolean isPrime(final long num) {
        final long max_factor = (long) (Math.floor(Math.sqrt(num)));
        for (long factor = 2L; factor <= max_factor; factor++) {
            if (num % factor == 0) return false;
        }
        return true;
    }
}
```

To find the first 1000 prime numbers:

1. Paste the code into a file called `Primes.java`
1. In a terminal, navigate to the directory the file is in
1. Run these two commands:
 
    ```bash
    $ javac Primes.java
    $ java Primes 1000
    ```


## Python

This code is shorter than the Java equivalent, and might make more sense to a beginner. Or it might not.

```python
import datetime
import math
import sys

prime_count = int(sys.argv[1])
primes = [2]


def is_prime(num: int) -> bool:
    max_factor = math.floor(math.sqrt(num))
    for factor in range(2, max_factor + 1):
        if num % factor == 0:
            return False
    return True


start_time = datetime.datetime.now()
print(f'finding {prime_count} primes')
candidate = 3
while len(primes) < prime_count:
    if is_prime(candidate):
        primes.append(candidate)
    candidate += 2
elapsed = datetime.datetime.now() - start_time

print(f'last prime: {primes[-1]}')
print(f'elapsed: {elapsed}')
```

To find the first 1000 prime numbers:

1. Paste the code into a file called `Primes.py`
1. In a terminal, navigate to the directory the file is in
1. Run one of these two commands. Which command to use depends on how your computer is set up; try each and see what works.
 
    ```bash
    $ python Primes.py 1000
    $ python3 Primes.py 1000
    ```


## Ruby

Ruby takes about the same number of lines of code as Python. Some people find Ruby to be the closest language to how their thoughts naturally flow. Other people think it's... weird.

```ruby
prime_count = ARGV[0].to_i
primes = [2]

def prime?(num)
  max_factor = Math.sqrt(num).floor
  (2..max_factor).each do |factor|
    return false if (num % factor).zero?
  end
  true
end

start_time = Time.now
puts "finding #{prime_count} primes"
candidate = 3
while primes.size < prime_count do
  primes << candidate if prime?(candidate)
  candidate += 2
end
elapsed = Time.now - start_time

puts "last prime found: #{primes[-1]}"
puts "elapsed: #{elapsed}"
```

To find the first 1000 prime numbers:

1. Paste the code into a file called `Primes.rb`
1. In a terminal, navigate to the directory the file is in
1. Run this command:
 
    ```bash
    $ ruby Primes.rb 1000
    ```


## Further discussion

Please see the rest of this blog for performance-related posts involving this code.
