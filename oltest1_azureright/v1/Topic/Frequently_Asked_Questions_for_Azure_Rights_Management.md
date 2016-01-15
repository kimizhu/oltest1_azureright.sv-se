---
description: na
keywords: na
title: Frequently Asked Questions for Azure Rights Management
search: na
ms.date: na
ms.service: rights-management
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 71ce491f-41c1-4d15-9646-455a6eaa157d
---
# Vanliga fr&#229;gor om Azure Rights Management
Vissa vanliga frågor om Microsoft [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)], även kallad Azure RMS:

## Vad behöver jag att distribuera Azure RMS och hur hämta vi?
Kontrollera först [Krav för Azure Rights Management](../Topic/Requirements_for_Azure_Rights_Management.md), som innehåller information om alternativen för prenumerationen i molnet, hur du kan använda din lokala servrar med Azure RMS, vilka distributionsscenarier är för närvarande inte stöds, vilka enheter och program stöd Azure RMS och en länk om du behöver en lista över IP-adresser och domännamn för brandväggar och proxyservrar. Du kanske också vill kontrollera de övriga ämnena i det [Kom igång med Azure Rights Management](../Topic/Getting_Started_with_Azure_Rights_Management.md) avsnitt för att få en grundläggande förståelse för hur [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] kan hjälpa dig att skydda din organisations data, hur det fungerar med program, hur den jämförs med den lokala versionen av Active Directory Rights Management och förstå termer och förkortningar som är specifika för [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)].

Sedan när du är redo att testa Azure RMS för dig själv eller distribuera den till din organisation kan använda den [Översikt över Azure Rights Management-distribution](../Topic/Azure_Rights_Management_Deployment_Roadmap.md) en lista över steg med länkar till mer information och instruktioner instruktioner.

Om du behöver ytterligare information, resurser och support finns [Information och Support för Azure Rights Management](../Topic/Information_and_Support_for_Azure_Rights_Management.md).

