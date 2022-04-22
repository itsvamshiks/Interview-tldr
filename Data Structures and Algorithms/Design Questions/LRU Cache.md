##Implement the LRUCache class:

LRUCache(int capacity) Initialize the LRU cache with positive size capacity.
int get(int key) Return the value of the key if the key exists, otherwise return -1.
void put(int key, int value) Update the value of the key if the key exists. Otherwise, add the key-value pair to the cache. If the number of keys exceeds the capacity from this operation, evict the least recently used key.
The functions get and put must each run in O(1) average time complexity.

### #NOTE : Here, we are using Custom Doubly Linked List for achieving O(1) get and put operations. If there is no such restriction, you can use standard Java Queue which has O(n) get and put operations

```
class LRUCache {
    
    class DLLNode {
        int key;
        int value;
        DLLNode prev;
        DLLNode next;
    }
    
    private void addNode(DLLNode node){
        node.prev = head;
        node.next = head.next;
        
        head.next.prev = node;
        head.next = node;
        
    }
    
    private void removeNode(DLLNode node){
        DLLNode prev = node.prev;
        DLLNode next = node.next;
        
        prev.next = next;
        next.prev = prev;
    }
    
    private void moveToHead(DLLNode node){
        removeNode(node);
        addNode(node);
    }
    
    private DLLNode popTail(){
        DLLNode res = tail.prev;
        removeNode(res);
        return res;
    }
    
    private Map<Integer,DLLNode> cache = new HashMap<>();
    private int size,capacity;
    private DLLNode head,tail;

    public LRUCache(int capacity) {
        
        this.size = 0;
        this.capacity = capacity;
        this.head = new DLLNode();
        this.tail = new DLLNode();
        
        head.next = tail;
        tail.prev = head;
        
    }
    
    public int get(int key) {
        
        DLLNode node = cache.get(key);
        if (node == null) return -1;

        // move the accessed node to the head;
        moveToHead(node);

        return node.value;
        
    }
    
    public void put(int key, int value) {
        
        DLLNode node = cache.get(key);

        if(node == null) {
          DLLNode newNode = new DLLNode();
          newNode.key = key;
          newNode.value = value;

          cache.put(key, newNode);
          addNode(newNode);

          ++size;

          if(size > capacity) {
            // pop the tail
            DLLNode tail = popTail();
            cache.remove(tail.key);
            --size;
          }
        } else {
          // update the value.
          node.value = value;
          moveToHead(node);
        }
        
    }
}

/**
 * Your LRUCache object will be instantiated and called as such:
 * LRUCache obj = new LRUCache(capacity);
 * int param_1 = obj.get(key);
 * obj.put(key,value);
 */
 
```
