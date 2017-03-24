# 算法

```
// GCD alg
public static gcd(int p, int q)
{
    if (q == 0)
        return p;
    int r = p % q;
    return gcd(q, r);
}
```

- binarySearch

```
public class binarySearch
{
    /**
    *  return the positon of key, if not exists return -1
    */
    public static int rank(int key, int[] arr) {
        int low = 0;
        int high = arr.length - 1;

        while (low <= high) {
            int mid = low + (high - low) / 2;
            if (key < arr[mid])
                high = mid - 1;
            else if (key > arr[mid])
                low = mid + 1;
            else
                return mid;
        }

        return -1;
    }

    public static void main(String[] args) {
        int[] whitelist = In.readInts(args[0]);

        Arrays.sort(whitelist);

        while (!StdIn.isEmpty()) {
            int key = StdIn.readInt();
            if (rank(key, whitelist) == -1)
                System.out.println(key);
        }
    }
}
```

- 递归实现

```
public static int rank(int key, int[] arr) {
    return rank(key, arr, 0, arr.length - 1);
}

public static int rank(int key, int[] arr, int low, int high) {
    if (low > high)
        return -1;
    int mid = low + (high - low) / 2;
    if (key < a[mid])
        return rank(key, arr, low, mid - 1);
    else if (key > a[mid])
        return rank(key, arr, mid + 1, high);
    else
        return mid;
}
```

- Judge a String is Palindrome

```
public static boolean isPalidrome(String s) {
    int N = s.length();
    for (int i = 0; i < N/2; i++) {
        if (s.charAt(i) != s.charAt(N-1-i))
            return false;
    }

    return true;
}
```

- Double Stack to solve the problem

```
public class Evaluate {
    public static void main(String[] args) {
        Stack<String> ops = new Stack<>();
        Stack<Double> vals = new Stack<>();

        whilte (StdIn.isEmpty()) {
            String s = StdIn.readString();
            if (s.equals("("))                     ;
            else if (s.equals("+"))     ops.push(s);
            else if (s.equals("-"))     ops.push(s);
            else if (s.equals("*"))     ops.push(s);
            else if (s.equals("/"))     ops.push(s);
            else if (s.equals("sqrt"))  ops.push(s);
            else if (s.equals(")")) {
                String op = ops.pop();
                double v = vals.pop();

                if (op.equals("+"))     v = vals.pop() + v;
                else if (op.equals("-")) v = vals.pop() - v;
                else if (op.equals("*")) v = vals.pop() * v;
                else if (op.equals("/")) v = vals.pop() / v;
                else if (op.equals("sqrt")) v = Math.sqrt(v);

                vals.push(v);
            }
            else
                vals.push(Double.parseDouble(s));
        }
        System.out.println(vals.pop());
    }
}
```

```
// Stack implements by Array
import java.util.Iterator;

public class FixedCapacityStack<Item>
{
    private Item[] arr = (Item[]) new Object[1];
    private int N = 0;

    public Iterator<Item> iterator() {

    }

    public boolean isEmpty() {
        return N == 0;
    }

    public int size() {
        return N;
    }

    public void resize(int max) {
        Item[] temp = (Item[]) new Object[max];
        for (int i = 0; i < N; i++) {
            temp[i] = arr[i];
        }
        arr = temp;
    }

    public void push(Item item) {
        if (N == arr.length)
            resize(2 * arr.length);
        arr[N++] = item;
    }

    public Item pop() {
        Item item = arr[--N];
        arr[N] = null;

        if (N > 0 && N == arr.length / 4)
            resize(arr.length / 2);

        return item;
    }
}
```

```
public class Stack<Item>
{
    private Node first;
    private int N;

    private class Node {
        Item item;
        Node next;
    }

    public boolean isEmpty() {
        return first == null;
    }

    public int size() {
        return N;
    }

    public void push(Item item) {
        Node oldFirst = first;
        first = new Node();
        first.item = item;
        first.next = oldFirst;
        N++;
    }

    public Item pop() {
        Item item = first.item;
        first = first.next;
        N--;
        return item;
    }
}

public class Queue<Item>
{
    private Node first, last;
    private int N;

    private class Node {
        Item item;
        Node next;
    }

    public boolean isEmpty() {
        return N == 0;
    }

    public int size() {
        return N;
    }

    public void enqueue(Item item) {
        Node oldlast = last;
        last = new Node();
        last.item = item;
        last.next = null;
        if (isEmpty())
            first = last;
        else
            oldlast.next = last;
        N++;
    }

    public Item dequeue() {
        Item item = first.item;
        first = first.next;
        if (isEmpty())
            last = null;
        N--;
        return item;
    }
}


public class Bag<Item> implements Iterable<Item>
{
    private Node first;

    private class Node {
        Item item;
        Node next;
    }

    public void add(Item item) {
        Node oldFirst = first;
        first = new Node();
        first.item = item;
        first.next = oldFirst;
    }

    public Iterator<Item> iterator() {
        return new ListIterator();
    }

    private class ListIterator implements Iterator<Item>
    {
        private Node current = first;

        public boolean hasNext() {
            return current != null;
        }

        public void remove() { }

        public Item next() {
            Item item = current.item;
            current = current.next;
            return item;
        }
    }
}
```

