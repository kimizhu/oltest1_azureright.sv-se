---
description: na
keywords: na
title: Operations for Your Azure Rights Management Tenant Key
search: na
ms.date: na
ms.service: rights-management
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1284d0ee-0a72-45ba-a64c-3dcb25846c3d
---
# &#197;tg&#228;rder f&#246;r din Azure Rights Management-klient nyckel
Beroende på innehavaren nyckel topologin (hanteras av Microsoft eller hanteras av kunden) har olika nivåer av kontroll och ansvar för din Microsoft Azure Rights Management (Azure RMS) innehavaren nyckel när den används.

Detta kallas ofta att som en egen nyckel (BYOK) när du hanterar innehavaren nyckeln. Mer information om det här scenariot och hur du välja mellan två innehavaren nyckel topologier finns [Planera och implementera din Azure Rights Management innehavaren nyckel](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md).

I följande tabell anges vilka åtgärder som du kan göra beroende på miljön som du har valt för din Azure RMS-klient-nyckel.

|Livscykel åtgärden|Hanteras av Microsoft (standard)|Hanteras av kunden (BYOK)|
|----------------------|------------------------------------|-----------------------------|
|Återkalla klient-nyckel|Ingen (automatisk)|Ingen (automatisk)|
|Nytt nyckel klient-nyckel|Ja|Ja|
|Säkerhetskopiera och återställa klient-nyckel|Nej|Ja|
|Exportera klient-nyckel|Ja|Nej|
|Svara på en överträdelse|Ja|Ja|
När du har identifierat vilka topologi som du har implementerat med någon av följande avsnitt för mer information om dessa åtgärder för din Azure RMS-klient-nyckel.

## <a name="BKMK_MSManagedOperations"></a>Microsoft hanteras: Innehavaren nyckel livscykel operations
Om Microsoft hanterar klient-nyckel för Azure Rights Management (standard), kan du använda följande avsnitt för mer information om hur livscykel som är relevanta för den här topologin:

-   [Återkalla klient-nyckel](../Topic/Operations_for_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_MSRevoke)

-   [Nytt nyckel klient-nyckel](../Topic/Operations_for_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_MSRekey)

-   [Säkerhetskopiera och återställa klient-nyckel](../Topic/Operations_for_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_MSBackup)

-   [Exportera klient-nyckel](../Topic/Operations_for_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_MSExport)

-   [Svara på en överträdelse](../Topic/Operations_for_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_MSBreach)

### <a name="BKMK_MSRevoke"></a>Återkalla klient-nyckel
När du slutar prenumerera på Azure RMS Azure RMS slutar med klient-nyckel och ingen åtgärd krävs från dig.

### <a name="BKMK_MSRekey"></a>Nytt nyckel klient-nyckel
Nya nycklar kallas även rullande nyckeln. Inte igen nyckel klient-nyckeln om det inte är verkligen behövs. Äldre klienter, till exempel Office 2010 har inte konstruerade för att hantera viktiga ändringar skalas. I detta fall måste du radera RMS tillstånd på datorer med hjälp av en grupprincip eller ett motsvarande mekanism. Det finns vissa tillförlitligt händelser som kan göra så att du nyckeln klient-nyckeln igen. Exempel:

-   Ditt företag har delat i två eller flera företag. När du nyckel klient-nyckeln igen, har inte tillgång till nytt innehåll som dina anställda publicera det nya företaget. De får tillgång till gamla innehållet om de har en kopia av nyckeln gamla innehavaren.

-   Du tror master kopian av din innehavaren nyckel (kopiera din innehar) har äventyras.

Du kan nyckel klient-nyckeln igen genom att anropa Microsoft kundservice (CSS) och bevisa att du är Innehavaradministratör.

När du nyckel klient-nyckeln igen, skyddad nytt innehåll med hjälp av nyckeln innehavaren. Det här inträffar på ett sätt som fasindelad så för en viss tidsperiod vissa nytt innehåll kommer att fortsätta att skyddas med nyckeln gamla innehavaren. Skyddat innehåll ligger tidigare skyddade till din gamla innehavaren nyckel. För att stödja scenariot behåller Azure RMS gamla innehavaren nyckeln så att den kan utfärda licenser för gamla innehåll.

