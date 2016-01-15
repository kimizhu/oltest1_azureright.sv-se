---
description: na
keywords: na
title: Activating Azure Rights Management
search: na
ms.date: na
ms.service: rights-management
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f8707e01-b239-4d1a-a1ea-0d1cf9a8d214
---
# Aktivera Azure Rights Management
När du aktiverar [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] (Azure RMS) som din organisation kan starta skydda viktiga data med hjälp av program och tjänster som stöder denna information protection lösning. Administratörer kan även hantera och övervaka skyddade filer och e-postmeddelanden som äger i din organisation. Du måste aktivera [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)] innan du kan använda information rights management (IRM) funktioner i Office och SharePoint Exchange och skydda en fil som känslig eller konfidentiell.

Om du vill veta mer om Azure Rights Management innan du aktiverar tjänsten, till exempel vilka lösningar det löses tillfällen typisk användning och hur det fungerar, se [Vad är Azure Rights Management?](../Topic/What_is_Azure_Rights_Management_.md)

> [!IMPORTANT]
> Innan du aktiverar [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)], kontrollera att din organisation har en tjänst plan som innehåller [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)] tjänster. Annars du kommer inte att kunna aktivera Azure RMS.
> 
> Mer information finns i [Molnet prenumerationer som har stöd för Azure RMS](../Topic/Requirements_for_Azure_Rights_Management.md#BKMK_SupportedSubscriptions) under den [Krav för Azure Rights Management](../Topic/Requirements_for_Azure_Rights_Management.md) ämne.

När du har aktiverat Azure RMS kan alla användare i organisationen kan använda information protection för sina filer och alla användare kan öppna (förbruka) filer har skyddats av Azure RMS. Om du vill kan begränsa du emellertid som kan använda information protection med inledande kontroller för en fasindelad distribution. Mer information finns i [Konfigurera inledande kontroller för en fasindelad distribution](../Topic/Activating_Azure_Rights_Management.md#BKMK_OnboardingControls) i det här avsnittet.

## Aktivera Rights Management
Använda något av följande procedurer för att aktivera [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)].

> [!TIP]
> Du kan också använda Windows PowerShell-cmdlet [Aktivera Aadrm](http://msdn.microsoft.com/library/windowsazure/dn629412.aspx), för att aktivera [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)].

#### Aktivera Rights Management från administrationscentret för Office 365

1.  När du har registrerat dig för ett Office 365-plan som innehåller Rights Management [Logga in på Office 365 med kontot arbetet eller skolan](https://portal.office.com/) som administratör för distribution av Office 365.

2.  Om inte automatiskt visas administrationscentret för Office 365, välj ikonen starta app i övre vänstra och välj **Admin**. Den **Admin** bricka visas endast för Office 365-administratörer.

    > [!TIP]
    > Mer information om admin center finns [Administrationscenter om Office 365 - administratör hjälp](https://support.office.com/article/About-the-Office-365-admin-center-Admin-Help-58537702-d421-4d02-8141-e128e3703547).

3.  I det vänstra fönstret, expandera **TJÄNSTINSTÄLLNINGARNA**.

4.  Klicka på **Rights Management**.

    > [!NOTE]
    > Om det här alternativet inte visas kanske eftersom service planen eller produkten versionen stöder inte Rights Management eller den har ännu inte uppgraderats för att stödja Rights Management.
    > 
    > Använda informationen i den [Molnet prenumerationer som har stöd för Azure RMS](../Topic/Requirements_for_Azure_Rights_Management.md#BKMK_SupportedSubscriptions) under den [Krav för Azure Rights Management](../Topic/Requirements_for_Azure_Rights_Management.md) avsnittet om att bekräfta support. Om din service planen eller produkten version stöds men du inte ser alternativet Rights Management, kanske eftersom tjänsten inte har ännu uppgraderats. Om du behöver hjälp med det här problemet, skicka ett e-postmeddelande till [askipteam](mailto:askipteam@microsoft.com?subject=I%20cannot%20activate%20RMS).

5.  På den **RIGHTS MANAGEMENT** klickar du på **hantera**.

6.  På den **rights management** klickar du på **Aktivera**.

7.  När du uppmanas **vill du aktivera Rights Management?**, klickar du på **Aktivera**.

Du bör nu visas **Rights management har aktiverats** och möjlighet att inaktivera.

#### Aktivera Rights Management från Azure-hanteringsportalen

1.  När du har registrerat dig för kontot Azure [Logga in på Azure-hanteringsportalen](http://go.microsoft.com/fwlink/p/?LinkID=275081).

2.  I det vänstra fönstret klickar du på **ACTIVE DIRECTORY**.

3.  Från den **active directory** klickar du på **RIGHTS MANAGEMENT**.

4.  Välj den katalog att hantera för [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)], klickar du på **Aktivera**, och bekräfta åtgärden.

    > [!NOTE]
    > Om du ser ett fel vid aktivering kanske eftersom service planen eller produkten versionen inte stöder [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)].
    > 
    > Använda informationen i den [Molnet prenumerationer som har stöd för Azure RMS](../Topic/Requirements_for_Azure_Rights_Management.md#BKMK_SupportedSubscriptions) under den [Krav för Azure Rights Management](../Topic/Requirements_for_Azure_Rights_Management.md) avsnittet om att bekräfta RMS-support. Om du behöver hjälp med det här problemet, skicka ett e-postmeddelande till [askipteam](mailto:askipteam?subject=I%20cannot%20activate%20RMS).

Den **RIGHTS MANAGEMENT STATUS** ska nu visa **Active** och **Aktivera** alternativet ersätts med **inaktivera**.

### Rights Management statusvärden och beskrivningar i Azure-hanteringsportalen
Utöver de **Active** status, som anger att Rights Management-tjänsten är aktiverad och redo att användas, du kan också se **inaktiv**, **ej tillgänglig**, eller **Ej behörig**.

|Statusvärdet|Beskrivning|
|----------------|---------------|
|**Aktiv**|[!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)] är aktiverad och redo att användas.|
|**Inaktiv**|[!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)] är inaktiverat och måste aktiveras innan din organisation kan skydda filer.|
|**Inte tillgängligt**|Den [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)] -tjänsten har stoppats. Försök igen senare.|
|**Obehörig**|Du har inte behörighet att visa status för de [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)] service. Till exempel ditt konto är utelåst eller du är inte global administratör för den valda innehavaren.|

## <a name="BKMK_OnboardingControls"></a>Konfigurera inledande kontroller för en fasindelad distribution
Om du inte vill att alla användare ska kunna skydda filer omedelbart med hjälp av Azure RMS, kan du konfigurera inledande användarinställningar med hjälp av den [mängd AadrmOnboardingControlPolicy](http://msdn.microsoft.com/library/azure/dn857521.aspx) Windows PowerShell-kommandot. Du kan köra det här kommandot innan eller när du har aktiverat Azure RMS.

> [!IMPORTANT]
> Om du vill använda detta kommando måste du ha version **2.1.0.0** av den [Azure RMS Windows PowerShell-modul](http://go.microsoft.com/fwlink/?LinkId=257721).
> 
> Om du vill kontrollera den version som du har installerat kör du: **(Get-Module aadrm –ListAvailable).Version**

Om du vill ursprungligen bara administratörer i gruppen "IT-avdelningen" (som har ett objekt-ID för fbb99ded-32a0-45f1-b038-38b519009503) för att kunna skydda innehåll för test, använder du följande kommando:

```
Set-AadrmOnboardingControlPolicy – SecurityGroupObjectId fbb99ded-32a0-45f1-b038-38b519009503
```
Observera att det här alternativet för konfiguration, måste du ange en grupp. Du kan inte ange enskilda användare.

Eller om du vill se till att endast användare med rätt licens för att använda Azure RMS kan skydda innehåll:

```
Set-AadrmOnboardingControlPolicy -UseRmsUserLicense $true
```
När du använder de här kontrollerna inledande alla användare i organisationen kan alltid använda skyddat innehåll som har skyddats av en delmängd användare, men de kan inte gälla information protection själva från klientprogram. Inte till exempel finns i klienterna Office standardmallar som publiceras automatiskt när Azure RMS är aktiverad eller anpassade mallar som du kan konfigurera.  Serversidan program, till exempel Exchange kan genomföra sina egna per användare kontroller för RMS-integrering att uppnå samma resultat.

## Nästa steg
Nu när du har aktiverat [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] för din organisation använda den [Översikt över Azure Rights Management-distribution](../Topic/Azure_Rights_Management_Deployment_Roadmap.md) att kontrollera om det finns andra konfigurationssteg som du kanske behöver innan du lansera [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] för användare och administratörer. Exempel: du kanske vill använda [anpassade mallar](http://technet.microsoft.com/library/dn642472.aspx) om du vill göra det lättare för användare att använda information protection för filer, ansluta dina lokala servrar att använda [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] genom att installera den [RMS-koppling](http://technet.microsoft.com/library/dn375964.aspx), och distribuera den [delningsapplikation Rights Management](http://technet.microsoft.com/library/jj585031.aspx) som stöder skyddar alla filtyper på alla enheter. Office-tjänster, till exempel Exchange Online och SharePoint Online kräver ytterligare konfiguration innan du kan använda sina Information Rights Management (IRM)-funktioner. Men om det finns inga andra konfigurationen steg som du behöver, ser [Använda Azure Rights Management](../Topic/Using_Azure_Rights_Management.md) operativa riktlinjer för att stödja en lyckad distribution för din organisation.

Information om hur programmen fungerar med [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)], se [Hur program stöd för Azure Rights Management](../Topic/How_Applications_Support_Azure_Rights_Management.md).

## Se även
[Konfigurera Azure Rights Management](../Topic/Configuring_Azure_Rights_Management.md)

