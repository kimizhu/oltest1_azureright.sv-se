---
description: na
keywords: na
title: Configuring Applications for Azure Rights Management
search: na
ms.date: na
ms.service: rights-management
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ea09cbc5-b98b-444e-8b60-5bc3cb199c36
---
# Konfigurera program f&#246;r Azure Rights Management
> [!NOTE]
> Den här informationen är för IT-administratörer och konsulter som har distribuerat Azure Rights Management. Om du söker efter Användarhjälp och information om hur du använder Rights Management för ett visst program eller öppna en fil som är skyddad rättigheter använda Hjälp och vägledning som medföljer programmet.
> 
> Till exempel för Office-program, klicka på ikonen Hjälp och ange sökvillkor som **Rights Management** eller **IRM**. RMS-delning program för Windows, finns i [Rights Management delning användaren guide till](http://technet.microsoft.com/library/dn339006.aspx).

När du har distribuerat Azure Rights Management (Azure RMS) för din organisation, kan du använda följande information för att konfigurera program och tjänster för att stödja Azure RMS. Dessa omfattar Office-program, till exempel Word 2013 och Word 2010 och services som Exchange Online (transportregler, förhindra dataförlust, överensstämmer inte framåt och kryptering av meddelanden) och SharePoint Online (skyddade bibliotek). Information om hur dessa program och tjänster som stöder Rights Management finns [Hur program stöd för Azure Rights Management](../Topic/How_Applications_Support_Azure_Rights_Management.md).

> [!IMPORTANT]
> Information om versioner som stöds och andra krav finns [Krav för Azure Rights Management](../Topic/Requirements_for_Azure_Rights_Management.md).

-   [Office 365: Konfiguration för klienter och de onlinetjänster](../Topic/Configuring_Applications_for_Azure_Rights_Management.md#BKMK_O365)

    -   [Exchange Online: IRM-konfiguration](../Topic/Configuring_Applications_for_Azure_Rights_Management.md#BKMK_ExchangeOnline)

    -   [SharePoint Online och OneDrive för företag: IRM-konfiguration](#BKMK_SharePointOnline)

-   [Office 2016 och Office 2013: Konfiguration för klienter](#BKMK_Office2013Configuration)

-   [Office 2010: Konfiguration för klienter](../Topic/Configuring_Applications_for_Azure_Rights_Management.md#BKMK_Office2010Configuration)

-   [Rights Management delning: Installation och konfiguration för klienter](../Topic/Configuring_Applications_for_Azure_Rights_Management.md#BKMK_SharingApp)

    -   [RMS-delning program för Windows: Installation och konfiguration](../Topic/Configuring_Applications_for_Azure_Rights_Management.md#BKMK_SharingAppforWindows)

    -   [RMS-delning program för mobila plattformar: Installation](../Topic/Configuring_Applications_for_Azure_Rights_Management.md#BKMK_SharingAppMovileDevices)

-   [Andra program som stöder RMS APIs: Installation och konfiguration](../Topic/Configuring_Applications_for_Azure_Rights_Management.md#BKMK_RMSAPIs)

Om du vill konfigurera lokala servrar som Exchange Server och SharePoint Server, se [Distribuera Azure Rights Management-koppling](../Topic/Deploying_the_Azure_Rights_Management_Connector.md).

> [!TIP]
> Högsta nivå exempel och skärmbilder av program som har konfigurerats för att använda Azure RMS finns på [Azure RMS i åtgärd: Administratörer och användare ser](../Topic/What_is_Azure_Rights_Management_.md#BKMK_RMSpictures) avsnitt från den [Vad är Azure Rights Management?](../Topic/What_is_Azure_Rights_Management_.md) ämne.

## <a name="BKMK_O365"></a>Office 365: Konfiguration för klienter och de onlinetjänster
Eftersom Office 365 stöder internt Azure RMS, krävs ingen konfiguration av en klientdator som stöd för informationsrättighetshantering (IRM) för program som Word, Excel, PowerPoint, Outlook och Outlook Web App. Alla användare behöver är logga in på Office-programmen med sina [!INCLUDE[o365_1](../Token/o365_1_md.md)] autentiseringsuppgifter och de kan skydda filer och e-post och använda filer och e-postmeddelanden som har skyddats av andra.

Men rekommenderar vi att du komplettera dessa program med Rights Management delning, så att användarna får nytta av Office-tillägg. Mer information finns i [Rights Management delning: Installation och konfiguration för klienter](../Topic/Configuring_Applications_for_Azure_Rights_Management.md#BKMK_SharingApp) i det här avsnittet.

### <a name="BKMK_ExchangeOnline"></a>Exchange Online: IRM-konfiguration
Om du vill konfigurera Exchange Online för att stödja Azure RMS, måste du konfigurera tjänsten information rights management (IRM) för Exchange Online. Det gör du använder Windows PowerShell (behöver inte installera en separat modul), och kör [PowerShell-kommandon för Exchange Online](https://technet.microsoft.com/library/jj200677.aspx).

> [!NOTE]
> Du kan inte för närvarande Konfigurera Exchange Online för att stödja Azure RMS om du använder en kund hanteras innehavaren nyckel (BYOK) för Azure RMS i stället för standardkonfigurationen av en nyckel som hanteras av Microsoft-klient. Mer information finns i [BYOK pricing and restrictions](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_Pricing) under den [Planera och implementera din Azure Rights Management innehavaren nyckel](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md) ämne.
> 
> Om du försöker konfigurera Exchange Online när Azure RMS använder BYOK kommandot för att importera nyckeln (steg 5 i följande procedur) misslyckas med felmeddelande **[FailureCategory = Cmdlet FailedToGetTrustedPublishingDomainFromRmsOnlineException]**.

Följande steg får en typisk uppsättning kommandon som du vill köra om du vill aktivera Exchange Online att använda Azure RMS:

1.  Om det är första gången du använder Windows PowerShell för Exchange Online på din dator måste du konfigurera Windows PowerShell för att köra signerade skript. Starta Windows PowerShell-session med hjälp av den **Kör som administratör** alternativet och skriv sedan:

    ```
    Set-ExecutionPolicy RemoteSigned
    ```

2.  I Windows PowerShell-session inloggningen till Exchange Online genom att använda ett konto som har aktiverats för fjärråtkomst till gränssnittet. Alla konton som skapas i Exchange Online är aktiverad som standard för fjärråtkomst till Shell men det kan vara inaktiverat (och aktiverad) med hjälp av den   [Set-användare &lt; användaridentiteten &gt; - RemotePowerShellEnabled](https://technet.microsoft.com/library/jj984292%28v=exchg.160%29.aspx) kommandot.

    Om du vill logga in skriver du:

    ```
    $Cred = Get-Credential
    ```
    I den **Windows PowerShell autentiseringsuppgifter begäran** dialogrutan skriver, ange ditt Office 365-användarnamn och lösenord.

3.  Ansluta till Exchange Online-tjänsten genom att köra följande två kommandon:

    ```
    $Session = New-PSSession -ConfigurationName Microsoft.Exchange -ConnectionUri https://ps.outlook.com/powershell/ -Credential $Cred -Authentication Basic –AllowRedirection
    ```

    ```
    Import-PSSession $Session
    ```

4.  Ange platsen för nyckeln Azure RMS-klient, enligt din region:

    För Nordamerika (och statliga prenumerationer):

    ```
    Set-IRMConfiguration -RMSOnlineKeySharingLocation "https://sp-rms.na.aadrm.com/TenantManagement/ServicePartner.svc"
    ```
    Europa:

    ```
    Set-IRMConfiguration -RMSOnlineKeySharingLocation "https://sp-rms.eu.aadrm.com/TenantManagement/ServicePartner.svc"
    ```
    För Asien:

    ```
    Set-IRMConfiguration -RMSOnlineKeySharingLocation "https://sp-rms.ap.aadrm.com/TenantManagement/ServicePartner.svc"
    ```
    För South Nordamerika:

    ```
    Set-IRMConfiguration -RMSOnlineKeySharingLocation "https://sp-rms.sa.aadrm.com/TenantManagement/ServicePartner.svc"
    ```

5.  Importera konfigurationsdata från Azure RMS till Exchange Online, i form av den betrodda publicering domänen (betrodda Publiceringsdomänen). Detta omfattar Azure RMS-klient nyckel och Azure RMS-mallar:

    ```
    Import-RMSTrustedPublishingDomain -RMSOnline -name "RMS Online"
    ```
    I det här kommandot vi hade namnet på **RMS Online** för grundläggande namnet på den betrodda Publiceringsdomänen för Azure RMS i Exchange Online. När den betrodda Publiceringsdomänen har importerats heter **RMS Online - 1** i Exchange Online.

6.  Aktivera Azure RMS-funktioner så att IRM-funktioner är tillgängliga för Exchange Online:

    ```
    Set-IRMConfiguration -InternalLicensingEnabled $true
    ```
    När du kör det här kommandot aktiveras automatiskt Rights Management för Outlook-klienten, webbprogram Outlook och Exchange Active Sync.

7.  Alternativt kan du testa att den här konfigurationen har lyckats med hjälp av följande kommando:

    ```
    Test-IRMConfiguration -Sender <user email address>
    ```
    Exempel: **Test-IRMConfiguration -Sender  adams@contoso.com**

    Detta kommando kör ett antal kontroller som innehåller verifierar anslutningen till tjänsten, konfigurationen, hämtar URI: er, licenser och alla mallar. I Windows PowerShell-session visas resultaten av varje och i slutet om allt skickar de här kontrollerna: **ÖVERGRIPANDE RESULTAT: PASS**

8.  Koppla från remote PowerShell-session:

    ```
    Remove-PSSession $Session
    ```

Användare kan nu skydda sina e-postmeddelanden med hjälp av Azure RMS. Välj exempelvis i webbprogram Outlook **Ange behörigheter** utökade menyn (**...**), och välj sedan **Vidarebefordra inte** eller någon av de tillgängliga mallarna gälla information protection för att e-postmeddelandet och bifogade filer. Eftersom Outlook Web App cachelagrar Användargränssnittet för en dag, vänta på att den här tidsperioden ska vara inaktiv innan du försöker använda information protection till e-postmeddelanden och när du har kört kommandona konfiguration. Innan Användargränssnittet uppdateras för att återspegla den nya konfigurationen, visas inte alla alternativ från den **Ange behörigheter** menyn.

> [!IMPORTANT]
> Om du skapar nya [anpassade mallar](https://technet.microsoft.com/library/dn642472.aspx) för Azure RMS eller uppdatera mallar, varje gång du måste köra kommandot Exchange Online PowerShell (om nödvändigt kör steg 2 och 3 först) att synkronisera ändringarna till Exchange Online: `Import-RMSTrustedPublishingDomain -Name "RMS Online - 1" -RefreshTemplates –RMSOnline`

Som administratör Exchange du nu konfigurera funktioner som gäller information protection automatiskt, såsom [transport regler](https://technet.microsoft.com/library/dd302432.aspx), [data går förlorade förhindra (DLP) principer](https://technet.microsoft.com/library/jj150527%28v=exchg.150%29.aspx), och [skyddade röstmeddelanden](https://technet.microsoft.com/library/dn198211%28v=exchg.150%29.aspx) (Unified Messaging).

Detaljerade anvisningar om hur du konfigurerar Exchange Online om du vill aktivera IRM funktionen finns i dokumentationen i Exchange-biblioteket. Exempel:

-   [Ansluta till Exchange Online med remote PowerShell](https://technet.microsoft.com/library/jj984289%28v=exchg.160%29.aspx)

-   [Konfigurera IRM om du vill använda Azure Rights Management](https://technet.microsoft.com/library/dn151475%28v=exchg.150%29.aspx)

#### Kryptering av Office 365-meddelanden
Kör på samma sätt som beskrivs ovan, men om du inte vill mallar som ska visas före steg 6, kör följande kommando för att förhindra IRM mallar visas i Outlook Web App och Outlook-klienten: `Set-IRMConfiguration -ClientAccessServerEnabled $false`

Sedan du redo att konfigurera [transport regler](https://technet.microsoft.com/library/dd302432.aspx) automatiskt ändra message säkerhet när mottagare finns utanför organisationen och välj de **använda Office 365-meddelandekryptering** alternativet.

Mer information om kryptering av meddelanden, se [kryptering i Office 365](https://technet.microsoft.com/library/dn569286.aspx) i Exchange-biblioteket.

### <a name="BKMK_SharePointOnline"></a>SharePoint Online och OneDrive för företag: IRM-konfiguration
Om du vill konfigurera SharePoint Online- och OneDrive för företag att stödja Azure RMS, måste du först aktivera tjänsten information rights management (IRM) för SharePoint Online med hjälp av Administrationscenter för SharePoint. Sedan ägare kan IRM-skydda sina SharePoint-listor och dokumentbibliotek och användare kan skydda sina OneDrive för Business bibliotek IRM så att dokument som har sparat och dela med andra automatiskt skyddas av Azure RMS.

Om du vill aktivera tjänsten information rights management (IRM) för SharePoint Online finns i följande instruktioner från Office-webbplatsen:

-   [Ställ in Information Rights Management (IRM) i Administrationscenter för SharePoint](http://office.microsoft.com/office365-sharepoint-online-enterprise-help/set-up-information-rights-management-irm-insharepoint-online-HA102895193.aspx)

Den här konfigurationen görs av Office 365-administratör.

#### Konfigurera IRM för bibliotek och listor
När du har aktiverat tjänsten IRM för SharePoint kan ägare IRM-skydda sina SharePoint-dokumentbibliotek och listor. Instruktioner finns i följande från Office-webbplatsen:

-   [Använd Information Rights Management till en lista eller ett bibliotek](http://office.microsoft.com/sharepoint-help/apply-information-rights-management-to-a-list-or-library-HA102891460.aspx)

Den här konfigurationen görs av administratören för SharePoint-webbplats.

#### <a name="BKMK_OneDrive"></a>Konfigurera IRM för OneDrive för företag
När du har aktiverat tjänsten IRM för SharePoint Online konfigureras användarnas OneDrive för Business dokumentbiblioteket sedan för Rights Management skydd.  Konfigurera användare kan detta själva med hjälp av den **inställningar** ikonen i sina OneDrive. Även om administratörer inte kan konfigurera Rights Management för användarnas OneDrive för företag med hjälp av Administrationscenter för SharePoint, kan du göra detta med hjälp av Windows PowerShell.

> [!NOTE]
> Mer information om hur du konfigurerar OneDrive för företag finns i dokumentationen för Office[ställer in OneDrive för företag i Office 365](https://support.office.com/article/Set-up-OneDrive-for-Business-in-Office-365-3e21f8f0-e0a1-43be-aa3e-8c0236bf11bb).

##### Konfiguration för användare
Ge användare instruktionerna så att de kan konfigurera sina OneDrive för företag och IRM-skydda sina business-filer.

1.  I OneDrive, klickar du på den **inställningar** ikonen för att öppna menyn Inställningar och klicka sedan på **webbplats innehållet**.

2.  Låt pekaren på den **dokument** sida vid sida, välja punkter (**...**), och klicka sedan på **Inställningar.**

3.  På den **inställningar** sidan i den **behörigheter och hantering** Klicka **Information Rights Management**.

4.  På den **Information Rights Management inställningar** väljer **begränsa behörigheterna för det här biblioteket vid hämtning** kryssrutan, ange ditt val av namn och en beskrivning för behörigheterna och om klickar du på **Visa alternativ** konfigurera valfria konfigurationer och klicka sedan på **OK**.

    Mer information om konfigurationsalternativen finns instruktioner i [gälla Information Rights Management till listan eller biblioteket](https://support.office.com/article/Apply-Information-Rights-Management-to-a-list-or-library-3bdb5c4e-94fc-4741-b02f-4e7cc3c54aa1) från Office-dokumentationen.

Eftersom den här konfigurationen är beroende av användare i stället för en administratör för att skydda sina OneDrive för Business bibliotek IRM, informera användarna om fördelarna med att skydda filer och hur du gör detta. Till exempel förklara att när de har ett dokument från OneDrive för företag endast personer de godkänna kan komma åt den med alla begränsningar som de konfigurerar, även om filen byter namn och kopierade någon annanstans.

##### Konfiguration för administratörer
Men du inte kan konfigurera IRM för användarnas OneDrive för företag med hjälp av Administrationscenter för SharePoint, kan du göra detta med hjälp av Windows PowerShell. Följ dessa steg om du vill aktivera IRM för dessa bibliotek:

1.  Hämta och installera den [SharePoint Online Client Components SDK](http://www.microsoft.com/en-us/download/details.aspx?id=42038).

2.  Hämta och installera den [SharePoint Online Management Shell](http://www.microsoft.com/en-us/download/details.aspx?id=35588).

3.  Kopiera innehållet i följande skript och filnamnet mängd IRMOnOneDriveForBusiness.ps1 på datorn.

    *&#42;&#42;Friskrivning från&#42;&#42;*: Det här exempelskriptet stöds inte under en Microsoft support standard program eller tjänst. Det här exempelskriptet tillhandahålls som är utan garanti av något slag.

    ```
    # Requires Windows PowerShell version 3 <# Description: Configures IRM policy settings for OneDrive for Business and can also be used for SharePoint Online libraries and lists Script Installation Requirements: SharePoint Online Client Components SDK http://www.microsoft.com/en-us/download/details.aspx?id=42038 SharePoint Online Management Shell http://www.microsoft.com/en-us/download/details.aspx?id=35588 ====== #> # URL will be in the format https://<tenant-name>-admin.sharepoint.com $sharepointAdminCenterUrl = "https://contoso-admin.sharepoint.com" $tenantAdmin = "admin@contoso.com" $webUrls = @("https://contoso-my.sharepoint.com/personal/user1_contoso_com", "https://contoso-my.sharepoint.com/personal/user2_contoso_com", "https://contoso-my.sharepoint.com/personal/user3_contoso_com") <# As an alternative to specifying the URLs as an array, you can import them from a CSV file (no header, single value per row). Then, use: $webUrls = Get-Content -Path "File_path_and_name.csv" #> $listTitle = "Documents" function Load-SharePointOnlineClientComponentAssemblies { [cmdletbinding()] param() process { # assembly location: C:\Program Files\Common Files\microsoft shared\Web Server Extensions\16\ISAPI try { Write-Verbose "Loading Assembly: Microsoft.Office.Client.Policy, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c" [System.Reflection.Assembly]::Load("Microsoft.Office.Client.Policy, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null Write-Verbose "Loading Assembly: Microsoft.Office.Client.TranslationServices, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c" [System.Reflection.Assembly]::Load("Microsoft.Office.Client.TranslationServices, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c" [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.DocumentManagement, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c" [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.DocumentManagement, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Publishing, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c" [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Publishing, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Runtime, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c" [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Runtime, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Search.Applications, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c" [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Search.Applications, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Search, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c" [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Search, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Taxonomy, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c" [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Taxonomy, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.UserProfiles, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c" [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.UserProfiles, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null return $true } catch { if($_.Exception.Message -match "Could not load file or assembly") { Write-Error -Message "Unable to load the SharePoint Server 2013 Client Components.`nDownload Location: http://www.microsoft.com/en-us/download/details.aspx?id=42038" } else { Write-Error -Exception $_.Exception } return $false } } } function Load-SharePointOnlineModule { [cmdletbinding()] param() process { do { # Installation location: C:\Program Files\SharePoint Online Management Shell\Microsoft.Online.SharePoint.PowerShell $spoModule = Get-Module -Name Microsoft.Online.SharePoint.PowerShell -ErrorAction SilentlyContinue if(-not $spoModule) { try { Import-Module Microsoft.Online.SharePoint.PowerShell -DisableNameChecking return $true } catch { if($_.Exception.Message -match "Could not load file or assembly") { Write-Error -Message "Unable to load the SharePoint Online Management Shell.`nDownload Location: http://www.microsoft.com/en-us/download/details.aspx?id=35588" } else { Write-Error -Exception $_.Exception } return $false } } else { return $true } } while(-not $spoModule) } } function Set-IrmConfiguration { [cmdletbinding()] param( [parameter(Mandatory=$true)][Microsoft.SharePoint.Client.List]$List, [parameter(Mandatory=$true)][string]$PolicyTitle, [parameter(Mandatory=$true)][string]$PolicyDescription, [parameter(Mandatory=$false)][switch]$IrmReject, [parameter(Mandatory=$false)][DateTime]$ProtectionExpirationDate, [parameter(Mandatory=$false)][switch]$DisableDocumentBrowserView, [parameter(Mandatory=$false)][switch]$AllowPrint, [parameter(Mandatory=$false)][switch]$AllowScript, [parameter(Mandatory=$false)][switch]$AllowWriteCopy, [parameter(Mandatory=$false)][int]$DocumentAccessExpireDays, [parameter(Mandatory=$false)][int]$LicenseCacheExpireDays, [parameter(Mandatory=$false)][string]$GroupName ) process { Write-Verbose "Applying IRM Configuration on '$($List.Title)'" # reset the value to the default settings $list.InformationRightsManagementSettings.Reset() $list.IrmEnabled = $true # IRM Policy title and description $list.InformationRightsManagementSettings.PolicyTitle       = $PolicyTitle $list.InformationRightsManagementSettings.PolicyDescription = $PolicyDescription # Set additional IRM library settings # Do not allow users to upload documents that do not support IRM $list.IrmReject = $IrmReject.IsPresent $parsedDate = Get-Date if([DateTime]::TryParse($ProtectionExpirationDate, [ref]$parsedDate)) { # Stop restricting access to the library at <date> $list.IrmExpire = $true $list.InformationRightsManagementSettings.DocumentLibraryProtectionExpireDate = $ProtectionExpirationDate } # Prevent opening documents in the browser for this Document Library $list.InformationRightsManagementSettings.DisableDocumentBrowserView = $DisableDocumentBrowserView.IsPresent # Configure document access rights # Allow viewers to print $list.InformationRightsManagementSettings.AllowPrint = $AllowPrint.IsPresent # Allow viewers to run script and screen reader to function on downloaded documents $list.InformationRightsManagementSettings.AllowScript = $AllowScript.IsPresent # Allow viewers to write on a copy of the downloaded document $list.InformationRightsManagementSettings.AllowWriteCopy = $AllowWriteCopy.IsPresent if($DocumentAccessExpireDays) { # After download, document access rights will expire after these number of days (1-365) $list.InformationRightsManagementSettings.EnableDocumentAccessExpire = $true $list.InformationRightsManagementSettings.DocumentAccessExpireDays   = $DocumentAccessExpireDays } # Set group protection and credentials interval if($LicenseCacheExpireDays) { # Users must verify their credentials using this interval (days) $list.InformationRightsManagementSettings.EnableLicenseCacheExpire = $true $list.InformationRightsManagementSettings.LicenseCacheExpireDays   = $LicenseCacheExpireDays } if($GroupName) { # Allow group protection. Default group: $list.InformationRightsManagementSettings.EnableGroupProtection = $true $list.InformationRightsManagementSettings.GroupName             = $GroupName } } end { if($list) { Write-Verbose "Committing IRM configuration settings on '$($list.Title)'" $list.InformationRightsManagementSettings.Update() $list.Update() $script:clientContext.Load($list) $script:clientContext.ExecuteQuery() } } } function Get-CredentialFromCredentialCache { [cmdletbinding()] param([string]$CredentialName) #if( Test-Path variable:\global:CredentialCache ) if( Get-Variable O365TenantAdminCredentialCache -Scope Global -ErrorAction SilentlyContinue ) { if($global:O365TenantAdminCredentialCache.ContainsKey($CredentialName)) { Write-Verbose "Credential Cache Hit: $CredentialName" return $global:O365TenantAdminCredentialCache[$CredentialName] } } Write-Verbose "Credential Cache Miss: $CredentialName" return $null } function Add-CredentialToCredentialCache { [cmdletbinding()] param([System.Management.Automation.PSCredential]$Credential) if(-not (Get-Variable CredentialCache -Scope Global -ErrorAction SilentlyContinue)) { Write-Verbose "Initializing the Credential Cache" $global:O365TenantAdminCredentialCache = @{} } Write-Verbose "Adding Credential to the Credential Cache" $global:O365TenantAdminCredentialCache[$Credential.UserName] = $Credential } # load the required assemblies and Windows PowerShell modules if(-not ((Load-SharePointOnlineClientComponentAssemblies) -and (Load-SharePointOnlineModule)) ) { return } # Add the credentials to the client context and SharePoint Online service connection # check for cached credentials to use $o365TenantAdminCredential = Get-CredentialFromCredentialCache -CredentialName $tenantAdmin if(-not $o365TenantAdminCredential) { # when credentials are not cached, prompt for the tenant admin credentials $o365TenantAdminCredential = Get-Credential -UserName $tenantAdmin -Message "Enter the password for the Office 365 admin" if(-not $o365TenantAdminCredential -or -not $o365TenantAdminCredential.UserName -or $o365TenantAdminCredential.Password.Length -eq 0 ) { Write-Error -Message "Could not validate the supplied tenant admin credentials" return } # add the credentials to the cache Add-CredentialToCredentialCache -Credential $o365TenantAdminCredential } # connect to Office365 first, required for SharePoint Online cmdlets to run Connect-SPOService -Url $sharepointAdminCenterUrl -Credential $o365TenantAdminCredential # enumerate each of the specified site URLs foreach($webUrl in $webUrls) { $grantedSiteCollectionAdmin = $false try { # establish the client context and set the credentials to connect to the site $script:clientContext = New-Object Microsoft.SharePoint.Client.ClientContext($webUrl) $script:clientContext.Credentials = New-Object Microsoft.SharePoint.Client.SharePointOnlineCredentials($o365TenantAdminCredential.UserName, $o365TenantAdminCredential.Password) # initialize the site and web context $script:clientContext.Load($script:clientContext.Site) $script:clientContext.Load($script:clientContext.Web) $script:clientContext.ExecuteQuery() # load and ensure the tenant admin user account if present on the target SharePoint site $tenantAdminUser = $script:clientContext.Web.EnsureUser($o365TenantAdminCredential.UserName) $script:clientContext.Load($tenantAdminUser) $script:clientContext.ExecuteQuery() # check if the tenant admin is a site admin if( -not $tenantAdminUser.IsSiteAdmin ) { try { # grant the tenant admin temporary admin rights to the site collection Set-SPOUser -Site $script:clientContext.Site.Url -LoginName $o365TenantAdminCredential.UserName -IsSiteCollectionAdmin $true | Out-Null $grantedSiteCollectionAdmin = $true } catch { Write-Error $_.Exception return } } try { # load the list orlibrary using CSOM $list = $null $list = $script:clientContext.Web.Lists.GetByTitle($listTitle) $script:clientContext.Load($list) $script:clientContext.ExecuteQuery() # **************  ADMIN INSTRUCTIONS  ************** # If necessary, modify the following Set-IrmConfiguration parameters to match your required values # The supplied options and values are for example only # Example that shows the Set-IrmConfiguration command with all parameters: Set-IrmConfiguration -List $list -PolicyTitle "Protected Files" -PolicyDescription "This policy restricts access to authorized users" -IrmReject -ProtectionExpirationDate $(Get-Date).AddDays(180) -DisableDocumentBrowserView -AllowPrint -AllowScript -AllowWriteCopy -LicenseCacheExpireDays 25 -DocumentAccessExpireDays 90 Set-IrmConfiguration -List $list -PolicyTitle "Protected Files" -PolicyDescription "This policy restricts access to authorized users" } catch { Write-Error -Message "Error setting IRM configuration on site: $webUrl.`nError Details: $($_.Exception.ToString())" } } finally { if($grantedSiteCollectionAdmin) { # remove the temporary admin rights to the site collection Set-SPOUser -Site $script:clientContext.Site.Url -LoginName $o365TenantAdminCredential.UserName -IsSiteCollectionAdmin $false | Out-Null } } } Disconnect-SPOService -ErrorAction SilentlyContinue
    ```

4.  Granska skriptet och göra följande ändringar:

    1.  Söka efter `$sharepointAdminCenterUrl` och ersätta exempel värdet med ditt eget URL för SharePoint-administratören.

        Du hittar det här värdet som den grundläggande Webbadressen när du gå till Administrationscenter för SharePoint och den har följande format: https://*&lt; tenant_name &gt;*-admin.sharepoint.com

        Exempel: om innehavaren namnet är "contoso", sedan anger du: **https://contoso-admin.sharepoint.com**

    2.  Söka efter `$tenantAdmin` och ersätta exempelvärde med fullständigt kvalificerade global administratörskontot för Office 365.

        Det här värdet är samma som du använder för att logga in på Office 365 admin portal som global administratör och har följande format: användarnamn @*&lt; domännamn innehavaren &gt;*com

        Om användarnamnet för Office 365 global administratör är "admin" för "contoso.com" innehavaren domän, anger du: **admin@contoso.com**

    3.  Söka efter `$webUrls` och ersätta exempelvärden med OneDrive för dina användare för Business webbadresser, lägga till eller ta bort så många poster som du behöver.

        Du kan också visa kommentarer i skriptet om hur du ersätta den här matrisen genom att importera en. CSV-fil som innehåller alla URL: er måste du konfigurera.  Vi har angett ett annat exempelskript för att söka efter och extrahera URL: er att fylla i det här. CSV-fil. När du är redo att göra detta expanderar den [Ytterligare skript för utmatning av alla OneDrive för Business URL: er till en. CSV-fil](#BKMK_Script_OD4B_URLS) omedelbart efter dessa steg.

        Webben URL för användarens OneDrive för företag finns i följande format: https://*&lt; innehavaren namn &gt;*-my.sharepoint.com/personal/*&lt; användarnamn &gt;*_*&lt; innehavaren namn &gt;*_com

        Om användaren i contoso innehavaren har ett användarnamn på "rsimone", anger du: **https://contoso-my.sharepoint.com/personal/rsimone_contoso_com**

    4.  Eftersom vi använder skriptet för att konfigurera OneDrive för företag, inte ändra värdet för **Documents** för den `$listTitle` variabeln.

    5.  Söka efter `ADMIN INSTRUCTIONS`. Om du gör några ändringar i det här avsnittet kommer användarens OneDrive för företag att konfigureras för IRM med "Skyddade filer" princip rubrik och beskrivning av "den här principen begränsar åtkomst till behöriga användare".  Inga andra alternativ för IRM ställs in, vilket är förmodligen lämpligt för de flesta miljöer. Du kan dock ändra föreslagna rubrik och beskrivning och även lägga till andra IRM alternativ som är lämpliga för din miljö. Se kommenterad exemplet i skriptet som hjälper dig att skapa en egen uppsättning parametrar för kommandot Set-IrmConfiguration.

5.  Spara skriptet och registrera den. Om du inte logga in skriptet (säkrare), måste Windows PowerShell konfigureras på datorn för att köra osignerade skript. Genom att köra en Windows PowerShell-session med den **Kör som administratör** alternativ och skriver: **Set-ExecutionPolicy Unrestricted**. Den här konfigurationen kan dock alla unsigned-skript som körs (mindre säkert).

    Mer information om signering Windows PowerShell-skript, se [about_Signing](https://technet.microsoft.com/library/hh847874.aspx) i dokumentationsbiblioteket till PowerShell.

6.  Kör skriptet och om du uppmanas att ange lösenordet för administratörskonto Office 365. Om du ändrar skriptet och körs i samma Windows PowerShell-session ombeds du inte för autentiseringsuppgifter.

> [!TIP]
> Du kan också använda det här skriptet för att konfigurera IRM för SharePoint Online-biblioteket. För den här konfigurationen du förmodligen vill aktivera alternativet ytterligare **tillåter inte användare att överföra dokument som inte stöder IRM**, för att säkerställa att biblioteket innehåller endast skyddat dokument.    Lägg till som gör det `-IrmReject` parameter för kommandot Set-IrmConfiguration i skriptet.
> 
> Du också behöver ändra den `$webUrls` variabeln (till exempel **https://contoso.sharepoint.com**) och  `$listTitle` variabeln (till exempel **$Reports**).

Om du behöver inaktivera IRM för användarens OneDrive för Business bibliotek expanderar den [Skript för att inaktivera IRM för OneDrive för företag](#BKMK_Script_OD4B_DisableIRM) avsnitt.

###### <a name="BKMK_Script_OD4B_URLS"></a>Ytterligare skript för utmatning av alla OneDrive för Business URL: er till en. CSV-fil
Du kan använda följande Windows PowerShell-skriptet ska extraheras URL: erna för alla användare OneDrive för Business-bibliotek som du kan markera, redigera vid behov och importera sedan till huvudsakliga skriptet för steg 4c ovan.

Det här skriptet kräver den [SharePoint Online Client Components SDK](http://www.microsoft.com/en-us/download/details.aspx?id=42038) och [SharePoint Online Management Shell](http://www.microsoft.com/en-us/download/details.aspx?id=35588). Följ instruktionerna för samma att kopiera och klistra in den, spara filen lokalt (till exempel "rapport-OneDriveForBusinessSiteInfo.ps1"), ändra den   `$sharepointAdminCenterUrl` och `$tenantAdmin` värden som innan och kör skriptet.

*&#42;&#42;Friskrivning från&#42;&#42;*: Det här exempelskriptet stöds inte under en Microsoft support standard program eller tjänst. Det här exempelskriptet tillhandahålls som är utan garanti av något slag.

```
# Requires Windows PowerShell version 3 <# Description: Queries the search service of an Office 365 tenant to retrieve all OneDrive for Business sites. Details of the discovered sites are written to a .CSV file (by default,"OneDriveForBusinessSiteInfo_<date>.csv"). Script Installation Requirements: SharePoint Online Client Components SDK http://www.microsoft.com/en-us/download/details.aspx?id=42038 SharePoint Online Management Shell http://www.microsoft.com/en-us/download/details.aspx?id=35588 ====== #> # URL will be in the format https://<tenant-name>-admin.sharepoint.com $sharepointAdminCenterUrl = "https://contoso-admin.sharepoint.com" $tenantAdmin = "admin@contoso.onmicrosoft.com" $reportName = "OneDriveForBusinessSiteInfo_$((Get-Date).ToString("yyyy-MM-dd_hh.mm.ss")).csv" $oneDriveForBusinessSiteUrls= @() $resultsProcessed = 0 function Load-SharePointOnlineClientComponentAssemblies { [cmdletbinding()] param() process { # assembly location: C:\Program Files\Common Files\microsoft shared\Web Server Extensions\16\ISAPI try { Write-Verbose "Loading Assembly: Microsoft.Office.Client.Policy, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c" [System.Reflection.Assembly]::Load("Microsoft.Office.Client.Policy, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null Write-Verbose "Loading Assembly: Microsoft.Office.Client.TranslationServices, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c" [System.Reflection.Assembly]::Load("Microsoft.Office.Client.TranslationServices, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c" [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.DocumentManagement, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c" [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.DocumentManagement, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Publishing, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c" [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Publishing, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Runtime, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c" [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Runtime, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Search.Applications, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c" [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Search.Applications, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Search, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c" [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Search, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Taxonomy, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c" [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Taxonomy, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.UserProfiles, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c" [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.UserProfiles, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null return $true } catch { if($_.Exception.Message -match "Could not load file or assembly") { Write-Error -Message "Unable to load the SharePoint Server 2013 Client Components.`nDownload Location: http://www.microsoft.com/en-us/download/details.aspx?id=42038" } else { Write-Error -Exception $_.Exception } return $false } } } function Load-SharePointOnlineModule { [cmdletbinding()] param() process { do { # Installation location: C:\Program Files\SharePoint Online Management Shell\Microsoft.Online.SharePoint.PowerShell $spoModule = Get-Module -Name Microsoft.Online.SharePoint.PowerShell -ErrorAction SilentlyContinue if(-not $spoModule) { try { Import-Module Microsoft.Online.SharePoint.PowerShell -DisableNameChecking return $true } catch { if($_.Exception.Message -match "Could not load file or assembly") { Write-Error -Message "Unable to load the SharePoint Online Management Shell.`nDownload Location: http://www.microsoft.com/en-us/download/details.aspx?id=35588" } else { Write-Error -Exception $_.Exception } return $false } } else { return $true } } while(-not $spoModule) } } function Get-CredentialFromCredentialCache { [cmdletbinding()] param([string]$CredentialName) #if( Test-Path variable:\global:CredentialCache ) if( Get-Variable O365TenantAdminCredentialCache -Scope Global -ErrorAction SilentlyContinue ) { if($global:O365TenantAdminCredentialCache.ContainsKey($CredentialName)) { Write-Verbose "Credential Cache Hit: $CredentialName" return $global:O365TenantAdminCredentialCache[$CredentialName] } } Write-Verbose "Credential Cache Miss: $CredentialName" return $null } function Add-CredentialToCredentialCache { [cmdletbinding()] param([System.Management.Automation.PSCredential]$Credential) if(-not (Get-Variable CredentialCache -Scope Global -ErrorAction SilentlyContinue)) { Write-Verbose "Initializing the Credential Cache" $global:O365TenantAdminCredentialCache = @{} } Write-Verbose "Adding Credential to the Credential Cache" $global:O365TenantAdminCredentialCache[$Credential.UserName] = $Credential } # load the required assemblies and Windows PowerShell modules if(-not ((Load-SharePointOnlineClientComponentAssemblies) -and (Load-SharePointOnlineModule)) ) { return } # Add the credentials to the client context and SharePoint Online service connection # check for cached credentials to use $o365TenantAdminCredential = Get-CredentialFromCredentialCache -CredentialName $tenantAdmin if(-not $o365TenantAdminCredential) { # when credentials are not cached, prompt for the tenant admin credentials $o365TenantAdminCredential = Get-Credential -UserName $tenantAdmin -Message "Enter the password for the Office 365 admin" if(-not $o365TenantAdminCredential -or -not $o365TenantAdminCredential.UserName -or $o365TenantAdminCredential.Password.Length -eq 0 ) { Write-Error -Message "Could not validate the supplied tenant admin credentials" return } # add the credentials to the cache Add-CredentialToCredentialCache -Credential $o365TenantAdminCredential } # establish the client context and set the credentials to connect to the site $clientContext = New-Object Microsoft.SharePoint.Client.ClientContext($sharepointAdminCenterUrl) $clientContext.Credentials = New-Object Microsoft.SharePoint.Client.SharePointOnlineCredentials($o365TenantAdminCredential.UserName, $o365TenantAdminCredential.Password) # run a query against the Office 365 tenant search service to retrieve all OneDrive for Business URLs do { # build the query object $query = New-Object Microsoft.SharePoint.Client.Search.Query.KeywordQuery($clientContext) $query.TrimDuplicates        = $false $query.RowLimit              = 500 $query.QueryText             = "SPSiteUrl:'/personal/' AND contentclass:STS_Site" $query.StartRow              = $resultsProcessed $query.TotalRowsExactMinimum = 500000 # run the query $searchExecutor = New-Object Microsoft.SharePoint.Client.Search.Query.SearchExecutor($clientContext) $queryResults = $searchExecutor.ExecuteQuery($query) $clientContext.ExecuteQuery() # enumerate the search results and store the site URLs $queryResults.Value[0].ResultRows | % { $oneDriveForBusinessSiteUrls += $_.Path $resultsProcessed++ } } while($resultsProcessed -lt $queryResults.Value.TotalRows) $oneDriveForBusinessSiteUrls | Out-File -FilePath $reportName
```

###### <a name="BKMK_Script_OD4B_DisableIRM"></a>Skript för att inaktivera IRM för OneDrive för företag
Använd följande exempelskriptet om du behöver inaktivera IRM för användarnas OneDrive för företag.

Det här skriptet kräver den [SharePoint Online Client Components SDK](http://www.microsoft.com/en-us/download/details.aspx?id=42038) och [SharePoint Online Management Shell](http://www.microsoft.com/en-us/download/details.aspx?id=35588). Kopiera och klistra in innehållet, spara filen lokalt (till exempel "Inaktivera-IRMOnOneDriveForBusiness.ps1") och ändra den   `$sharepointAdminCenterUrl` och `$tenantAdmin` värden. Manuellt ange OneDrive för Business URL: er eller använda skript i avsnittet ovan så att du kan importera de och kör skriptet.

*&#42;&#42;Friskrivning från&#42;&#42;*: Det här exempelskriptet stöds inte under en Microsoft support standard program eller tjänst. Det här exempelskriptet tillhandahålls som är utan garanti av något slag.

```
# Requires Windows PowerShell version 3 <# Description: Disables IRM for OneDrive for Business and can also be used for SharePoint Online libraries and lists Script Installation Requirements: SharePoint Online Client Components SDK http://www.microsoft.com/en-us/download/details.aspx?id=42038 SharePoint Online Management Shell http://www.microsoft.com/en-us/download/details.aspx?id=35588 ====== #> $sharepointAdminCenterUrl = "https://contoso-admin.sharepoint.com" $tenantAdmin = "admin@contoso.com" $webUrls = @("https://contoso-my.sharepoint.com/personal/user1_contoso_com", "https://contoso-my.sharepoint.com/personal/user2_contoso_com", "https://contoso-my.sharepoint.com/personal/person3_contoso_com") <# As an alternative to specifying the URLs as an array, you can import them from a CSV file (no header, single value per row). Then, use: $webUrls = Get-Content -Path "File_path_and_name.csv" #> $listTitle = "Documents" function Load-SharePointOnlineClientComponentAssemblies { [cmdletbinding()] param() process { # assembly location: C:\Program Files\Common Files\microsoft shared\Web Server Extensions\16\ISAPI try { Write-Verbose "Loading Assembly: Microsoft.Office.Client.Policy, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c" [System.Reflection.Assembly]::Load("Microsoft.Office.Client.Policy, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null Write-Verbose "Loading Assembly: Microsoft.Office.Client.TranslationServices, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c" [System.Reflection.Assembly]::Load("Microsoft.Office.Client.TranslationServices, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c" [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.DocumentManagement, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c" [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.DocumentManagement, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Publishing, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c" [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Publishing, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Runtime, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c" [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Runtime, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Search.Applications, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c" [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Search.Applications, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Search, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c" [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Search, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Taxonomy, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c" [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Taxonomy, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.UserProfiles, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c" [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.UserProfiles, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null return $true } catch { if($_.Exception.Message -match "Could not load file or assembly") { Write-Error -Message "Unable to load the SharePoint Server 2013 Client Components.`nDownload Location: http://www.microsoft.com/en-us/download/details.aspx?id=42038" } else { Write-Error -Exception $_.Exception } return $false } } } function Load-SharePointOnlineModule { [cmdletbinding()] param() process { do { # Installation location: C:\Program Files\SharePoint Online Management Shell\Microsoft.Online.SharePoint.PowerShell $spoModule = Get-Module -Name Microsoft.Online.SharePoint.PowerShell -ErrorAction SilentlyContinue if(-not $spoModule) { try { Import-Module Microsoft.Online.SharePoint.PowerShell -DisableNameChecking return $true } catch { if($_.Exception.Message -match "Could not load file or assembly") { Write-Error -Message "Unable to load the SharePoint Online Management Shell.`nDownload Location: http://www.microsoft.com/en-us/download/details.aspx?id=35588" } else { Write-Error -Exception $_.Exception } return $false } } else { return $true } } while(-not $spoModule) } } function Remove-IrmConfiguration { [cmdletbinding()] param( [parameter(Mandatory=$true)][Microsoft.SharePoint.Client.List]$List ) process { Write-Verbose "Disabling IRM Configuration on '$($List.Title)'" $List.IrmEnabled = $false $List.IrmExpire  = $false $List.IrmReject  = $false $List.InformationRightsManagementSettings.Reset() } end { if($List) { Write-Verbose "Committing IRM configuration settings on '$($list.Title)'" $list.InformationRightsManagementSettings.Update() $list.Update() $script:clientContext.Load($list) $script:clientContext.ExecuteQuery() } } } function Get-CredentialFromCredentialCache { [cmdletbinding()] param([string]$CredentialName) #if( Test-Path variable:\global:CredentialCache ) if( Get-Variable O365TenantAdminCredentialCache -Scope Global -ErrorAction SilentlyContinue ) { if($global:O365TenantAdminCredentialCache.ContainsKey($CredentialName)) { Write-Verbose "Credential Cache Hit: $CredentialName" return $global:O365TenantAdminCredentialCache[$CredentialName] } } Write-Verbose "Credential Cache Miss: $CredentialName" return $null } function Add-CredentialToCredentialCache { [cmdletbinding()] param([System.Management.Automation.PSCredential]$Credential) if(-not (Get-Variable CredentialCache -Scope Global -ErrorAction SilentlyContinue)) { Write-Verbose "Initializing the Credential Cache" $global:O365TenantAdminCredentialCache = @{} } Write-Verbose "Adding Credential to the Credential Cache" $global:O365TenantAdminCredentialCache[$Credential.UserName] = $Credential } # load the required assemblies and Windows PowerShell modules if(-not ((Load-SharePointOnlineClientComponentAssemblies) -and (Load-SharePointOnlineModule)) ) { return } # Add the credentials to the client context and SharePoint Online service connection # check for cached credentials to use $o365TenantAdminCredential = Get-CredentialFromCredentialCache -CredentialName $tenantAdmin if(-not $o365TenantAdminCredential) { # when credentials are not cached, prompt for the tenant admin credentials $o365TenantAdminCredential = Get-Credential -UserName $tenantAdmin -Message "Enter the password for the Office 365 admin" if(-not $o365TenantAdminCredential -or -not $o365TenantAdminCredential.UserName -or $o365TenantAdminCredential.Password.Length -eq 0 ) { Write-Error -Message "Could not validate the supplied tenant admin credentials" return } # add the credentials to the cache Add-CredentialToCredentialCache -Credential $o365TenantAdminCredential } # connect to Office365 first, required for SharePoint Online cmdlets to run Connect-SPOService -Url $sharepointAdminCenterUrl -Credential $o365TenantAdminCredential # enumerate each of the specified site URLs foreach($webUrl in $webUrls) { $grantedSiteCollectionAdmin = $false try { # establish the client context and set the credentials to connect to the site $script:clientContext = New-Object Microsoft.SharePoint.Client.ClientContext($webUrl) $script:clientContext.Credentials = New-Object Microsoft.SharePoint.Client.SharePointOnlineCredentials($o365TenantAdminCredential.UserName, $o365TenantAdminCredential.Password) # initialize the site and web context $script:clientContext.Load($script:clientContext.Site) $script:clientContext.Load($script:clientContext.Web) $script:clientContext.ExecuteQuery() # load and ensure the tenant admin user account if present on the target SharePoint site $tenantAdminUser = $script:clientContext.Web.EnsureUser($o365TenantAdminCredential.UserName) $script:clientContext.Load($tenantAdminUser) $script:clientContext.ExecuteQuery() # check if the tenant admin is a site admin if( -not $tenantAdminUser.IsSiteAdmin ) { try { # grant the tenant admin temporary admin rights to the site collection Set-SPOUser -Site $script:clientContext.Site.Url -LoginName $o365TenantAdminCredential.UserName -IsSiteCollectionAdmin $true | Out-Null $grantedSiteCollectionAdmin = $true } catch { Write-Error $_.Exception return } } try { # load the list orlibrary using CSOM $list = $null $list = $script:clientContext.Web.Lists.GetByTitle($listTitle) $script:clientContext.Load($list) $script:clientContext.ExecuteQuery() Remove-IrmConfiguration -List $list } catch { Write-Error -Message "Error setting IRM configuration on site: $webUrl.`nError Details: $($_.Exception.ToString())" } } finally { if($grantedSiteCollectionAdmin) { # remove the temporary admin rights to the site collection Set-SPOUser -Site $script:clientContext.Site.Url -LoginName $o365TenantAdminCredential.UserName -IsSiteCollectionAdmin $false | Out-Null } } } Disconnect-SPOService -ErrorAction SilentlyContinue
```

## <a name="BKMK_Office2013Configuration"></a>Office 2016 och Office 2013: Konfiguration för klienter
Eftersom dessa senare versioner av Office stöder Azure RMS, krävs ingen konfiguration av en klientdator som stöd för informationsrättighetshantering (IRM) för program som Word, Excel, PowerPoint, Outlook och Outlook Web App. Alla användare behöver är logga in på Office-programmen med sina [!INCLUDE[o365_1](../Token/o365_1_md.md)] autentiseringsuppgifter och de kan skydda filer och e-post och använda filer och e-postmeddelanden som har skyddats av andra.

Men rekommenderar vi att du komplettera dessa program med Rights Management delning, så att användarna får nytta av Office-tillägg. Mer information finns i [Rights Management delning: Installation och konfiguration för klienter](../Topic/Configuring_Applications_for_Azure_Rights_Management.md#BKMK_SharingApp) i det här avsnittet.

## <a name="BKMK_Office2010Configuration"></a>Office 2010: Konfiguration för klienter
För klientdatorer använder Azure RMS med Office 2010 måste de ha installerat Rights Management dela program för Windows. Ingen ytterligare konfiguration krävs än användare måste logga in med sitt [!INCLUDE[o365_1](../Token/o365_1_md.md)] autentiseringsuppgifter och de kan skydda filer och använda filer har skyddats av andra.

Mer information om delningsapplikation Rights Management finns på [Rights Management delning: Installation och konfiguration för klienter](../Topic/Configuring_Applications_for_Azure_Rights_Management.md#BKMK_SharingApp) i det här avsnittet.

## <a name="BKMK_SharingApp"></a>Rights Management delning: Installation och konfiguration för klienter
Rights Management (RMS) delning krävs för klientdatorer använder Azure RMS med Office 2010 och rekommenderas för alla datorer och mobila enheter som stöder Azure RMS. RMS-delning programmet integreras med Office program genom att installera en Office-tillägg så att användarna kan enkelt skydda filer och e-postmeddelanden direkt från menyfliksområdet. Det ger också allmän skydd för filtyper som inte stöds av Azure RMS och dokument spårning webbplats för användare för att spåra och återkalla filer som de har skyddat.

### <a name="BKMK_SharingAppforWindows"></a>RMS-delning program för Windows: Installation och konfiguration
Om du vill installera och konfigurera RMS-delning program för Windows för en enterprise-distribution finns i [Rights Management dela program administratörshandboken](http://technet.microsoft.com/library/dn339003.aspx).

> [!TIP]
> Om du vill snabbt installera och testa RMS-delning program för en enstaka dator, se [Hämta och installera delningsapplikation Rights Management](http://technet.microsoft.com/library/dn574734.aspx) från den [Rights Management delning användaren guide till](http://technet.microsoft.com/library/dn339006.aspx).

### <a name="BKMK_SharingAppMovileDevices"></a>RMS-delning program för mobila plattformar: Installation
Om du vill installera RMS-delning program för mobila plattformar, du kan hämta relevanta app med hjälp av länkarna på den [Microsoft Rights Management sidan](http://go.microsoft.com/fwlink/?LinkId=303970). Ingen konfiguration krävs för att använda Azure RMS med den här appen.

## <a name="BKMK_RMSAPIs"></a>Andra program som stöder RMS APIs: Installation och konfiguration
Den här kategorin innehåller av branschspecifika program som utvecklas internt med hjälp av RMS-SDK och program från leverantörer som är skrivna med hjälp av RMS-SDK. Följ instruktionerna som medföljer programmet för dessa program.

## Nästa steg
När du har konfigurerat programmen stöd Azure Rights Management kan använda den [Översikt över Azure Rights Management-distribution](../Topic/Azure_Rights_Management_Deployment_Roadmap.md) att kontrollera om det finns andra konfigurationssteg som du kan göra innan du lansera [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] för användare och administratörer. Om det inte finns i avsnittet [Använda Azure Rights Management](../Topic/Using_Azure_Rights_Management.md) för nästa steg.

## Se även
[Konfigurera Azure Rights Management](../Topic/Configuring_Azure_Rights_Management.md)

