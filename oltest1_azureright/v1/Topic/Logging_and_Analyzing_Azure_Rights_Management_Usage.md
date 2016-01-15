---
description: na
keywords: na
title: Logging and Analyzing Azure Rights Management Usage
search: na
ms.date: na
ms.service: rights-management
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a735f3f7-6eb2-4901-9084-8c3cd3a9087e
---
# Loggning och analysera Azure Rights Management anv&#228;ndning
Använd informationen i det här avsnittet för att förstå hur du kan använda användning loggar med Azure Rights Management (Azure RMS). Azure Rights Management-tjänsten kan logga varje begäran att den gör för din organisation, bland annat förfrågningar från användare, åtgärder som utförs av Rights Management administratörer i din organisation och åtgärder som utförs av Microsoft operatörer att stödja distribution av Azure Rights Management.

Du kan sedan använda loggarna Azure Rights Management business följande scenarier:

-   Analysera för business insikter.

    Azure Rights Management skriver loggar i utökat loggfilsformat för W3C i ett Azure storage-konto som du anger. Du kan sedan instruera loggarna i en databas i valfri (till exempel en databas, ett system för online analytical processing (OLAP), eller en karta minska system) att analysera informationen och skapa rapporter. Exempelvis kan du identifiera vem som har åtkomst till din RMS-skyddade data. Du kan se vad RMS-skyddade data personer använder, och från vilka enheter och var. Du kan ta reda om personer har kan läsa skyddat innehåll. Du kan också identifiera vilka användare har läst viktiga dokument som var skyddad.

-   Övervaka missbruk.

    Azure Rights Management loggningsinformation finns tillgängliga i närheten-realtid, så att du kan övervaka företagets användning av Rights Management kontinuerligt. 99,9% av loggar finns inom 15 minuter en RMS-initierade åtgärd.

    Du kanske vill bli aviserad om det finns en plötslig ökning av läsa RMS-skyddade data utanför standard arbetstid, vilket kan tyda på att en obehörig användare samlar in information för att sälja till konkurrenter. Eller, om samma användare program som verkar vara kommer åt data från två olika IP-adresser inom en kort tidsperiod, som kan indikera att ett användarkonto har komprometterats.

-   Utföra kriminalteknisk analys.

    Om du har en minnesläcka information kan du bli ombedd som nyligen har använt specifika dokument och vilken information som ett misstänkt person åtkomst till nyligen. Du kan svara här typen av frågor när du använder Azure Rights Management och loggning eftersom personer som använder skyddat innehåll måste alltid få en Rights Management-licens för att öppna dokument och bilder som skyddas av Azure Rights Management, även om de här filerna flyttas via e-post eller kopieras till USB-enheter eller andra lagringsenheter. Det innebär att du kan använda Azure Rights Management loggar som en slutgiltig informationskälla för kriminalteknisk analys när du skyddar dina data med Azure Rights Management.