---
1. Java中HashMap的实现
2. Java中Synchronize的用法
3. Android中弱引用的使用（防止GC）
4. 介绍项目中遇到的一个问题（防止被测试坑）
5. 对于本科生的介绍
---
```
// This class is the base of All Sort Alg
public abstract class baseSort {

    public abstract void sort(Comparable[] arr);

    protected static boolean less(Comparable v, Comparable w) {
        return v.compareTo(w) < 0;
    }

    protected static void exch(Comparable[] arr, int i, int j) {
        Comparable t = arr[i];
        arr[i] = arr[j];
        arr[j] = t;
    }

    protected static void show(Comparable[] arr) {
        for (int i = 0; i < arr.length; i++) {
            System.out.print(arr[i] + " ");
        }
        System.out.println();
    }

    protected static boolean isSorted(Comparable[] arr) {
        for (int i = 1; i < arr.length; i++) {
            if (less(arr[i], arr[i - 1]))
                return false;
        }
        return true;
    }

}

---
// Selection Sort
import java.util.Random;

public class SelectionSort extends baseSort {
    @Override
    public void sort(Comparable[] arr) {
        int N = arr.length;
        for (int i = 0; i < N; i++) {
            int min = i;
            for (int j = i + 1; j < N; j++) {
                if (less(arr[j], arr[min]))
                    min = j;
            }
            exch(arr, i, min);
        }
    }

    public static void main(String[] args) {
        Comparable[] arr1 = new Comparable[10];
        int len = arr1.length;
        for (int i = 0; i < len; i++) {
            arr1[i] = new Random().nextInt() % 100;
        }

        System.out.println("Before Sort: ");
        show(arr1);

        baseSort mSort = new SelectionSort();   // Other sort function can only change this scope.
        mSort.sort(arr1);

        assert isSorted(arr1);

        System.out.println("After Sort: ");
        show(arr1);
    }
}
```

```
// Insertion
class Insertion extends baseSort {
    @Override
    protected void sort(Comparable[] arr) {
        int N = arr.length;
        for (int i = 1; i < N; i++) {
            for (int j = i; j > 0 && less(arr[j], arr[j-1]); j--)
                exch(arr, j, j-1);
        }
    }
}

// Shell alg
public class Shell extends baseSort {
    public static void sort(Comparable[] arr) {
        int N = arr.length;
        int h = 1;
        while(h < N/3) {
            h = 3*h + 1;
        }
        while(h >= 1) {
            for (int i = h; i < N; i++) {
                for (int j = i; j >= h && less(arr[j], arr[j-h]); j -= h) {
                    exch(arr, j, j-h);
                }
            }
            h /= 3;
        }
    }
}

// Merge sort
public static void merge(Comparable[] arr, int low, int mid, int high) {
    int i = low, j = mid + 1;   // i for left part begin, j is the right part begin.

    for (int k = low; k <= high; k++) {
        aux[k] = arr[k];
    }

    for (int k = low; k <= high; k++) {
        if      (i > mid)               arr[k] = aux[j++]; // The left part is used
        else if (j > high)              arr[k] = aux[i++]; // The right part is used
        else if (less(aux[j], aux[i]))  arr[k] = aux[j++];
        else                            arr[k] = aux[i++];
    }
}

public class Merge {
    private static Comparable[] aux;

    public static void sort(Comparable[] arr) {
        aux = new Comparable[arr.length];
        sort(arr, 0, a.length-1);
    }

    private static void sort(Comparable[] arr, int low, int high) {
        if (high <= low)    return;
        int mid = low + (high - low) / 2;
        sort(arr, low, mid);    // Sort the left slide
        sort(arr, mid+1, high); // Sort the right part
        merge(arr, low, mid, high);
    }
}

class MergeBU {
    private static Comparable[] aux;
    public static void sort(Comparable[] arr) {
        int N = arr.length;
        aux = new Comparable[N];

        for (int sz = 1; sz < N; sz = sz + sz) {
            for (int low = 0; low < N-sz; low += sz+sz) {
                merge(arr, low, low+sz-1, Math.min(low+sz+sz-1, N-1));
            }
        }
    }
}

class Quick {
    public static void sort(Comparable[] arr) {
        StdRandom.shuffle(arr);
        sort(arr, 0, a.length-1);
    }

    private static void sort(Comparable[] arr, int low, int high) {
        if (low >= high)    return;
        int j = partition(arr, low, high);
        sort(arr, low, j - 1);
        sort(arr, j+1, high);
    }
}

class Quick3way extends baseSort {
    @Override
    public void sort(Comparable[] arr) {
        sort(arr, 0, arr.length-1);
    }

    private void sort(Comparable[] arr, int low, int high) {
        if (high <= low)
            return;
        int lt = low, i = low+1, gt = high;
        Comparable v = arr[low];

        while (i < gt) {
            int cmp = arr[i].compareTo(v);
            if (cmp < 0)
                exch(arr, lt++, i++);
            else if (cmp > 0)
                exch(arr, i, gt--);
            else
                i++;
        }
        sort(arr, low, lt-1);
        sort(arr, gt+1, high);
    }
}
```
