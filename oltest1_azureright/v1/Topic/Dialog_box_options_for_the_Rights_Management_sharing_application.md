---
description: na
keywords: na
title: Dialog box options for the Rights Management sharing application
search: na
ms.date: na
ms.service: rights-management
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7b91ab30-6363-4929-bcbd-4dfbd05f644a
---
# Dialogrutan f&#246;r delningsapplikation Rights Management
Använda denna information för att ange alternativ i RMS-delning program **Lägg till skydd** dialogrutan eller **Dela skyddat** dialogrutan. Den här dialogrutan visas när du [skydda en fil för att dela](http://technet.microsoft.com/library/dn574735.aspx) eller [skydda en fil på plats](http://technet.microsoft.com/library/dn574733.aspx) och Välj anpassade behörigheter.

> [!IMPORTANT]
> Om de alternativ som visas skiljer sig från dem som dokumenteras här du förmodligen inte den senaste versionen av den delade programmet ska installeras. Du kan hämta den senaste versionen från den [Microsoft Rights Management](http://go.microsoft.com/fwlink/?LinkId=303970) sidan.
> 
> Hur hittar du om du har den senaste versionen? Leta efter **delningsapplikation för Microsoft Rights Management** visas i program och funktioner och kontrollera motsvarande versionsnummer. Om du vill se och använda alternativen i tabellen versionen ska vara minst **1.0.1770.0**. Du kan kontrollera det senaste versionsnumret från hämtningssidan.

Förutom de alternativ som du kan välja kanske du också undrar:

-   [Vad är .ppdf-fil som skapas automatiskt?](../Topic/Dialog_box_options_for_the_Rights_Management_sharing_application.md#BKMK_PPDF)

-   [Vad är skillnaden mellan allmän skydd och inbyggda (intern) skydd?](../Topic/Dialog_box_options_for_the_Rights_Management_sharing_application.md#BKMK_GenericNative)

|Alternativet|Beskrivning|
|----------------|---------------|
|**ANVÄNDARE**|Om du inte redan har angett en e-postadress från Outlook, anger du e-postadresser för de personer som du vill öppna filen.<br /><br />Om din organisation använder den lokala versionen av Rights Management (AD RMS), är e-postadresser som du kan ange begränsad till personer i din organisation. När det gäller, och försök att ange externa e-postadresser, visas ett meddelande om företagskonfigurationen tillåter delning av skyddat innehåll i företaget. Om din organisation använder Azure RMS måste kan följande e-postadresser dock för personer inom organisationen eller för personer i en annan organisation.<br /><br />Exempel: janetm@contoso.com; p.Dover@Fabrikam.com|
|**Allmän skydd**|Om det här alternativet är markerat innebär det att den markerade filen inte kan skyddas program. Mer information finns i. [Vad är skillnaden mellan allmän skydd och inbyggda (intern) skydd?](../Topic/Dialog_box_options_for_the_Rights_Management_sharing_application.md#BKMK_GenericNative) i det här avsnittet.|
|**Viewer – endast**<br /><br />**Granskare – visa och redigera**<br /><br />**Författaren – visa, redigera, kopiera och Skriv ut**<br /><br />**Ägarna – alla behörigheter** **Note:** Dessa alternativ har en runda ikon innan namnet som representerar en världen över hela världen. Den här ikonen används eftersom normalt du välja ett av alternativen när du skickar din koppling till någon i en annan organisation.|Välj något av följande alternativ om du vill ange behörighet för ett skyddat dokument. Klicka på varje alternativ för att visa en beskrivning.<br /><br />När du väljer ett av alternativen endast personerna som du anger i **användare** har du anger för att öppna och använda dokumentet. Till exempel om de vidarebefordra dem till någon annan kan dokumentet inte öppnas.|
|Principmallar som administratören konfigurerar.<br /><br />Om till exempel företagets namn är Contoso AB: **Contoso AB - konfidentiell vy** **Note:** Dessa alternativ har en fyrkant ikon innan namnet som representerar ett office bygga. Den här ikonen används eftersom normalt du välja ett av alternativen när du skickar din koppling till någon i din organisation.|När du delar ett dokument med personer som arbetar för din organisation finns tillgängliga principmallar som administratören konfigurerar. Välj något av följande när dokumentet inte får vara delad utanför organisationen.<br /><br />När du väljer ett av alternativen definierar administratören rättigheter för dokumentet och som kan öppna den.|
|**Går ut dokumenten**|Välj det här alternativet endast för viktiga filer som användarna som du har valt inte ska kunna öppna efter ett datum som du anger. Du kan fortfarande öppna originalfilen men ny (din aktuella tidszon), dag som du anger andra kommer inte kunna öppna filen.<br /><br />Det här alternativet är inte tillgänglig om du väljer en principmall för som administratören konfigurerar.|
|**Mejla mig när någon försöker öppna dokumenten**|**Note:** Det här alternativet är för närvarande i Förhandsgranska.<br />Välj det här alternativet om du vill ta emot e-postaviseringar när någon försöker öppna dokument som du skydda. E-postmeddelandet står som försökte öppna, när och om de har installerats.<br /><br />Det här alternativet är endast tillgänglig om din organisation använder Azure RMS. Om din organisation använder den lokala versionen av Rights Management (AD RMS), visas inte det här alternativet.|
|**Låt mig omedelbart återkalla åtkomst till dessa dokument**|Välj det här alternativet om du kanske behöver återkalla åtkomst till dokumenten senare med hjälp av dokumentet spårning plats och återkallade ska börja gälla. Anger det här alternativet innebär som när dokumentet inte har återkallats, måste användare alltid emellertid Internetanslutning att läsa dokument, varje gång de komma åt den. Det kan finnas vissa situationer där användare kan inte ansluta sin enhet till Internet och användare kan inte läsa dokumentet som du vill.<br /><br />Om du inte väljer det här alternativet om kan du fortfarande återkalla dokumenten senare med hjälp av dokument spårning av webbplatsen. Men eftersom användare inte alltid måste ha en Internetanslutning att läsa dokumentet vet de inte omedelbart att dokument har återkallats och kan fortsätta att läsa den tills de nästa autentiseras med Azure RMS. Det maximala antalet dagar som någon kan fortsätta att läsa ett skyddat dokument som du har återkallats är 30 dagar som standard, men en administratör kan ändra det här värdet ska vara färre eller större än 30 dagar.<br /><br />Det här alternativet är endast tillgänglig om din organisation använder Azure RMS. Om din organisation använder den lokala versionen av Rights Management (AD RMS), visas inte det här alternativet.|

## <a name="BKMK_GenericNative"></a>Vad är skillnaden mellan allmän skydd och inbyggda (intern) skydd?

-   När du **datorverifieringsprocessen skydda en fil**, obehöriga går inte att öppna filen. Men när behöriga användare öppna filen, kan sedan vidarebefordra Borttaget skydd till andra eller spara på en plats som andra kan komma åt. De, men visas ett meddelande om dem vilka behörigheter de har för filen, och de uppmanas att respektera dessa men skyddet kan tillämpas. Dessutom kan du begränsa behörigheterna ytterligare tillstånd när du datorverifieringsprocessen skydda en fil. Till exempel du kan inte begränsa innehållet till skrivskyddat eller inte ut.:

    > [!NOTE]
    > En datorverifieringsprocessen skyddad fil har alltid filnamnstillägget av **.pfile**.

-   I jämförelse när du använder den **inbyggda (intern) protection** av Rights Management med program som har stöd för detta (till exempel Office-filer) skydd gäller fil även om filen skickas till någon annan eller sparas i en annan plats. När du skyddar filerna, du kan också använda begränsade behörigheter som skrivskyddad, eller behörighet att redigera men inte skriva ut eller kopiera. Exempel: du kan välja **Viewer – Visa endast**, så att det inte går att redigera innehållet, skriva ut eller kopiera.

Ytterligare teknisk information finns i [Skydd – intern och allmän](../Topic/Rights_Management_sharing_application_administrator_guide.md#BKMK_LevelsofProtection) under den [Rights Management dela program administratörshandboken](../Topic/Rights_Management_sharing_application_administrator_guide.md).

## <a name="BKMK_PPDF"></a>Vad är .ppdf-fil som skapas automatiskt?

-   När du delar en skyddad fil via e-post (dela skyddat) RMS-delning program automatiskt skapar en **.ppdf** version av filen för Word, Excel, PowerPoint eller PDF. Det här är en skrivskyddad skyddade version av filen som bara behöriga användare kan öppna och det innebär att mottagarna kan alltid läsa bifogad fil, även om de använder en mobil enhet som inte har ett program som ursprungligen har stöd Rights Management. Ger dessa användare har installerat appen RMS-delning kan kommer de att kunna läsa filen.

    I det här fallet, till skillnad från en datorverifieringsprocessen skyddad fil tillämpas användning begränsningen. Mottagaren kommer inte att kunna spara den här versionen av filen och om de vidarebefordrar dem till någon annan ursprungliga begränsningar kvar med dokumentet. Personer som har behörighet att skyddat dokument kommer att kunna öppna den.

    > [!NOTE]
    > En .ppdf-fil skapas automatiskt när du dela skyddade (dela via e-post) men inte skapas när du skydda på plats.

## Exempel och andra instruktioner
Exempel på hur du kan använda den Rights Management dela program och instruktioner finns i följande avsnitt från Rights Management delning application användaren guide:

-   [Exempel på hur RMS-delning program](../Topic/Rights_Management_sharing_application_user_guide.md#BKMK_SharingExamples)

-   [Vad vill du göra?](../Topic/Rights_Management_sharing_application_user_guide.md#BKMK_SharingInstructions)

## Se även
[Rights Management delning användaren guide till](../Topic/Rights_Management_sharing_application_user_guide.md)

