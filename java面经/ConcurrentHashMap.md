# ConcurrentHashMap

## 如何解决HashMap线程不安全的问题

HashMap是线程不安全的，为了保证线程安全，Java提供Hashtable等同步，所谓同步容器，其实大部分就是在原有容器的方法上加上粗粒度的Synchronize包装，在高并发场景下，性能较差。后来，大家更加普遍的选择是利用并发包提供的线程安全容器类，比如ConcurrentHashMap等。

## ConcurrentHashMap的演进过程

早期版本，采用分离锁机制，对map进行分段处理，多个线程不能同时去修改相同段内的数据。

在 Java 8 和之后的版本中，ConcurrentHashMap 发生了哪些变化呢？

+ 总体结构上，它的内部存储变得和我在专栏上一讲介绍的 HashMap 结构非常相似，同样是大的桶（bucket）数组，然后内部也是一个个所谓的链表结构（bin），同步的粒度要更细致一些。
+ 其内部仍然有 Segment 定义，但仅仅是为了保证序列化时的兼容性而已，不再有任何结构上的用处。
+ 因为不再使用 Segment，初始化操作大大简化，修改为 lazy-load 形式，这样可以有效避免初始开销，解决了老版本很多人抱怨的这一点。
+ 数据存储利用 volatile 来保证可见性。
+ 使用 CAS 等操作，在特定场景进行无锁并发操作。
+ 使用 Unsafe、LongAdder 之类底层手段，进行极端情况的优化。