### <a name="BKMK_MSBackup"></a>Säkerhetskopiera och återställa klient-nyckel
Microsoft ansvarar för att säkerhetskopiera klient-nyckeln och ingen åtgärd krävs från dig.

### <a name="BKMK_MSExport"></a>Exportera klient-nyckel
Du kan exportera dina Azure RMS-konfiguration och innehavaren nyckel genom att följa instruktionerna i följande tre steg:

##### Steg 1: Initiera export

-   Kontakta Microsoft Customer Service Support (CSS) om du vill göra detta. Du måste bekräftar du är administratör för Azure RMS-klient.

##### Steg 2: Vänta för verifiering

-   Microsoft kontrollerar att din förfrågan till din RMS-klient-tangenten är tillförlitligt. Den här processen kan ta upp till tre veckor.

##### Steg 3: Ta emot viktiga instruktioner från CSS

-   Microsoft kundservice (CSS) skickar din Azure RMS-konfiguration och innehavaren nyckel som krypterade i en fil som har filnamnstillägget .tpd lösenord. Om du vill göra det skickar CSS först (som den person som initierat exporten) ett verktyg via e-post. Du måste köra verktyget från en kommandotolk på följande sätt:

    ```
    AadrmTpd.exe -createkey
    ```
    Detta genererar ett RSA-nyckelpar och sparar offentliga och privata hälften som filer i den aktuella mappen. Exempel: **PublicKey-FA29D0FE-5049-4C8E-931B-96C6152B0441.txt** och **PrivateKey-FA29D0FE-5049-4C8E-931B-96C6152B0441.txt**.

    Svara på e-postmeddelandet från CSS, bifoga filen som har ett namn som börjar med **PublicKey**. CSS nästa skickar en betrodda Publiceringsdomänen-fil som en XML-fil som krypteras med RSA-nyckel. Kopiera filen till samma mapp som du har kört verktyget AadrmTpd ursprungligen och köra verktyget igen med hjälp av filen som börjar med **PrivateKey** och CSS-filen. Exempel:

    ```
    AadrmTpd.exe -key PrivateKey-FA29D0FE-5049-4C8E-931B-96C6152B0441.txt -target TPD-77172C7B-8E21-48B7-9854-7A4CEAC474D0.xml
    ```
    Utdata från det här kommandot ska vara två filer: En innehåller lösenord för den lösenordsskyddat betrodda Publiceringsdomänen och den andra är den betrodda som lösenordsskyddat av Publiceringsdomänen och sig själv. Båda måste ha samma GUID som offentliga och privata nycklar filer från när du körde kommandot AadrmTpd.exe - createkey för korsreferenser syfte:

    -   Password-FA29D0FE-5049-4C8E-931B-96C6152B0441.txt

    -   ExportedTPD-FA29D0FE-5049-4C8E-931B-96C6152B0441.xml

    Säkerhetskopiera dessa filer och lagrar dem på ett säkert sätt att se till att du kan fortsätta att dekryptera innehåll som skyddas med den här innehavaren nyckel. Om du migrerar till AD RMS kan du dessutom importera filen betrodda Publiceringsdomänen (filen som börjar med **ExportedTDP**) till AD RMS-server.

##### Steg 4: Pågående: Skydda din klient-nyckel

-   När du har fått klient-nyckel hålla väl skyddad eftersom om någon får tillgång till den de dekryptera alla dokument som skyddas med hjälp av nyckeln.

    Om orsaken till att exportera klient-nyckeln är eftersom du inte längre vill använda Azure RMS som bästa praxis, inaktivera nu RMS-klient. Fördröjning inte göra detta när du har fått klient-nyckel eftersom denna försiktighetsåtgärd hjälper minimera konsekvenserna om din innehavaren nyckeln används av någon som inte ska ha. Instruktioner finns i [Inaktivering och inaktivera Azure Rights Management](../Topic/Decommissioning_and_Deactivating_Azure_Rights_Management.md).

