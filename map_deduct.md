Document number: PxxxxR0  
Date: 2021-0x-0y  
Audience: Library Working Group  
Author: Mike Spertus, Amazon  
Reply-To: msspertu@amazon.com  
# Deducing ordered containers from initializer lists

## The problem
The resolution for [LWG3025](https://cplusplus.github.io/LWG/issue3025) enabled code like the following to be accepted
```c++
map m1{pair{1, 2}, {3, 4}}; // map<int, int>
```
but breaks code that had been previously working like the following
```c++
using value_type = pair<const int, int>;
map m2 = {value_type{1, 2}, {3, 4}};
```
as shown in https://godbolt.org/z/195MWT. 

Since `value_type` is the usual key-value type for a map, we believe this would be expected to work as well, which we fix with the wording below

**Acknowledgment:** We would like to acknowledge Tim Song and Arthur O'Dwyer for independently pointing out this case on the LWG mailing list.

## Solution
T
