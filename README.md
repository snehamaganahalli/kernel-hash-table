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

hash_del(&my_data.node);

hash_for_each - iterate over a hashtable
unsigned bkt;
struct my_info *curr;
hash_for_each(tbl, bkt, curr, node) // no need to declare/define node.

hash_for_each_safe - iterate over a hashtable safe against removal of hash entry
struct hlist_node *temp;
hash_for_each_safe(tbl, bkt, temp, curr, node) // no need to declare/define node

hash_for_each_possible - iterate over all possible objects hashing to the same bucket
hash_for_each_possible(tbl, curr, node, KEY) // no need to declare/define node
```

You can secure the hash table 'tbl' with the spinlock.

```
DEFINE_SPINLOCK(tbl_lock);
or static DEFINE_SPINLOCK(tbl_lock);

my_info* function() {
  spin_lock_bh(&tbl_lock);
  hash_for_each_safe(tbl, bkt, temp, curr, node) {
    if (curr->some_data == 5) {
      return curr;
      spin_unlock_bh(&tbl_lock);
    }
  }
  return NULL;
  spin_unlock_bh(&tbl_lock);
}
```
