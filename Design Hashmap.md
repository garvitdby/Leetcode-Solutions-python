# Intuition
<!-- Describe your first thoughts on how to solve this problem. -->
The intuition behind this hash map implementation is to use a large array (called a hash table) as the primary data structure. To map a key to an index in this array, a hash function is applied. Since different keys can produce the same hash value (a collision), the implementation uses a technique called separate chaining. In this method, each index of the hash table holds a list (or "chain") of all key-value pairs that hash to that index. 

The operations (put, get, remove) involve a two-step process: first, use the hash function to find the correct bucket (the list at a particular index); second, perform a linear search within that bucket's list to find or manipulate the specific key-value pair.

# Approach
<!-- Describe your approach to solving the problem. -->
The solution implements a hash map from scratch using the following components:
1. __init__(self):
- Initializes a fixed-size table (self.size = 1000) and creates a list of self.size empty lists. This list of lists serves as the hash table with separate chaining.
2. _hash(self, key):
- A private helper function that computes the hash value for a given integer key using the modulo operator (key % self.size). This determines which bucket to use for the key.
3. put(self, key: int, value: int):
- Calculates the hash for the given key.
- Iterates through the bucket list at the hash_key to check if the key already exists.
- If the key is found, it updates the corresponding value.
- If the key is not found, it appends a new [key, value] pair to the bucket list.
4. get(self, key: int):
- Calculates the hash for the key.
- Iterates through the bucket list at the hash_key.
- If the key is found, it returns the stored value.
- If the loop finishes without finding the key, it returns -1.
5. remove(self, key: int):
- Calculates the hash for the key.
- Iterates through the bucket list at the hash_key using enumerate to get the index i of each pair.
- If the key is found, it removes the pair from the list using del at the correct index. 

# Complexity
- Time complexity:
<!-- Add your time complexity here, e.g. $$O(n)$$ -->
- **put: O(N/K)** where K is the size of the hash table and N is the number of all possible keys. In the best scenario, this approaches O(1).
- **get: O(N/K)** for similar reasons as put.
- **remove: O(N/K).**

- Space complexity:
<!-- Add your space complexity here, e.g. $$O(n)$$ -->
- **O(N + K)** due to storage in lists and the table size.

# Code
```python3 []
class MyHashMap:

    def __init__(self):
        self.size  = 1000
        self.table = [[] for _ in range(self.size)]

    def _hash(self ,key):
        return key % self.size

    def put(self, key: int, value: int) -> None:
        hash_key = self._hash(key)
        for pair in self.table[hash_key]:
            if pair[0] == key:
                pair[1] = value
                return
        self.table[hash_key].append([key, value])

    def get(self, key: int) -> int:
        hash_key = self._hash(key)
        for pair in self.table[hash_key]:
            if pair[0] == key:
                return pair[1]
        return -1

    def remove(self, key: int) -> None:
        hash_key = self._hash(key)
        for i, pair in enumerate(self.table[hash_key]):
            if pair[0] == key:
                del self.table[hash_key][i]
                return


# Your MyHashMap object will be instantiated and called as such:
# obj = MyHashMap()
# obj.put(key,value)
# param_2 = obj.get(key)
# obj.remove(key)
```
