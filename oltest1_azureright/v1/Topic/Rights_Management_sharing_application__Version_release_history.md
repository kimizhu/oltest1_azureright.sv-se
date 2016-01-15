---
description: na
keywords: na
title: Rights Management sharing application: Version release history
search: na
ms.date: na
ms.service: rights-management
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6751bd90-959f-4eba-91ed-6588ac983762
---
# Rights Management delning: Versionshistorik f&#246;r version
Rights Management-teamet uppdaterar regelbundet på delningsapplikation för korrigeringar och nya funktioner för Rights Management. Använd följande information för att se vad som är nya eller har ändrats i en version. Den mest aktuella versionen visas först.

Versioner före 1 januari 2015 visas inte.

> [!NOTE]
> Om du har feedback eller en fråga om RMS-delning program kan skicka ett e-postmeddelande till [AskIPTeam](mailto:AskIPTeam@microsoft.com?subject=RMS%20sharing%20app:%20Feedback%20or%20question).

## Version 1.0.1908.0

|||
|-|-|
|Publicerat|9/16/2015|
|Korrigeringar|-   Stöd för multifaktorautentisering (MFA) för Azure RMS då försvinner även beroende på Microsoft-inloggningsassistent för program som använder moderna autentisering.<br />    Mer information finns i [Multifaktorautentisering (MFA) och Azure RMS](../Topic/Requirements_for_Azure_Rights_Management.md#BKMK_MFA)   under  [Krav för Azure Rights Management](../Topic/Requirements_for_Azure_Rights_Management.md).|

## Version 1.0.1784.0

|||
|-|-|
|Publicerat|7/30/2015|
|Korrigeringar|-   Som standard uppdateringsintervall för rättigheter principmallar minskas från 7 dagar till dag.<br />-   Litet antal bakslag och mindre buggar.|

## Version 1.0.1770.0

|||
|-|-|
|Publicerat|4/25/2015|
|Korrigeringar|-   Nu endast ägare och medarbetare ägare kan ta bort skyddet. Det går inte att medarbetare författare.<br />-   Filer som finns på en nätverksresurs kan nu skyddas.|
|Nya funktioner|<ul><li>Stöd för dokument spårning och återkallade certifikat. Mer information finns i [Spåra och återkalla dokumenten när du använder RMS-delning program](../Topic/Track_and_revoke_your_documents_when_you_use_the_RMS_sharing_application.md)</li><li>Stöd för mallen när du väljer **Dela skyddat**:<br /><br /><ul><li>Nu kan du välja mallar.</li><li>I stället för skjutreglaget ser du en listruta som innehåller mallar och anpassade behörigheter.</li><li>Alternativ för visas inte längre **Tillåt användning på alla enheter** och **genomdriva användningsrestriktioner**. I stället **allmän Protection** markeras automatiskt, beroende på filtypen.</li></ul>    Mer information finns i [Dialogrutan för delningsapplikation Rights Management](../Topic/Dialog_box_options_for_the_Rights_Management_sharing_application.md).</li></ul>|

## Version 1.0.1667.0

|||
|-|-|
|Publicerat|1/19/2015|
|Korrigeringar|-   Stöd för kinesiska teckensnitt i RMS-delning app PPDF viewer.<br />-   Bättre felhantering och meddelanden.<br />-   Rätta till ett problem med automatisk uppdatering anmälan när en nyare version av appen är tillgänglig för hämtning.|
|Nya funktioner|-   **Stöd för flera e-domäner inom organisationen,**: Om du använder AD RMS användare i organisationen har flera domäner för e-post och kan den här uppdateringen användarna allt innehåll som har skyddats av användare i din organisation i andra domäner. Mer information finns i [Endast AD RMS: Stöd för flera domäner för e-post i din organisation](../Topic/Rights_Management_sharing_application_administrator_guide.md#BKMK_FederatedDomains) under den [Rights Management dela program administratörshandboken](../Topic/Rights_Management_sharing_application_administrator_guide.md).|