> [!NOTE]
> Om du är intresserad av i loggning av administrativa uppgifter för Azure Rights Management och gör inte vill spåra hur användare använder Rights Management kan du använda den [Get-AadrmAdminLog](https://msdn.microsoft.com/library/azure/dn629430.aspx) Windows PowerShell-cmdlet för Azure Rights Management.
> 
> Du kan också använda Azure-portalen för utförlig användningsrapporter som innehåller **RMS användning**, **mest aktiva RMS användare**, **användning av RMS enhet**, och **RMS-aktiverade program som körs på**. Klicka på för att komma åt de här rapporterna från Azure-portalen **Active Directory**, Välj och öppna en katalog och klicka sedan på **rapporter**,

Använd följande avsnitt för mer information om loggning för användning av Azure Rights Management.

-   [Så här aktiverar du loggning för användning av Azure Rights Management](../Topic/Logging_and_Analyzing_Azure_Rights_Management_Usage.md#BKMK_EnableRMSLogging)

-   [Loggar för att få åtkomst till och använda Azure Rights Management-användning](../Topic/Logging_and_Analyzing_Azure_Rights_Management_Usage.md#BKMK_AccesAndUseLogs)

-   [Så här hanterar du din Azure Rights Management loggen lagring](../Topic/Logging_and_Analyzing_Azure_Rights_Management_Usage.md#BKMK_ManageStorage)

-   [Hur ska få åtkomst till din Azure Rights Management användningsloggar](../Topic/Logging_and_Analyzing_Azure_Rights_Management_Usage.md#BKMK_Delegate)

-   [Hur du tolkar användning loggarna Azure Rights Management](../Topic/Logging_and_Analyzing_Azure_Rights_Management_Usage.md#BKMK_Interpret)

-   [Windows PowerShell-referens](../Topic/Logging_and_Analyzing_Azure_Rights_Management_Usage.md#BKMK_PowerShell)

## <a name="BKMK_EnableRMSLogging"></a>Så här aktiverar du loggning för användning av Azure Rights Management
Azure Rights Management användningsloggning är valfri, så om du vill använda den, måste du utföra specifika steg. När du använder Azure Rights Management användningsloggning, det finns ingen ändring i hur Rights Management fungerar och hur loggning är gratis. Men du måste ange ett Azure storage-konto för loggarna och du kommer att debiteras för den här lagringen.

Innan du börjar kontrollerar du att du uppfyller följande krav för att använda loggning för användning av Azure Rights Management:

|Krav|Mer information|
|--------|-------------------|
|En IT-baserad prenumeration som innehåller Azure Rights Management|Du måste ha en prenumeration på Microsoft Azure Rights Management som hanteras av din organisation. Organisationer som använder RMS för enskilda användare kan inte använda loggning för användning av Azure Rights Management.<br /><br />Om din organisation har användare som använder RMS för individer, innehåller Azure Rights Management användningsloggning en väldigt spännande business orsak till att omvandla RMS för enskilda användare till en Microsoft Azure Rights Management-prenumeration.<br /><br />Mer information om prenumerationer med Azure RMS finns i [Molnet prenumerationer som har stöd för Azure RMS](../Topic/Requirements_for_Azure_Rights_Management.md#BKMK_SupportedSubscriptions) i avsnittet den [Krav för Azure Rights Management](../Topic/Requirements_for_Azure_Rights_Management.md) artikeln.<br /><br />Mer information om RMS för individer finns [RMS för personer och Azure Rights Management](../Topic/RMS_for_Individuals_and_Azure_Rights_Management.md)|
|Azure-prenumeration|Du måste ha en prenumeration till Azure och tillräckligt lagringsutrymme på Azure för Azure Rights Management-loggar.|
|Windows PowerShell för Azure Rights Management|Om du inte redan gjort det, kan du hämta och installera Windows PowerShell-modulen för Azure Rights Management. Du använder Windows PowerShell-cmdlets för att konfigurera och hantera användningen loggarna Azure Rights Management.<br /><br />Mer information finns i [Installera Windows PowerShell för Azure Rights Management](../Topic/Installing_Windows_PowerShell_for_Azure_Rights_Management.md).|
Använd följande procedur för att aktivera Azure Rights Management användningsloggning, vilket innefattar steg för att skapa ett Azure storage-konto och sedan konfigurera Azure för att använda det här lagringskontot för Rights Management-loggar.

> [!NOTE]
> Den här proceduren förutsätts att du har en Azure-konto. Azure Rights Management användningsloggning stöder enskilda konton men som bör använda arbetet eller skolan konton. Vi rekommenderar dessutom att du skapar en dedikerad lagringskontot för Rights Management-loggar. Om de använder också loggfilerna måste du dela snabbtangenter lagring med Azure Rights Management och eventuellt andra.
> 
> Mer information om Azure-lagring finns i [Azure dokumentationen för lagring](http://azure.microsoft.com/documentation/services/storage/).

#### Hur du skapar ditt lagringskonto och aktivera loggning för användning av Azure Rights Management

1.  Logga in på den [Azure-portalen](https://manage.windowsazure.com/).

2.  Välj **lagring**.

    > [!TIP]
    > Om du inte ser det här alternativet kan du kontrollera att du har en Azure-prenumeration förutom prenumerationen för Rights Management.

3.  Klicka på **Skapa ett LAGRINGSKONTO** och för den **URL**, ange ett unikt namn för lagringskontot och om det behövs ändrar den **plats/AFFINITETSGRUPP** så att den matchar din region.

4.  Klicka på **OK**, och vänta tills du hittar namnet på lagringsplatsen statusen **Online**.

5.  Klicka på **Hantera snabbtangenter**.

6.  Från den **Hantera snabbtangenter** dialogruta som visar din primära och sekundära snabbtangenter kopiera den primära åtkomstnyckeln till Urklipp och stäng sedan dialogrutan.

7.  Starta Windows PowerShell med den **Kör som administratör** alternativet. Kör den [Anslut AadrmService](https://msdn.microsoft.com/library/azure/dn629415.aspx) kommando för att ansluta till Azure Rights Management-tjänsten:

    ```
    Connect-AadrmService
    ```

8.  Använd den [Set AadrmUsageLogStorageAccount](https://msdn.microsoft.com/library/azure/dn629426.aspx) kommando för att ange om du vill behålla din användningsloggar Azure Rights Management ersätta *&lt; Access_Key &gt;* med den primära nyckeln som du kopierade i steg 6 och *&lt; StorageAccount &gt;* med namnet på lagringskonto som du skapade i steg 3:

    ```
    $accesskey = convertto-securestring -asplaintext -force –string <Access_Key> Set-AadrmUsageLogStorageAccount -AccessKey $accesskey -StorageAccount <StorageAccount>
    ```

9. Använd den [Aktivera AadrmUsageLogFeature](https://msdn.microsoft.com/library/azure/dn629421.aspx) kommando för att aktivera loggning för användning av Azure Rights Management:

    ```
    Enable-AadrmUsageLogFeature
    ```
    Du bör se meddelandet: **Funktionen användning loggen har aktiverats för Rights management-tjänsten.**

Användningsloggning är aktiverat, Azure Rights Management börjar att logga alla åtgärder för din organisation och sparar informationen i ditt lagringskonto. Loggningsinformation är inte tillgänglig innan den här platsen.

## <a name="BKMK_AccesAndUseLogs"></a>Loggar för att få åtkomst till och använda Azure Rights Management-användning
Azure Rights Management skriver loggar till ditt Azure storage-konto som en serie BLOB. Varje blob innehåller en eller flera poster, i utökat loggfilsformat för W3C. Blob-namn är talen i den ordning de skapades. Den [Hur du tolkar användning loggarna Azure Rights Management](../Topic/Logging_and_Analyzing_Azure_Rights_Management_Usage.md#BKMK_Interpret) senare i det här dokumentet innehåller mer information om logginnehållet och de har skapats.

Det kan ta en stund för loggar ska visas i ditt lagringskonto efter en åtgärd för Azure Rights Management. De flesta loggar visas inom 15 minuter.

Lagringskontot som du skapade för Azure Rights Management användning loggarna är t.ex. en postlåda och har stöd för läsning direkt från lagringskontot, men är inte optimerad för att användas på det här sättet. I stället för bästa prestanda och för att minska kostnaderna rekommenderar vi att du laddar ned loggarna till lokal lagring, till exempel en lokal mapp, en databas eller en karta minska databasen.

Du kan hämta användning loggarna på två sätt:

-   Använd Windows PowerShell-cmdlet [Get-AadrmUsageLog](https://msdn.microsoft.com/library/azure/dn629401.aspx).

    Detta är det enklaste sättet att få åtkomst till användningsloggar. Denna cmdlet hämtar loggar till din dator, hämtar varje blob som en fil till en plats som du anger.

-   Använd den [Azure Storage SDK:](http://www.windowsazure.com/en-us/develop/net/) att skriva anpassade program att hämta loggarna.

    Ett anpassat program kan ge bättre flexibilitet än cmdlet: en Get-AadrmUsageLogs. Du kanske vill delegera hämtning av loggar till någon eller en process som inte får använda dina administrativa autentiseringsuppgifter för Azure Rights Management. Eller så kanske du vill avsöka loggar i realtid eftersom du vill övervaka missbruk för.

#### Hämta din användning loggar in med hjälp av PowerShell

-   Starta Windows PowerShell med den **Kör som administratör** alternativet och kör **Get-AadrmUsageLog –Path &lt;location&gt;**. Till exempel när du har skapat en mapp med namnet **logs** på E-enheten:

    -   Så här hämtar alla tillgängliga loggar till mappen E:\logs: `Get-AadrmUsageLog -Path "e:\logs"`

    -   Hämta ett specifikt intervall med BLOB: `Get-AadrmUsageLog –Path "e:\logs" –FromCounter 1024 –ToCounter 2047`

När du kör dessa cmdlets, visar Windows PowerShell namnet på det sista blob som har hämtats. Du kan tilldela det här namnet till en variabel som du kan köra Get-AadrmUsageLog i en slinga eller ett schema jobb, ladda ned inkrementell loggarna varje gång.

Exempel:

**PS C:\ &gt; $LastBlobName = Get-AadrmUsageLog – sökvägen "e:\logs"**

**1527**

**PS C:\ &gt; $LastBlobName**

**1527**

> [!TIP]
> Du kan aggregera alla hämtade loggfiler till en CSV-format genom att använda [Microsofts loggen parsern](http://www.microsoft.com/download/details.aspx?id=24659), vilket är ett verktyg för att konvertera mellan olika välkända loggformat. Du kan också använda verktyget för att konvertera data till SYSLOG-format eller importera den till en databas. När du har installerat verktyget kör **LogParser.exe /?** Hjälp och information för att använda det här verktyget. Du kan till exempel köra följande kommando för att importera alla information till .log-filformat: **logparser –i:w3c –o:csv “SELECT &#42; INTO AllLogs.csv FROM &#42;.log”**.

Du kan pausa och återuppta användningsloggning. När du pausar loggning behåller Azure Rights Management kontoinformationen lagring, så att du enkelt kan återuppta loggning igen.

#### Du pausar och återupptar användningsloggning

-   Om du vill pausa loggning, använder du följande cmdlet: [Inaktivera AadrmUsageLogFeature](https://msdn.microsoft.com/library/azure/dn629404.aspx)

-   Använd följande cmdlet för att återuppta loggning: [Aktivera AadrmUsageLogFeature](https://msdn.microsoft.com/library/azure/dn629421.aspx)

-   Om du vill kontrollera om loggning är aktiverad eller inaktiverad, använder du följande cmdlet: [Get-AadrmUsageLogFeature](https://msdn.microsoft.com/library/azure/dn629425.aspx)

    Värdet **Sant** innebär att användningsloggning är aktiverat för Azure Rights Management och värdet **Falskt** innebär att användningsloggning är inaktiverad.

## <a name="BKMK_ManageStorage"></a>Så här hanterar du din Azure Rights Management loggen lagring
Du debiteras för lagringsutrymmet som används för att hålla loggarna Azure Rights Management.

Azure Rights Management har ingen automatisk hantering av din användning av loggfiler. Om ingen åtgärd kvar de i ditt lagringskonto. Dock kan du vill ta bort dem när du har hämtat dem för att spara utrymme och minska lagringskostnader. Eller så kan du välja vilka filer att ta bort. Med ett undantag använder Azure Rights Management inte dessa loggfiler, så det finns inga begränsningar om när du tar bort dem.

Den fil som du inte måste ta bort (eller ändra) heter **metadata** i den **rms-metadata** behållare. Azure Rights Management använder den här blob för att hålla reda på det sista blob-numret som användes. Om den här filen har tagits bort, Azure Rights Management startar en ny behållare för loggar med ett blob-nummer som startar från 1 och alla framtida hämtningar med cmdlet: en Get-AadrmUsageLog använder den här nya behållaren för att hämta loggfiler. Loggar i den ursprungliga behållaren är därför kvar men frånkopplade. Det enda sättet att hämta loggarna överblivna är att använda Azure storage SDK.

> [!TIP]
> I stället för att hantera din Azure Rights Management loggen lagring själv, kan du delegera hantering funktionen till ett annat företag genom att dela din storage-konto och åtkomstnyckeln. Mer information finns i [Hur ska få åtkomst till din Azure Rights Management användningsloggar](../Topic/Logging_and_Analyzing_Azure_Rights_Management_Usage.md#BKMK_Delegate) senare i det här avsnittet.

I vissa fall kanske du vill återskapa ditt lagringsutrymme snabbtangenter. Exempel:

-   Du kan ändra det företag som hanterar användning loggarna Azure Rights Management.

-   Du misstänker att din lagring åtkomstnyckel manipuleras.

Om detta händer du är när du använder den sekundära åtkomstnyckeln (på antagandet att du tidigare använde den primära åtkomstnyckeln) till avbrott i tjänsten. När du återskapa åtkomstnyckeln som du inte har använt tidigare, konfigurerar du sedan Azure Rights Management för att använda den nya nyckeln. Använd följande procedur återskapa den sekundära åtkomstnyckeln och konfigurera Azure Rights Management för att använda den:

#### Återskapa den sekundära åtkomstnyckeln

1.  Logga in på den [Azure-portalen](https://manage.windowsazure.com/).

2.  Välj **lagring**.

3.  Klicka på **Hantera snabbtangenter**.

4.  I den **Hantera snabbtangenter** dialogrutan klickar du på **Återskapa** bredvid sekundära åtkomstnyckeln och kopiera den nya sekundära åtkomstnyckeln till Urklipp.

5.  Starta Windows PowerShell med den **Kör som administratör** alternativet och använda den [Set AadrmUsageLogStorageAccount](https://msdn.microsoft.com/library/azure/dn629426.aspx) cmdlet för att konfigurera Azure Rights Management för att använda den här nya snabbtangenten ersätta *&lt; StorageAccount &gt;* med namnet på ditt lagringskonto och *&lt; Access_Key &gt;* med den sekundära åtkomstnyckeln som du kopierade:

    ```
    Set-AadrmUsageLogStorageAccount -StorageAccount <StorageAccount>-AccessKey <Access_Key>
    ```
    > [!WARNING]
    > Även om du kan växla till ett annat lagringskonto när du kör det här kommandot, åtgärden orphans tidigare loggarna och de kommer inte längre att komma åt till cmdlet Set-AadrmUsageLogStorageAccount eller liknande management kommandon och funktioner.

6.  I den **Hantera snabbtangenter** dialogrutan och återskapa den primära åtkomstnyckeln.

## <a name="BKMK_Delegate"></a>Hur ska få åtkomst till din Azure Rights Management användningsloggar
Du kan delegera åtkomst till RMS-loggarna genom att dela din storage-konto och åtkomstnyckeln. Du kanske vill delegera tillgång till en annan administratör, en utvecklare inom din organisation eller någon oberoende programvaruleverantör (ISV). Eftersom de inte har dina administratörsautentiseringsuppgifter för RMS, kan de inte kan använda cmdlet: en Get-AardrmUsageLog för att hämta RMS-loggar. De måste i stället använda Windows Storage SDK: hämta loggarna. De kan också skriva ett program för att läsa loggarna direkt från Azure Storage.

Det är säkert att dela din lagring och kontonyckel på det här sättet när lagringskontot är dedikerad för RMS-loggar. Även om andra användare har åtkomst till nyckeln, kan inte de används för att komma åt andra storage-konto eller använda ditt konto för RMS-klienten.

## <a name="BKMK_Interpret"></a>Hur du tolkar användning loggarna Azure Rights Management
Använd följande information för att tolka Azure Rights Management användningsloggar.

### Kontot lagringslayout
Första gången Azure Rights Management loggar som skrivs till ditt lagringskonto skapas följande två behållare:

-   **Rms-metadata**: Den här behållaren är reserverad för Azure Rights Management. Inte ändra eller ta bort den här behållaren.

-   **Rms - loggar - &lt; guid &gt;**: Behållaren finns där Azure Rights Management skapas och sparas i loggarna. Om du vill logga information som de innehåller inte längre kan du ta bort alla filer i den här behållaren.

Över tiden, Azure Rights Management kan skapa ytterligare **Rms - loggar - &lt; guid &gt;** behållare. Till exempel om den **Rms-metadata** behållare skadas eller raderas av misstag, Azure Rights Management återställer innehållet och skapar en ny **Rms - loggar - &lt; guid &gt;** behållare för alla framtida loggar. De gamla loggarna i behållaren gamla tas inte bort men är frånkopplade.

### Ordningsföljden logg
Azure Rights Management skriver loggarna som en serie BLOB. Varje blob innehåller en eller flera poster, i utökat loggfilsformat för W3C.

Namnet på varje blob är ett tal. I varje logg behållaren heter första blob 000000001. Varje blob heter sekventiellt i den ordning som den skapades. Varje blob innehåller en eller flera poster. Varje loggpost har en UTC-tidsstämpel som anger när motsvarande begäran skickades av Azure Rights Management.

> [!IMPORTANT]
> Azure Rights Management loggning systemet är optimerat för att förse dig med loggar snabbt, i stället för i strikt ordningsföljd. Ordningen på blobbar som ordningen på loggposter inom en blob kanske inte kronologisk ordning. Endast blobbar som heter sekventiellt orsaken är så att du kan hämta dem effektivt inkrementellt.
> 
> Två exempel på potentiella loggen sekvens resultat:
> 
> -   Loggposter i blob 000000004 överlappa kronologisk ordning med loggposter i blob 000000003. I extrema fall, kan alla poster i blob 000000004 har skapats innan alla poster i blob 000000003.
> -   Andra loggposten i en blob kan ha genererats innan den första loggposten, men har skrivits till lagring i omvänd ordning.

Innan du analysera Azure Rights Management användning loggarna rekommenderar vi att du hämtar och importera loggen till en databas där du kan sortera loggarna baserat på deras tidsstämpel. Mer information om hur du hämtar loggarna finns i [Loggar för att få åtkomst till och använda Azure Rights Management-användning](../Topic/Logging_and_Analyzing_Azure_Rights_Management_Usage.md#BKMK_AccesAndUseLogs) i det här avsnittet.

Eftersom loggarna är inte nödvändigtvis kronologisk men flesta skrivs inom 15 minuter för begäran, när du identifierar de loggar som du vill med hjälp av deras tidsstämpel, lägger du till 15 minuter till den tid som du är intresserad av. Hämta de här loggarna. Den här strategin bör se till att du får nästan alla loggar.

En annan sak att komma ihåg är att tidsstämpeln på varje loggpost är lokal tid för Azure Rights Management-tjänsten som bearbetas begäran. Eftersom Azure Rights Management körs på flera servrar i flera datacenter, kan loggarna ibland vara felaktig ordningsföljd, även om de sorteras efter deras tidsstämpel. De olika är dock liten och vanligen inom en minut. I de flesta fall är det inte ett problem som skulle ha uppstått för analys av loggen.

### Blob-format
Varje blob har utökat loggfilsformat för W3C. Det börjar med följande två rader:

**#Software: RMS**

**#Version: 1.1**

Den första raden anger att de är Azure Rights Management loggar. Den andra raden identifierar att resten av blobben följer specifikationen version 1.1. Vi rekommenderar att alla program som parsa loggarna kontrollerar dessa två rader innan du fortsätter att tolka resten av BLOB-objektet.

Den tredje raden räknar upp en lista med fältnamn som är avgränsade med flikar:

**#Fields: datum tid rad-id typ av tjänstbegäran användar-id resultatet Korrelations-id innehålls-id e-ägare utfärdaren mall-id filnamn publicerad c-info c-ip**

Efterföljande rader är en loggpost. Värdena för fälten i samma ordning som föregående rad och avgränsas med tabbar. Använd följande tabell för att tolka fält.

|Fältnamn|Datatypen för W3C|Beskrivning|Exempelvärde|
|------------|---------------------|---------------|----------------|
|datum|Datum|UTC-datum när begäran behandlades.<br /><br />Källan är den lokala klockan på den server som hanteras av begäran.|2013-06-25|
|tid|Tid|UTC-tid i 24-timmarsformat när begäran behandlades.<br /><br />Källan är den lokala klockan på den server som hanteras av begäran.|21:59:28|
|rad-id|Text|Unikt GUID för den här loggpost.<br /><br />Det här värdet är användbart när du sammanställa loggar eller kopiera loggar till ett annat format.|1c3fe7a9-d9e0-4654-97b7-14fafa72ea63|
|typ av tjänstbegäran|Namn|Namnet på RMS-API som begärdes.|AcquireLicense|
|användar-id|Sträng|Användaren som gjorde begäran.<br /><br />Värdet är inom enkla citattecken. Vissa typer av begäranden är anonyma, i vilket fall värdet är ".|'joe@contoso.com'|
|resultat|Sträng|'Lyckades om begäran behandlades lyckades.<br /><br />Feltypen av i enkla citattecken om begäran misslyckades.|"Lyckades|
|Korrelations-id|Text|GUID som är gemensamma mellan loggen för RMS-klienten och serverloggen för en viss begäran.<br /><br />Det här värdet kan vara praktiskt att felsökning på kundernas frågor.|cab52088-8925-4371-be34-4b71a3112356|
|innehålls-id|Text|GUID omges av klammerparenteser som identifierar det skyddade innehållet (till exempel ett dokument).<br /><br />Det här fältet har ett värde om begäran-typ är AcquireLicense och är tomt för alla andra typer av begäranden.|{bb4af47b-cfed-4719-831d-71b98191a4f2}|
|e-ägare|Sträng|E-postadressen för ägaren till dokumentet.|Alice@contoso.com|
|utfärdaren|Sträng|E-postadress av dokument utfärdaren.|Alice@contoso.com (eller) FederatedEmail.4c1f4d-93bf-00a95fa1e042@contoso.onmicrosoft.com'|
|Mall-id|Sträng|ID för den mall som används för att skydda dokumentet.|{6d9371a6-4e2d-4e97-9a38-202233fed26e}|
|Filnamn|Sträng|Filnamnet för det dokument som skyddas.|TopSecretDocument.docx|
|Publicerade datum|Datum|Datum när dokumentet skyddas.|2015-10-15T21:37:00|
|c-info|Sträng|Information om klienten plattformen som har att göra begäran.<br /><br />Specifik sträng varierar beroende på vilket program (till exempel operativsystemet eller webbläsaren).|' MSIPC, version = 1.0.623.47; AppName = WINWORD. EXE; AppVersion = 15.0.4753.1000; AppArch = x 86; OSName = Windows; OSVersion = 6.1.7601; OSArch = amd64'|
|c-ip|Adress|IP-adressen för den klient som skickar begäran.|64.51.202.144|

#### Undantag för fältet användar-id
Även om användaren som gjorde begäran anger oftast att fältet användar-id, finns det två undantag där värdet inte mappas till en verklig användare:

-   Värdet **' microsoftrmsonline @&lt; YourTenantID &gt;. &lt; region &gt; rms.. aadrm.com'**.

    Detta anger att en tjänst för Office 365, till exempel Exchange Online eller Sharepoint Online är att göra begäran. I strängen *&lt; YourTenantID &gt;* är GUID för din klient och *&lt; region &gt;* är den region där din klient har registrerats. Till exempel **na** representerar Nordamerika **eu** representerar Europa, och **ap** representerar Asien.

-   Om du använder RMS-kopplingen.

    Begäran från den här anslutningen loggas med tjänstens huvudnamn som RMS genererar automatiskt när du installerar RMS-anslutningen.

#### Typer av vanliga begäranden
Det finns många typer av begäranden för Azure Rights Management, men i följande tabell visas några av de mest vanliga begäran.

|Typ av tjänstbegäran|Beskrivning|
|------------------------|---------------|
|AcquireLicense|en klient från en Windows-baserad dator begär en licens för RMS-skyddat innehåll.|
|AcquirePreLicense|en klient från användare, begär för en licens för RMS-skyddat innehåll.|
|AcquireTemplates|en samtal gjordes till förvärvar mallar utifrån mallen ID|
|AcquireTemplateInformation|en samtal gjordes att hämta ID: N för mallen från tjänsten.|
|AddTemplate|ett anrop görs från Azure-portalen för att lägga till en mall.|
|BECreateEndUserLicenseV1|görs ett samtal från en mobil enhet att skapa en Slutanvändarlicens.|
|BEGetAllTemplatesV1|görs ett samtal från en mobil enhet (backend) att hämta alla mallar.|
|Certifiera|klienten intygar innehållet för skydd.|
|Dekryptera|klienten försöker att dekryptera RMS-skyddad innehåll.|
|DeleteTemplateById|ett anrop görs från Azure-portalen för att ta bort en mall som mall-ID.|
|ExportTemplateById|ett anrop från Azure-portalen du exporterar en mall baserat på en mall ID.|
|FECreateEndUserLicenseV1|liknar AcquireLicense begäran men från mobila enheter.|
|FECreatePublishingLicenseV1|samma certifiera och GetClientLicensorCert kombineras från mobila klienter.|
|FEGetAllTemplates|ett anrop, från en mobil enhet (frontend) att hämta mallar.|
|GetAllTemplates|ett anrop görs från Azure-portalen för att hämta alla mallar.|
|GetClientLicensorCert|klienten begär en publishing certifikat (som senare används för att skydda innehåll) från en Windows-baserad dator.|
|GetConfiguration|kallas en Azure PowerShell-cmdlet för att hämta konfigurationen av Azure RMS-klienten.|
|GetConnectorAuthorizations|ett anrop från RMS-kopplingar att hämta konfigurationen från molnet.|
|GetTenantFunctionalState|i Azure-portalen kontrollerar om Azure RMS är aktiverat.|
|GetTemplateById|är ringa från Azure portalen att hämta en mall genom att ange en mall för ID.|
|ExportTemplateById|ett samtal görs från Azure portalen så här exporterar du en mall genom att ange en mall för ID.|
|FindServiceLocationsForUser|är ringa till fråga för URL: er, som används för att anropa certifiera eller AcquireLicense.|
|ImportTemplate|är ringa från Azure portalen att importera en mall.|
|ServerCertify|är ringa från en RMS-aktiverade klienten (t.ex SharePoint) att certifiera servern.|
|SetUsageLogFeatureState|ringa är att aktivera användningsloggning.|
|SetUsageLogStorageAccount|ringa är att ange platsen för Azure RMS-loggarna.|
|SignDigest|är ringa när en nyckel används för att signera ändamål. Kallas normalt en gång per AcquireLicence (eller FECreateEndUserLicenseV1) certifiera, och GetClientLicensorCert (eller FECreatePublishingLicenseV1).|
|UpdateTemplate|är ringa från Azure portalen att uppdatera en befintlig mall.|

## <a name="BKMK_PowerShell"></a>Windows PowerShell-referens
Använd följande Windows PowerShell-cmdlets för att du konfigurerar och använder loggning för användning av Azure Rights Management:

-   [Inaktivera AadrmUsageLogFeature](https://msdn.microsoft.com/library/azure/dn629404.aspx)

-   [Aktivera AadrmUsageLogFeature](https://msdn.microsoft.com/library/azure/dn629421.aspx)

-   [Hämta AadrmUsageLog](https://msdn.microsoft.com/library/azure/dn629401.aspx)

-   [Hämta AadrmUsageLogFeature](https://msdn.microsoft.com/library/azure/dn629425.aspx)

-   [Hämta AadrmUsageLogLastCounterValue](https://msdn.microsoft.com/library/azure/dn629423.aspx)

-   [Hämta AadrmUsageLogStorageAccount](https://msdn.microsoft.com/library/azure/dn629419.aspx)

-   [Ange AadrmUsageLogStorageAccount](https://msdn.microsoft.com/library/azure/dn629426.aspx)

Mer information om hur du använder Windows PowerShell för Azure Rights Management finns [Administrera Azure Rights Management med Windows PowerShell](../Topic/Administering_Azure_Rights_Management_by_Using_Windows_PowerShell.md).

## Se även
[Använda Azure Rights Management](../Topic/Using_Azure_Rights_Management.md)

