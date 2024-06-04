---
title: ExecuteNonQuery 메서드
created: 2024-06-04 09:54
alias:
tags:
---
데이터베이스에 대한 `INSERT`, `UPDATE`, `DELETE` 등의 명령을 실행하고, 
실행된 명령으로 인해 영향을 받은 행(row)의 수를 반환하는 메서드입니다. 
아래는 제공된 `ExecuteNonQuery` 메서드의 설명입니다.

#### 메서드 구조

```csharp
public override int ExecuteNonQuery()
{
    int returnValue = -1;

    // 1. 명령 인터셉터가 있고 ExecuteNonQuery가 성공하면 returnValue 반환
    if (connection?.commandInterceptor != null && connection.commandInterceptor.ExecuteNonQuery(CommandText, ref returnValue))
    {
        return returnValue;
    }

    // 2. MySqlDataReader 사용하여 ExecuteReader 호출 후 데이터 리더 닫기
    using MySqlDataReader mySqlDataReader = ExecuteReader();
    mySqlDataReader.Close();

    // 3. RecordsAffected 값을 반환
    return mySqlDataReader.RecordsAffected;
}
```

#### 단계별 설명

###### 1. 명령 인터셉터 확인 및 실행

```csharp
if (connection?.commandInterceptor != null && connection.commandInterceptor.ExecuteNonQuery(CommandText, ref returnValue))
{
    return returnValue;
}
```

- `connection` 객체와 `commandInterceptor`가 null이 아닌지 확인합니다.
- `commandInterceptor.ExecuteNonQuery` 메서드를 호출하여 `CommandText`를 실행하고, `returnValue`에 결과를 저장합니다.
- `ExecuteNonQuery`가 성공하면 `returnValue`를 반환합니다.

명령 인터셉터는 데이터베이스 명령의 실행을 가로채고, 
필요한 경우 다른 처리를 수행하거나 
실행을 수정할 수 있는 기능을 제공합니다.

###### 2. 데이터 리더를 사용하여 명령 실행

```csharp
using MySqlDataReader mySqlDataReader = ExecuteReader();
mySqlDataReader.Close();
```

- `ExecuteReader` 메서드를 호출하여 `MySqlDataReader` 객체를 생성합니다.
- 데이터 리더를 사용하여 명령을 실행하고, `RecordsAffected` 값을 얻기 위해 데이터를 읽습니다.
- 데이터를 다 읽은 후 데이터 리더를 닫습니다.

###### 3. 영향을 받은 행 수 반환

```csharp
return mySqlDataReader.RecordsAffected;
```

- `mySqlDataReader.RecordsAffected` 값을 반환합니다. 
- 이는 실행된 명령으로 인해 영향을 받은 행의 수를 나타냅니다.

### 요약

- **명령 인터셉터 사용**: 명령 인터셉터가 있으면 이를 사용하여 명령을 실행하고 결과를 반환합니다.
- **데이터 리더 사용**: `ExecuteReader` 메서드를 사용하여 명령을 실행하고, 데이터를 읽은 후 닫습니다.
- **영향 받은 행 수 반환**: 명령이 성공적으로 실행되면 영향을 받은 행의 수를 반환합니다.

### 주요 포인트 요약

###### 명령 인터셉터
- 명령 인터셉터가 존재하면 이를 사용하여 명령을 실행합니다.
- 인터셉터는 명령 실행을 수정하거나 추가 처리를 할 수 있습니다.

###### 데이터 리더 사용
- `ExecuteReader`를 사용하여 명령을 실행하고 데이터를 읽습니다.
- 데이터 리더는 실행된 명령의 영향을 받은 행 수를 제공합니다.

###### 반환 값
- 영향을 받은 행의 수를 반환하여 `INSERT`, `UPDATE`, `DELETE` 명령의 결과를 나타냅니다.

Q1: 명령 인터셉터는 어떤 상황에서 유용하게 사용될 수 있을까요?
Q2: `ExecuteNonQuery` 메서드와 `ExecuteReader` 메서드의 차이점은 무엇인가요?


### 명령 인터셉터의 유용성

