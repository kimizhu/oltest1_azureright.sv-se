---
description: na
keywords: na
title: Planning and Implementing Your Azure Rights Management Tenant Key
search: na
ms.date: na
ms.service: rights-management
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f0d33c5f-a6a6-44a1-bdec-5be1bc8e1e14
---
# Planera och implementera din Azure Rights Management innehavaren nyckel
Använd informationen i det här avsnittet som hjälper dig att planera för och hantera din Rights Management (RMS) klienten nyckel för Azure RMS. I stället för Microsoft hantera din klient-nyckel (standard), kanske du vill hantera din egen innehavaren nyckel för att uppfylla specifika förordningar som gäller för din organisation.  Hantera klienten nyckeln kallas också för att göra egna nyckel eller BYOK som.

> [!NOTE]
> RMS-klienten nyckeln kallas även nyckeln Server licensgivarens certifikatet (Serverlicensgivarcertifikat). Azure RMS har en eller flera nycklar för varje organisation prenumererar på Azure RMS. Varje gång en nyckel som används för RMS i en organisation (till exempel användarnycklar, dator nycklar, dokument krypteringsnycklar), de kryptografiskt i en kedja till din nyckel för RMS-klienten.

**En överblick över:** Använd följande tabell som en Snabbguide till topologin rekommenderade innehavaren. Använd sedan ytterligare avsnitt för mer information.

Om du distribuerar Azure RMS med en nyckel för innehavaren som hanteras av Microsoft, kan du ändra till BYOK senare. Du kan inte för närvarande ändra din nyckel för Azure RMS-klienten från BYOK som hanteras av Microsoft.

|Affärsbehov|Rekommenderade innehavaren nyckel topologi|
|---------------|----------------------------------------------|
|Distribuera Azure RMS snabbt och utan speciell maskinvara|Hanteras av Microsoft|
|Måste ha fullständig IRM-funktionerna i Exchange Online med Azure RMS|Hanteras av Microsoft|
|Dina nycklar skapas av dig och skyddas i hardware security module (HSM)|BYOK<br /><br />För närvarande är leder den här konfigurationen till minskade IRM-funktionerna i Exchange Online. Mer information finns i [BYOK pricing and restrictions](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_Pricing) avsnitt.|
Använd följande avsnitt för att hjälpa dig att välja vilken klient nyckel topologi ska användas, Förstå innehavaren nyckel livscykel, hur du implementerar sätta egna nyckel (BYOK) och hur nästa:

-   [Choose your tenant key topology: Managed by Microsoft (the default) or managed by you (BYOK)](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_ChooseTenantKey)

-   [BYOK pricing and restrictions](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_Pricing)

-   [Implementing bring your own key (BYOK)](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_ImplementBYOK)

-   [Next steps](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_NextSteps)

## <a name="BKMK_ChooseTenantKey"></a>Välj din klient topologi för nyckel: Hanteras av Microsoft (standard) och hanteras av dig (BYOK)
Bestäm vilken klient nyckel är bäst för din organisation. Som standard Azure RMS genererar din nyckel för klienten och hanterar de flesta aspekter av innehavaren nyckel livscykel. Detta är det enklaste alternativet med de lägsta administrativa kostnader. I de flesta fall bör behöver du även inte vet att du har en klient-nyckel. Du registrera bara dig för Azure RMS och resten av processen nyckelhantering hanteras av Microsoft.

Alternativt kan du fullständig kontroll över din nyckel för innehavaren som innebär att skapa din klient nyckel och hålla huvudkopian på din lokala. Det här scenariot kallas ofta som gör en egen nyckel (BYOK). Med det här alternativet händer följande:

1.  Du kan generera nyckeln klient på din lokala i enlighet med din IT-principer.

2.  Du överföra säkert nyckeln klient från en maskinvara säkerhet modulen (HSM) i din ägo till HSM som ägs och hanteras av Microsoft. Hela processen lämnar din klient nyckel aldrig maskinvara skydd gräns.

3.  När du överför din klient nyckel till Microsoft, förblir den skyddas av Thales HSM. Microsoft har arbetat med Thales så att din klient-nyckel inte kan extraheras från Microsofts HSM.

Men det är valfritt, kommer du förmodligen också vill använda nära realtid användningen loggar från Azure RMS kan se exakt hur och när din klient nyckel används.

> [!NOTE]
> Som en ytterligare skydd åtgärd använder Azure RMS separat säkerhet världar för sina datacenter i Nordamerika, EMEA (Europa, Mellanöstern och Afrika) och Asien. När du hanterar klient nyckeln kopplat den till säkerhet världen av region där din RMS-klient är registrerat. Exempelvis kan kan en klient nyckel från en Europeiska kund inte användas i datacenter i Nordamerika eller Asien.

## <a name="BKMK_OverviewLifecycle"></a>Innehavaren nyckel livscykel
Om du väljer att Microsoft ska hantera din klient nyckel, hanterar Microsoft de flesta livscykelåtgärder nyckel. Om du vill hantera din klient nyckel ansvarar du för många av de viktiga livscykel åtgärderna och vissa ytterligare procedurer.

Följande diagram visar och jämför dessa två alternativ. Första diagram visar hur administratör omkostnader som det finns för dig i standardkonfigurationen när Microsoft hanterar nyckeln för innehavaren.

![](../Image/RMS_BYOK_cloud.png)

Andra diagram visar de ytterligare steg som krävs när du hanterar klient nyckeln.

![](../Image/RMS_BYOK_onprem.png)

Om du bestämmer dig att hantera din innehavare för Microsoft ingen ytterligare åtgärd krävs för att generera nyckeln och du kan hoppa över följande avsnitt och gå direkt till [Next steps](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_NextSteps).

Läs följande avsnitt för mer information om du vill hantera din klient nyckel själv.

### Mer information om Thales HSM och Microsoft-tillägg
Azure RMS använder Thales HSM för att skydda dina nycklar.

