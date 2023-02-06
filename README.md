# Searching

## 1) Linear search
```cpp
#include <bits/stdc++.h>
using namespace std;

bool search(int arr[], int n, int target)
{
    for (int i = 0; i < n; i++)
    {
        if (arr[i] == target)
            return true;
    }
    return false;
}

int main()
{
    int arr[] = {3, 2, 4, 1, 5}, n = 5, target;

    cout << "Enter element to search: ";
    cin >> target;

    if (search(arr, n, target))
        cout << "Element found." << endl;
    else
        cout << "Element not found." << endl;

    return 0;
}

```
## 2) Binary search
```cpp
#include <bits/stdc++.h>
using namespace std;

bool search(int arr[], int n, int target)
{
    int left = 0;
    int right = n - 1;

    while (left <= right)
    {
        int mid = left + (right - left) / 2;
        if (arr[mid] == target)
            return mid;
        else if (arr[mid] < target)
            left = mid + 1;
        else
            right = mid - 1;
    }
    return false;
}

int main()
{
    int arr[] = {1, 2, 3, 4, 5}, n = 5, target;

    cout << "Enter element to search: ";
    cin >> target;

    if (search(arr, n, target))
        cout << "Element found." << endl;
    else
        cout << "Element not found." << endl;

    return 0;
}
```

## 3) Fibonacci search
```cpp
#include <bits/stdc++.h>
using namespace std;

// Function to find the nearest Fibonacci number
bool fibMonaccianSearch(int arr[], int n, int target)
{
    // Initialize fibonacci numbers
    int fibMMm2 = 0;              // (m-2)'th Fibonacci No.
    int fibMMm1 = 1;              // (m-1)'th Fibonacci No.
    int fibM = fibMMm2 + fibMMm1; // mth Fibonacci

    // Fibonacci numbers are generated until
    // the fibM is less than or equal to n
    while (fibM < n)
    {
        fibMMm2 = fibMMm1;
        fibMMm1 = fibM;
        fibM = fibMMm2 + fibMMm1;
    }

    // Initialize variables for Binary Search
    int offset = -1;
    while (fibM > 1)
    {
        // Check if fibMm2 is a valid location
        int i = min(offset + fibMMm2, n - 1);

        // If target is greater than the value at index fibMm2,
        // cut the subarray after i
        if (arr[i] < target)
        {
            fibM = fibMMm1;
            fibMMm1 = fibMMm2;
            fibMMm2 = fibM - fibMMm1;
            offset = i;
        }

        // If target is greater than the value at index fibMm2,
        // cut the subarray before i
        else if (arr[i] > target)
        {
            fibM = fibMMm2;
            fibMMm1 = fibMMm1 - fibMMm2;
            fibMMm2 = fibM - fibMMm1;
        }

        // element found. return true
        else
            return true;
    }

    // comparing the last element with target
    if (fibMMm1 && arr[offset + 1] == target)
        return offset + 1;

    // element not found. return -1
    return false;
}

int main()
{
    int arr[] = {3, 2, 4, 1, 5}, n = 5, target;

    cout << "Enter element to search: ";
    cin >> target;

    if (fibMonaccianSearch(arr, n, target))
        cout << "Element found." << endl;
    else
        cout << "Element not found." << endl;

    return 0;
}

```

# Sorting

## 1) Bubble sort
```cpp
#include <bits/stdc++.h>
using namespace std;

void bubbleSort(int arr[], int n)
{
    for (int i = 0; i < n - 1; i++)
    {
        for (int j = 0; j < n - i - 1; j++)
        {
            if (arr[j] > arr[j + 1])
            {
                swap(arr[j], arr[j + 1]);
            }
        }
    }
}

int main()
{
    int arr[] = {5, 3, 4, 2, 1}, n = 5;

    bubbleSort(arr, n);

    cout << "Sorted array: ";
    for (int i = 0; i < n; i++)
    {
        cout << arr[i] << " ";
    }
    cout << endl;

    return 0;
}

```

