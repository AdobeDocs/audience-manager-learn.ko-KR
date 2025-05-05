---
title: 추적 서버에서 보고서 세트 수준의 서버측 전달로 마이그레이션
description: Adobe Analytics 데이터의 서버측 전달을 Audience Manager 서버 수준이 아닌 보고서 세트 수준에서 추적하는 방법에 대해 알아봅니다.
product: audience manager
feature: Adobe Analytics Integration
topics: null
activity: implement
doc-type: technical video
team: Technical Marketing
kt: 1776
role: Developer, Data Engineer
level: Intermediate
exl-id: 08b81e52-a28a-43e4-a284-df2460a43016
source-git-commit: 4adaade180545bcf5f911b7453a7e9939e2ed178
workflow-type: tm+mt
source-wordcount: '582'
ht-degree: 0%

---

# 추적 서버에서 보고서 세트 수준의 서버측 전달로 마이그레이션 {#migrating-from-tracking-server-to-report-suite-level-server-side-forwarding}

이 문서와 비디오에서는 [!DNL Analytics] 데이터의 서버측 전달을 사용하여 [!UICONTROL tracking server] 수준이 아닌 [!UICONTROL report suite] 수준에서 Audience Manager을 수행하는 방법을 보여 줍니다.

## 소개 {#introduction}

Adobe Audience Manager 및 Adobe Analytics이 있는 경우 [!DNL Analytics] 데이터의 서버측 전달을 Audience Manager에 구현할 수 있습니다. 즉, 페이지에서 히트를 두 개(하나는 [!DNL Analytics]에, 하나는 Audience Manager에) 보내는 대신 히트를 [!DNL Analytics]에 보낼 수 있으며 [!DNL Analytics]에서 해당 데이터를 Audience Manager에 전달합니다.

이미 이 기능을 실행 중이고 2017년 10월 이전에 활성화/구현한 경우 서버측 전달은 Adobe 고객 지원 센터 또는 Adobe Consulting에서 활성화해야 하는 [!UICONTROL Tracking Server]을(를) 기반으로 할 수 있습니다. 2017년 10월부터 직접 서버측 전달을 구성하고 보고서 세트 수준에서 수행할 수 있습니다(보고서 세트당 전달). 이에 대한 상당한 이점이 있는데, 이에 대해서는 아래에서 살펴본다.

## [!UICONTROL Tracking server] 전달 {#tracking-server-forwarding}

[!UICONTROL tracking server]은(는) [!DNL Analytics] 데이터를 보내는 위치이며 이미지 요청 및 쿠키가 작성된 도메인입니다. DTM 또는 [!DNL Experience Platform Launch] 또는 [!DNL AppMeasurement.js] 파일에서 설정해야 하며 일반적으로 다음과 같이 표시되며 사이트 또는 비즈니스 이름이 &quot;mysite&quot;를 대체합니다.

`s.trackingServer = "mysite.sc.omtrdc.net";`

서버측 전달이 [!UICONTROL tracking server] 수준에서 전달하도록 설정되어 있는 경우, 이 [!UICONTROL tracking server] (Experience Cloud ID 서비스 또한 사용하도록 설정된 경우)로 전송되는 모든 히트가 Audience Manager으로 전달됩니다. 이는 Adobe 고객 지원 센터 또는 Adobe Consulting에서 활성화해야 합니다. 또한 아래 설명된 대로 [!UICONTROL report suite] 전달로 전환한 후 이를 비활성화할 수 있습니다.

[!DNL tracking server forwarding]이(가) 활성화되어 있는지 확실하지 않은 경우 Adobe 고객 지원 센터 또는 Adobe Consulting에 연락하면 알려 줄 수 있습니다.

## [!UICONTROL Report-suite] 수준 서버측 전달 {#report-suite-level-server-side-forwarding}

[!UICONTROL tracking server] 전달에서 [!UICONTROL report suite] 전달로 이동하는 가장 큰 이점 중 하나는 이제 &quot;Audience Analytics&quot;를 사용할 수 있다는 것입니다. 이 기능은 자세한 세그먼트 분석을 위해 Audience Manager [!UICONTROL segments]을(를) Adobe Analytics으로 다시 전달하는 기능입니다. [!UICONTROL report suite] 전달이 아닌 [!UICONTROL tracking server] 전달을 사용하는 경우에는 이 기능이 지원되지 않습니다. Audience Analytics에 대한 자세한 내용은 [설명서](https://experienceleague.adobe.com/docs/analytics/integration/audience-analytics/mc-audiences-aam.html?lang=ko)를 참조하세요.

>[!VIDEO](https://video.tv.adobe.com/v/23701/?quality=12)

## 중요한 팁 {#additional-resources}

위의 비디오에 설명된 대로 Audience Manager에게 전달할 모든 [!UICONTROL report suites]을(를) 전달한 후에는 Adobe 고객 지원 센터 또는 Adobe Consulting에 연락하여 [!UICONTROL tracking server] 전달을 비활성화하도록 해야 합니다. [!UICONTROL tracking server] 전달과 [!UICONTROL report suite] 전달을 모두 가지면 히트가 중복되지 않으므로 이 작업을 수행하는 것은 긴급하지 않습니다. 그러나 [!UICONTROL report suite] 전달만 사용하는 것이 좋습니다.

[!UICONTROL tracking server] 전달을 켜두면 전달하지 않으려는 [!UICONTROL report suites]의 데이터를 전달할 수 있을 뿐만 아니라, 나중에 사용자(및 회사의 모든 사용자)가 [!UICONTROL tracking server] 전달이 켜져 있다는 것을 잊어버린 후 특정 [!UICONTROL report suite]에 대해 데이터가 전달되지 않는다고 생각할 수 있습니다. 이는 보고서 세트 수준에서 설정되어 있지 않지만 [!UICONTROL tracking server] 때문에 데이터가 계속 전달되기 때문입니다. 그러면 왜 전달인지 파악하고 예상하지 못한 AAM 서버 호출에 대해서도 요금을 지불하면서 시간과 비용을 낭비하게 됩니다. 따라서 비즈니스 요구 사항에 맞게 모든 [!UICONTROL report suites]을(를) 전달하도록 설정하는 즉시 [!UICONTROL tracking server] 전달을 비활성화하는 것이 좋습니다.
