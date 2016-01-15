---
description: na
keywords: na
title: Requirements for Azure Rights Management
search: na
ms.date: na
ms.service: rights-management
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: dc78321d-d759-4653-8818-80da74b6cdeb
---
# Krav f&#246;r Azure Rights Management
Kontrollera att du har följande förutsättningar för att distribuera Microsoft Azure Rights Management (Azure RMS) i din organisation. Du kan sedan använda den [Översikt över Azure Rights Management-distribution](../Topic/Azure_Rights_Management_Deployment_Roadmap.md) för att distribuera Rights Management för din organisation.

|Krav|Mer information|
|--------|-------------------|
|En prenumeration för molnet för RMS|Din organisation måste ha en prenumeration för molnet som stöd för RMS.<br /><br />Licensinformationen, finns det [Molnet prenumerationer som har stöd för Azure RMS](../Topic/Requirements_for_Azure_Rights_Management.md#BKMK_SupportedSubscriptions) i det här avsnittet.|
|Azure AD-katalog|Din organisation måste ha en katalog för Azure AD RMS för autentisering av användare. Om du vill använda dina användarkonton från din lokala katalog (AD DS), måste du dessutom även konfigurera katalogintegrering.<br /><br />Multifaktorautentisering (MFA) stöds med Azure RMS när du har nödvändig programvara för klienter och korrekt konfigurerad MFA stödjande infrastruktur.<br /><br />Mer information finns i [Azure AD-katalog](../Topic/Requirements_for_Azure_Rights_Management.md#BKMK_AzureADTenant) i det här avsnittet.|
|Klientenheter|Användarna måste ha en klientenheter (dator eller mobil enhet) som kör ett operativsystem som stöder RMS.<br /><br />Mer information finns i [Klientenheter som stöd för Azure RMS](../Topic/Requirements_for_Azure_Rights_Management.md#BKMK_SupportedDevices) i det här avsnittet.|
|Program|Användaren måste köra program som stöder RMS.<br /><br />Mer information finns i [Program som stöder Azure RMS](../Topic/Requirements_for_Azure_Rights_Management.md#BKMK_SupportedApplications) i det här avsnittet.|
|Infrastruktur som stöder anslutning till Internet och beroende molntjänster|Om du har en brandvägg eller liknande delta nätverksenheter som måste konfigureras för att tillåta specifika anslutningar, se [Office 356 URL: er och IP-adressintervall](https://support.office.com/en-US/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2).<br /><br />Lista över URL: er och IP-adresser i det **Office 356 portal och identitet** gäller för Office 365-portalen, Azure Active Directory-resurser och Azure Rights Management. Följ instruktionerna i den här artikeln att uppdaterade med ändringar för den här informationen genom att prenumerera på en RSS-feed.<br /><br />Förutom informationen i Office-artikel specifika för Azure RMS:<br /><br />-   Avsluta inte TLS klient-till-tjänst-anslutning (till exempel för att göra paket nivå kontrollsystem). Gör det bryts certifikatet fästa som RMS-klienter använda med Microsoft hanterar certifikatutfärdare till att skydda deras kommunikation med Azure RMS.<br />-   Använd inte en webbproxykonfigurationen som autentiserar för en användares räkning.|

Om du vill använda Azure RMS med lokala servrar stöds följande produkter:

-   Exchange Server

-   SharePoint-servern

-   Windows Server-filservrar som stöder fil klassificering infrastruktur

Information om ytterligare Azure RMS kraven för det här scenariot finns i [Lokala servrar som stöder Azure RMS](../Topic/Requirements_for_Azure_Rights_Management.md#BKMK_SupportedServers) i det här avsnittet.

> [!IMPORTANT]
> I följande scenario för distribution stöds inte:
> 
> -   Kör AD RMS och Azure RMS sida-vid-sida i samma organisation, utom vid migrering, enligt beskrivningen i [Migrera från AD RMS till Azure Rights Management](../Topic/Migrating_from_AD_RMS_to_Azure_Rights_Management.md).
> 
> Det finns en sökväg av migreringar stöds [från AD RMS till Azure RMS](http://technet.microsoft.com/library/Dn858447.aspx), och från [Azure RMS till AD RMS](http://msdn.microsoft.com/library/azure/dn629429.aspx). Om du distribuerar Azure RMS och sedan bestämma att du inte längre vill att använda den här Molntjänsten finns [Inaktivering och inaktivera Azure Rights Management](../Topic/Decommissioning_and_Deactivating_Azure_Rights_Management.md).

Använd följande avsnitt om du vill veta mer om kraven på Azure RMS.

## <a name="BKMK_SupportedSubscriptions"></a>Molnet prenumerationer som har stöd för Azure RMS
Om du vill använda Azure RMS, måste din organisation ha minst en av följande prenumerationer med ett tillräckligt antal licenser för användare och tjänster som skyddar filer och e-postmeddelanden. Om du har en tjänst som gäller skydd för användare (ägare till filer eller e-postmeddelanden) kan behöver dessa användare en av dessa licenser. Användare som kommer att endast använda (till exempel läsa och redigera) den här skyddade data behöver inte en licens.

-   Office 365

-   Azure Rights Management Premium (tidigare Azure RMS fristående)

-   Enterprise Mobility Suite

-   RMS för individer

Använd följande avsnitt för mer information och logga in alternativ.

En licensiering jämförelse av Azure RMS-funktioner för betalda prenumerationer finns [erbjudanden för jämförelse av Rights Management Services (RMS)](http://technet.microsoft.com/dn858608).

### Office 365-prenumeration
[Kostnadsfri 30-dagars utvärderingsversion: Enterprise E3](http://go.microsoft.com/fwlink/p/?LinkID=403802)

Den här prenumerationen är utformat för företag som vill använda Office online-tjänster och använda deras Information Rights Management-funktionen som använder Azure RMS. Dock innehåller inte alla prenumerationer på Office 365 Azure RMS.

|Alternativet licensiering|Office 365 Business Essentials|Office 365 Business Premium|Office 365 Enterprise E1<br /><br />Office 365 utbildning A1|Office 365 Enterprise E3<br /><br />Office 365 utbildning A3<br /><br />Office 365 statlig G3|Office 365 Enterprise E4<br /><br />Office 365 utbildning A4<br /><br />Office 365 statlig G4|Office 365 Enterprise K1|SharePoint-Plan 1<br />SharePoint Plan 2|Exchange Online Plan 1<br />Exchange Online Plan 2|
|-----------------------------|----------------------------------|-------------------------------|--------------------------------------------------------|---------------------------------------------------------------------------------|---------------------------------------------------------------------------------|----------------------------|----------------------------------------|--------------------------------------------------|
|Informationsskydd rättigheter (IRM)|Nej|Nej|Nej|Ja|Ja|Nej|Nej|Nej|

### Azure Rights Management Premium-prenumeration
[Kostnadsfri 30-dagars utvärderingsversion](https://portal.microsoftonline.com/Signup/MainSignUp15.aspx?&amp;OfferId=A43415D3-404C-4df3-B31B-AAD28118A778&amp;dl=RIGHTSMANAGEMENT&amp;ali=1)

Den här prenumerationen som tidigare kallades Azure RMS fristående och den är avsedd för organisationer som använder Azure RMS, men inte har en prenumeration som innehåller Azure RMS. Till exempel om du har en prenumeration för Office 365 Business Essentials eller Office 365 Enterprise E1 dessa prenumerationer saknar Azure RMS (finns i tabellen i föregående avsnitt). Om du vill använda Azure RMS, kan du köpa en prenumeration för Azure Rights Management Premium (eller köpa ytterligare en prenumeration, till exempel Office 365 Enterprise E4 med Azure RMS).

Mer information finns i [Microsoft Azure Rights Management](http://products.office.com/business/microsoft-azure-rights-management).

Den här prenumerationen har även en provperiod att prova Azure RMS för 25 användare, utan kostnad. Om prenumerationen går ut innan du köper en ersättning prenumeration finns i följande avsnitt "Vad händer när utvärderingsprenumeration upphör att gälla?"

|Alternativet licensiering|Office 365 Business Essentials|Office 365 Business Premium|Office 365 Enterprise E1<br /><br />Office 365 utbildning A1|Office 365 Enterprise E3<br /><br />Office 365 utbildning A3<br /><br />Office 365 statlig G3|Office 365 Enterprise E4<br /><br />Office 365 utbildning A4<br /><br />Office 365 statlig G4|Office 365 Enterprise K1|SharePoint-Plan 1<br />SharePoint Plan 2|Exchange Online Plan 1<br />Exchange Online Plan 2|
|-----------------------------|----------------------------------|-------------------------------|--------------------------------------------------------|---------------------------------------------------------------------------------|---------------------------------------------------------------------------------|----------------------------|----------------------------------------|--------------------------------------------------|
|Informationsskydd rättigheter (IRM)|Ja|Yes <sup>1</sup>|Ja|Ja|Ja|Ja|Ja|Ja|
<sup>1</sup> för Business Premium och det finns vissa begränsningar för klienten: Du kan skydda innehåll och använder skyddat innehåll med RMS genom att använda Outlook Web App och RMS-delningsappen. Du kan använda skyddat innehåll med hjälp av alla andra Office-program som innehåller Office Online och klientprogrammen för Office 365 Business Premium.

#### <a name="BKMK_TrialExpiryBehavior"></a>Vad händer när utvärderingsprenumeration upphör att gälla?
Om din utvärderingsprenumeration går ut förlorar åtkomst till innehåll som har skyddats med din utvärderingsprenumeration för Azure RMS. Om du sedan köpa en prenumeration som har stöd för Azure RMS, återställs automatiskt åtkomst.

Ett undantag till att förlora åtkomst vid utgången är om din organisation används Azure RMS med RMS för individer prenumerationen innan du har köpt utvärderingsprenumeration. Sedan åtkomst till tidigare skyddade innehållet förblir, även när utvärderingsprenumeration upphör att gälla.

### Enterprise Mobility Suite prenumeration
[Kostnadsfri 30-dagars utvärderingsversion](http://go.microsoft.com/fwlink/?LinkId=615385)

Den här prenumerationen är utformat för företag som vill använda en kombination av Azure Active Directory Premium, Windows Intune och Azure Rights Management. Mer information finns i [Översikt över Microsoft Enterprise Mobility](http://go.microsoft.com/fwlink/?LinkId=615386).

|Alternativet licensiering|Office 365 Business Essentials|Office 365 Business Premium|Office 365 Enterprise E1<br /><br />Office 365 utbildning A1|Office 365 Enterprise E3<br /><br />Office 365 utbildning A3<br /><br />Office 365 statlig G3|Office 365 Enterprise E4<br /><br />Office 365 utbildning A4<br /><br />Office 365 statlig G4|Office 365 Enterprise K1|SharePoint-Plan 1<br />SharePoint Plan 2|Exchange Online Plan 1<br />Exchange Online Plan 2|
|-----------------------------|----------------------------------|-------------------------------|--------------------------------------------------------|---------------------------------------------------------------------------------|---------------------------------------------------------------------------------|----------------------------|----------------------------------------|--------------------------------------------------|
|Informationsskydd rättigheter (IRM)|Ja|Yes <sup>1</sup>|Ja|Ja|Ja|Ja|Ja|Ja|
<sup>1</sup> för Business Premium och det finns vissa begränsningar för klienten: Du kan skydda innehåll och använder skyddat innehåll med RMS genom att använda Outlook Web App och RMS-delningsappen. Du kan använda skyddat innehåll med hjälp av alla andra Office-program som innehåller Office Online och klientprogrammen för Office 365 Business Premium.

### RMS för individer prenumeration
Den här prenumerationen är utformat för personer i organisationen som inte har distribuerats Azure RMS eller AD RMS. Den kan dessa användare läsa innehåll som har skyddats av en organisation som använder Azure RMS och de kan även skydda sin egen innehåll.

Mer information finns i [RMS för personer och Azure Rights Management](../Topic/RMS_for_Individuals_and_Azure_Rights_Management.md).

## <a name="BKMK_AzureADTenant"></a>Azure AD-katalog
Du måste ha en Azure AD-katalog som använder Azure RMS. Du kan använda din organisation kontot för den här katalogen för att logga in på Azure Management Portal, om t.ex, du kan konfigurera och hantera Rights Management mallar.

Om du inte redan har en Azure-prenumeration för din organisation kan du skaffa ett genom att registrera dig för en kostnadsfri utvärderingsversion.: Gå till den [Azure få igång](https://account.windowsazure.com/organization) sidan och följ instruktionerna.

Mer information finns i dokumentationen för Azure Active Directory följande resurser:

-   [Vad är en Azure AD-katalog?](http://msdn.microsoft.com/en-us/library/185da266-58a9-43e6-9c66-2c8f702545c6)

-   [Hur Azure-prenumerationer som är kopplade till Azure AD](http://msdn.microsoft.com/en-us/library/edf05c2e-944a-4da5-a330-dc9dc479f127)

Om du vill integrera din Azure AD-katalog med din lokala AD-skogar finns [katalogintegrering](http://msdn.microsoft.com/en-us/library/bf82bdff-2467-403b-8c1a-0e9eebcf31e8).

> [!NOTE]
> Om du har mobila enheter eller Mac-datorer som autentiseras lokalt med hjälp av AD FS eller en motsvarande autentiseringsprovider:
> 
> -   Du måste använda AD FS på den lägsta versionen av **Windows Server 2012 R2**, eller en alternativ autentiseringsprovider som stöder OAuth 2.0-protokoll.

### <a name="BKMK_MFA"></a>Multifaktorautentisering (MFA) och Azure RMS
Om du vill använda Multi-Factor kräver authentication (MFA) med Azure RMS minst en av följande:

-   Office 2013 (minst version):

    -   Om du har Office 2013, måste du även installera den [9 juni 2015 uppdatering för Office 2013 (KB3054853)](https://support.microsoft.com/kb/3054853). Uppdatera och hur modern autentisering blåser Active Directory Authentication Library ADAL-baserade tecken Office 2013, finns mer information om detta [Office 2013 modern autentisering public preview meddelade](https://blogs.office.com/2015/03/23/office-2013-modern-authentication-public-preview-announced/)  i Office-blogg.

-   Rights Management sharing application för Windows:

    -   Du måste ha installerat den lägsta versionen av 1.0.1908.0, vilket kan anges med hjälp av Kontrollpanelen, program och funktioner. Mer information om delningsprogrammet finns  [Delningsapplikation för Windows Rights Management](../Topic/Rights_Management_Sharing_Application_for_Windows.md).

-   Rights Management-delningsapp för mobila enheter och Mac-datorer:

    -   Kontrollera att du har den senaste installerade versionen. Stöd för MFA försattes i September 2015 version av RMS-delningsappen.

Konfigurera sedan MFA lösningen:

-   För Microsoft hanterar klienter (du har Azure Active Directory eller Office 365):

    -   Konfigurera Azure MFA för att använda Multifaktorautentisering för användare. Instruktioner finns i [komma igång med Azure Multi-Factor Authentication i molnet](https://azure.microsoft.com/documentation/articles/multi-factor-authentication-get-started-cloud/) från Azure-dokumentationen.

        Mer information om Azure MFA finns [Vad är Azure Multi-Factor Authentication?](https://azure.microsoft.com/documentation/articles/multi-factor-authentication/)

-   För federerad klienter (du använder federation servrar lokalt):

    -   Konfigurera dina federationsservrar för Azure Active Directory eller Office 365. Till exempel om du använder AD FS finns [Konfigurera ytterligare autentiseringsmetoder för AD FS](https://technet.microsoft.com/library/dn758113.aspx) på TechNet.

        Mer information om det här scenariot finns  [av arbetar med Office 365-identitet programmet nu effektiviserade](https://blogs.office.com/2014/01/30/the-works-with-office-365-identity-program-now-streamlined/) i Office-blogg.

## <a name="BKMK_SupportedDevices"></a>Klientenheter som stöd för Azure RMS
Använd följande avsnitt för att identifiera vilka enheter som stöder Azure Rights Management (RMS) och vilka RMS-funktioner stöder:

-   [Datorer](../Topic/Requirements_for_Azure_Rights_Management.md#BKMK_RMSSupportedComputers)

-   [Mobila enheter](../Topic/Requirements_for_Azure_Rights_Management.md#BKMK_RMSSupportedMobileDevices)

-   [Klienten enhetsfunktioner](../Topic/Requirements_for_Azure_Rights_Management.md#BKMK_ClientCapabilities)

### <a name="BKMK_RMSSupportedComputers"></a>Datorer
Azure Rights Management stöd för följande operativsystem:

-   **Windows 7** (x 86, x 64)

-   **Windows 8** (x 86, x 64)

-   **Windows 8.1** (x 86, x 64)

-   **Windows 10** (x 86, x 64)

-   **Mac OS X**: Lägsta version av Mac OS X 10,8 (Mountain Lion)

### <a name="BKMK_RMSSupportedMobileDevices"></a>Mobila enheter
Följande operativsystem för mobila enheter stöder Azure Rights Management:

-   **Windows Phone**: Windows Phone 8.1

-   **Android-Telefoner och surfplattor**: Lägsta version av Android 4.0.3 eller en nyare

-   **iPhone och iPad**: Lägsta versionen av iOS 7.0

-   **Windows RT surfplattor**: Windows 8 RT, Windows 8.1 RT

### <a name="BKMK_ClientCapabilities"></a>Klienten enhetsfunktioner
Inte alla klientenheter som stöds stöder för närvarande alla funktioner för RMS. Använd följande tabell för att identifiera vilka program som stöder RMS-funktioner och undantag.

Om inget annat anges gäller vilka funktioner som stöds både Azure RMS och AD RMS. Dessutom kräver AD RMS-stöd på iOS, Android, OS X och Windows Phone 8.1 [Active Directory Rights Management Services mobila enhet tillägget](http://technet.microsoft.com/library/a69ead9d-7dd3-4b38-9830-4728e9757341).

Information om tabellkolumnerna:

-   **Skyddad PDF**: Filer som har filnamnstillägget .ppdf och som skapas automatiskt när du använder RMS-delningsprogrammet för att dela Office-filer och PDF-filer via e-post. RMS-delningsprogrammet innehåller en läsare för skyddade PDF-filer. Tidigare, om du har skapat PDF-filer som du skyddat med Azure RMS eller AD RMS kan du fortsätta att läsa de här filerna på Windows, iOS och Android-enheter med hjälp av Foxit läsare och Nitro Pro.

-   **E-post:** De e-postklienter som visas kan skydda e-postmeddelandet, som automatiskt ska skydda eventuella bifogade filer. I det här scenariot kan funktionen för förhandsgranskning av klientens visa skyddat innehåll (meddelandet och bifogade filer) till behörig mottagare. Om ett e-postmeddelande själva inte är skyddad, men den bifogade filen är skyddad, kan inte klientens preview-funktionen Visa skyddade bilagan till behörig mottagare.

-   **Andra filtyper**: Text-och bildfiler innehåller filer som har ett filnamnstillägg som txt, XML, JPG, JPEG-och. Dessa filer ändra deras filnamnstillägget när de skyddas internt av RMS och blir skrivskyddade. Filer som inte kan skyddas internt har filnamnstillägget .pfile när de allmänt skydd av RMS. Mer information finns i [skyddsnivåer – interna och allmänna](https://technet.microsoft.com/library/dn339003.aspx) och [stöds filtyper och filnamnstillägg](https://technet.microsoft.com/library/dn339003.aspx) avsnitt från den [Rights Management administratörsguiden för delningsapplikationen](http://technet.microsoft.com/library/dn339003%28v=ws.10%29.aspx).

|**Enhetens operativsystem**|Word, Excel, PowerPoint|Skyddad PDF-fil|E-post|Andra filtyper|
|-------------------------------|---------------------------|-------------------|----------|------------------|
|**Windows**|Office 2010<br /><br />Office 2013<br /><br />Mobila Office appar (endast Azure RMS)<sup>1</sup><br /><br />Office Online<sup>2</sup>|Gaaiho dokument<br /><br />GigaTrust Desktop PDF-klienten för Adobe<br /><br />Foxit läsare<br /><br />Nitro PDF-läsare<br /><br />RMS-delningsprogrammet tidigare|Outlook 2010<br /><br />Outlook 2013<br /><br />Outlook Web App (OWA)<br /><br />Windows Mail<sup>3</sup>|RMS-delningsprogrammet för Windows: Text, bilder pfile<br /><br />Siemens JT2Go: JT-filer (endast Windows 10)|
|**iOS**|Office för iPad och iPhone<sup>4</sup><br /><br />Office Online<sup>2</sup><br /><br />TITUS dokument|Foxit läsare<br /><br />RMS-delningsappen<sup>1</sup><br /><br />TITUS dokument|NitroDesk<br /><br />Outlook för iPad och iPhone<sup>3</sup><br /><br />OWA för iOS<br /><br />Skydda öar IQProtector<sup>1</sup><br /><br />TITUS e-post|RMS-delningsappen<sup>1</sup>: Text, bilder pfile<br /><br />TITUS dokument: Pfile|
|**Android**|GigaTrust App för Android<br /><br />Office Online<sup>2</sup>|GigaTrust App för Android<br /><br />Foxit läsare<br /><br />RMS-delningsappen<sup>1</sup>|9Folders<br /><br />GigaTrust App för Android<br /><br />NitroDesk<br /><br />OWA för Android<sup>5</sup><br /><br />Samsung e-post (S3 och senare)<br /><br />Skydda öar IQProtector<sup>1</sup><br /><br />TITUS klassificering för mobila enheter|RMS-delningsappen<sup>1</sup>: Text, bilder pfile|
|**OS X**|Office 2011 (endast AD RMS)<br /><br />2016 Office för Mac<br /><br />Office Online<sup>2</sup>|Foxit läsare<br /><br />RMS-delningsappen<sup>1</sup>|Outlook 2011 (endast AD RMS)<br /><br />Outlook 2016 för Mac<br /><br />Outlook för Mac|RMS-delningsappen<sup>1</sup>: Text, bilder pfile|
|**Windows RT**|Office 2013 RT<br /><br />Office Online<sup>2</sup>|Stöds inte|Outlook 2013 RT<br /><br />E-postprogrammet för Windows<br /><br />Windows Mail<sup>3</sup>|Siemens JT2Go: JT-filer|
|**Windows Phone 8.1**|Office Mobile (endast AD RMS)|RMS-delningsappen<sup>1</sup>|Outlook Mobile|RMS-delningsappen<sup>1</sup>: Text, bilder pfile|
|**BlackBerry 10**|Stöds inte|Stöds inte|E-post BlackBerry<sup>3</sup>|Stöds inte|
<sup>1</sup> kan du visa skyddat innehåll.

<sup>2</sup> har stöd för att visa skyddat innehåll i SharePoint Online, OneDrive för företag och Outlook Web Access.

<sup>3</sup> använder Exchange ActiveSync IRM, som måste aktiveras av Exchange-administratören. Användare kan visa, svara och svara alla för skyddade e-postmeddelanden, men användarna inte kan skydda e-post sig själva.

<sup>4</sup> har stöd för att visa och redigera skyddade dokument. Mer information finns i följande post i Office-blogg: [Azure Rights Management-support kommer att Office för iPad och iPhone](https://blogs.office.com/2015/07/22/azure-rights-management-support-comes-to-office-for-ipad-and-iphone-2/)

<sup>5</sup> mer information finns i följande post i Office-blogg: [OWA för Android är nu tillgängligt på enheter som väljer](http://blogs.office.com/2014/06/11/owa-for-android-now-available-on-select-devices/)

> [!TIP]
> Mer information om kommande RMS-stöd i Office för olika plattformar, finns i följande post från Office-blogg: [Office överallt, kryptering överallt](http://blogs.office.com/2015/02/18/office-everywhere-encryption-everywhere/)

## <a name="BKMK_SupportedApplications"></a>Program som stöder Azure RMS
Följande program har inbyggt stöd för Azure RMS, vilket innebär att RMS nära integrerad i programmen med RMS APIs för att stödja restriktioner för användning. Dessa program kallas även som RMS-upplysta:

-   **Microsoft Office-program** (Word, Excel, PowerPoint och Outlook) från följande paket kan skydda innehåll med hjälp av Azure RMS:

    -   Office 365 ProPlus

    -   Office 365 Enterprise E3

    -   Office 365 Enterprise E4

    -   Office Professional Plus 2016

    -   Office Professional Plus 2013

    -   Office Professional Plus 2010

    Andra versioner av Office (med undantag av Office 2007) kan använda skyddat innehåll.

    > [!NOTE]
    > Azure RMS med Office Professional Plus 2010 eller Office Professional 2010:
    > 
    > -   Kräver Rights Management sharing application för Windows
    > -   Stöds inte i Windows 10

-   **Rights Management sharing application för Windows**

    Mer information om delningsapplikationen för Rights Management för Windows finns i följande resurser:

    -   [Rights Management dela program administratörshandboken](http://technet.microsoft.com/library/dn339003.aspx)

    -   [Rights Management delning användaren guide till](http://technet.microsoft.com/library/dn339006.aspx)

-   **Rights Management sharing application för mobila plattformar**

    Mer information om delningsapplikationen för Rights Management för mobila plattformar finns i följande resurser:

    -   Hämta relevanta appen med hjälp av länkarna på [Microsoft Rights Management sidan](http://go.microsoft.com/fwlink/?LinkId=303970)

    -   Om du hanterar mobila enheter med Microsoft Intune kan du distribuera och konfigurera appen på [iOS och Android-enheter som en princip för hanterad app](https://technet.microsoft.com/library/dn878026.aspx).

    -   [Vanliga frågor och svar för Delningsapplikationen för mobila plattformar för Microsoft Rights Management](http://technet.microsoft.com/dn451248)

-   **Andra program som stöder RMS APIs**:

    -   Line-of-business-program som har skrivits internt med hjälp av RMS SDK

    -   Program från leverantörer som är skrivna med hjälp av RMS SDK

    Mer information om SDK finns på [Microsoft Rights Management SDK](http://msdn.microsoft.com/library/hh552972%28v=vs.85%29.aspx).

> [!IMPORTANT]
> Följande program stöds inte av Azure RMS:
> 
> -   Microsoft Office för Mac 2011
> -   Microsoft OneDrive för företag för SharePoint Server 2013
> -   Visningsprogrammet
> 
> Dessutom har RMS-delningsprogrammet följande begränsningar:
> 
> -   För Windows-datorer: Kräver en lägsta version av Windows 7 Service Pack 1

Mer information om hur dessa program stöder Azure RMS finns [Hur program stöd för Azure Rights Management](../Topic/How_Applications_Support_Azure_Rights_Management.md).

Information om hur du konfigurerar dem finns [Konfigurera program för Azure Rights Management](../Topic/Configuring_Applications_for_Azure_Rights_Management.md).

## <a name="BKMK_SupportedServers"></a>Lokala servrar som stöder Azure RMS
Följande lokala serverprodukterna stöds med Azure RMS när du använder Azure RMS-anslutningen, som fungerar som ett kommunikationsgränssnitt (ett relay) mellan lokala servrar och Azure RMS. Dessutom kan krävs den här konfigurationen att du konfigurerar katalogsynkronisering mellan din Active Directory-skogar och Azure Active Directory.

-   **Exchange Server**:

    -   Exchange Server 2013

    -   Exchange Server 2010

-   **Office SharePoint Server**:

    -   Office SharePoint Server 2013

    -   Office SharePoint Server 2010

-   **Filservrar som kör Windows Server och använda filen klassificering infrastruktur (FCI)**:

    -   Windows Server 2012 R2

    -   Windows Server 2012

    > [!NOTE]
    > Eftersom filen servrar som kör Windows Server 2008 R2 inte har en inbyggd filen management uppgiftsåtgärd att tillämpa RMS-skydd kan använda du inte RMS-kopplingen för det här scenariot. Du kan dock använda filen klassificering infrastruktur och Azure RMS i dessa operativsystem om du konfigurerar en anpassad filhanteringsaktivitet för att köra en körbar fil eller skript som kan skydda filer med hjälp av Azure RMS. Till exempel en Windows PowerShell-skript som använder den [RMS-skydd cmdlets](https://msdn.microsoft.com/library/azure/mt433195.aspx).
    > 
    > Du kan också använda dessa cmdlets med servrar som kör senare versioner av Windows Server med fördelen att dessa cmdlets kan skydda alla filtyper. RMS-kopplingen skyddar Office-filer. Instruktioner, se [RMS-skydd med infrastrukturen i Windows Server-filen klassificering &#40;FCI&#41;](../Topic/RMS_Protection_with_Windows_Server_File_Classification_Infrastructure__FCI_.md).

RMS-anslutningen stöds på Windows Server 2012 R2, Windows Server 2012 och Windows Server 2008 R2.

Mer information om hur du konfigurerar RMS-koppling för de lokala servrarna finns [Distribuera Azure Rights Management-koppling](../Topic/Deploying_the_Azure_Rights_Management_Connector.md).

## Se även
[Kom igång med Azure Rights Management](../Topic/Getting_Started_with_Azure_Rights_Management.md)

