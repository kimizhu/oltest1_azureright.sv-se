---
description: na
keywords: na
title: Rights Management sharing application administrator guide
search: na
ms.date: na
ms.service: rights-management
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d9992e30-f3d1-48d5-aedc-4e721f7d7c25
---
# Rights Management dela program administrat&#246;rshandboken
Använd följande information om du är ansvarig för delningsapplikation i ett företagsnätverk Microsoft Rights Management, eller om du vill ha mer teknisk information än i den [Rights Management delning användaren guide till](../Topic/Rights_Management_sharing_application_user_guide.md) eller [vanliga frågor och svar för Microsoft Rights Management dela program för Windows](http://go.microsoft.com/fwlink/?LinkId=303971):

-   [Automatisk distribution för delningsapplikation för Microsoft Rights Management](../Topic/Rights_Management_sharing_application_administrator_guide.md#BKMK_ScriptedInstall)

    -   [Verifierar installationen lyckades](../Topic/Rights_Management_sharing_application_administrator_guide.md#BKMK_verifyscripted)

    -   [Avinstallera kommandon](../Topic/Rights_Management_sharing_application_administrator_guide.md#BKMK_uninstallscripted)

    -   [Utelämna automatiska uppdateringar](../Topic/Rights_Management_sharing_application_administrator_guide.md#BKMK_SuppressAutomaticUpdates)

    -   [Azure RMS: Konfigurera spårning av dokument](#BKMK_DocumentTracking)

    -   [Endast AD RMS: Stöd för flera domäner för e-post i din organisation](../Topic/Rights_Management_sharing_application_administrator_guide.md#BKMK_FederatedDomains)

-   [Teknisk översikt för delningsapplikation för Microsoft Rights Management](../Topic/Rights_Management_sharing_application_administrator_guide.md#BKMK_AdminOverview)

    -   [Skydd – intern och allmän](../Topic/Rights_Management_sharing_application_administrator_guide.md#BKMK_LevelsofProtection)

    -   [Filtyper och filnamnstillägg](../Topic/Rights_Management_sharing_application_administrator_guide.md#BKMK_SupportFileTypes)

    -   [Ändra skyddsnivån standard filer](../Topic/Rights_Management_sharing_application_administrator_guide.md#BKMK_ChangeDefaultProtection)

> [!TIP]
> Om du är ny appen RMS-delning eller letar du efter mer information, se [hur RMS skyddar alla filtyper – med hjälp av RMS-delningsappen](https://curah.microsoft.com/191031/how-rms-protects-all-file-types-by-using-the-rms-sharing-app).

RMS-delning program passar bäst att arbeta med Azure RMS eftersom den här distributionskonfiguration stöder skicka skyddade bilagor till användare i en annan organisation och alternativ, till exempel e-postaviseringar och dokument spårning med återkallade.  Men med vissa begränsningar fungerar med den lokala versionen, AD RMS. En omfattande jämförelse av funktioner som stöds av Azure RMS och AD RMS Se [jämföra Azure Rights Management och AD RMS](https://technet.microsoft.com/library/jj739831.aspx). Om du har AD RMS och vill flytta till Azure RMS Se [migrera från AD RMS till Azure Rights Management](https://technet.microsoft.com/library/dn858447.aspx).

## <a name="BKMK_ScriptedInstall"></a>Automatisk distribution för delningsapplikation för Microsoft Rights Management
Windows-versionen av RMS-delning programmet stöder skript installationen, vilket gör den lämplig för företagsdistributioner.

Endast förutsättningar för installationer är att datorerna som kör en minimal version av Windows 7 Service Pack 1 och att Microsoft Framework lägsta version 4.0 är installerat. Om du behöver installera Microsoft .NET Framework 4.0 kan du [Hämta för installation från Microsoft Download Center](http://www.microsoft.com/download/details.aspx?id=17718).

#### Hämta RMS-delning program för automatisk distribution

1.  Gå till den [delningsapplikation för Windows Microsoft Rights Management](http://www.microsoft.com/download/details.aspx?id=40857) i Microsoft Download Center och på **Hämta**.

2.  Markera och hämta filer som du behöver. Det finns två klienten installationspaket: en för Windows 64-bitars (Microsoft Rights Management dela program x64.zip) och en annan för Windows 32-bitars (Microsoft Rights Management med programmet x86.zip).

3.  Extrahera filer från komprimerade installationspaket, till exempel genom att dubbelklicka på dem. Kopiera extraherade filer till en nätverksplats som har åtkomst till klientdatorer.

Installationspaket för RMS-delning stöder distribution av olika och omfattar följande:

|Beskrivning|Scenario för distribution|
|---------------|-----------------------------|
|Microsoft Online-inloggningsassistent|Krävs för följande:<br /><br />-   Office 2010 och Azure RMS<br />-   Office 2013 och Azure RMS om du inte har installerat det [9 juni 2015, uppdatera för Office 2013](https://support.microsoft.com/kb/3054853) (KB3054853)|
|Snabbkorrigeringen för Office (KB 2596501)|Krävs för följande:<br /><br />-   Office 2010 och Azure RMS<br />-   RMS med Office 2010 och Active Directory|
|Snabbkorrigeringen att aktivera AD RMS-klienten 1.0 att arbeta med Azure RMS (KB 2843630)|Krävs för följande:<br /><br />-   Office 2010 och Azure RMS<br />-   RMS med Office 2010 och Active Directory|
|AD RMS-klienten och RMS-delning|Krävs för följande:<br /><br />-   Office 2016 eller Office 2013 och Azure RMS eller Active Directory RMS<br />-   Office 2010 och Azure RMS<br />-   RMS med Office 2010 och Active Directory<br />-   RMS-delning program och Office-tillägg endast|
|Office-tillägg för menyfliksområdet|Krävs för följande:<br /><br />-   Office 2016 eller Office 2013 och Azure RMS eller Active Directory RMS<br />-   Office 2010 och Azure RMS<br />-   RMS med Office 2010 och Active Directory<br />-   RMS-delning program och Office-tillägg endast|
|Verktyget Azure Active Directory Rights Management|Krävs för följande:<br /><br />-   Office 2010 och Azure RMS|
Använd följande procedurer för att identifiera de kommandon som krävs för att distribuera RMS-delning program för dessa scenarier för distribution:

-   **Office 2016 eller Office 2013 och Azure RMS eller Active Directory RMS**

    Dina användare använder Office 2016 eller Office 2013 och din organisation använder Azure RMS eller Active Directory RMS användare samarbeta med andra organisationer som använder Azure RMS eller Active Directory RMS.

-   **Office 2010 och Azure RMS**

    Användarna kör Office 2010 och din organisation använder Azure RMS användare samarbeta med andra organisationer som använder Azure RMS eller Active Directory RMS.

-   **RMS med Office 2010 och Active Directory**

    Användarna kör Office 2010 och din organisation använder AD RMS användare samarbeta med andra organisationer som använder Azure RMS.

-   **RMS-delning program och Office-tillägg endast**

    Dina användare kör Office 2016, Office 2013 eller Office 2010 och din organisation använder AD RMS användare behöver inte samarbeta med andra organisationer som använder Azure RMS. Installationen kan du installera bara delning program och Office-tillägg.

> [!NOTE]
> I så fall kan om organisationen kör AD RMS kan användarna kan ta emot skyddat innehåll från andra företag som använder Azure RMS, men användarna inte skicka skyddat innehåll till användare i en organisation som använder Azure RMS. Men om din organisation använder Azure RMS kan kan användarna skicka och ta emot skyddat innehåll från andra företag.

Om du vill slutföra installationen för varje procedur datorn måste startas om. Du kan starta en automatisk omstart med hjälp av kommandot /i.

#### Distribuera RMS-delning program för Office 2016 Office 2013 och Azure RMS eller Active Directory RMS

-   Kör följande kommando på varje dator som du vill installera RMS-delning program och relaterade komponenter, med förhöjd behörighet:

    ```
    setup.exe /s
    ```

Om du vill kontrollera, finns i [Verifierar installationen lyckades](../Topic/Rights_Management_sharing_application_administrator_guide.md#BKMK_verifyscripted) i det här avsnittet.

#### Distribuera RMS-delning program för Office 2010 och Azure RMS

1.  Du måste vara global administratör för Office 365- eller Azure Active Directory-klient så att du kan få organisationens URL för certifiering genom att köra verktyget förberedelse av Azure Active Directory Rights Management. Du måste köra verktyget bara en gång på en enda dator. URL: en för certifiering tjänsten används när du installerar RMS-delning program på varje dator:

    1.  Logga in på en dator med hjälp av ett lokalt administratörskonto.

    2.  På den datorn [Hämta och installera den Microsoft Online inloggningsassistent](http://www.microsoft.com/download/details.aspx?id=28177).

    3.  Kör följande kommando för att se visas på skärmen certifiering service URL-Adressen som du kan sedan kopiera och spara till nästa steg:

        -   För Windows 8.1 och Windows 8, 64-bitars:

            ```
            x64\aadrmprep.exe /findCertificationUrl /logfile "<log file path and name>"
            ```

        -   För Windows 8.1 och Windows 8, 32-bitars:

            ```
            X86\aadrmprep.exe /findCertificationUrl /logfile "<log file path and name>"
            ```

        -   För Windows 7, 64-bitars:

            ```
            x64\win7\aadrmprep.exe /findCertificationUrl /logfile "<log file path and name>"
            ```

        > [!NOTE]
        > Detta kommando kan du ombedd att ange autentiseringsuppgifter för Azure. Om datorn inte är ansluten till en domän uppmanas du att. Om datorn är ansluten till en domän kan verktyget att kunna använda cachelagrade autentiseringsuppgifter.

2.  Kör följande kommando på varje dator som du vill installera RMS-delning program, med förhöjd behörighet:

    ```
    setup.exe /s /configureO2010Admin /certificationUrl <certification_url>
    ```

3.  På varje dator som du vill installera RMS-delning program, måste användarna kör följande kommando (du behöver inte förhöjd). Det finns olika sätt att göra detta, inklusive frågar användare att köra kommandot (till exempel en länk i ett e-postmeddelande eller en länk i Hjälp skrivbord portal) eller lägga till den till sina inloggningsskript:

    ```
    bin\RMSSetup.exe /configureO2010Only
    ```

Om du vill kontrollera, finns i [Verifierar installationen lyckades](../Topic/Rights_Management_sharing_application_administrator_guide.md#BKMK_verifyscripted) i det här avsnittet.

#### Distribuera RMS-delning program för Office 2010 och Active Directory RMS

1.  Kör följande kommando på varje dator som du vill installera RMS-delning program, med förhöjd behörighet:

    ```
    setup.exe /s /configureO2010Admin
    ```

2.  På varje dator som du vill installera RMS-delning program, måste användarna kör följande kommando (du behöver inte förhöjd). Det finns olika sätt att göra detta, inklusive frågar användare att köra kommandot (till exempel en länk i ett e-postmeddelande eller en länk i Hjälp skrivbord portal) eller lägga till den till sina inloggningsskript:

    -   För Windows 10, Windows 8.1 och Windows 8, 64-bitars:

        ```
        x64\aadrmprep.exe /configureO2010
        ```

    -   För Windows 10, Windows 8.1 och Windows 8, 32-bitars:

        ```
        X86\aadrmprep.exe /configureO2010
        ```

    -   För Windows 7, 64-bitars:

        ```
        x64\win7\aadrmpep.exe /configureO2010
        ```

Om du vill kontrollera, finns i [Verifierar installationen lyckades](../Topic/Rights_Management_sharing_application_administrator_guide.md#BKMK_verifyscripted) i det här avsnittet.

#### Installera RMS-delning av program och Office-tillägg endast

1.  Installera AD RMS-klienten och RMS-delning med hjälp av följande kommando:

    -   64-bitars Windows:

        ```
        x64\setup_ipviewer.exe /norestart /quiet /msicl "MSIRESTARTMANAGERCONTROL=Disable" /log "<log file path and name>"
        ```

    -   32-bitars Windows:

        ```
        X86\setup_ipviewer.exe /norestart /quiet /msicl "MSIRESTARTMANAGERCONTROL=Disable" /log "<log file path and name>"
        ```

    Exempel: `\\server5\apps\rms\x64\setup_ipviewer.exe /norestart /quiet /msicl "MSIRESTARTMANAGERCONTROL=Disable" /log "C:\Log files\ipviewerinstall.log"`

2.  Installera tilläggsprogrammet Office med hjälp av följande kommandon:

    -   64-bitarsversionen av Office:

        ```
        msiexec.exe /norestart /quiet MSIRESTARTMANAGERCONTROL=Disable /i "x64\Setup64.msi" /L*v "<log file path and name>"
        ```

    -   För 32-bitarsversion av Office:

        ```
        msiexec.exe /norestart /quiet MSIRESTARTMANAGERCONTROL=Disable /i "x86\Setup.msi" /L*v "<log file path and name>"
        ```

    Exempel: `\\server5\apps\rms\msiexec.exe /norestart /quiet MSIRESTARTMANAGERCONTROL=Disable /i "x64\Setup64.msi" /L*v "C:\Log files\rmsofficeinstall.log"`

Om du vill kontrollera, finns i [Verifierar installationen lyckades](../Topic/Rights_Management_sharing_application_administrator_guide.md#BKMK_verifyscripted) i det här avsnittet.

### <a name="BKMK_verifyscripted"></a>Verifierar installationen lyckades
Du kan använda installationsloggfiler för att verifiera att installationen ska lyckas.

##### Att kontrollera installationen för RMS-delning program för Office 2016 Office 2013 och Azure RMS eller Active Directory RMS

-   Om du vill kontrollera av kommandot Setup.exe på varje dator, söka efter installationsloggen **RMInstaller.log** i den *%temp%\RMS_installer_ &lt; guid &gt;* mapp, och identifiera slutkod.

    En lyckad installation har slutkoden 0 och annat nummer anger en misslyckad installation.

    Exempel loggfilens namn: **C:\temp\RMS_Installer_9352fc91-1982-43bf-958a-2ef1fe9c2ed0\RMInstaller.log**

##### Att kontrollera installationen för RMS-delning program för Office 2010 och Azure RMS

1.  Om du vill kontrollera av kommandot Setup.exe på varje dator, söka efter installationsloggen **RMInstaller.log** i den *%temp%\RMS_installer_ &lt; guid &gt;* mapp, och identifiera slutkod.

    En lyckad installation har slutkoden 0 och annat nummer anger en misslyckad installation.

    Exempel loggfilens namn: **C:\temp\RMS_Installer_9352fc91-1982-43bf-958a-2ef1fe9c2ed0**

2.  Om du vill kontrollera för kommandot RMSSetup.exe, användaren ska ha följande filer som skapats i deras *%localappdata%\microsoft\drm* mapp:

    -   CERTIFIKAT-dator-2048.drm

    -   Machine.drm certifikat

    -   CLC &#42;.drm

    -   GIC &#42;.drm

    Exempel på en CLC &#42;.drm fil:

    **CLC-alice@isvtenant999.onmicrosoft.com-{1b9cfccf; k5b11; k4a10; kac15; k29b2b6980f4c} .drm**

##### Att kontrollera installationen för RMS-delning program för Office 2010 och Active Directory RMS

1.  Om du vill kontrollera av kommandot Setup.exe på varje dator, söka efter installationen i loggfilen i den *%temp%\RMS_installer_ &lt; guid &gt;* mapp, och identifiera slutkod.

    En lyckad installation har slutkoden 0 och annat nummer anger en misslyckad installation.

    Exempel loggfilens namn: **C:\temp\RMS_Installer_9352fc91-1982-43bf-958a-2ef1fe9c2ed0**

2.  Om du vill kontrollera av kommandot aadrmprep.exe på varje dator, söka efter följande text i installationsloggen: **aadrmprep.exe avslutades med status fungerande**

    > [!NOTE]
    > Ibland kan kan installationen köras två gånger. den första förekomsten misslyckas och andra har lyckats.

    Om du vill kontrollera registret ändringar som gör att det här verktyget manuellt berörs de:

    -   [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSDRM\Federation]

        "FederationHomeRealm"="urn: HostedRmsOnlineService:Certification"

    -   [HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\MSDRM\Federation]

        "FederationHomeRealm"="urn: HostedRmsOnlineService:Certification"

    -   [HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\MSDRM\ServiceLocation\Activation]

        @= "&lt; certifiering url &gt;"

    -   [HKEY_CURRENT_USER\SOFTWARE\Microsoft\Office\14.0\Common\DRM]

        Standardanvändare = "&lt; default_user &gt;"

##### Att kontrollera installationen för RMS-delning program och Office-tillägg endast

1.  Om du vill kontrollera av kommandot Setup_ipviewer.exe, söka efter följande text i installationsloggen: **Slutfört eller fel installationsstatusen: 0**

    Exempel rader från en lyckad installation:

    **MSI (s) (F0:B8) [14:19:57:854]: Produkt: Active Directory Rights Management Services Client 2.1 - installationen har slutförts.**

    **MSI (s) (F0:B8) [14:19:57:854]: Windows Installer installerat produkten. Produktnamn: Active Directory Rights Management Services Client 2.1. Produktversion: 1.0.1179.1. Produkten språk: 1033. Tillverkare: Microsoft Corporation. Slutfört eller fel installationsstatusen: 0.**

2.  Sök efter följande text i installationsloggen om du vill kontrollera i Office-tillägget, på varje dator: **Slutfört eller fel installationsstatusen: 0**

    Exempel rader från en lyckad installation:

    **MSI (s) (9C: 88) [18:49:04:007]: Produkt: Microsoft RMS Office-tilläggsprogram--Installationen har slutförts.**

    **MSI (s) (9C: 88) [18:49:04:007]: Windows Installer installerat produkten. Produktnamn: Microsoft RMS Office-tilläggsprogram. Produktversion: 1.0.7. Produkten språk: 1033. Tillverkare: Microsoft. Slutfört eller fel installationsstatusen: 0.**

### <a name="BKMK_uninstallscripted"></a>Avinstallera kommandon
Alla kommandona installation som krävs för dessa distributioner stöder inte ett kommando avinstallationen. Du kan avinstallera AD RMS-klienten och dela programmet och du kan avinstallera Office-tillägg. Använd följande kommandon för att avinstallera de här elementen.

##### Så här avinstallerar du AD RMS-klienten och RMS-delning

-   Använd följande kommandon:

    -   64-bitars Windows:

        ```
        x64\setup_ipviewer.exe /uninstall /quiet
        ```

    -   32-bitars Windows:

        ```
        x86\setup_ipviewer.exe /uninstall /quiet
        ```

##### Så här avinstallerar du Office-tillägg

-   Använd följande kommandon:

    -   64-bitarsversionen av Office:

        ```
        msiexec /x \x64\Setup[64].msi /quiet
        ```

    -   För 32-bitarsversion av Office:

        ```
        msiexec /x \x86\Setup.msi /quiet
        ```

### <a name="BKMK_SuppressAutomaticUpdates"></a>Utelämna automatiska uppdateringar
Som standard är användarna ett meddelande om det finns en senare version av programmet RMS-delning och uppmanas att hämta den. Du kan inaktivera meddelandet genom att redigera följande registret:

1.  Navigera till **HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC** och om den inte redan finns kan du skapa en ny nyckel med namnet **RmsSharingApp**.

2.  Välj **RmsSharingApp**, skapa ett nytt DWORD-värde för **AllowUpdatePrompt**, och värdet **0**.

Eftersom RMS-delning programmet inte stöds av WSUS, kan du använda följande metod för att testa alla nya versioner av RMS-delning programmet innan du distribuerar för alla användare:

1.  Kör ett skript för att förhindra automatiska uppdateringar på alla användarnas datorer. På datorer som administratörer använda för att testa kör nya versioner, inte det här skriptet.

2.  När en ny version är tillgänglig kan administratörer hämta och testa den.

3.  När testningen är klar och eventuella problem som lösts distribuera den senaste versionen av alla användare med hjälp av automatisk distribution anvisningarna i handboken.

### <a name="BKMK_DocumentTracking"></a>Azure RMS: Konfigurera spårning av dokument
Om du har en [prenumeration som stöder dokument spårning](https://technet.microsoft.com/en-us/dn858608), dokumentet spårning platsen är aktiverad som standard för alla användare i organisationen.  Spårning visas information, t.ex e-postadresser med personer som försökte komma åt skyddade dokument som användare när dessa personer försökte komma åt dem och deras plats. Om Visa den här informationen inte är tillåtet i din organisation på grund av sekretesskrav som finns, kan du inaktivera åtkomst till dokumentet spårning webbplats med hjälp av den  [Inaktivera AadrmDocumentTrackingFeature](http://go.microsoft.com/fwlink/?LinkId=623032) cmdlet. Du kan återaktivera åtkomst till webbplatsen när som helst genom att använda den [Aktivera AadrmDocumentTrackingFeature](http://go.microsoft.com/fwlink/?LinkId=623037), och du kan kontrollera om åtkomst är aktiverat eller inaktiverat genom att använda [Get-AadrmDocumentTrackingFeature](http://go.microsoft.com/fwlink/?LinkId=623037).

 Om du vill köra dessa cmdlet: ar du har version **2.3.0.0** av Azure RMS-modulen för Windows PowerShell.  Installation instruktioner finns i [installera Windows PowerShell för Azure Rights Management](https://technet.microsoft.com/library/jj585012.aspx).

> [!TIP]
> Om du tidigare har hämtats och installerats modulen Kontrollera versionsnumret genom att köra: `(Get-Module aadrm –ListAvailable).Version`

Följande webbadresser som används för att spåra dokument och får (till exempel lägga till dem i ditt betrodda webbplatser om du använder Internet Explorer med förbättrad säkerhet):

-   https://&#42;.azurerms.com

-   https://ecn.dev.virtualearth.net

    > [!NOTE]
    > denna URL är för Bing maps.

-   https://&#42;.microsoftonline.com

-   https://&#42;.microsoftonline-p.com

### <a name="BKMK_FederatedDomains"></a>Endast AD RMS: Stöd för flera domäner för e-post i din organisation
Om du använder AD RMS och användare i din organisation har flera domäner för e-post, måste kanske på grund av en fusion eller dataanskaffningsjobb, du göra följande registret redigera:

1.  Navigera till **HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC** och om den inte redan finns kan du skapa en ny nyckel med namnet **RmsSharingApp**.

2.  Välj **RmsSharingApp**, skapa ett nytt flera strängvärde med namnet **FederatedDomains**, och lägger sedan till domäner och alla underdomäner som används i din organisation. Jokertecken stöds inte.

    Exempel: Företag Coho Vineyard &amp; Winery har en standard e-domän **cohovineyardandwinery.com**, men på grund av fusion, de också använda e-domäner **cohowinery.com**, **eastcoast.cohowinery.com**, och **cohovineyard**. För den **FederatedDomains** datavärde administratören anger: **cohowinery.com; eastcoast.cohowinery.com; cohovineyard**

Om du inte kan göra detta register ändra kanske användare inte allt innehåll som har skyddats av andra användare i organisationen. Den här registret redigera behövs inte om du använder Azure RMS.

## <a name="BKMK_AdminOverview"></a>Teknisk översikt för delningsapplikation för Microsoft Rights Management
Delningsapplikation för Microsoft Rights Management är ett valfritt hämtningsbara program för Microsoft Windows och andra plattformar som innehåller följande:

-   Skydd av en fil eller massinfogning skydd av flera filer liksom alla i en angiven mapp.

-   Fullständigt stöd för skydd av någon typ av fil- och inbyggda visningsprogram för vanliga filtyper text och bild.

-   Allmän skydd för filer som inte stöder RMS skydd.

-   Fullständig samverkan med filer som skyddas med Office Information Rights Management (IRM).

-   Fullständig samverkan med PDF-filer som skyddas med SharePoint, FCI och stöds PDF-verktyg för att skapa.

Delningsapplikation för Microsoft Rights Management använder den nya [AD RMS-klienten 2.1 runtime](http://www.microsoft.com/download/details.aspx?id=38396). Genom att använda tillhandahåller funktionen i AD RMS 2.1, delningsapplikation för Microsoft Rights Management slutanvändare en enkel skydd och förbrukning.

Med oktober 2013-versionen av RMS du internt skydda dokument med Office 2010 och skicka dem till användare i ett annat företag som kan sedan använda dem med hjälp av Azure RMS. Dessutom med den här versionen kan om du använder AD RMS i kryptografiska läge 2, du använda RMS för personer och allt innehåll från personer i ett annat företag som använder Azure RMS. Mer information om kryptografiska läge 2, se [AD RMS kryptografiska lägen](http://technet.microsoft.com/library/hh867439%28v=ws.10%29.aspx).

### <a name="BKMK_LevelsofProtection"></a>Skydd – intern och allmän
Delningsapplikation för Microsoft Rights Management stöder skydd på två olika nivåer som beskrivs i följande tabell.

|Typ av skydd|Ursprunglig|Allmän|
|----------------|---------------|----------|
|Beskrivning|För text, bild, Microsoft Office (Word, Excel, PowerPoint) filer, PDF-filer och andra filtyper för program som har stöd för AD RMS, innehåller intern skydd ett starkt skydd nivå som innehåller både kryptering och efterlevnad av rättigheter (behörigheter).|För alla andra program och filtyper ger allmän protection ett skydd som innehåller både filen inkapsling med .pfile filtyp och autentisering för att verifiera om en användare har behörighet att öppna filen.|
|Skydd|Filer är helt krypterade och skydd tillämpas på följande sätt:<br /><br />-   Innan skyddat innehåll återges måste autentisering infalla för dem som tar emot filen via e-post eller få tillgång till den via behörigheterna eller dela.<br />-   Dessutom tillämpas användningsrättigheter och princip som innehållets ägare när filer är skyddade fullständigt när innehållet återges i IP-Viewer (för skyddade filer text och bild) eller associerade program (för alla andra filtyper som stöds).|Filskydd tillämpas på följande sätt:<br /><br />-   Innan skyddat innehåll återges inträffar autentiseringen lyckas för dem som har behörighet att öppna filen och angivna åtkomst till den. Om tillståndet inte det inte att öppna filen.<br />-   Användningsrättigheter och princip som innehållets ägare visas för att informera behöriga användare för principen användning.<br />-   Granskningsloggning av behöriga användare öppna och komma åt filer inträffar, men inga användningsrättigheter framtvingas av inte stöder program.|
|Standardvärdet för filtyper|Det här är standardnivån skydd av följande filtyper:<br /><br />-   Text och bildfiler<br />-   Microsoft Office (Word, Excel, PowerPoint) filer<br />-   Bärbar dokumentformat (PDF)<br /><br />Mer information finns i följande avsnitt [Filtyper och filnamnstillägg](../Topic/Rights_Management_sharing_application_administrator_guide.md#BKMK_SupportFileTypes).|Det här är standard skydd för alla andra filtyper (till exempel .vsdx, RTF och så vidare) som inte stöds via heltäckande skydd.|
Du kan ändra standard skyddsnivån som gäller RMS-delning programmet. Du kan ändra standardnivån för intern till allmän, från allmän till ursprunglig och även förhindra RMS-delning program från att tillämpa skydd. Mer information finns i [Ändra skyddsnivån standard filer](../Topic/Rights_Management_sharing_application_administrator_guide.md#BKMK_ChangeDefaultProtection) i det här avsnittet.

### <a name="BKMK_SupportFileTypes"></a>Filtyper och filnamnstillägg
I följande tabell anges filtyper som stöds av Microsoft Rights Management dela program. För dessa filtyper ändras ursprungliga filnamnstillägget när enhetligt skyddade används och de här filerna skrivskyddad.

Dessutom när RMS-delning program internt skyddar en Word, Excel eller PowerPoint-fil som användare skydda genom att dela, åtgärden skapas automatiskt en andra fil som är en kopia av ursprungligt med samma namn, men med en **.ppdf** filnamnstillägg ¹. Den här versionen av filen garanterar att mottagarna installerar RMS-delning alltid kan öppna filen som innehåller ursprunglig skydd tillämpas.

Filer som skyddas datorverifieringsprocessen ändras ursprungliga filnamnstillägget alltid till .pfile.

> [!WARNING]
> Om du har brandväggar, web proxyservrar eller programvara som granska och vidta åtgärder enligt filnamnstillägg kan behöva du konfigurera dessa att stödja dessa nya filnamnstillägg.

|Ursprungliga filnamnstillägg|RMS-skyddad filnamnstillägg|
|--------------------------------|-------------------------------|
|txt|.ptxt|
|XML|.pxml|
|.jpg|.pjpg|
|JPEG|.ppng|
|PDF|.ppdf|
|.PNG|.ppng|
|TIFF|.ptiff|
|BMP|.pbmp|
|GIF|.pgif|
|.giff|.pgiff|
|.jpe|.pjpe|
|.jfif|.pjfif|
|.jif|.pjif|
|.JT|.pjt|
¹ PDF-Rendering tillhandahålls av Foxit. Copyright © 2003-2014 Foxit Corporation.

I följande tabell visas filtyper som Microsoft Rights Management delning programmet stöder program i Microsoft Office 2016, Office 2013 och Office 2010. För de här filerna förblir filnamnstillägget detsamma när filen skyddas av RMS.

|Filtyper som stöds av Office|Filtyper som stöds av Office|
|--------------------------------|--------------------------------|
|doc<br /><br />.docm<br /><br />.docx<br /><br />dot<br /><br />.dotm<br /><br />.dotx<br /><br />.potm<br /><br />.potx<br /><br />.PPS<br /><br />.ppsm<br /><br />.ppsx<br /><br />ppt<br /><br />.pptm|.pptx<br /><br />.thmx<br /><br />xla<br /><br />.xlam<br /><br />.xls<br /><br />.xlsb<br /><br />.xlt<br /><br />.xlsm<br /><br />xlsx<br /><br />.xltm<br /><br />.xltx<br /><br />XPS|

### <a name="BKMK_ChangeDefaultProtection"></a>Ändra skyddsnivån standard filer
Du kan ändra hur RMS-delning programmet skyddar filer genom att redigera registret. Exempelvis kan du göra så att filer som stöder intern skydd datorverifieringsprocessen skyddas av RMS-delning program.

Orsaker till varför du kanske vill göra detta:

-   Att se till att alla användare kan öppna filen från sina mobila enheter.

-   För att säkerställa att alla användare kan öppna filen om de inte har ett program stöder som intern skydd.

-   Att anpassa säkerhetssystem som utför en åtgärd på filer med sina filnamnstillägg och kan konfigureras för att anpassa .pfile filnamnstillägg men kan inte konfigureras för att anpassa flera filnamnstillägg för intern skydd.

På samma sätt kan du göra så att RMS-delning program ska gälla ursprunglig protection för filer som skulle ha allmän skydd som används som standard. Det kan vara lämpligt om du har ett program som stöder RMS-APIs – till exempel, ett för branschspecifika program som skrivits av interna utvecklarna eller ett program som har köpt från oberoende programvaruleverantör (ISV).

Du kan också tvinga RMS-delning programmet att blockera skydd av filer (gäller inte för intern skydd eller allmänna skydd). Exempel: Det kan vara nödvändigt om du har en automatisk program eller en tjänst som måste kunna öppna en viss fil om du vill bearbeta innehållet. När du blockerar skydd för en filtyp kan inte användare använda RMS-delning programmet för att skydda en fil med filtypen. När de försöker visas ett meddelande om att administratören har förhindrat skydd och de måste avbryta sina åtgärd för att skydda filen.

Om du vill konfigurera RMS-delning program ska gälla alla filer som skulle ha ursprungliga skydd som används som standard allmän protection göra följande ändringar i registret:

1.  **HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\RMSSharingApp\FileProtection**: Skapa en ny nyckel med namnet **&#42;**.

    Den här inställningen anger filer med alla filnamnstillägg.

2.  I den nya nyckeln för **HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\RMSSharingApp\FileProtection\ &#42;**, skapa ett nytt strängvärde (REG_SZ) med namnet **kryptering** som har datavärdet för **Pfile**.

    Den här inställningen innebär att RMS-delning programmet tillämpar allmän skydd.

De två inställningarna medföra RMS-delning programmet tillämpar allmän skydd för alla filer som har ett filnamnstillägg. Om målet är krävs ingen ytterligare konfiguration. Du kan också definiera undantag för specifika filtyper, så att de fortfarande internt skyddade. Om du vill göra det måste du göra tre ytterligare registret redigeringar för varje filtyp:

1.  **HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\RMSSharingApp\FileProtection**: Lägg till en ny nyckel med namnet på filnamnstillägget (utan föregående period).

    Till exempel för filer som har en .docx filnamnstillägg, skapa en nyckel med namnet **DOCX**.

2.  I den nya fil typen nyckeln (till exempel **HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\RMSSharingApp\FileProtection\DOCX**), skapa ett nytt DWORD-värde med namnet **AllowPFILEEncryption** som har ett **0**.

3.  I den nya fil typen nyckeln (till exempel **HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\RMSSharingApp\FileProtection\DOCX**), skapa ett nytt strängvärde med namnet **kryptering** som har ett **Ursprunglig**.

Alla filer skyddas datorverifieringsprocessen utom filer som har ett .docx filnamnstillägg som internt skyddas av RMS-delning programmet på grund av de här inställningarna.

Upprepa stegen tre för andra filtyper som du vill definiera som undantag eftersom de har stöd för intern skydd och du inte vill att de ska datorverifieringsprocessen vara skyddat av RMS-delning programmet.

Du kan göra liknande registret redigeringar för andra scenarier genom att ändra värdet för den **kryptering** sträng som stöder följande värden:

-   **Pfile**: Allmän skydd

-   **Ursprunglig**: Ursprunglig skydd

-   **Off**: Blockera skydd

## Se även
[Rights Management delning användaren guide till](../Topic/Rights_Management_sharing_application_user_guide.md)

