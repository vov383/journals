---
title: Unity의 Scene 뷰 툴바
created: 2024-12-12 04:29
alias:
tags:
---
Unity에서 작업 환경을 효율적으로 설정하는 중요한 도구입니다. 
특히 툴바의 각 옵션은 작업 중 시각적인 참고나 디버깅에 도움을 줄 수 있지만, 의도치 않게 작업 환경을 복잡하게 만들 수도 있습니다. 
간단히 씬 뷰 툴바의 주요 기능을 정리


### 씬 뷰 툴바 주요 기능

#### 1. **Skybox**

- 씬 뷰에서 **스카이박스(Skybox)**를 보여줄지 여부를 설정합니다.
- 끄면 단색 배경으로 변경되어 작업 환경이 단순해집니다.

#### 2. **Fog**

- 씬 뷰에서 안개 효과(Fog)를 활성화하거나 비활성화합니다.
- Fog는 거리에 따라 물체가 흐릿해지는 효과로, 환경 분위기 조정에 유용합니다.

#### 3. **Flares**

- 렌즈 플레어 효과를 활성화/비활성화합니다.
- 조명 또는 빛나는 물체에서 빛이 반사되는 효과를 보여줍니다.

#### 4. **Post Processing**

- 게임 뷰에서 설정된 Post-Processing Volume의 효과를 씬 뷰에서 보여줍니다.
- 활성화하면 Bloom, Depth of Field 등의 효과를 미리 볼 수 있으나, 비활성화하면 씬 뷰에서 후처리 효과를 제거해 작업을 간소화할 수 있습니다.

#### 5. **Always Refresh**

- 씬 뷰를 항상 업데이트하도록 설정합니다.
- 끄면 성능을 절약할 수 있지만, 실시간 미리 보기가 제한됩니다.

#### 6. **Particle Systems**

- 씬 뷰에서 파티클 효과(예: 불꽃, 연기)를 렌더링합니다.
- 비활성화하면 파티클을 보지 않고 작업할 수 있습니다.

#### 7. **Visual Effect Graphs**

- Visual Effect Graphs를 사용하는 경우, 이 옵션을 통해 씬 뷰에서 해당 효과를 확인할 수 있습니다.


### 씬 뷰 툴바로 인한 문제 방지

1. **필요한 기능만 활성화**:
    
    - 작업에 필요하지 않은 옵션은 끄고, 성능 부하를 줄이세요.
    - 특히 Post-Processing, Particle Systems는 자주 확인하지 않는 한 비활성화 상태로 두는 것이 좋습니다.
2. **문제 발생 시 옵션 점검**:
    
    - 이상 현상이 보이면 툴바에서 관련 옵션(Post-Processing, Flares 등)을 하나씩 끄고 테스트해 보세요.
3. **툴바 옵션 익히기**:
    
    - 옵션마다 켜고 끄는 효과를 직접 테스트해 보면 기능을 더 잘 이해할 수 있습니다.


