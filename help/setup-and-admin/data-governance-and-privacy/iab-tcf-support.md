---
title: IAB TCF 2.2 지원
description: IAB TCF에 대한 Audience Manager 플러그인과 Adobe의 옵트인 개체 및 동의 관리 공급자(CMP)와 함께 작동하는 방법에 대해 알아봅니다.
feature: Data Governance & Privacy
thumbnail: 26434.jpg
kt: 5027
role: Developer, Data Engineer, Architect
level: Experienced
exl-id: 04b4e786-0457-4dcc-bcf9-a79eda67bb2e
source-git-commit: f9708e705d95b43084ff11e342dc54ff11d6326c
workflow-type: tm+mt
source-wordcount: '1059'
ht-degree: 0%

---

# Audience Manager에서 IAB TCF 2.2 지원 {#iab-tcf-support-in-audience-manager}

Adobe은 옵트인 기능 및 Audience Manager 플러그인을 통해 IAB TCF 2.2(Transparency and Consent Framework 2.2) 지원에 대한 사용자의 개인 정보 보호 선택을 관리 및 소통할 수 있는 수단을 제공합니다. 이 문서는 IAB TCF에 대한 Audience Manager 플러그인 및 Adobe의 옵트인 개체 및 동의 관리 공급자(CMP)와 함께 작동하는 방법을 이해하는 데 도움이 되는 문서와 함께 작동합니다. IAB에 대해 자세히 알아보려면 해당 웹 사이트([https://www.iabeurope.eu/](https://www.iabeurope.eu/))를 참조하십시오.

## 첫 번째 단계: Experience Cloud ID 옵트인 이해 {#first-step-understand-ecid-s-opt-in}

IAB TCF 작업 방법을 이해하려면 먼저 ECID(Experience Cloud ID 서비스) 라이브러리의 일부인 [!DNL Opt-in] 기능을 이해해야 합니다. 옵트인 작동 방식을 잘 모를 경우 먼저 [이 유용한 문서](https://experienceleague.adobe.com/docs/core-services-learn/tutorials/id-service/use-opt-in-to-control-experience-cloud-activities-based-on-user-consent.html?lang=ko)를 참조하세요. 옵트인 [설명서](https://experienceleague.adobe.com/docs/id-service/using/implementation/opt-in-service/optin-overview.html?lang=ko)도 검토해야 합니다. 해당 리소스를 모두 사용한 후에는 이 페이지로 돌아가 계속하십시오.

## IAB TCF를 위한 Audience Manager 플러그인 {#the-audience-manager-plug-in-for-iab-tcf}

이제 옵트인 서비스가 작동하는 방식에 대한 기본적인 이해를 했으므로 Audience Manager이 [!DNL IAB Transparency and Consent Framework (TCF)] 지원에 레이어를 적용할 수 있습니다. 이 작업은 플러그인을 통해 옵트인 개체에 적용됩니다.

IAB TCF용 Audience Manager 플러그인은 옵트인의 기능을 확장하며 AAM 고객이 IAB TCF에 따라 사용자 개인 정보 보호 선택 사항을 평가하고 준수하며 다운스트림 파트너에게 전달할 수 있도록 합니다. 데이터 컨트롤러(Adobe 고객) 및 공급업체(DMP, DSP, SSP, 광고 서버 등)에 대한 표준을 제공합니다. 을 사용하여 동의 환경 전체에서 동의를 이해할 수 있습니다.

## IAB TCF 활성화 {#enabling-iab-tcf}

Adobe Experience Platform Launch을 사용하는 경우 아래 짧은 비디오에 표시된 간단한 확인란이므로 IAB TCF용 Audience Manager 플러그인을 쉽게 활성화할 수 있습니다.

>[!VIDEO](https://video.tv.adobe.com/v/38262/?quality=12&captions=kor)

또는 Launch를 사용하지 않는 경우 Experience Cloud 방문자를 인스턴스화할 때 `isIabContext=true`을(를) 사용하여 활성화할 수 있습니다. 이렇게 하면 IAB TCF 흐름이 시작됩니다. 즉, 동의 수집에 다른 단계를 추가하고, IAB TCF를 사용하여 IAB TC 문자열을 쿼리하고 이를 다시 옵트인에 제공하여 Experience Cloud 솔루션과 통신합니다.

## IAB TC 문자열 {#iab-tcf-consent-string}

IAB가 제공하는 표준 중 하나는 &quot;동의 문자열&quot;(DaisyBit이라고도 함)이며, 실제로는 두 개의 목록으로 구성됩니다.

1. 목적: **수행할 동의**&#x200B;는 무엇입니까?
1. 공급업체: **누구에게 동의합니까**?

### 목적 {#purposes}

IAB TCF 2.2에는 동의를 수집하는 10가지 &quot;목적&quot;이 있습니다(공급업체가 방문자의 데이터로 수행할 수 있는 작업). Adobe Audience Manager은 10개 모두를 필요로 하지 않으며, 공급업체 동의 외에 다음 목적으로만 동의해야 합니다.

* **목적 1:** 장치에 정보를 저장 및/또는 액세스;
* **목적 10:** 제품 개발 및 개선;
* **특수 목적 1:** 보안을 보장하고, 사기를 방지하고, 디버그를 수행합니다.

이는 IAB TC 문자열의 첫 번째 부분이며 해당 목적/활동이 승인되었는지 여부를 나타내는 1과 0으로 기록됩니다.

>[!NOTE]
>
>IAB 규정에 따라 특수 목적 1(보안 보장, 사기 방지 및 디버그)은 항상 동의하며 사용자는 이에 반대할 수 없습니다.

### 공급업체 {#vendors}

IAB TC 문자열의 또 다른 부분은 수백 개의 공급업체가 포함된 긴 목록이므로 방문자는 사이트에 태그가 있고 사용할 공급업체를 선택할 수 있는 해당 공급업체 목록을 제공받을 수 있습니다. 공급업체는 목록에 위치를 유지합니다. 예를 들어 이 목록에 있는 Adobe Audience Manager의 공급업체 번호는 565입니다. 목록의 해당 번호에 &quot;1&quot;이 있는 경우 Audience Manager은 목록의 맨 앞에서 승인된 목적을 수행할 수 있습니다. AAM 스폿에 &quot;0&quot;이 있으면 데이터로 아무 작업도 할 수 없습니다.

**고객이 IAB TCF를 사용하여 이러한 목적과 공급업체를 선택하거나 모든 활동을 승인/승인할 수 있는 UI를 제공하기 위한 Audience Manager의 경우, IAB TCF에 등록된 CMP 파트너를 사용하거나 IAB TCF를 지원하고 IAB TCF에 등록된 파트너를 빌드해야 합니다.**

## 옵트인: IAB와 Adobe 애플리케이션 간 번역 {#opt-in-translating-between-iab-and-adobe-solutions}

IAB TCF를 사용하면 이점 중 하나는 위에 나열된 표준 목적을 통해 최종 사용자는 Adobe 솔루션 목록보다 자신이 승인하는 것에 대한 아이디어를 더 많이 얻을 수 있다는 것입니다. 최종 사용자는 Audience Manager 또는 [!DNL Target]을(를) &quot;승인&quot;하는 것이 무엇을 의미하는지 알 수 없지만 &quot;장치에 정보를 저장 및/또는 액세스&quot; 또는 &quot;제품 개발 및 개선&quot;하는 것이 더 쉽게 이해하고 동의할 수 있습니다.

Audience Manager이 승인되려면(즉, 옵트인에 대한 IAB 목적을 번역하여 AAM에 &quot;예&quot; 투표를 제공하려면 위에 나열된 목적 1과 10은 최종 사용자의 동의를 받아야 합니다. 이 중 하나가 승인되지 않거나 공급업체가 승인되지 않은 경우 AAM은 픽셀 실행을 실행하거나 쿠키를 설정하지 않습니다. 또한 많은 고객이 최종 사용자에게 &quot;모두 또는 전혀 없음&quot; UI를 제공하도록 선택함으로써 Audience Manager(및 기타 Experience Cloud 솔루션)의 사용을 허용하거나 허용하지 않는다는 것을 아는 것도 좋습니다.

IAB TCF 흐름용 Audience Manager 플러그인이 게시자와 광고주 사용 사례 모두에 적용되는 방식에 대한 유용한 정보가 [설명서](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/consent-management/aam-iab-plugin.html?lang=ko)에 있습니다.

## IAB: 동의 다운스트림 전송 {#iab-sending-consent-downstream}

IAB TCF용 Audience Manager 플러그인을 사용하면, 글로벌 공급업체 목록에 있는 파트너의 플랫폼 수준(타사) ID 동기화에도 사용자의 동의 선택 사항이 전송되어 파트너가 사용자 동의 정보를 가지고 그에 따라 작동할 수 있습니다. 이 정보는 다음 두 가지 변수로 전송됩니다.

* gdpr = 1
* gdpr_consent = [인코딩된 동의 문자열]

Audience Manager이 IAB 컨텍스트에 있고 동의를 제공하지 않거나(또는 부정적인 동의를 제공), 사용자가 IAB TC 문자열을 전혀 수집하지 않는 경우 호출이 삭제되므로 주의해야 합니다. 그러니까, 그 경우에는... 다운스트림으로 동의를 전달하지 않습니다.

## 데모 {#demo}

아래 비디오에서는 ECID 및 솔루션의 쿠키 및 비콘이 IAB 사용자 선택 사항의 영향을 받는 방식을 확인할 수 있습니다.

>[!VIDEO](https://video.tv.adobe.com/v/38246/?quality=12&captions=kor)

구현 및 테스트 방법, 사용 사례 및 워크플로를 포함하여 IAB TCF 2.2용 Audience Manager 플러그인에 대한 자세한 내용은 [설명서](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/consent-management/aam-iab-plugin.html?lang=ko)를 참조하세요.
