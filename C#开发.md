# C# 开发

## 异步编程
- **`async` 和 `await`**：用于异步方法的声明和调用，避免阻塞主线程。
  ```csharp
  public async Task<string> GetDataAsync()
  {
      await Task.Delay(1000);
      return "Data Loaded";
  }
  ```
- **`Task` 和 `Task<T>`**：表示异步操作的结果。
- **`ConfigureAwait(false)`**：在库代码中避免捕获上下文，提升性能。

## LINQ（Language Integrated Query）
- **查询表达式**：简化对集合的查询操作。
  ```csharp
  var results = from item in items
                where item.Age > 18
                select item;
  ```
- **方法语法**：链式调用查询方法。
  ```csharp
  var results = items.Where(item => item.Age > 18).Select(item => item.Name);
  ```
- **延迟执行**：LINQ 查询在访问结果时才执行。

## 委托与事件
- **委托**：类型安全的函数指针。
  ```csharp
  public delegate void MyDelegate(string message);
  MyDelegate del = Console.WriteLine;
  del("Hello, Delegate!");
  ```
- **事件**：基于委托的发布/订阅模式。
  ```csharp
  public event EventHandler MyEvent;
  MyEvent?.Invoke(this, EventArgs.Empty);
  ```

## 反射
- **动态加载类型和调用方法**：
  ```csharp
  var type = typeof(MyClass);
  var method = type.GetMethod("MyMethod");
  method.Invoke(instance, null);
  ```
- **获取属性和字段信息**：
  ```csharp
  var properties = type.GetProperties();
  ```

## 泛型
- **泛型类和方法**：提高代码复用性和类型安全性。
  ```csharp
  public class GenericClass<T>
  {
      public T Value { get; set; }
  }
  ```
- **泛型约束**：限制泛型类型的范围。
  ```csharp
  public void MyMethod<T>() where T : new()
  {
      T instance = new T();
  }
  ```

## 依赖注入（DI）
- **构造函数注入**：通过构造函数传递依赖。
  ```csharp
  public class MyService
  {
      private readonly IRepository _repository;
      public MyService(IRepository repository)
      {
          _repository = repository;
      }
  }
  ```
- **使用 .NET Core 内置 DI 容器**：
  ```csharp
  services.AddScoped<IMyService, MyService>();
  ```

## 内存管理
- **`IDisposable` 和 `using`**：管理非托管资源。
  ```csharp
  using (var resource = new Resource())
  {
      // Use resource
  }
  ```
- **垃圾回收（GC）**：自动管理内存分配和释放。
- **`GC.Collect()`**：强制触发垃圾回收（不推荐频繁使用）。

## 并发与多线程
- **`Task` 并行库（TPL）**：简化并发编程。
  ```csharp
  var tasks = new List<Task>
  {
      Task.Run(() => DoWork()),
      Task.Run(() => DoMoreWork())
  };
  await Task.WhenAll(tasks);
  ```
- **`lock` 关键字**：防止多线程访问共享资源时的竞争条件。
  ```csharp
  lock (_lockObject)
  {
      // Critical section
  }
  ```
- **`Parallel.For` 和 `Parallel.ForEach`**：并行处理集合。
  ```csharp
  Parallel.For(0, 10, i => Console.WriteLine(i));
  ```

## 序列化与反序列化
- **JSON 序列化**：
  ```csharp
  var json = JsonSerializer.Serialize(myObject);
  var obj = JsonSerializer.Deserialize<MyClass>(json);
  ```
- **XML 序列化**：
  ```csharp
  var serializer = new XmlSerializer(typeof(MyClass));
  using (var writer = new StringWriter())
  {
      serializer.Serialize(writer, myObject);
  }
  ```

## 属性与索引器
- **自动属性**：简化属性声明。
  ```csharp
  public string Name { get; set; }
  ```
- **只读属性**：通过 `get` 访问器实现。
  ```csharp
  public string Name => "ReadOnly";
  ```
- **索引器**：通过索引访问对象的值。
  ```csharp
  public string this[int index] => _items[index];
  ```

## 异常处理
- **`try-catch-finally`**：捕获和处理异常。
  ```csharp
  try
  {
      // Code that may throw an exception
  }
  catch (Exception ex)
  {
      Console.WriteLine(ex.Message);
  }
  finally
  {
      // Cleanup code
  }
  ```
- **自定义异常**：
  ```csharp
  public class MyException : Exception
  {
      public MyException(string message) : base(message) { }
  }
  ```

## 设计模式
- **单例模式**：
  ```csharp
  public class Singleton
  {
      private static readonly Singleton _instance = new Singleton();
      public static Singleton Instance => _instance;
      private Singleton() { }
  }
  ```
- **工厂模式**：
  ```csharp
  public class Factory
  {
      public static IProduct CreateProduct(string type)
      {
          return type switch
          {
              "A" => new ProductA(),
              "B" => new ProductB(),
              _ => throw new ArgumentException("Invalid type")
          };
      }
  }
  ```
- **依赖注入模式**：通过构造函数或接口注入依赖。

---

将以上内容保存到 `C#开发.md` 文件中即可。# C# 开发

