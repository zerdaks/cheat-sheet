# README

- [README](#readme)
  - [Algorithmic Thinking](#algorithmic-thinking)
    - [Big O Notation](#big-o-notation)
    - [Logarithms](#logarithms)
    - [NP-completeness](#np-completeness)
    - [Reductions](#reductions)
  - [Bit Manipulation](#bit-manipulation)
    - [Binary Numbers](#binary-numbers)
      - [Binary Numbers and Base-2](#binary-numbers-and-base-2)
      - [Binary to Hexadecimal](#binary-to-hexadecimal)
      - [Binary to Octal](#binary-to-octal)
      - [Negative Numbers and Two's Complement](#negative-numbers-and-twos-complement)
    - [Bitwise AND](#bitwise-and)
    - [Bitwise OR](#bitwise-or)
    - [Bitwise XOR (exclusive OR)](#bitwise-xor-exclusive-or)
    - [Bitwise NOT](#bitwise-not)
    - [Bit Shifting](#bit-shifting)
      - [Left Shifts](#left-shifts)
      - [Logical Right Shifts](#logical-right-shifts)
      - [Arithmetic Right Shifts](#arithmetic-right-shifts)
  - [Java](#java)
    - [Java Primitive Data Types](#java-primitive-data-types)
    - [Java Arrays](#java-arrays)
    - [Java Class Library (JCL) Performance](#java-class-library-jcl-performance)
    - [Java Variance](#java-variance)
    - [Java Virtual Machine Stacks](#java-virtual-machine-stacks)
    - [Heap](#heap)
    - [Generational Garbage Collection](#generational-garbage-collection)
  - [Networking](#networking)
    - [Open Systems Interconnection (OSI) Reference Model](#open-systems-interconnection-osi-reference-model)
  - [Numbers](#numbers)
    - [Data Units](#data-units)
    - [Latencies](#latencies)
    - [Powers of Two](#powers-of-two)
  - [Memory Hierarchy](#memory-hierarchy)
  - [ACID](#acid)
  - [REST](#rest)

## Algorithmic Thinking

### Big O Notation

notation | name | complexity class | algorithm
:---: | :---: | :---: | :---:
O(1) | constant || in-place
O(log n) | logarithmic
O(n) | linear || one-pass, n-pass
O(n log n) | log-linear
O(n<sup>2</sup>) | quadratic
O(n<sup>c</sup>) | polynomial | **P**
O(c<sup>n</sup>) | exponential (with linear exponent) | **E**
O(c<sup>poly(n)</sup>) | exponential | **EXPSPACE**/**EXPTIME**
O(n!) | factorial

- all pairs: n<sup>2</sup>
- all triples: n<sup>3</sup>
- all subsets of set n: 2<sup>n</sup>
- all k combinations of set n (n choose k): <img src="https://render.githubusercontent.com/render/math?math={n \choose k} = n!/(k!(n-k)!)">
- all permutations: n!

See also:
- [Big-O Cheat Sheet](http://bigocheatsheet.com/)
- [Orders of common functions](https://en.wikipedia.org/wiki/Big_O_notation#Orders_of_common_functions)
- [Table of common time complexities](https://en.wikipedia.org/wiki/Time_complexity#Table_of_common_time_complexities)

### Logarithms

The logarithm for a base *b* and a number *x* is defined to be the inverse function of taking *b* to the power *x*. For any *x* and *b*:

<img src="https://render.githubusercontent.com/render/math?math=log_b(x) = y \iff b^y = x">

For example:

<img src="https://render.githubusercontent.com/render/math?math=log_2(64) = 6 \iff 2^6 = 64">

### NP-completeness

- The class **P** consists of problems that are solvable in polynomial time.
- The class **NP** consists of problems that are *verifiable* in polynomial time.
- Any problem in **P** is also in **NP**. And any problem in **NP** is also in **EXPTIME**. More formally:
  - <img src="https://render.githubusercontent.com/render/math?math=P \subseteq NP \subseteq PSPACE \subseteq EXPTIME \subseteq NEXPTIME \subseteq EXPSPACE">
  - <img src="https://render.githubusercontent.com/render/math?math=P \subsetneq EXPTIME">
  - <img src="https://render.githubusercontent.com/render/math?math=NP \subsetneq NEXPTIME">
- A problem is in class **NPC** (and is referred to as being **NP-complete**) if it is in **NP** and is as *hard* as any problem in **NP**.
- If any **NP-complete** problem can be solved in polynomial time, then every problem in **NP** can be solved in polynomial time.

See also:
- [EXPTIME](https://en.wikipedia.org/wiki/EXPTIME)

![](https://upload.wikimedia.org/wikipedia/commons/a/a0/P_np_np-complete_np-hard.svg)

### Reductions

- Given an instance &alpha; of problem *A*, use a polynomial-time **reduction algorithm** to transform it to an instance &beta; of problem *B*.
- Run the polynomial-time decision algorithm for *B* on the instance &beta;.
- Use the answer for &alpha; as the answer for &beta;.

## Bit Manipulation

### Binary Numbers

#### Binary Numbers and Base-2

decimal (base-10) | binary (base-2) | powers | octal (base-8) | hexadecimal (base-16)
:---: | :---: | :---: | :---: | :---:
0 | 0000 0000 || 0 | 00
1 | 0000 0001 | 2<sup>0</sup> | 1 | 01
2 | 0000 0010 | 2<sup>1</sup> | 2 | 02
3 | 0000 0011 | 2<sup>1</sup> + 2<sup>0</sup> | 3 | 03
4 | 0000 0100 | 2<sup>2</sup> | 4 | 04
5 | 0000 0101 | 2<sup>2</sup> + 2<sup>0</sup> | 5 | 05
6 | 0000 0110 | 2<sup>2</sup> + 2<sup>1</sup> | 6 | 06
7 | 0000 0111 | 2<sup>2</sup> + 2<sup>1</sup> + 2<sup>0</sup> | 7 | 07
8 | 0000 1000 | 2<sup>3</sup> | 8 | 08
9 | 0000 1001 | 2<sup>3</sup> + 2<sup>0</sup> | 10 | 09
10 | 0000 1010 | 2<sup>3</sup> + 2<sup>1</sup> | 11 | 0A
11 | 0000 1011 | | 12 | 0B
12 | 0000 1100 | | 13 | 0C
13 | 0000 1101 | | 14 | 0D
14 | 0000 1110 | | 15 | 0E
15 | 0000 1111 | | 16 | 0F
16 | 0001 0000 | | 20 | 10
17 | 0001 0001 | | 21 | 11
18 | 0001 0010 | | 22 | 12
19 | 0001 0011 | | 23 | 13
20 | 0001 0100 | | 24 | 14

#### Binary to Hexadecimal

Convert hexadecimal to binary by replacing each hexadecimal digit with its equivalent four-bit group in binary:

- <img src="https://render.githubusercontent.com/render/math?math=58_{10} = 3A_{16} = (0011\ 1010)_{2}">
- <img src="https://render.githubusercontent.com/render/math?math=231_{10} = E7_{16} = (1110\ 0111)_{2}">

Convert binary to hexadecimal by dividing the binary number into four-bit groups (starting at the radix point) and replacing each group with its equivalent hexadecimal digit:

- <img src="https://render.githubusercontent.com/render/math?math=82_{10} = (0101\ 0010)_{2} = 52_{16}">
- <img src="https://render.githubusercontent.com/render/math?math=221_{10} = (1101\ 1101)_{2} = DD_{16}">

#### Binary to Octal

Convert octal to binary by replacing each octal digit with its equivalent three-bit group in binary:

- <img src="https://render.githubusercontent.com/render/math?math=58_{10} = 72_{8} = (111\ 010)_{2}">
- <img src="https://render.githubusercontent.com/render/math?math=231_{10} = 347_{8} = (011\ 100\ 111)_{2}">

Convert binary to octal by dividing the binary number into three-bit groups (starting at the radix point) and replacing each group with its equivalent octal digit:

- <img src="https://render.githubusercontent.com/render/math?math=82_{10} = (001\ 010\ 010)_{2} = 122_{8}">
- <img src="https://render.githubusercontent.com/render/math?math=221_{10} = (011\ 011\ 101)_{2} = 335_{8}">

#### Negative Numbers and Two's Complement

decimal | binary | interpretation
:---: | :---: | :---:
−5 | 1011 | -8 + 2 + 1
−4 | 1100 | -8 + 4
−3 | 1101 | -8 + 4 + 1
−2 | 1110 | -8 + 4 + 2
−1 | 1111 | -8 + 4 + 2 + 1
0 | 0000 | 0
1 | 0001 | 1
2 | 0010 | 2
3 | 0011 | 2 + 1
4 | 0100 | 4
5 | 0101 | 4 + 1

### Bitwise AND

The ```AND``` operation takes two bits and returns ```1``` if *both* bits are ```1```. Otherwise, it returns ```0```.

```java
(1 & 1) == 1
(1 & 0) == 0
(0 & 1) == 0
(0 & 0) == 0
```

When performing ```AND``` on two integers, the ```AND``` operation is calculated on each pair of bits (the two bits at the same index in each number).

```java
(5 & 6) == 4

// at bit level:
//   0101 (5)
// & 0110 (6)
// = 0100 (4)
```

### Bitwise OR

The ```OR``` operation takes two bits and returns ```1``` if *either* of the bits are 1. Otherwise, it returns ```0```.

```java
(1 | 1) == 1
(1 | 0) == 1
(0 | 1) == 1
(0 | 0) == 0
```

When performing ```OR``` on two integers, the ```OR``` operation is calculated on each pair of bits (the two bits at the same index in each number).

```java
(5 | 6) == 7

// at bit level:
//   0101 (5)
// | 0110 (6)
// = 0111 (7)
```

### Bitwise XOR (exclusive OR)

The ```XOR``` operation (or ```exclusive or```) takes two bits and returns ```1``` if *exactly one* of the bits is ```1```. Otherwise, it returns ```0```.

```java
(1 ^ 1) == 0
(1 ^ 0) == 1
(0 ^ 1) == 1
(0 ^ 0) == 0
```

When performing ```XOR``` on two integers, the ```XOR``` operation is calculated on each pair of bits (the two bits at the same index in each number).

```java
(5 ^ 6) == 3

// at bit level:
//   0101 (5)
// | 0110 (6)
// = 0011 (3)
```

### Bitwise NOT

The ```NOT``` bitwise operation takes one set of bits, and for each bit returns ```0``` if the bit is ```1```, and ```1``` if the bit is ```0```.

When performing ```NOT``` on an integer, each bit of the integer is inverted.

```java
~ 5 == -6

// at bit level:
// ~ 0101 (5)
// = 1010 (-6 in two's complement as interpreted by the compiler)
```

### Bit Shifting

#### Left Shifts

When shifting left, the most-significant bit is lost, and a ```0``` bit is inserted on the other end.

```java
0010 << 1 -> 0100
0010 << 2 -> 1000
```

A single left shift multiplies a binary number by ```2```.

```java
2 << 1 == 4

// at bit level:
// 0010 << 1 = 0100
```

#### Logical Right Shifts

When shifting right with a **logical right shift**, the least-significant bit is lost and a ```0``` is inserted on the other end.

```java
1011 >>> 1 -> 0101
1011 >>> 3 -> 0001
```

For positive numbers, a single logical right shift divides a number by ```2```, throwing out any remainders.

```java
5 >>> 1 == 2

// at bit level:
// 0101 >>> 1 = 0010
```

#### Arithmetic Right Shifts

When shifting right with an **arithmetic right shift**, the least-significant bit is lost and the most-significant bit is *copied*.

```java
1011 >> 1 -> 1101
1011 >> 3 -> 1111

0011 >> 1 -> 0001
0011 >> 2 -> 0000
```

The first two numbers had a ```1``` as the most significant bit, so more ```1```'s were inserted during the shift. The last two numbers had a ```0``` as the most significant bit, so the shift inserted more ```0```'s.

If a number is encoded using [two's complement](#negative-numbers-and-twos-complement), then an arithmetic right shift preserves the number's sign, while a logical right shift makes the number positive.

```java
-5 >> 1 == -3

// at bit level:
// 1011 >> 1 = 1101

-1 >>> 1 == 7

// at bit level:
// 1111 >>> 1 = 0111
```

## Java

### Java Primitive Data Types

- **byte**: 8-bit signed two's complement integer
- **short**: 16-bit signed two's complement integer
- **int**: 32-bit signed two's complement integer
- **long**: 64-bit unsigned (Java SE 8 and later) two's complement integer
- **float**: a single-precision 32-bit IEEE 754 floating point
- **double**: a double-precision 64-bit IEEE 754 floating point
- **boolean**: has only two possible values: true and false
- **char**: a single 16-bit Unicode character

category | Java type | native type | size | range | exponent
:---: | :---: | :---: | :---: | :---: | :---:
integral | byte | jbyte | 8-bit signed | -128 to 127 | -2<sup>7</sup> to 2<sup>7</sup> - 1
integral | short | jshort | 16-bit signed | -32,768 to 32,767 | -2<sup>15</sup> to 2<sup>15</sup> - 1
integral | int | jint | 32-bit signed | -2,147,483,648 to 2,147,483,647 | -2<sup>31</sup> to 2<sup>31</sup> - 1
integral | long | jlong | 64-bit signed | -9,223,372,036,854,775,808 to 9,223,372,036,854,775,807 | -2<sup>63</sup> to 2<sup>63</sup> - 1
integral | char | jchar | 16-bit | ```'\u0000'``` to ```'\uffff'```
floating-point | float | jfloat | 32-bit | 32-bit IEEE 754 floating-point numbers
floating-point | double | jdouble | 64-bit | 64-bit IEEE 754 floating-point numbers
other | boolean | jboolean | N/A  | ```true``` and ```false```

See also:
- [Common integral data types](https://en.wikipedia.org/wiki/Integer_(computer_science)#Common_integral_data_types)
- [Some selected powers of two](https://en.wikipedia.org/wiki/Power_of_two#Some_selected_powers_of_two)
- [Orders of magnitude (data)](https://en.wikipedia.org/wiki/Orders_of_magnitude_(data))

See also:
- [Big-O Cheat Sheet](http://bigocheatsheet.com/)

### Java Arrays

Java supports arrays of arrays (with order that can be considered **row-major**) rather than multidimensional arrays.

Arrays must be indexed by ```int```, ```short```, ```byte```, or ```char``` values. The size of an array cannot exceed 2<sup>31</sup> - 1 elements.

### Java Class Library (JCL) Performance

```java.lang```
- ```StringBuilder#append(char)```: amortized constant time
- ```StringBuilder#append(String)```:
  - best case: amortized constant time
  - worst case: amortized linear time
- ```System#arraycopy```: platform-dependent

See also:
- [The Android Open Source Project](https://android.googlesource.com/platform/dalvik.git/+/android-4.2.2_r1/vm/native/java_lang_System.cpp)

> The VM makes guarantees about the atomicity of accesses to primitive variables. These guarantees also apply to elements of arrays. In particular, 8-bit, 16-bit, and 32-bit accesses must be atomic and must not cause "word tearing". Accesses to 64-bit array elements must either be atomic or treated as two 32-bit operations. References are always read and written atomically, regardless of the number of bits used to represent them.
>
> We can't rely on standard ```libc``` functions like ```memcpy()``` and ```memmove()``` in our implementation of ```System.arraycopy()```, because they may copy byte-by-byte (either for the full run or for "unaligned" parts at the start or end). We need to use functions that guarantee 16-bit or 32-bit atomicity as appropriate.

- [OpenJDK implementation of System.arraycopy](https://stackoverflow.com/a/11210623/9349175)
- [jdk8u_hotspot/objArrayKlass.cpp](https://github.com/JetBrains/jdk8u_hotspot/blob/master/src/share/vm/oops/objArrayKlass.cpp)

```cpp
template <class T> void ObjArrayKlass::do_copy(arrayOop s, T* src, arrayOop d, T* dst, int length, TRAPS) {
  ...
```

- [jdk8u_hotspot/copy.hpp](https://github.com/JetBrains/jdk8u_hotspot/blob/master/src/share/vm/utilities/copy.hpp)

```cpp
static void conjoint_oops_atomic(narrowOop* from, narrowOop* to, size_t count) {
  ...
```

- [jdk8u_hotspot/copy_windows_x86.inline.hpp](https://github.com/JetBrains/jdk8u_hotspot/blob/master/src/os_cpu/windows_x86/vm/copy_windows_x86.inline.hpp)

```cpp
static void pd_conjoint_jints_atomic(jint* from, jint* to, size_t count) {
  ...
```

```java.util.List```
- ```ArrayList```
  - constant time for methods ```get``` and ```set```
  - amortized constant time for method ```add```
- ```LinkedList```
  - constant time for methods ```add/offer```, ```remove/poll``` and ```peek```
  - linear time for methods ```contains(Object)``` and ```remove(Object)```
- ```PriorityQueue```
  - log(n) time for methods ```add/offer``` and ```remove/poll```
  - linear time for methods ```contains(Object)``` and ```remove(Object)```
  - constant time for method ```peek```

```java.util.Map```
- ```HashMap/LinkedHashMap```
  - constant time for methods ```containsKey``` and ```get```
  - amortized constant time for methods ```put``` and ```remove```
- ```TreeMap```
  - guaranteed log(n) time for methods ```put```, ```get```, ```containsKey``` and ```remove```

```java.util.Set```
- ```HashSet/LinkedHashSet```
  - constant time for methods ```add```, ```contains``` and ```remove```
- ```TreeSet```
  - guaranteed log(n) time for methods ```add```, ```contains``` and ```remove```

### Java Variance

Given a generic class ```C<X>```:
- ```C<X>``` is said to be **covariant** with respect to ```X``` if ```S <: T``` implies ```C<S> <: C<T>``` (where ```<:``` denotes the subtyping relation)
- ```C<X>``` is said to be **contravariant** with respect to ```X``` if ```S <: T``` implies ```C<T> <: C<S>```
- ```C<X>``` is said to be **invariant** when ```C<S> <: C<T>``` is derived only if ```S = T```

A generic collection whose element type is abstracted as a type parameter is typically:
- read-only when **covariant**
    - reading is allowed because the upper bound restricts the element type to a specific type or a subtype of that type
    - writing is not allowed because the element type accepted by the collection is unknown
- write-only when **contravariant**
    - writing is allowed because the lower bound restricts the element type to a specific type or a supertype of that type
    - reading is not allowed because the element type returned by the collection is unknown

See also:
- [On Variance-Based Subtyping for Parametric Types](http://www.fos.kuis.kyoto-u.ac.jp/~igarashi/papers/variance.html)
- Using the OpenJDK to Investigate Covariance in Java
- [Variance in Java and Scala](https://medium.com/@sinisalouc/variance-in-java-and-scala-63af925d21dc)

### Java Virtual Machine Stacks

Each Java Virtual Machine thread has a private *Java Virtual Machine stack*, created at the same time as the thread. A Java Virtual Machine stack stores frames. A Java Virtual Machine stack is analogous to the stack of a conventional language such as C: it holds local variables and partial results, and plays a part in method invocation and return.

### Heap

The Java Virtual Machine has a *heap* that is shared among all Java Virtual Machine threads. The heap is the run-time data area from which memory for all class instances and arrays is allocated.

The heap is created on virtual machine start-up. Heap storage for objects is reclaimed by an automatic storage management system (known as a *garbage collector*); objects are never explicitly deallocated.

### Generational Garbage Collection

An object is considered garbage and its memory can be reused by the VM when it can no longer be reached from any reference of any other live object in the running program.

While naive garbage collection examines every live object in the heap every time, *generational collection* exploits several empirically observed properties of most applications to minimize the work required to reclaim unused (garbage) objects. The most important of these observed properties is the weak generational hypothesis, which states that most objects survive for only a short period of time.

To optimize for this scenario, memory is managed in *generations* (memory pools holding objects of different ages). Garbage collection occurs in each generation when the generation fills up.

The vast majority of objects are allocated in a pool dedicated to young objects (the *young generation*), and most objects die there. When the young generation fills up, it causes a *minor collection* in which only the young generation is collected; garbage in other generations isn't reclaimed. The costs of such collections are, to the first order, proportional to the number of live objects being collected; a young generation full of dead objects is collected very quickly. Typically, some fraction of the surviving objects from the young generation are moved to the *old generation* during each minor collection. Eventually, the old generation fills up and must be collected, resulting in a *major collection*, in which the entire heap is collected. Major collections usually last much longer than minor collections because a significantly larger number of objects are involved.

See also:
- [Go GC: Prioritizing low latency and simplicity](https://blog.golang.org/go15gc)
- [Idle-Time Garbage-Collection Scheduling](https://cacm.acm.org/magazines/2016/10/207771-idle-time-garbage-collection-scheduling/fulltext)

## Networking

### Open Systems Interconnection (OSI) Reference Model

layer \# | layer name | data unit | protocol examples | Internet layer
:---: | :---: | :---: | :---: | :---:
7 | application | data | FTP, HTTP | application
6 | presentation | data | ASCII, MPEG | application
5 | session | data | named pipes, sockets | application
4 | transport | TCP segment, datagram | TCP, UDP| transport
3 | network | packet | IP (IPv4, IPv6) | Internet
2 | data link | frame | IEEE 802.3 (Ethernet) | link
1 | physical | one or more bits

- A **network (layer 4) load balancer** functions at the fourth layer of the OSI reference model.
- An **application (layer 7) load balancer** functions at the seventh layer of the OSI reference model.

See also:
- [RFC 1122 - Requirements for Internet Hosts - Communication Layers](https://tools.ietf.org/html/rfc1122#section-2.2)
- [Using AWS Application Load Balancer and Network Load Balancer with EC2 Container Service](https://medium.com/containers-on-aws/using-aws-application-load-balancer-and-network-load-balancer-with-ec2-container-service-d0cb0b1d5ae5)

## Numbers

### Data Units

name | symbol | size | bit rate
:---: | :---: | :---: | :---:
bit | ```b``` | 0 or 1 | ```bit/s```
byte | ```B``` | 8 bits | ```B/s```
kilobyte | ```KB``` | 1024 bytes | ```kb/s```
megabyte | ```MB``` | 1024 kilobytes | ```Mb/s```
gigabyte | ```GB``` | 1024 megabytes | ```Gb/s```
terabyte | ```TB``` | 1024 gigabytes | ```Tb/s```
petabyte | ```PB``` | 1024 terabytes
exabyte | ```EB``` | 1024 terabytes

See also:
- [Data Measurement Chart](http://www.wu.ece.ufl.edu/links/dataRate/DataMeasurementChart.html)
- [Data-rate units](https://en.wikipedia.org/wiki/Data-rate_units)
- [Some selected powers of two](https://en.wikipedia.org/wiki/Power_of_two#Some_selected_powers_of_two)

### Latencies

description | nanoseconds | microseconds | milliseconds | notes
:---: | :---: | :---: | :---: | :---:
L1 cache reference | 0.5 ns
branch mispredict | 5 ns
L2 cache reference | 7 ns ||| 14x L1 cache
mutex lock/unlock | 25 ns
main memory reference | 100 ns ||| 20x L2 cache, 200x L1 cache
compress 1K w/cheap compression algorithm | 3,000 ns
send 2K bytes over 1 Gbps network | 20,000 ns | 20 us
read 4K randomly from SSD | 150,000 ns | 150 us || ~1GB/sec SSD
read 1 MB sequentially from memory | 250,000 ns | 250 us
round trip within same data center | 500,000 ns | 500 us
read 1 MB sequentially from SSD | 1,000,000 ns | 1,000 us | 1 ms | ~1GB/sec SSD, 4x memory
disk seek | 10,000,000 ns | 10,000 us | 10 ms | 20x datacenter roundtrip
read 1 MB sequentially from disk | 20,000,000 ns | 20,000 us | 20 ms | 20x SSD, 80x memory
send packet CA->Netherlands->CA | 150,000,000 ns | 150,000 us | 150 ms

Notes:
- 1 ns = 10<sup>-9</sup> seconds
- 1 us = 10<sup>-6</sup> seconds = 1,000 ns
- 1 ms = 10<sup>-3</sup> seconds = 1,000 us = 1,000,000 ns

See also:
- [Building Software Systems at Google and Lessons Learned](https://static.googleusercontent.com/media/research.google.com/en//people/jeff/Stanford-DL-Nov-2010.pdf)
- [Latency Numbers Every Programmer Should Know](https://gist.github.com/jboner/2841832)

### Powers of Two

base 2 | bit size | binary value | description
:---: | :---: | :---: | :---:
2<sup>0</sup> | 1
2<sup>1</sup> | 2 | ```1b```
2<sup>2</sup> | 4
2<sup>3</sup> | 8
2<sup>4</sup> | 16
2<sup>5</sup> | 32
2<sup>6</sup> | 64
2<sup>7</sup> | 128 || signed byte
2<sup>8</sup> | 256 | ```1B``` | unsigned byte
2<sup>9</sup> | 512
2<sup>10</sup> | 1024 | ```1KB```
2<sup>15</sup> | 32,768 || 16-bit word, signed short
2<sup>16</sup> | 65,536 || 16-bit word, unsigned short, char
2<sup>20</sup> | 1,048,576 | ```1MB```
2<sup>30</sup> | 1,073,741,824 | ```1GB```
2<sup>31</sup> | 2,147,483,648 || 32-bit word, signed int
2<sup>32</sup> | 4,294,967,296 || 32-bit word, unsigned int, float
2<sup>40</sup> | 1,099,511,627,776 | ```1TB```
2<sup>63</sup> | 9,223,372,036,854,775,808 || 64-bit word, signed long
2<sup>64</sup> | 18,446,744,073,709,551,616 || 64-bit word, unsigned long, double

See also:
- [Common integral data types](https://en.wikipedia.org/wiki/Integer_(computer_science)#Common_integral_data_types)
- [Some selected powers of two](https://en.wikipedia.org/wiki/Power_of_two#Some_selected_powers_of_two)
- [Orders of magnitude (data)](https://en.wikipedia.org/wiki/Orders_of_magnitude_(data))

## Memory Hierarchy

![](https://upload.wikimedia.org/wikipedia/commons/0/0c/ComputerMemoryHierarchy.svg)

[//]: # (TODO)

[//]: # (https://en.wikipedia.org/wiki/CPU_cache)
[//]: # (https://en.wikipedia.org/wiki/Memory_hierarchy#Examples)

## ACID

A **transaction** is a unit of work comprising actions that access or change the contents of a database.

The four basic (**ACID**) properties that define a transaction are:
- **atomicity**: a transaction is an indivisible unit that is either performed in its entirety or is not performed at all
- **consistency**: a transaction must transform the database from one consistent state to another consistent state
- **isolation**: transactions execute independently of one another
- **durability**: the effects of a successfully completed (committed) transaction are permanently recorded in the database and must not be lost because of a subsequent failure

## REST

A basic HTTP request consists of:
- a verb (or method)
- a resource (or endpoint)

Each HTTP verb:
- has a meaning
- is idempotent or not: *a request method is considered "idempotent" if the intended effect on the server of multiple identical requests with that method is the same as the effect for a single such request* (see [RFC7231: Idempotent methods](https://tools.ietf.org/html/rfc7231#section-4.2.2)).
- is safe or not: *request methods are considered "safe" if their defined semantics are essentially read-only* (see [RFC7231: Safe methods](https://tools.ietf.org/html/rfc7231#section-4.2.1)).
- is cacheable or not

verb | meaning | idempotent | safe | cacheable
:---: | :---: | :---: | :---: | :---:
GET | reads a resource | yes | yes | yes
POST | creates a resource or triggers a data-handling process | no | no | only cacheable if response contains explicit freshness information
PUT | fully updates (replaces) an existing resource or creates a resource | yes | no | no
PATCH | partially updates a resource | no | no | only cacheable if response contains explicit freshness information
DELETE | deletes a resource | yes | no | no

[//]: # (TODO)

[//]: # (http://highscalability.com/blog/2011/1/26/google-pro-tip-use-back-of-the-envelope-calculations-to-choo.html)
[//]: # (https://www.educative.io/collection/page/5668639101419520/5649050225344512/5668600916475904)
[//]: # (https://www.educative.io/collection/page/5668639101419520/5649050225344512/5673385510043648)
