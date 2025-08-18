---
title: 유사 모델을 사용하여 판매된 재고를 자사 데이터에서 확장
description: 이 자습서에서는 새로운 유사 대상을 만들고 전환 세그먼트의 확장으로 판매할 수 있도록 유사 모델을 설정하고 사용하는 데 필요한 단계를 안내합니다.
feature: Algorithmic Models
topics: null
activity: use
doc-type: feature video
team: Technical Marketing
thumbnail: 23523.jpg
kt: 1688
role: User, Developer, Data Engineer, Architect, Data Architect, Admin, Leader
level: Intermediate
exl-id: 6820528e-3211-4a1d-be05-50f1292179d2
source-git-commit: 2094d3bcf658913171afa848e4228653c71c41de
workflow-type: tm+mt
source-wordcount: '849'
ht-degree: 0%

---

# 유사 모델을 사용하여 판매된 재고를 자사 데이터에서 확장 {#using-look-alike-models-to-extend-sold-out-inventory-from-your-st-party-data}

이 자습서에서는 새로운 유사 대상을 만들고 전환 세그먼트의 확장으로 판매할 수 있도록 유사 [!UICONTROL Models]을(를) 설정하고 사용하는 데 필요한 단계를 안내합니다.

## 사용 사례 세부 정보 {#use-case-details}

콘텐츠 게시자입니다. 사이트에서 변환기에 대한 재고가 이미 매진되었다면, 해당 영업 기회는 여기서 끝난다고 생각할 수 있습니다. AAM의 유사 [!UICONTROL Models]을(를) 입력하십시오. 이 기능을 사용하면 품절된 인벤토리를 추가로 확장할 수 있으며, 아직 전환되지 않았지만 전환된 사람들처럼 보이는/행동하는 사람들의 대상자도 판매할 수 있습니다. 이 대상 세그먼트는 일반적으로 실제 변환기 미만의 가격으로 판매되지만, 사이트에 광고를 게재하려는 광고주를 위한 추가 대상 옵션을 제공하여 실적을 추가할 수 있습니다. 이 사용 사례의 추가적인 이점은 자사 데이터에서 이 모델을 실행하는 데 드는 비용이 전혀 들지 않는다는 것입니다.

이 자습서의 단계는 다음과 같습니다.

1. 이상적인 사용자(전환) 트레이트 또는 세그먼트 식별/생성
1. 이 전환 트레이트/세그먼트를 기본 항목으로 사용하여 모델 만들기
1. 모델에서 [!UICONTROL First party]개의 데이터 원본을 선택하고 모델을 실행하십시오.
1. 모델 결과에서 [!UICONTROL Algorithmic Trait]을(를) 만들고 트레이트를 세그먼트에 추가합니다.
1. 관심 있는 광고주에게 세그먼트를 제공하여 전환 세그먼트 판매 확장

## 이상적인 사용자(전환) 트레이트 또는 세그먼트 식별 또는 생성 {#identify-create-an-ideal-user-conversion-trait-or-segment}

사이트에서 사람들이 수행하도록 하려는 것은 무엇입니까? 전환 이벤트란 무엇입니까? 물론 사이트 유형/수직 및 조직의 목표에 따라 이 질문에 대한 답변은 매우 다양합니다. 어떤 경우든 AAM에서는 이러한 기준을 충족한 방문자를 위한 트레이트를 만드는 것이 일반적입니다.

이 사용 사례에서는 변환자인 사용자에 대한 재고가 모두 판매되었기 때문에 이미 이 것으로 간주됩니다. 그러나 이 자습서의 목적상 나머지 사용 사례에 대해 참조할 수 있도록 논의하는 것이 좋습니다.

또한, 이벤트를 사용하여 트레이트를 만들 때 트레이트에 들어가야 하는 사용자 수를 초과하여 모으지 않도록 주의해야 하는 중요한 문제가 있습니다. 대규모 공개를 위해 다음 비디오를 시청하십시오. :)

>[!VIDEO](https://video.tv.adobe.com/v/23431/?quality=12)

**참고:** 위 비디오에서 보이는 예제에서는 Adobe Analytics이 있다고 가정합니다. 분명히, 이것은 그렇지 않을 수 있습니다. Google Analytics(GA)가 있는 경우 AAM으로 데이터를 전송하는 데 사용할 수 있는 모듈이 있습니다([설명서](https://experienceleague.adobe.com/docs/audience-manager/user-guide/dil-api/dil-overview.html) 참조). 사이트의 전환 활동이 GA에 의해 AAM으로 전송되는 경우 여기에서 전환 트레이트를 만들 수 있습니다. 다른 분석 솔루션이 있는 경우(또는 분석 솔루션이 없는 경우) DIL 코드 및 `submit` 함수 등을 통해 AAM으로 데이터를 전송할 수 있습니다. ([설명서](https://experienceleague.adobe.com/docs/audience-manager/user-guide/dil-api/dil-modules.html) 참조). 그런 다음 다시 사이트에서 전환 활동이 수행될 때 전송된 데이터를 기반으로 전환 트레이트를 만듭니다.

## 자사 데이터에서 유사 모델 만들기 {#creating-a-look-alike-model-from-first-party-data}

이 단계에서는 [!UICONTROL First Party] 유사 모델을 만듭니다. 즉, 기본 트레이트/세그먼트에 자사 전환 트레이트/세그먼트를 사용하게 되며(어차피 대부분의 모델에는 정상일 수 있음), 변환기처럼 보이는 더 많은 사용자에 대한 자사 데이터 풀만 살펴보게 됩니다. 제2자 또는 제3자 데이터는 보지 않습니다.

이 사용 사례에서는 사이트 내에 전환자와 비슷하게 보이지만 아직 전환되지 않은 사용자 세그먼트를 만들어 관심 있는 광고주에게 유사 세그먼트를 판매할 수 있도록 하는 것이 중요합니다.

>[!VIDEO](https://video.tv.adobe.com/v/23504/?quality-12)

## 알고리즘 트레이트 만들기 {#creating-an-algorithmic-trait}

그런 다음 모델 결과를 사용할 수 있도록 [!UICONTROL Algorithmic Trait]을(를) 만들어야 합니다. 트레이트를 만들지 않으면 모델이 무용지물이 됩니다. 따라서 모델이 실행되면 트레이트 대화 상자로 이동하여 [!UICONTROL Algorithmic Trait]을(를) 만드십시오. 다음 비디오는 안내서와 몇 가지 팁을 보여 줍니다.

>[!VIDEO](https://video.tv.adobe.com/v/23523/?quality=12)

## 광고주에게 [!UICONTROL Algorithmic Segment] 제공 {#offering-the-algorithmic-segment-to-advertisers}

[!UICONTROL Algorithmic Trait]을(를) 만든 후에는 데이터를 활성화할 수 있도록 세그먼트를 새로 만들 수 있습니다. 트레이트는 활성화할 수 없으며 대신 세그먼트를 활성화(사용)할 수 있도록 트레이트가 포함된 새로운 트레이트가 있는 세그먼트를 만들 수 있습니다.[!UICONTROL Algorithmic Trait]

유사 모델에서 높은 점수를 받은 자사 방문자 세그먼트를 만들면(즉, 변환기로 보이지만 아직 전환하지 않은 경우) 사이트에서 실제 변환기 인벤토리를 모두 판매한 후에도 이 세그먼트를 사이트의 광고주에게 제공할 수 있습니다. 이는 Audience Manager에서 유사 [!UICONTROL Models]을(를) 사용하여 이 대상을 확장하고 추가 매출을 계속 볼 수 있는 좋은 방법입니다.
