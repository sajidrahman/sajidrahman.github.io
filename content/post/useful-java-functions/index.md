---
title: Miscellaneous and Handy Java Functions

# Summary for listings and search engines
summary: Miscellaneous and Handy Java Functions

# Link this post with a project
projects: []

# Date published
date: "2020-12-13T00:00:00Z"

# Date updated
lastmod: "2020-11-13T00:00:00Z"

# Is this an unpublished draft?
draft: false

# Show this page in the Featured widget?
featured: false

# Featured image
# Place an image named `featured.jpg/png` in this page's folder and customize its options here.
image:
  caption: 'Image credit: [**Unsplash**](https://unsplash.com/photos/CpkOjOcXdUY)'
  focal_point: ""
  placement: 2
  preview_only: false

authors:
- admin

tags: [Java, Miscellaneous, Functions]


categories:
- How-to
---

### Object Ordering/Comparing:

1. A ``List l`` can be sorted as follows:
``Collections.sort(l)``. If the ``List`` consists of built-in class objects, e.g. ``String, Integer, Long, Date, Character, File`` etc., then the objects will be sorted in a way of _natural_ ordering of that class. But for objects from custom classes, our class needs to either implement ``Comparable`` interface or it can implement ``Comparator`` interface to provide a custom comparator for ``Collections.sort(list, comparator)`` method. The following example is adapted from [Oracle's tutorial](https://docs.oracle.com/javase/tutorial/collections/interfaces/order.html) page.

```java

import java.util.*;
public class EmpSort {
  //we can either define a comparator here
    static final Comparator<Employee> SENIORITY_ORDER =
                                        new Comparator<Employee>() {
            public int compare(Employee e1, Employee e2) {
                return e2.hireDate().compareTo(e1.hireDate());
            }
    };

    // Employee database
    static final Collection<Employee> employees = ... ;

    public static void main(String[] args) {
        List<Employee> employeeList = new ArrayList<Employee>(employees);
        //Collections.sort(employeeList,  SENIORITY_ORDER);
        // Or we can define comparator in-line with the sort method, as shown below
        @Override
        Collections.sort(employeeList, new Comparator<Employee>() {
            public int compare(Employee e1, Employee e2) {
                return e2.hireDate().compareTo(e1.hireDate());
            }
    });
        System.out.println(employeeList);
    }
}
```
2. Similar to `List`, `java.util.Arrays` also provides convenient `sort()` method for ordering primitive data types. For example, the following example sorts an integer array in `O(n log(n))`. The sort method here implements a [dual-pivot Quicksort](https://docs.oracle.com/javase/7/docs/api/java/util/Arrays.html#sort(int[]) algorithm.

```java

import java.util.Arrays;

public class SortExample
{
    public static void main(String[] args)
    {
        int[] arr = {13, 77, 609, 45, 21, 9, 101, 102, -101, 30};

        Arrays.sort(arr);

        System.out.printf("Modified arr[] : %s", Arrays.toString(arr));
    }
}
```

### Conversion
1. String to Character array:

```java

String string = "Hello world!";
char[] stringToCharArray = string.toCharArray();
```