## 异步编程
- **`async` 和 `await`**：用于异步方法的声明和调用，避免阻塞主线程。
  ```csharp
  public async Task<string> GetDataAsync()
  {
      await Task.Delay(1000);
      return "Data Loaded";
  }
  ```
- **`Task` 和 `Task<T>`**：表示异步操作的结果。
- **`ConfigureAwait(false)`**：在库代码中避免捕获上下文，提升性能。

## LINQ（Language Integrated Query）
- **查询表达式**：简化对集合的查询操作。
  ```csharp
  var results = from item in items
                where item.Age > 18
                select item;
  ```
- **方法语法**：链式调用查询方法。
  ```csharp
  var results = items.Where(item => item.Age > 18).Select(item => item.Name);
  ```
- **延迟执行**：LINQ 查询在访问结果时才执行。

## 委托与事件
- **委托**：类型安全的函数指针。
  ```csharp
  public delegate void MyDelegate(string message);
  MyDelegate del = Console.WriteLine;
  del("Hello, Delegate!");
  ```
- **事件**：基于委托的发布/订阅模式。
  ```csharp
  public event EventHandler MyEvent;
  MyEvent?.Invoke(this, EventArgs.Empty);
  ```

## 反射
- **动态加载类型和调用方法**：
  ```csharp
  var type = typeof(MyClass);
  var method = type.GetMethod("MyMethod");
  method.Invoke(instance, null);
  ```
- **获取属性和字段信息**：
  ```csharp
  var properties = type.GetProperties();
  ```

## 泛型
- **泛型类和方法**：提高代码复用性和类型安全性。
  ```csharp
  public class GenericClass<T>
  {
      public T Value { get; set; }
  }
  ```
- **泛型约束**：限制泛型类型的范围。
  ```csharp
  public void MyMethod<T>() where T : new()
  {
      T instance = new T();
  }
  ```

## 依赖注入（DI）
- **构造函数注入**：通过构造函数传递依赖。
  ```csharp
  public class MyService
  {
      private readonly IRepository _repository;
      public MyService(IRepository repository)
      {
          _repository = repository;
      }
  }
  ```
- **使用 .NET Core 内置 DI 容器**：
  ```csharp
  services.AddScoped<IMyService, MyService>();
  ```

## 内存管理
- **`IDisposable` 和 `using`**：管理非托管资源。
  ```csharp
  using (var resource = new Resource())
  {
      // Use resource
  }
  ```
- **垃圾回收（GC）**：自动管理内存分配和释放。
- **`GC.Collect()`**：强制触发垃圾回收（不推荐频繁使用）。

## 并发与多线程
- **`Task` 并行库（TPL）**：简化并发编程。
  ```csharp
  var tasks = new List<Task>
  {
      Task.Run(() => DoWork()),
      Task.Run(() => DoMoreWork())
  };
  await Task.WhenAll(tasks);
  ```
- **`lock` 关键字**：防止多线程访问共享资源时的竞争条件。
  ```csharp
  lock (_lockObject)
  {
      // Critical section
  }
  ```
- **`Parallel.For` 和 `Parallel.ForEach`**：并行处理集合。
  ```csharp
  Parallel.For(0, 10, i => Console.WriteLine(i));
  ```

## 序列化与反序列化
- **JSON 序列化**：
  ```csharp
  var json = JsonSerializer.Serialize(myObject);
  var obj = JsonSerializer.Deserialize<MyClass>(json);
  ```
- **XML 序列化**：
  ```csharp
  var serializer = new XmlSerializer(typeof(MyClass));
  using (var writer = new StringWriter())
  {
      serializer.Serialize(writer, myObject);
  }
  ```

## 属性与索引器
- **自动属性**：简化属性声明。
  ```csharp
  public string Name { get; set; }
  ```
- **只读属性**：通过 `get` 访问器实现。
  ```csharp
  public string Name => "ReadOnly";
  ```
- **索引器**：通过索引访问对象的值。
  ```csharp
  public string this[int index] => _items[index];
  ```

## 异常处理
- **`try-catch-finally`**：捕获和处理异常。
  ```csharp
  try
  {
      // Code that may throw an exception
  }
  catch (Exception ex)
  {
      Console.WriteLine(ex.Message);
  }
  finally
  {
      // Cleanup code
  }
  ```
- **自定义异常**：
  ```csharp
  public class MyException : Exception
  {
      public MyException(string message) : base(message) { }
  }
  ```

## 设计模式
- **单例模式**：
  ```csharp
  public class Singleton
  {
      private static readonly Singleton _instance = new Singleton();
      public static Singleton Instance => _instance;
      private Singleton() { }
  }
  ```
- **工厂模式**：
  ```csharp
  public class Factory
  {
      public static IProduct CreateProduct(string type)
      {
          return type switch
          {
              "A" => new ProductA(),
              "B" => new ProductB(),
              _ => throw new ArgumentException("Invalid type")
          };
      }
  }
  ```
- **依赖注入模式**：通过构造函数或接口注入依赖。

---

将以上内容保存到 `C#开发.md` 文件中即可。