### <a name="BKMK_MSBreach"></a>Svara på en överträdelse
Ingen säkerhetssystem, oavsett hur stark har slutförts utan en överträdelse svar process. Klient-nyckeln kan skadas eller blir stulen. Även om den är väl skyddad väl, kan säkerhetsrisk hittas i aktuell HSM teknik eller aktuella nyckellängd och algoritmer.

Microsoft har en särskild grupp kan svara på säkerhet incidenter i sina produkter och tjänster. Så snart en trovärdig rapport om en incident är aktiverar team att undersöka omfattningen, grundläggande orsaken och ändringarna som orsakas av. Om incidenten påverkar dina tillgångar, sedan meddelar Microsoft din Azure RMS-klient administratörer via e-post med hjälp av adressen som du angav när du prenumererar på.

Om du har en överträdelse bästa åtgärd du eller Microsoft kan ta är beroende av omfattningen för överträdelse. Microsoft kommer att fungera med dig via den här processen. I följande tabell visas några vanliga situationer och sannolika svaret, även om exakt svaret beror på den information som visas i undersökningen.

|Incident beskrivning|Sannolika svar|
|------------------------|------------------|
|Klient-nyckeln är känd.|Nytt nyckel klient-nyckel. Finns det [Nytt nyckel klient-nyckel](../Topic/Operations_for_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_MSRekey) i det här avsnittet.|
|En obehörig person eller skadlig kod har rättigheter att använda klient-nyckel men själva nyckeln läcker inte.|Nya nycklar klient-nyckel hjälper inte här och kräver Rotorsaksanalys. Om en process eller ett program bugg var ansvarig för obehörig person att få tillgång till måste denna situation vara löst.|
|Att bli ur möjligt säkerhetsproblem har identifierats i RSA-algoritm eller nyckellängd eller intrång attacker.|Microsoft måste uppdatera Azure RMS för att stödja nya algoritmer och längre nyckellängd som är flexibel och att alla kunder att förnya sina innehavaren nycklar.|

## <a name="BKMK_BYOKManagedOperations"></a>Kunden hanteras: Innehavaren nyckel livscykel operations
Om du hanterar klient-nyckel för Azure Rights Management (se till att ditt eget nyckel eller BYOK, scenario), använda följande avsnitt för mer information om hur livscykel som är relevanta för den här topologin:

-   [Återkalla klient-nyckel](../Topic/Operations_for_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_BYOKRevoke)

-   [Nytt nyckel klient-nyckel](../Topic/Operations_for_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_BYOKRekey)

-   [Säkerhetskopiera och återställa klient-nyckel](../Topic/Operations_for_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_BYOKBackup)

-   [Exportera klient-nyckel](../Topic/Operations_for_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_BYOKExport)

-   [Svara på en överträdelse](../Topic/Operations_for_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_BYOKBreach)

### <a name="BKMK_BYOKRevoke"></a>Återkalla klient-nyckel
När du slutar prenumerera på Azure RMS Azure RMS slutar med klient-nyckel och ingen åtgärd krävs från dig.

### <a name="BKMK_BYOKRekey"></a>Nytt nyckel klient-nyckel
Nya nycklar kallas även rullande nyckeln. Inte igen nyckel klient-nyckeln om det inte är verkligen behövs. Äldre klienter, till exempel Office 2010 har inte konstruerade för att hantera viktiga ändringar skalas. I detta fall måste du radera RMS tillstånd på datorer med hjälp av en grupprincip eller ett motsvarande mekanism. Det finns vissa tillförlitligt händelser som kan göra så att du nyckeln klient-nyckeln igen. Exempel:

-   Ditt företag har delat i två eller flera företag. När du nyckel klient-nyckeln igen, har inte tillgång till nytt innehåll som dina anställda publicera det nya företaget. De får tillgång till gamla innehållet om de har en kopia av nyckeln gamla innehavaren.

-   Du tror master kopian av din innehavaren nyckel (kopiera din innehar) har äventyras.

När du nyckel klient-nyckeln igen, skyddad nytt innehåll med hjälp av nyckeln innehavaren. Det här inträffar på ett sätt som fasindelad så för en viss tidsperiod vissa nytt innehåll kommer att fortsätta att skyddas med nyckeln gamla innehavaren. Skyddat innehåll ligger tidigare skyddade till din gamla innehavaren nyckel. För att stödja scenariot behåller Azure RMS gamla innehavaren nyckeln så att den kan utfärda licenser för gamla innehåll.

