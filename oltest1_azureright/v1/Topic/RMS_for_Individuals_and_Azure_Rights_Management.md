---
description: na
keywords: na
title: RMS for Individuals and Azure Rights Management
search: na
ms.date: na
ms.service: rights-management
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2efcb440-fefd-45e9-872b-f471573aadf2
---
# RMS f&#246;r personer och Azure Rights Management
RMS för personer är en kostnadsfri prenumeration för självbetjäning för användare i en organisation som har skickats känsliga filer har skyddats med Microsoft Azure Rights Management (Azure RMS), men de kan inte verifieras eftersom deras IT-avdelningen inte hanterar ett konto för dem i Azure. IT-avdelningen inte har Office 365 eller använda Azure-tjänster.

Dessa användare kan registrera dig för en gratis arbetet eller skolan konto med Azure RMS och hämta och installera delningsapplikation Rights Management. Dessa användare kan därför nu autentisera för att bevisa att de är den person som skyddade filer har skickats till och läsa skyddade filer på datorer eller mobila enheter.

Med den Rights Management delning på Windows-datorer, kan dessa användare också skydda filer på plats eller skicka skyddade filer med e-post till användare i eller utanför deras organisation. Om mottagare av e-post som de skickar finns i en organisation som också inte hanterar användarkonton i Azure, kan de för registrera dig för en RMS för enskilda konto att läsa den skyddade e-postmeddelande.

