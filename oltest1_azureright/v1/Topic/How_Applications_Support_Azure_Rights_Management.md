---
description: na
keywords: na
title: How Applications Support Azure Rights Management
search: na
ms.date: na
ms.service: rights-management
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2cdc7bde-4044-4021-b887-11476f99afd9
---
# Hur program st&#246;d f&#246;r Azure Rights Management
Använd följande information för att hjälpa dig att förstå hur dina slutanvändarprogram (till exempel i Office-program, Word, Excel, PowerPoint och Outlook) och tjänster (till exempel Exchange- och SharePoint) kan använda Microsoft [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] för att skydda din organisations data:

-   [RMS-delning program för Windows och mobila plattformar](../Topic/How_Applications_Support_Azure_Rights_Management.md#BKMK_SharingAppIntro)

-   [Office-program: Word och Excel, PowerPoint, Outlook](../Topic/How_Applications_Support_Azure_Rights_Management.md#BKMK_OfficeAppsIntro)

    -   [Exchange Online och Exchange Server](../Topic/How_Applications_Support_Azure_Rights_Management.md#BKMK_ExchangeIntro)

    -   [SharePoint Online och SharePoint Server](../Topic/How_Applications_Support_Azure_Rights_Management.md#BKMK_SharePointIntro)

-   [Filservrar som kör Windows Server och Använd fil klassificering infrastruktur (FCI)](../Topic/How_Applications_Support_Azure_Rights_Management.md#BKMK_FCIIntro)

-   [Andra program som stöder RMS APIs](../Topic/How_Applications_Support_Azure_Rights_Management.md#BKMK_APIAppsIntro)

> [!NOTE]
> Kontrollera program och versioner som [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] (Azure RMS) stöder, se [Krav för Azure Rights Management](../Topic/Requirements_for_Azure_Rights_Management.md).

I vissa fall används automatiskt information protection, enligt principer som du konfigurerar. Exempel: Detta är fallet med SharePoint-bibliotek, klassificerad filer och Exchange regler. I annat fall måste måste användarna installera information protection själva från sina program genom att välja en mall eller genom att välja särskilda alternativ. Exempel: Detta är fallet när användarna dela en fil med e-post eller skydda en fil på plats genom att begränsa åtkomsten eller användningen till utvalda användare eller användare utanför organisationen.

Mallar gör det enklare för användare (och administratörer som konfigurerar principer) att använda rätt skyddsnivån och begränsa åtkomsten till personer i din organisation. Även om [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] kommer med två standardmallar vill du förmodligen skapa mallar för att minska gånger när de behöver ange olika alternativ. Mer information finns i [Konfigurera anpassade mallar för Azure Rights Management](../Topic/Configuring_Custom_Templates_for_Azure_Rights_Management.md).

För de fall där du måste använda information protection själva ska du se hur förser dem med instruktioner och riktlinjer och när du gör detta. Instruktionerna ska vara specifika för program- och versioner som används och hur de använder dem och vägledning för när och hur för att ge skydd ska vara lämpliga för ditt företag. Mer information finns i [Hjälper användarna att skydda filer med Azure Rights Management](../Topic/Helping_Users_to_Protect_Files_by_Using_Azure_Rights_Management.md).

Information om hur du konfigurerar dessa program för Azure RMS finns [Konfigurera program för Azure Rights Management](../Topic/Configuring_Applications_for_Azure_Rights_Management.md).

> [!TIP]
> Exempel och skärmbilder av program med hjälp av Azure RMS finns på [Azure RMS i åtgärd: Administratörer och användare ser](../Topic/What_is_Azure_Rights_Management_.md#BKMK_RMSpictures) avsnitt från den [Vad är Azure Rights Management?](../Topic/What_is_Azure_Rights_Management_.md) ämne.

## <a name="BKMK_SharingAppIntro"></a>RMS-delning program för Windows och mobila plattformar
RMS-delning programmet är ett kostnadsfritt program som krävs för att stödja Office 2010, men du bör också för Windows-datorer, Mac-datorer och mobila enheter. En av dess fördelar är att det gäller allmän skydd för program och filer som inte stöder internt [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)], vilket innebär att alla filer kan skyddas. Mer information om de olika skydd nivåerna finns i [för skydd – intern och allmän](http://technet.microsoft.com/library/dn339003.aspx) avsnitt från den [Rights Management dela program administratörshandboken](http://technet.microsoft.com/library/dn339003.aspx).

När användarna skyddar filer med RMS kan delning, de även spåra dokument som de skyddade och återkalla åtkomst till dem om det behövs. De gör det genom att använda den [dokument spårning webbplats](http://go.microsoft.com/fwlink/?LinkId=529562).

RMS-delning program diskret integreras med för Windows-datorer och ger ökad de program som redan används:

-   En Office-tillägg för Word, Excel, PowerPoint och Outlook är installerad. Detta ger användare med en **Dela skyddat** knapp i menyfliksområdet, som startar ett enkelt att använda dialogrutan Inställningar som vanligtvis används för att skydda filer som ska skickas. Den här knappen innehåller också ett snabbt sätt att spåra plats.

-   En ny högerklickar du på alternativet för filen Explorer. Detta ger användare med en **skydda på plats** alternativ, som startar ett enkelt att använda dialogrutan Inställningar som vanligtvis används för att skydda filer som lagras på en disk.

-   Ett visningsprogram för att öppna filer har skyddats av [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)]. Detta program anropas automatiskt när det finns inget andra program som kan öppna den skyddade filen.

-   Backend-konfiguration för Office 2010 som gör att Word, Excel, PowerPoint och Outlook från det här paketet samverkan med [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)].

Även om RMS-delning program för Windows kan hämtas och installeras för en enstaka dator med hjälp av den [Microsoft Rights Management sidan](http://go.microsoft.com/fwlink/?LinkId=303970), stöder även en enterprise-distribution för tyst installation och anpassad konfiguration. Mer information finns i följande resurser:

-   [Rights Management dela program administratörshandboken](http://technet.microsoft.com/library/dn339003.aspx)

-   [Rights Management delning användaren guide till](http://technet.microsoft.com/library/dn339006.aspx)

RMS-delning program för mobila enheter stöder de vanligaste mobila enheter, till exempel iPad och iPhone, Android, Windows Phone och Windows hö Användare kan hämta den här appen på relevanta Store och det finns länkar till dessa från den [Microsoft Rights Management sidan](http://go.microsoft.com/fwlink/?LinkId=303970).

## <a name="BKMK_OfficeAppsIntro"></a>Office-program: Word och Excel, PowerPoint, Outlook
Dessa program internt stöder Rights Management med information rights management (IRM) och användarna kan användas skydd för ett sparat dokument eller i ett e-postmeddelande ska skickas. Användare kan använda mallar eller välj mycket anpassade inställningar för begränsningar åtkomst, rättigheter och användning. Användare kan konfigurera en fil så att den kan endast användas av personer i din organisation eller kontroll om filen kan redigeras eller begränsat till skrivskyddad eller förhindra att den skrivs ut. Viktiga filer förfallotiden kan konfigureras (direkt av användare eller genom att använda en mall) för när filen inte längre kan nås. För Outlook, du kan också välja den **Vidarebefordra inte** alternativet för att förhindra att data läcker.

### <a name="BKMK_ExchangeIntro"></a>Exchange Online och Exchange Server
När du använder Exchange Online eller Exchange Server, kan du använda information rights management (IRM) integration, som ger ytterligare information protection lösningar:

-   **Exchange ActiveSync IRM** så att mobila enheter kan skydda och förbruka skyddade e-postmeddelanden.

-   RMS-stöd för den **Outlook Web App**, genomföras på samma sätt till Outlook-klienten, så att användare kan skydda e-postmeddelanden i mallar eller genom att ange olika alternativ och användare kan läsa och använda skyddade e-postmeddelanden som skickas till dem.

-   **Protection regler** för Outlook-klienter att administratör konfigurerar om du vill använda automatiskt RMS-mallar för e-postmeddelanden för angivna mottagare. Till exempel när interna e-postmeddelanden skickas till din juridiska avdelningen de kan bara läsas av medlemmar i avdelningen juridiska och kan inte vidarebefordras. Användarna ser skydd tillämpas på e-postmeddelande innan du skickar den och som standard de kan ta bort den om de inte är det nödvändigt. E-postmeddelanden krypteras innan de skickas. Mer information finns i [Outlook Protection regler](http://technet.microsoft.com/library/dd638178%28v=exchg.150%29.aspx) och [Skapa en regel för Outlook Protection](http://technet.microsoft.com/library/dd638196%28v=exchg.150%29.aspx) i Exchange-biblioteket.

-   **Transport regler** att en administratör konfigurerar om du vill använda automatiskt RMS-mallar för e-post meddelanden utifrån egenskaper, till exempel avsändare, mottagare, ämne och innehåll. Dessa liknar koncept protection regler men användare kan inte ta bort skyddet, kan tillämpas på Outlook Web Access och e-postmeddelanden skickas av mobila enheter och kryptera inte e-postmeddelanden innan de skickas från klienten. Mer information finns i [Skapa en regel för Transport Protection](http://technet.microsoft.com/library/dd302432.aspx) i Exchange-biblioteket.

-   **Data går förlorade förhindra (DLP) principer** som innehåller en uppsättning villkor för att filtrera e-postmeddelanden och vidta åtgärder för att förhindra förlust av data för konfidentiell eller känslig innehåll (till exempel personlig information eller kontokortsinformationen). Princip Tips kan användas när känsliga data upptäcks att meddela användare som de behöver använda information protection utifrån informationen i e-postmeddelandet. Mer information finns i [förhindra dataförlust](http://technet.microsoft.com/library/jj150527%28v=exchg.150%29.aspx) i Exchange-biblioteket.

-   **Office 365-meddelandekryptering** som använder transport regler för att skicka krypterade e-postmeddelanden till personer utanför företaget och e-postmeddelandet läses från en webbläsare med ett gränssnitt som liknar Outlook Web App. Du kan anpassa friskrivning från text och text i sidhuvudet i ditt företags krypterade e-postmeddelanden och även lägga till en företagslogotyp. Mer information finns i [Office 365-meddelandekryptering](http://office.microsoft.com/o365-message-encryption-FX104179182.aspx) från Office-webbplatsen.

Om du använder Exchange Server kan du använda information protection funktionerna med [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] genom att distribuera RMS-koppling som fungerar som en relä mellan lokala servrarna och RMS-Molntjänsten. Mer information finns i [Distribuera Azure Rights Management-koppling](../Topic/Deploying_the_Azure_Rights_Management_Connector.md).

### <a name="BKMK_SharePointIntro"></a>SharePoint Online och SharePoint Server
När du använder SharePoint Online eller SharePoint Server kan använda du information rights management (IRM) integration, vilket kan administratörer skydda listor eller bibliotek så att när en användare kontrollerar ur ett dokument, filen skyddas så att endast behöriga användare kan visa och använda filen enligt de information principer för skadlig programvara som du anger. Exempel: filen kan vara skrivskyddad, inaktivera kopiering av text, förhindra att spara en lokal kopia och förhindra att skriva ut filen.

Listor och bibliotek används information protection alltid av en administratör aldrig en slutanvändare. Och tillämpas på listan eller biblioteket nivå för alla dokument i behållaren och inte för enskilda filer.  Om du använder SharePoint Online kan användare också använda IRM till sina OneDrive för Business bibliotek.

Tjänsten IRM måste först aktiveras för SharePoint. Sedan kan ange du Information Rights Management för ett bibliotek. SharePoint Online och OneDrive för företag ange användare även Information Rights Management för sina OneDrive för Business bibliotek. SharePoint används inte principmallar, även om det finns SharePoint konfigurationsinställningar som du kan välja som motsvarar de inställningar som du kan ange i mallar.

Om du använder SharePoint Server kan du använda information protection funktionerna med [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] genom att distribuera RMS-koppling som fungerar som en relä mellan lokala servrarna och RMS-Molntjänsten. Mer information finns i [Distribuera Azure Rights Management-koppling](../Topic/Deploying_the_Azure_Rights_Management_Connector.md).

> [!NOTE]
> Det finns vissa begränsningar när du använder IRM med SharePoint:
> 
> -   Du kan inte använda den standard eller anpassade mallar som du hanterar i Azure-portalen.
> -   Filer som har en. PPDF filnamnstillägg för skyddade PDF-filer stöds inte. Filer som har. PDF-filnamnstillägg och som har skyddats internt av RMS stöds när du använder en PDF-läsare som ursprungligen har stöd för RMS.
> -   Eftersom Office på mobila enheter inte ännu stöder RMS enheterna måste använda en webbläsare för att visa filer som har skyddats med RMS och filerna är skrivskyddad.

Azure RMS gäller användningsrestriktioner och datakryptering för dokument när de har hämtats från SharePoint och inte när dokumentet skapas i SharePoint eller överföras i biblioteket. Information om hur dokument som skyddas innan de hämtas finns [datakryptering i OneDrive för företag och SharePoint Online](https://technet.microsoft.com/library/dn905447.aspx) från SharePoint-dokumentationen.

Mer information om hur du använder Azure RMS med SharePoint finns i följande inlägget från Office-blogg: [Vad är nytt med Information Rights Management i SharePoint- och SharePoint Online](http://blogs.office.com/2012/11/09/whats-new-with-information-rights-management-in-sharepoint-and-sharepoint-online/)

## <a name="BKMK_FCIIntro"></a>Filservrar som kör Windows Server och Använd fil klassificering infrastruktur (FCI)
När du konfigurerar Windows Server att använda filen klassificering infrastruktur File Server Resource Manager funktionen igenom lokala filer och avgöra om de innehåller känsliga data. Filer som uppfyller kriterierna taggats de med Klassificeringsegenskaper som definierar en administratör. Filen klassificering infrastruktur kan sedan vidta de automatiska åtgärder enligt klassificering. En av dessa åtgärder bland annat koppling information protection med hjälp av [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] och distribution av Rights Management-koppling (även kallat RMS-koppling). Office-filer är sedan automatiskt skyddas av Azure RMS.

Om du vill skydda alla filtyper, ska du inte använda RMS-koppling utan i stället köra Windows PowerShell-skript med hjälp av cmdlet: ar från den [RMS Protection verktyget](https://www.microsoft.com/en-us/download/details.aspx?id=47256).

Principer för klassificering är fullständigt konfigureras och mycket utökningsbara så att du kan förhindra potentiella data läcker från obehörig och auktoriserade användare. Den kan även bidra till att minska risken för data läcker av administratörer eftersom du kan konfigurera principer som inte kräver administratörer har åtkomst till filer.

Anvisningarna för att distribuera och konfigurera RMS-koppling för Office-filer, se [Distribuera Azure Rights Management-koppling](../Topic/Deploying_the_Azure_Rights_Management_Connector.md).

Instruktioner att använda Windows PowerShell-skript för alla filtyper finns i [RMS-skydd med infrastrukturen i Windows Server-filen klassificering &#40;FCI&#41;](../Topic/RMS_Protection_with_Windows_Server_File_Classification_Infrastructure__FCI_.md).

## <a name="BKMK_APIAppsIntro"></a>Andra program som stöder RMS APIs
Med hjälp av RMS-SDK interna utvecklarna kan skriva av branschspecifika program till stöder [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)]. Hur information protection är integrerad med dessa program beror på hur de skrivs. Till exempel integrering kan tillämpas automatiskt med minimal användaråtgärder krävs eller för en mer anpassade upplevelse användare uppmanas att konfigurera inställningar för gäller information protection filer. Mer information om SDK finns på [Microsoft Rights Management SDK](http://msdn.microsoft.com/library/hh552972%28v=vs.85%29.aspx).

På samma sätt ger många leverantörer program tillhandahåller information protection lösningar, kallas även enterprise rights management (ERM) produkter. Populära exempel är en PDF-läsare som stöder [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)] för specifika plattformar. Du kan använda tabellen i den [Klienten enhetsfunktioner](../Topic/Requirements_for_Azure_Rights_Management.md#BKMK_ClientCapabilities) delen av den [Krav för Azure Rights Management](../Topic/Requirements_for_Azure_Rights_Management.md) avsnittet om du vill identifiera program som stöder RMS (RMS-enlightened-program) och sedan använda en webbsökning köp eller hämta programmet.

> [!TIP]
> Nyligen utgiven program du RMS community kanaler, som anges i [Information och Support för Azure Rights Management](../Topic/Information_and_Support_for_Azure_Rights_Management.md).

## Se även
[Kom igång med Azure Rights Management](../Topic/Getting_Started_with_Azure_Rights_Management.md)

