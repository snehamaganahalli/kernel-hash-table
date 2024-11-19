# kernel-hash-table
Kernel hash table

```
DEFINE_HASHTABLE(tbl, TABLE_SIZE);
```

// Suppose TABLE_SIZE is 2 => 2^2 =4 \
// Suppose TABLE_SIZE is 3 => 2^3 =8

This is the size of the buckets.

**Eg:**

```
typedef struct my_info{
int key;
int some_data;
struct hlist_node node; // hash node
}

my_info my_data;

hash_add(tbl, &my_data.node, my_data.key);
i.e.
hash_add(table, hash_node_element, hash_key)
```

```