Thales e-säkerhet är en inledande globala provider för kryptering av data och cyber security lösningar finansiella tjänster, hög teknik, tillverkning, regering och teknik sektorer. Med en 40 år spåra post för att skydda företagets och statlig information Thales lösningar används av de fyra fem största energi och flyg företag, 22 NATO länder och skydda mer än 80 procent av transaktioner över hela världen.

Microsoft samarbetar med Thales att förbättra tillståndet för bilder för HSM. Dessa förbättringar kan du hämta vanliga fördelarna med värdtjänster utan lämnar kontroll över dina nycklar. Mer specifikt kan förbättrade hantera HSM så att du inte behöver Microsoft. Azure RMS skalas med kort varsel att uppfylla organisationens användning hjul som en molntjänst. På samma gång skyddas din nyckel i Microsofts HSM: Du kan behålla kontroll över nyckel livscykel eftersom du generera nyckeln och överför den till Microsofts HSM.

Mer information finns i [Thales HSM och Azure RMS](http://www.thales-esecurity.com/msrms/cloud) på webbplatsen Thales.

## <a name="BKMK_Pricing"></a>BYOK prissättning och begränsningar
Organisation som har en IT-hanterade Azure-prenumeration kan du använda BYOK och logga användning utan extra kostnad. Organisationer som använder RMS för enskilda användare kan inte använda BYOK och loggar eftersom de inte har en Innehavaradministratör för att konfigurera dessa funktioner.

> [!NOTE]
> Mer information om RMS för individer finns [RMS för personer och Azure Rights Management](../Topic/RMS_for_Individuals_and_Azure_Rights_Management.md).

![](../Image/RMS_BYOK_noExchange.png)

BYOK och loggning fungerar sömlöst med alla program som kan integreras med Azure RMS. Detta omfattar molntjänster, till exempel SharePoint Online, lokala servrar som kör Exchange och SharePoint som fungerar med Azure RMS med hjälp av RMS-koppling och klientprogram, till exempel Office 2013. Du får nyckelanvändning loggar oavsett som gör programmet begäranden av Azure RMS.

Det finns ett undantag: För närvarande **Azure RMS BYOK är inte kompatibel med Exchange Online**.  Vi rekommenderar att du distribuerar Azure RMS i nyckelhantering standardläget nu där Microsoft skapar och hanterar din nyckel om du vill använda Exchange Online. Du har möjlighet att flytta till BYOK senare, till exempel när Exchange Online stöder Azure RMS BYOK. Om du inte vill vänta, är ett annat alternativ att distribuera Azure RMS med BYOK nu med nedsatt RMS-funktionalitet för Exchange Online (oskyddade e-post och oskyddade bifogade filer förblir fullt fungerande):

-   Skyddad e-post eller skyddade bifogade filer i Outlook Web Access kan inte visas.

-   Skyddad e-post på mobila enheter som använder Exchange ActiveSync IRM kan inte visas.

-   Flytta dekryptering (till exempel för att söka efter skadlig kod) och journalen dekryptering inte är möjligt, så skyddade e-post och skyddade bifogade filer kommer att hoppas över.

-   Transport skydd regler och data förhindra dataförlust (DLP) som använder IRM-principer är inte möjligt så RMS-skydd inte kan användas med hjälp av dessa metoder.

-   Server-baserade söka efter skyddad e-post, så kommer att hoppas över skyddade e-postmeddelanden.

När du använder Azure RMS BYOK med nedsatt RMS-funktionalitet för Exchange Online fungerar RMS med e-klienter i Outlook på Windows- och Mac och på andra e-klienter som inte använder Exchange ActiveSync IRM.

Om du migrerar till Azure RMS från AD RMS kan importeras nyckeln som en betrodd publiceringsdomän (betrodda Publiceringsdomänen) till Exchange Online (kallas även BYOK i Exchange terminologi som är separat från Azure RMS BYOK). I det här scenariot måste du ta bort den betrodda Publiceringsdomänen från Exchange Online för att undvika motstridiga mallar och principer. Mer information finns i [Ta bort RMSTrustedPublishingDomain](https://technet.microsoft.com/library/jj200720%28v=exchg.150%29.aspx) från Exchange Online-cmdlet: ar-biblioteket.

Ibland är Azure RMS BYOK undantag för Exchange Online inte ett problem i praktiken. Till exempel köra organisationer som behöver BYOK och loggning sina data program (Exchange, SharePoint, Office) lokalt, och använda Azure RMS för funktioner som inte är tillgängliga med lokala AD RMS (till exempel samarbete med andra företag och åtkomst från mobila klienter). Både BYOK och loggning fungerar bra i det här scenariot och Tillåt organisationen för att ha fullständig kontroll över sin Azure RMS-prenumeration.

## <a name="BKMK_ImplementBYOK"></a>Implementera gör en egen nyckel (BYOK)
Använd information och procedurer i det här avsnittet om du har valt att skapa och hantera din klient-nyckeln. Gör nyckel (BYOK) scenariot:

-   [Prerequisites for BYOK](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_Preqs)

-   [Generate and transfer your tenant key – over the Internet](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_BYOK_Internet)

-   [Generate and transfer your tenant key – in person](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_BYOK_InPerson)

> [!IMPORTANT]
> Om du redan har börjat använda [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] (tjänsten aktiveras) och du har användare som kör Office 2010, kontakta Microsofts kundtjänst (CSS) innan du kör dessa procedurer. Beroende på din scenario och krav, kan du fortfarande använda BYOK men med vissa begränsningar eller ytterligare steg.
> 
> Kontakta också CSS om din organisation har specifika principer för hantering av nycklar.

### <a name="BKMK_Preqs"></a>Krav för BYOK
I tabellen nedan finns en lista över förutsättningarna för sätta en egen nyckel (BYOK).

|Krav|Mer information|
|--------|-------------------|
|En prenumeration som har stöd för Azure RMS|Mer information om tillgängliga prenumerationer, finns det [Molnet prenumerationer som har stöd för Azure RMS](../Topic/Requirements_for_Azure_Rights_Management.md#BKMK_SupportedSubscriptions) i avsnittet den [Krav för Azure Rights Management](../Topic/Requirements_for_Azure_Rights_Management.md) artikeln.|
|Du använder inte RMS för enskilda personer eller till Exchange Online. Eller, om du använder Exchange Online måste du förstå och godkänna begränsningar med hjälp av BYOK med den här konfigurationen.|Mer information om aktuella begränsningar för BYOK och begränsningar finns i [BYOK pricing and restrictions](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_Pricing) i det här avsnittet. **Important:** BYOK är för närvarande inte kompatibel med Exchange Online.|
|Thales HSM, smartkort och programvara<br /><br />Om du migrerar från AD RMS till Azure RMS med hjälp av programvarunyckeln till maskinvarunyckeln, måste du ha en lägsta version av 11.62 för Thales drivrutiner.|Du måste ha åtkomst till en Thales Hardware Security Module och grundläggande operativa kunskaper om Thales HSM. Se [Thales Hardware Security Module](http://www.thales-esecurity.com/msrms/buy) för listan över kompatibla modeller eller köpa en HSM om du inte har något.|
|Om du vill överföra din klient nyckel via Internet i stället för att vara fysiskt närvarande i Redmond, USA:<br /><br />1.  En offline x 64 arbetsstation med en minsta Windows-operativsystemet för Windows 7 och Thales nShield-programvara som är minst version 11.62.<br />    Om den här arbetsstationen kör Windows 7, måste du [installera Microsoft .NET Framework 4.5](http://go.microsoft.com/fwlink/?LinkId=225702).<br />2.  En arbetsstation som är ansluten till Internet och har en minsta Windows-operativsystemet Windows 7.<br />3.  En USB-enhet eller annan bärbar lagringsenhet som har minst 16 MB ledigt utrymme.|Dessa krav krävs inte om du reser till Redmond och överför din klient nyckel personligen.<br /><br />Av säkerhetsskäl rekommenderar vi att den första arbetsstationen inte är anslutet till ett nätverk. Men tillämpas detta programmässigt inte. **Note:** I anvisningarna som följer, kallas den här arbetsstationen frånkopplade arbetsstationen.<br />Om innehavaren nyckeln är för ett produktionsnätverk, rekommenderar vi dessutom att du använder en andra, separat arbetsstation att hämta verktygsuppsättningen och överföra nyckeln för innehavaren. Men i testsyfte kan du använda samma arbetsstation som först. **Note:** I anvisningarna som följer, kallas arbetsstationen andra Internet-anslutna arbetsstationen.|
|Valfritt: Azure-prenumeration|Om du vill logga din klient nyckelanvändning (och användning av Rights Management) måste du ha en prenumeration till Azure och tillräckligt lagringsutrymme på Azure för att lagra loggarna.|
Procedurerna för att skapa och använda egna innehavaren beror på om du vill göra detta via Internet eller personliga:

-   **Via Internet:** Detta kräver vissa ytterligare konfigurationssteg och exempelvis hämta och använda en uppsättning verktyg och Windows PowerShell-cmdlets. Du behöver inte vara fysiskt i en Microsoft-anläggning överföra din klient-nyckel. Säkerhet underhålls av följande metoder:

    -   Du kan generera nyckeln för innehavaren från offline arbetsstation, vilket minskar risken för angrepp.

    -   Klient-nyckeln är krypterad med en nyckel Exchange nyckel (KEK), som är krypterade tills den överförs till Azure RMS HSM. Endast krypterad version av nyckeln innehavaren lämnar den ursprungliga arbetsstationen.

    -   Ett verktyg anger egenskaper i din klient-nyckel som binder din klient nyckel för Azure RMS säkerhet världen. Så kan Azure RMS HSM ta emot och dekryptera din klient nyckel endast dessa HSM använda. Din klient nyckeln kan exporteras. Den här bindningen påtvingas av Thales HSM.

    -   Den Key Exchange nyckel (KEK) som används för att kryptera din klient nyckel genereras i Azure RMS HSM och kan inte exporteras. HSM genomdriva att det kan finnas någon Rensa version av KEK utanför HSM. Dessutom innehåller verktygsuppsättningen intyg från Thales att KEK kan inte exporteras och genererades inuti en äkta HSM som har tillverkats av Thales.

    -   Verktygsuppsättningen innehåller intyg från Thales Azure RMS säkerhet världen skapades även på ett äkta HSM tillverkats av Thales. Intygar du att Microsoft använder äkta maskinvara.

    -   Microsoft använder separata KEKs samt separata säkerhet världar i varje geografiska område, vilket garanterar att din klient-nyckel kan användas endast i datacenter i området där krypteras den. Exempelvis kan kan en klient nyckel från en Europeiska kund inte användas i datacenter i Nord amerikanska eller Asien.

    > [!NOTE]
    > Din klient nyckel kan på ett säkert sätt att flytta via ej betrodda datorer och nätverk eftersom den är krypteras och skyddas med behörighet nivå för åtkomstkontroll, som kan användas i din HSM och Microsofts HSM för Azure RMS. Du kan använda skript som ingår i verktygsuppsättningen att verifiera skyddsåtgärder och läsa mer information om hur det fungerar i Thales: [Hantering av maskinvara i molnet RMS](https://www.thales-esecurity.com/knowledge-base/white-papers/hardware-key-management-in-the-rms-cloud).

-   **Personliga:** Detta kräver att du kontaktar Microsoft kundservice (CSS) om du vill schemalägga en överföringen nyckeln tid för Azure RMS. Du måste reser till ett Microsoft office i Redmond, Washington, USA överföra din klient nyckel till Azure RMS säkerhet världen.

### <a name="BKMK_BYOK_Internet"></a>Generera och överför din klient nyckel – via Internet
Använd följande procedurer om du vill överföra din klient nyckel via Internet snarare än reser till en Microsoft-anläggning överföra innehavaren nyckel personligen:

-   [Prepare your Internet-connected workstation](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_InternetPrepareWorkstation)

-   [Prepare your disconnected workstation](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_DisconnectedPrepareWorkstation)

-   [Generate your tenant key](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_InternetGenerate)

-   [Prepare your tenant key for transfer](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_InternetPrepareTransfer)

-   [Transfer your tenant key to Azure RMS](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_InternetTransfer)

#### <a name="BKMK_InternetPrepareWorkstation"></a>Förbered din Internet-anslutna arbetsstation
Så här 3 för att förbereda din arbetsstation som är ansluten till Internet:

-   [Step 1: Install Windows PowerShell for Azure Rights Management](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_PrepareInternetConnectedWorkstation1)

-   [Step 2: Get your Azure Active Directory tenant ID](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_PrepareInternetConnectedWorkstation2)

-   [Step 3: Download the BYOK toolset](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_PrepareInternetConnectedWorkstation3)

##### <a name="BKMK_PrepareInternetConnectedWorkstation1"></a>Steg 1: Installera Windows PowerShell för Azure Rights Management
Hämta och installera Windows PowerShell-modulen för Azure Rights Management från Internetanslutna-arbetsstationen.

> [!NOTE]
> Om du tidigare har hämtat Windows PowerShell-modulen kör du följande kommando för att kontrollera att versionsnumret är minst 2.1.0.0: `(Get-Module aadrm -ListAvailable).Version`

Installationsinstruktioner finns [Installera Windows PowerShell för Azure Rights Management](../Topic/Installing_Windows_PowerShell_for_Azure_Rights_Management.md).

##### <a name="BKMK_PrepareInternetConnectedWorkstation2"></a>Steg 2: Hämta din Azure Active Directory-klient-ID
Starta Windows PowerShell med den **Kör som administratör** alternativet och kör sedan följande kommandon:

-   Använd den [Anslut AadrmService](http://msdn.microsoft.com/library/windowsazure/dn629415.aspx) cmdlet för att ansluta till tjänsten Azure RMS:

    ```
    Connect-AadrmService
    ```
    När du uppmanas ange din [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] klient administratörsautentiseringsuppgifter (vanligtvis använder du ett konto som är en global administratör för Azure Active Directory eller Office 365).

-   Använd den [Get-AadrmConfiguration](http://msdn.microsoft.com/library/windowsazure/dn629410.aspx) cmdlet för att visa konfigurationen för din klient:

    ```
    Get-AadrmConfiguration
    ```
    Spara GUID från utdata från den första raden (BPOSId). Det här är din Azure Active Directory klient-ID som du behöver senare när du förbereder din klient nyckel för överföring.

-   Använd den [Koppla från AadrmService](http://msdn.microsoft.com/library/windowsazure/dn629416.aspx) cmdlet för att koppla från Azure RMS-tjänsten tills du är redo att överföra din nyckel:

    ```
    Disconnect-AadrmService
    ```

Stäng inte Windows PowerShell-fönstret.

##### <a name="BKMK_PrepareInternetConnectedWorkstation3"></a>Steg 3: Hämta BYOK verktygsuppsättningen
Gå till Microsoft Download Center och [Hämta verktygsuppsättningen BYOK](http://go.microsoft.com/fwlink/?LinkId=335781) för din region:

|Region|Paketnamn|
|----------|-------------|
|Nordamerika|AzureRMS-BYOK-verktyg-Förenade States.zip|
|Europa|AzureRMS-BYOK-verktyg-Europe.zip|
|Asien|AzureRMS-BYOK-verktyg-AsiaPacific.zip|
Verktygsuppsättningen omfattar följande:

-   Ett paket med nyckeln Exchange nyckel (KEK) som har ett namn som börjar med **BYOK-KEK-pkg -**.

-   Ett säkerhet World paket som har ett namn som börjar med **BYOK-SecurityWorld-pkg -**.

-   Skriptet python **verifykeypackage.py**.

-   En kommandorad körbar fil med namnet **KeyTransferRemote.exe**, en metadatafil med namnet **KeyTransferRemote.exe.config**, och tillhörande DLL-filer.

-   En Visual C++ Redistributable Package, med namnet **vcredist_x64.exe**.

Kopiera paketet till en USB-enhet eller annan bärbar lagring.

#### <a name="BKMK_DisconnectedPrepareWorkstation"></a>Förbered din frånkopplade arbetsstation
Så här 2 för att förbereda din arbetsstation som inte är ansluten till ett nätverk (Internet eller ditt interna nätverk):

-   [Step 1: Prepare the disconnected workstation with Thales HSM](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_PrepareDisconnectedWorkstation1)

-   [Step 2: Install the BYOK toolset on the disconnected workstation](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_PrepareDisconnectedWorkstation2)

##### <a name="BKMK_PrepareDisconnectedWorkstation1"></a>Steg 1: Förbereda frånkopplade arbetsstationen med Thales HSM
På den frånkopplade arbetsstationen installera programvaran för support nCipher (Thales) på en Windows-dator och sedan koppla en Thales HSM till datorn.

Se till att Thales verktyg som finns i sökvägen **(%nfast_home%\bin** och **%nfast_home%\python\bin**). Skriv till exempel följande:

```
set PATH=%PATH%;”%nfast_home%\bin”;”%nfast_home%\python\bin”
```
Mer information finns i användarhandboken som ingår i Thales HSM eller gå till Thales-webbplatsen för Azure RMS på [http://www.thales-esecurity.com/msrms/cloud](http://www.thales-esecurity.com/msrms/cloud).

##### <a name="BKMK_PrepareDisconnectedWorkstation2"></a>Steg 2: Installera BYOK verktygsuppsättningen på den frånkopplade arbetsstationen
Kopiera BYOK verktygsuppsättningen paketet från USB-enhet eller andra bärbar lagringsenhet och gör sedan följande:

1.  Extrahera filerna från det Hämta paketet till en annan mapp.

2.  Kör vcredist_x64.exe från mappen.

3.  Följ instruktionerna för att installera Visual C++-körtidskomponenter för Visual Studio 2012.

#### <a name="BKMK_InternetGenerate"></a>Skapa din klient-nyckel
På den frånkopplade arbetsstationen följande 3 steg att skapa en egen innehavaren nyckel:

-   [Step 1: Create a security world](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_InternetGenerate1)

-   [Step 2: Validate the downloaded package](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_InternetGenerate2)

-   [Step 3: Create a new key](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_InternetGenerate3)

##### <a name="BKMK_InternetGenerate1"></a>Steg 1: Skapa en värld av säkerhet
Starta en kommandotolk och kör programmet Thales ny värld.

```
new-world.exe --initialize --cipher-suite=DLf1024s160mRijndael --module=1 --acs-quorum=2/3
```
Det här programmet skapar en **säkerhet World** filen % NFAST_KMDATA%\local\world som motsvarar C:\ProgramData\nCipher\Key Management Data\local mapp. Du kan använda olika värden för kvorum men i vårt exempel uppmanas du att ange tre tomt kort och PIN-koder för var och en. Sedan måste två kort ha administratörsbehörighet för säkerhet världen (det angivna kvorumet).  Korten blir den **administratören kort ange** för nya säkerhet världen. Du kan ange lösenordet eller PIN-kod för varje ACS-kort eller lägga till den senare med kommandot i det här skedet.

> [!TIP]
> Du kan kontrollera status för aktuella konfiguration av din HSM med hjälp av den `nkminfo` kommandot.

Sedan gör du följande:

1.  Installera Thales CNG-providern som beskrivs i dokumentationen för Thales och konfigurera den nya säkerhet världen.

2.  Säkerhetskopiera filen world i **%nfast_kmdata%\local**. Säkra och skydda filen världen, administratör kort och sina PIN-koder och se till att ingen enskild har åtkomst till mer än ett kort.

##### <a name="BKMK_InternetGenerate2"></a>Steg 2: Verifiera det Hämta paketet
Det här är valfritt men rekommenderas så att du kan verifiera följande:

-   Nyckeln Key Exchange som ingår i verktygsuppsättningen har skapats från en äkta Thales HSM.

-   Hash för Azure RMS säkerhet världen som ingår i verktygsuppsättningen har skapats i en äkta Thales HSM.

-   Utbytesnyckeln nyckeln kan inte exporteras.

> [!NOTE]
> För att verifiera det Hämta paketet HSM måste vara ansluten, påslagen, och måste ha en värld med säkerhet på den (till exempel ett som du har skapat).

###### Validera det Hämta paketet

1.  Kör skriptet verifykeypackage.py genom att något av följande, beroende på din region:

    -   För Nordamerika:

        ```
        python verifykeypackage.py -k BYOK-KEK-pkg-NA-1 -w BYOK-SecurityWorld-pkg-NA-1
        ```

    -   För Europa:

        ```
        python verifykeypackage.py -k BYOK-KEK-pkg-EU-1 -w BYOK-SecurityWorld-pkg-EU-1
        ```

    -   För Asien:

        ```
        python verifykeypackage.py -k BYOK-KEK-pkg-AP-1 -w BYOK-SecurityWorld-pkg-AP-1
        ```

    > [!TIP]
    > Thales programvaran innehåller en Python tolken vid %NFAST_HOME%\python\bin

2.  Bekräfta att du ser nedan, vilket betyder att du har verifierat: **Resultat:  LYCKADES**

Det här skriptet validerar undertecknare kedjan upp till Thales rotnyckeln. Hash för den här rotnyckeln är inbäddad i skriptet och dess värde bör vara **59178a47 de508c3f 291277ee 184f46c4 f1d9c639**. Du kan också bekräfta det här värdet separat genom att besöka den [Thales webbplats](http://www.thalesesec.com/).

Du är nu redo att skapa en ny nyckel som ska vara din nyckel för RMS-klienten.

##### <a name="BKMK_InternetGenerate3"></a>Steg 3: Skapa en ny nyckel
Skapa en CNG-nyckel med hjälp av Thales **generatekey** och **cngimport** program.

Kör följande kommando för att generera nyckeln:

```
generatekey --generate simple type=RSA size=2048 protect=module ident=contosokey plainname=contosokey nvram=no pubexp=
```
När du kör det här kommandot kan du använda dessa anvisningar:

-   Vi rekommenderar 2048 men stöder även 1024-bitars RSA-nycklar för befintliga AD RMS-kunder som har sådana nycklar och migrerar till Azure RMS för nyckelns storlek.

-   Ersätt värdet *contosokey* för den **inget** och **plainname** med valfritt strängvärde. Om du vill minimera administrativa omkostnader och minska risken för fel, rekommenderar vi att du använder samma värde för båda och Använd alla gemener.

-   Pubexp lämnas tomt (standard) i det här exemplet, men du kan ange specifika värden. Mer information finns i dokumentationen för Thales.

Kör sedan följande kommando för att importera nyckeln till CNG:

```
cngimport --import -M --key=contosokey --appname=simple contosokey
```
När du kör det här kommandot kan du använda dessa anvisningar:

-   Ersätt *contosokey* med samma värde som du angav i [Step 1: Create a security world](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_InternetGenerate1) från den *Generera nyckeln innehavaren* avsnitt.

-   Använd den **- M** alternativet så att nyckeln är lämplig för det här scenariot. Utan, blir nyckeln gällande ett specifikt nyckeln för den aktuella användaren.

Det här kommandot skapar en Tokeniserad nyckel-fil i mappen %NFAST_KMDATA%\local med ett namn som börjar med **key_caping_** följt av en SID. Exempel: **key_caping_machine--801c1a878c925fd9df4d62ba001b94701c039e2fb**. Den här filen innehåller en krypterad nyckel.

> [!TIP]
> Du kan se status för aktuella konfiguration av nycklarna med hjälp av den `nkminfo –k` kommandot.

Säkerhetskopiera nyckeln Tokeniserad filen på en säker plats.

> [!IMPORTANT]
> När du överför senare din nyckel till Azure RMS, exportera inte Microsoft nyckeln till dig så att det blir mycket viktigt att du säkert säkerhetskopierar din nyckel och säkerhet världen. Kontakta Thales för vägledning och bästa praxis för att säkerhetskopiera din nyckel.

Du är nu redo att överföra din klient nyckel till Azure RMS.

#### <a name="BKMK_InternetPrepareTransfer"></a>Förbered din klient nyckel för överföring
På den frånkopplade arbetsstationen 4 följande Förbered klient nyckeln:

-   [Step 1: Create a copy of your key with reduced permissions](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_InternetPrepareTransfer1)

-   [Step 2: Inspect the new copy of the key](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_InternetPrepareTransfer2)

-   [Step 3: Encrypt your key by using Microsoft’s Key Exchange Key](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_InternetPrepareTransfer3)

-   [Step 4: Copy your key transfer package to the Internet-connected workstation](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_InternetPrepareTransfer4)

##### <a name="BKMK_InternetPrepareTransfer1"></a>Steg 1: Skapa en kopia av din nyckel med minskad behörighet
För att minska behörigheter på din klient-nyckel kan du göra följande:

-   Kör något av följande, beroende på din region från en kommandotolk:

    -   För Nordamerika:

        ```
        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-NA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-NA-1
        ```

    -   För Europa:

        ```
        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-EU-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-EU-1
        ```

    -   För Asien:

        ```
        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AP-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AP-1
        ```

När du kör det här kommandot ersätter *contosokey* med samma värde som du angav i [Step 1: Create a security world](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_InternetGenerate1) från den *Generera nyckeln innehavaren* avsnitt.

Du blir ombedd att ansluta din säkerhet world ACS-kort, och om sina lösenord eller en PIN-kod anges...

När kommandot har slutförts visas **resultat: Fungerande** och kopian av din klient nyckel med minskade behörigheter i den fil som heter key_xferacId_*&lt; contosokey &gt;*.

##### <a name="BKMK_InternetPrepareTransfer2"></a>Steg 2: Granska den nya kopian av nyckeln
Du kan också köra Thales verktyg för att bekräfta minimala behörigheter på den nya nyckeln för innehavaren:

-   aclprint.PY:

    ```
    "%nfast_home%\bin\preload.exe" -m 1 -A xferacld -K contosokey "%nfast_home%\python\bin\python" "%nfast_home%\python\examples\aclprint.py"
    ```

-   kmfile-dump.exe:

    ```
    "%nfast_home%\bin\kmfile-dump.exe" "%NFAST_KMDATA%\local\key_xferacld_contosokey"
    ```

När du kör följande kommando ersätter *contosokey* med samma värde som du angav i [Step 1: Create a security world](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_InternetGenerate1) från den *Generera nyckeln innehavaren* avsnitt.

##### <a name="BKMK_InternetPrepareTransfer3"></a>Steg 3: Kryptera din nyckel med hjälp av Microsofts nyckeln utbytesnyckeln
Kör något av följande kommandon, beroende på din region:

-   För Nordamerika:

    ```
    KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-NA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-NA-1 -TenantBposId GUID -KeyFriendlyName ContosoFirstkey
    ```

-   För Europa:

    ```
    KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-EU-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-EU-1 -TenantBposId GUID -KeyFriendlyName ContosoFirstkey
    ```

-   För Asien:

    ```
    KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AP-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AP-1 -TenantBposId GUID -KeyFriendlyName ContosoFirstkey
    ```

När du kör det här kommandot kan du använda dessa anvisningar:

-   Ersätt *contosokey* med det ID som du använde för att generera nyckeln i [Step 1: Create a security world](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_InternetGenerate1) från den *Generera nyckeln innehavaren* avsnitt.

-   Ersätt *GUID* med Azure Active Directory klient-ID som du har hämtat i [Step 2: Get your Azure Active Directory tenant ID](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_PrepareInternetConnectedWorkstation2) från den *förbereda arbetsstationen Internetanslutna* avsnitt.

-   Ersätt *ContosoFirstKey* med en etikett som ska användas för dina utdata-filnamn.

När detta har slutförts den visar **resultat: Fungerande** och det är en ny fil i den aktuella mappen som har följande namn: TransferPackage -*ContosoFirstkey*.byok

##### <a name="BKMK_InternetPrepareTransfer4"></a>Steg 4: Kopiera paketet överföringen av nyckeln till Internet-anslutna arbetsstationen
Använda en USB-enhet eller annan bärbar lagring för att kopiera filen från föregående steg (KeyTransferPackage -*ContosoFirstkey*.byok) på din Internet-anslutna arbetsstation.

> [!NOTE]
> Använd säkerhetspraxis för att skydda filen eftersom den innehåller den privata nyckeln.

#### <a name="BKMK_InternetTransfer"></a>Överföra din klient nyckel till Azure RMS
Så här 3 för att överföra den nya innehavare nyckeln till Azure RMS på arbetsstationen Internetanslutna:

-   [Step 1: Connect to Azure RMS](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_InternetTransfer1)

-   [Step 2: Upload the key package](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_InternetTransfer2)

-   [Step 3: Enumerate your tenant keys – as needed](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_InternetTransfer3)

##### <a name="BKMK_InternetTransfer1"></a>Steg 1: Ansluta till Azure RMS
Gå tillbaka till Windows PowerShell-fönstret och Skriv följande:

1.  Återanslut till den [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] service:

    ```
    Connect-AadrmService
    ```

2.  Använd den [Get-AadrmKeys](http://msdn.microsoft.com/library/windowsazure/dn629420.aspx) cmdlet för att se din aktuella nyckel klientkonfiguration:

    ```
    Get-AadrmKeys
    ```

##### <a name="BKMK_InternetTransfer2"></a>Steg 2: Ladda upp nyckel paketet
Använd den [Lägg till AadrmKey](http://msdn.microsoft.com/library/windowsazure/dn629418.aspx) cmdlet för att ladda upp överföringen av nyckeln paketet som du kopierade från frånkopplade arbetsstationen:

```
Add-AadrmKey –KeyFile <PathToPackageFile> -Verbose
```
> [!WARNING]
> Du uppmanas att bekräfta åtgärden. Det är viktigt att du förstår att den här åtgärden inte kan ångras. När du överför en klient nyckel blir den automatiskt din organisations innehavaren primär nyckel och användarna börjar använda den här nyckeln för klienten när de skyddar dokument och filer.

Om överföringen lyckas visas följande meddelande: **Rights management-tjänsten har lagts till nyckeln.**

Förvänta dig en replikeringsfördröjningen för att ändringen sprids till alla [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] datacenter.

##### <a name="BKMK_InternetTransfer3"></a>Steg 3: Räkna upp din klientorganisationsnycklar – efter behov
Använd cmdlet Get-AadrmKeys igen för att se ändringarna i din klient nyckel och när du vill se en lista över dina nycklar för innehavaren. Klientorganisationsnycklar som visas är den ursprungliga klientadministratörskonto nyckel som genereras av Microsoft och några klientorganisationsnycklar som du har lagt till:

```
Get-AadrmKeys
```
Nyckeln för innehavaren som är markerad **Active** är det som din organisation använder för att skydda dokument och filer.

Du har nu slutfört alla steg som krävs för att sätta en egen nyckel via Internet och kan gå till [Next steps](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_NextSteps).

### <a name="BKMK_BYOK_InPerson"></a>Generera och överför din klient nyckel – personligen
Använd följande procedurer om du inte vill överföra din klient nyckel via Internet, men i stället överföra din klient nyckel personligen.

-   [Generate your tenant key](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_GenerateKey)

-   [Transfer your tenant key to Azure RMS](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_Transfer)

#### <a name="BKMK_GenerateKey"></a>Skapa din klient-nyckel
Så här 3 om du vill skapa en egen innehavaren nyckel:

-   [Step 1: Prepare a workstation with Thales HSM](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_GenerateYourKey1)

-   [Step 2: Create a security world](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_GenerateYourKey2)

-   [Step 3: Create a new key](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_GenerateYourKey3)

##### <a name="BKMK_GenerateYourKey1"></a>Steg 1: Förbered en arbetsstation med Thales HSM
Installera programvara på nCipher (Thales) på en Windows-dator. Koppla en Thales HSM till datorn. Kontrollera Thales verktyg som finns i sökvägen. Mer information finns i användarhandboken som ingår i Thales HSM eller gå till Thales-webbplatsen för Azure RMS på [http://www.thales-esecurity.com/msrms/cloud](http://www.thales-esecurity.com/msrms/cloud).

##### <a name="BKMK_GenerateYourKey2"></a>Steg 2: Skapa en värld av säkerhet
Starta en kommandotolk och kör programmet Thales ny värld.

```
new-world.exe --initialize --cipher-suite=DLf1024s160mRijndael --module=1 --acs-quorum=2/3
```
Det här programmet skapar en **säkerhet World** filen % NFAST_KMDATA%\local\world som motsvarar C:\ProgramData\nCipher\Key Management Data\local mapp. Du kan använda olika värden för kvorum men i vårt exempel uppmanas du att ange tre tomt kort och PIN-koder för var och en. Två kort ge sedan fullständig åtkomst till hela världen säkerhet.  Korten blir den **administratören kort ange** för nya säkerhet världen.

Sedan gör du följande:

1.  Installera Thales CNG-providern som beskrivs i dokumentationen för Thales och konfigurera den nya säkerhet världen.

2.  Säkerhetskopiera filen världen. Säkra och skydda filen världen, administratör kort och sina PIN-koder och se till att ingen enskild har åtkomst till mer än ett kort.

Du är nu redo att skapa en ny nyckel som ska vara din nyckel för RMS-klienten.

##### <a name="BKMK_GenerateYourKey3"></a>Steg 3: Skapa en ny nyckel
Skapa en CNG-nyckel med hjälp av Thales **generatekey** och **cngimport** program.

Kör följande kommando för att generera nyckeln:

```
generatekey --generate simple type=RSA size=2048 protect=module ident=contosokey plainname=contosokey nvram=no pubexp=
```
När du kör det här kommandot kan du använda dessa anvisningar:

-   Vi rekommenderar 2048 men stöder även 1024-bitars RSA-nycklar för befintliga AD RMS-kunder som har sådana nycklar och migrerar till Azure RMS för nyckelns storlek.

-   Ersätt värdet *contosokey* för den **inget** och **plainname** med valfritt strängvärde. Om du vill minimera administrativa omkostnader och minska risken för fel, rekommenderar vi att du använder samma värde för båda och Använd alla gemener.

-   Pubexp lämnas tomt (standard) i det här exemplet, men du kan ange specifika värden. Mer information finns i dokumentationen för Thales.

Kör sedan följande kommando för att importera nyckeln till CNG:

```
cngimport --import –M --key=contosokey --appname=simple contosokey
```
När du kör det här kommandot kan du använda dessa anvisningar:

-   Ersätt *contosokey* med samma värde som du angav i steg 1.

-   Använd den **- M** alternativet så att nyckeln är lämplig för det här scenariot. Utan, blir nyckeln gällande ett specifikt nyckeln för den aktuella användaren.

Det här kommandot skapar en Tokeniserad nyckel-fil i mappen %NFAST_KMDATA%\local med ett namn som börjar med **key_caping_** följt av en SID. Exempel: **key_caping_machine--801c1a878c925fd9df4d62ba001b94701c039e2fb**. Den här filen innehåller en krypterad nyckel.

Säkerhetskopiera nyckeln Tokeniserad filen på en säker plats.

> [!IMPORTANT]
> När du överför senare din nyckel till Azure RMS, har Microsoft en oåterkalleligt kopia av din nyckel. Det innebär att ingen kan hämta nyckeln från HSM hos Microsoft. På så sätt kan du behålla exklusiv kontroll över din klient-nyckel. Därför blir det mycket viktigt att du säkert säkerhetskopierar din nyckel och säkerhet världen. Kontakta Thales för vägledning och bästa praxis för att säkerhetskopiera din nyckel.

Du är nu redo att överföra din klient nyckel till Azure RMS.

#### <a name="BKMK_Transfer"></a>Överföra din klient nyckel till Azure RMS
När du har genererat en egen nyckel kan överföra du den till Azure RMS innan du använder den. Den här överföringen är en manuell process som kräver att du Lägg till Microsoft office i Redmond, Washington, USA för den högsta säkerhetsnivån. Om du vill slutföra processen genom att följa dessa 3 steg:

-   [Step 1: Bring your key to Microsoft](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_TransferYourKey1)

-   [Step 2: Transfer your key to the Window Azure RMS security world](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_TransferYourKey2)

-   [Step 3: Closing procedures](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_TransferYourKey3)

###### Steg 1: Ta din nyckel till Microsoft

-   Kontakta Microsofts kundtjänst (CSS) att schemalägga en nyckel överför möte för Azure RMS. Hämta följande till Microsoft i Redmond:

    -   Kvorum för dina administrativa kort. Om du har följt anvisningarna i föregående [Step 2: Create a security world](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_GenerateYourKey2), detta är några två av tre kort.

    -   Personal som har behörighet att utföra administrativa korten och PIN-koder, vanligtvis två (en för varje kort).

    -   Säkerhet World filen (% NFAST_KMDATA%\local\world) på en USB-enhet.

    -   Tokeniserad nyckelfilen på en USB-enhet.

###### Steg 2: Överföra din nyckel till Windows Azure RMS säkerhet världen

1.  När du kommer till Microsoft för att överföra din nyckel händer följande:

    -   Microsoft ger dig en offline arbetsstation som har en Thales HSM kopplade, Thales installerad programvara och en förinstallerade Azure RMS säkerhet World filen till mappen C:\Temp\Destination.

    -   På den här arbetsstationen du läsa in din säkerhet World fil- och Tokeniserad nyckelfilen från USB-enheten till mappen C:\Temp\Source.

    -   Azure RMS operatörer överför på ett säkert sätt din nyckel till Azure RMS säkerhet världen med Thales verktyg.

    Den här processen ser ut ungefär så följande, där den sista parametern för nyckeln xfer im i det här exemplet ersätts av dina Tokeniserad nyckel-filnamn:

    **C:\ &gt; mk reprogram.exe--ägare c:\Temp\Destination lägga till c:\Temp\Source**

    **C:\ &gt; nyckel-xfer-im.exe c:\Temp\Source c:\Temp\Destination--modulen c:\Temp\Source\key_caping_machine--801c1a878c925fd9df4d62ba001b94701c039e2fb**

2.  MK omprogrammera ber du och Azure RMS-operatörer att ansluta sina respektive administratör kort och PIN-koder. De här kommandona utdata Tokeniserad nyckelfilen i C:\Temp\Destination som innehåller din nyckel som skyddas av Azure RMS säkerhet världen.

###### Steg 3: Stänger procedurer

-   I din närvaro gör Azure RMS operatörer du följande:

    -   Köra ett verktyg som utvecklats av Microsoft tillsammans med Thales som tar bort två behörigheter: Behörighet att återställa nyckeln och behörighet att ändra behörigheter. Den här kopian av din nyckel är låst till Azure RMS säkerhet världen när det är klart. Thales HSM tillåter inte Azure RMs operatörer med sina administratör kort att återställa klartext kopia av din nyckel.

    -   Kopiera den resulterande nyckelfilen till en USB-enhet för att överföra senare till tjänsten Azure RMS.

    -   Fabriksåterställning HSM och rensa arbetsstationen ren.

Du har nu slutfört alla de steg som krävs för sätta egna nyckeln personliga och kan gå tillbaka till din organisation i nästa steg.

## <a name="BKMK_NextSteps"></a>Nästa steg

1.  Börja använda din klient nyckel:

    -   Om du inte redan gjort det, måste du nu aktivera Rights Management så att din organisation kan börja använda RMS. Användare börja omedelbart använda din klient-nyckel (hanteras av Microsoft eller hanteras av du).

        Mer information om aktivering finns [Aktivera Azure Rights Management](../Topic/Activating_Azure_Rights_Management.md).

    -   Om du har redan aktiverats Rights Management och vill hantera din egen innehavaren nyckel, användare gradvis övergång från den gamla klient nyckeln till den nya nyckeln för klienten och successiva övergången kan ta några veckor ska slutföras. Dokument och filer som är skyddade med den gamla nyckeln för klienten är fortfarande tillgängliga för auktoriserade användare.

2.  Överväg att aktivera användningsloggning som loggar varje transaktion som utför RMS.

    Om du vill hantera innehavare nyckeln innehåller loggning information om hur du använder din klient-nyckel. Finns i följande exempel på en loggfil som visas i Excel där den **dekryptera** och **SignDigest** begära typer visar att nyckeln för klienten används.

    ![](../Image/RMS_Logging.gif)

    Mer information om användningsloggning finns [Loggning och analysera Azure Rights Management användning](../Topic/Logging_and_Analyzing_Azure_Rights_Management_Usage.md).

3.  Underhålla din klient-nyckel.

    Mer information finns i [Åtgärder för din Azure Rights Management-klient nyckel](../Topic/Operations_for_Your_Azure_Rights_Management_Tenant_Key.md).

## Se även
[Konfigurera Azure Rights Management](../Topic/Configuring_Azure_Rights_Management.md)