> [!IMPORTANT]
> Den här kostnadsfria prenumerationen garanterar att behöriga användare kan alltid läsa filer har skyddats. För närvarande kan du kan även använda den här kostnadsfria prenumerationen för att skydda dokument och skapa nya skyddade e-postmeddelanden, men möjligheten att skapa nya skyddat innehåll är avsedd för utvärderingsversion användning och kan tas bort i framtiden. Mer information och ändringar som använder RMS för att skydda innehållet finns i [Microsoft Rights Management användarvillkoren](https://portal.aadrm.com/Legal/Service).

Mer information om hur du kan skydda filer med hjälp av den kostnadsfria delningsapplikation Rights Management finns på [Rights Management dela program guide för användare](http://technet.microsoft.com/library/dn339006.aspx).

RMS för personer som är ett exempel på en självservice anmälan som stöds av Azure Active Directory. Mer information om hur det fungerar, se [Vad är Self-Service registrering för Azure?](https://azure.microsoft.com/documentation/articles/active-directory-self-service-signup/) i Microsoft Azure-dokumentationen. Använd följande avsnitt för mer information som är specifik för RMS för:

-   [Hur användarna logga för RMS för personer](../Topic/RMS_for_Individuals_and_Azure_Rights_Management.md#BKMK_SignUp)

    -   [Teknisk översikt](../Topic/RMS_for_Individuals_and_Azure_Rights_Management.md#BKMK_TechnicalOverview)

-   [Hur administratörer kan styra konton som skapats för RMS för personer](../Topic/RMS_for_Individuals_and_Azure_Rights_Management.md#BKMK_TakeControlofAccounts)

-   [Hur du tar reda på om dina användare har registrerat för RMS personer](#BKMK_Detect)

## <a name="BKMK_SignUp"></a>Hur användarna logga för RMS för personer
Om du vill registrera dig för den här kostnadsfria konto på begäran genom att besöka den [Microsoft Rights Management sidan](https://portal.aadrm.com/), och tillhandahålla arbetet eller skolan e-postadress. Det vanligaste sättet att du ska dirigeras till den här registrera sidan är om du har fått ett e-postmeddelande med en bifogad fil skyddade som innehåller instruktioner för hur att registrera. Du får ett e-postmeddelande i svaret från Microsoft och kan sedan fylla i registreringsprocessen genom att ange information om du vill skapa ett konto. När du får ett e-postmeddelande från Microsoft skickas denna sista e-postmeddelande till en sida där du kan hämta dela program för olika enheter och en länk till guiden användare.

#### Logga för RMS för personer

1.  Med hjälp av en Windows- eller Mac-dator, gå till den [Microsoft Rights Management sidan](https://portal.aadrm.com).

2.  Ange e-postadress som du använder för din organisation som **janetm@contoso.com** eller **p.dover@fabrikam.com**.

    > [!IMPORTANT]
    > Personliga e-postkonton stöds inte, så att inte ange ett Microsoft-konto (tidigare känt som Microsoft Live ID-konto) eller en annan kontoinformation som du kan använda hemma från Internet-leverantör.

3.  Klicka på **börja**.

    Microsoft använder din e-postadress för att kontrollera om din organisation redan har en [betald prenumeration som innehåller Azure RMS](https://technet.microsoft.com/library/dn655136.aspx). Om så är fallet behöver du inte RMS för personer så att du ska vara inloggad omedelbart och självservice registreringssidan för RMS för personer har avbrutits. Om en betald prenumeration för Azure RMS inte påträffas, ska du fortsätta till nästa steg.

4.  Vänta tills en bekräftelse e-postmeddelande skickas till den adress som du har angett. Det är från Microsoft (DoNotReply@microsoft.com) och har ämne **Microsoft RMS**.

5.  När du tar emot e-postmeddelandet klickar du på länken i instruktionerna för att slutföra registreringen.

6.  Länken öppnar en ny **Microsoft Rights Management** sida där du kan ange information för ditt konto. Skriva in ditt förnamn, efternamn, ange och bekräfta ett lösenord för ditt val, Välj ditt land (eller närmaste land till din om ditt land inte visas) i listrutan och klicka sedan på **skapa**.

7.  Vänta tills en annan e-postmeddelande från Microsoft som nu bekräftar att ditt konto är redo att användas.

8.  Klicka på länken om du vill logga in och läsa anvisningarna för att hämta och installera programmet delning eller klicka på länken Hjälp om du vill läsa delning application användaren guide när du tar emot e-postmeddelandet.

Du är redo att starta skydda filer och läsa filer som andra har skyddat nu ditt konto har skapats. När du uppmanas att logga in för att skydda eller läsa skyddade filer, ange din e-postadress och lösenord som användes för att skapa kontot för RMS för personer.

### <a name="BKMK_TechnicalOverview"></a>Teknisk översikt
RMS för personer som använder en självservice registreringen som också används av andra tjänster som använder Microsoft molnbaserade teknik för att autentisera användare.

Detta är vad som händer i bakgrunden när en användare loggar för RMS för personer och deras organisation inte har en Office 365-prenumeration eller Azure-prenumeration, och därför ingen katalog i Azure för att autentisera användare:

1.  När den första användaren från en organisation begär en prenumeration för RMS för personer, kontrolleras domännamnet i deras e-postadress för att se om den redan är associerad med en Azure-klient. Om det finns inga befintliga innehavaren, skapas automatiskt en ny klient och Azure katalog för den organisation som innehåller ett konto för den här första användaren. Till skillnad från med en betald prenumeration för Azure, är första kontot inte en global administratör, men en vanlig användare. Det nya kontot använder e-postadress och lösenord som användaren har angett.

    > [!NOTE]
    > Vissa domännamn kan inte användas för att skapa katalogen och därför kan inte användas för RMS för personer. Lista över blockerade domännamn kan visas från filen JavaScript objekt format: [http://portal.aadrm.com/content/blocked_domains.json](http://portal.aadrm.com/content/blocked_domains.json)

    Om en befintlig klient hittas kontrolleras den för att se om det redan finns en prenumeration för Azure RMS. När det finns ingen prenumeration, kan ledigt RMS för enskilda prenumerationen läggas till.

2.  Organisationen beviljas RMS för enskilda prenumerationen. Nu kan kan användaren kan autentisera med Azure skydda filer och läsa filer som andra har skyddat med Azure Rights Management. Om du vill skydda och läsa skyddade filer måste användaren ha ett RMS-enlightened program, till exempel en kostnadsfri [delningsapplikation Rights Management](https://technet.microsoft.com/library/dn919648.aspx).

3.  När den andra användaren från samma organisation begär ett RMS för enskilda prenumeration, läggs ett nytt konto till skapats tidigare Azure katalogen med organisationens RMS för enskilda prenumeration. Den här andra användare kan göra allt som skulle kunna göra för den första användaren (skydda filer och läsa skyddade filer), men dessutom dessa två användare kan nu mer enkelt samarbeta eftersom de snabbt kan använda standardmallar för filer med begränsad åtkomst till konton i organisationens Azure directory.

4.  Följande användare från samma organisation följer samma mönster att lägga till användarkonton (när nya användare loggar) organisationens Azure katalogen. Fler konton som läggs till katalogen fler användare kan samarbeta säkert med kollegor och partner och mer läsa sina filer när de inte ska ha åtkomst till dem lätt att obehöriga.

Hela processen finns utan kostnad på organisationen och inget arbete från IT-avdelningen. IT-avdelningen kan dock välja att göra något av följande:

-   **Hantera konton och registreringen**: IT-administratörer kan bli ägare av automatiskt skapade katalogen och konton i Azure. De kan sedan hantera konton genom att implementera directory-integrering lösningar, till exempel Lösenordssynkronisering och enkel inloggning. Eller de kan hindra användare från att skapa konton eller registrerar sig för RMS för personer.

    Mer information finns i följande avsnitt [Hur administratörer kan styra konton som skapats för RMS för personer](../Topic/RMS_for_Individuals_and_Azure_Rights_Management.md#BKMK_TakeControlofAccounts).

-   **Hantera Rights Management**: IT-administratörer kan konvertera RMS för enskilda prenumerationen för organisationen till en betald prenumeration som innehåller Azure Rights Management. När de gör det bevaras befintliga Azure katalogen och konton för en smidig övergång för befintliga användare som använder RMS för personer. Alla filer som användare skyddade tidigare fortfarande skyddas med samma principer och de personer att de behörighet att använda filerna som fortfarande kommer att kunna använda filerna på samma sätt.

    När du gå kursen för åtgärden, förmånerna med din organisation genom att integrera dess arbetsflöden, tjänster och datalager Rights Management. Dessutom kan du nu hantera Rights Management eftersom du har kontroll över din organisation innehavaren nyckel för Azure Rights Management. Du kan nu göra följande:

    -   Konfigurera Exchange och SharePoint för att stödja Azure Rights Management, även om de körs lokalt. Exchange- och SharePoint stöds för onlinetjänster och de stöds av en koppling för lokala servrar. Mer information finns i följande avsnitt:

        -   Avsnitten Exchange Online och SharePoint Online från [Office 365: Konfiguration för klienter och de onlinetjänster](../Topic/Configuring_Applications_for_Azure_Rights_Management.md#BKMK_O365) i den [Konfigurera program för Azure Rights Management](../Topic/Configuring_Applications_for_Azure_Rights_Management.md) ämne

        -   [Distribuera Azure Rights Management-koppling](../Topic/Deploying_the_Azure_Rights_Management_Connector.md)

    -   Utföra e-identifiering för ägs av företagets data så att du kan, om det behövs att dekryptera filer är skyddade med Rights Management. Mer information finns i [Konfigurera Super Users för Azure Rights Management och identifiering av tjänster eller återställning av Data](../Topic/Configuring_Super_Users_for_Azure_Rights_Management_and_Discovery_Services_or_Data_Recovery.md).

    -   Logga all aktivitet för Rights Management som används i din organisation. Detta är mycket kraftfull eftersom inte bara kan du övervaka vilka filer skyddas och som har åtkomst till skyddade filer, men du kan också identifiera eventuellt misstänkt beteende från obehöriga som försöker få åtkomst till skyddade filer. Mer information finns i [Loggning och analysera Azure Rights Management användning](../Topic/Logging_and_Analyzing_Azure_Rights_Management_Usage.md).

    -   Ge användare möjlighet att spåra och återkalla dokumenten skyddade om dessa funktioner som stöds av din [Azure RMS-prenumeration](https://technet.microsoft.com/dn858608). Mer information finns i  [Spåra och återkalla filer](https://technet.microsoft.com/library/dn986611.aspx) från den [RMS-delning användaren guide till](https://technet.microsoft.com/library/dn339006.aspx).

    -   Implementera en ta ditt eget nyckel lösning (BYOK) så att din innehavaren nyckel för Azure Rights Management genererade lokalt enligt dina IT-principer och säker överförs till Microsoft genom att använda maskinvara säkerhet modulen (HSM). Mer information finns i [Planera och implementera din Azure Rights Management innehavaren nyckel](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md).

## <a name="BKMK_TakeControlofAccounts"></a>Hur administratörer kan styra konton som skapats för RMS för personer
Om du inte vill konvertera organisationens RMS för enskilda prenumerationen till en betald prenumeration kan du fortfarande styra användarkonton i Azure katalogen som har skapats för din organisation på följande sätt:

-   Implementera directory-integrering lösningar för Azure Active Directory och Active Directory DS-infrastruktur. Du kan synkronisera konton och lösenord så att användare inte skapa nya konton om du vill använda Rights Management och din lokala lösenordsprinciper gäller för nya Azure användarkonton. Du kan också synkronisera lösenord så att användare inte behöver ett annat lösenord om du vill använda Rights Management.

-   Du kan hindra användare från att logga på använder Azure Rights Management med RMS för enskilda prenumeration. I de flesta fall finns liten nytta i detta eftersom användare antingen delar filer utan skydd (som kan medföra ditt företag risker) eller använder en annan fil protection mekanism som inte har IT-avdelningen med alternativet för att komma åt data. Men om du vill hindra användare från att logga på använda RMS för enskilda gör något av följande när du har blivit ägare till organisationens katalog i Azure:

    -   Förhindra att registrerar sig för självbetjäning prenumerationer som innehåller RMS för alla användare.  För närvarande kan kan inte du ange av tjänsten. inställningen gäller för alla Azure prenumerationer som använder Self service-processen. Genom att ange den **AllowAdHocSubscriptions** parametern false med den [mängd MsolCompanySettings](http://technet.microsoft.com/library/dn194127.aspx) cmdlet från Windows PowerShell-modul för Azure Active Directory. Exempel: **Set-MsolCompanySettings -AllowAdHocSubscriptions $false**

    -   Hindra användare från att skapa ett nytt konto i Azure, vilket innebär att endast användare som redan har ett konto i Azure kan registrera dig för självbetjäning prenumerationer, som innehåller RMS för personer.  Genom att ange den **AllowEmailVerifiedUsers** parametern false med den [mängd MsolCompanySettings](http://technet.microsoft.com/library/dn194127.aspx) cmdlet från Windows PowerShell-modul för Azure Active Directory. Exempel: **Set-MsolCompanySettings -AllowEmailVerifiedUsers $false -AllowAdHocSubscriptions $true**

    -   Synkronisera Active Directory DS-infrastruktur med Azure Active Directory. Den här åtgärden förhindrar att nya konton skapas när användare registrera dig för självbetjäning prenumerationer som RMS för personer, och du kan ta bort eller inaktivera konton som skapats tidigare i Azure-katalogen.

Styra användarkonton i Azure katalogen eller hindra användare från att registrerar sig för RMS för måste du ha någon Azure-prenumeration och äger katalogen. Om du inte redan har en Azure-prenumeration kan få du ett utan kostnad. Om en katalog har skapats automatiskt för dig under processen Self service, bli ägare till den domän som användes för att skapa den. Om du redan har en katalog i Azure men användare anges en ny domän som du använder i din organisation, koppla domänen till den befintliga katalogen. Mer information finns i instruktionerna i [Vad är Self-Service registrering för Azure?](https://azure.microsoft.com/documentation/articles/active-directory-self-service-signup/)

## <a name="BKMK_Detect"></a>Hur du tar reda på om dina användare har registrerat för RMS personer
Som administratör hur du vet om användarna har registrerat dig för RMS för? Du kan använda någon eller en kombination av följande metoder:

-   Be användaren hur de skydda strikt konfidentiell filer, särskilt när samarbeta med andra utanför organisationen.

-   När du har en Azure-prenumeration för din organisation kan du använda den [Get-MsolAccountSku](https://msdn.microsoft.com/library/azure/dn194118.aspx) cmdlet om du vill se **RIGHTSMANAGEMENT_ADHOC** returneras som en av abonnemang. Om det är är det här RMS för enskilda prenumeration som har beviljats på organisationen med en pool med aktiva enheter som är tillgängliga för användare använder självservice registreringsprocessen.

-   Använd system-hanteringslösning, till exempel System Center Configuration Manager för inventering av programvaran och programvara som används. Delningsapplikation Rights Management körs med hjälp av den **ipviewer.exe** program och du kan [Hämta och installera programmet](http://go.microsoft.com/fwlink/?LinkId=303970) kostnadsfritt för att identifiera andra egenskaper om det här programmet som du sedan använder för programvaruinventering.

-   Vara uppmärksam filnamnstillägg som skapas av Rights Management dela program. .Pfile och .ppdf filnamnstillägg är de vanligaste exemplen, men det finns andra filer som kan ändra sina filnamnstillägg när de program skyddas av Rights Management. Mer information finns i [stöds filtyper och filnamnstillägg](http://technet.microsoft.com/library/dn339003.aspx) under den [Rights Management dela program administratörshandboken](http://technet.microsoft.com/library/dn339003.aspx).

## Se även
[Kom igång med Azure Rights Management](../Topic/Getting_Started_with_Azure_Rights_Management.md)

