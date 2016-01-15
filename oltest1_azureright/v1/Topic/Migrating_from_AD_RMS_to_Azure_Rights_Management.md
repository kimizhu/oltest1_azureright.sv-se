---
description: na
keywords: na
title: Migrating from AD RMS to Azure Rights Management
search: na
ms.date: na
ms.service: rights-management
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 828cf1f7-d0e7-4edf-8525-91896dbe3172
---
# Migrera fr&#229;n AD RMS till Azure Rights Management
Använd följande instruktioner för att migrera din distribution av Active Directory Rights Management Services (AD RMS) till Azure Rights Management (Azure RMS). Efter migreringen, användare kommer fortfarande ha åtkomst till dokument och e-postmeddelanden som din organisation skyddas med hjälp av AD RMS och nyligen skyddat innehåll använder Azure RMS.

Osäker om AD RMS migreringen passar din organisation?

-   En introduktion till Azure RMS, affärsproblem som den kan lösa, ser det ut för administratörer och användare och hur det fungerar finns i [Vad är Azure Rights Management?](../Topic/What_is_Azure_Rights_Management_.md)

-   En jämförelse av Azure RMS med AD RMS finns [Jämföra Azure Rights Management och AD RMS](../Topic/Comparing_Azure_Rights_Management_and_AD_RMS.md).

## Förutsättningar för att migrera AD RMS till Azure RMS
Innan du påbörjar migreringen till Azure RMS, kontrollera att följande krav är uppfyllda och att du förstår några begränsningar.