## Kan jag integrera Azure RMS med min lokala servrar?
Ja. Azure RMS kan integreras med dina lokala servrar, till exempel Exchange Server, SharePoint och Windows-filservrar. Om du vill göra detta måste du använda den [Rights Management-koppling](https://technet.microsoft.com/library/dn375964.aspx). Om du är intresserad av filen klassificering infrastruktur (FC) med Windows Server, kan du använda den [RMS-skydd cmdlets](https://technet.microsoft.com/library/mt601315%28v=ws.10%29.aspx). Du kan också synkronisera och federera domänkontrollanterna Active Directory med Azure AD för en mer sömlös autentisering upplevelse för användare, till exempel med hjälp av [Azure AD Connect](http://azure.microsoft.com/documentation/articles/active-directory-aadconnect/).

Azure RMS automatiskt skapar och hanterar XrML certifikat som krävs, så att den inte använda en lokal PKI. Mer information om hur Azure RMS använder certifikat finns i [Information om hur Azure RMS fungerar: Först använda, innehåll skydd, innehåll förbrukning](../Topic/What_is_Azure_Rights_Management_.md#BKMK_Walthrough) i avsnittet den [Vad är Azure Rights Management?](../Topic/What_is_Azure_Rights_Management_.md) artikeln.

## Jag har en hybriddistribution av Exchange med vissa användare på Exchange Online och andra Exchange Server – är det stöds av Azure RMS?
Absolut, och det bra som är användare kommer att kunna skydda och använda skyddad e-post och bifogade filer mellan två Exchange-distributioner sömlöst. För den här konfigurationen [Aktivera Azure RMS](https://technet.microsoft.com/library/jj658941.aspx) och [Aktivera IRM för Exchange Online](https://technet.microsoft.com/library/dn151475%28v=exchg.150%29.aspx), sedan [distribuera och konfigurera RMS-anslutningen](https://technet.microsoft.com/library/dn375964.aspx) för Exchange Server.

## Om jag distribuerar Azure RMS i produktion mitt företag låses i lösningen eller risken att förlora åtkomsten till innehåll som vi skyddat med Azure RMS?
Nej, du alltid förblir kontroll över dina data och kan fortsätta använda den, även om du väljer att inte längre använda Azure RMS. Mer information finns i [Inaktivering och inaktivera Azure Rights Management](../Topic/Decommissioning_and_Deactivating_Azure_Rights_Management.md).

Men innan du inaktiverar distributionen Azure RMS vill vi hör av dig och förstå varför du har gjort detta beslut. Om Azure RMS inte uppfyller dina affärskrav, kontrollera med oss om nya funktioner som är planerat för en nära framtid eller om det finns alternativ. Skicka ett e-postmeddelande till [AskIPTeam@Microsoft.com](mailto:askipteam@microsoft.com?subject=Planning%20to%20decommission%20Azure%20RMS) och vi att uppskatta diskutera dina krav teknisk och affärskrav.

## Kan du styra som användarna kan använda Azure RMS för att skydda innehåll?
Ja, Azure RMS har onboarding användarkontroller för det här scenariot. Mer information finns i [Konfigurera inledande kontroller för en fasindelad distribution](../Topic/Activating_Azure_Rights_Management.md#BKMK_OnboardingControls) i avsnittet den [Aktivera Azure Rights Management](../Topic/Activating_Azure_Rights_Management.md) artikeln.

## Hindrar användare från att dela skyddade dokument med specifika organisationer?
En av de största fördelarna med Azure RMS är stöder business-to-business samarbete utan att konfigurera explicita förtroenden för varje partnerorganisation eftersom Azure AD tar hand om autentisering för dig.

Det finns inget administrationsalternativ för att hindra användare från att dela dokument på ett säkert sätt med specifika organisationer. Exempelvis kan du vill blockera en organisation som du inte litar eller som har ett konkurrerande företag. Förhindrar att Azure RMS skicka skyddade dokument till användare i den här organisationer inte särskilt meningsfullt eftersom användarna kan sedan dela dokument oskyddade, som troligen är det sista som du vill i det här scenariot! Du kan till exempel inte kan identifieras som delar företagets konfidentiella dokument med vilka användare i dessa företag som du kan göra när dokumentet (eller e-post) skyddas av Azure RMS.

## När jag delar ett skyddat dokument med någon utanför mitt företag hur användaren hämta autentiserad?
Azure RMS använder alltid ett Azure Active Directory-konto och en tillhörande e-postadress för autentisering av användare, vilket gör business-to-business samarbete sömlös för administratörer. Om den andra organisationen använder Azure-tjänster, har användare redan konton i Azure Active Directory, även om de här kontona skapas och hanteras lokalt och sedan synkroniseras till Azure.  Om organisationen har Office 365 under omfattar, använder tjänsten också Azure Active Directory för användarkonton.  Om användarens organisation saknar hanterade konton i Azure kan användarna kan registrera dig för [RMS för individer](https://technet.microsoft.com/library/dn592127.aspx), vilket skapar en ohanterad Azure-klient- och katalogtjänster för organisationen med ett konto för användaren, så att användaren kan sedan autentiseras för Azure RMS.

Autentiseringsmetod för dessa konton kan variera beroende på hur administratören i den andra organisationen har konfigurerat Azure Active Directory-konton. De kan till exempel använda lösenord som har skapats för dessa konton, multifaktorautentisering (MFA), federation eller lösenord som har skapats i Active Directory Domain Services och sedan synkroniseras till Azure Active Directory.

## Kan jag lägga till användare från utanför mitt företag anpassade mallar?
Ja.  Skapa egna mallar som slutanvändarna (och administratörer) kan välja från program som gör det snabbt och enkelt att tillämpa informationsskydd med hjälp av fördefinierade principer som du anger. En av inställningarna i mallen är som kan få tillgång till innehållet och du kan ange användare och grupper från inom organisationen och användare från utanför organisationen.

Om du vill ange användare från utanför din organisation använder den [Windows PowerShell-modulen för Azure Rights Management](https://technet.microsoft.com/library/jj585012.aspx). Du kan använda något av dessa alternativ:

-   **Export, redigera och importera den uppdaterade mallen**:  Detta är den enklaste metoden om du vill lägga till dessa externa användare i en befintlig mall som innehåller andra grupper. Använd den [Export AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727078.aspx) cmdlet när du vill exportera mall till en. CSV-fil som du kan redigera för att lägga till externa e-postadresser användarna och deras rättigheter till befintliga grupper och rättigheter. Använd den [Importera AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727077.aspx) cmdlet när du vill importera ändringen tillbaka till Azure RMS.

-   **Använder ett objekt för definition av rättigheter att skapa eller uppdatera en mall för**:    Ange externa e-postadresser och deras rättigheter i ett rättigheter definition objekt, som du sedan använder för att skapa eller uppdatera en mall. Rättigheter definition objektet anges med hjälp av den [Ny AadrmRightsDefinition](https://msdn.microsoft.com/library/azure/dn727080.aspx) cmdlet för att skapa en variabel och ange sedan den här variabeln till parametern - RightsDefinition med den [Lägg till AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727075.aspx) (för en ny mall) eller [Set AadrmTemplateProperty](https://msdn.microsoft.com/library/azure/dn727076.aspx) cmdlet (om du ändrar en befintlig mall). Men om du lägger till dessa användare i en befintlig mall, behöver du definiera rättigheter definition objekt för befintliga grupper i mallar och inte bara de externa användarna.

Mer information om anpassade mallar finns [Konfigurera anpassade mallar för Azure Rights Management](../Topic/Configuring_Custom_Templates_for_Azure_Rights_Management.md).

## Vilka enheter och vilka filtyper som stöds av Azure RMS?
En lista över enheter som stöds finns i [Klientenheter som stöd för Azure RMS](../Topic/Requirements_for_Azure_Rights_Management.md#BKMK_SupportedDevices) i avsnittet den [Krav för Azure Rights Management](../Topic/Requirements_for_Azure_Rights_Management.md) artikeln. Eftersom stöds inte alla enheter kan för närvarande stöder alla funktioner för RMS, måste du också kontrollera att den [Klienten enhetsfunktioner](../Topic/Requirements_for_Azure_Rights_Management.md#BKMK_ClientCapabilities) tabellen i avsnittet om samma.

Azure RMS har stöd för alla filtyper. För text, bild, Microsoft Office (Word, Excel, PowerPoint) filer, PDF-filer och vissa andra filtyper för program ger Azure RMS internt skydd som innehåller både kryptering och tillämpning av rättigheter (behörigheter). För alla andra program och filtyper ger Allmänt skydd filen inkapsling och autentisering för att kontrollera om en användare har behörighet att öppna filen.

En lista med filnamnstillägg som stöds av Azure RMS finns på [stöds filtyper och filnamnstillägg](http://technet.microsoft.com/library/dn339003.aspx) avsnitt i den [Rights Management administratörsguiden för delningsapplikationen](http://technet.microsoft.com/library/dn339003.aspx). Filnamnstillägg som visas inte stöds med hjälp av RMS-delningsprogrammet som automatiskt gäller allmänt skydd för de här filerna.

## När stöder migrering från AD RMS?
Inledningsvis stöder inte Azure RMS migrering från en lokal distribution av Rights Management, till exempel AD RMS. Men stöds nu.

Mer information finns i [Migrera från AD RMS till Azure Rights Management](../Topic/Migrating_from_AD_RMS_to_Azure_Rights_Management.md).

## Vi vill använda BYOK med Azure RMS men lära dig att detta inte är kompatibel med Exchange Online – vad är din råd?
Låt inte den här aktuell begränsning fördröjning distributionen Azure RMS. Om du har Exchange Online och vill använda gör en egen nyckel (BYOK), rekommenderar vi att du distribuerar Azure RMS i nyckelhantering standardläget nu där Microsoft skapar och hanterar din nyckel. På så sätt kan du få alla fördelar med att skydda viktiga filer och e-post nu, med alternativet för att flytta till BYOK senare (till exempel när Exchange Online stöder BYOK).

Om företagsprinciperna måste du använda en maskinvarusäkerhetsmodul (HSM) och det annars skulle blockera din Azure RMS-distribution, men är ett annat alternativ att distribuera Azure RMS med BYOK nu med begränsad RMS-funktionalitet för Exchange. Mer information finns i [BYOK pricing and restrictions](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_Pricing) under den [Planera och implementera din Azure Rights Management innehavaren nyckel](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md) ämne.

## En funktion som du letar efter verkar arbeta med SharePoint skyddade bibliotek – finns stöd för funktionen Mina planerade?
För närvarande skyddade SharePoint stöder RMS-skyddade dokument med hjälp av IRM bibliotek som inte stöder anpassade mallar, dokument och vissa andra funktioner.  Mer information, expandera den   [SharePoint Online och OneDrive för företag: IRM-konfiguration](../Topic/Configuring_Applications_for_Azure_Rights_Management.md#BKMK_SharePointOnline) i avsnittet den [Hur program stöd för Azure Rights Management](../Topic/How_Applications_Support_Azure_Rights_Management.md) artikeln.

Om du är intresserad av i en specifik funktion som ännu inte stöds, se till att hålla ett öga på meddelanden den [RMS-teamets blogg](http://blogs.technet.com/b/rms/).

## Konfigurera en enhet för företag i SharePoint Online så att användare kan dela sina filer säkert med personer i och utanför företaget?
Som standard konfigurera som Office 365-administratör du inte. användarna göra.

Precis som en SharePoint-webbplatsens administratör aktiverar och konfigurerar IRM för en SharePoint-dokumentbibliotek som de äger, är OneDrive för företag utformade för användare att aktivera och konfigurera IRM för sina egna OneDrive för Business-biblioteket.  Men med hjälp av PowerShell, kan du göra detta för dem. Instruktioner, expandera den [SharePoint Online och OneDrive för företag: IRM-konfiguration](../Topic/Configuring_Applications_for_Azure_Rights_Management.md#BKMK_SharePointOnline)  i avsnittet den [Konfigurera program för Azure Rights Management](../Topic/Configuring_Applications_for_Azure_Rights_Management.md) artikeln.

## Har du alla tips och tricks RMS distributionen?
Efter att övervaka många distributioner och lyssna på våra kunder, partner och uppstå konsulter och tekniker – en av de största tips som vi kan vidarebefordra från: **Design och distribuera principer för enkla rättigheter**.

Eftersom Azure RMS stöder delning på ett säkert sätt med alla kan råd du att bli ambitiösa med räckhåll information skydd. Men vara försiktig med principer för användarrättigheter. För många organisationer utgör kommer den största inverkan på verksamheten från förhindrar läckage av data genom att använda standard rättighetsprincipmall som begränsar åtkomsten till personer i organisationen. Naturligtvis, du kan få mycket mer detaljerad än som om du behöver – förhindra personer skrivs ut, redigera osv. Behåll mer detaljerade begränsningarna som undantag för dokument som verkligen behöver säkerhet på hög nivå men inte implementerar dessa mer restriktiva principer på en dag, men plan för mer stegvis.

## Vilka funktioner som kan eller inte kan användas med olika prenumerationer för Azure RMS?
Det finns vissa skillnader i RMS-funktioner som stöds för betalda prenumerationer som har stöd för Azure RMS (Office 365, Azure RMS Premium och Enterprise Mobility Suite). En lista över dessa finns [erbjudanden för jämförelse av Rights Management Services (RMS)](http://technet.microsoft.com/dn858608).

Kostnadsfri prenumeration som har stöd för Azure RMS (RMS för enskilda användare) har stöd för mycket innehåll som har skyddats av Azure RMS. Mer information finns i [RMS för personer och Azure Rights Management](../Topic/RMS_for_Individuals_and_Azure_Rights_Management.md).

## Var hittar teknisk information om ledigt Azure RMS prenumerationen (RMS för individer), till exempel hur det fungerar i praktiken, så ta kontroll av konton och kan inte användas som domäner?
Du hittar svaren på dessa frågor i den [RMS för personer och Azure Rights Management](../Topic/RMS_for_Individuals_and_Azure_Rights_Management.md) artikeln.

## Hur vi för att få åtkomst till filer som skyddades av en medarbetare som har lämnat organisationen nu?
Använd funktionen super user i Azure RMS, som gör att behöriga användare ha behörigheten Fullständig ägare för alla licenser som har beviljats av organisationens RMS-klienten. Funktionen samma kan auktoriserade tjänster index och inspektera filer efter behov.

Mer information finns i [Konfigurera Super Users för Azure Rights Management och identifiering av tjänster eller återställning av Data](../Topic/Configuring_Super_Users_for_Azure_Rights_Management_and_Discovery_Services_or_Data_Recovery.md).

## Rights Management kan hindra skärmdumpar?
Rights Management blockerar skärmdumpar från de flesta vanliga skärmen avbilda verktyg som hjälper dig för att undvika oavsiktlig eller grund avslöjande av konfidentiell eller känslig information. Det finns många sätt att en användare kan dela data som visas på skärmen och ta en skärmbild är bara en av metoderna. En användare avsiktshantering delning av information som visas kan till exempel ta en bild av den med sin kamera telefon, skriva in data eller bara muntligt vidarebefordra den till någon.

Eftersom de här exemplen visar kan inte teknik enbart alltid hindra användare från att dela data som de inte ska. När Rights Management kan bidra till att skydda viktiga data genom att använda auktorisering och användningsprinciper, ska enterprise rights management lösningen användas med andra kontroller. Till exempel implementera fysiska säkerheten, noggrant skärmbild och övervaka personer som har behörighet för åtkomst till företagets data och investera i utbildning av användarna så att användarna förstår vilka data som inte ska delas.

## Var hittar jag stödjande för Azure RMS, till exempel juridiska, kompatibilitet och servicenivåavtal?
Azure RMS stöder andra tjänster och även beroende av andra tjänster. Om du letar efter information som är relaterad till Azure RMS, men inte om hur du använder Azure RMS-tjänsten kontrollerar du följande resurser:

**Juridisk och integritet:**

-   För information om Microsoft Azure: [Microsoft Azure-avtalet](http://azure.microsoft.com/support/legal/subscription-agreement/)

-   Sekretessinformation om Microsoft Azure: [Sekretesspolicy för Microsoft Azure](http://azure.microsoft.com/support/legal/privacy-statement/)

**Säkerhet, kompatibilitet och granskning:**

Finns det [Säkerhet och efterlevnad krav](../Topic/What_is_Azure_Rights_Management_.md#BKMK_RMScompliance) under den [Vad är Azure Rights Management?](../Topic/What_is_Azure_Rights_Management_.md) ämne. Dessutom:

-   För externa certifikat för Azure RMS: [Microsoft Azure Säkerhetscenter](http://azure.microsoft.com/support/trust-center/)

-   FIPS 140 information: [FIPS 140 verifieringen](https://technet.microsoft.com/library/security/cc750357.aspx)

**Servicenivåavtal:**

-   Servicenivåavtal för Azure RMS med valda landet: [Servicenivåavtal](http://microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&amp;DocumentTypeId=37)

-   Servicenivåavtal för Azure Active Directory: [Servicenivåavtal](http://azure.microsoft.com/support/legal/sla/)

**Dokumentation:**

-   Azure dokumentationen för Active Directory-plats: [Azure Active Directory](http://azure.microsoft.com/documentation/services/active-directory/)

-   Azure Active Directory-bibliotek: [Azure Active Directory](http://msdn.microsoft.com/library/azure/jj673460.aspx)

-   Office 365-bibliotek: [Office 365](http://technet.microsoft.com/library/dn127064%28v=office.14%29.aspx)

## Vad gör jag om min fråga inte här?
Använda länkar och resurser som visas i [Information och Support för Azure Rights Management](../Topic/Information_and_Support_for_Azure_Rights_Management.md).

Dessutom finns vanliga frågor och svar för slutanvändare:

-   [Vanliga frågor och svar för Delningsapplikation för Windows Rights Management](https://technet.microsoft.com/dn467883)

-   [Vanliga frågor och svar för Delningsapplikation för Mobile och Mac-plattformar Rights Management](https://technet.microsoft.com/dn451248)

-   [Frågor och svar om spårning av dokument](http://go.microsoft.com/fwlink/?LinkId=523977)

Den här sidan vanliga frågor och svar uppdateras regelbundet med nya tillägg som listas i månatliga dokumentation update meddelanden på den [Microsoft Rights Management (RMS) Team](http://blogs.technet.com/b/rms/) blogg.

> [!TIP]
> Du kan använda den [dokument taggen](http://blogs.technet.com/b/rms/archive/tags/docs/) på bloggen, att enkelt hitta meddelandena dokumentation.

## Se även
[Kom igång med Azure Rights Management](../Topic/Getting_Started_with_Azure_Rights_Management.md)

