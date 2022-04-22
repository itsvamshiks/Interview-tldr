
# Collections Basics


### Sorting

Sorting Collections  - ```Collections.sort(array)``` <br/>
Sorting in reverse order - ```Collections.sort(array,Collections.reverseOrder())```<br/><br/>

Sorting by Custom Comparator <br/>

```
ArrayList<Employee> employees = getUnsortedEmployeeList();
             
Comparator<Employee> compareById = (Employee o1, Employee o2) -> o1.getId().compareTo( o2.getId() );
 
Collections.sort(employees, compareById);
 
Collections.sort(employees, compareById.reversed());
```


### Iterators on Collections

```
PriorityQueue<Integer> pQueue
            = new PriorityQueue<Integer>(
                Collections.reverseOrder());
                
Iterator<Integer> itr2 = pQueue.iterator(); 

(or)

Iterator itr = pQueue.iterator();

while (itr.hasNext())
     System.out.println(itr.next());

```



### Heap

<b>Min Heap </b>

```
PriorityQueue<Integer> pQueue = new PriorityQueue<Integer>();
```

<b>Max Heap </b>

```
PriorityQueue<Integer> pQueue = new PriorityQueue<Integer>(Collections.reverseOrder());
```

Peeking - ```pQueue.peek()``` (See Top element in heap) <br/>
Polling - ```pQueue.poll()``` (Get and remove Top element in heap) <br/>


