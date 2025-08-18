---
title: 알고리즘(유사) 모델을 사용하여 ROAS 증가
description: Audience Manager 유사 모델링의 진정한 힘은 세컨드 및 서드파티 데이터 소스의 새로운 고급 사용자 세트에 대해 기준선 대상자를 확장하려고 할 때 나옵니다. 이 자습서에서는 이 데이터에서 모델을 만드는 단계를 알아봅니다.
feature: Algorithmic Models
topics: null
activity: use
doc-type: feature video
team: Technical Marketing
thumbnail: 25188.jpg
kt: 1849
role: User, Developer, Data Engineer, Architect, Data Architect, Admin, Leader
level: Intermediate
exl-id: 6626ae11-8709-4302-9e03-0d55878d2409
source-git-commit: 2094d3bcf658913171afa848e4228653c71c41de
workflow-type: tm+mt
source-wordcount: '896'
ht-degree: 0%

---

# Audience Manager에서 알고리즘(유사) 모델을 사용하여 ROAS 증가 {#increase-roas-by-using-algorithmic-look-alike-models-in-audience-manager}

Audience Manager 유사 [!UICONTROL Modeling]의 진정한 장점은 타사 및 타사 데이터 소스의 새로운 고급 사용자 집합에 대해 기본 대상을 확장하려고 할 때 발생합니다. 이 자습서에서는 이 데이터에서 모델을 만드는 데 필요한 단계에 대해 알아봅니다.

## Audience Marketplace에서 서드파티 또는 서드파티 데이터 스트림 활성화 {#enable-2nd-or-3rd-party-data-streams-from-the-audience-marketplace}

유사 모델에서 서드파티 및 서드파티 데이터를 사용하려면 먼저 이 데이터를 Audience Manager 인터페이스에 활성화해야 합니다. Adobe에는 선택할 수 있는 많은 수의 타사 및 타사 데이터 공급자가 있습니다. 이러한 기능은 Audience Marketplace을 통해 AAM의 셀프서비스 인터페이스에서 사용할 수 있습니다. Audience Marketplace으로 이동하여 가능성을 찾아봅니다. 다음 비디오에서는 데이터 제공업체의 가격을 책정하기 전에 조직에 가장 유용한 데이터를 잠그고 사용할 수 있도록 무료 &quot;구매 전 시도&quot; 스트림을 활성화하는 방법을 포함하여 이러한 작업을 수행하는 방법을 보여 줍니다.

