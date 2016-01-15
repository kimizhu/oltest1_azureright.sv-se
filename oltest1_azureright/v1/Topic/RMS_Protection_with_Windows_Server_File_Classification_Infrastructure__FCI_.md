---
description: na
keywords: na
title: RMS Protection with Windows Server File Classification Infrastructure (FCI)
search: na
ms.date: na
ms.service: rights-management
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9aa693db-9727-4284-9f64-867681e114c9
---
# RMS-skydd med infrastrukturen i Windows Server-filen klassificering (FCI)
Använd den här artikeln anvisningar och ett skript för att använda Rights Management (RMS) klienten med verktyget RMS-skydd för att konfigurera Hanteraren för filserverresurser och filen klassificering infrastruktur (FCI).

Denna lösning kan du skydda automatiskt alla filer i en mapp på en filserver som kör Windows Server eller automatiskt skydda filer som uppfyller ett visst villkor. Till exempel filer som har klassificerats innehåller konfidentiell eller känslig information. Den här lösningen använder [Azure Rights Management](../Topic/Azure_Rights_Management.md) (Azure RMS) för att skydda filer, så du måste ha den här tekniken som används i din organisation.

> [!NOTE]
> Även om Azure RMS innehåller en [koppling](https://technet.microsoft.com/library/dn375964.aspx) som stöder fil klassificering infrastruktur, att lösningen stöder endast internt skydd – till exempel Office-filer.
> 
> Du måste använda Windows PowerShell för att stödja alla filtyper med filen klassificering infrastruktur **RMS-skydd** modul, som beskrivs i den här artikeln. RMS-skydd-cmdlets som RMS-delningsprogrammet, stöd för Allmänt skydd samt internt skydd, vilket innebär att alla filer kan skyddas. Mer information om dessa olika skyddsnivåer finns i [Skydd – intern och allmän](../Topic/Rights_Management_sharing_application_administrator_guide.md#BKMK_LevelsofProtection) i avsnittet i [Rights Management dela program administratörshandboken](../Topic/Rights_Management_sharing_application_administrator_guide.md).

Följ instruktionerna är för Windows Server 2012 R2 eller Windows Server 2012. Om du kör andra versioner av Windows som stöds, kan du behöva anpassa vissa av stegen för skillnader mellan din version av operativsystemet och de beskrivs i den här artikeln.

## Förutsättningar för skydd av Azure RMS med Windows Server FCI
Krav för dessa anvisningar:

-   På varje server där du kör resurshanterare med filen klassificering infrastruktur:

    -   Du har installerat hanteraren för filserverresurser som en rolltjänster för rollen Filtjänster.

    -   Du har identifierat en lokal mapp som innehåller filer som ska skyddas med Rights Management. Till exempel C:\FileShare.

    -   Du har installerat verktyget RMS-skydd, inklusive krav för verktyget (till exempel RMS-klienten) och Azure RMS (till exempel kontot service principal). Mer information finns i [RMS-skydd Cmdlets](https://msdn.microsoft.com/library/azure/mt433195.aspx).

    -   Om du vill ändra standardnivån från RMS-skydd (interna eller Allmänt) för specifika filändelser du har redigerat registret, enligt beskrivningen i den [filen API configuration](https://msdn.microsoft.com/library/dn197834%28v=vs.85%29.aspx) sidan.

    -   Du har en Internet-anslutning med inställningar som är konfigurerade datorn om det krävs för en proxyserver. Exempel: `netsh winhttp import proxy source=ie`

-   Du har konfigurerat ytterligare förutsättningar för din Azure Rights Management-distribution, enligt beskrivningen i [about_RMSProtection_AzureRMS](https://msdn.microsoft.com/library/mt433202.aspx). Mer specifikt har följande värden för att ansluta till Azure RMS med ett huvudnamn för tjänsten:

    -   BposTenantId

    -   AppPrincipalId

    -   Symmetriska nyckeln

-   Du har synkroniserat din lokala Active Directory-användarkonton med Azure Active Directory eller Office 365, inklusive deras e-postadress. Detta krävs för alla användare som behöver komma åt filer när de är skyddade med FCI och Azure RMS. Om du inte gör det här steget (till exempel i en testmiljö), kan användare blockeras från att komma åt de här filerna. Om du behöver mer information om den här kontokonfigurationen finns [Förbereder Azure Rights Management](../Topic/Preparing_for_Azure_Rights_Management.md).

-   Du har identifierat Rights Management mallen ska användas, som skyddar filerna. Kontrollera att du känner till ID för den här mallen med hjälp av den [Get-RMSTemplate](https://msdn.microsoft.com/library/azure/mt433197.aspx) cmdlet.

## Anvisningar för att konfigurera Hanteraren för filserverresurser FCI för Azure RMS-skydd
Följ instruktionerna för att skydda automatiskt alla filer i en mapp genom att använda ett Windows PowerShell-skript som en anpassad aktivitet. Gör de här procedurerna i följande ordning:

1.  Spara Windows PowerShell-skript

2.  Skapa en klassificeringsegenskap för för Rights Management (RMS)

3.  Skapa en klassificeringsregel (klassificera för RMS)

4.  Konfigurera schemat klassificering

5.  Skapa en anpassad filhanteringsaktivitet (skydda filer med RMS)

6.  Testa konfigurationen genom att manuellt köra regeln och aktivitet

Alla filer i den valda mappen klassificeras med den anpassade egenskapen av RMS i slutet av dessa anvisningar och filerna skyddas av Rights Management. Du kan sedan skapa eller använda en annan klassificeringsegenskap och en regel med en aktivitet för filer som skyddar filer för en mer komplex konfiguration som skyddar selektivt vissa filer och inte andra.

#### Spara Windows PowerShell-skript

1.  Expandera den [Windows PowerShell-skript för Azure RMS-skydd med hjälp av hanteraren för filserverresurser FCI](#BKMK_RMSProtection_Script) avsnitt i den här artikeln och kopiera innehållet. Klistra in innehållet i skriptet och filnamnet **RMS-Protect-FCI.ps1** på din dator.

2.  Granska skriptet och göra följande ändringar:

    -   Sök efter följande sträng och Ersätt den med din egen AppPrincipalId som du använder med den [Set RMSServerAuthentication](https://msdn.microsoft.com/library/mt433199.aspx) cmdlet för att ansluta till Azure RMS:

        ```
        <enter your AppPrincipalId here>
        ```
        Skriptet kan se ut så här:

        `[Parameter(Mandatory = $false)]`

        `[Parameter(Mandatory = $false)] [string]$AppPrincipalId = "b5e3f76a-b5c2-4c96-a594-a0807f65bba4",`

    -   Sök efter följande sträng och Ersätt den med din egen symmetriska nyckel som du använder med den [Set RMSServerAuthentication](https://msdn.microsoft.com/library/mt433199.aspx) cmdlet för att ansluta till Azure RMS:

        ```
        <enter your key here>
        ```
        Skriptet kan se ut så här:

        `[Parameter(Mandatory = $false)]`

        `[string]$SymmetricKey = "zIeMu8zNJ6U377CLtppkhkbl4gjodmYSXUVwAO5ycgA="`

    -   Sök efter följande sträng och Ersätt den med din egen BposTenantId (klient-ID) som du använder med den [Set RMSServerAuthentication](https://msdn.microsoft.com/library/mt433199.aspx) cmdlet för att ansluta till Azure RMS:

        ```
        <enter your BposTenantId here>
        ```
        Skriptet kan se ut så här:

        `[Parameter(Mandatory = $false)]`

        `[string]$BposTenantId = "23976bc6-dcd4-4173-9d96-dad1f48efd42",`

    -   Om servern kör Windows Server 2012, måste du kanske manuellt läsa in modulen RMSProtection i början av skriptet. Lägg till följande kommando (eller motsvarande om mappen "Program" finns på en annan enhet än enhet C::

        ```
        Import-Module "C:\Program Files\WindowsPowerShell\Modules\RMSProtection\RMSProtection.dll"
        ```

3.  Logga skriptet. Om du inte registrerar skriptet (säkrare), måste du konfigurera Windows PowerShell på servrar som kör den. Kör till exempel en Windows PowerShell-session med den **Kör som administratör** och anger: **Set-ExecutionPolicy Unrestricted**. Den här konfigurationen kan dock alla unsigned-skript som körs (mindre säkert).

    Mer information om signering Windows PowerShell-skript, se [about_Signing](https://technet.microsoft.com/library/hh847874.aspx) i dokumentationsbiblioteket till PowerShell.

4.  Spara filen lokalt på varje filserver som ska köras resurshanterare med filen klassificering infrastruktur. Spara filen i till exempel **C:\RMS-Protection**. Skydda den här filen med NTFS-behörigheter så att obehöriga användare inte kan ändra den.

Du är nu redo att börja konfigurera Hanteraren för filserverresurser.

#### Skapa en klassificeringsegenskap för för Rights Management (RMS)

-   I hanteraren för filserverresurser, hantering av klassificering, skapa en ny lokal egenskap:

    -   **Name**: Typ **RMS**

    -   **Beskrivning**:   Typ **Rights Management protection**

    -   **Egenskapstypen**: Välj **Ja/Nej**

    -   **Value**: Välj **Ja**

Vi kan nu skapa en klassificeringsregel som använder den här egenskapen.

#### Skapa en klassificeringsregel (klassificera för RMS)

-   Skapa en ny klassificeringsregel:

    -   På den **allmänna** fliken:

        -   **Name**: Typ **Classify for RMS**

        -   **Aktiverad**: Behåll standardvärdet, vilket är att den här kryssrutan är markerad.

        -   **Beskrivning**: Typ av **Classify all files in the &lt;folder name&gt; folder for Rights Management**.

            Ersätt *&lt; mappnamn &gt;* med dina valda mappnamn. Till exempel **klassificera alla filer i mappen C:\FileShare för Rights Management**

        -   **Scope**: Lägg till den valda mappen. Till exempel **C:\FileShare**.

            Välj inte kryssrutorna.

    -   På den **klassificering** fliken:

    -   **Klassificering metoden**: Välj **mappen klassificeraren**

    -   **Egenskapen** namn: Välj **RMS**

    -   Egenskapen **värdet**: Välj **Ja**

Även om du kan köra Klassificeringsregler manuellt för pågående åtgärder du den här regeln ska köras enligt ett schema, så att nya filer klassificeras med egenskapen RMS.

#### Konfigurera schemat klassificering

-   På den **automatiska klassificeringen** fliken:

    -   **Aktivera fast schema**: Markera den här kryssrutan.

    -   Konfigurera schemat för alla Klassificeringsregler körs, vilket innefattar våra ny regel om du vill klassificera filer med egenskapen RMS.

    -   **Tillåt kontinuerlig klassificering för nya filer**: Markera den här kryssrutan så att nya filer klassificeras.

    -   Valfritt: Se alla ändringar som du vill, till exempel konfigurering av alternativ för rapporter och meddelanden.

Du är redo att konfigurera en hanteringsaktivitet för att tillämpa RMS-skydd på filerna nu du har slutfört konfigurationen av klassificering.

#### Skapa en anpassad filhanteringsaktivitet (skydda filer med RMS)

-   I **filhanteringsåtgärder**, skapa en ny filhanteringsaktivitet:

    -   På den **allmänna** fliken:

        -   **Aktivitet**: Typ **Protect files with RMS**

        -   Behåll den **Aktivera** markerad.

        -   **Beskrivning**: Typ **Protect files in &lt;folder name&gt; with Rights Management and a template by using a Windows PowerShell script.**

            Ersätt *&lt; mappnamn &gt;* med dina valda mappnamn. Till exempel **Skydda filer i C:\FileShare med Rights Management och en mall med ett Windows PowerShell-skript**

        -   **Scope**: Välj den valda mappen. Till exempel **C:\FileShare**.

            Välj inte kryssrutorna.

    -   På den **åtgärd** fliken:

        -   **Type**: Välj **anpassade**

        -   **Körbara**: Ange följande:

            ```
            C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe
            ```
            Om Windows inte finns på enhet C: ändra sökvägen eller bläddra till den här filen.

        -   **Argumentet**: Ange följande, med egna värden för &lt; sökväg &gt; och &lt; mall-ID &gt;:

            ```
            -Noprofile -Command "<path>\RMS-Protect-FCI.ps1 -File '[Source File Path]' -TemplateID <template GUID> -OwnerMail [Source File Owner Email]"
            ```
            Till exempel om du kopierade skriptet till C:\RMS-Protection och mall-ID som du har identifierat kraven är e6ee2481-26b9-45e5-b34a-f744eacd53b0, anger du följande:

            `-Noprofile -Command "C:\RMS-Protection\RMS-Protect-FCI.ps1 -File '[Source File Path]' -TemplateID e6ee2481-26b9-45e5-b34a-f744eacd53b0 -OwnerMail [Source File Owner Email]"`

            I det här kommandot **[sökvägen till källfilen]** och **[källa filen ägare e-post]** är båda FCI specifika variabler, så Skriv dessa exakt som de visas i kommandot ovan. Den första som används av FCI för att ange den identifiera filen i mappen automatiskt och andra är för FCI att automatiskt hämta den identifiera filen namngivna ägare e-postadress. Det här kommandot upprepas för varje fil i mappen, som i vårt exempel är alla filer i mappen C:\FileShare dessutom med RMS som en egenskap för klassificering av filen.

            > [!NOTE]
            > Den **-OwnerMail [Source File Owner Email]** parameter och värde garanterar att den ursprungliga ägaren av filen beviljas Rights Management ägaren av filen när den är skyddad. Detta garanterar att den ursprungliga filägaren har alla Rights Management-behörighet till sina egna filer. När filerna har skapats av en domänanvändare hämtas automatiskt e-postadressen från Active Directory med hjälp av namnet på användarkontot i filens ägare egenskap. Detta gör filen servern måste vara i samma domän eller betrodd domän som användare.
            > 
            > När det är möjligt, tilldela de ursprungliga ägarna skyddade dokument, så att dessa användare fortsätter att ha fullständig kontroll över de filer som de har skapats. Men om du använder variabeln [källa filen ägare e-] som ovan och en fil inte har en domänanvändare som definierats som ägare (till exempel ett lokalt konto användes för att skapa filen, så att ägaren visar SYSTEM), skriptet misslyckas.
            > 
            > För filer som inte har en domänanvändare som ägare, kan du kopiera och spara filerna som en domänanvändare så att du blir ägare till bara dessa filer. Eller, om du har behörighet kan du manuellt ändra ägare.  Eller också kan du ange en specifik e-postadress (till exempel din egen eller en grupp adresser för IT-avdelningen) i stället för variabeln [källa filen ägare e-], vilket innebär att alla filer som du skyddar med det här skriptet ska använda e-postadressen för att definiera den nya ägaren.

    -   **Kör kommandot som**: Välj **lokalt System**

    -   På den **villkoret** fliken:

        -   **Egenskapen**: Välj **RMS**

        -   **Operator**: Välj **lika**

        -   **Value**: Välj **Ja**

    -   På den **schema** fliken:

        -   **Run at**: Konfigurera önskade schemat.

            Ha tillräckligt med tid för att skriptet ska slutföras. Även om den här lösningen skyddar alla filer i mappen, körs skriptet en gång för varje fil och varje gång. Även om detta tar längre tid än att skydda alla filer på samma gång, vilket verktyget RMS-skydd har stöd för, är den här konfigurationen för varje fil för FCI mer kraftfulla. Skyddade filer kan till exempel ha olika ägare (behåller den ursprungliga ägaren) när du använder variabeln [källa filen ägare e-] och åtgärden fil kommer att krävs om du senare ändrar konfigurationen för att skydda filer i stället för alla filer i en mapp selektivt.

        -   **Köras på nya filer**: Markera den här kryssrutan.

#### Testa konfigurationen genom att manuellt köra regeln och aktivitet

1.  Kör Klassificeringsregeln:

    1.  Klicka på **Klassificeringsregler** &gt; **Kör klassificering med alla regler nu**

    2.  Klicka på **Vänta klassificering att slutföra**, och klicka sedan på **OK**.

2.  Vänta tills den **Kör klassificering** dialogrutan för att stänga och sedan visa resultatet i rapporten visas automatiskt. Du bör se **1** för den **Egenskaper** fältet och antalet filer i mappen. Bekräfta genom att använda Utforskaren och kontrollera egenskaper för filer i den valda mappen. På den **klassificering** fliken bör du se **RMS** som ett egenskapsnamn och **Ja** för dess **värdet**.

3.  Kör filen hanteringsaktivitet:

    1.  Klicka på **filhanteringsåtgärder** &gt; **Skydda filer med RMS** &gt; **Kör filen Management uppgiften nu**

    2.  Klicka på **Vänta tills åtgärden har slutförts**, och klicka sedan på **OK**.

4.  Vänta tills den **Kör filen hanteringsaktivitet** dialogrutan för att stänga och sedan visa resultatet i rapporten visas automatiskt. Du bör se hur många filer som finns i den valda mappen i den **filer** fält. Kontrollera att filerna i den valda mappen är nu skyddade med RMS. Till exempel om den valda mappen är C:\FileShare, skriver du följande i en Windows PowerShell-session och kontrollera att inga filer har statusen **UnProtected**:

    ```
    foreach ($file in (Get-ChildItem -Path C:\FileShare -Force | where {!$_.PSIsContainer})) {Get-RMSFileStatus -f $file.PSPath}
    ```
    > [!TIP]
    > Vissa felsökningstips:
    > 
    > -   Om du ser **0** i rapporten, i stället för antalet filer i mappen detta anger att skriptet inte kördes. Kontrollera först själva skript som läses in i Windows PowerShell ISE kontrollera innehållet skriptet och kör den för att se om några fel visas. Skriptet försöker att ansluta och autentiseras av Azure RMS med några argument.
    > 
    >     -   Om skriptet rapporterar att den inte kunde ansluta till Azure RMS, kontrollerar du de värden som visas för primära konto, som du angav i skriptet.  Mer information om hur du skapar huvudnamn tjänstkontot finns andra krav i [about_RMSProtection_AzureRMS](https://msdn.microsoft.com/library/mt433202.aspx)
    >     -   Om skriptet rapporterar att den kan ansluta till Azure RMS och Azure-regionen är utanför Nordamerika, kontrollera att du har redigerat registret korrekt för den här konfigurationen. Ett bra test för detta är att köra Get-RMSTemplate direkt från Windows PowerShell på servern. Mer information om ändringar i registret finns tredje krav i [about_RMSProtection_AzureRMS](https://msdn.microsoft.com/library/mt433202.aspx).
    > -   Om skriptet ensamt körs i Windows PowerShell ISE utan fel, försöka köra på följande sätt från en PowerShell-session, ange ett filnamn för att skydda och utan parametern - OwnerEmail:
    > 
    >     ```
    >     powershell.exe -Noprofile -Command "<path>\RMS-Protect-FCI.ps1 -File <full path and name of a file>' -TemplateID <template GUID>"
    >     ```
    >     -   Om skriptet har körts i Windows PowerShell-sessionen, kontrollera posterna för **Executive** och **argumentet** i filen management uppgiftsåtgärd.  Om du har angett **- OwnerEmail [källa filen ägare e-post]**, tar du bort den här parametern.
    > 
    >         Om filen hanteringsaktivitet fungerar korrekt utan  **- OwnerEmail [källa filen ägare e-post]**, kontrollera att de oskyddade filerna har en domänanvändare som anges som ägare filen i stället **SYSTEM**.  Genom att använda den **säkerhet** för filens egenskaper och klicka sedan på **Avancerat**. Den **ägare** värde visas omedelbart efter filen **namn**. Kontrollera också att filservern är i samma domän eller en betrodd domän för att hämta användarens e-postadress från Active Directory Domain Services.
    > -   Om du ser rätt antal filer i rapporten men filerna inte är skyddade, försöker skydda filerna manuellt med hjälp av den [skydda RMSFile](https://msdn.microsoft.com/library/azure/mt433201.aspx) cmdlet för att se om några fel visas.

När du har bekräftat att dessa uppgifter köras, kan du stänga resurshanterare. Nya filer skyddas automatiskt och alla filer som skyddas igen när scheman kör. Nytt skydda filer garanterar att alla ändringar av mallen används för filerna.

### <a name="BKMK_RMSProtection_Script"></a>Windows PowerShell-skript för Azure RMS-skydd med hjälp av hanteraren för filserverresurser FCI
Det här avsnittet innehåller exempelskript för att kopiera och redigera, enligt beskrivningen i föregående avsnitt.

*&#42;&#42;Friskrivning&#42;&#42;: Det här exempelskriptet stöds inte under en Microsoft support standard program eller tjänst. Det här exempelskriptet tillhandahålls som är utan garanti av något slag.*

```
<# .SYNOPSIS Helper script to protect all file types with Azure RMS and FCI. .DESCRIPTION Protect files with Azure RMS and Windows Server FCI, using an RMS template ID. #> param( [Parameter(Mandatory = $false)] [ValidateScript({ If($_ -eq "") {$true} else { if (Test-Path -Path $_ -PathType Leaf) {$true} else {throw "Can't find file specified"} } })] [string]$File, [Parameter(Mandatory = $false)] [string]$TemplateID, [Parameter(Mandatory = $false)] [string]$OwnerMail, [Parameter(Mandatory = $false)] [string]$AppPrincipalId = "<enter your AppPrincipalId here>", [Parameter(Mandatory = $false)] [string]$SymmetricKey = "<enter your key here>", [Parameter(Mandatory = $false)] [string]$BposTenantId = "<enter your BposTenantId here>" ) # script information [String] $Script:Version = 'version 1.0' [String] $Script:Name = "RMS-Protect-FCI.ps1" #global working variables [switch] $Script:isScriptProcess = $False # Controls the script process. If false, the script gracefully stops running. #**Functions (general helper)*************************************** function Get-ScriptName(){ return $MyInvocation.ScriptName.Substring($MyInvocation.ScriptName.LastIndexOf('\') + 1, $MyInvocation.ScriptName.LastIndexOf('.') - $MyInvocation.ScriptName.LastIndexOf('\') - 1) } #**Functions (script specific)************************************** function Check-Module{ param ([String]$Module = $(Throw "Module name not specified")) [bool]$isResult = $False #try to load the module if (get-module -list -name $Module) { import-module $Module if (get-module -name $Module ) { $isResult = $True } else { $isResult = $False } } else { $isResult = $False } return $isResult } function Protect-File ($ffile, $ftemplateId, $fownermail) { [bool] $returnValue = $false try { If ($OwnerMail -eq $null -or $OwnerMail -eq "") { $protectReturn = Protect-RMSFile -File $ffile -TemplateID $ftemplateId $returnValue = $true Write-Host ( "Information: " + "Protected File: $ffile with Template: $ftemplateId") } else { $protectReturn = Protect-RMSFile -File $ffile -TemplateID $ftemplateId -OwnerEmail $fownermail $returnValue = $true Write-Host ( "Information: " + "Protected File: $ffile with Template: $ftemplateId, set Owner: $fownermail") } } catch { Write-Host ( "ERROR" + "During protection of file: $ffile with Template: $ftemplateId") } return $returnValue } function Set-RMSConnection ($fappId, $fkey, $fbposId) { [bool] $returnValue = $false try { Set-RMSServerAuthentication -AppPrincipalId $fappId -Key $fkey -BposTenantId $fbposId Write-Host ("Information: " + "Connected to Azure RMS Service with BposTenantId: $fbposId using AppPrincipalId: $fappId") $returnValue = $true } catch { Write-Host ("ERROR" + "During connection to Azure RMS Service with BposTenantId: $fbposId using AppPrincipalId: $fappId") } return $returnValue } #**Main Script (Script)********************************************* Write-Host ("-== " + $Script:Name + " " + $Version + " ==-") $Script:isScriptProcess = $True # Validate Azure RMS connection by checking the module and then connection if ($Script:isScriptProcess) { if (Check-Module -Module RMSProtection){ $Script:isScriptProcess = $True } else { Write-Host ("The RMSProtection module is not loaded") -foregroundcolor "yellow" -backgroundcolor "black" $Script:isScriptProcess = $False } } if ($Script:isScriptProcess) { #Write-Host ("Try to connect to Azure RMS with AppId: $AppPrincipalId and BPOSID: $BposTenantId" ) if (Set-RMSConnection $AppPrincipalId $SymmetricKey $BposTenantId) { Write-Host ("Connected to Azure RMS") } else { Write-Host ("Couldn't connect to Azure RMS") -foregroundcolor "yellow" -backgroundcolor "black" $Script:isScriptProcess = $False } } #  Start working loop if ($Script:isScriptProcess) { if ( !(($File -eq $null) -or ($File -eq "")) ) { if (!(Protect-File -ffile $File -ftemplateId $TemplateID -fownermail $OwnerMail)) { $Script:isScriptProcess = $False } } } # Closing if (!$Script:isScriptProcess) { Write-Host "ERROR occurred during script process" -foregroundcolor "red" -backgroundcolor "black"} write-host ("-== " + $Script:Name + " " + $Version + "  ==-") if (!$Script:isScriptProcess) { exit(-1) } else {exit(0)}
```

## Ändra anvisningarna för att skydda selektivt filer
När du har instruktionerna fungerar, är det sedan mycket enkelt att ändra dem för en mer avancerad konfiguration. Till exempel skydda filer genom att använda samma skript, men endast för filer som innehåller personligt identifierbar information och välja en mall som har mer restriktiva behörigheter kanske.

Genom att använda någon av egenskaperna inbyggda klassificering (till exempel **personligt identifierbar Information**) eller skapa egna ny egenskap. Skapa sedan en ny regel som använder den här egenskapen. Du kan till exempel välja den **innehåll klassificeraren**, välja den **personligt identifierbar Information** egenskapen med värdet **hög**, och konfigurera mönstret sträng eller ett uttryck som identifierar den fil som ska konfigureras för den här egenskapen (till exempel strängen "**Födelsedatum**").

Nu är allt du behöver skapa en ny filhanteringsaktivitet som använder samma skript men kanske med en annan mall och konfigurera villkoret för egenskapen klassificering som du just har konfigurerat. Till exempel i stället för villkoret som vi tidigare har konfigurerat (**RMS** egenskapen **lika**, **Ja**), Välj den **personligt identifierbar Information** egenskap med den **Operator** värdet **lika** och **värde** av **hög**.