## 2) Insertion sort
```cpp
#include <bits/stdc++.h>
using namespace std;

void insertionSort(int arr[], int n)
{
    int i, key, j;
    for (i = 1; i < n; i++)
    {
        key = arr[i];
        j = i - 1;
        while (j >= 0 && arr[j] > key)
        {
            arr[j + 1] = arr[j];
            j = j - 1;
        }
        arr[j + 1] = key;
    }
}
int main()
{
    int arr[] = {5, 3, 4, 2, 1}, n = 5;

    insertionSort(arr, n);

    cout << "Sorted array: ";
    for (int i = 0; i < n; i++)
    {
        cout << arr[i] << " ";
    }
    cout << endl;

    return 0;
}
```
## 3) Quick sort
```cpp
#include <bits/stdc++.h>
using namespace std;

void quickSort(int arr[], int low, int high)
{
    if (low < high)
    {
        int pivotIndex = (low + high) / 2;
        int pivot = arr[pivotIndex];
        int i = low - 1;
        int j = high + 1;

        while (true)
        {
            do
            {
                i++;
            } while (arr[i] < pivot);

            do
            {
                j--;
            } while (arr[j] > pivot);

            if (i >= j)
            {
                pivotIndex = j;
                break;
            }

            swap(arr[i], arr[j]);
        }

        quickSort(arr, low, pivotIndex);
        quickSort(arr, pivotIndex + 1, high);
    }
}

int main()
{
    int arr[] = {5, 3, 4, 2, 1}, n = 5;

    quickSort(arr, 0, n);

    cout << "Sorted array: ";
    for (int i = 0; i < n; i++)
    {
        cout << arr[i] << " ";
    }
    cout << endl;

    return 0;
}
```

## 4) Selection sort
```cpp
#include <bits/stdc++.h>
using namespace std;

void selectionSort(int arr[], int n) {
    for (int i = 0; i < n - 1; i++) {
        int minIndex = i;

        for (int j = i + 1; j < n; j++) {
            if (arr[j] < arr[minIndex]) {
                minIndex = j;
            }
        }

        swap(arr[minIndex], arr[i]);
    }
}

int main()
{
    int arr[] = {5, 3, 4, 2, 1}, n = 5;

    selectionSort(arr, n);

    cout << "Sorted array: ";
    for (int i = 0; i < n; i++)
    {
        cout << arr[i] << " ";
    }
    cout << endl;

    return 0;
}
```

## 5) Radix sort
```cpp
#include <bits/stdc++.h>
using namespace std;

const int MAX_ARRAY_SIZE = 100;
const int MAX_DIGIT = 10;

void radixSort(int arr[], int n) {
  int maxVal = 0;

  // Find the maximum value in the array
  for (int i = 0; i < n; i++) {
    if (arr[i] > maxVal) {
      maxVal = arr[i];
    }
  }

  // Get the number of digits in the maximum value
  int numDigits = (int) log10(maxVal) + 1;

  // Repeat the sorting process for each digit
  for (int digit = 0; digit < numDigits; digit++) {
    int count[MAX_DIGIT] = {0};
    int result[n];

    // Count the frequency of each digit
    for (int i = 0; i < n; i++) {
      count[(arr[i] / (int) pow(10, digit)) % MAX_DIGIT]++;
    }

    // Calculate the cumulative count
    for (int i = 1; i < MAX_DIGIT; i++) {
      count[i] += count[i - 1];
    }

    // Place the elements in the result array
    for (int i = n - 1; i >= 0; i--) {
      result[--count[(arr[i] / (int) pow(10, digit)) % MAX_DIGIT]] = arr[i];
    }

    // Copy the elements back to the original array
    for (int i = 0; i < n; i++) {
      arr[i] = result[i];
    }
  }
}

int main()
{
    int arr[] = {5, 3, 4, 2, 1}, n = 5;

    radixSort(arr, n);

    cout << "Sorted array: ";
    for (int i = 0; i < n; i++)
    {
        cout << arr[i] << " ";
    }
    cout << endl;

    return 0;
}
```
## 6) Counting sort
```cpp
#include <bits/stdc++.h>
using namespace std;

void countingSort(int arr[], int n, int maxVal)
{
    int count[maxVal + 1];
    for (int i = 0; i <= maxVal; i++)
    {
        count[i] = 0;
    }

    for (int i = 0; i < n; i++)
    {
        count[arr[i]]++;
    }

    int j = 0;
    for (int i = 0; i <= maxVal; i++)
    {
        for (int k = 0; k < count[i]; k++)
        {
            arr[j++] = i;
        }
    }
}

int main()
{
    int arr[] = {5, 3, 4, 2, 1}, n = 5;

    countingSort(arr, n, arr[0]);

    cout << "Sorted array: ";
    for (int i = 0; i < n; i++)
    {
        cout << arr[i] << " ";
    }
    cout << endl;

    return 0;
}
```

