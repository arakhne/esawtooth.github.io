---
layout: post
title: "Hoare Partitioning and Pivot Selection"
date: 2015-09-06 16:44:51 +0530
comments: true
categories: algorithms
---

Quicksort is a remarkably flexible algorithm with several variations. Here, I wanted to write about the Hoare partitioning method, in particular, about the special choice of its pivot as the leftmost element. First, lets quickly write down the partitioning algorithm from CLRS [exercise 7.1](http://clrs.skanev.com/07/problems/01.html).

{% highlight python %}
    def Hoare_Partition(A, p, r):
        x = A[p]
        i = p - 1
        j = r + 1
        while True:
            while True:
                j = j - 1
                if A[j] <= x:
                    break
            while True:
                i = i + 1
                if A[i] >= x:
                    break
            if i < j:
                A[i], A[j] = A[j], A[i]
            else:
                return j        
    # Output Assertion: A[p..j] <= x and A[j+1..r] >= x
    # in case we use last element to pivot
{% endhighlight %}
   
This partitioning can be called from quicksort as 

{% highlight python %}
    def Quick_Sort(A, p, r):
        if p < r:
            q = Hoare_Partition(A, p, r)
            Quick_Sort(A, p, q)
            Quick_Sort(A, q + 1, r)
{% endhighlight %}

Here, I have translated the algorithm into a simple python function. The only departure from the original algorithm are my implementations of the repeat-until loops as unconditional while loops that break. The parameter `A` is the array which is 0-indexed, though it does not really matter here. `p` and `r` are the boundaries of the sub-array which we wish to partition. Now, if one looks at the function definition, the pivot is used for comparisons of the array elements. However, most of the code looks to be pretty symmetric, when we compare the left and right endpoints of the sub-array. Essentially, in the code we are not "favouring" any particular endpoint, and repeating the same steps for both of them. The only place where there is some bias, is in the `return j` statement, wherein we return the current value of the right endpoint index. 

This led me to try using `A[r]` as the pivot. However, when I simply chose this element as the pivot, the algorithm did not terminate and went into an infinite loop with my test case. Some looking revealed that this was because the algorithm was not able to reduce the size of the partitions. Essentially, the array of size n, in the first recursion itself, was getting "partitioned" into two sub-arrays: `[0..n]` and `[n+1..n]`. This is obviously an error, as the second subarray is meaningless, and the first subarray is the same as the input itself! Clearly, the partitioning is sensitive to the positioning of the pivot. This is corroborated by CLRS exercise 7.1 where it is proved that if `r - p >= 2`, then `p <= j < r`. The strict inequality between j and r breaks down if we use the last element as the pivot. In fact, if we peep into the [proof](http://clrs.skanev.com/07/problems/01.html) of this ordering (which, in turn is required to prove the correctness of the partitioning), it assumes that the first element is the pivot. All this suggests that the recursive calls made in `Quick_Sort` should to be altered to,

{% highlight python %}
    def Quick_Sort_modded(A, p, r):
        if p < r:
            q = Hoare_Partition(A, p, r)
            self.Quick_Sort(A, p, q - 1)
            self.Quick_Sort(A, q, r)
{% endhighlight %}

However, in order to do this, we must depend upon an altered output assertion of Hoare_Partition that looks like `A[p..i-1] <= x and A[i..r] >= x`. Symmetry in the function suggests that we should return i instead of j, and this can be further proved as well by formulating an invariant. So, the modified Hoare Partitioning should look like

{% highlight python %}
    def Hoare_Partition_modded(A, p, r):
        x = A[r]
        i = p - 1
        j = r + 1
        while True:
            while True:
                j = j - 1
                if A[j] <= x:
                    break
            while True:
                i = i + 1
                if A[i] >= x:
                    break
            if i < j:
                A[i], A[j] = A[j], A[i]
            else:
                return i
    # Output Assertion: A[p..i-1] <= x and A[i..r] >= x
    # in case we use last element to pivot
{% endhighlight %}

So, this partitioning is pretty rigid in terms of the choice of the pivot. Hence, if we wish to randomize the pivot selection, we would have to do that in the `Quick_Sort_modded` call itself, by swapping the chosen pivot with the first/last element of the array.
