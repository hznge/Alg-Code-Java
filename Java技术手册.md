# Java 技术手册
> Java中基本的数据类型：boolean, char, byte, long, int, double, float, short

> synchronize(expression) expression必须为一个对象或数组。

try 语句后面的finally会执行情况：
1. 正常结束：到达块末尾
2. 由break、continue或return语句导致
3. 抛出异常，由上述的catch语句处理
4. 抛出异常，未被捕获处理
- 但是,如果在try中调用了System.exit(), 解释器会立即退出，不执行finally字句。

> 引用类型与基本类型的比较：
- 八种基本类型由Java语言定义，程序员不能定义新的类型。引用类型由用户定义，因此有无限多个。
- 基本类型表示单个值，引用类型是聚合类型，可以保存0...多个基本值或对象。
- 基本类型需要一到八个字节的内存空间。把基本值存储到变量中，或传入方法时，计算机会复制表示这个值的字节。
对象则需要更多的内存，创建对象时会在堆(heap)中动态分配内存，存储这个对象。如果不需要这个对象了，存储它的内存会被GC

String 不是基本的数据类型.


接口：接口不能直接实例化，也不能创建这种接口类型的成员。接口必须通过类实现，而且类要提供所需的方法主体。

枚举: 枚举是特殊的类，可以拥有成员（即字段、方法）。
枚举的属性：
1. 都扩展自java.lang.Enum类，
2. 不能泛型化
3. 可以实现接口
4. 不能被扩展
5. 如果枚举中所有值都有实现主体，那么只能定义为抽象方法
6. 只能有一个私有（或者默认访问权限的）构造方法


委托：某个特殊类型的对象保存一个引用，指向一个兼容类型的附属对象，而且把所有的操作交给这个附属对象完成。（这种技术一般使用接口实现）

```
public interface Employee {
    void work();
}

public class Programmer implements Employee {
    public void work {
        System.out.println("Programmer program");
    }
}

class Manager implements Employee {
    private Employee report;

    public Manager(Employee staff) {
        report = staff;
    }

    public Employee setReport(Employee staff) {
        report = staff;
    }

    public void work() {
        report.work();
    }
}
```

- volatile关键字：这个关键字指明，应用代码使用字段或变量前，必须重新从主存读取值。同时，修改使用volatile关键字修饰的值后，在写入变量之后，必须存回主内存。
