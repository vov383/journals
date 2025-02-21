---
title: 부동소수점(Floating Point) 개념
created: 2025-02-20 09:48
alias:
tags:
---
#### 부동소수점이란?
소수점을 기준으로 숫자의 위치가 변동될 수 있는 표현 방식
이는 매우 큰 숫자나 매우 작은 숫자를 표현할 때 유용함.
컴퓨터 시스템에서 부동소수점은 실수를 표현하는 표준 방식

#### 부동소수점 표현 방식

부동소수점 숫자는 기본적으로 다음과 같은 형태로 표현됩니다:
$[\text{숫자} = \text{유효숫자} \times \text{기수}^{\text{지수}}]$

- **유효숫자 (Significand/Mantissa)**: 숫자의 중요한 부분으로, 소수점 이하의 숫자를 포함합니다.
- **기수 (Base/Radix)**: 숫자 체계의 기준, 일반적으로 2진수(기수 2)로 사용됩니다.
- **지수 (Exponent)**: 유효숫자가 기수의 몇 제곱인지 나타냅니다.

예를 들어, 123.45를 부동소수점으로 표현하면:
$[ 123.45 = 1.2345 \times 10^2 ]$

컴퓨터에서는 주로 2진수로 표현하므로, 다음과 같이 나타낼 수 있습니다:
$[ 1101.11_2 = 1.10111 \times 2^3 ]$

#### IEEE 754 표준

부동소수점 숫자는 IEEE 754 표준에 따라 표현됩니다. 
이 표준은 부동소수점을 저장하고 계산하는 방식을 정의합니다. 
주요 포맷으로는 
	단정밀도(Single Precision)와 
	배정밀도(Double Precision)가 있습니다.

###### 단정밀도 (Single Precision)
32비트로 구성되며, 
1비트는 부호, 
8비트는 지수, 
23비트는 유효숫자로 사용됩니다.


###### 배정밀도 (Double Precision)
64비트로 구성되며, 
1비트는 부호, 
11비트는 지수, 
52비트는 유효숫자로 사용됩니다.

#### 예제: 단정밀도와 배정밀도

단정밀도 예:
$\[ \text{숫자} = -1.011 \times 2^3 \]$

배정밀도 예:
$\[ \text{숫자} = 1.110101 \times 2^{-4} \]$

#### 부동소수점 연산의 문제점

부동소수점 연산에는 몇 가지 문제가 있습니다

###### 정밀도 손실 (Precision Loss)
모든 실수를 정확하게 표현할 수 없으므로 
근사값을 사용하게 됩니다.
###### 오차 누적 (Accumulated Error)
연산을 반복하면 작은 오차들이 누적되어 
큰 오차로 이어질 수 있습니다.
###### 비교의 어려움
근사값을 사용하므로, 
부동소수점 숫자끼리의 정확한 비교가 어려울 수 있습니다.

#### 예제: 부동소수점 오차

```csharp
double a = 0.1;
double b = 0.2;
double c = 0.3;

Console.WriteLine((a + b) == c);  // 출력: False
```

이 예제에서 `a + b`는 `0.3`이 아니며, 
이는 부동소수점 연산의 정밀도 문제로 인한 것입니다.

### 요약

1. **부동소수점**: 실수를 표현하는 방식으로, 소수점의 위치가 변동될 수 있음.
2. **유효숫자, 기수, 지수**: 부동소수점의 기본 구성 요소.
3. **IEEE 754 표준**: 부동소수점 표현을 정의하는 표준, 단정밀도와 배정밀도가 있음.
4. **정밀도 손실**: 부동소수점 연산에서 발생하는 문제.
5. **오차 누적**: 반복 연산으로 인해 작은 오차들이 누적되는 문제.
6. **비교의 어려움**: 부동소수점 숫자끼리의 정확한 비교가 어려움.


### 부동소수점 연산의 정밀도를 개선하기 위한 방법

부동소수점 연산의 정밀도를 개선하기 위한 몇 가지 방법.

#### 1. 고정소수점 연산 (Fixed-point Arithmetic)
고정된 소수점 위치를 사용하여 정밀도를 유지하는 방식입니다. 
특정한 정밀도가 필요한 상황에서 사용됩니다. 
특히, 금융 계산이나 소수점 이하 자릿수의 변동이 없어야 하는 경우에 유용합니다.

