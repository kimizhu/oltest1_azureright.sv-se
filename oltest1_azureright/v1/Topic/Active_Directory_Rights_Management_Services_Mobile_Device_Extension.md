---
description: na
keywords: na
title: Active Directory Rights Management Services Mobile Device Extension
search: na
ms.date: na
ms.tgt_pltfrm: na
ms.assetid: a69ead9d-7dd3-4b38-9830-4728e9757341
robots: noindex,nofollow
---
# Till&#228;gg till mobila enheter f&#246;r Active Directory Rights Management Services
AD RMS-tillägget (Active Directory Rights Management Services) för mobila enheter körs ovanpå en befintlig AD RMS-distribution. På så sätt kan användare som har mobila enheter skydda och använda känsliga data om enheten har stöd för den senaste RMS-klienten och använder RMS-upplysta appar. Användare kan exempelvis göra följande på dessa enheter:

-   Använda RMS-delningsappen för att använda skyddade textfiler i olika format (inklusive TXT-, CSV- och XML-filer).

-   Använda RMS-delningsappen för att använda skyddade bildfiler (inklusive JPG-, GIF- och TIFF-filer).

-   Använda RMS-delningsappen för att öppna en fil som har allmänt skydd (PFILE-formatet).

-   Använda RMS-delningsappen för att skydda bildfiler på enheten.

-   Använda en RMS-upplyst PDF-visningsapp för mobila enheter för att öppna PDF-filer som är skyddade med RMS-delningsprogrammet för Windows eller en något annat RMS-upplyst program.

-   Använda andra appar från leverantörer som tillhandahåller RMS-upplysta appar som stöder filtyper med internt stöd för RMS.

-   Använd internt utvecklade RMS-upplysta appar som har skapats med hjälp av RMS SDK.

