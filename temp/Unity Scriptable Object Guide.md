---
title: Unity Scriptable Object Guide
created: 2024-12-24 11:29
alias:
tags:
---
## 개요
Scriptable Object는 Unity에서 제공하는 데이터 컨테이너로, 프로젝트의 데이터를 효율적으로 관리하고 저장할 수 있게 해주는 에셋 타입입니다.

## 특징
- 메모리 효율성: 데이터를 한 번만 메모리에 로드
- 재사용성: 여러 오브젝트에서 동일한 데이터 참조 가능
- 직렬화: Unity 에디터에서 데이터 수정 및 저장 가능
- 프리팹/씬 독립성: 데이터를 독립적으로 관리

## 기본 구현
```csharp
[CreateAssetMenu(fileName = "NewData", menuName = "ScriptableObjects/DataObject")]
public class DataObject : ScriptableObject
{
    public string itemName;
    public int value;
    public float multiplier;
}
```

## 주요 사용 사례
1. 게임 데이터 관리
   - 아이템 데이터베이스
   - 캐릭터 스탯
   - 스킬 시스템
   - 퀘스트 정보

2. 설정 관리
   - 게임 설정
   - 난이도 설정
   - 사운드 설정

3. 이벤트 시스템
   - 게임 이벤트
   - 상태 관리
   - 알림 시스템

## 사용 방법

### 1. 생성
```csharp
// Unity 에디터에서:
// 1. Project 창에서 우클릭
// 2. Create > ScriptableObjects > DataObject
```

### 2. 참조 및 사용
```csharp
public class DataUser : MonoBehaviour
{
    public DataObject data; // Inspector에서 할당

    void UseData()
    {
        Debug.Log(data.itemName);
    }
}
```

## 장점
- 데이터와 로직의 분리
- 프로젝트 구조 개선
- 메모리 사용 최적화
- 에디터 지원으로 쉬운 데이터 관리
- 버전 관리 용이

## 주의사항
- 런타임 중 데이터 수정 시 모든 참조에 영향
- 기본값으로 복원이 필요한 경우 별도 처리 필요
- 대용량 데이터의 경우 로딩 시간 고려

## 활용 팁
1. 데이터 컨테이너로 사용
```csharp
[CreateAssetMenu]
public class GameDatabase : ScriptableObject
{
    public List<ItemData> items;
    public Dictionary<int, LevelData> levels;
}
```

2. 이벤트 시스템 구현
```csharp
[CreateAssetMenu]
public class GameEvent : ScriptableObject
{
    private List<GameEventListener> listeners = new List<GameEventListener>();
    
    public void Raise()
    {
        foreach(var listener in listeners)
        {
            listener.OnEventRaised();
        }
    }
}
```

3. 설정 관리
```csharp
[CreateAssetMenu]
public class GameSettings : ScriptableObject
{
    public float musicVolume;
    public float sfxVolume;
    public int difficulty;
}
```

## 결론
Scriptable Object는 Unity 프로젝트의 데이터 관리를 위한 강력한 도구입니다. 적절히 활용하면 코드 구조 개선과 성능 최적화를 동시에 달성할 수 있습니다.


