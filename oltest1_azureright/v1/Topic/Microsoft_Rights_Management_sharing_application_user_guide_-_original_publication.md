---
description: na
keywords: na
title: Microsoft Rights Management sharing application user guide - original publication
search: na
ms.date: na
ms.tgt_pltfrm: na
ms.assetid: 350b6869-084d-4e8a-a4d3-df44a40fa13b
robots: noindex,nofollow
---
# Anv&#228;ndarhandbok f&#246;r delningsapplikationen f&#246;r Microsoft Rights Management –  ursprunglig publikation
Användarhandboken för delningsapplikationen för Microsoft Rights Management för Windows innehåller följande avsnitt:

-   [Evaluating and Installing Microsoft Rights Management sharing application](../Topic/Microsoft_Rights_Management_sharing_application_user_guide_-_original_publication.md#BKMK_Eval)

-   [Using Microsoft Rights Management sharing application](../Topic/Microsoft_Rights_Management_sharing_application_user_guide_-_original_publication.md#BKMK_UsingMSRMSApp)

-   [Using User-Authored Permissions and Sharing Protected Content](../Topic/Microsoft_Rights_Management_sharing_application_user_guide_-_original_publication.md#BKMK_Custom)

-   [Using the Office Toolbar Add-in](../Topic/Microsoft_Rights_Management_sharing_application_user_guide_-_original_publication.md#BKMK_OfficeToolbar)

-   [Administrator’s guidance for Microsoft Rights Management sharing application](../Topic/Microsoft_Rights_Management_sharing_application_user_guide_-_original_publication.md#BKMK_AdminGuide)

Vanliga frågor och svar samt felsökningsinformation finns i [FAQ for Microsoft Rights Management Sharing Application for Windows](http://go.microsoft.com/fwlink/?LinkId=303971).

## <a name="BKMK_Eval"></a>Utvärdera och installera delningsapplikationen för Microsoft Rights Management
I det här avsnittet beskrivs vad delningsapplikationen för Microsoft Rights Management är och hur du installerar det:

-   [What is the Microsoft Rights Management sharing application?](../Topic/Microsoft_Rights_Management_sharing_application_user_guide_-_original_publication.md#BKMK_WhatIs)

-   [Requirements for Microsoft Rights Management sharing application](../Topic/Microsoft_Rights_Management_sharing_application_user_guide_-_original_publication.md#BKMK_Reqs)

-   [Installing the Microsoft Rights Management sharing application](../Topic/Microsoft_Rights_Management_sharing_application_user_guide_-_original_publication.md#BKMK_Install)

### <a name="BKMK_WhatIs"></a>Vad är delningsapplikationen för Microsoft Rights Management?
Delningsapplikationen för Microsoft Rights Management är ett valfritt hämtningsbart program för Microsoft Windows. Det innehåller följande:

-   Utökar funktionerna i Utforskaren så att du kan skydda en enda fil eller masskydda flera filer, samt alla filer i en vald mapp.

-   Lägger till stöd för skydd av alla filtyper och ett inbyggt visningsprogram för vanliga text- och bildfiler.

-   Lägger till nya knappar i Microsoft Office-verktygsfältet för Word, PowerPoint och Excel.

### <a name="BKMK_Reqs"></a>Krav för delningsapplikationen för Microsoft Rights Management
För att kunna använda delningsapplikationen för Microsoft Rights Management måste din dator köra Windows 8.1, Windows 8 eller Windows 7.

Delningsapplikationen för Microsoft Rights Management kräver AD RMS Client 2.1, vilket installeras som en del av installationspaketet. Delningsapplikationen för Microsoft Rights Management fungerar endast med den här versionen av AD RMS-klienten.

### <a name="BKMK_Install"></a>Installera delningsapplikationen för Microsoft Rights Management
Om du vill installera delningsapplikationen för Microsoft Rights Management gör du följande:

1.  Gå till sidan [Microsoft Rights Management](http://go.microsoft.com/fwlink/?LinkId=303970) på Microsofts webbplats.

2.  Klicka på ikonen för **RMS-program för Windows** i avdelningen **Datorer** och spara installationspaketet för delningsapplikationen Microsoft Rights Managements på din dator.

3.  Dubbelklicka på den hämtade komprimerade filen och dubbelklicka sedan på **setup.exe**. Klicka på **Ja** om du ser en uppmaning.

4.  På sidan **Setup Microsoft RMS** klickar du på **Nästa** och väntar på att installationen ska slutföras.

5.  När installationen är klar klickar du på **Starta om** för att starta om din dator och slutföra installationen. Eller klicka på **Stäng** och starta om din dator senare för att slutföra installationen.

## <a name="BKMK_UsingMSRMSApp"></a>Använda delningsapplikationen för Microsoft Rights Management
I det här avsnittet beskrivs olika sätt att använda delningsapplikationen för Microsoft Rights Management:

-   [Creating a protected text (.ptxt) file](../Topic/Microsoft_Rights_Management_sharing_application_user_guide_-_original_publication.md#BKMK_CreatePTXT)

-   [Viewing a protected text (.ptxt) or a protected image file](../Topic/Microsoft_Rights_Management_sharing_application_user_guide_-_original_publication.md#BKMK_ViewPTXT)

-   [Creating a generic protected (.pfile) file](../Topic/Microsoft_Rights_Management_sharing_application_user_guide_-_original_publication.md#BKMK_CreatePFILE)

-   [Viewing a generic protected (.pfile) file](../Topic/Microsoft_Rights_Management_sharing_application_user_guide_-_original_publication.md#BKMK_ViewPFILE)

-   [Removing protection from a file](../Topic/Microsoft_Rights_Management_sharing_application_user_guide_-_original_publication.md#BKMK_Unprotect)

### <a name="BKMK_CreatePTXT"></a>Skapa en skyddad textfil (.ptxt)
Delningsapplikationen för Microsoft Rights Management kan användas för att omvandla en vanlig textfil (.txt) till en skyddad fil(.ptxt).

##### Skapa en skyddad textfil (.ptxt)

1.  I Utforskaren högerklickar du i en mapp, pekar på **Nytt** och klickar sedan på **Textdokument**.

2.  Byt namn på filen (till exempel Test.txt).

3.  Dubbelklicka på filen för att öppna den i Anteckningar.

4.  Lägg till några rader text i filen i Anteckningar, som exempelvis nedan, och spara den.

    ```
    This is a sample text file.
    This is a sample text file.
    This is a sample text file.
    This is a sample text file. 
    This is a sample text file.
    This is a sample text file.
    ```

5.  Högerklicka på filen, peka på **Skydda på plats** och välj en mall i listan. (Observera att om detta är första gången du har använt verktyget måste du välja **Företagsskydd** för att påbörja hämtningen av din organisations mallar.)

6.  På skärmbilden **Delningsapplikation för Microsoft Rights Management** bekräftar du vilken princip du vill använda, klickar på **Tillämpa** och när filen är skyddad klickar du på **Stäng**.

### <a name="BKMK_ViewPTXT"></a>Visa en skyddad textfil (.ptxt) eller en skyddad bildfil
Om du vill visa en skyddad textfil dubbelklickar du på filen (till exempel Test.ptxt) i Utforskaren. Du kan uppmanas att godkänna att programmet ska erhålla rättigheter. Skyddsprincipen visas överst i filen.

Skyddade bilder kan öppnas och visas på samma sätt.

### <a name="BKMK_CreatePFILE"></a>Skapa en fil med allmänt skydd (.pfile)
Det allmänna skyddsformatet för filer (.pfile) kan användas för att ge ett allmänt skydd för filtyper som inte direkt stöds av delningsapplikationen för Microsoft Rights Management eller andra program som innehåller ett inbyggt RMS-skydd.

Det allmänna skyddsformatet för filer kan till exempel skydda .vsd filer från Microsoft Visio (som för närvarande inte stöder inbyggt skydd).

> [!NOTE]
> Filer som använder allmänt skydd skyddas endast för autentisering. En användare som har behörighet att använda en skyddad fil (.pfile) autentiseras och användarens rättigheter och behörigheter visas, men kan inte tillämpas när filen har öppnats i sitt ursprungliga format (till exempel när .vsd-filen har öppnats i Visio). En användare som inte har behörighet eller inte kan autentiseras kommer inte att kunna öppna den skyddade filen.

##### Om du vill skapa ett allmänt skyddad fil (.pfile) från en Visio-ritningsfil (.vsd)

1.  I Utforskaren högerklickar du i en mapp, pekar på **Nytt** och klickar sedan på **Nytt Visio-dokument**.

2.  Byt namn på filen (till exempel Prov.vsd).

3.  Dubbelklicka på filen för att öppna den i Visio.

4.  I Visio lägger du till element i ritningen och sparar och stänger sedan filen.

5.  Högerklicka på filen, peka på **Skydda på plats** och välj en principmall i listan. (Observera att om detta är första gången du har använt verktyget måste du välja **Företagsskydd** för att påbörja hämtningen av din organisations mallar.)

6.  På skärmbilden **Delningsapplikation för Microsoft Rights Management** markerar du den princip du vill tillämpa och klickar sedan på **Tillämpa**.

7.  Ett meddelande visas om att en skyddad fil har sparats som Test.vsd.pfile (originalfilen tas bort).

### <a name="BKMK_ViewPFILE"></a>Visa en fil (.pfile) med allmänt skydd
För att visa en fil med allmänt skydd (.pfile) dubbelklickar du på den (till exempel Test.vsd.pfile) i Utforskaren och klickar på **Öppna**.

### <a name="BKMK_Unprotect"></a>Ta bort skyddet från en fil
Delningsapplikationen för Microsoft Rights Management ger dig möjlighet att ta bort skyddet från filer som du tidigare har skyddat.

Om du vill ta bort skyddet från en fil du tidigare har skyddat använder du alternativet **Ta bort skydd** enligt följande:

1.  Högerklicka på **Test.ptxt**, peka på **Skydda på plats** och klicka på **Ta bort skydd**. Du kan uppmanas att godkänna att programmet ska erhålla rättigheter.

2.  Test.ptxt kommer att tas bort och ersättas av Test.txt.

## <a name="BKMK_Custom"></a>Använda användarskapade behörigheter och dela skyddat innehåll
I det här avsnittet beskrivs hur du skyddar och använder en fil med användarskapade behörigheter, hur du delar skyddat innehåll och hur du skyddar flera filer:

-   [Protecting a file with user-authored permissions](../Topic/Microsoft_Rights_Management_sharing_application_user_guide_-_original_publication.md#BKMK_ProtectCustom)

-   [Consuming files that have user-authored protection](../Topic/Microsoft_Rights_Management_sharing_application_user_guide_-_original_publication.md#BKMK_UserDefined)

-   [Sharing protected content](../Topic/Microsoft_Rights_Management_sharing_application_user_guide_-_original_publication.md#BKMK_ShareProtected)

-   [Using keyboard shortcuts](../Topic/Microsoft_Rights_Management_sharing_application_user_guide_-_original_publication.md#BKMK_AccessKeys)

-   [Applying protection to multiple files and folders](../Topic/Microsoft_Rights_Management_sharing_application_user_guide_-_original_publication.md#BKMK_Multiple)

### <a name="BKMK_ProtectCustom"></a>Skydda en fil med användarskapade behörigheter
Användarskapat skydd kan användas för att uppnå följande:

-   För att begränsa filåtkomsten så att den bara omfattar en viss lista med enskilda användare som identifieras av sina e-postadresser.

-   För att begränsa användningen av filen till endast specifika rättigheter, till exempel läsrättigheter till ett dokument.

För att skydda en fil med användarskapade behörigheter högerklickar du på filen, klickar på **Skydda på plats** och klickar sedan på **Anpassade behörigheter**. Följande skärm startas:

![](../Image/ADRMS_MSRMSApp_ProtectCustom.gif)

Skriv in e-postadresserna till användarna i listan och använd skjutreglaget för att välja behörigheter till filen. Klicka sedan på **Använd**.

### <a name="BKMK_UserDefined"></a>Använda filer som har användarskapat skydd
De flesta skyddade filer som hanteras av delningsapplikationen för Microsoft Rights Management kommer att ha skyddats med mallbaserade skyddsnivåer. Delningsapplikationen för Microsoft Rights Management har dock också stöd för filer som har fått en användarskapad skyddsnivå.

Användarskapat skydd kan användas för att uppnå följande typer av skydd för en fil:

-   För att begränsa filåtkomsten så att den bara omfattar en mycket specifik lista med enskilda användare som identifieras av sina e-postadresser.

-   För att begränsa användningen av filen till endast en specifik rättighet, till exempel att bara kunna skriva ut ett dokument.

För text- och bildfilformat kräver den här skyddsnivån att alla program du använder för att redigera, spara eller begränsa text- eller bildfilerna ska ha stöd för RMS-skydd och att de implementerat skydds-API:erna som finns i AD RMS SDK.

När du visar en skyddad textfil som har användarskapat skydd, ser du en viss skillnad i hur behörigheterna för filen visas, enligt följande exempel.

För filer som skyddas med hjälp av filformatet för allmänt skydd (.pfile), visas särskilda rättigheter eller behörigheter från användaren på bekräftelseskärmen i stället för namnet på den mall som användes för att skydda filen, vilket visas i följande bild.

![](../Image/ADRMS_MSRMSApp_SP_ConsumePfile.gif)

### <a name="BKMK_ShareProtected"></a>Dela skyddat innehåll
Om du vill skydda och dela innehåll högerklickar du på filen och klickar på **Dela skyddat**. Följande skärm startas:

![](../Image/ADRMS_MSRMSAPP_SP_ShareProtected.gif)

Skriv in e-postadresserna till användarna i listan och använd skjutreglaget för att välja behörigheter till filen. Klicka sedan på **Skicka**. Programmet startar Outlook och öppnar ett nytt e-postmeddelande som har den skyddade filen bifogad. Den ursprungliga filen är inte skyddad.

Om du vill att användarna ska kunna visa skyddade filer på enheter med andra operativsystem än Windows, klickar du på **Tillåt användning på alla enheter**. Användarna måste [hämta delningsapplikationen för Microsoft Rights Management](http://go.microsoft.com/fwlink/?LinkId=303970) till sin enhet.

### <a name="BKMK_AccessKeys"></a>Användning av kortkommandon
Tryck på **Alt**-tangenten för att se tillgängliga snabbtangenter. Tryck på **Alt** + snabbtangenten för att välja ett alternativ. I dialogrutan **Dela skyddat** kan du t.ex. trycka på **Alt** för att se snabbtangenterna och sedan trycka på **Alt + u** för att välja **Användarna måste logga in varje gång de öppnar den här filen**.

![](../Image/ADRMS_MSRMSApp_AccessKeys.png)

### <a name="BKMK_Multiple"></a>Använda skydd på flera filer och mappar
Delningsapplikationen för Microsoft Rights Management kan också användas för att tillämpa skydd på mer än en fil, t.ex. genom att markera flera filer eller en mapp som innehåller oskyddade filer i Utforskaren.

##### Så här skyddar du flera eller alla filer i en angiven mapp

1.  Markera flera filer i Utforskaren, eller välj en mapp som innehåller flera filer som ska skyddas.

2.  Högerklicka på den valda mappen eller filerna, klicka på **Skydda på plats** och välj en mall i listan. (Observera att om detta är första gången du har använt verktyget måste du välja **Företagsskydd** för att påbörja hämtningen av din organisations mallar.)

3.  På skärmbilden **Delningsapplikation för Microsoft Rights Management** bekräftar du att filerna har skyddats.

Om något fel inträffar kan du läsa mer i [FAQ for Microsoft Rights Management Sharing Application for Windows](http://go.microsoft.com/fwlink/?LinkId=303971).

## <a name="BKMK_OfficeToolbar"></a>Använda tillägget för Office-verktygsfältet
Du kan skydda och dela filer som finns i Word, PowerPoint och Excel direkt från Microsoft Office med tillägget för menyfliksområdet i Office för delningsapplikationen för Microsoft Rights Management. Klicka på **Dela skyddat** i menyfliksområdet för att starta delningsapplikationen för Microsoft Rights Management.

![](../Image/ADRMS_MSRMSApp_SP_OfficeToolbar.png)

## <a name="BKMK_AdminGuide"></a>Administratörens handbok för delningsapplikationen för Microsoft Rights Management
Administratörens handbok för delningsapplikationen för Microsoft Rights Management innehåller följande avsnitt:

-   [Microsoft Rights Management sharing application Technical Overview](../Topic/Microsoft_Rights_Management_sharing_application_user_guide_-_original_publication.md#BKMK_AdminOverview)

-   [Supported File Types](../Topic/Microsoft_Rights_Management_sharing_application_user_guide_-_original_publication.md#BKMK_SupportFileTypes)

-   [Automatic deployment for the Microsoft Rights Management sharing application](../Topic/Microsoft_Rights_Management_sharing_application_user_guide_-_original_publication.md#BKMK_ScriptedInstall)

### <a name="BKMK_AdminOverview"></a>Teknisk översikt för delningsapplikationen för Microsoft Rights Management
Delningsapplikation för Microsoft Rights Management är ett valfritt hämtningsbart program för Microsoft Windows och andra plattformar. Det innehåller följande:

-   Skydd för enskilda eller flera filer, eller skydd för alla filer i en specifik mapp.

-   Fullständigt stöd för skydd av alla filtyper och inbyggt visningsprogram för vanliga text- och bildfiler.

-   Allmänt skydd för filer som inte stöder RMS-skydd.

-   Fungerar helt och hållet tillsammans med filer som skyddas med IRM (Office Information Rights Management)

-   Fungerar helt och hållet med PDF-filer som skyddas med SharePoint, FCI och andra PDF-redigeringsverktyg som stöds

Delningsapplikationen för Microsoft Rights Management använder den nya [AD RMS Client 2.1-körningen](http://www.microsoft.com/download/details.aspx?id=38396). Den ger användare möjlighet att skydda innehåll med hjälp av fördefinierade eller användardefinierade mallar som du kan anpassa och distribuera till din organisation. Genom att använda funktionerna i AD RMS 2.1 kan RMS-delningsprogrammet tillhandahålla en enkel lösning för att skydda och använda filer.

Med den version av Windows Azure AD RMS som lanserades i oktober 2013 kan du internt skydda dokument med Office 2010 och skicka dem till användare i ett annat företag som sedan kan använda dem med hjälp av Windows Azure AD RMS. Dessutom kan du med den här versionen, om du använder AD RMS i kryptografiskt läge 2, använda RMS för enskilda användare och använda innehåll från personer i ett annat företag som använder Windows Azure AD RMS. Mer information om kryptografiskt läge 2 finns i [AD RMS Cryptographic Modes](http://technet.microsoft.com/library/hh867439%28v=ws.10%29.aspx).

Om du vill hämta delningsapplikationen för Microsoft Rights Management gör du följande:

1.  Logga in på [Microsoft Connect](http://connect.microsoft.com/) med ditt Microsoft-konto (kallades tidigare Live ID).

2.  På sidan **Start** söker du efter **Rights Management Services** och ansluter till gruppen.

3.  Klicka på **Hämtningsbara filer** och sedan på **Delningsapplikation för Microsoft Rights Management**.

4.  På sidan **Hämtningsinformation** väljer du **Microsoft Rights Management sharing application.zip** och klickar på **Hämta**.

5.  Om det behövs installerar du Microsoft File Transfer Manager och följer instruktionerna för att hämta delningsapplikationen för Microsoft Rights Management.

#### Skyddsnivåer som stöds av delningsapplikationen för Microsoft Rights Management
Delningsapplikationen för Microsoft Rights Management stöder skydd på två olika nivåer som beskrivs i följande tabell.

||||
|-|-|-|
|Typ av skydd|Intern|Allmän|
|Beskrivning|För text-, bild-, Microsoft Office- (Word, Excel-, PowerPoint-) filer, PDF-filer och andra filtyper för program som har stöd för AD RMS, innehåller det interna skyddet en stark skyddsnivå som innehåller både kryptering och tillämpning av rättigheter (behörigheter).|För alla andra program och filtyper ger det allmänna skyddet ett skydd som innehåller både filinkapsling med filtypen PFILE och autentisering för att verifiera att en användare har behörighet att öppna filen.|
|Skydd|Filerna är helt krypterade och skyddet tillämpas på följande sätt:<br /><br />-   Innan det skyddade innehållet återges måste autentisering ske för dem som tar emot filen via e-post eller får tillgång till den via behörigheter till filer eller filresurser.<br />-   Dessutom tillämpas användningsrättigheter och -principer som innehållets ägare har angett fullt ut när filerna återges antingen i IP-Viewer (för skyddade text- och bildfiler) eller i associerade program (för alla andra filtyper som stöds).|Filskydd tillämpas på följande sätt:<br /><br />-   Innan det skyddade innehållet återges måste autentiseringen slutföras för dem som har behörighet att öppna filen och som har fått åtkomst till den. Om auktoriseringen misslyckas kan filen inte öppnas.<br />-   Användningsrättigheter och -principer som innehållets ägare har angett visas för att informera behöriga användare om den avsedda principen för användning.<br />-   Granskningsloggning av behöriga användare som öppnar och använder filer förekommer, men inga användningsrättigheter tillämpas av program som inte stöder sådan loggning.|
|Standard för filtyper|Det här är standardnivån skydd av följande filtyper:<br /><br />-   Text- och bildfiler<br />-   Microsoft Office-filer (Word, Excel, PowerPoint)<br />-   Portable Document Format (.pdf)<br /><br />Mer information finns i Filtyper som stöds.|Det här är standardskyddet för alla andra filtyper (till exempel .vsdx, .rtf och så vidare) som inte stöds via det fullständiga skyddet.|

### <a name="BKMK_SupportFileTypes"></a>Filtyper som stöds
I följande tabell anges vilka filtyper som stöds av delningsapplikationen för Microsoft Rights Management.

|Filnamnstillägg|Beskrivning|Ursprungligt filnamnstillägg|
|-------------------|---------------|--------------------------------|
|.ptxt|Skyddad textfil|.txt|
|.pxml|Skyddad XML-fil|.xml|
|.pjpg|Skyddad JPG-bildfil|.jpg|
|.pjpeg|Skyddad JPEG-bildfil|.jpeg|
|.ppng|Skyddad PNG-bildfil|.png|
|.ptiff|Skyddad TIFF-bildfil|.tiff|
|.pbmp|Skyddad Windows-bitmappfil|.bmp|
|.pgif|Skyddad GIF-bildfil|.gif|
|.pgiff|Skyddad GIFF-bildfil|.giff|
|.pjpe|Skyddad JPE-bildfil|.jpe|
|.pjfif|Skyddad JFIF-bildfil|.jfif|
|.pjif|Skyddad JIF-bildfil|.jif|
I följande tabell visas de filtyper som stöds av Microsoft Office 2013, Office 2010 och Office 2007. Det finns två skyddstyper: MsoIrmProtector och OpcIrmProtector. Mer information om dessa skyddstyper finns i [Microsoft Office File Format Protectors](http://archive.msdn.microsoft.com/OfficeProtectors).

|||
|-|-|
|MsoIrmProtector stöder följande filtyper:<br /><br />-   doc<br />-   dot<br />-   xla<br />-   xls<br />-   xlt<br />-   pps<br />-   ppt|OpcIrmProtector stöder följande filtyper:<br /><br />-   docm<br />-   docx<br />-   dotm<br />-   dotx<br />-   xlam<br />-   xlsb<br />-   xlsm<br />-   xlsx<br />-   xltm<br />-   xltx<br />-   xps<br />-   potm<br />-   potx<br />-   ppsx<br />-   ppsm<br />-   pptm<br />-   pptx<br />-   thmx|

### <a name="BKMK_ScriptedInstall"></a>Automatisk distribution av Delningsapplikation för Microsoft Rights Management
Windows-versionen av RMS-delningsprogrammet stöder skriptinstallation, vilket gör den lämplig för företagsdistributioner.

##### Så här hämtar du RMS-delningsprogrammet för automatisk distribution

1.  Gå till sidan [Microsoft Rights Management sharing application for Windows](http://www.microsoft.com/en-us/download/details.aspx?id=40857) i Microsoft Download Center och klicka på **Download**.

2.  Markera och hämta de filer du behöver. Det finns två klientinstallationspaket: en för 64-bitars Windows (Microsoft Rights Management sharing application x64.zip) och en annan för 32-bitars (Microsoft Rights Management sharing application x86.zip).

3.  Extrahera filerna från de komprimerade installationspaketen, till exempel genom att dubbelklicka på dem. Kopiera de extraherade filerna till en nätverksplats som klientdatorer kan komma åt.

Installationspaketen för RMS-delningsprogrammet har stöd för olika distributioner och omfattar följande:

|Beskrivning|Distributionsscenario|
|---------------|-------------------------|
|Microsoft onlineinloggningsassistent|Krävs för följande:<br /><br />-   Office 2010 och Windows Azure RMS|
|Snabbkorrigering för Office (KB 2596501)|Krävs för följande:<br /><br />-   Office 2010 och Windows Azure RMS|
|Snabbkorrigering för kryptografiskt läge 2 (KB 2627273)|Krävs för följande:<br /><br />-   Office 2010 och Windows Azure RMS|
|AD RMS-klienten och RMS-delningsprogrammet|Krävs för följande:<br /><br />-   Office 2013 och Windows Azure RMS<br />-   Office 2010 och Windows Azure RMS<br />-   Office 2013 och Active Directory RMS<br />-   Office 2010 och Active Directory RMS<br />-   Uppgradering av RMS-delningsprogrammet|
|Office-tillägget för menyfliken|Krävs för följande:<br /><br />-   Office 2013 och Windows Azure RMS<br />-   Office 2013 och Active Directory RMS<br />-   Office 2010 och Active Directory RMS<br />-   Uppgradering av RMS-delningsprogrammet|
|Förberedelseverktyg för Windows Azure Active Directory Rights Management|Krävs för följande:<br /><br />-   Office 2010 och Windows Azure RMS|
> [!NOTE]
> För scenariot med **Office 2010 och Windows Azure RMS** kanske du använder Windows Azure RMS eller Active Directory RMS, men vill kunna skicka dokument på ett säkert sätt till personer i andra företag som använder Windows Azure RMS.
> 
> När du installerar och kör förberedelseverktyget Windows Azure Active Directory Rights Management för Office 2010 gör det två saker:
> 
> -   Det redigerar registret för att stödja RMS-delningsprogrammet.
> -   Det ”startar” användaren, vilket innebär att datorn kontaktar AD RMS-servern eller Windows Azure RMS och erhåller de certifikat som datorn och användaren behöver för att kunna använda RMS.

Använd följande procedurer för att identifiera de kommandon som krävs för att distribuera RMS-delningsprogrammet för dessa distributionsscenarier:

-   Office 2013 och Windows Azure RMS

-   Office 2010 och Windows Azure RMS

-   Office 2013 eller Office 2010 och Active Directory RMS

-   Uppgradering av RMS-delningsprogrammet

Exemplen i kommandona förutsätter att du har kopierat de hämtade och extraherade filerna till en nätverksresurs som klientdatorerna har åtkomst till med hjälp av **\\server5\apps\rms** och att klientdatorerna redan har en mapp med namnet **C:\Log files** där du lagrar programmets installationsloggfiler. Du väljer namnet på installationsloggen för varje installation, men den måste ha filnamnstillägget .log.

> [!IMPORTANT]
> Innan du distribuerar RMS-delningsprogrammet måste du paketera nödvändiga kommandon i dessa procedurer så att de kan installeras i datorns kontext för alla användare, samt installeras med lokal administratörsbehörighet. Du kan sedan distribuera paketet till datorerna med hjälp av ditt standardprogram för distribution, till exempel en grupprincip eller System Center Configuration Manager.
> 
> Ett undantag är förberedelseverktyget Windows Azure Active Directory Rights Management: Detta måste köras en gång för varje användare på datorn och verktyget måste köras med förhöjd behörighet för att kunna redigera registret. Det finns olika sätt att göra detta, exempelvis att be användarna att köra kommandot (till exempel via en länk i ett e-postmeddelande eller i supportportalen) eller lägga till kommandot i deras inloggningsskript: Om du inte kan använda kommandot RunAs eftersom användarna inte har något lokalt administratörskonto, finns distributionsverktyg som automatiskt höjer ett kommando enligt de regler som du anger.

##### Så här distribuerar du RMS-delningsprogrammet för Office 2013 och Windows Azure RMS

1.  Installera AD RMS-klienten och RMS-delningsprogrammet med hjälp av följande kommandon:

    -   För 64-bitars Windows: x64\setup_ipviewer.exe /norestart /quiet /msicl "MSIRESTARTMANAGERCONTROL=Disable" /log "&lt;log file path and name&gt;"

        ```
        x64\setup_ipviewer.exe /norestart /quiet /msicl "MSIRESTARTMANAGERCONTROL=Disable" /log "<log file path and name>"
        ```

    -   För 32-bitars Windows:

        ```
        X86\setup_ipviewer.exe /norestart /quiet /msicl "MSIRESTARTMANAGERCONTROL=Disable" /log "<log file path and name>"
        ```

    Till exempel: `\\server5\apps\rms\x64\setup_ipviewer.exe /norestart /quiet /msicl "MSIRESTARTMANAGERCONTROL=Disable" /log "C:\Log files\ipviewerinstall.log"`

2.  Installera Office-tillägget med hjälp av följande kommandon:

    -   För 64-bitarsversionen av Office:

        ```
        msiexec.exe /norestart /quiet MSIRESTARTMANAGERCONTROL=Disable /i "x64\Setup64.msi" /L*v "<log file path and name>"
        ```

    -   För 32-bitarsversionen av Office:

        ```
        msiexec.exe /norestart /quiet MSIRESTARTMANAGERCONTROL=Disable /i "x86\Setup.msi" /L*v "<log file path and name>"
        ```

    > [!NOTE]
    > För att slutföra installationen måste datorn startas om. Du kan göra en automatisk omstart med hjälp av kommandot shutdown /i.

    Till exempel: `\\server5\apps\rms\msiexec.exe /norestart /quiet MSIRESTARTMANAGERCONTROL=Disable /i "x64\Setup64.msi" /L*v "C:\Log files\rmsoffice.log"`

##### Så här distribuerar du RMS-delningsprogrammet för Office 2010 och Windows Azure RMS

1.  Installera Microsoft onlineinloggningsassistent med hjälp av följande kommandon:

    -   För 64-bitars Windows:

        ```
        msiexec.exe /norestart /quiet MSIRESTARTMANAGERCONTROL=Disable /i "x64\msoidcli_64bit.msi" /L*v "<log file path and name >"
        ```

    -   För 32-bitars Windows:

        ```
        msiexec.exe /norestart /quiet MSIRESTARTMANAGERCONTROL=Disable /i "x64\msoidcli_64bit.msi" /L*v "<log file path and name>"
        ```

    Till exempel: `\\server5\apps\rms\msiexec.exe /norestart /quiet MSIRESTARTMANAGERCONTROL=Disable /i "x64\msoidcli_64bit.msi" /L*v "C:\Log files\assistant.log"`

2.  Installera Office-snabbkorrigeringen med hjälp av följande kommandon:

    -   För 64-bitarsversionen av Office:

        ```
        x64\office2010-kb2596501-fullfile-x64-glb.exe /norestart /quiet /log:"<log file path and name >"
        ```

    -   För 32-bitarsversionen av Office:

        ```
        x86\office2010-kb2596501-fullfile-x86-glb.exe /norestart /quiet /log:"<log file path and name>"
        ```

    Till exempel: `\\server5\apps\rms\x64\office2010-kb2596501-fullfile-x64-glb.exe /norestart /quiet /log:"C:\Log files\kb2596501install.log"`

3.  Installera snabbkorrigeringen för kryptografiskt läge 2 med hjälp av följande kommandon:

    -   För 64-bitars Windows:

        ```
        wusa.exe /norestart /quiet "x64\Windows6.1-KB2627273-v4-x64.msu" /log:"<log file path and name >"
        ```

    -   För 32-bitars Windows:

        ```
        wusa.exe /norestart /quiet "x86\Windows6.1-KB2627273-v4-x86.msu" /log:"<log file path and name>"
        ```

    Till exempel: `\\server5\apps\rms\wusa.exe /norestart /quiet "x64\Windows6.1-KB2627273-v4-x64.msu" /log:"C:\Log files\kb267273.log"`

4.  Installera AD RMS-klienten och RMS-delningsprogrammet med hjälp av följande kommando:

    -   För 64-bitars Windows:

        ```
        x64\setup_ipviewer.exe /norestart /quiet /msicl "MSIRESTARTMANAGERCONTROL=Disable" /log "<log file path and name >"
        ```

    -   För 32-bitars Windows:

        ```
        X86\setup_ipviewer.exe /norestart /quiet /msicl "MSIRESTARTMANAGERCONTROL=Disable" /log "<log file path and name>"
        ```

    Till exempel: `\\server5\apps\rms\x64\setup_ipviewer.exe /norestart /quiet /msicl "MSIRESTARTMANAGERCONTROL=Disable" /log "C:\Log files\ipviewerinstall.log"`

5.  Installera Office-tillägget med hjälp av följande kommandon:

    -   För 64-bitarsversionen av Office:

        ```
        msiexec.exe /norestart /quiet MSIRESTARTMANAGERCONTROL=Disable /i "x64\Setup64.msi" /L*v "<log file path and name>"
        ```

    -   För 32-bitarsversionen av Office:

        ```
        msiexec.exe /norestart /quiet MSIRESTARTMANAGERCONTROL=Disable /i "x86\Setup.msi" /L*v "<log file path and name>"
        ```

    > [!NOTE]
    > För att slutföra installationen måste datorn startas om. Du kan göra en automatisk omstart med hjälp av kommandot shutdown /i.

    Till exempel: `\\server5\apps\rms\msiexec.exe /norestart /quiet MSIRESTARTMANAGERCONTROL=Disable /i "x64\Setup64.msi" /L*v "C:\Log files\rmsoffice.log"`

6.  Installera förberedelseverktyget för Windows Azure Active Directory Rights Management genom att lägga till följande kommando i inloggningsskripten:

    > [!IMPORTANT]
    > Användarna måste ha lokal administratörsbehörighet för att kunna köra kommandot.

    -   För 64-bitars Windows 8:

        ```
        x64\aadrmprep.exe /initiateMe /logfile "<log file path and name>"
        ```

    -   För 32-bitars Windows 8:

        ```
        X86\aadrmprep.exe /initiateMe /logfile "<log file path and name>"
        ```

    -   För 64-bitars Windows 7:

        ```
        x64\win7\aadrmprep.exe /initiateMe /logfile "<log file path and name>"
        ```

    -   För 32-bitars Windows 7:

        ```
        X86\win7\aadrmprep.exe /initiateMe /logfile "<log file path and name>"
        ```

    > [!NOTE]
    > Detta kommando kan eventuellt uppmana användaren att ange sina autentiseringsuppgifter för Windows Azure. Om datorn inte är ansluten till en domän uppmanas användaren att göra det. Om datorn är ansluten till en domän kan verktyget använda cachelagrade autentiseringsuppgifter.

    Till exempel: `\\server5\apps\rms\x64\aadrmprep.exe /initiateMe /logfile "C:\Log files\aadrmprepinstall.log"`

##### Så här distribuerar du RMS-delningsprogrammet för Office 2013 eller Office 2010 och Active Directory RMS

1.  Installera AD RMS-klienten och RMS-delningsprogrammet med hjälp av följande kommandon:

    -   För 64-bitars Windows:

        ```
        x64\setup_ipviewer.exe /norestart /quiet /msicl "MSIRESTARTMANAGERCONTROL=Disable" /log "<log file path and name>"
        ```

    -   För 32-bitars Windows:

        ```
        X86\setup_ipviewer.exe /norestart /quiet /msicl "MSIRESTARTMANAGERCONTROL=Disable" /log "<log file path and name>"
        ```

    Till exempel: `\\server5\apps\rms\x64\setup_ipviewer.exe /norestart /quiet /msicl "MSIRESTARTMANAGERCONTROL=Disable" /log "C:\Log files\ipviewerinstall.log"`

2.  Installera Office-tillägget med hjälp av följande kommandon:

    -   För 64-bitarsversionen av Office:

        ```
        msiexec.exe /norestart /quiet MSIRESTARTMANAGERCONTROL=Disable /i "x64\Setup64.msi" /L*v "<log file path and name>"
        ```

    -   För 32-bitarsversionen av Office:

        ```
        msiexec.exe /norestart /quiet MSIRESTARTMANAGERCONTROL=Disable /i "x86\Setup.msi" /L*v "<log file path and name>"
        ```

    > [!NOTE]
    > För att slutföra installationen måste datorn startas om. Du kan göra en automatisk omstart med hjälp av kommandot shutdown /i.

    Till exempel: `\\server5\apps\rms\msiexec.exe /norestart /quiet MSIRESTARTMANAGERCONTROL=Disable /i "x64\Setup64.msi" /L*v "C:\Log files\rmsofficeinstall.log"`

##### Så här uppgraderar du RMS-delningsprogrammet

1.  Installera AD RMS-klienten och RMS-delningsprogrammet med hjälp av följande kommando:

    -   För 64-bitars Windows:

        ```
        x64\setup_ipviewer.exe /norestart /quiet /msicl "MSIRESTARTMANAGERCONTROL=Disable" /log "<log file path and name>"
        ```

    -   För 32-bitars Windows:

        ```
        X86\setup_ipviewer.exe /norestart /quiet /msicl "MSIRESTARTMANAGERCONTROL=Disable" /log "<log file path and name>"
        ```

    Till exempel: `\\server5\apps\rms\x64\setup_ipviewer.exe /norestart /quiet /msicl "MSIRESTARTMANAGERCONTROL=Disable" /log "C:\Log files\ipviewerinstall.log"`

2.  Installera Office-tillägget med hjälp av följande kommandon:

    -   För 64-bitarsversionen av Office:

        ```
        msiexec.exe /norestart /quiet MSIRESTARTMANAGERCONTROL=Disable /i "x64\Setup64.msi" /L*v "<log file path and name>"
        ```

    -   För 32-bitarsversionen av Office:

        ```
        msiexec.exe /norestart /quiet MSIRESTARTMANAGERCONTROL=Disable /i "x86\Setup.msi" /L*v "<log file path and name>"
        ```

    > [!NOTE]
    > För att slutföra installationen måste datorn startas om. Du kan göra en automatisk omstart med hjälp av kommandot shutdown /i.

    Till exempel: `\\server5\apps\rms\msiexec.exe /norestart /quiet MSIRESTARTMANAGERCONTROL=Disable /i "x64\Setup64.msi" /L*v "C:\Log files\rmsofficeinstall.log"`

#### <a name="BKMK_verifyscripted"></a>Verifierar att installationen slutfördes
Du kan använda installationsloggfilerna för att verifiera att installationen slutförs.

###### Så här verifierar du installationen för Microsoft onlineinloggningsassistenten

-   Sök efter följande text i installationsloggfilen för att verifiera att installationen har slutförts: **Installationsstatus – slutförd eller misslyckades: 0**

    Exempelrader från en slutförd installation:

    **MSI (s) (9C:88) [18:49:04:007]: Produkt: Microsoft RMS Office-tillägg -- Installationen slutfördes korrekt.**

    **MSI (s) (9C:88) [18:49:04:007]: Windows Installer installerade produkten. Produktnamn: Microsoft RMS Office-tilläggsprogram. Produktversion: 1.0.7. Produktspråk: 1033. Tillverkare: Microsoft. Installationsstatus – slutförd eller misslyckades: 0.**

###### Så här kontrollerar du installationen av snabbkorrigeringen för Office

-   Sök efter någon av följande textsträngar i installationsloggfilen för att verifiera att installationen har slutförts:

    -   För 64-bitarsversionen av Office:

        -   **office2010-kb2596501-fullfile-x64-glb.exe exited with status SUCCESS**

        -   **office2010-kb2596501-fullfile-x64-glb.exe exited with status NOTAPPLICABLE**

    -   För 32-bitarsversionen av Office:

        -   **office2010-kb2596501-fullfile-x86-glb.exe exited with status SUCCESS**

        -   **office2010-kb2596501-fullfile-x86-glb.exe exited with status NOTAPPLICABLE**

###### Så här kontrollerar du installationen av snabbkorrigeringen för kryptografiskt läge 2

-   Sök efter någon av följande textsträngar i installationsloggfilen för att verifiera att installationen har slutförts:

    -   För 64-bitars Windows:

        -   **Windows6.1-KB2627273-v4-x64.msu exited with status SUCCESS**

        -   **Windows6.1-KB2627273-v4-x64.msu exited with status NOTAPPLICABLE**

    -   För 32-bitars Windows:

        -   **Windows6.1-KB2627273-v4-x86.msu exited with status SUCCESS**

        -   **Windows6.1-KB2627273-v4-x86.msu exited with status NOTAPPLICABLE**

###### Så här kontrollerar du installationen för AD RMS-klienten och RMS-delningsprogrammet

-   Sök efter följande text i installationsloggfilen för att verifiera att installationen har slutförts: **Installationsstatus – slutförd eller misslyckades: 0**

    Exempelrader från en slutförd installation:

    **MSI (s) (F0:B8) [14:19:57:854]: Produkt: Active Directory Rights Management Services Client 2.1 -- Installationen slutfördes korrekt.**

    **MSI (s) (F0:B8) [14:19:57:854]: Windows Installer installerade produkten. Produktnamn: Active Directory Rights Management Services Client 2.1. Produktversion: 1.0.1179.1. Produktspråk: 1033. Tillverkare: Microsoft Corporation. Installationsstatus – slutförd eller misslyckades: 0.**

###### Så här kontrollerar du installationen av tillägget för Office

-   Sök efter följande text i installationsloggfilen för att verifiera att installationen har slutförts: **Installationsstatus – slutförd eller misslyckades: 0**

    Exempelrader från en slutförd installation:

    **MSI (s) (9C:88) [18:49:04:007]: Produkt: Microsoft RMS Office-tillägg -- Installationen slutfördes korrekt.**

    **MSI (s) (9C:88) [18:49:04:007]: Windows Installer installerade produkten. Produktnamn: Microsoft RMS Office-tilläggsprogram. Produktversion: 1.0.7. Produktspråk: 1033. Tillverkare: Microsoft. Installationsstatus – slutförd eller misslyckades: 0.**

###### Så här kontrollerar du installationen av förberedelseverktyget för Windows Azure Active Directory Rights Management

-   Sök efter följande text i installationsloggfilen för att verifiera att installationen har slutförts: **aadrmprep.exe exited with status SUCCESS**

    > [!NOTE]
    > Ibland kan den här installationen köras två gånger; den första gången misslyckas den, och den andra slutförs den utan problem.

Om du manuellt vill kontrollera registerändringarna som det här verktyget gör, är det dessa som berörs:

-   [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSDRM\Federation]

    "FederationHomeRealm"="urn:HostedRmsOnlineService:Certification"

-   [HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\MSDRM\Federation]

    "FederationHomeRealm"="urn:HostedRmsOnlineService:Certification"

-   [HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\MSDRM\ServiceLocation\Activation]

    @="&lt;certifiering url&gt;"

-   [HKEY_CURRENT_USER\SOFTWARE\Microsoft\Office\14.0\Common\DRM]

    DefaultUser="&lt;default_user&gt;"

#### <a name="BKMK_uninstallscripted"></a>Avinstallationskommandon
Det är inte alla installationskommandon som krävs för dessa distributioner som stöder ett avinstallationskommando. Du kan avinstallera AD RMS-klienten och delningsprogrammet, och du kan avinstallera Office-tillägget. Använd följande kommandon för att avinstallera de här elementen.

###### Så här avinstallerar du AD RMS-klienten och RMS-delningsprogrammet

-   Använd följande kommandon:

    -   För 64-bitars Windows:

        ```
        x64\setup_ipviewer.exe /uninstall /quiet
        ```

    -   För 32-bitars Windows:

        ```
        x86\setup_ipviewer.exe /uninstall /quiet
        ```

###### Så här avinstallerar du Office-tillägget

-   Använd följande kommandon:

    -   För 64-bitarsversionen av Office:

        ```
        msiexec /x \x64\Setup[64].msi /quiet
        ```

    -   För 32-bitarsversionen av Office:

        ```
        msiexec /x \x86\Setup.msi /quiet
        ```

## Se även
[Hämta delningsapplikationen för Microsoft Rights Management (http://go.microsoft.com/fwlink/?LinkId=303970)](http://go.microsoft.com/fwlink/?LinkId=303970)
 [Vanliga frågor och svar för delningsapplikationen Microsoft Rights Management för Windows](http://go.microsoft.com/fwlink/?LinkId=303971)

