---
title: DOTween Sequence in Unity
created: 2025-01-02 03:22
alias:
tags:
---
## 기본 개념
DOTween의 Sequence는 여러 트윈 애니메이션을 조합하고 제어하는 기능을 제공합니다.

## 시퀀스 생성
```csharp
Sequence sequence = DOTween.Sequence();
```

## 주요 메서드

### 1. Append
```csharp
sequence.Append(transform.DOMove(target, duration));
```
- 이전 동작이 완료된 후 실행
- 순차적 실행이 필요할 때 사용

### 2. Join
```csharp
sequence.Join(transform.DOScale(newScale, duration));
```
- 이전 동작과 동시에 실행
- 병렬 실행이 필요할 때 사용

### 3. PrependInterval & AppendInterval
```csharp
sequence.PrependInterval(1f);  // 시작 전 대기
sequence.AppendInterval(1f);   // 완료 후 대기
```
- 시간 간격 추가

### 4. 이벤트 콜백
```csharp
sequence.OnStart(() => { /* 시작 시 실행 */ });
sequence.OnComplete(() => { /* 완료 시 실행 */ });
sequence.OnUpdate(() => { /* 매 프레임 실행 */ });
```

## 시퀀스 제어
```csharp
// 실행 제어
sequence.Play();      // 시작
sequence.Pause();     // 일시정지
sequence.Kill();      // 중지 및 삭제

// 반복 설정
sequence.SetLoops(3); // 3회 반복
sequence.SetLoops(-1); // 무한 반복
```

## 예시 코드
```csharp
Sequence sequence = DOTween.Sequence();

// 이동과 회전을 동시에
sequence.Append(transform.DOMove(targetPos, 1f))
        .Join(transform.DORotate(targetRot, 1f))
        // 1초 대기
        .AppendInterval(1f)
        // 크기 변경
        .Append(transform.DOScale(targetScale, 0.5f))
        // 완료 시 콜백
        .OnComplete(() => Debug.Log("시퀀스 완료"));
```

## 자주 사용되는 Ease 타입
```csharp
SetEase(Ease.InOutQuad)   // 부드러운 가속/감속
SetEase(Ease.Linear)      // 일정한 속도
SetEase(Ease.InOutBack)   // 약간의 반동
SetEase(Ease.OutBounce)   // 통통 튀는 효과
```

## 주의사항
- Kill()을 호출하지 않으면 메모리 누수 가능
- Scene 전환 시 실행 중인 시퀀스 정리 필요
- 너무 많은 시퀀스는 성능에 영향을 줄 수 있음

## 활용 예
1. UI 애니메이션
2. 카메라 움직임
3. 캐릭터 동작
4. 게임 오브젝트 변형
5. 복잡한 애니메이션 시퀀스