Om du vill återaktivera nyckel klient-nyckel, generera och skapa en ny nyckel via Internet eller person, med hjälp av procedurerna i den [Implementing bring your own key (BYOK)](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_ImplementBYOK) avsnitt från den [Planera och implementera din Azure Rights Management innehavaren nyckel](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md) ämne.

### <a name="BKMK_BYOKBackup"></a>Säkerhetskopiera och återställa klient-nyckel
Du är ansvarig för att säkerhetskopiera klient-nyckel. Om du genererade klient-nyckel i en Thales HSM om du vill säkerhetskopiera nyckeln kan bara säkerhetskopiera filen Tokeniserad nyckel, filen världen och administratören kort.

Om du överförde nyckeln genom att följa instruktionerna i den [Implementing bring your own key (BYOK)](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_ImplementBYOK) avsnitt från den [Planera och implementera din Azure Rights Management innehavaren nyckel](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md) uppslaget Azure RMS kvar Tokeniserad nyckel filen skydd mot fel på några Azure RMS-noder. Dock anser att en fullständig säkerhetskopia. Exempel: Om du behöver en oformaterade kopia av nyckeln för att använda utanför en Thales HSM Azure RMS kommer inte att kunna hämta du eftersom den endast har en oåterkalleligt kopia.

### <a name="BKMK_BYOKExport"></a>Exportera klient-nyckel
Om du använder BYOK kan du exportera klient-nyckel från Azure RMS. Kopiera i Azure RMS är oåterkalleligt borta. Kontakta Microsoft Customer Service Support (CSS) om du vill ta bort den här nyckeln så att den inte längre kan användas.

### <a name="BKMK_BYOKBreach"></a>Svara på en överträdelse
Ingen säkerhetssystem, oavsett hur stark har slutförts utan en överträdelse svar process. Klient-nyckeln kan skadas eller blir stulen. Även om den är väl skyddad väl, kan säkerhetsrisk hittas i aktuell HSM teknik eller aktuella nyckellängd och algoritmer.

Microsoft har en särskild grupp kan svara på säkerhet incidenter i sina produkter och tjänster. Så snart en trovärdig rapport om en incident är aktiverar team att undersöka omfattningen, grundläggande orsaken och ändringarna som orsakas av. Om incidenten påverkar dina tillgångar, sedan meddelar Microsoft din Azure RMS-klient administratörer via e-post med hjälp av adressen som du angav när du prenumererar på.

Om du har en överträdelse bästa åtgärd du eller Microsoft kan ta är beroende av omfattningen för överträdelse. Microsoft kommer att fungera med dig via den här processen. I följande tabell visas några vanliga situationer och sannolika svaret, även om exakt svaret beror på den information som visas i undersökningen.

|Incident beskrivning|Sannolika svar|
|------------------------|------------------|
|Klient-nyckeln är känd.|Nytt nyckel klient-nyckel. Finns det [Nytt nyckel klient-nyckel](../Topic/Operations_for_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_BYOKRekey) i det här avsnittet.|
|En obehörig person eller skadlig kod har rättigheter att använda klient-nyckel men själva nyckeln läcker inte.|Nya nycklar klient-nyckel hjälper inte här och kräver Rotorsaksanalys. Om en process eller ett program bugg var ansvarig för obehörig person att få tillgång till måste denna situation vara löst.|
|Problem som identifieras i aktuellt generations HSM teknik.|Microsoft måste uppdatera HSM. Om det finns skäl att tro att problemet exponeras nycklar, be Microsoft alla kunder att förnya sina innehavaren nycklar.|
|Att bli ur möjligt säkerhetsproblem har identifierats i RSA-algoritm eller nyckellängd eller intrång attacker.|Microsoft måste uppdatera Azure RMS för att stödja nya algoritmer och längre nyckellängd som är flexibel och att alla kunder att förnya sina innehavaren nycklar.|

## Se även
[Använda Azure Rights Management](../Topic/Using_Azure_Rights_Management.md)

