---
description: na
keywords: na
title: Helping Users to Protect Files by Using Azure Rights Management
search: na
ms.date: na
ms.service: rights-management
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 58f9a6ff-4121-4c8c-9865-1bb290604ad2
---
# Hj&#228;lper anv&#228;ndarna att skydda filer med Azure Rights Management
När du har distribuerat och Azure Rights Management (Azure RMS) har konfigurerats för din organisation kan du få hjälp och vägledning för användare och administratörer supportavdelningen:

-   **Information om slutanvändaren:**

    Hur och när användarna att skydda dokument och e-postmeddelanden som innehåller känslig information. När det är möjligt, tillhandahåller denna information för sina befintliga arbeta så att de kan inkludera ytterligare information om en redan välbekanta process i stället för introduktion till helt nya processer. Se till att meddela fördelarna (och risker) som är specifika för ditt företag, samt ge vägledning för när de ska skydda filer och e-post. Om du har konfigurerat [anpassade mallar](http://technet.microsoft.com/library/dn642472.aspx), anvisningar om en Markera om mallnamn och beskrivning inte är tillräckliga att välja rätt.

    > [!TIP]
    > Exempel videor för slutanvändare:
    > 
    > -   [Azure RMS-användarupplevelsen](http://channel9.msdn.com/Series/Information-Protection/Azure-RMS-user-experience)
    > -   [Spårning av Azure RMS-dokument och återkallade](http://channel9.msdn.com/Series/Information-Protection/Azure-RMS-Document-Tracking-and-Revocation)

-   **Information för administratörer:**

    Vissa program använder automatiskt information protection med principer och inställningar som administratörer konfigurera. Dessa program kan du behöva anvisningar för andra administratörer som hanterar dessa program och tjänster. Mer information finns i [Hur program stöd för Azure Rights Management](../Topic/How_Applications_Support_Azure_Rights_Management.md) och [Konfigurera program för Azure Rights Management](../Topic/Configuring_Applications_for_Azure_Rights_Management.md).

-   **Hjälp om fast information:**

    En av de mest användbart verktyg för supporten är den [RMS analysera](https://www.microsoft.com/en-us/download/details.aspx?id=46437).   Hjälp om fast operatörer kan köras med alternativet Azure RMS-administratören och de kan begära att användare ska köras med alternativet Azure RMS-användare. Det här verktyget kan inte bara hjälpa dig att identifiera problem, men också åtgärda problem hittas, och om du fortfarande inte fast post spårningen loggar.

    Om det är tillförlitligt begäranden fullständig behörighet åtkomst till skyddade dokument, till exempel en begäran med juridiska avdelningen eller en manager när en anställd har lämnade organisationen, kontrollera supporten har processer för att begära detta med hjälp av Azure RMS [superanvändare funktionen](https://technet.microsoft.com/en-us/library/mt147272.aspx).

    Dessutom kan är det här några vanliga problem som användarna kan rapportera:

    -   **Hjälp för inloggning:**

        Användare kan måste ange autentiseringsuppgifter när Azure RMS måste autentisera en användare och det går inte att använda cachelagrade autentiseringsuppgifter. Det här är användarens arbetet eller skolan konto och lösenord som är kopplat till ditt Office 365-klient eller Azure Active Directory-klient. Det kommer inte att ett Microsoft-konto (tidigare Microsoft Live ID) eller deras personliga e-postkonto, eftersom dessa inte stöds för närvarande av Azure RMS. Ange användare och supportavdelningen anvisningar för det konto som ska användas när användare uppmanas autentiseringsuppgifter när de använder dessa program med Azure RMS.

    -   **Problem med att skydda eller förbrukar innehåll:**

        Kontrollera att användarna har instruktioner för program att de använder och använder program och enheter som stöds av Azure RMS. Mer information om program som stöds och enheter, se [Krav för Azure Rights Management](../Topic/Requirements_for_Azure_Rights_Management.md).

        Om användare visas ett fel när du försöker skydda eller allt innehåll uppmaning om att köra den [RMS analysera](https://www.microsoft.com/en-us/download/details.aspx?id=46437) som Azure RMS-användare.

        Om användarna rapportera att de kan öppna skyddat innehåll men har inte de rättigheter som de behöver, be dem att köra den [RMS analysera](https://www.microsoft.com/en-us/download/details.aspx?id=46437) som en användare av Azure RMS och ladda ned och visa mallarna. Detta bekräftar att de har hämtats mallar och vilka behörigheter mallarna tillhandahålla. Problemet kan vara att användaren inte är i rätt grupp som konfigurerats för mallen eller att mallen måste konfigurera för användaren.

Använd följande avsnitt programspecifika information som hjälper användarna att skydda känsliga dokument och e-post.

## Med Rights Management delning programmet information protection
Rights Management (RMS) delning krävs att skydda och förbruka skyddat innehåll om de använder Office 2010-användare, men du bör också för alla datorer och mobila enheter som stöder Azure RMS.

Förutom att göra det enklare för användare att skydda viktiga dokument, tillåter RMS-delning programmet att användare spåra dokument som de har skyddat och vid behov återkalla åtkomst till dem.

Instruktioner att använda programmet för Windows-datorer finns i [Rights Management delning användaren guide till](http://technet.microsoft.com/library/dn339006.aspx).

Mobila enheter finns på [vanliga frågor och svar för Microsoft Rights Management dela program för mobila plattformar](http://technet.microsoft.com/dn451248).

> [!TIP]
> En hög exempel med skärmbilder finns i [Användare dela på ett säkert sätt bifogade filer med mobila användare](../Topic/What_is_Azure_Rights_Management_.md#BKMK_Example_SharingApp) avsnitt i den [Vad är Azure Rights Management?](../Topic/What_is_Azure_Rights_Management_.md) ämne.

## Med hjälp av information protection med Office 365, Office 2016 eller Office 2013
Om du använder Azure RMS och inte har installerat delningsapplikation Rights Management användare ser inte den **Dela skyddat** knapp i menyfliksområdet eller **skydda på plats** från filen Explorer som gör det lättare för dem att skydda filer. De måste följa instruktionerna liknar dessa för dessa användare.

> [!TIP]
> Om du vill hitta programspecifika hjälp och instruktioner för användning av information protection med dessa program, söka efter **IRM** och programnamn och version.

#### Skydda ett dokument i Word 2013

1.  Skapa ett nytt dokument i Microsoft Word.

2.  Från den **filen** -menyn klickar du på **Info**, klickar du på **Skydda dokument**, klickar du på **begränsa åtkomst**, och välj en mall för att snabbt tillämpa lämpliga användningsrättigheterna, eller välj **begränsa åtkomst** och välj användningsrättigheterna själv.

    > [!NOTE]
    > Om det är första gången du använder Rights Management kan du kontakta den [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] service och uppmanas att ange autentiseringsuppgifter för att konfigurera Office IRM-klienten.

3.  Spara dokumentet.

När andra öppnar dokumentet autentiseras de först. Om de inte har behörighet att öppna dokument, öppnas inte dokumentet. Om de har behörighet att öppna dokument, öppnas med begränsade användningsrättigheterna som har angetts för den aktuella användaren. En användning i skrivskyddat tillåter till exempel inte användaren att redigera eller spara dokument, även om det första kopieras till en annan plats. Användningsrättigheterna visas överst i dokumentet med hjälp av en begränsning banderoll. Banderollen kan visa de behörigheter som tillämpas på dokumentet eller den kan innehålla en länk om du vill visa dem.

#### Skydda ett e-postmeddelande med Outlook 2013 och Exchange Online

1.  Skapa ett nytt e-postmeddelande till en mottagare i din organisation i Outlook.

2.  Från den **alternativ** klickar du på **behörighet**, och sedan välja ett alternativ. Exempel: **Vidarebefordra inte**, **&lt; Företagsnamn &gt; - konfidentiell** eller **&lt; Företagsnamn &gt; - konfidentiell visa**.

3.  Skicka meddelandet.

På samma sätt att visa ett skyddat dokument, autentiseras när mottagarna får e-postmeddelande de först. Om de har behörighet att se e-postmeddelande öppnas med begränsade användningsrättigheterna som har angetts för den aktuella användaren. Exempel: Om du har valt **Vidarebefordra inte**, knappen framåt i menyfliksområdet är inte tillgänglig.

#### Skydda ett e-postmeddelande med Outlook Web App

1.  Skapa ett nytt e-postmeddelande till en mottagare i din organisation i webbprogram Outlook.

2.  Klicka på  **...**,  klickar du på **Ange behörigheter**, och sedan välja ett alternativ. Exempel: **Vidarebefordra inte**, **inte svara alla**, **&lt; Företagsnamn &gt; - konfidentiell** eller **&lt; Företagsnamn &gt; - konfidentiell visa**.

3.  Skicka meddelandet.

På samma sätt att visa ett skyddat dokument, autentiseras när mottagarna får e-postmeddelande de först. Om de har behörighet att se e-postmeddelande öppnas med begränsade användningsrättigheterna som har angetts för den aktuella användaren. Exempel: Om du har valt **gör inte svara alla**,  **Svara alla** alternativet i meddelandefönstret är inte tillgänglig.

## Se även
[Använda Azure Rights Management](../Topic/Using_Azure_Rights_Management.md)

