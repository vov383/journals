---
title: Visual Studio의 CSPROJ 파일
created: 2024-06-19 08:14
alias:
tags:
---
#### CSPROJ 파일이란?
Visual Studio에서 
.NET 애플리케이션을 위한 XML 기반 프로젝트 파일입니다. 
이 파일은 프로젝트의 구조와 설정 정보를 포함하고 있으며, 
라이브러리 참조, 빌드 옵션, 구성 세부 정보 등을 담고 있습니다.

#### CSPROJ 파일의 구조
CSPROJ 파일은 일반적으로 다음과 같은 섹션으로 구성됩니다:

#### 프로젝트 요소 (Project Element)
- 모든 다른 요소를 포함하는 루트 요소입니다.
- 예시: `<Project Sdk="Microsoft.NET.Sdk">`

#### 속성 그룹 (PropertyGroup)
- 프로젝트의 속성을 정의하는 섹션입니다. 
- 여기에는 타겟 프레임워크, 출력 형식, 버전 정보 등이 포함됩니다.
- 예시: 
```xml
<PropertyGroup>
  <OutputType>Exe</OutputType>
  <TargetFramework>net5.0</TargetFramework>
</PropertyGroup>
```

#### 아이템 그룹 (ItemGroup)
- 프로젝트에 포함된 파일과 참조를 정의하는 섹션입니다. 
- 컴파일할 파일, 포함할 리소스 파일, 패키지 참조 등을 나열합니다.
- 예시: 
```xml
<ItemGroup>
  <Compile Include="Program.cs" />
  <PackageReference Include="Newtonsoft.Json" Version="12.0.3" />
</ItemGroup>
```

#### Import 요소 (Import Element)
- 다른 파일을 가져와서 포함시킵니다. 
- 주로 공통 속성 파일이나 타겟 파일을 포함하는 데 사용됩니다.
- 예시: 
```xml
<Import Project="..\common.props" />
```

### CSPROJ 파일 예시
```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <OutputType>Exe</OutputType>
    <TargetFramework>net5.0</TargetFramework>
  </PropertyGroup>

  <ItemGroup>
    <Compile Include="Program.cs" />
    <PackageReference Include="Newtonsoft.Json" Version="12.0.3" />
  </ItemGroup>

</Project>
```

#### 요약
- CSPROJ 파일은 프로젝트의 구조와 설정 정보를 포함합니다.
- 주요 섹션은 Project, PropertyGroup, ItemGroup, Import입니다.
- XML 형식으로 작성되어 있으며, Visual Studio가 이를 해석하여 프로젝트를 빌드합니다.


