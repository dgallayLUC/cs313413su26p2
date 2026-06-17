# Code Questions
TestIterator:
Question: Also try with a LinkedList - does it make any difference? (TestIterator)
    - functionally no, but a LL is more efficient:
    we can remove in O(1), whereas arrayList requires us to shift following elements = O(n)
Question: What happens if you use list.remove(Integer.valueOf(77))?
    - the list's count while change mid-iteration,
    and it will fail on the next loop with a ConcurrentModificationException
TestList:
Question: Also try with a LinkedList - does it make any difference? (TestList)
    - this has no functional or efficiency benefit, other than a change to the underlying data structure
    when rerunning the unit tests with each, both were within .05s
Question: What does this method do? (testRemoveObject)
    - it tests the removal of an item from the list using list.remove(index)
    in this given line, it removes the item at index 5 (the 3rd occurrence of 77)
Question: What does this one do? (list.remove(Integer.valueOf(5)))
    - it removes the first occurrence of the value '5' in the list (index 4)
TestPerformance:
Run test and record running times for SIZE = 10, 100, 1000, 10000
    SIZE    ArrayListAccess ArrayListAddRemove  LinkedListAccess    LinkedListAddRemove 	Total
    10      0.021           0.036               0.013               0.040                   0.110s
    100     0.026           0.056               0.034               0.049                   0.165s
    1000    0.023           0.162               0.404               0.037                   0.626s
    10000   0.013           1.032               5.206               0.029                   6.280s
Question: What conclusions can you draw about the performance of LinkedList vs. ArrayList
    - arrayLists can jump directly to the index, while a LL has to traverse an entire list for lookups.
    we see this in Access tests, where ArrayList performs ~.02 seconds consistently, while LL's scale very poorly
    and take >5s as n->10000+
    however, LLs are much more efficient for add and remove operations.
    this is expected, as they can simply drop the value and repoint, whereas arrays need to shift all values.
    we see this in the AddRemove tests, where LL stays ~.04s and ArrayList starts there and scales poorly
Which of the two lists performs better as the size increases?
    - this depends on the end goal. does the production system expect to see more add/remove or lookups?
    i'd lean towards the arrayList, because LL access is the true bottleneck in the system
    (5s at n=10000, vs 1s for ArrayList add/remove), but this can't be answered without understanding the product
Choose this value (SIZE) in such a way that you can observe an actual effect
    - selecting 1000 as SIZE constant
    it has the best combination of high enough variation to see performance differences
    while still being fast enough to not wait on tests to finish