|Krav|Mer information|
|--------|-------------------|
|En RMS-distribution som stöds|Alla versioner av AD RMS från Windows Server 2008 och Windows Server 2012 R2 stöder en migrering till Azure RMS:<br /><br />-   Windows Server 2008 (x 86 eller x 64)<br />-   Windows Server 2008 R2 (x 64)<br />-   Windows Server 2012 (x 64)<br />-   Windows Server 2012 R2 (x 64) **Note:** Om du kör Windows RMS på Windows Server 2003, kommer den här versionen av operativsystemet inte stöd under 2015. Du kan migrera den här versionen av RMS till Azure RMS, men den här processen stöds endast om operativsystemet fortfarande stöds. Som en lösning kan du importera dina betrodd publiceringsdomän (betrodda Publiceringsdomänen) till en version av AD RMS som stöds och sedan importera den betrodda Publiceringsdomänen utan alternativet RMS 1.0 kompatibilitet. Mer information om betrodda publiceringsdomäner finns [betrodd publiceringsdomän](http://technet.microsoft.com/library/dd996639%28v=ws.10%29.aspx)<br />Alla giltiga AD RMS-topologier stöds:<br /><br />-   En enda skog, enstaka RMS-kluster<br />-   Skog, flera bara RMS-kluster<br />-   Flera skogar, flera RMS-kluster **Note:** Som standard Migrera flera RMS-kluster till ett enda Azure RMS-klienten. Om du vill annat RMS-innehavare, måste du hantera dem som olika migreringar. En nyckel från en RMS-klustret kan inte importeras till mer än en Azure RMS-klienten.|
|Alla krav för att köra Azure RMS, inklusive en Azure RMS-klient (aktiveras inte)|Se [Krav för Azure Rights Management](../Topic/Requirements_for_Azure_Rights_Management.md).<br /><br />Men du måste ha en Azure RMS-klienten innan du kan migrera från AD RMS, rekommenderar vi att du inte aktivera Rights Management-tjänsten innan migreringen. Migreringen innehåller det här steget när du har exporterat nycklar och mallar från AD RMS och importera dem till Azure RMS. Om Azure RMS har redan aktiverats, kan du dock fortfarande migrera från AD RMS.|
|Förberedelser för Azure RMS:<br /><br />-   Katalogsynkronisering mellan din lokala katalog och Azure Active Directory<br />-   E-postaktiverade grupper i Azure Active Directory|Se [Förbereder Azure Rights Management](../Topic/Preparing_for_Azure_Rights_Management.md).|
|Om du har använt funktionen Information Rights Management (IRM) i Exchange Server (till exempel regler och Outlook Web Access) eller SharePoint-Server med AD RMS:<br /><br />-   Planera för en kort tidsperiod när IRM är inte tillgängliga på dessa servrar|Du kan fortsätta att använda IRM på dessa servrar med Azure RMS efter migreringen. Ett steg migrering är dock att tillfälligt inaktivera IRM-tjänsten, installera och konfigurera en anslutning, konfigurera om servrarna och sedan återaktivera IRM.<br /><br />Detta är endast avbrott till tjänsten under migreringen.|
Begränsningar:

-   Migreringen stöder migrera din licensiering certifikatet (Serverlicensgivarcertifikat) nyckel till en maskinvarusäkerhetsmodul (HSM) för Azure RMS-server, stöder Exchange Online för närvarande inte den här konfigurationen. Om du vill att alla IRM-funktioner med Exchange Online när du har migrerat till Azure RMS, din nyckel för Azure RMS-klienten måste vara [hanteras av Microsoft](http://technet.microsoft.com/library/dn440580.aspx). Du kan också köra IRM med begränsad funktionalitet i Exchange Online när din Azure RMS-klient som hanteras av dig (BYOK). Mer information om hur du använder Exchange Online med Azure RMS finns [Step 6. Configure IRM integration for Exchange Online](#BKMK_Step6Migration) i dessa instruktioner.

-   Om du har programvara och klienter som inte stöds med Azure RMS kan att de inte kunna skydda eller använda innehåll som skyddas av Azure RMS. Kontrollera att program som stöds och klienter i avsnittet den [Krav för Azure Rights Management](../Topic/Requirements_for_Azure_Rights_Management.md) artikeln.

-   Om du importerar den lokala nyckeln till Azure RMS som arkiveras (du inte anger den betrodda Publiceringsdomänen ska vara aktiv under importen) och du migrerar användare i batchar för en stegvis migrering, innehåll som nyligen skyddas av användare är inte tillgänglig för användare som finns kvar på AD RMS. I det här scenariot när det är möjligt att tiden för migrering kort och migrera användare i logiska grupper så att om de samarbeta med varandra, de har migrerats tillsammans.

    Den här begränsningen gäller inte när du anger den betrodda Publiceringsdomänen till aktiv under importen, eftersom alla användare ska skydda innehåll med samma nyckel. Vi rekommenderar den här konfigurationen eftersom du kan migrera alla användare oberoende och i din egen takt.

-   Om du samarbetar med externa partners (t.ex, genom att använda betrodda användardomäner eller federation) måste de även migrera till Azure RMS antingen samtidigt som migreringen, eller så snart som möjligt efteråt. Att få åtkomst till innehåll som din organisation som tidigare skyddats med hjälp av AD RMS, måste de fatta klienten konfigurationsändringar som liknar dem som du gör och ingår i det här dokumentet.

    På grund av möjliga configuration variationer som partner kan ha ligger exakt instruktioner för denna omkonfigurering utanför omfånget för det här dokumentet. Hjälp att kontakta Microsofts kundtjänst (CSS).

## Så här migrerar AD RMS Azure RMS

|Steg för migrering|Mer information|
|----------------------|-------------------|
|**1. Hämta Azure RMS-hanteringsverktyg för Administration**|Instruktioner finns i [Step 1: Download the Azure Rights Management Administration Tool](../Topic/Migrating_from_AD_RMS_to_Azure_Rights_Management.md#BKMK_Step1Migration).|
|**2. Exportera konfigurationsdata från AD RMS och importera det till Azure RMS**|Du exporterar konfigurationsdata (nycklar, mallar, URL: er) från AD RMS till en XML-fil och sedan överföra filen till Azure RMS med importera AadrmTpd Windows PowerShell-cmdlet. Ytterligare åtgärder kan behövas, beroende på AD RMS nyckel konfigurationen:<br /><br />-   Programvara-skyddade nyckel till programvara-skyddade nyckel migrering: Centralt hanterade lösenordsbaserad nycklar i AD RMS kan hanteras av Microsoft Azure RMS innehavaren nyckeln. Detta är den enklaste migrering sökvägen och krävs ingen ytterligare åtgärd.<br />-   HSM-skyddade nyckel till HSM-skyddade nyckel migrering: Nycklar som lagras som en HSM för AD RMS till kunden hanteras Azure RMS innehavaren nyckeln (den "bring egna nyckeln" eller BYOK scenario). Detta kräver ytterligare steg för att överföra nyckeln från din lokala Thales HSM till Azure RMS HSM.<br />-   Programvara-skyddade nyckel till HSM-skyddade nyckel migrering: Centralt hanterade lösenordsbaserad nycklar i AD RMS till kunden hanteras Azure RMS innehavaren nyckeln (den "bring egna nyckeln" eller BYOK scenario). Detta kräver de flesta konfigurationen eftersom du måste först extrahera programvarunyckeln och importera det till en lokal HSM och gör sedan ytterligare steg för att överföra nyckeln från din lokala Thales HSM till Azure RMS HSM.<br /><br />Instruktioner finns i [Step 2. Export configuration data from AD RMS and import it to Azure RMS](../Topic/Migrating_from_AD_RMS_to_Azure_Rights_Management.md#BKMK_Step2Migration).|
|**3. Aktivera din RMS-klient**|Om möjligt bör göra efter importen och inte före.<br /><br />Mer information och instruktioner finns [Step 3. Activate your RMS tenant](../Topic/Migrating_from_AD_RMS_to_Azure_Rights_Management.md#BKMK_Step3Migration).|
|**4. Konfigurera importerade mallar**|När du importerar principmallar för rättigheter arkiverade deras status. Om du vill att användarna ska kunna se och använda dem, måste du ändra mallstatus som publiceras i Azure-hanteringsportalen.<br /><br />Instruktioner finns i [Step 4. Configure imported templates](../Topic/Migrating_from_AD_RMS_to_Azure_Rights_Management.md#BKMK_Step4Migration).|
|**5. Konfigurera klienter för att använda Azure RMS**|Befintliga Windows-datorer måste konfigureras för att använda tjänsten Azure RMS i stället för AD RMS. Det här steget gäller för datorer i din organisation och för datorer i partnerorganisationer om du har bidragit med dem när du kör AD RMS.<br /><br />Om du har distribuerat den [tillägg för mobila enheter](http://technet.microsoft.com/library/dn673574.aspx) för mobila enheter, till exempel iOS Telefoner och iPads, Android-Telefoner och surfplattor, Windows phone och Mac-datorer, måste du ta bort SRV-poster i DNS som omdirigeras dessa klienter att använda AD RMS.<br /><br />Instruktioner finns i [Step 5. Reconfigure clients to use Azure RMS](../Topic/Migrating_from_AD_RMS_to_Azure_Rights_Management.md#BKMK_Step5Migration).|
|**6. Konfigurera IRM-integrering med Exchange Online**|Det här steget krävs om du vill använda Exchange Online med Azure RMS.<br /><br />Instruktioner finns i [Step 6. Configure IRM integration for Exchange Online](#BKMK_Step6Migration).|
|**7. Distribuera RMS-koppling**|Det här steget är nödvändigt om du vill använda någon av följande lokala tjänster med Azure RMS:<br /><br />-   Exchange Server (till exempel regler och Outlook Web Access)<br />-   SharePoint-servern<br />-   Windows Server som kör filen klassificering infrastruktur<br /><br />Instruktioner finns i [Step 7. Deploy the RMS connector](#BKMK_Step7Migration).|
|**8. Inaktivera AD RMS**|När du har bekräftat som alla klienter använder Azure RMS och inte längre åtkomst till AD RMS-servrar, kan du ställa av AD RMS-distribution.<br /><br />Instruktioner finns i [Step 8. Decommission AD RMS](#BKMK_Step8Migration).|
|**9. Nytt nyckeln din nyckel för Azure RMS-klient**|Det här steget krävs om du inte har körs i kryptografiskt läge 2 innan migreringen, och valfritt men rekommenderas för alla migreringar till att skydda säkerheten för din nyckel för Azure RMS-klienten.<br /><br />Instruktioner finns i [Step 9. Re-key your Azure RMS tenant key](#BKMK_Step9Migration).|

### <a name="BKMK_Step1Migration"></a>Steg 1: Hämta verktyget Azure Rights Management
Gå till Microsoft Download Center och hämta den [administrationsverktyget för Azure Rights Management](http://go.microsoft.com/fwlink/?LinkId=257721), som innehåller modulen Azure RMS administration för Windows PowerShell.

### <a name="BKMK_Step2Migration"></a>Steg 2. Exportera konfigurationsdata från AD RMS och importera det till Azure RMS
Det här steget är en process i två steg:

1.  Exportera konfigurationsdata från AD RMS genom att exportera de publishing domänerna (betrodda publiceringsdomäner) till en .xml-fil. Den här processen är densamma för alla migreringar.

2.  Importera konfigurationsdata till Azure RMS. Det finns olika processer för det här steget, beroende på din aktuella konfiguration för AD RMS-distribution och topologin prioriterade för din nyckel för Azure RMS-klienten.

#### Exportera konfigurationsdata från AD RMS
Utför följande procedur på alla AD RMS-kluster för alla betrodda publishing domäner som har skyddat innehåll för din organisation. Du behöver inte köra detta på bara kluster.

> [!NOTE]
> Om du använder Windows Server 2003 Rights Management, i stället för dessa anvisningar följer du proceduren [Exportera Serverlicensgivarcertifikatet, betrodd användardomän, betrodda Publiceringsdomänen och RMS privat nyckel](http://technet.microsoft.com/library/jj835767%28v=ws.10%29.aspx) från den [migrering från Windows RMS till AD RMS i en annan infrastruktur](http://technet.microsoft.com/library/jj835767%28v=ws.10%29.aspx) artikeln.

###### Om du vill exportera konfigurationsdata betrodd (domän publiceringsinformation)

1.  Logga in AD RMS-klustret som en användare med AD RMS administrationsbehörighet.

2.  Från AD RMS-hanteringskonsolen (**Active Directory Rights Management Services**), expandera klusternamnet AD RMS, expandera **förtroendeprinciper**, och klicka sedan på **betrodda Publishing domäner**.

3.  Välj betrodd publiceringsdomän i resultatfönstret och klicka, i åtgärdsfönstret på **Exportera betrodd publiceringsdomän**.

4.  I den **Exportera betrodd publiceringsdomän** dialogrutan:

    -   Klicka på **Spara som** och spara sökväg och ett filnamn som du väljer. Se till att ange **.xml** som filnamnstillägget (detta inte läggs automatiskt).

    -   Ange och bekräfta ett starkt lösenord. Kom ihåg lösenordet, eftersom du behöver det senare, när du importerar konfigurationsdata till Azure RMS.

    -   Markera inte kryssrutan om du vill spara filen med betrodd domän i RMS version 1.0.

När du har exporterat betrodda publishing domäner, är du redo att starta proceduren för att importera data till Azure RMS.

#### Importera konfigurationsdata till Azure RMS
Exakt procedurerna i det här steget beror på din aktuella konfiguration för AD RMS-distribution och topologin prioriterade för din nyckel för Azure RMS-klienten.

Din aktuella AD RMS-distribution kommer att använda någon av följande konfigurationer för din server licensgivarens certifikatet (Serverlicensgivarcertifikat) nyckel:

-   Lösenordsskydd i AD RMS-databasen. Detta är standardinställningar.

-   HSM skydd genom att använda en Thales maskinvara HSM (security module).

-   HSM skydd genom att använda en maskinvarusäkerhetsmodul (HSM) från en leverantör än Thales.

-   Lösenordet som skyddas med hjälp av en extern kryptografiprovidern.

> [!NOTE]
> Mer information om hur du använder maskinvara säkerhetsmoduler med AD RMS finns [med AD RMS med maskinvara säkerhetsmoduler](http://technet.microsoft.com/library/jj651024.aspx).

Två Azure RMS innehavaren nyckel topologi alternativ är: Microsoft hanterar din klient-nyckel (**Microsoft hanterar**) eller om du hanterar din klient-nyckel (**kunden hanteras**). När du hanterar en egen Azure RMS-klient nyckel ibland refererar till "ta dina egna nyckeln" (BYOK) och kräver en maskinvarusäkerhetsmodul (HSM) från Thales. Mer information finns i [Choose your tenant key topology: Managed by Microsoft (the default) or managed by you (BYOK)](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_ChooseTenantKey) i avsnittet den [Planera och implementera din Azure Rights Management innehavaren nyckel](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md) artikeln.

> [!IMPORTANT]
> Exchange Online är inte kompatibelt med Azure RMS BYOK.  Om du vill använda BYOK efter migreringen och planerar att använda Exchange Online, se till att du förstår hur den här konfigurationen minskar IRM-funktioner för Exchange Online. Granska informationen på den [BYOK pricing and restrictions](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_Pricing) i avsnittet i  [Planera och implementera din Azure Rights Management innehavaren nyckel](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md) artikel som hjälper dig att välja den bästa Azure RMS klient nyckel topologi för migreringen.

Använd följande tabell för att identifiera vilken metod som ska användas för migreringen. Kombinationer som inte listas stöds inte.

|Aktuella AD RMS-distribution|Vald Azure RMS innehavaren nyckel topologi|Instruktioner för migrering|
|--------------------------------|----------------------------------------------|-------------------------------|
|Lösenordsskydd i AD RMS-databasen|Hanteras av Microsoft|Finns det **programvara-skyddade nyckel till programvara-skyddade nyckel migrering** proceduren efter den här tabellen.<br /><br />Detta är den enklaste migrering sökvägen och bara kräver att du överför konfigurationsdata till Azure RMS.|
|HSM skydd genom att använda en Thales nShield HSM hardware security module)|Hanteras av kunden (BYOK)|Finns det **HSM-skyddade nyckel till HSM-skyddade nyckel migrering** proceduren efter den här tabellen.<br /><br />Detta kräver BYOK verktygsuppsättningen och två uppsättning steg för att överföra nyckeln från din lokala HSM till Azure RMS HSM och därefter överföra konfigurationsdata till Azure RMS.|
|Lösenordsskydd i AD RMS-databasen|Hanteras av kunden (BYOK)|Finns det **programvara-skyddade nyckel till HSM-skyddade nyckel migrering** proceduren efter den här tabellen.<br /><br />Detta kräver BYOK verktygsuppsättningen och tre uppsättningar steg först extrahera din programvara och importera den till en lokal HSM sedan överföra nyckeln från din lokala HSM till Azure RMS HSM och slutligen överför konfigurationsdata till Azure RMS.|
|HSM skydd genom att använda en maskinvarusäkerhetsmodul (HSM) från en leverantör än Thales|Hanteras av kunden (BYOK)|Kontakta leverantören för du HSM anvisningar överföra nyckeln från den här HSM till en Thales nShield maskinvara säkerhet modulen (HSM). Följ sedan instruktionerna för den **HSM-skyddade nyckel till HSM-skyddade nyckel migrering** proceduren efter den här tabellen.|
|Lösenordsskyddad med hjälp av en extern kryptografiprovider|Hanteras av kunden (BYOK)|Kontakta leverantören för du kryptografiprovidern anvisningar överföra din nyckel till en Thales nShield maskinvara HSM (security module). Följ sedan instruktionerna för den **HSM-skyddade nyckel till HSM-skyddade nyckel migrering** proceduren efter den här tabellen.|
Kontrollera att du har åtkomst till XML-filer som du skapade tidigare när du har exporterat betrodda publishing domäner innan du startar procedurerna. Dessa kan till exempel sparas på ett USB-minne som du flyttar från AD RMS-servern till Internet-anslutna arbetsstationen.

> [!NOTE]
> Dock lagra dessa filer, använda säkerhetsmetoder för att skydda dem eftersom dessa data innehåller en privat nyckel.

##### Programvara-skyddade nyckel till programvara-skyddade nyckel migrering
Använd den här proceduren om du vill importera AD RMS-konfiguration till Azure RMS leda till din Azure RMS-klienten nyckel som hanteras av Microsoft.

###### Importera konfigurationsdata till Azure RMS

1.  På en Internet-anslutna arbetsstationen hämta och installera Windows PowerShell-modulen för Azure RMS (minst version 2.1.0.0) som innehåller den [Importera AadrmTpd](http://msdn.microsoft.com/library/azure/dn857523.aspx) cmdlet.

    > [!TIP]
    > Om du tidigare har hämtat och installerat modulen, kontrollera versionsnumret med: `(Get-Module aadrm -ListAvailable).Version`

    Instruktioner för installationen finns i [Installera Windows PowerShell för Azure Rights Management](../Topic/Installing_Windows_PowerShell_for_Azure_Rights_Management.md).

2.  Starta Windows PowerShell med den **Kör som administratör** alternativet och använda den [Anslut AadrmService](http://msdn.microsoft.com/library/azure/dn629415.aspx) cmdlet för att ansluta till tjänsten Azure RMS:

    ```
    Connect-AadrmService
    ```
    När du uppmanas ange din [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] klient administratörsautentiseringsuppgifter (vanligtvis använder du ett konto som är en global administratör för Azure Active Directory eller Office 365).

3.  Använd den [Importera AadrmTpd](http://msdn.microsoft.com/library/azure/dn857523.aspx) cmdlet för att ladda upp först exporteras publishing domän (.xml) betrodd. Om du har fler än en .xml-fil eftersom du har flera betrodda publishing domäner, väljer du den fil som innehåller det exporterade betrodd publiceringsdomän som du vill använda i Azure RMS för att skydda innehåll efter migreringen. Använder du följande kommando:

    ```
    Import-AadrmTpd -TpdFile <PathToTpdPackageFile> -ProtectionPassword -Active $True -Verbose
    ```
    Exempel: **Import-AadrmTpd -TpdFile E:\contosokey1.xml -ProtectionPassword -Active $true -Verbose**

    När du uppmanas ange lösenordet som du tidigare angett och bekräfta att du vill utföra den här åtgärden.

4.  Upprepa steg 3 för varje återstående .xml-fil som du skapade genom att exportera dina betrodda domäner publishing när kommandot har slutförts. Men för de här filerna **-Active** till **false** när du kör kommandot Importera. Exempel: **Import-AadrmTpd -TpdFile E:\contosokey2.xml -ProtectionPassword -Active $false -Verbose**

5.  Använd den [Koppla från AadrmService](http://msdn.microsoft.com/library/azure/dn629416.aspx) cmdlet för att koppla från Azure RMS-tjänsten:

    ```
    Disconnect-AadrmService
    ```

Nu är du redo att gå till [Step 3. Activate your RMS tenant](../Topic/Migrating_from_AD_RMS_to_Azure_Rights_Management.md#BKMK_Step3Migration).

##### HSM-skyddade nyckel till HSM-skyddade nyckel migrering
Det är ett tvådelat procedur för att importera HSM nyckel och AD RMS-konfiguration till Azure RMS leda till din Azure RMS-klienten nyckel som hanteras av dig (BYOK).

Först måste du paketera HSM nyckeln så att det är redo att överföra till Azure RMS och sedan importera den konfigurationsdata.

###### Del 1: Paketet HSM nyckeln så att det är redo att överföra till Azure RMS

1.  Följ stegen i den [Implementing bring your own key (BYOK)](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_ImplementBYOK) delen av den [Planera och implementera din Azure Rights Management innehavaren nyckel](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md), med hjälp av proceduren **Generera och överför din klient nyckeln – via Internet** med följande undantag:

    -   Inte följer stegen för **Generera nyckeln innehavaren**, eftersom du redan har motsvarande från AD RMS-distribution. Du måste identifiera den nyckel som används av AD RMS-server från Thales installationen och använder den här nyckeln under migreringen. Thales krypterade viktiga filer namnges vanligtvis **key_(keyAppName)_(keyIdentifier)** lokalt på servern.

    -   Inte följer stegen för **överföra din klient nyckel till Azure RMS**, som använder kommandot Lägg till AadrmKey.  I stället överförs förberedda HSM nyckeln när du överför din exporterade betrodd publiceringsdomän med hjälp av kommandot Import AadrmTpd.

2.  På den Internet-anslutna arbetsstationen i Windows PowerShell-session ansluta till tjänsten Azure RMS.

Nu när du har förberett din HSM nyckel för Azure RMS, är du redo att importera HSM nyckelfil och konfigurationsdata för AD RMS.

###### Del 2: Importera HSM nyckel och konfiguration data till Azure RMS

1.  Fortfarande på arbetsstationen med Internet-anslutning och Windows PowerShell-sessionen, överföra första exporterade betrodda publishing domän (.xml) filen. Om du har fler än en .xml-fil eftersom du har flera betrodda publishing domäner, väljer du den fil som innehåller det exporterade betrodd publiceringsdomän som motsvarar den HSM nyckeln som du vill använda i Azure RMS för att skydda innehåll efter migreringen. Använder du följande kommando:

    ```
    Import-AadrmTpd -TpdFile <PathToTpdPackageFile> -ProtectionPassword -HsmKeyFile <PathToBYOKPackage> -Active $True -Verbose
    ```
    Exempel: **Import -TpdFile E:\no_key_tpd_contosokey1.xml  -HsmKeyFile E:\KeyTransferPackage-contosokey.byok -ProtectionPassword -Active $true -Verbose**

    När du uppmanas ange lösenordet som du tidigare angett och bekräfta att du vill utföra den här åtgärden.

2.  Upprepa steg 1 för varje återstående .xml-fil som du skapade genom att exportera dina betrodda domäner publishing när kommandot har slutförts. Men för de här filerna **-Active** till **false** när du kör kommandot Importera.  Exempel: **Import -TpdFile E:\contosokey2.xml -HsmKeyFile E:\KeyTransferPackage-contosokey.byok -ProtectionPassword -Active $false -Verbose**

3.  Använd den [Koppla från AadrmService](http://msdn.microsoft.com/library/windowsazure/dn629416.aspx) cmdlet för att koppla från Azure RMS-tjänsten:

    ```
    Disconnect-AadrmService
    ```

Nu är du redo att gå till [Step 3. Activate your RMS tenant](../Topic/Migrating_from_AD_RMS_to_Azure_Rights_Management.md#BKMK_Step3Migration).

##### Programvara-skyddade nyckel till HSM-skyddade nyckel migrering
Det är en tre delar procedur för att importera AD RMS-konfiguration till Azure RMS leda till din Azure RMS-klienten nyckel som hanteras av dig (BYOK).

Du måste först extrahera din server licensgivarens certifikatet (Serverlicensgivarcertifikat) nyckel från konfigurationsdata och överför den till en lokal Thales HSM, och sedan paketet överföra dina HSM nyckel till Azure RMS och sedan importera konfigurationsdata.

###### Del 1: Extrahera din Serverlicensgivarcertifikat från konfigurationsdata och importera nyckeln till din lokala HSM

1.  Använd följande steg i den [Implementing bring your own key (BYOK)](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_ImplementBYOK) delen av den [Planera och implementera din Azure Rights Management innehavaren nyckel](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md) artikeln:

    -   **Generera och överför din klient nyckeln – via Internet**: **Förbered din Internet-anslutna arbetsstation**

    -   **Generera och överför din klient nyckeln – via Internet**: **Förbered din frånkopplade arbetsstation**

    Följ inte stegen för att generera nyckeln för klienten eftersom du redan har en motsvarighet i den exporterade konfigurationsfilen data (.xml). I stället ska du köra ett kommando för att extrahera den här nyckeln från filen och importera det till din lokala HSM.

2.  Kör följande kommando på den frånkopplade arbetsstationen:

    ```
    KeyTransferRemote.exe -ImportRmsCentrallyManagedKey -TpdFilePath <TPD> -ProtectionPassword -KeyIdentifier <KeyID> -ExchangeKeyPackage <BYOK-KEK-pka-Region> -NewSecurityWorldPackage <BYOK-SecurityWorld-pkg-Region>
    ```
    Till exempel för Nordamerika: **KeyTransferRemote.exe -ImportRmsCentrallyManagedKey -TpdFilePath E:\contosokey1.xml -ProtectionPassword -KeyIdentifier contosorms1key –- -ExchangeKeyPackage &lt;BYOK-KEK-pka-NA-1&gt; -NewSecurityWorldPackage &lt;BYOK-SecurityWorld-pkg-NA-1&gt;**

    Ytterligare information:

    -   Parametern ImportRmsCentrallyManagedKey anger att åtgärden är att importera Serverlicensgivarcertifikatet nyckeln.

    -   Om du inte anger lösenordet i kommandot, uppmanas du att ange den.

    -   Parametern KeyIdentifier är ett eget nyckelnamn som skapar nyckel filnamnet. Du måste använda endast små ASCII-tecken.

    -   Parametern ExchangeKeyPackage anger en region specifika nyckelutbyte nyckel (KEK) paket som har ett namn som börjar med BYOK-KEK - pkg-.

    -   Parametern NewSecurityWorldPackage anger en specifik region world säkerhetspaket som har ett namn som börjar med BYOK-SecurityWorld - pkg-.

    Det här kommandot resulterar i följande:

    -   En HSM nyckelfil: %NFAST_KMDATA%\local\key_mscapi_ &lt; KeyID &gt;

    -   RMS-konfiguration datafilen med Serverlicensgivarcertifikatet tas bort: %NFAST_KMDATA%\local\no_key_tpd_ &lt; KeyID &gt; .xml

3.  Upprepa steg 2 för återstoden av dessa filer om du har fler än en RMS-data konfigurationsfiler.

Nu när ditt Serverlicensgivarcertifikat har extraherats så att det är en HSM-baserade nyckel, är du redo att paketet och överför den till Azure RMS.

###### Del 2: Paketera och överföra dina HSM nyckel till Azure RMS

1.  Använd följande steg från den [Implementing bring your own key (BYOK)](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_ImplementBYOK) delen av den [Planera och implementera din Azure Rights Management innehavaren nyckel](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md):

    -   **Generera och överför din klient nyckeln – via Internet**: **Förbered din klient nyckel för överföring**

    -   **Generera och överför din klient nyckeln – via Internet**: **Överföra din klient nyckel till Azure RMS**

Nu när du har överfört din HSM nyckel till Azure RMS, är du redo att importera konfigurationsdata AD RMS, som innehåller endast en pekare till nyckeln nyligen överförda innehavaren.

###### Del 3: Importera konfigurationsdata till Azure RMS

1.  Fortfarande på arbetsstationen med Internet-anslutna och Windows PowerShell-sessionen, kopiera över konfigurationsfiler RMS med Serverlicensgivarcertifikatet bort (från arbetsstationen frånkopplade %NFAST_KMDATA%\local\no_key_tpd_ &lt; KeyID &gt; .xml)

2.  Överför den första filen. Om du har fler än en .xml-fil eftersom du har flera betrodda publishing domäner, väljer du den fil som innehåller det exporterade betrodd publiceringsdomän som motsvarar den HSM nyckeln som du vill använda i Azure RMS för att skydda innehåll efter migreringen. Använder du följande kommando:

    ```
    Import-AadrmTpd -TpdFile <PathToNoKeyTpdPackageFile> -ProtectionPassword -HsmKeyFile <PathToKeyTransferPackage> -Active $true -Verbose
    ```
    Exempel: **Import -TpdFile E:\no_key_tpd_contosorms1key.xml -ProtectionPassword -HsmKeyFile E:\KeyTransferPackage-contosorms1key.byok -Active $true -Verbose**

    När du uppmanas ange lösenordet som du tidigare angett och bekräfta att du vill utföra den här åtgärden.

3.  Upprepa steg 2 för varje återstående .xml-fil som du skapade genom att exportera dina betrodda domäner publishing när kommandot har slutförts. Men för de här filerna **-Active** till **false** när du kör kommandot Importera. Exempel: **Import -TpdFile E:\no_key_tpd_contosorms2key.xml -ProtectionPassword -HsmKeyFile E:\KeyTransferPackage-contosorms1key.byok -Active $false -Verbose**

4.  Använd den [Koppla från AadrmService](http://msdn.microsoft.com/library/windowsazure/dn629416.aspx) cmdlet för att koppla från Azure RMS-tjänsten:

    ```
    Disconnect-AadrmService
    ```

Nu är du redo att gå till [Step 3. Activate your RMS tenant](../Topic/Migrating_from_AD_RMS_to_Azure_Rights_Management.md#BKMK_Step3Migration).

### <a name="BKMK_Step3Migration"></a>Steg 3. Aktivera din RMS-klient
Instruktioner för det här steget fullständigt beskrivs i den [Aktivera Azure Rights Management](../Topic/Activating_Azure_Rights_Management.md) artikeln.

> [!TIP]
> Om du har en Office 365-prenumeration kan aktivera du Azure RMS från Office 365 Administrationscenter eller Azure-hanteringsportalen. Vi rekommenderar att du använder Azure-hanteringsportalen eftersom du använder hanteringsportalen för att utföra nästa steg.

**Vad händer om din Azure RMS-klient har redan aktiverats?** Om Azure RMS-tjänsten har redan aktiverats för din organisation, kanske användare har redan använt Azure RMS för att skydda innehåll med en automatiskt genererad klient-nyckel (och standardmallar) i stället för din befintliga nycklar (och mallar) från AD RMS. Detta är inte troligt att göras på datorer som är väl hanterade på intranätet, eftersom de konfigureras automatiskt för AD RMS-infrastruktur. Men det kan hända på arbetsgruppsdatorer och datorer som sällan ansluter till intranätet. Tyvärr är det också svårt att identifiera dessa datorer som är därför rekommenderar vi att du inte aktivera tjänsten innan du importerar konfigurationsdata från AD RMS.

Om din Azure RMS-klienten redan är aktiverad och du kan identifiera dessa datorer, se till att du kör skriptet CleanUpRMS_RUN_Elevated.cmd på dessa datorer enligt beskrivningen i steg 5. Kör skriptet tvingar dem att initiera om användarmiljö så att de kan hämta den uppdaterade klienten och importerade mallar.

### <a name="BKMK_Step4Migration"></a>Steg 4. Konfigurera importerade mallar
Eftersom de mallar som du importerade har ett standardtillstånd **arkiverade**, måste du ändra det här tillståndet att **publicerade** om du vill att användarna ska kunna använda dessa mallar med Azure RMS.

Dessutom mallarna i AD RMS används den **ANYONE** gruppen för den här gruppen automatiskt bort när du importerar mallar till Azure RMS, måste du manuellt lägga till motsvarande grupp eller användare och samma rättigheter att importerade mallar. Motsvarande gruppen för Azure RMS heter **AllStaff-&lt;tenant_GUID&gt;@&lt;tenant_name&gt;.onmicrosoft.com&gt;**. Till exempel den här gruppen kan se ut så följande för Contoso AB: **AllStaff-9c11c87a-ac8b-46a3-8d5c-f4d0b72ee29a@contoso.onmicrosoft.com**.

Du kan se din organisation har automatiskt skapade grupp om du kopierar en standard principmallar för i Azure-portalen och sedan identifiera den **användarnamn** på den **rättigheter** sidan. Men du kan inte använda Azure-portalen för att lägga till den här gruppen och i stället använda en av följande alternativ för Azure RMS PowerShell:

-   Använd den [Export AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727078.aspx) cmdlet för att exportera mallen till en. CSV-fil som du kan redigera om du vill lägga till gruppen "AllStaff" och åtkomsträttigheter till de befintliga grupper och rättigheter och sedan använda den [Importera AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727077.aspx) cmdlet för att importera den här ändringen tillbaka till Azure RMS.

-   Använd den [Ny AadrmRightsDefinition](https://msdn.microsoft.com/library/azure/dn727080.aspx) PowerShell-cmdlet för att definiera "AllStaff" grupp och rättigheter som rättigheter definition objekt och kör kommandot igen för att definiera de befintliga grupper och rättigheter för mallen. Sedan lägger till dessa rättigheter definition objekt till mallar med den [Lägg till AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727075.aspx) cmdlet.

> [!NOTE]
> Motsvarande gruppen "AllStaff" är inte exakt detsamma som ANYONE i AD RMS:  "AllStaff"-gruppen innehåller alla användare i din Azure-klient, gruppen Alla omfattar alla autentiserade användare som kan vara utanför organisationen.
> 
> På grund av den här skillnaden mellan de två grupperna, kan du behöva även lägga till externa användare förutom gruppen "AllStaff". Externa e-postadresser för grupper stöds inte.

Mallar som du importerar från AD RMS ser ut och fungerar som egna mallar som du kan skapa i Azure-hanteringsportalen. Om du vill ändra importerade mallar som ska publiceras så att användare kan visa dem och markera dem från program eller göra andra ändringar i mallarna [Konfigurera anpassade mallar för Azure Rights Management](../Topic/Configuring_Custom_Templates_for_Azure_Rights_Management.md).

> [!TIP]
> För en mer konsekvent upplevelse för användare under migreringen inte göra ändringar i importerade mallarna än två ändringarna. och inte publicera de två mallar som levereras med Azure RMS eller skapa nya mallar just nu. Vänta tills migreringen är klar och du har inaktiverat AD RMS-servrar i stället.

### <a name="BKMK_Step5Migration"></a>Steg 5. Konfigurera klienter för att använda Azure RMS
För Windows-klienter:

1.  [Hämta migrering skripten](http://go.microsoft.com/fwlink/?LinkId=524619):

    -   CleanUpRMS_RUN_Elevated.cmd

    -   Redirect_OnPrem.cmd

    Dessa skript Återställ konfigurationen på Windows-datorer så att de använder Azure RMS-tjänsten i stället för AD RMS.

2.  Följ anvisningarna i skriptet omdirigering (Redirect_OnPrem.cmd) för att ändra skriptet så att den pekar till din nya Azure RMS-klient.

3.  Kör dessa skript med förhöjd behörighet i användarens kontext på Windows-datorer.

För klienter för mobila enheter och Mac-datorer:

-   Ta bort DNS SRV-poster som du skapade när du har distribuerat den [AD RMS-tillägget för mobila enheter](http://technet.microsoft.com/library/dn673574.aspx).

#### Ändringar som gjorts av migreringsskript
Det här avsnittet dokumenteras de ändringar som gör migreringsskript. Du kan använda den här informationen endast för referens, eller för att felsöka eller om du vill göra dessa ändringar själv.

CleanUpRMS_RUN_Elevated.cmd:

-   Ta bort innehållet i mapparna %userprofile%\AppData\Local\Microsoft\DRM och %userprofile%\AppData\Local\Microsoft\MSIPC, inklusive eventuella undermappar och filer med långa filnamn.

-   Ta bort innehållet i följande registernycklar:

    -   HKEY_LOCAL_MACHINE\Software\Microsoft\Office\ (11.0|12.0|14.0) \Common\DRM

    -   HKEY_CURRENT_USER\Software\Microsoft\Office\ (11.0|12.0|14.0) \Common\DRM

    -   HKEY_LOCAL_MACHINE\Software\WoW6432Node\Microsoft\Office\ (11.0|12.0|14.0) \Common\DRM

    -   HKEY_CURRENT_USER\Software\WoW6432Node\Microsoft\Office\ (11.0|12.0|14.0) \Common\DRM

    -   HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\ServiceLocation

    -   HKEY_LOCAL_MACHINE\SOFTWARE\WoW6432Node\Microsoft\MSIPC\ServiceLocation

    -   HKEY_LOCAL_MACHINE\Software\Microsoft\MSDRM\ServiceLocation

-   Ta bort följande registervärden:

    -   HKEY_CURRENT_USER\Software\Microsoft\Office\15.0\Common\DRM\DefaultServerURL

    -   HKEY_CURRENT_USER\Software\Microsoft\Office\15.0\Common\DRM\DefaultServer

Redirect_OnPrem.cmd:

-   Skapa följande registervärden för varje URL anges som en parameter under var och en av följande platser:

    -   HKEY_CURRENT_USER\Software\Microsoft\Office\ (11.0|12.0|14.0) \Common\DRM\LicenseServerRedirection

    -   HKEY_CURRENT_USER\Software\WoW6432Node\Microsoft\Office\ (11.0|12.0|14.0) \Common\DRM\LicenseServerRedirection

    -   HKEY_LOCAL_MACHINE\Software\Microsoft\Office\ (11.0|12.0|14.0) \Common\DRM\LicenseServerRedirection

    -   HKEY_LOCAL_MACHINE\Software\WoW6432Node\Microsoft\Office\ (11.0|12.0|14.0) \Common\DRM\LicenseServerRedirection

    -   HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC\LicensingRedirection

    Varje post har värdet REG_SZ **https://OldRMSserverURL/_wmcs/licensing** med informationen i följande format: **https://&lt;YourTenantURL&gt;/_wmcs/licensing**.

    > [!NOTE]
    > *&lt; YourTenantURL &gt;* har följande format: **{GUID} .rms. [Region].aadrm.com**.
    > 
    > Exempel:  5c6bb73b 1038-4eec-863d-49bded473437.rms.na.aadrm.com
    > 
    > Du hittar det här värdet genom att identifiera den **RightsManagementServiceId** värde när du kör den [Get-AadrmConfiguration](http://msdn.microsoft.com/library/windowsazure/dn629410.aspx) för Azure RMS.

### <a name="BKMK_Step6Migration"></a>Steg 6. Konfigurera IRM-integration för Exchange Online
Om du har importerats tidigare din TDP från AD RMS till Exchange Online måste du ta bort den här TDP för att undvika motstridiga mallar och principer när du har migrerat till Azure RMS. Genom att använda den [Ta bort RMSTrustedPublishingDomain](https://technet.microsoft.com/en-us/library/jj200720%28v=exchg.150%29.aspx) cmdlet från Exchange Online.

Om du väljer en Azure RMS klient nyckel topologi **Microsoft hanteras**:

-   Finns det [Exchange Online: IRM-konfiguration](../Topic/Configuring_Applications_for_Azure_Rights_Management.md#BKMK_ExchangeOnline) i avsnittet den [Konfigurera program för Azure Rights Management](../Topic/Configuring_Applications_for_Azure_Rights_Management.md) artikeln. Det här avsnittet innehåller vanliga kommandon som ska köras som ansluter till Exchange Online-tjänsten, importerar nyckeln för innehavaren från Azure RMS och aktiverar IRM-funktioner för Exchange Online. När du har slutfört de här stegen har fullständig RMS-funktioner med Exchange Online.

Om du väljer en Azure RMS klient nyckel topologi **kund-hanterade (BYOK)**:

-   Du kommer har minskat RMS-funktioner med Exchange Online, enligt beskrivningen i den [BYOK pricing and restrictions](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_Pricing) avsnitt i den [Planera och implementera din Azure Rights Management innehavaren nyckel](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md) artikeln.

### <a name="BKMK_Step7Migration"></a>Steg 7. Distribuera RMS-koppling
Om du har använt funktionen Information Rights Management (IRM) i Exchange Server eller SharePoint-Server med AD RMS, måste du först inaktivera IRM på dessa servrar och ta bort AD RMS-konfiguration. Sedan kan du distribuera kopplingen Rights Management (RMS), som fungerar som ett kommunikationsgränssnitt (ett relay) mellan lokala servrar och Azure RMS.

Slutligen för det här steget måste om du har importerat flera betrodda publiceringsdomäner till Azure RMS som användes för att skydda e-postmeddelanden, du manuellt redigera registret på Exchange Server-datorer ska kunna omdirigera alla betrodda publiceringsdomäner URL: er till RMS-kopplingen.

> [!NOTE]
> Innan du börjar kontrollera vilka versioner av lokala servrar som stöder RMS-anslutningen i "lokala servrar som stöder Azure RMS" i den [Program som stöder Azure RMS](../Topic/Requirements_for_Azure_Rights_Management.md#BKMK_SupportedApplications) delen av den [Krav för Azure Rights Management](../Topic/Requirements_for_Azure_Rights_Management.md) artikeln.

##### Inaktivera IRM på Exchange-servrar och ta bort AD RMS-konfiguration

1.  Leta upp följande mapp på varje Exchange-servern och ta bort alla poster i mappen: \ProgramData\Microsoft\DRM\Server\S-1-5-18

2.  Använd någon av Exchange-servrar, Exchange [Set_IRMConfiguration](http://technet.microsoft.com/library/dd979792.aspx) cmdlet först inaktivera IRM-funktioner för meddelanden som skickas till interna mottagare:

    ```
    Set-IRMConfiguration -InternalLicensingEnabled $false
    ```

3.  Använd sedan cmdlet samma inaktivera IRM-funktionerna för meddelanden som skickas till externa mottagare:

    ```
    Set-IRMConfiguration -ExternalLicensingEnabled $false
    ```

4.  Därefter kan du använda samma cmdlet för att inaktivera IRM i Microsoft Office Outlook Web App och Microsoft Exchange ActiveSync:

    ```
    Set-IRMConfiguration -ClientAccessServerEnabled $false
    ```

5.  Slutligen, använder du samma cmdlet för att rensa alla cachelagrade certifikat:

    ```
    Set-IRMConfiguration -RefreshServerCertificates
    ```

6.  På varje Exchange-Server nu återställa IIS, till exempel genom att köra en kommandotolk som administratör och skriver **iisreset**.

##### Inaktivera IRM på SharePoint-servrar och ta bort AD RMS-konfiguration

1.  Kontrollera att det inte finns några dokument utcheckad från RMS-skyddad bibliotek. Om det finns vara de blir tillgänglig i slutet av den här proceduren.

2.  På SharePoint Central Administration-webbplats i den **Snabbstart** klickar du på **säkerhet**.

3.  På den **säkerhet** sidan den **informationsprincip** klickar du på **Konfigurera information rights management**.

4.  På den **Information Rights Management** sidan den **Information Rights Management** sektionen, Välj **inte använder IRM på den här servern**, klicka på **OK**.

5.  Ta bort innehållet i mappen \ProgramData\Microsoft\MSIPC\Server\ på alla SharePoint-Server-datorer,*&lt; SID för det konto som kör SharePoint Server &gt;*.

##### Installera och konfigurera RMS-anslutning

-   Följ instruktionerna i den [Distribuera Azure Rights Management-koppling](../Topic/Deploying_the_Azure_Rights_Management_Connector.md) artikeln.

##### För Exchange endast och flera betrodda publiceringsdomäner: Redigera registret

-   På varje Exchange-servern manuellt lägga till följande registernycklar för varje ytterligare betrodda Publiceringsdomänen importerade, omdirigerings-URL: er för betrodda Publiceringsdomänen RMS-anslutningen. Registerposterna är specifika för migrering och lägga till inte verktyget serverkonfiguration för Microsoft RMS-anslutningen.

    Använd följande anvisningar när du gör dessa ändringar i registret:

    -   Ersätt *ConnectorFQDN* med namnet som du har definierat i DNS för kopplingen. Till exempel **rmsconnector.contoso.com**.

    -   Använd HTTP eller HTTPS-prefix för koppling URL-Adressen, beroende på om du har konfigurerat anslutningen för att använda HTTP eller HTTPS för att kommunicera med dina lokala servrar.

    **För Exchange 2013:**

    |Sökväg till register|Typ|Värde|Data|
    |------------------------|-------|---------|--------|
    |HKLM\SOFTWARE\Microsoft\ExchangeServer\v15\IRM\LicenseServerRedirection|Reg_SZ|https://&lt;AD RMS intranät licensiering URL &gt;/_wmcs/licensing|En av följande, beroende på om du använder HTTP eller HTTPS från Exchange-servern RMS-anslutningen:<br /><br />-   http://&lt;connectorFQDN&gt;/_wmcs/Licensing<br />-   https://&lt;connectorName&gt;/_wmcs/Licensing|
    |HKLM\SOFTWARE\Microsoft\ExchangeServer\v15\IRM\LicenseServerRedirection|Reg_SZ|https://&lt;AD RMS-extranät licensiering URL &gt;/_wmcs/licensing|En av följande, beroende på om du använder HTTP eller HTTPS från Exchange-servern RMS-anslutningen:<br /><br />-   http://&lt;connectorFQDN&gt;/_wmcs/Licensing<br />-   https://&lt;connectorFQDN&gt;/_wmcs/Licensing|
    **För Exchange Server 2010:**

    |Sökväg till register|Typ|Värde|Data|
    |------------------------|-------|---------|--------|
    |HKLM\SOFTWARE\Microsoft\ExchangeServer\v14\IRM\LicenseServerRedirection|Reg_SZ|https://&lt;AD RMS intranät licensiering URL &gt;/_wmcs/licensing|En av följande, beroende på om du använder HTTP eller HTTPS från Exchange-servern RMS-anslutningen:<br /><br />-   http://&lt;connectorName&gt;/_wmcs/Licensing<br />-   https://&lt;connectorName&gt;/_wmcs/Licensing|
    |HKLM\SOFTWARE\Microsoft\ExchangeServer\v14\IRM\LicenseServerRedirection|Reg_SZ|https://&lt;AD RMS-extranät licensiering URL &gt;/_wmcs/licensing|En av följande, beroende på om du använder HTTP eller HTTPS från Exchange-servern RMS-anslutningen:<br /><br />-   http://&lt;connectorName&gt;/_wmcs/Licensing<br />-   https://&lt;connectorName&gt;/_wmcs/Licensing|

När du har slutfört de här procedurerna, bör du läsa den **Nästa steg** i avsnittet den [Distribuera Azure Rights Management-koppling](../Topic/Deploying_the_Azure_Rights_Management_Connector.md) artikeln.

### <a name="BKMK_Step8Migration"></a>Steg 8. Inaktivera AD RMS
Valfritt: Ta bort den tjänstanslutningspunkt (SCP) från Active Directory för att förhindra att datorer från identifiering av lokal Rights Management-infrastruktur. Det här är valfritt på grund av omdirigering som du konfigurerade i registret (till exempel genom att köra skriptet migrering). Ta bort tjänstanslutningspunkt med verktyget AD SCP registrera från den [Rights Management Services Administration Toolkit](http://www.microsoft.com/download/details.aspx?id=1479).

Övervaka AD RMS-servrar för aktivitet, till exempel genom att kontrollera den [begäranden i rapporten systemhälsan](https://technet.microsoft.com/library/ee221012%28v=ws.10%29.aspx),  [ServiceRequest tabell](http://technet.microsoft.com/library/dd772686%28v=ws.10%29.aspx) eller [granskning av användaråtkomst till skyddat innehåll](http://social.technet.microsoft.com/wiki/contents/articles/3440.ad-rms-frequently-asked-questions-faq.aspx). När du har bekräftat att RMS-klienter inte längre kommunicera med servrarna och att klienterna använder har Azure RMS, kan du ta bort AD RMS-serverrollen dessa server. Om du använder dedicerade servrar kanske du föredrar systemprinciper steg i första stängs av servrar för en viss tid för att se till att det inte finns några rapporterade problem som kan behöva starta om servrarna för att avbrott i tjänsten när du undersöka varför klienter som inte använder Azure RMS.

Efter inaktivering av AD RMS-servrar, kanske du vill ta chansen att granska dina mallar i Azure-hanteringsportalen och sammanställa dem så att användarna har färre att välja mellan, eller konfigurera om dem, även lägga till nya mallar. Detta är också dags att publicera standardmallar. Mer information finns i [Konfigurera anpassade mallar för Azure Rights Management](../Topic/Configuring_Custom_Templates_for_Azure_Rights_Management.md).

### <a name="BKMK_Step9Migration"></a>Steg 9. Nytt nyckeln din nyckel för Azure RMS-klient
Det här steget krävs när migreringen är klar om AD RMS-distribution med RMS Cryptographic läge 1, eftersom nya nycklar skapar en ny nyckel klient som använder RMS kryptografiskt läge 2. Använder Azure RMS med kryptografiskt läge 1 stöds endast under migreringen.

Det här är valfritt men rekommenderas när migreringen är klar även om du körde i RMS kryptografiskt läge 2, eftersom det hjälper till att skydda din Azure RMS innehavaren nyckeln från potentiella säkerhetsöverträdelser din AD RMS-nyckel. När du nyckel igen din nyckel för innehavaren av Azure RMS (även kallat "rullande nyckeln"), en ny nyckel har skapats och den ursprungliga nyckeln arkiveras. Men eftersom du flyttar från en nyckel till en annan inte sker omedelbart men över några veckor inte vänta förrän du misstänker brott till din ursprungliga nyckeln men nyckeln din nyckel för RMS-klienten igen så snart som migreringen är klar.

Till nytt nyckeln din nyckel för Azure RMS-klienten:

-   Om din nyckel för RMS-klienten hanteras av Microsoft: Kontakta Microsofts kundtjänst (CSS) och bekräftar att du är Innehavaradministratör RMS.

-   Om din nyckel för RMS-klienten hanteras av dig (BYOK): Upprepa proceduren för att generera och skapa en ny nyckel via Internet eller personliga BYOK.

Mer information om hur du hanterar din nyckel för RMS-klienten finns [Åtgärder för din Azure Rights Management-klient nyckel](../Topic/Operations_for_Your_Azure_Rights_Management_Tenant_Key.md).

## Se även
[Konfigurera Azure Rights Management](../Topic/Configuring_Azure_Rights_Management.md)

