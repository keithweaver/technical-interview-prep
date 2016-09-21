# Hash Tables


Pros: 
- Speed is priority
- In theory, can be constant time

https://www.youtube.com/watch?v=h2d9b_nEzoA

Hash table are key value storage.

Collision: when two keys go to the same data set.

Resolving collisions:
Linear Probing
If key hashes to same spot, it then goes to the next avalaible spot.

[1:apple]
[2:banana]
[3:cat]
[4:ant]
[5:another]

Separate Chaining
Pointers to linked list, this forces to search the entire linked list

Runtime:O(n/k)

Developing a hash function, use all data given.

```
public class HashEntry {
      private int key;
      private int value;
 
      HashEntry(int key, int value) {
            this.key = key;
            this.value = value;
      }     
 
      public int getKey() {
            return key;
      }
 
      public int getValue() {
            return value;
      }
}

public class HashMap {
      private final static int TABLE_SIZE = 128;
 
      HashEntry[] table;
 
      HashMap() {
            table = new HashEntry[TABLE_SIZE];
            for (int i = 0; i < TABLE_SIZE; i++)
                  table[i] = null;
      }
 
      public int get(int key) {
            int hash = (key % TABLE_SIZE);
            while (table[hash] != null && table[hash].getKey() != key)
                  hash = (hash + 1) % TABLE_SIZE;
            if (table[hash] == null)
                  return -1;
            else
                  return table[hash].getValue();
      }
 
      public void put(int key, int value) {
            int hash = (key % TABLE_SIZE);
            while (table[hash] != null && table[hash].getKey() != key)
                  hash = (hash + 1) % TABLE_SIZE;
            table[hash] = new HashEntry(key, value);
      }
}
```
