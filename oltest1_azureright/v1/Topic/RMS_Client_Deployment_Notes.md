---
description: na
keywords: na
title: RMS Client Deployment Notes
search: na
ms.date: na
ms.service: rights-management
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 03cc8c6f-3b63-4794-8d92-a5df4cdf598f
---
# RMS klientdistribution anteckningar
Rights Management-tjänsten client (RMS-klienten) version 2 kallas också MSIPC-klienten. Det är programvara för Windows-datorer som kommunicerar med Microsoft Rights Management services lokalt eller i molnet för att skydda åtkomsten till och användning av information som den flödar genom program och enheter inom gränser i din organisation eller utanför de hanterade gränser. Förutom leverans med den [delningsapplikation för Windows Rights Management](https://technet.microsoft.com/library/dn919648.aspx), RMS-klienten är tillgänglig [som en valfri uppdatering](http://www.microsoft.com/download/details.aspx?id=38396) som kan med bekräftelse och godkännande av ett licensavtal, fritt distribueras med programvara från tredje part så att klienter kan skydda och allt innehåll som har skyddats av Rights Management services.

Det här avsnittet finns i följande avsnitt:

-   [Distribuerar RMS-klienten](#BKMK_RedistributeInstaller)

-   [Installera RMS-klienten](#BKMK_InstallClient)

-   [Frågor och svar om RMS-klienten](#BKMK_QA)

-   [RMS-klienten inställningar](#BKMK_Settings)

-   [Endast AD RMS: Begränsa RMS-klienten att använda betrodda AD RMS-servrar](#BKMK_UsingTrustedServers)

-   [Identifiering av RMS-tjänsten](#BKMK_ServiceDiscovery)

## <a name="BKMK_RedistributeInstaller"></a>Distribuerar RMS-klienten
RMS-klienten kan distribueras fritt och tillsammans med andra program och IT-lösningar. Om du är en programutvecklare eller lösning provider och vill distribuera RMS-klienten har två alternativ:

-   Rekommenderas: Bädda in installationsprogram för RMS-klienten i installationen av programmet och körs i tyst läge (den **/quiet** switch som beskrivs i nästa avsnitt).

-   Kontrollera RMS-klienten krävs för programmet. Med det här alternativet kan du behöva ge användare med ytterligare instruktioner att hämta, installera och uppdatera sina datorer med klienten innan de kan använda programmet.

## <a name="BKMK_InstallClient"></a>Installera RMS-klienten
RMS-klienten ingår i en installer körbar fil med namnet **setup_msipc_***&lt; arch &gt;***.exe**, där *&lt; arch &gt;* är antingen **x86** (för 32-bitars klientdatorer) eller **x64** (för 64-bitars klientdatorer). 64-bitars (x 64) installer-paketet installerar både en 32-bitars runtime körbara för kompatibilitet med 32-bitars program som körs på en 64-bitars operativsystem installation, samt en 64-bitars runtime körbara för att stödja intern 64-bitars program. Installationsprogram för 32-bitars (x 86) körs inte på en 64-bitars Windows-installation.

> [!NOTE]
> Du måste förhöjd behörighet för att installera RMS-klienten som medlem i gruppen Administratörer på den lokala datorn.

Du kan installera RMS-klienten med någon av följande installationsmetoder:

-   **Tyst läge.** Med hjälp av den **/quiet** Växla som en del av kommandoradsalternativ kan du installera RMS-klienten på datorer bakgrunden. I följande exempel visas en installation i tyst läge för RMS-klienten på en 64-bitars klientdator:

    ```
    setup_msipc_x64.exe /quiet
    ```

-   **Interaktivt läge.** Alternativt kan installera du RMS-klienten med hjälp av Grafiskt-baserade installationsprogrammet som tillhandahålls av installationsguiden för RMS-klienten. Genom att dubbelklicka på installer-paketet RMS-klienten (**setup_msipc_***&lt; arch &gt;***.exe**) i mappen där det kopieras eller hämtas på den lokala datorn.

## <a name="BKMK_QA"></a>Frågor och svar om RMS-klienten
Följande avsnitt innehåller vanliga frågor och svar om RMS-klienten och svaren på dem.

### Vilka operativsystem stöder RMS-klienten?
RMS-klienten kan användas med följande operativsystem:

|Windows-serveroperativsystem|Windows-klientoperativsystem|
|--------------------------------|--------------------------------|
|Windows Server 2012 R2|Windows 8.1|
|Windows Server 2012|Windows 8|
|Windows Server 2008 R2|Windows 7 med minsta SP1|
|Windows Server 2008 (endast AD RMS)|Windows Vista med minst SP2 (endast AD RMS)|

### Vilka processorer eller plattformar stöd för RMS-klienten?
RMS-klienten stöds på x 86 och x 64-datorer plattformar.

### Där installeras RMS-klienten
Som standard RMS-klienten installeras i %ProgramFiles%\Active Directory Rights Management Services Client 2. &lt; lägre versionsnummer &gt;.

### Vilka filer som är associerade med RMS-klientprogrammet?
Följande filer installeras som en del av RMS-klientprogrammet:

-   Msipc.dll

-   Ipcsecproc.dll

-   Ipcsecproc_ssp.dll

-   MSIPCEvents.man

Förutom de här filerna installeras RMS-klienten också flera gränssnitt (MUI) support användarfiler 44 språk. Kontrollera de språk som stöds kör klientinstallation RMS och granska innehållet i stöd för flera språk mapparna under standardsökvägen när installationen är klar.

### Är RMS-klienten som ingår som standard när jag installerar operativsystemet stöds?
Nej. Den här versionen av RMS-klienten som levereras som en valfri uppdatering som kan installeras separat på datorer som kör versioner av Microsoft Windows-operativsystem som stöds.

### RMS-klienten uppdateras automatiskt av Microsoft Update?
Om du har installerat RMS-klienten med hjälp av alternativet tyst installation ärver RMS-klienten de aktuella inställningarna för Microsoft Update. Om du har installerat RMS-klienten med hjälp av installationsprogrammet med Grafiskt uppmanas installationsguiden för RMS-klienten du att aktivera Microsoft Update.

## <a name="BKMK_Settings"></a>RMS-klienten inställningar
Följande avsnitt innehåller för inställningsinformation om RMS-klienten. Den här informationen kan vara användbart om du har problem med program eller tjänster som använder RMS-klienten.

> [!NOTE]
> Vissa inställningar är beroende av om enlightened RMS-programmet körs som en läge klientprogrammet (till exempel Microsoft Word och Outlook och RMS-delning) eller serverprogram läge (till exempel SharePoint och Exchange).  I följande tabeller inställningarna identifieras **klientläge** och **Server-läge**, respektive.

### Där lagras för RMS-klienten licenser på klientdatorer
RMS-klienten lagrar licenser på datorns lokala hårddisk och cachelagrar också information i Windows-registret.

|Beskrivning|Klienten läge sökvägar|Server-läge sökvägar|
|---------------|--------------------------|------------------------|
|Lagringsplats för licens|%localappdata%\Microsoft\MSIPC|%ALLUSERSPROFILE%\Microsoft\MSIPC\Server\*&lt; SID &gt;*\|
|Lagringsplats för mall|%localappdata%\Microsoft\MSIPC\Templates|%ALLUSERSPROFILE%\Microsoft\MSIPC\Server\Templates\*&lt; SID &gt;*\|
|Plats i registret|HKEY_CURRENT_USER<br /> \Software<br /> \Classes<br /> \Local inställningar<br /> \Software<br /> \Microsoft<br /> \MSIPC|HKEY_CURRENT_USER<br /> \Software<br /> \Microsoft<br /> \MSIPC<br /> \Server<br /> \*&lt; SID &gt;*|
> [!NOTE]
> *&lt; SID &gt;* är säker-ID (SID) för kontot som programmet körs under. Exempel: om programmet körs under kontot Network Service inbyggda ersätta *&lt; SID &gt;* med värdet för välkända SID för kontot (S-1-5-20).

### Windows-registerinställningar för RMS-klienten
Du kan använda Windows-registernycklar för att ange eller ändra vissa konfigurationer för RMS-klienten. Till exempel som administratör för RMS-enlightened program som kommunicerar med AD RMS-servrar kan du kanske vill uppdatera enterprise service plats (Åsidosätt AD RMS-server som är markerad för publicering) beroende på klientdatorns aktuella plats i Active Directory-replikeringstopologin. Eller du kanske vill aktivera RMS spårning på klientdatorn för felsökning av problem med ett program med RMS-enlightened. Använd följande tabell för att identifiera registerinställningarna som du kan ändra för RMS-klienten.

|Aktivitet|Inställningar|
|-------------|-----------------|
|Endast AD RMS: Uppdatera enterprise service platsen för en klientdator|Uppdatera följande registernycklar:<br /><br />-   HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\ServiceLocation\EnterpriseCertification<br />    REG_SZ: standard<br />    **Värde:**&lt; http eller https &gt; :// *RMS_Cluster_Name*/_wmcs/Certification<br />-   HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\ServiceLocation\EnterprisePublishing<br />    REG_SZ: standard<br />    **Värde:** &lt; http eller https &gt; :// *RMS_Cluster_Name*/_wmcs/Licensing|
|Aktivera och inaktivera spårning|Uppdatera följande registernyckel:<br /><br />-   HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC<br />    REG_DWORD: Spårningen<br />    **Värde:** 1 för att aktivera spårning 0 om du vill inaktivera spårning (standard)|
|Ändra frekvensen i dagar och uppdatera mallar|Följande registervärden anger hur ofta mallar uppdateras på användarens dator om TemplateUpdateFrequencyInSeconds-värdet är inte.  Om inget av dessa värden är inställda är standardintervallet för program med RMS-klienten (version 1.0.1784.0) hämta mallar för dag. Versioner innan det har ett standardvärde varje 7 dagar.<br /><br />**Klientläge:**<br /><br />-   HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC<br />    REG_DWORD: TemplateUpdateFrequency<br />    **Värde:** Ett heltal som anger hur många dagar (minst 1) mellan hämtningsbara filer.<br /><br />**Server-läge:**<br /><br />-   HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\Server\*&lt; SID &gt;*<br />    REG_DWORD: TemplateUpdateFrequency<br />    **Värde:** Ett heltal som anger hur många dagar (minst 1) mellan hämtningsbara filer.|
|Så här ändrar du frekvens i sekunder för att uppdatera mallar **Important:** Om detta anges ignoreras värdet att uppdatera mallar i dagar. Ange en eller andra, inte båda.|Följande registervärden anger hur ofta mallar uppdateras på användarens dator. Om det här värdet eller värdet du ändrar frekvensen i dagar (TemplateUpdateFrequency) inte har angetts är standardintervallet för program med RMS-klienten (version 1.0.1784.0) hämta mallar för dag. Versioner innan det har ett standardvärde varje 7 dagar.<br /><br />**Klientläge:**<br /><br />-   HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC<br />    REG_DWORD: TemplateUpdateFrequencyInSeconds<br />    **Värde:** Ett heltal som anger hur många sekunder (minst 1) mellan hämtningsbara filer.<br /><br />**Server-läge:**<br /><br />-   HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\Server\*&lt; SID &gt;*<br />    REG_DWORD: TemplateUpdateFrequencyInSeconds<br />    **Värde:** Ett heltal som anger hur många sekunder (minst 1) mellan hämtningsbara filer.|
|Endast AD RMS: Hämta mallar direkt på nästa publicering begäran|Du kanske vill RMS-klienten att hämta mallar så snart som möjligt under testning och utvärderingar. Genom att ta bort följande registernyckel och RMS-klienten ska hämta mallar direkt på nästa publicering begäran i stället för att vänta på den tid som anges av TemplateUpdateFrequency registerinställning:<br /><br />-   HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC\ &lt; servernamn &gt; \Template **Note:** &lt; servernamn &gt; kan ha extern (corprights.contoso.com) och URL: er för intern (corprights) och därför två olika poster.|
|Endast AD RMS: Aktivera stöd för federerad autentisering|Om RMS-klientdatorn ansluter till AD RMS-kluster med hjälp av en federerad förtroende, måste du konfigurera federationens hemsfär.<br /><br />-   HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\Federation<br />    REG_SZ: FederationHomeRealm<br />    **Värde:** Värdet för registerposten är uniform resource identifier (URI) för federationstjänsten (till exempel "https://fs-01.contoso.com").|
|Endast AD RMS: Stöd för partner federationsservrar som kräver formulärbaserad autentisering för användarindata|RMS-klienten körs i tyst läge och användarindata krävs inte som standard. Partner federationsservrar kan dock konfigureras för att kräva användarindata sådana som som formulärbaserad autentisering. I så fall måste du konfigurera RMS-klienten Ignorera tyst läge så att formuläret federerad autentisering visas i ett webbläsarfönster och användaren upphöja för autentisering.<br /><br />-   HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\Federation<br />    REG_DWORD: EnableBrowser **Note:** Om federationsservern konfigureras för formulärbaserad autentisering kan är den här nyckeln obligatoriskt. Den här nyckeln är inte krävs om federationsservern har konfigurerats för att använda integrerad Windows-autentisering.|
|Endast AD RMS: Så här blockerar du ILS förbrukning|RMS-klienten gör mycket innehåll som skyddas av tjänsten ILS som standard, men du kan konfigurera klienten så att blockera den här tjänsten genom att ange följande registernyckel. Om den här registernyckeln är inställt på blockera tjänsten ILS, alla försök öppna och allt innehåll som skyddas av tjänsten ILS returneras följande fel:<br />HRESULT_FROM_WIN32(ERROR_ACCESS_DISABLED_BY_POLICY)<br /><br />-   HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC<br />    REG_DWORD: **DisablePassportCertification**<br />    **Värde:** 1 för att blockera ILS förbrukning 0 för att ILS förbrukning (standard)|

### Hantera Distribution av mallen för RMS-klienten
Mallar gör det lätt för användare och administratörer att snabbt använda Rights Management skydd och RMS-klienten laddar ned automatiskt mallar från dess RMS-servrar eller tjänst om du placerar mallarna i följande plats, RMS-klienten inte kan hämta alla mallar från standardplatsen och hämta mallar som du har placerat i den här mappen i stället. RMS-klienten kan fortsätta att hämta mallar från andra tillgängliga RMS-servrar.

**Klientläge:** %localappdata%\Microsoft\MSIPC\UnmanagedTemplates

**Server-läge:** %allusersprofile%\Microsoft\MSIPC\Server\UnmanagedTemplates\*&lt; SID &gt;*

När du använder den här mappen, det finns inga särskilda namngivningskonvention krävs förutom att mallarna ska utfärdas av RMS-servern eller tjänsten och de måste ha filnamnstillägget .xml. Till exempel är Contoso Confidential.xml eller Contoso ReadOnly.xml giltiga namn.

## <a name="BKMK_UsingTrustedServers"></a>Endast AD RMS: Begränsa RMS-klienten att använda betrodda AD RMS-servrar
RMS-klienten kan vara begränsad till med endast specifika betrodda AD RMS-servrar genom att göra följande ändringar i Windows-registret på lokala datorer.

**Om du vill aktivera begränsa RMS betrodda-klienten ska endast använda AD RMS-servrar**

-   HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\TrustedServers\
    REG_DWORD: AllowTrustedServersOnly

    **Värde:** Om du anger värdet noll litar RMS-klienten på de angivna servrar som har konfigurerats i listan TrustedServers och Azure Rights Management-tjänsten.

**Lägga till medlemmar i listan över betrodda AD RMS-servrar**

-   HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\TrustedServers\
    REG_SZ: *&lt; URL_or_HostName &gt;*

    **Värde:** Strängvärden som lagts till i den här nyckeln registerplatsen kan vara antingen DNS-domän namnformat (till exempel **adrms.contoso.com**) eller fullständiga URL: er till betrodda AD RMS-servrar (till exempel **https://adrms.contoso.com**). Om en angiven URL som börjar med **https://**,  RMS-klienten ska använda SSL- eller TLS för att kontakta den angivna AD RMS-servern.

## <a name="BKMK_ServiceDiscovery"></a>Identifiering av RMS-tjänsten
Identifiering av RMS kan kontrollera vilka RMS-server eller en tjänst ska kunna kommunicera med innan du skyddar innehållet RMS-klienten. Identifiering av tjänsten kan också inträffa när RMS-klienten förbrukar skyddat innehåll, men det är mindre troligt att bero på att principen kopplat till innehållet innehåller önskad RMS-server eller tjänst och bara om som misslyckas har klienten kör identifiering.

Identifiering av först letar efter en lokala version av Rights Management (AD RMS). Om som misslyckas söker automatiskt identifiering för moln-versionen av Rights Management (Azure RMS).

För att utföra identifiering för ett lokalt distribution kontrollerar RMS-klienten följande:

1.  Windows-registret på den lokala datorn: Om inställningar för identifiering av tjänsten konfigureras i registret, används de här inställningarna först.  Inställningarna har inte konfigurerats i registret som standard.

2.  Active Directory Domain Services: En domänanslutna dator frågar Active Directory efter en tjänstanslutningspunkt (SCP). Om en Tjänstanslutningspunkt är registrerad returneras URL för RMS-server till RMS-klienten att använda.

### Endast AD RMS: Aktivera identifiering av serversidan med hjälp av Active Directory
Om ditt konto har tillräcklig behörighet (Företagsadministratörer och lokal administratör för AD RMS-server), kan du automatiskt registrera en tjänstanslutningspunkt (SCP) när du installerar AD RMS underliggande-klusterserver. Om det redan finns en Tjänstanslutningspunkt i skogen måste du först radera befintliga SCP innan du kan registrera en ny.

Du kan registrera och ta bort en Tjänstanslutningspunkt när AD RMS installeras genom att använda följande procedur. Innan du börjar måste du kontrollera att ditt konto har behörighet (Företagsadministratörer och lokal administratör för AD RMS-server).

##### Aktivera identifiering av AD RMS-tjänst genom att registrera en SCP i Active Directory

1.  Öppna konsolen Active Directory Management Services på AD RMS-server:

    -   Om du använder Windows Server 2008 R2 eller Windows Server 2008 klickar du på **Starta**, klickar du på **Administrationsverktyg**, och klicka sedan på **Active Directory Rights Management Services**.

    -   Om du använder Windows Server 2012 R2 eller Windows Server 2012 i Serverhanteraren, klickar du på **Verktyg**, och klicka sedan på **Active Directory Rights Management Services**.

2.  Högerklicka på AD RMS-kluster i AD RMS-konsolen och klicka sedan på **Egenskaper**.

3.  Klicka på den **SCP** fliken.

4.  Välj den **Byt SCP** kryssrutan.

5.  Välj den **Ange SCP till den aktuella certifieringsklustret** alternativ och klickar sedan på **OK**.

### Aktivera identifiering av klientsidans med hjälp av Windows-registret
Som ett alternativ till att använda en Tjänstanslutningspunkt eller där en Tjänstanslutningspunkt finns inte kan konfigurera du registret på klientdatorn så att RMS-klienten kan hitta sin AD RMS-server.

##### Aktivera identifiering av klientsidans AD RMS med Windows-registret

1.  Öppna Registereditorn, Regedit.exe:

    -   Skriv på klientdatorn i fönstret kör **regedit**, och tryck sedan på RETUR för att öppna Registereditorn.

2.  I Registereditorn navigerar du till **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC**.

    > [!IMPORTANT]
    > Om du kör en 32-bitars program på en 64-bitars dator är sökvägen följande: 
    > **HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\MSIPC**

3.  Om du vill skapa den ServiceLocation, högerklickar du på **MSIPC**, peka på **nya**, klickar du på **nyckel**, och skriv sedan **ServiceLocation**.

4.  Om du vill skapa den EnterpriseCertification, högerklickar du på **ServiceLocation**, peka på **nya**, klickar du på **nyckel**, och skriv sedan **EnterpriseCertification**.

5.  Ange URL: en certifiering enterprise Dubbelklicka på den **(standard)** värde under den **EnterpriseCertification** nyckel, och när den **Redigera sträng** i dialogrutan för **värde data**, typ &lt;http or https&gt;://*AD RMS_cluster_name*/_wmcs/Certification, och klicka sedan på **OK**.

6.  Om du vill skapa den EnterprisePublishing, högerklickar du på **ServiceLocation**, peka på **nya**, klickar du på **nyckel**, och skriv sedan EnterprisePublishing.

7.  Om du vill ange företaget publicerar URL dubbelklickar du på **(standard)** , under den **EnterprisePublishing** nyckel, och när den **Redigera sträng** dialogrutan visas, Skriv för **värde data** följande &lt;http or https&gt;://*AD RMS_cluster_name*/_wmcs/Licensing, och klicka sedan på **OK**.

8.  Stäng Registereditorn.

Identifiering av tjänstanrop för AD RMS misslyckas om RMS-klienten kan inte hitta en Tjänstanslutningspunkt genom att fråga Active Directory och det inte har angetts i registret.

### Omdirigerar Licensing Server-trafik
I vissa fall kan behöva du omdirigera trafik under tjänstidentifiering av, till exempel när två organisationer slås samman och den gamla volymlicensavtal servern i en organisation slutade och klienter behöver omdirigeras till en ny volymlicensavtal server. Eller du migrera från AD RMS till Azure RMS. Använd följande procedur om du vill aktivera volymlicensavtal omdirigering.

##### Så här aktiverar du RMS licensing omdirigering med hjälp av Windows-registret

1.  Öppna Registereditorn, Regedit.exe:

    -   Skriv på klientdatorn i fönstret kör **regedit**, och tryck sedan på RETUR för att öppna Registereditorn.

2.  I Registereditorn navigerar du till något av följande:

    -   För 64-bitarsversionen av Office på x 64-plattform: HKLM\SOFTWARE\Microsoft\MSIPC\Servicelocation

    -   För 32-bitarsversion av Office på x 64-plattform: HKLM\SOFTWARE\Wow6432Node\Microsoft\MSIPC\Servicelocation

3.  Skapa en LicensingRedirection-nyckel genom att högerklicka **Servicelocation**, peka på **nya**, klickar du på **nyckel**, och skriv sedan **LicensingRedirection**.

4.  Om du vill ange volymlicensavtal omdirigering högerklickar du på den **LicensingRedirection** nyckel, väljer **nya**, och välj sedan **strängvärde**.  För **namn**, ange den tidigare servern licensing URL och **värdet** ange den nya servern licensing URL.

    Till exempel vill dirigera licensing från en server på Contoso.com till en på Fabrikam.com, kan du ange följande värden:

    **Namn:** `https://contoso.com/_wmcs/licensing`

    **Värde:** `https://fabrikam.com/_wmcs/licensing`

    > [!NOTE]
    > Om den gamla volymlicensavtal servern har både intranät och extranät-URL: er anges sedan ett nytt namn och värdemappning måste anges för båda dessa webbadresser under nyckeln LicensingRedirection.

5.  Upprepa det föregående steget för alla servrar som ska omdirigeras.

6.  Stäng Registereditorn.