명령 인터셉터는 
데이터베이스 명령을 실행하기 전후에 추가적인 로직을 수행하거나 
명령의 실행을 수정하는 데 매우 유용합니다. 

다음과 같은 상황에서 특히 유용하게 사용될 수 있습니다:
###### 로깅 및 감사
- 데이터베이스 명령의 실행 전후에 로깅을 수행하여 
- 누가, 언제, 어떤 명령을 실행했는지 추적할 수 있습니다.
- 감사 기록을 유지하여 보안 및 규정 준수를 보장할 수 있습니다.

###### 성능 모니터링
- 명령의 실행 시간을 측정하여 성능 병목 현상을 파악할 수 있습니다.
- 자주 실행되는 쿼리의 성능을 분석하고 최적화할 수 있습니다.

###### 보안
- 실행될 명령을 검사하여 SQL 인젝션 등의 공격을 방지할 수 있습니다.
- 특정 사용자나 역할에 대한 명령 실행을 제한할 수 있습니다.

###### 변경 관리
- 명령 실행 전후에 데이터를 변경하거나 수정할 수 있습니다.
- 예를 들어, 특정 조건을 만족하는 경우 명령을 수정하거나 추가적인 명령을 실행할 수 있습니다.

###### 에러 처리 및 복구
- 명령 실행 중 발생할 수 있는 오류를 가로채고 
- 적절히 처리할 수 있습니다.
- 실패한 명령에 대해 복구 절차를 수행할 수 있습니다.

### `ExecuteNonQuery`와 `ExecuteReader`의 차이점

#### Q2: `ExecuteNonQuery` 메서드와 `ExecuteReader` 메서드의 차이점은 무엇인가요?

`ExecuteNonQuery`와 `ExecuteReader`는 각각 다른 목적을 가지고 있는 데이터베이스 명령 실행 메서드입니다. 아래는 두 메서드의 주요 차이점입니다:

###### `ExecuteNonQuery`

- **주요 목적**: 데이터베이스에 대한 `INSERT`, `UPDATE`, `DELETE` 명령과 같은 데이터 조작 언어(DML) 명령을 실행합니다.
- **반환 값**: 명령의 실행으로 인해 영향을 받은 행(row)의 수를 반환합니다. 예를 들어, 3개의 행이 업데이트되었다면 `3`을 반환합니다.
- **사용 예시**:
  ```csharp
  string insertSql = "INSERT INTO Customers (Name, Age) VALUES ('John Doe', 30)";
  int rowsAffected = command.ExecuteNonQuery();
  ```

###### `ExecuteReader`

- **주요 목적**: 데이터베이스에서 데이터를 검색하기 위한 `SELECT` 명령을 실행합니다.
- **반환 값**: `MySqlDataReader` 객체를 반환하며, 이 객체를 사용하여 결과 집합을 순회하고 읽을 수 있습니다.
- **사용 예시**:
  ```csharp
  string selectSql = "SELECT Name, Age FROM Customers";
  using (MySqlDataReader reader = command.ExecuteReader())
  {
      while (reader.Read())
      {
          string name = reader.GetString(0);
          int age = reader.GetInt32(1);
          // 데이터를 처리
      }
  }
  ```

### 요약

###### 명령 인터셉터

- 로깅, 성능 모니터링, 보안, 변경 관리, 에러 처리 및 복구에 유용합니다.
- 데이터베이스 명령의 실행 전후에 추가적인 로직을 수행하거나 명령을 수정할 수 있습니다.

###### `ExecuteNonQuery` 메서드

- 데이터 조작 언어(DML) 명령(`INSERT`, `UPDATE`, `DELETE`)을 실행합니다.
- 영향을 받은 행(row)의 수를 반환합니다.

###### `ExecuteReader` 메서드

- 데이터 검색을 위한 `SELECT` 명령을 실행합니다.
- `MySqlDataReader` 객체를 반환하여 결과 집합을 읽을 수 있습니다.

Q1: 명령 인터셉터를 사용할 때 발생할 수 있는 잠재적인 문제점은 무엇인가요?
Q2: `ExecuteNonQuery` 메서드와 `ExecuteReader` 메서드를 함께 사용해야 하는 상황은 어떤 경우일까요?
