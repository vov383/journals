---
title: 인터페이스의 메서드를 public으로 구현해야 하는 이유와 사례
created: 2024-08-29 02:15
alias:
tags:
---
인터페이스 메서드를 `public`으로 구현해야 하는 이유는 인터페이스가 정의하는 계약을 외부에서 사용할 수 있어야 하기 때문입니다. 실무에서 이를 이해하기 쉽게 설명할 수 있는 몇 가지 예시를 살펴보겠습니다.

#### 1. **플러그인 아키텍처**

플러그인 기반 아키텍처에서 인터페이스는 플러그인이 제공해야 할 기능을 정의합니다. 예를 들어, 플러그인이 특정 데이터를 처리하는 메서드를 제공해야 한다고 가정해 봅시다. 이 경우, 인터페이스를 사용하여 해당 메서드를 정의합니다.

```csharp
public interface IPlugin
{
    void ProcessData(string data);
}

public class DataProcessor : IPlugin
{
    public void ProcessData(string data)
    {
        // 데이터 처리 로직
    }
}
```

- **이유**: 플러그인 로딩 시스템이 `IPlugin` 인터페이스를 구현한 클래스의 `ProcessData` 메서드를 호출하려면, 이 메서드는 외부에서 접근 가능해야 합니다. 만약 `ProcessData`가 `private`으로 구현된다면, 플러그인 시스템은 이 메서드를 호출할 수 없게 되어 인터페이스의 목적을 달성할 수 없습니다.

#### 2. **의존성 주입 (Dependency Injection)**

의존성 주입 패턴에서 인터페이스는 종속성을 주입받는 클래스가 어떤 기능을 사용할 수 있는지를 정의합니다. 예를 들어, 서비스 클래스가 특정 로깅 기능에 의존한다고 가정해 봅시다.

```csharp
public interface ILogger
{
    void Log(string message);
}

public class FileLogger : ILogger
{
    public void Log(string message)
    {
        // 로그를 파일에 기록하는 로직
    }
}

public class Service
{
    private readonly ILogger _logger;

    public Service(ILogger logger)
    {
        _logger = logger;
    }

    public void DoWork()
    {
        _logger.Log("작업을 수행 중입니다.");
    }
}
```

- **이유**: `ILogger` 인터페이스의 `Log` 메서드는 `Service` 클래스에서 호출되므로, 이 메서드는 `public`이어야 합니다. `private`으로 구현된다면 `Service` 클래스는 로그를 기록할 수 없게 됩니다. 이는 의존성 주입이 실패하는 상황을 초래할 수 있습니다.

#### 3. **웹 API 컨트롤러**

ASP.NET 같은 웹 프레임워크에서 인터페이스는 웹 API 컨트롤러가 제공해야 하는 기능을 정의할 수 있습니다. 각 컨트롤러는 인터페이스를 구현하며, 인터페이스에 정의된 메서드는 웹 클라이언트가 호출할 수 있는 엔드포인트가 됩니다.

```csharp
public interface IWeatherService
{
    string GetWeatherForecast();
}

public class WeatherController : IWeatherService
{
    public string GetWeatherForecast()
    {
        return "맑음";
    }
}
```

- **이유**: `WeatherController` 클래스의 `GetWeatherForecast` 메서드는 웹 API의 엔드포인트로 외부 클라이언트가 호출할 수 있어야 합니다. 만약 이 메서드가 `private`이라면, 클라이언트는 이 엔드포인트에 접근할 수 없게 되어 API의 목적이 상실됩니다.

### 요약

- **플러그인 아키텍처**: 플러그인 시스템에서 인터페이스를 통해 정의된 메서드는 외부에서 호출 가능해야 플러그인이 올바르게 동작합니다.
- **의존성 주입**: 의존성 주입 패턴에서 인터페이스의 메서드는 주입받은 클래스에서 호출 가능해야 하므로 `public`이어야 합니다.
- **웹 API 컨트롤러**: 웹 API에서 인터페이스를 통해 정의된 메서드는 클라이언트가 접근할 수 있어야 하므로 `public`이어야 합니다.

이러한 실무 사례를 통해 인터페이스 메서드를 `public`으로 구현해야 하는 이유를 이해할 수 있습니다. 인터페이스는 외부에서 접근 가능한 계약을 정의하며, 이를 준수하지 않으면 시스템의 핵심 기능이 제대로 동작하지 않을 수 있습니다.


