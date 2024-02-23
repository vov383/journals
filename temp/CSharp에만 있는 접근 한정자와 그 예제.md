---
title: CSharp에만 있는 접근 한정자와 그 예제
created: 2024-02-22 04:54
alias:
tags:
---
# 1. `internal`

`internal` 접근 한정자는 해당 멤버가 정의된 어셈블리 내에서만 접근 가능하도록 제한합니다. 
다른 어셈블리에서는 접근할 수 없습니다. 이는 어플리케이션 또는 라이브러리 내부에서만 사용되는 타입이나 멤버를 정의할 때 유용합니다.

**예제:**
```csharp
internal class InternalClass
{
    internal int InternalMethod() => 42;
}

public class AccessExample
{
    public void Test()
    {
        InternalClass internalInstance = new InternalClass();
        int result = internalInstance.InternalMethod(); // 같은 어셈블리 내에서 접근 가능
    }
}
```
`InternalClass`와 그의 메서드 `InternalMethod`는 같은 어셈블리 내부에서만 접근 가능합니다.

# 2. `protected internal`

`protected internal` 접근 한정자는 해당 멤버가 정의된 어셈블리 내에서, 또는 파생 클래스에서 접근할 수 있도록 합니다. 
이는 `protected`와 `internal`의 조합으로, 둘 중 하나의 조건을 만족하면 접근이 가능합니다.

**예제:**
```csharp
public class BaseClass
{
    protected internal int MyProtectedInternalMethod() => 42;
}

public class DerivedClass : BaseClass
{
    public int TestMethod()
    {
        return MyProtectedInternalMethod(); // 파생 클래스에서 접근 가능
    }
}

public class OtherClass
{
    public void TestMethod()
    {
        BaseClass baseInstance = new BaseClass();
        int result = baseInstance.MyProtectedInternalMethod(); // 같은 어셈블리 내에서 접근 가능
    }
}
```
`MyProtectedInternalMethod` 메서드는 `BaseClass`의 파생 클래스 또는 같은 어셈블리 내의 다른 클래스에서 접근할 수 있습니다.

# 3. `private protected`

`private protected` 접근 한정자는 
해당 멤버가 선언된 클래스에서 또는 동일한 어셈블리 내의 파생 클래스에서만 접근할 수 있도록 제한합니다. 
이는 `private`와 `protected`의 조합으로, 두 조건 모두를 만족하는 상황에서만 접근이 가능합니다.

**예제:**
```csharp
public class BaseClass
{
    private protected int MyPrivateProtectedMethod() => 42;
}

public class DerivedClass : BaseClass
{
    public int TestMethod()
    {
        return MyPrivateProtectedMethod(); // 동일 어셈블리 내의 파생 클래스에서 접근 가능
    }
}

public class OtherClass
{
    public void TestMethod()
    {
        BaseClass baseInstance = new BaseClass();
        // int result = baseInstance.MyPrivateProtectedMethod(); // 접근 불가능, 컴파일 에러
    }
}
```
`MyPrivateProtectedMethod` 메서드는 `BaseClass` 또는 동일한 어셈블리 내의 `BaseClass`의 파생 클래스에서만 접근할 수 있습니다.

이러한 접근 한정자들은 
C#의 타입 시스템을 이용한 세밀한 접근 제어를 가능하게 하며, 
특히 라이브러리 설계나 대규모 어플리케이션 개발에서 유용하게 사용됩니다. 

