## Pain and Suffering

To summarize this, We as developers in this course will go through hell and back in order to achieve something that would take a regular developer 2 years worth of experience and even then it would not cut it.

We have to stay focus minded on why we are doing this?, what our goals are?, are we doing this for us?, and stay positive because after this we will be among the experienced developers.

## Beginners Guide to Big O
Some of it is taken from [Beginners Guide to Big O](https://rob-bell.net/2009/06/a-beginners-guide-to-big-o-notation)

Here there is a talk about algorithms which developers face and are somewhat hard at the beginning but are used for a purpose. 

These are: 

### O(1):
>which describes an algorithm that will always execute in the same time (or space) regardless of the size of the input data set.

```
bool IsFirstElementNull(IList<String> elements)
{
    return elements[0] == null;
}
```

### O(N):
>Which describes an algorithm whose performance will grow linearly and in direct proportion to the size of the input data set. 

which in my opinion sounds like N is the number of loops inside the algorithm. I think
```
bool ContainsValue(IEnumerable<string> elements, string value)
{
    foreach (var element in elements)
    {
        if (element == value) return true; 
    }     
    return false; 
}
```
### O(N²):
> represents an algorithm whose performance is directly proportional to the square of the size of the input data set. This is common with algorithms that involve nested iterations over the data set. Deeper nested iterations will result in O(N³), O(N⁴) etc.
```
bool ContainsDuplicates(IList<string> elements)
{
    for (var outer = 0; outer < elements.Count; outer++) 
    {
        for (var inner = 0; inner < elements.Count; inner++) 
        { 
            // Don't compare with self 
            if (outer == inner) continue;             
            
            if (elements[outer] == elements[inner]) return true; 
        }
    }    
    return false;
}
```

### O(2^N):
which says that the higher the data set input the more curved it will be and that it is an exponential relationship, which somewhat represents the fibonacci function.
```
int Fibonacci(int number)
{
    if (number <= 1) return number;
       
    return Fibonacci(number - 2) + Fibonacci(number - 1); 
}
```

### Logarithms:
> it is like binary search which is a technique used to search sorted data sets. It works by selecting the middle element of the data set, essentially the median, and compares it against a target value. If the values match, it will return success. If the target value is higher than the value of the probe element, it will take the upper half of the data set and perform the same operation against it. Likewise, if the target value is lower than the value of the probe element, it will perform the operation against the lower half. It will continue to halve the data set with each iteration until the value has been found or until it can no longer split the data set.

This type is defined as  O(log N) which keeps cutting data set in half until it finds the item it is searching for or the data set reaches a point where it can no longer split.

----------------------------------------------------
## Names and Values in Python

First thing is an assignment (=) never copies data ie
it only finds the data so x and y have the same list
if something happens to it x and y will change.
lists  are mutable   
```
x = [1,2,3,4]
y = x 
x.append(5)
print(y) 
the output here would be [1,2,3,4,5] 
```
Immutable values are values that can not change no matter what, like strings, integers,floats and tuples. 

but here we need to look at difference between rebinding and mutating. 
x got rebinded into a new int not that the int changed so it remains immutable, but add 8 to the list changed it and therefore it is mutable.
```
x = x + 2 
nums = append(8)
```
-------------------------------------------

So what i have figured out is that when you add to a list it actually uses something called peseudo code. which changes 
```
nums.append(6) into
class Nums: 
            def __iadd__(self,other):
            self.extend(other) 
            return self
            then it reassigns it self
            nums = nums
``` 
-----------------------------------------------
### References

- object attributes
- List elements
- Dictionary key value pairs
- Anything located on the left side of an assignment is a reference 

-------------------------------------------------
### Assignment
Assignments are not always just =  it can be in other forms like:
For in 
def fn()
import 

-------------------------------------------------
#### Notes
> Best advice for mutable alliasing is dont mutate values but create new lists!
> Names have no type, values have no scope