# Data Structures

## Linked List
```cpp
#include <bits/stdc++.h>
using namespace std;

struct Node {
  int data;
  Node* next;
};

class LinkedList {
  private:
    Node* head;

  public:
    LinkedList() : head(nullptr) {}

    void insert(int data) {
      Node* newNode = new Node;
      newNode->data = data;
      newNode->next = head;
      head = newNode;
    }

    void deleteNode(int data) {
      Node* current = head;
      Node* prev = nullptr;
      while (current != nullptr && current->data != data) {
        prev = current;
        current = current->next;
      }
      if (current == nullptr) return;
      prev->next = current->next;
      delete current;
    }

    void traverse() {
      Node* current = head;
      while (current != nullptr) {
        cout << current->data << " ";
        current = current->next;
      }
    }
};

int main() {
  LinkedList list;
  list.insert(1);
  list.insert(2);
  list.insert(3);
  list.insert(4);
  list.deleteNode(2);
  list.traverse();
  return 0;
}

```

## Stack
```cpp
#include <bits/stdc++.h>
using namespace std;

#define MAX_SIZE 100

class Stack {
  private:
    int data[MAX_SIZE];
    int top_index;

  public:
    Stack() : top_index(-1) {}

    bool isEmpty() {
      return top_index == -1;
    }

    bool isFull() {
      return top_index == MAX_SIZE - 1;
    }

    void push(int value) {
      if (isFull()) {
        cout << "Stack overflow\n";
        return;
      }
      data[++top_index] = value;
    }

    void pop() {
      if (isEmpty()) {
        cout << "Stack underflow\n";
        return;
      }
      --top_index;
    }

    int top() {
      if (isEmpty()) {
        cout << "Stack underflow\n";
        return -1;
      }
      return data[top_index];
    }
};

int main() {
  Stack stack;
  stack.push(1);
  stack.push(2);
  stack.push(3);
  while (!stack.isEmpty()) {
    cout << stack.top() << endl;
    stack.pop();
  }
  stack.pop();
  return 0;
}

```

## Queue
```cpp
#include <bits/stdc++.h>
using namespace std;

#define MAX_SIZE 100

class Queue {
  private:
    int data[MAX_SIZE];
    int head, tail;

  public:
    Queue() : head(0), tail(0) {}

    bool isEmpty() {
      return head == tail;
    }

    bool isFull() {
      return (tail + 1) % MAX_SIZE == head;
    }

    void insert(int value) {
      if (isFull()) {
        cout << "Queue overflow\n";
        return;
      }
      data[tail] = value;
      tail = (tail + 1) % MAX_SIZE;
    }

    void remove() {
      if (isEmpty()) {
        cout << "Queue underflow\n";
        return;
      }
      head = (head + 1) % MAX_SIZE;
    }

    int front() {
      if (isEmpty()) {
        cout << "Queue underflow\n";
        return -1;
      }
      return data[head];
    }
};

int main() {
  Queue queue;
  queue.insert(1);
  queue.insert(2);
  queue.insert(3);
  while (!queue.isEmpty()) {
    cout << queue.front() << endl;
    queue.remove();
  }
  queue.remove();
  return 0;
}

```