또한 사용할 데이터 공급자를 조사하고 결정하는 데 도움이 되는 유용한 리소스는 [[!DNL Adobe Audience Finder]](https://www.adobe-audience-finder.com/)입니다.

>[!VIDEO](https://video.tv.adobe.com/v/25188/?quality=12)

## 이상적인 사용자(전환) 트레이트 또는 세그먼트 식별 또는 생성 {#identify-create-an-ideal-user-conversion-trait-or-segment}

사이트에서 사람들이 수행하도록 하려는 것은 무엇입니까? 전환 이벤트란 무엇입니까? 물론 사이트 유형/수직 및 조직의 목표에 따라 이 질문에 대한 답변은 매우 다양합니다. 어떤 경우든 AAM에서는 이러한 기준을 충족한 방문자를 위한 트레이트를 만드는 것이 일반적입니다.

아래 비디오에서는 이 튜토리얼을 계속 진행하여 유사 모델을 만들 때 사용할 전환 트레이트를 만드는 방법을 보여 줍니다.

또한 Adobe Analytics 이벤트를 사용하여 트레이트를 만들 때 트레이트에 표시되어야 하는 사용자 수를 더 많이 수집하지 않도록 기억해야 하는 중요한 문제가 있습니다. 대규모 공개를 위해 다음 비디오를 시청하십시오. :)

>[!VIDEO](https://video.tv.adobe.com/v/23431/?quality=12)

**참고:** 위 비디오에서 보이는 예제에서는 Adobe Analytics이 있다고 가정합니다. 분명히, 이것은 그렇지 않을 수 있습니다. Google Analytics(GA)가 있는 경우 AAM으로 데이터를 전송하는 데 사용할 수 있는 모듈이 있습니다([설명서](https://experienceleague.adobe.com/docs/audience-manager/user-guide/dil-api/dil-modules.html?lang=ko) 참조). 사이트의 전환 활동이 GA에 의해 AAM으로 전송되는 경우 여기에서 전환 트레이트를 만들 수 있습니다. 다른 분석 솔루션이 있는 경우(또는 분석 솔루션이 없는 경우) DIL 코드 및 `submit` 함수 등을 통해 AAM으로 데이터를 전송할 수 있습니다. ([설명서](https://experienceleague.adobe.com/docs/audience-manager/user-guide/dil-api/dil-overview.html?lang=ko) 참조). 그런 다음 사이트에서 전환 활동이 수행될 때 전송된 데이터를 기반으로 전환 트레이트를 만듭니다.

## 타사 또는 타사 데이터에서 유사 모델 생성 {#create-a-look-alike-model-from-2nd-or-3rd-party-data}

위의 단계를 완료하고 나면 이제 알고리즘(유사) 모델을 만들 준비가 되었습니다. 모델을 설정하고 있을 때 전환 트레이트를 기본 트레이트(복제하려는 주요 방문자)로 사용하며, 활성화된 타사 데이터 스트림을 가져올 사용자 풀로 사용합니다.

>[!VIDEO](https://video.tv.adobe.com/v/25190/?quality-12)

## 중요한 모범 사례 {#an-important-best-practice}

Audience Manager에서 알고리즘 모델을 만들 때 모델이 가능한 한 효과적이길 바랍니다. 모델은 기본 트레이트/세그먼트의 멤버가 속한 모든 트레이트를 고려하고 있으므로, 모든 사람이 트레이트/세그먼트에 있는 경우에는 모델에 도움이 되지 않습니다. 따라서 수퍼 일반 트레이트(예: 사이트를 방문한 모든 사람 또는 귀하로부터 광고를 받은 모든 사람 등)가 있는 경우, 해당 트레이트가 속한 데이터 소스가 모델의 데이터 소스에 포함되어 있지 않은지 확인하십시오. 이 문서의 사용 사례에서는 새로운 디자인을 위해 서드파티 데이터를 보는 데 중점을 두고 있으므로 가능성은 낮지만 언급할 가치가 있으며 모든 알고리즘 모델에 적용됩니다.

## [!UICONTROL Algorithmic Trait] 만들기 {#creating-an-algorithmic-trait}

그런 다음 모델 결과를 사용할 수 있도록 [!UICONTROL Algorithmic Trait]을(를) 만들어야 합니다. 트레이트를 만들지 않으면 모델이 무용지물이 됩니다. 따라서 모델이 실행되면 트레이트 대화 상자로 이동하여 [!UICONTROL Algorithmic Trait]을(를) 만드십시오. 다음 비디오는 안내서와 몇 가지 팁을 보여 줍니다.

>[!VIDEO](https://video.tv.adobe.com/v/25191/?quality=12)

## 모델 데이터에서 세그먼트를 생성하여 DSP로 보내기 {#creating-a-segment-from-the-model-data-and-sending-it-to-dsps}

[!UICONTROL Algorithmic Trait]을(를) 만든 후에는 데이터를 활성화할 수 있도록 세그먼트를 새로 만들 수 있습니다. 트레이트를 활성화할 수는 없지만, 대신 세그먼트를 활성화(사용)할 수 있도록 [!UICONTROL Algorithmic Trait]이(가) 포함된 트레이트가 하나인 새 세그먼트를 만들 수 있습니다.

이 알고리즘 트레이트에서 세그먼트를 만들면 사이트에서 이미 전환된 사람처럼 보이는 잠재 고객 대상을 갖게 됩니다. 이제 이 세그먼트를 Audience Manager의 DSP 대상에 매핑할 수 있습니다. 일반 대중보다 사이트에서 전환할 가능성이 더 높은 잠재 고객을 대상으로 마케팅을 타깃팅하여 광고 투자 수익률을 높일 수 있습니다.