**예시:**
```csharp
public struct FixedPoint
{
    private long value;
    private const int SCALE = 10000;

    public FixedPoint(decimal number)
    {
        value = (long)(number * SCALE);
    }

    public decimal ToDecimal()
    {
        return (decimal)value / SCALE;
    }
}
```

#### 2. 다중 정밀도 라이브러리 (Multiple Precision Libraries)
고정된 비트 수를 넘어서는 정밀도가 필요한 경우, 
다중 정밀도 라이브러리를 사용할 수 있습니다. 
예를 들어, .NET에서는 `System.Numerics.BigInteger`나 외부 라이브러리인 `Arbitrary-Precision Arithmetic`을 사용할 수 있습니다.

**예시:**
```csharp
using System.Numerics;

BigInteger a = BigInteger.Parse("123456789012345678901234567890");
BigInteger b = BigInteger.Parse("987654321098765432109876543210");
BigInteger c = a + b;
Console.WriteLine(c);
```

#### 3. 분수 표현 (Fraction Representation)
분수를 사용하여 정밀도를 유지하는 방법입니다. 
분수로 표현하면 정밀도 손실 없이 연산을 수행할 수 있습니다.

**예시:**
```csharp
public struct Fraction
{
    public int Numerator { get; }
    public int Denominator { get; }

    public Fraction(int numerator, int denominator)
    {
        Numerator = numerator;
        Denominator = denominator;
    }

    public Fraction Add(Fraction other)
    {
        return new Fraction(
            this.Numerator * other.Denominator + other.Numerator * this.Denominator,
            this.Denominator * other.Denominator
        );
    }
}
```

#### 4. 정확도 증가 (Increased Precision)
단정밀도(float) 대신 배정밀도(double)를 사용하거나, 
double 대신 소수점 연산을 지원하는 
Decimal을 사용하는 것도 방법입니다. 
Decimal은 특히 금융 계산에 유리합니다.

**예시:**
```csharp
decimal a = 0.1m;
decimal b = 0.2m;
decimal c = 0.3m;

Console.WriteLine((a + b) == c);  // 출력: True
```


### 부동소수점 대신 사용할 수 있는 다른 숫자 표현 방식

부동소수점 대신 사용할 수 있는 다른 숫자 표현 방식에는 다음과 같은 것들이 있습니다:

#### 1. 고정소수점 (Fixed-point)
고정된 위치의 소수점을 사용하여 숫자를 표현합니다. 
주로 소수점 이하의 자릿수가 일정하게 필요한 경우에 사용됩니다.

**사용 사례:**
- 임베디드 시스템
- 금융 계산

#### 2. 분수 (Fraction)
분수 형태로 숫자를 표현하여 정밀도를 유지합니다. 유리수를 표현하는데 적합합니다.

**사용 사례:**
- 계산 정확도가 중요한 수학적 연산
- 기하학적 계산

#### 3. 정수 (Integer)
정수만을 사용하는 방식으로, 필요한 경우 정수로 변환하여 계산합니다. 소수점 이하가 필요 없는 경우에 사용됩니다.

**사용 사례:**
- 카운팅 연산
- 고정 길이의 데이터 처리

#### 4. 다중 정밀도 숫자 (Multiple Precision)
임의의 정밀도를 가지는 숫자를 표현하는 방식으로, 매우 큰 수나 매우 작은 수를 다룰 때 사용됩니다.

**사용 사례:**
- 암호학
- 과학적 계산

### 요약

1. **고정소수점 연산**: 소수점 위치가 고정된 연산으로 정밀도를 유지.
2. **다중 정밀도 라이브러리**: 매우 큰 수나 작은 수를 처리하는 라이브러리.
3. **분수 표현**: 분수를 사용하여 정밀도 손실 없이 연산.
4. **정확도 증가**: float 대신 double, double 대신 decimal 사용.
5. **고정소수점**: 고정된 소수점 위치를 사용하여 정밀도 유지.
6. **분수**: 분수 형태로 숫자를 표현하여 정밀도 유지.
7. **정수**: 정수만을 사용하여 필요한 경우 정수로 변환하여 계산.
8. **다중 정밀도 숫자**: 임의의 정밀도를 가지는 숫자를 표현.