> [!NOTE]
> Du kan hämta RMS-delningsappen från sidan [Microsoft Rights Management](http://go.microsoft.com/fwlink/?LinkId=303970) på Microsofts webbplats.
> 
> Mer information om de olika filtyper som RMS stöder finns i avsnittet [Supported file types and file name extensions](http://technet.microsoft.com/library/dn339003.aspx) i administratörsguiden för Delningsapplikationen för Microsoft Rights Management.

Du behöver inte tillägget för mobila enheter för att kunna använda eller redigera skyddad e-post på enheter om de använder ett e-postprogram som stöder Exchange ActiveSync IRM. Det här inbyggda stödet för RMS och mobila enheter introducerades i Exchange 2010 Service Pack 1.

Du kan använda följande avsnitt för att distribuera AD RMS- tillägget för mobila enheter:

-   [Prerequisites for the AD RMS mobile device extension](../Topic/Active_Directory_Rights_Management_Services_Mobile_Device_Extension.md#BKMK_Preqs)

    -   [Configuring AD FS for the AD RMS mobile device extension](../Topic/Active_Directory_Rights_Management_Services_Mobile_Device_Extension.md#BKMK_ADFS)

    -   [Configuring AD FS for the AD RMS mobile device extension](../Topic/Active_Directory_Rights_Management_Services_Mobile_Device_Extension.md#BKMK_ADFS)

-   [Specifying the DNS SRV records for the AD RMS mobile device extension](../Topic/Active_Directory_Rights_Management_Services_Mobile_Device_Extension.md#BKMK_SRV)

-   [Deploying the AD RMS mobile device extension](../Topic/Active_Directory_Rights_Management_Services_Mobile_Device_Extension.md#BKMK_Deploy)

## <a name="BKMK_Preqs"></a>Krav för AD RMS-tillägget för mobila enheter
Kontrollera att dessa beroenden är på plats innan du installerar AD RMS-tillägget för mobila enheter.

|Krav|Mer information|
|--------|-------------------|
|En befintlig AD RMS-distribution på Windows Server 2012 R2 eller Windows Server 2012. **Note:** AD RMS måste använda en fullständig Microsoft SQL Server-baserad databas på en separat server och inte den interna Windows-databasen, som ofta används för testning på samma server.|Dokumentation för AD RMS finns i [Active Directory Rights Management Services](http://technet.microsoft.com/library/hh831364.aspx) i Windows Server-biblioteket.|
|AD FS distribuerat på Windows Server 2012 R2|Dokumentation för AD FS finns i [Windows Server 2012 R2 AD FS Deployment Guide](http://technet.microsoft.com/library/dn486820.aspx) i Windows Server-biblioteket.<br /><br />AD FS måste konfigureras för tillägget för mobila enheter. Instruktioner finns i avsnittet [Configuring AD FS for the AD RMS mobile device extension](../Topic/Active_Directory_Rights_Management_Services_Mobile_Device_Extension.md#BKMK_ADFS) i det här ämnet.|
|SRV-poster i DNS|Skapa en eller flera SRV-poster i företagets domän eller domäner:<br /><br />-   En post för varje e-postdomänsuffix som användarna ska använda<br />-   En post för varje FQDN som används av RMS-klustren för att skydda innehållet<br /><br />När användarna anger sina e-postadresser från sina mobila enheter används domänsuffixet för att identifiera om de ska använda en AD RMS-infrastruktur eller Azure RMS. När SRV-posten hittas, omdirigeras klienterna till AD RMS-servern som svarar på URL:en.<br /><br />När användarna använder skyddat innehåll på en mobil enhet söker klientprogrammet i DNS efter en post som matchar FQDN i URL:en för klustret som skyddade innehållet. Enheten omdirigeras sedan till AD RMS-klustret som anges i DNS-posten och hämtar en licens för att öppna innehållet. I de flesta fall kommer RMS-klustret att vara samma RMS-kluster som skyddar innehållet.<br /><br />Mer information om hur du anger SRV-poster finns i avsnittet [Specifying the DNS SRV Records for the AD RMS mobile device extension](../Topic/Active_Directory_Rights_Management_Services_Mobile_Device_Extension.md#BKMK_SRV) i det här ämnet.|
|Klienter som stöds för närvarande:<br /><br />-   Android-enheter som har den senaste versionen av RMS-delningsappen för Android|Android 4.0.3 eller en nyare version.<br /><br />Hämta RMS-delningsappen för Android från [Microsoft Connect](https://connect.microsoft.com/site1170/Downloads) läs in den separat till enheten.|

### <a name="BKMK_ADFS"></a>Konfigurera AD FS för AD RMS-tillägget för mobila enheter
Du måste först konfigurera AD FS och sedan godkänna RMS-delningsappen för Android.

##### Steg 1: Så här konfigurerar du AD FS

-   Du kan antingen köra ett Windows PowerShell-skript för att automatiskt konfigurera AD FS för att stödja AD RMS-tillägget för mobila enheter eller manuellt ange konfigurationsalternativ och värden:

    -   Om du vill konfigurera AD FS automatiskt kopierar du och klistrar in följande i en Windows PowerShell-skriptfil och kör den:

        ```
        # This Script Configures the Microsoft Rights Management Mobile Device Extension and Claims used in the ADFS Server

        # Check if Microsoft Rights Management Mobile Device Extension is configured on the Server 
        $CheckifConfigured = Get-AdfsRelyingPartyTrust -Identifier "api.rms.rest.com"
        if ($CheckifConfigured)
        {
        Write-Host "api.rms.rest.com Identifer used for Microsoft Rights Management Mobile Device Extension is already configured on this Server"
        Write-Host $CheckifConfigured 
        }
        else
        {
        Write-Host "Configuring  Microsoft Rights Management Mobile Device Extension "

        # TransformaRules used by Microsoft Rights Management Mobile Device Extension
        # Claims: E-mail, UPN and ProxyAddresses
        $TransformRules = @"
        @RuleTemplate = "LdapClaims"
        @RuleName = "Jwt Token"
        c:[Type ==
        "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname",
        Issuer == "AD AUTHORITY"]
         => issue(store = "Active Directory", types =
        ("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress",
        "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn",
        "http://schemas.xmlsoap.org/claims/ProxyAddresses"), query =
        ";mail,userPrincipalName,proxyAddresses;{0}", param = c.Value);

        @RuleTemplate = "PassThroughClaims"
        @RuleName = "JWT pass through"
        c:[Type == "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress"]
         => issue(claim = c);

        @RuleTemplate = "PassThroughClaims"
        @RuleName = "JWT pass through"
        c:[Type == "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn"]
         => issue(claim = c);

        @RuleTemplate = "PassThroughClaims"
        @RuleName = "JWT pass through Proxy addresses"
        c:[Type == "http://schemas.xmlsoap.org/claims/ProxyAddresses"]
         => issue(claim = c);
        "@

        # AuthorizationRules used by Microsoft Rights Management Mobile Device Extension
        # Allow All users
        $AuthorizationRules = @"
        @RuleTemplate = "AllowAllAuthzRule"
         => issue(Type = "http://schemas.microsoft.com/authorization/claims/permit",
        Value = "true");
        "@

        # Add a Relying Part Truest with Name -"Microsoft Rights Management Mobile Device Extension" Identifier "api.rms.rest.com"
        Add-ADFSRelyingPartyTrust -Name "Microsoft Rights Management Mobile Device Extension" -Identifier "api.rms.rest.com" -IssuanceTransformRules $TransformRules -IssuanceAuthorizationRules  $AuthorizationRules

        Write-Host "Microsoft Rights Management Mobile Device Extension Configured"
        }
        ```

    -   Använd de här inställningarna för att konfigurera AD FS manuellt:

        |Konfiguration|Värde|
        |-----------------|---------|
        |**Förtroende för en förlitande part**|api.rms.rest.com|
        |**Anspråksregel**|**Attributarkiv**:  Active Directory<br /><br />**E-postadresser**:  E-postadress<br /><br />**Användarens huvudnamn**:  UPN<br /><br />**Proxy-adress**:  https://schemas.xmlsoap.org/claims/ProxyAddresses|

##### Steg 2: Godkänn RMS-delningsappen för Android

-   Kör följande Windows PowerShell-kommando för att lägga till stöd för Android-enheter:

    ```
    Add-AdfsClient -Name "RMSsharingAndroid" -ClientId "com.microsoft.ipviewer" -RedirectUri @("com.microsoft.ipviewer://authorize")
    ```

### <a name="BKMK_SRV"></a>Ange DNS SRV-poster för AD RMS-tillägget för mobila enheter
Du måste skapa DNS SRV-poster för varje e-postdomän som användarna använder. Om alla användare använder underordnade domäner från en enda överordnad domän och alla användare från den här sammanhängande namnrymden använder samma RMS-kluster, kan du använda en enda SRV-post i den överordnade domänen så hittar RMS lämpliga DNS-poster.

SRV-posterna har följande format: _rmsdisco._http._tcp. *&lt;emailsuffix&gt;**&lt;portnumber&gt;**&lt;RMSClusterFQDN&gt;*

Om din organisation till exempel har användare med följande e-postadresser:

-   user@contoso.com

-   user@sales.contoso.com

-   user@fabrikam.com

och det inte finns några andra underdomäner för contoso.com som använder ett annat RMS-kluster än det som heter **rmsserver.contoso.com** skapar du två DNS SRV-poster som har följande värden:

-   _rmsdisco._http._tcp.contoso.com 443 rmsserver.contoso.com

-   _rmsdisco._http._tcp.fabrikam.com 443 rmsserver.contoso.com

Utöver dessa DNS SRV-poster för e-postdomänerna måste du skapa en annan DNS SRV-post i användardomänerna. Den här posten måste ange URL:er till det RMS-kluster som skyddar innehållet. Varje fil som skyddas av RMS innehåller en URL till det kluster som skyddade filen. Mobila enheter använder DNS SRV-posten och FQDN för URL:en som anges i posten för att hitta det RMS-kluster som kan stödja mobila enheter.

Om RMS-klustret till exempel är **rmsserver.contoso.com**, skapar du ett DNS SRV-kluster som har följande värden: **_rmsdisco._http._tcp.rmsserver.contoso.com 443 rmsserver.contoso.com**

## <a name="BKMK_Deploy"></a>Distribuera AD RMS-tillägget för mobila enheter
Kontrollera att nödvändiga komponenter från föregående avsnitt finns på plats och att du känner till URL:en till AD FS-servern, innan du installerar AD RMS-tillägget för mobila enheter. Gör sedan följande:

1.  Hämta AD RMS-tillägget för mobila enheter från [Microsoft Connect](http://go.microsoft.com/fwlink/?LinkId=397245).

2.  Kör Setup.exe om du vill starta installationsguiden för Active Directory Rights Management Services-tillägget för mobila enheter.

3.  Ange URL:en till AD FS-servern som du konfigurerat tidigare, när du uppmanas att göra det.

4.  Slutför guiden.

Kör guiden på alla noder i RMS-klustret.

