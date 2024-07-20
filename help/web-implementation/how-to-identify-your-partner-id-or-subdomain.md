---
title: 파트너 ID 또는 하위 도메인을 식별하는 방법
description: 일부 Experience Cloud 기능을 구현할 때 파트너 ID 또는 하위 도메인을 식별하는 방법에 대해 알아보고, Audience Manager UI에서 이 ID를 가져올 수 있는 두 가지 위치에 대해 알아봅니다.
feature: Implementation Basics
topics: null
activity: implement
doc-type: technical video
team: Technical Marketing
kt: 2359
role: Developer, Data Engineer
level: Intermediate
exl-id: d3f4a12d-acc5-47b7-a38a-a6a14152bf3a
source-git-commit: 62b43b5627dabf754cf821f974a56c60989ef7ef
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 0%

---

# Audience Manager 하위 도메인을 식별하는 방법 {#how-to-identify-your-audience-manager-partner-id-or-subdomain}

일부 Experience Cloud 기능을 구현할 때는 Audience Manager `Subdomain`이(가) 무엇인지 알고 있어야 합니다(`client ID` 또는 `Partner ID`이라고도 함). 이 비디오에서는 Audience Manager UI에서 이 정보를 가져올 수 있는 두 위치를 보여 줍니다.

## 결말을 퍼붓는 중... {#giving-away-the-ending}

이 짧은 비디오를 시청하지 않고 바로 들어가서 찾는 것이 나을 경우 UI의 두 위치에서 `Partner Subdomain`을(를) 찾을 수 있습니다.

1. [!UICONTROL rule-based] 트레이트를 이미 만든 경우 **[!UICONTROL Get Trait URL]**을(를) 클릭합니다.
   [!UICONTROL Get Trait URL]은(는) 해당 폴더의 특성 목록에서 특성 옆에 있으며 URL에 하위 도메인이 포함됩니다.
1. **[!UICONTROL Tools]** > **[!UICONTROL Tags]** 인터페이스로 이동하여 컨테이너에 대해 **[!UICONTROL Get code]**&#x200B;을(를) 클릭하면 하위 도메인이 Akamai 줄의 끝으로 이동합니다.

이러한 빠른 참조로 빠르게 찾을 수 없는 경우 이 비디오는 짧은 시간 약속입니다. :)

>[!VIDEO](https://video.tv.adobe.com/v/25922/?quality=12)

>[!IMPORTANT]
>
>Adobe Experience Cloud의 각 고객에게 할당된 숫자 ID가 있으며 이를 종종 &quot;PID&quot; 또는 파트너 ID라고도 합니다. 이 문서와 비디오에서 이야기하는 ID는 아닙니다. 대신, 파트너 ID라고도 하는 &quot;파트너 하위 도메인&quot;은 일반적으로 클라이언트 이름의 버전이며 데이터가 전송되는 서버의 하위 도메인입니다. 예를 들어 회사가 &quot;Bob의 Knobs&quot;(모든 사물함 문고리, 물론 하하)인 경우 파트너 하위 도메인은 &quot;bobsknobs&quot;이지만 &quot;PID&quot;는 &quot;12345&quot;과 같을 수 있습니다. 일반적으로 PID를 알 필요는 없지만 Audience Manager 구현을 구성할 수 있도록 하위 도메인을 아는 것이 중요합니다.
>
