---
title: AAM으로 데이터를 전송할 때 SPA 페이지에서 모범 사례 사용
description: 단일 페이지 애플리케이션(SPA)에서 Adobe Audience Manager(AAM)로 데이터를 전송하는 모범 사례에 대해 알아봅니다. 이 문서에서는 권장 구현 방식인 Experience Platform 태그 사용에 중점을 둡니다.
feature: Implementation Basics
topics: spa
activity: implement
doc-type: technical video
team: Technical Marketing
kt: 1390
topic: SPA
role: Developer, Data Engineer
level: Experienced
exl-id: 99ec723a-dd56-4355-a29f-bd6d2356b402
source-git-commit: d4874d9f6d7a36bb81ac183eb8b853d893822ae0
workflow-type: tm+mt
source-wordcount: '547'
ht-degree: 0%

---

# AAM으로 데이터를 전송할 때 SPA 페이지에서 모범 사례 사용 {#using-best-practices-on-spa-pages-when-sending-data-to-aam}

이 문서에서는 단일 페이지 애플리케이션(SPA)에서 Adobe Audience Manager(AAM)로 데이터를 전송하는 몇 가지 모범 사례에 대해 설명합니다. 이 문서에서는 권장 구현 방식인 [!UICONTROL Experience Platform tags]을(를) 사용하는 데 중점을 둡니다.

## 초기 참고 사항

* 아래 항목은 Platform 태그를 사용하여 사이트에서 구현하고 있다고 가정합니다. Platform 태그를 사용하지 않는 경우에도 고려 사항은 여전히 존재하지만, 이를 구현 방식에 맞게 조정해야 합니다.
* 모든 SPA가 다르므로 요구 사항을 가장 잘 충족하기 위해 다음 항목 중 일부를 수정해야 할 수 있지만, Adobe은 SPA 페이지에서 Audience Manager으로 데이터를 전송할 때 고려해야 할 몇 가지 모범 사례를 공유하려고 합니다.

## Experience Platform 태그(이전의 Launch)의 SPA 및 AAM 작업에 대한 간단한 다이어그램{#simple-diagram-of-working-with-spas-and-aam-in-experience-platform-launch}

태그의 aam용 ![spa](assets/spa_for_aam_in_launch.png)

>[!NOTE]
>설명된 대로, 이는 Platform 태그를 사용하여 Adobe Audience Manager 구현(Adobe Analytics 없음)에서 SPA 페이지를 처리하는 방법에 대한 간단한 다이어그램입니다. 보다시피 이것은 매우 솔직하며, 보기 변경(또는 작업)을 Platform 태그에 전달하는 방식이 가장 큽니다.

## SPA 페이지에서 태그 트리거 {#triggering-launch-from-the-spa-page}

Platform 태그에서 규칙을 트리거하여 데이터를 Audience Manager으로 전송하는 두 가지 일반적인 방법은 다음과 같습니다.

* JavaScript 사용자 지정 이벤트 설정(Adobe Analytics을 사용한 [여기](https://helpx.adobe.com/analytics/kt/using/spa-analytics-best-practices-feature-video-use.html) 예 참조)
* [!UICONTROL Direct Call Rule] 사용

이 Audience Manager 예제에서는 Platform 태그의 [!UICONTROL Direct Call rule]을(를) 사용하여 Audience Manager으로 이동하는 히트를 트리거합니다. 다음 절에서 볼 수 있듯이 이 기능은 [!UICONTROL Data Layer]을(를) 새 값으로 설정하여 Platform 태그의 [!UICONTROL Data Element]에서 선택할 수 있도록 하는 데 유용합니다.

## 데모 페이지 {#demo-page}

다음은 SPA 페이지에서 수행할 수 있는 것처럼 데이터 레이어에서 값을 변경하여 Audience Manager으로 전송하는 방법을 보여 주는 작은 페이지입니다. 이 기능은 필요한 보다 정교한 변경 사항에 대해 모델링할 수 있습니다. 이 데모 페이지는 [여기](https://aam.enablementadobe.com/SPA-Launch.html)에서 찾을 수 있습니다.

## 데이터 레이어 설정 {#setting-the-data-layer}

위에서 언급했듯이 페이지에 새 콘텐츠를 로드할 때 또는 사이트에서 작업을 수행할 때 플랫폼 태그가 호출되어 [!UICONTROL rules]을(를) 실행하기 전에 데이터 레이어를 페이지의 헤드에 동적으로 설정해야 합니다. 그러면 플랫폼 태그가 데이터 레이어에서 새 값을 선택하여 Audience Manager으로 푸시할 수 있습니다.

위에 나열된 데모 사이트로 이동하여 페이지 소스를 살펴보면 다음과 같이 표시됩니다.

* 데이터 레이어는 Platform 태그 호출 전 페이지의 헤드에 있습니다.
* 시뮬레이션된 SPA 링크의 JavaScript이 [!UICONTROL Data Layer]을(를) 변경한 다음 플랫폼 태그(`_satellite.track()` 호출)를 호출합니다. 이 [!UICONTROL Direct Call Rule] 대신 JavaScript 사용자 지정 이벤트를 사용하는 경우 단원은 동일합니다. 먼저 [!DNL data layer]을(를) 변경한 다음 Platform 태그를 호출합니다.

>[!VIDEO](https://video.tv.adobe.com/v/23322/?quality=12)

## 추가 리소스 {#additional-resources}

* [Adobe 포럼의 SPA 토론](https://forums.adobe.com/thread/2451022)
* [플랫폼 태그에서 SPA를 구현하는 방법을 보여 주는 참조 아키텍처 사이트](https://helpx.adobe.com/experience-manager/kt/integration/using/launch-reference-architecture-SPA-tutorial-implement.html)
* [Adobe Analytics에서 SPA를 추적할 때 모범 사례 사용](https://helpx.adobe.com/analytics/kt/using/spa-analytics-best-practices-feature-video-use.html)
* [이 문서에 사용되는 데모 사이트](https://aam.enablementadobe.com/SPA-Launch.html)
