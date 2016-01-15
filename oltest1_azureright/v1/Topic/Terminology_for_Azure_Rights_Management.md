---
description: na
keywords: na
title: Terminology for Azure Rights Management
search: na
ms.date: na
ms.service: rights-management
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 742877bf-26f5-40e3-b1f7-8475e7c3ce11
---
# Terminologi f&#246;r Azure Rights Management
Förväxlas av ett ord, fras eller förkortningen som är relaterade till Microsoft [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] (Azure RMS)? Hitta definitionen för uttryck och förkortningar som är specifika för Azure RMS eller har en specifik betydelse när de används i samband med [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)].

|Termen|Definition|
|----------|--------------|
|AADRM|Namnet på Windows PowerShell-modulen för Azure Rights Management som har härletts från inofficiella förkortningen för [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] när det som tidigare kallades (Windows) Azure Active Directory Rights Management.|
|Aktivera|Så här aktiverar du den [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] tjänsten så att en organisation kan lägga till informationsskydd dokument och e-post. Den här åtgärden kan också funktioner för Rights Management i Exchange Online och SharePoint Online.|
|Active Directory Rights Management Services|Ofta förkortat till *AD RMS*.<br /><br />Rollen Windows Server som ger informationsskydd genom att använda kryptering och principer för att säkra dokument, filer och e-post.|
|AD RMS|Se *Active Directory Rights Management Services*.|
|Azure Rights Management|Ofta förkortat till *Azure RMS*.<br /><br />En Azure-tjänst som ger informationsskydd genom att använda kryptering och principer för att säkra dokument, filer och e-post.  Även känd som *Azure Rights Management-tjänsten*. Det finns tidigare namn:<br /><br />-   *Windows Azure Active Directory Rights Management*: Ofta förkortat till Windows Azure AD Rights Management Service.<br />-   *RMS Online*: Det ursprungliga, föreslagna namnet som ibland kan uppstå i felmeddelanden och loggfilsposter.|
|Azure RMS|Se *Azure Rights Management*.|
|BYOK|Se *Ta en egen nyckel*.|
|Gör en egen nyckel|Ofta förkortat till *BYOK*.<br /><br />Ett konfigurationsalternativ som valts av en organisation som du vill skapa och hantera sina egna innehavaren nyckel för [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)].|
|nyckeln|En unik nyckel som skapas av RMS-upplysta program för varje dokument eller e-post som är skyddade med [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)] och som hjälper till att minska risken för avslöjande av information.|
|använda|Låsa en fil för att läsa eller använda den när filen har skyddats av [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)].|
|inaktivera|Inaktivera Rights Management-tjänsten så att organisationen kan inte längre använda [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)].|
|avdelningens mall|En rättighetsprincipmall som du skapar (en anpassad mall) och är konfigurerad för att vara synliga för valda användare i stället för alla användare i din organisation.|
|upplysta program|Program som har inbyggt stöd för Rights Management, bland annat Office-program som Word och Excel. Oberoende programvaruleverantörer (ISV) och utvecklare kan även skriva program som har inbyggt stöd för [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)].|
|Enterprise rights management|En branschstandard, allmän term som ofta används för att beskriva produkter och lösningar som hjälper företag att skydda känslig eller värdefull information med hjälp av en kombination av kryptering och verktyg för auktorisering. Microsoft Rights Management är ett exempel på en enterprise rights management (ERM) lösning.|
|ERM|Se *enterprise rights management-*.|
|Allmänt skydd|En skyddsnivå som krypterar alla filtyper och förhindrar att obehöriga användare från att öppna filen. När filen har öppnats, filen är okrypterad och kan användas i ett program som inte har inbyggt stöd för [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)].|
|informationsskydd|Ibland förkortas till *IP*.<br /><br />En branschstandard, allmän term som refererar till att skydda data och filer från obehörig åtkomst, även efter data och filer lämna organisatoriska gränser med hjälp av e-post eller dela dokument. Microsoft Rights Management är ett exempel på en informationsskydd (IP).|
|Information Rights Management|Ofta förkortat till *IRM*.<br /><br />En term som används tillsammans med Office tjänster, till exempel Exchange Server, Word och SharePoint Online för att beskriva möjlighet att stödja Rights Management.|
|IRM|Se *Information Rights Management*.|
|MSDRM|Ibland som referenser för RMS-klienten 1.0, som ersätts med nyare RMS-klienten, MSIPC. Den här äldre klienten har stöd för program som har utvecklats med RMS SDK 1.0 och har stöd för Office 2010 och Office 2007, Exchange 2010 och Exchange 2013 och SharePoint 2010 och SharePoint 2007.|
|MSIPC|Ibland som referenser för RMS-klienten 2.0, som ersätts äldre RMS-klienten, MSDRM. Den här senare klienten har stöd för program som har utvecklats med RMS SDK 2.0 och stöder Office 2016 och Office 2013, SharePoint 2013 och RMS-delningsprogrammet.|
|Internt skydd|En skyddsnivå tillgänglig i alla enlightened program som förhindrar att obehöriga användare från att öppna en fil och som kan också tvinga strängare principer som skrivskyddad, och inte ut. Dessutom förblir skyddet med filen, även om filen är vidarebefordras till andra eller spara på en offentlig plats som andra kan komma åt.|
|.pfile|Filnamnstillägg som läggs till på alla filer som Rights Management skyddar Allmänt.|
|.ppdf|Filnamnstillägg som Rights Management skapas när den skapas automatiskt en PDF-kopia av en fil (Word, Excel, PowerPoint eller PDF) som du delar via e-post, så att filen kan läsas (men inte redigera) på alla enheter.|
|åtkomstnivå|En logisk gruppering av användarrättigheter som gör det enklare för slutanvändare och administratörer kan välja konfigurationsalternativ som är rollbaserad. Granskning och medförfattare.|
|skydda|Tillämpa Rights Management kontroller filer eller e-postmeddelanden med hjälp av kryptering, identitet och åtkomst till principer för åtkomstkontroll för att säkra data.|
|Publicera|Du kan skydda en fil för att skydda den från obehörig åtkomst till och använda.|
|Rights Management-koppling|En utgående proxy relay som du kan distribuera för lokala tjänster som Exchange Server och SharePoint, för att skydda data med Azure Rights Management.|
|Rights Management services|Allmän term som gäller för både molnet versionen av [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)] ([!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)]) och den lokala versionen av [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)] (AD RMS).|
|Delningsapplikationen Rights Management|Ett valfritt hämtningsbart program för Windows och mest populära mobila enheter som har stöd för delning av filer på plats och via e-post på ett säkert sätt.|
|RMS|Se *Rights Management services*.|
|RMS-koppling|Se *Rights Management-koppling*.|
|RMS för individer|En kostnadsfri prenumeration för en användare att använda [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)] när deras organisation inte har en prenumeration på Office 365 eller Azure Active Directory.|
|RMS-delningsprogrammet tidigare|Se *delningsapplikationen Rights Management*.|
|Super-användare|En grupp pålitliga administratörer som kan dekryptera och få åtkomst till filer som organisationen har skyddat genom Rights Management. Den här åtkomstnivån är vanligtvis krävs för juridiska e-informationsavslöjande och genom att granska team.|
|nyckeln för klienten|Även känd som server licensgivarens certifikatet (Serverlicensgivarcertifikat) nyckeln.<br /><br />Den nyckel som är unikt för en organisation och slutligen skyddar alla [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)] kryptografiska funktioner som ingår i kedjan till den här nyckeln för innehavaren.|
|ta bort skyddet från|Ta bort Rights Management kontroller från filer eller e-postmeddelanden som används för kryptering, identitet och åtkomst till principer för åtkomstkontroll för att säkra data.|
|Använd licens|Ett certifikat för varje dokument som ges till en användare som öppnar en fil eller e-postmeddelande som har skyddats av [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)]. Det här certifikatet innehåller den användarrättigheter för filen eller e-postmeddelandet och den krypteringsnyckel som används för att kryptera innehållet, samt ytterligare åtkomstbegränsningar som definierats i dokumentets princip.|

## Se även
[Kom igång med Azure Rights Management](../Topic/Getting_Started_with_Azure_Rights_Management.md)

