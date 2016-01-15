---
description: na
keywords: na
title: Configuring Custom Templates for Azure Rights Management
search: na
ms.date: na
ms.service: rights-management
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1775d8d0-9a59-42c8-914f-ce285b71ac1c
---
# Konfigurera anpassade mallar f&#246;r Azure Rights Management
När du har aktiverat Azure Rights Management (Azure RMS) kan användare automatiskt att använda två standardmallar som gör det enklare att använda principer för att begränsar åtkomsten till behöriga användare i organisationen-känsliga filer. Dessa två mallar har följande rättigheter principbegränsningar:

-   Skrivskyddad visning för skyddat innehåll

    -   Visningsnamn: **&lt; organisationsnamn &gt; - konfidentiell Visa endast**

    -   Specifika behörighet: Visa innehåll

-   Läsa eller ändra behörigheter för skyddat innehåll

    -   Visningsnamn: **&lt; organisationsnamn &gt; - konfidentiell**

    -   Specifika behörigheter: Visa innehållet, spara filen, redigera innehåll, visa tilldelade rättigheter, Tillåt makron, vidarebefordra, svara, svara alla

Dessutom den [RMS-delning program](http://technet.microsoft.com/library/dn339006.aspx) användarna definiera sina egna behörigheter. Och för att Outlook-klienten och Outlook Web Access användare kan välja den **Vidarebefordra inte** alternativet för e-postmeddelanden.

För många organisationer vara standardmallarna som tillräckligt. Men om du vill skapa egna anpassade rättigheter principmallar kan du göra det. Skäl för att skapa en anpassad mall inkluderar följande:

-   Vill du en mall för att ge behörighet att en delmängd användare i organisationen i stället för alla användare.

-   Du vill att endast en delmängd av användare ska kunna se och markera en mallen (avdelningar) från program i stället för alla användare i organisationen se och kan välja mallen.

-   Du vill definiera en anpassad för en mall, till exempel visa och redigera, men inte kopiera och skriva ut.

-   Du vill konfigurera ytterligare alternativ i en mall som innehåller ett förfallodatum och om innehållet kan användas utan en Internetanslutning.

Om användarna ska kunna välja en anpassad mall som innehåller inställningar, till exempel dessa måste du först skapa en anpassad mall, konfigurerar den och publicera den.

Använd följande avsnitt som hjälper dig att konfigurera och använda anpassade mallar:

-   [Hur du skapar, konfigurera och publicera en egen mall](../Topic/Configuring_Custom_Templates_for_Azure_Rights_Management.md#BKMK_HowToConfigureCustomTemplates)

-   [Så här kopierar du en mall](../Topic/Configuring_Custom_Templates_for_Azure_Rights_Management.md#BKMK_HowToCopyTemplates)

-   [Ta bort (Arkiv) mallar](../Topic/Configuring_Custom_Templates_for_Azure_Rights_Management.md#BKMK_HowToArchiveTemplates)

-   [Uppdatera mallar för användare](../Topic/Configuring_Custom_Templates_for_Azure_Rights_Management.md#BKMK_RefreshingTemplates)

-   [Windows PowerShell-referens](../Topic/Configuring_Custom_Templates_for_Azure_Rights_Management.md#BKMK_PowerShellTemplates)

## <a name="BKMK_HowToConfigureCustomTemplates"></a>Hur du skapar, konfigurera och publicera en egen mall
Skapa och hantera egna mallar i Azure-hanteringsportalen. Du kan göra detta direkt från Azure-hanteringsportalen eller logga in på Office 365 Administrationscenter och välj de **Avancerade funktioner** för Rights Management som sedan omdirigeras till Azure-hanteringsportalen.

Du kan använda följande procedurer för att skapa, konfigurera och publicera anpassade mallar för Rights Management.

#### Skapa en anpassad mall

1.  Beroende på om du loggar in på Office 365 Administrationscenter eller Azure-portalen, gör något av följande:

    -   Från den [Office 365 Administrationscenter](https://portal.office.com/):

        1.  I det vänstra fönstret klickar du på **tjänstinställningar**.

        2.  Från den **tjänstinställningar** klickar du på **rights management**.

        3.  I den **skydda din information** Klicka **hantera**.

        4.  I den **rights management** Klicka **Avancerade funktioner**.

            > [!NOTE]
            > Om du inte har aktiverat Rights Management kan du först på **Aktivera** och bekräfta åtgärden. Mer information finns i [Aktivera Azure Rights Management](../Topic/Activating_Azure_Rights_Management.md).
            > 
            > Om du inte har klickat på **Avancerade funktioner** innan när Rights Management har aktiverats kan följa den på skärmen anvisningarna för att hämta en kostnadsfri Azure-prenumeration som krävs för att få åtkomst till Azure-portalen.

            Klicka på **Avancerade funktioner** läses in i Azure-portalen, där du kan hantera **RIGHTS MANAGEMENT** för organisationens Azure Active Directory.

    -   Från den [Azure-portalen](http://go.microsoft.com/fwlink/p/?LinkID=275081):

        1.  I det vänstra fönstret klickar du på **ACTIVE DIRECTORY**.

        2.  Från den **active directory** klickar du på **RIGHTS MANAGEMENT**.

        3.  Välj katalogen att hantera Rights Management.

        4.  Om du inte redan har aktiverat Rights Management klickar du på **Aktivera** och bekräfta åtgärden.

            > [!NOTE]
            > Mer information finns i [Aktivera Azure Rights Management](../Topic/Activating_Azure_Rights_Management.md).

2.  Skapa en ny mall:

    -   I Azure-portalen från den **Kom igång med Rights Management** snabbt startsida klickar du på **Skapa en ny rättigheter kan**.

        Om du inte omedelbart ser den här sidan efter att följa anvisningarna för Office 365 Använd navigering-instruktioner ovan för Azure-portalen.

3.  På den **lägga till en ny rättighetsprincipmall** väljer du ett språk som du skriver mallnamn och beskrivning som visas (du kan lägga till fler språk senare). Skriv ett unikt namn och en beskrivning sedan och klicka på Slutför.

Från den **Kom igång med Rights Management** snabbt startsida, klicka på **Hantera rättigheter principmallarna**. Nyskapade mallen läggs till i listan över mallar med statusen visas **arkiverade**. I det här skedet mallen skapats men inte konfigurerad och inte är synlig för användare.

#### Konfigurera och publicera en egen mall

1.  Välj den nya mallen från den **mallar** sida i Azure-hanteringsportalen.

2.  Från den **mallen har lagts** snabbt startsida klickar du på **börja** från steg 1, **Konfigurera rättigheter för användare och grupper,** klicka sedan på **Kom igång nu** eller **lägga till**, och Välj användare och grupper som har behörighet att använda innehåll som skyddas av den nya mallen.

    > [!NOTE]
    > Användare eller grupper som du väljer måste ha en e-postadress. Det här är nästan alltid fallet men i en enkel testning miljö kan du behöva lägga till e-postadresser till användarkonton eller grupper i en produktionsmiljö.

    Det bästa sättet att använda grupper i stället för användare som underlättar hanteringen av mallar. Om du har Active Directory lokalt och synkroniseras till Azure AD kan du använda e-postaktiverade grupper som är säkerhetsgrupper och distributionsgrupper. Om du vill ge behörighet att alla användare i organisationen ska det vara enklare att kopiera en av standardmallarna som i stället för att ange flera grupper. Mer information finns i [Så här kopierar du en mall](../Topic/Configuring_Custom_Templates_for_Azure_Rights_Management.md#BKMK_HowToCopyTemplates) i det här avsnittet.

    > [!TIP]
    > Du kan senare lägga till användare från utanför organisationen i mallen med hjälp av den [Windows PowerShell-modul för Azure Rights Management](https://technet.microsoft.com/library/jj585012.aspx) och använder en av följande metoder:
    > 
    > -   **Export, redigera och importera den uppdaterade mallen**:  Detta är det enklaste sättet att lägga till externa användare i en befintlig mall som innehåller andra grupper. Använd den [Export AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727078.aspx) cmdlet när du vill exportera mall till en. CSV-fil som du kan redigera för att lägga till externa e-postadresser användarna och deras rättigheter till befintliga grupper och rättigheter. Använd den [Importera AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727077.aspx) cmdlet när du vill importera ändringen tillbaka till Azure RMS.
    > -   **Använd rättigheter definition objekt för att uppdatera en mall**:    Ange externa e-postadresser och deras rättigheter i ett rättigheter definition objekt som du sedan använder för att uppdatera mallen. Du anger rättigheter definition objektet med hjälp av den [Ny AadrmRightsDefinition](https://msdn.microsoft.com/library/azure/dn727080.aspx) cmdlet när du vill skapa en variabel och ange den här variabeln till parametern - RightsDefinition med den [mängd AadrmTemplateProperty](https://msdn.microsoft.com/library/azure/dn727076.aspx) cmdlet när du vill ändra en befintlig mall. Men om du lägger till dessa användare i en befintlig mall, måste du också definiera rättigheter definition objekt för befintliga grupper i mallarna och inte bara de nya, externa användarna.

3.  Klicka på knappen Nästa och sedan tilldela en av de angivna rättigheterna till valda användare och grupper.

    Använd visas beskrivning för mer information om varje höger (och anpassade rättigheter). Mer detaljerad information finns också i [Konfigurera användningsrättigheter för Azure Rights Management](../Topic/Configuring_Usage_Rights_for_Azure_Rights_Management.md). Program som stöder RMS kan dock variera i hur de implementerar dessa rättigheter. Deras dokumentationen och göra egna tester med program som användare använder för att kontrollera problemet innan du distribuerar mallen för användare. Om du vill göra den här mallen visas bara administratörer för den här testning se den här mallen avdelningar mall (steg 6).

4.  Om du har valt **anpassade**, klicka på knappen Nästa och väljer sedan de anpassade rättigheterna.

    Men du kan använda en kombination av individuella rättigheter som är tillgängliga i vissa program, ha vissa rättigheter beroenden på andra enskilda rättigheter. När detta är fallet väljs automatiskt beroende rättigheter.

    > [!TIP]
    > Du kan lägga till den **Kopiera och extrahera innehåll** höger och tilldela det valda administratörer eller personal i andra roller som har ansvar för återställning av information. Bevilja denna rätt kan ta bort skyddet om det behövs från filer och e-postmeddelanden som skyddas med hjälp av den här mallen. Denna möjlighet att ta bort skyddet på nivån mall ger mer detaljerade kontroll än med hjälp av funktionen super-användare.

5.  Klicka på Slutför.

6.  Om du vill att mallen ska visas för en delmängd användare när de visas en lista över mallar i program: Klicka på **omfattning** att konfigurera detta som en mall för avdelningar och klicka på **Kom igång nu**. Annars går du till steg 9.

    Mer information om avdelningar mallar: Som standard är alla användare i katalogen Azure se alla publicerade mallar och de kan markera dem från program när de vill skydda innehåll. Om du vill att vissa användare endast finns några publicerade mallar måste du omfattningen mallar för dessa användare. Sedan ska endast dessa användare kunna välja mallarna. Andra användare som du inte anger visas inte mallarna och därför kan inte välja dem. Den här metoden kan göra att välja rätt mall enklare för användare, särskilt när du skapar du mallar som ska användas av grupper eller avdelningar. Användare se de mallar som har utformats för dem.

    Exempel: du har skapat en mall för hr-avdelningen som gäller endast läsbehörighet för medlemmar i avdelningen ekonomi. Så att endast medlemmar i hr-avdelningen kan använda den här mallen när de använder delningsapplikation Rights Management, namngiven omfattning mallen för e-post-aktiverade gruppen Personal. Endast medlemmar i den här gruppen finns och kan tillämpa sedan den här mallen.

7.  På den **mall SYNBARHETEN** väljer användare och grupper som kommer att kunna se och välj mallen enlightened RMS-program. Som måste före säkerhetsskäl, Använd grupper i stället för användare och grupper eller användare som du väljer ha en e-postadress.

8.  Klicka på knappen Nästa och Bestäm om du behöver för att konfigurera programkompatibiliteten avdelningar mallen för. Om du, klickar på **PROGRAMKOMPATIBILITETEN**, markerar du rutan och klicka på **fullständig**.

    Varför kan du behöva konfigurera programkompatibiliteten? Inte alla program kan stödja avdelningar mallar. Om du vill göra det autentisera programmet först med RMS-tjänsten innan du hämtar mallar. Om autentiseringen inte uppstår, som standard hämtas ingen avdelningar mallar. Du kan åsidosätta detta genom att ange att alla avdelningar mallar ska hämta, genom att konfigurera programkompatibiliteten och välja den **Visa den här mallen för alla användare när program inte stöder användaridentitet** kryssrutan.

    Exempel: Om du inte konfigurerar programkompatibiliteten på avdelningar mallen i vår personal exempel endast användare på hr-avdelningen avdelningar mallen visas när de använder programmet RMS-delning, men inga användare se avdelningar mallen när de använder Outlook Web Access (OWA) från Exchange Server 2013 eftersom Exchange OWA och Exchange ActiveSync för närvarande inte stöder avdelningar mallar. Om du åsidosätta den här standardfunktionen genom att konfigurera programkompatibiliteten endast användare på hr-avdelningen avdelningar mallen visas när de använder RMS-delning program, men alla användare se avdelningar mallen när de använder Outlook Web Access (OWA). Om användare använder OWA eller Exchange ActiveSync från Exchange Online, alla användare ser avdelningar mallar eller inga användare ser avdelningens mallar, baserat på mallstatus (arkivering eller publicerade) i Exchange Online.

    > [!NOTE]
    > Om du har program som inte ännu stöder avdelningar mallar kan du använda en [RMS mall hämta skriptet](http://go.microsoft.com/fwlink/?LinkId=524506) eller andra verktyg för att distribuera mallarna till mappen lokala RMS-klienten. Dessa program visas sedan korrekt avdelningar mallar till användare och grupper som du valt för mallen omfång:
    > 
    > -   För Office 2010 mappen klienten är **%localappdata%\Microsoft\DRM\Templates**.
    > -   Du kan kopiera och klistra in mallfiler till andra datorer från en klientdator som har laddat ned alla mallar.
    > 
    > Office 2016 internt stöder avdelningar mallar och så gör Office 2013 med de senaste uppdateringarna för Office ([KB 3054853](https://support.microsoft.com/kb/3054853)).

9. Klicka på **Konfigurera** och lägga till ytterligare språk som användare använder samt namn och beskrivning av mallen i respektive språk. När du har flera språk användare är det viktigt att lägga till varje språk som de använder och ange ett namn och en beskrivning på detta språk. Användarna ser sedan namn och beskrivning av mallen på samma språk som deras klientoperativsystem som säkerställer de förstår princip som tillämpas på ett dokument eller e-postmeddelande. Om det finns ingen matchning med sina klientoperativsystem, hamnar namn och beskrivning som finns i de till språk och beskrivning som du angett när du först skapade mallen.

    Markera om du vill ändra inställningarna för följande:

    |Inställningen|Mer information|
    |-----------------|-------------------|
    |**innehåll upphör att gälla**|Ange ett datum eller antal dagar för den här mallen när filer som skyddas av mallen inte öppna. Du kan ange ett datum eller ange ett antal dagar från den tid som skydd används till filen.<br /><br />När du anger ett datum är effektiva ny i den aktuella tidszonen.|
    |**offline-åtkomst**|Använd den här inställningen för att alla säkerhetskrav som du har mot kravet på att användaren måste kunna öppna skyddade filer när de inte har Internetanslutning.<br /><br />Om du anger att innehållet är inte tillgängligt utan Internet-anslutning eller innehållet är endast tillgänglig för ett angivet antal dagar, när det här tröskelvärdet uppnås användare måste vara igen autentiserad och deras åtkomst loggas. När detta händer om sina autentiseringsuppgifter inte cachelagras, uppmanas användarna att logga in innan de kan öppna filen.<br /><br />Förutom ny verifiering är principen och gruppmedlemskap för användare nytt utvärderade. Det innebär att användare kan uppleva olika åtkomst resultat för samma fil om det finns ändringar i principen eller gruppmedlemskap från när de senast komma åt filen.|

10. När du är säker på att mallen har konfigurerats korrekt för dina användare klickar du på **publicera** göra mallen synliga för användare och klicka sedan på **Spara**.

11. Klicka på knappen Bakåt i hanteringsportalen att återgå till den **mallar** sidan där mallen har en uppdaterad status för nu **publicerade**.

Om du vill göra ändringar i mallen, markerar du den och använda Snabbstart steg igen. Eller välj ett av följande alternativ:

-   Lägga till fler användare och grupper och definiera rättigheterna för dessa användare och grupper: Klicka på **rättigheter**, klicka på **lägga till**.

-   Ta bort användare eller grupper som du har valt: Klicka på **rättigheter**, Välj användare eller grupp i listan och klicka sedan på **Ta bort**.

-   Så här ändrar du vilka användare kan se mallar att välja dem från program: Klicka på **omfattning**, klicka på **lägga till** eller **Ta bort**, eller **PROGRAMKOMPATIBILITETEN**.

-   Så här gör mallen inte längre visas för alla användare: Klicka på **Konfigurera**, klickar du på **ARKIVET**, och klicka sedan på **Spara**.

-   Så här gör andra konfigurationsändringar: Klicka på **Konfigurera**, gör ändringarna och klicka sedan på **Spara**.

> [!WARNING]
> När du gör ändringar i en mall som sparats tidigare ser inte klienter ändringarna i mallen förrän mallar uppdateras på sina datorer. Mer information finns i [Uppdatera mallar för användare](../Topic/Configuring_Custom_Templates_for_Azure_Rights_Management.md#BKMK_RefreshingTemplates) i det här avsnittet.

## <a name="BKMK_HowToCopyTemplates"></a>Så här kopierar du en mall
Om du vill skapa en ny mall som har ungefär samma inställningar för en befintlig mall markerar du den ursprungliga mallen på den **mallar** klickar du på **Kopiera**, ange ett unikt namn och göra ändringar som du behöver.

> [!IMPORTANT]
> När du kopierar en mall i **publicerade** eller **arkiverade** status kopieras även. Så om du kopierar en mall för publicerade omedelbar status ska publiceras, såvida du inte ändrar den.

Du kan kopiera mallar och standardmallarna som. Det bästa sättet att kopiera en av standardmallarna som i stället för att skapa en ny egen mall om du vill använda mallen för att ge behörighet att alla användare i organisationen. Den här metoden innebär att du inte behöver skapa eller Välj flera grupper att ange alla användare. I det här scenariot, måste du ange ett nytt namn och en beskrivning för mallen kopierade för ytterligare språk.

## <a name="BKMK_HowToArchiveTemplates"></a>Ta bort (Arkiv) mallar
Kan inte tas bort standardmallarna som, men de kan arkiveras så att användarna inte ser dem.

På samma sätt om du har publicerat en anpassad mall och inte längre vill att användare ska kunna se den, du kan redigera mallen och välja **ARKIVET** och **Spara** från den **Konfigurera** sidan. Eller också kan du välja den från den **mallar** sidan och välj **ARKIVET**.

Eftersom du inte kan redigera standardmallar, om du vill arkivera dessa mallar, måste du använda den **ARKIVET** alternativet från den **mallar** sidan. Du kan inte arkivera Outlook **Vidarebefordra inte** alternativet.

#### Ta bort en standardmall

-   Från den **mallar** markerar standardmall, och klicka på **ARKIVET**.

Statusen ändras från **publicerade** till **arkiverade**. Om du ändrar dig, väljer mallen och klicka på **publicera**.

## <a name="BKMK_RefreshingTemplates"></a>Uppdatera mallar för användare
När du använder Azure RMS hämta mallar automatiskt till klientdatorer så att användarna kan välja dem från sina program. Du kanske måste vidta ytterligare åtgärder om du ändrar mallar:

|Program eller en tjänst|Hur mallar uppdateras när ändringar|
|---------------------------|---------------------------------------|
|Exchange Online|Manuell konfiguration krävs för att uppdatera mallar.<br /><br />Expandera avsnittet nedan för att konfigureringen [Exchange Online endast: Så här konfigurerar du Exchange för att hämta ändrade mallar](../Topic/Configuring_Custom_Templates_for_Azure_Rights_Management.md#BKMK_ExchangeOnlineTemplatesUpdate).|
|Office 365|Uppdateras automatiskt – inga ytterligare åtgärder krävs.|
|Office 2016 och Office 2013<br /><br />RMS-delning program för Windows|Uppdateras automatiskt – enligt ett schema:<br /><br />-   För dessa senare versioner av Office: Standardintervallet är varje 7 dagar.<br />-   För RMS-delning program för Windows: Från och med version 1.0.1784.0 är standardintervallet varje dag. Tidigare versioner har ett standardvärde uppdateringsintervall varje 7 dagar.<br /><br />Expandera avsnittet nedan om du vill uppdatera tidigare än schemat [Office 2016 Office 2013 och RMS-delning program för Windows: Hur du tvingar fram en uppdatering för en ändrad anpassade mall](#BKMK_Office2013ForceUpdate).|
|Office 2010|Uppdateras när användaren loggar in.<br /><br />Om du vill uppdatera, be eller tvinga användare att logga ut och logga in igen igen. Eller finns i följande avsnitt [Office-2010: Hur du tvingar fram en uppdatering för en ändrad anpassade mall](#BKMK_Office2010ForceUpdate).|
För mobila enheter som använder RMS-delning program mallar hämtas automatiskt (och uppdateras vid behov) utan ytterligare konfiguration krävs.

### <a name="BKMK_ExchangeOnlineTemplatesUpdate"></a>Exchange Online endast: Så här konfigurerar du Exchange för att hämta ändrade mallar
Om du redan har konfigurerat Information Rights Management (IRM) för Exchange Online hämta anpassade mallar inte för användare förrän du göra följande ändringar med Windows PowerShell i Exchange Online.

> [!NOTE]
> Mer information om hur du använder Windows PowerShell i Exchange Online, se [med hjälp av PowerShell med Exchange Online](https://technet.microsoft.com/library/jj200677%28v=exchg.160%29.aspx).

Du måste utföra den här proceduren varje gång du ändrar en mall.

##### Så här uppdaterar du mallar för Exchange Online

1.  Med Windows PowerShell i Exchange Online kan ansluta till tjänsten:

    1.  Ange ditt Office 365-användarnamn och lösenord:

        ```
        $Cred = Get-Credential
        ```

    2.  Ansluta till Exchange Online-tjänsten genom att köra följande två kommandon:

        ```
        $Session = New-PSSession -ConfigurationName Microsoft.Exchange -ConnectionUri https://ps.outlook.com/powershell/ -Credential $Cred -Authentication Basic –AllowRedirection
        ```

        ```
        Import-PSSession $Session
        ```

2.  Använd den [Importera RMSTrustedPublishingDomain](http://technet.microsoft.com/library/jj200724%28v=exchg.160%29.aspx) cmdlet importera betrodda publicering domänen (betrodda Publiceringsdomänen) från Azure RMS:

    ```
    Import-RMSTrustedPublishingDomain -Name "<TPD name>" -RefreshTemplates -RMSOnline
    ```
    Om du exempelvis betrodda Publiceringsdomänen-namnet är **Online RMS - 1** (en typisk namn för många organisationer), ange: **Import-RMSTrustedPublishingDomain -Name "RMS Online - 1" -RefreshTemplates -RMSOnline**

    > [!NOTE]
    > Kontrollera ditt betrodda Publiceringsdomänen namn, du kan använda den [Get-RMSTrustedPublishingDomain](http://technet.microsoft.com/library/jj200707%28v=exchg.160%29.aspx) cmdlet.

3.  Vänta några minuter för att bekräfta att mallarna har importerats och kör sedan den [Get-RMSTemplate](http://technet.microsoft.com/library/dd297960%28v=exchg.160%29.aspx) cmdlet och ange alla. Exempel:

    ```
    Get-RMSTemplate -TrustedPublishingDomain "RMS Online - 1" -Type All
    ```
    > [!TIP]
    > Det är praktiskt att spara en kopia av utdata så att du kan enkelt kopiera mallen namn eller GUID om du senare arkivera en mall.

4.  För varje importerade mallen som du vill ska vara tillgängliga i Outlook Web App måste du använda den [mängd RMSTemplate](http://technet.microsoft.com/library/hh529923%28v=exchg.160%29.aspx) cmdlet och ange vilket distribuerad:

    ```
    Set-RMSTemplate -Identity "<name  or GUID of the template>" -Type Distributed
    ```
    Eftersom Outlook Web Access cachelagrar Användargränssnittet 24 timmar, kan användare inte finns i den nya mallen för upp till en dag.

Dessutom du arkivera en mall (anpassad eller standard) och Använd Exchange Online med Office 365 användare kommer att kunna se de arkiverade mallarna om de använder Outlook Web App eller mobila enheter som använder Exchange ActiveSync-protokollet.

Så att användare inte längre visas mallarna ansluta till tjänsten med Windows PowerShell i Exchange Online och sedan använda den [mängd RMSTemplate](http://technet.microsoft.com/library/hh529923%28v=exchg.160%29.aspx) cmdlet genom att köra följande kommando:

```
Set-RMSTemplate -Identity "<name or GUID of the template>" -Type Archived
```

### <a name="BKMK_Office2013ForceUpdate"></a>Office 2016 Office 2013 och RMS-delning program för Windows: Hur du tvingar fram en uppdatering för en ändrad anpassade mall
Du kan ändra schema för automatisk så att ändrade mallar uppdateras på datorer oftare än standardvärdet genom att redigera registret på datorer som kör Office 2016, Office 2013 eller Rights Management (RMS) delning för Windows. Du kan också göra så att en uppdatering genom att ta bort befintliga data i ett registervärde.

> [!WARNING]
> Om du använder Registereditorn fel kan du orsaka allvarliga problem som kräver att du måste installera om operativsystemet. Microsoft kan inte garantera att du kan lösa problem som uppstår om du använder Registereditorn på ett felaktigt sätt. Använd Registereditorn på egen risk.

##### Så här ändrar du automatiskt schema

1.  Med hjälp av en Registereditorn, skapa och ange en av följande registervärden:

    -   Ange en uppdateringsfrekvensen i dagar (minst 1 dag):  Skapa ett nytt registervärde med namnet **TemplateUpdateFrequency** och definiera ett heltal för de data som anger frekvensen i dagar för att hämta alla ändringar i en mall för hämtade. Använder du följande tabell för att hitta registret sökvägen om du vill skapa nya registervärdet.

        |Sökväg till register|Typ|Värde|
        |------------------------|-------|---------|
        |HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC|REG_DWORD|TemplateUpdateFrequency|

    -   Att ange en uppdateringsfrekvensen i sekunder (minst 1 sekund):  Skapa ett nytt registervärde med namnet **TemplateUpdateFrequencyInSeconds** och definiera ett heltal för de data som anger frekvensen i sekunder att hämta alla ändringar i en mall för hämtade. Använder du följande tabell för att hitta registret sökvägen om du vill skapa nya registervärdet.

        |Sökväg till register|Typ|Värde|
        |------------------------|-------|---------|
        |HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC|REG_DWORD|TemplateUpdateFrequencyInSeconds|

    Kontrollera att du skapar och ange en av dessa registervärden inte båda. Om båda förekommer **TemplateUpdateFrequency** ignoreras.

2.  Gå till nästa procedur om du vill tvinga fram en uppdatering av mallar. Annars startar du om ditt Office-program och instanser av filen Explorer nu.

##### Tvingar fram en uppdatering

1.  Använd Registereditorn och ta bort data för den **LastUpdatedTime** värde. Data kan till exempel visa **2015-04-20T15:52**ta bort 2015-04-20T15:52 så att inga data visas. Använder du följande tabell för att hitta sökvägen registret för att ta bort det här värdet registerdata.

    |Sökväg till register|Typ|Värde|
    |------------------------|-------|---------|
    |HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC\ &lt; MicrosoftRMS_FQDN &gt; \Template|REG_SZ|LastUpdatedTime|
    > [!TIP]
    > I registret-sökvägen *&lt; MicrosoftRMS_FQDN &gt;* refererar till Microsoft RMS-tjänsten FQDN. Om du vill kontrollera detta värde:
    > 
    > 1.  Kör den [Get-AadrmConfiguration](https://msdn.microsoft.com/library/windowsazure/dn629410.aspx) cmdlet för Azure RMS. Om du inte redan installerat Windows PowerShell-modul för Azure RMS, se [Installera Windows PowerShell för Azure Rights Management](../Topic/Installing_Windows_PowerShell_for_Azure_Rights_Management.md).
    > 2.  Från utdata, identifiera den **LicensingIntranetDistributionPointUrl** värde.
    > 
    >     Exempel: **LicensingIntranetDistributionPointUrl: https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com/_wmcs/licensing**
    > 3.  Ta bort från värdet **https://** och **/_wmcs/licensing** från strängen. Återstående värdet är Microsoft RMS-tjänsten FQDN. I vårt exempel är FQDN för Microsoft RMS-tjänsten följande värde:
    > 
    >     **5c6bb73b 1038-4eec-863d-49bded473437.rms.na.aadrm.com**

2.  Ta bort följande mapp och alla filer som den innehåller: **%localappdata%\Microsoft\MSIPC\Templates**

3.  Starta om Office-program och instanser av filen Explorer.

### <a name="BKMK_Office2010ForceUpdate"></a>Office-2010: Hur du tvingar fram en uppdatering för en ändrad anpassade mall
Du kan ange ett värde så att ändrade mallar uppdateras på datorer utan att behöva vänta för användare att logga ut och sedan på genom att redigera registret på datorer som kör Office 2010. Du kan också göra så att en uppdatering genom att ta bort befintliga data i ett registervärde.

> [!WARNING]
> Om du använder Registereditorn fel kan du orsaka allvarliga problem som kräver att du måste installera om operativsystemet. Microsoft kan inte garantera att du kan lösa problem som uppstår om du använder Registereditorn på ett felaktigt sätt. Använd Registereditorn på egen risk.

##### Ändra uppdateringsfrekvensen

1.  Använd Registereditorn och skapa ett nytt registervärde med namnet **UpdateFrequency** och definiera ett heltal för de data som anger frekvensen i dagar för att hämta alla ändringar i en mall för hämtade. Använder du följande tabell för att hitta registret sökvägen om du vill skapa nya registervärdet.

    |Sökväg till register|Typ|Värde|
    |------------------------|-------|---------|
    |HKEY_CURRENT_USER\Software\Microsoft\MSDRM\TemplateManagement|REG_DWORD|UpdateFrequency|

2.  Gå till nästa procedur om du vill tvinga fram en uppdatering av mallar. Annars startar du om Office-programmen nu.

##### Tvingar fram en uppdatering

1.  Använd Registereditorn och ta bort data för den **LastUpdatedTime** värde. Data kan till exempel visa **2015-04-20T15:52**ta bort 2015-04-20T15:52 så att inga data visas. Använder du följande tabell för att hitta sökvägen registret för att ta bort det här värdet registerdata.

    |Sökväg till register|Typ|Värde|
    |------------------------|-------|---------|
    |HKEY_CURRENT_USER\Software\Microsoft\MSDRM\TemplateManagement|REG_SZ|lastUpdatedTime|

2.  Ta bort följande mapp och alla filer som den innehåller: **%localappdata%\Microsoft\MSIPC\Templates**

3.  Starta om Office-program.

## <a name="BKMK_PowerShellTemplates"></a>Windows PowerShell-referens
Allt du kan göra i Azure-hanteringsportalen att skapa och hantera mallar som du kan göra från kommandoraden, med hjälp av Windows PowerShell. Du kan också exportera och Importera mallar, så att du kan kopiera mallar mellan innehavare eller utför massredigering komplexa egenskaper i mallar, till exempel multilingual namn och beskrivningar.

Du kan också använda exportera och importera om du vill säkerhetskopiera och återställa dina egna mallar som bästa praxis, regelbundet säkerhetskopiera dina egna mallar, så att om du gör en ändring som inte är avsedd kan du enkelt återgå till en tidigare version.

> [!IMPORTANT]
> Om du vill använda Windows PowerShell för att skapa och hantera Azure RMS principmallar du har version 2.0.0.0 av den [Windows PowerShell-modul för Azure RMS](http://go.microsoft.com/fwlink/?LinkId=257721).
> 
> Om du tidigare har installerat Windows PowerShell-modul kör följande kommando i ett PowerShell-fönster för att kontrollera versionsnumret: `(Get-Module aadrm -ListAvailable).Version`

Instruktioner för installationen finns i [Installera Windows PowerShell för Azure Rights Management](../Topic/Installing_Windows_PowerShell_for_Azure_Rights_Management.md).

Cmdlet: ar som stöder skapa och hantera mallar:

-   [Lägg till AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727075.aspx)

-   [Exportera AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727078.aspx)

-   [Hämta AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727079.aspx)

-   [Hämta AadrmTemplateProperty](https://msdn.microsoft.com/library/azure/dn727081.aspx)

-   [Importera AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727077.aspx)

-   [Ny AadrmRightsDefinition](https://msdn.microsoft.com/library/azure/dn727080.aspx)

-   [Ta bort AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727082.aspx)

-   [Ange AadrmTemplateProperty](https://msdn.microsoft.com/library/azure/dn727076.aspx)

## Nästa steg
När du har konfigurerat mallar för Azure Rights Management kan använda den [Översikt över Azure Rights Management-distribution](../Topic/Azure_Rights_Management_Deployment_Roadmap.md) att kontrollera om det finns andra konfigurationssteg som du kan göra innan du lansera [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] för användare och administratörer. Om det finns inga andra konfigurationssteg som du behöver för att, se [Använda Azure Rights Management](../Topic/Using_Azure_Rights_Management.md) operativa riktlinjer för att stödja en lyckad distribution för din organisation.

## Se även
[Konfigurera Azure Rights Management](../Topic/Configuring_Azure_Rights_Management.md)

