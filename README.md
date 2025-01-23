# DESIGN PATTERN

## Categories
### 1) Creational: Object creational mechanisms to increase reusability.
# 1. Singleton
الـ **Singleton Pattern** هو تصميم يُقيد الـ `class` بحيث لا يمكن إنشاء أكثر من **Instance** واحد منه.
<br>
![image](https://github.com/user-attachments/assets/11ddbc99-135b-4fa1-a06d-66eb8d627443)

لحل مشكلة الـ **Multiple Instantiation**، هناك حلان رئيسيان:

1. **جعل الـ `class` abstract**:  
   هذا يمنع تمامًا إنشاء أي **Instance** من الـ `class`.

2. **جعل الـ Constructor private**:  
   هذا يمنع إنشاء **Instance** من خارج الـ `class`.

---
### أنواع الـ Singleton

### 1. Thread Unsafe Singleton

بعد جعل الـ Constructor `private`، يمكنك استدعاء الـ `class` عن طريق إنشاء **static property** من نوع الـ `class`.

الـ Property تحتوي على شرط (`condition`) باستخدام الـ `get`:

```csharp
if (instance == null) // instance هو static field من نوع الـ class وقيمته الافتراضية null
{
    return instance = new ClassName();
}
else
{
    return instance;
}
```
### 2. Thread Safety

(هذه تقنية لحماية الـ Singleton من إنشاء أكثر من Instance بسبب الـ Multi-Threading)

يتم تحقيق ذلك باستخدام الـ `lock`:

```csharp
lock (_lock)
{
    if (instance == null)
    {
        return instance = new ClassName();
    }
    return instance;
}
```
### 3. Thread Safe Double Checking

في حالة أن الـ `instance` ليس `null`، نحتاج إلى عمل **Double Checking** لتجنب عمل `sync` على شيء فارغ.

```csharp
if (instance == null)
{
    lock (_lock)
    {
        if (instance == null)
        {
            return instance = new MemoryLogger();
        }
    }
}
return instance;
```
### 4. Thread Safe Lazy/Eager Loading

  ![image](https://github.com/user-attachments/assets/6134ade5-c853-4d1c-9673-4bddf9a6ae1f)

#### IN Eager Loading
**ملاحظة**: الـ CLR عند بدء التطبيق يقوم بإنشاء جميع الـ `static fields`.

هنا نقوم بتعديل بسيط على الـ `instance field` الذي أنشأناه --> نجعله `readonly` ونقوم بإنشاء الـ `object` مباشرة.

```csharp
private static readonly MemoryLogger instance = new MemoryLogger();
```
#### IN Lazy Loading
إذا كان إنشاء الـ `object` مكلفًا، فمن الأفضل استخدام الـ **Lazy Loading** بدلًا من الـ **Eager Loading**.  
(وهي عملية إنشاء الـ `object` فقط عند الحاجة إليه).

```csharp
private static readonly Lazy<MemoryLogger> instance
    = new Lazy<MemoryLogger>(() => new MemoryLogger());
```



1. Factory Method
6. Abstract Factory
4. Builder
5. Prototype

### 2) Structural: Assembling objects/classes into larger structures.
  * Composite
  * Bridge
  * Facade
  * Adapter
  * Proxy
  * Decorator
  * FlyWeight
 
  
### 3) 
  
  
