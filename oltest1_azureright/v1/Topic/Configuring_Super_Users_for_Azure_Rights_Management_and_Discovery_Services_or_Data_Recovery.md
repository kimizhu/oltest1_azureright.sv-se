---
description: na
keywords: na
title: Configuring Super Users for Azure Rights Management and Discovery Services or Data Recovery
search: na
ms.date: na
ms.service: rights-management
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: acb4c00b-d3a9-4d74-94fe-91eeb481f7e3
---
# Konfigurera Super Users f&#246;r Azure Rights Management och identifiering av tj&#228;nster eller &#229;terst&#228;llning av Data
Super user-funktion i Microsoft [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] (Azure RMS) säkerställer att behöriga användare och tjänster kan alltid läsa och inspektera de data som Azure RMS skyddar för din organisation. Och om det behövs, ta bort skyddet eller ändra skyddet som tillämpades tidigare. Super-användare har alltid ägare fullständig behörighet för alla licenser som har beviljats av organisationens RMS-klienten. Denna funktion kallas ibland "motivering över data" och är en som är avgörande för att behålla kontrollen över din organisations data. Du skulle till exempel använda den här funktionen för någon av följande situationer:

-   En medarbetare lämnar organisationen och du behöver kunna läsa de filer som de skyddade.

-   En IT-administratör måste ta bort den aktuella skyddsprincip som har konfigurerats för filer och tillämpa en ny skyddsprincip.

-   Exchange Server måste index postlådor för sökningar.

-   Du har befintliga IT-tjänster för förlust förebyggande (DLP) lösningar, innehåll kryptering gateways (CEG) och skadlig produkter som behöver inspektera filer som redan skyddas.

-   Du behöver Massredigera dekryptera filer för granskning, juridiska eller andra kompatibilitetsskäl.

Super user-funktionen är inte aktiverad som standard, och inga användare har tilldelats den här rollen. Den är aktiverad för du automatiskt om du konfigurerar Rights Management-koppling för Exchange och det inte är obligatoriskt för standardtjänster som kör Exchange Online, SharePoint Online eller SharePoint-servern.

Om du manuellt Aktivera super user-funktionen kan du använda Windows PowerShell-cmdlet [Aktivera AadrmSuperUserFeature](https://msdn.microsoft.com/library/azure/dn629400.aspx), och därefter tilldela användare (eller tjänstkonton) vid behov genom att använda den [Lägg till AadrmSuperUser](https://msdn.microsoft.com/library/azure/dn629411.aspx) cmdlet. Du kan ha en eller flera super användare för din organisation, men du måste lägga till enskilda användare. grupper stöds inte.

> [!NOTE]
> Om du ännu inte har installerat Windows PowerShell-modulen för [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)], se [Installera Windows PowerShell för Azure Rights Management](../Topic/Installing_Windows_PowerShell_for_Azure_Rights_Management.md).

Rekommenderade säkerhetsmetoder för super user-funktionen:

-   Begränsa och övervaka de administratörer som tilldelas en global administratör för ditt Office 365 eller Azure RMS-klienten eller som har tilldelats rollen GlobalAdministrator med hjälp av den [Lägg till AadrmRoleBasedAdministrator](https://msdn.microsoft.com/library/azure/dn629417.aspx) cmdlet. Dessa användare kan aktivera funktionen super-användare och tilldela användare (och själva) som super användare och potentiellt dekryptera alla filer som skyddar din organisation.

-   Om du vill se vilka användare och tjänstkonton är tilldelad som super användare använder den [cmdlet Get-AadrmSuperUser](https://msdn.microsoft.com/library/azure/dn629408.aspx).  Aktivera eller inaktivera funktionen super och lägga till eller ta bort super användare är inloggad som alla administration åtgärder, och kan granskas med hjälp av den [Get-AadrmAdminLog](https://msdn.microsoft.com/library/azure/dn629430.aspx) kommando. När super användare dekrypterar filer, åtgärden loggas och kan granskas med [användningsloggning](https://technet.microsoft.com/library/dn529121.aspx).

-   Om du inte behöver super user-funktionen för dagliga tjänster, aktivera funktionen när du behöver den och inaktivera den genom att använda den [Inaktivera AadrmSuperUserFeature](https://msdn.microsoft.com/library/azure/dn629428.aspx) cmdlet.

Följande loggen extrahera visar några exempel posterna från och med hjälp av cmdleten Get-AadrmAdminLog. I det här exemplet bekräftar administratören för Contoso Ltd att super user-funktionen är inaktiverad, lägger till Richard Simone som en super user kontrollerar att Richard är bara super-användaren har konfigurerats för Azure RMS, och sedan aktiverar funktionen super-användare så att Richard nu kan dekryptera vissa filer som skyddades av en medarbetare som nu har lämnat företaget.

`2015-08-01T18:58:20	admin@contoso.com	GetSuperUserFeatureState	Passed	Disabled`
`2015-08-01T18:59:44	admin@contoso.com	AddSuperUser -id rsimone@contoso.com	Passed	True`
`2015-08-01T19:00:51	admin@contoso.com	GetSuperUser	Passed	rsimone@contoso.com`
`2015-08-01T19:01:45	admin@contoso.com	SetSuperUserFeatureState -state Enabled	Passed	True`

## <a name="BKMK_RMSProtectionModule"></a>Skriptalternativen för super användare
Ofta någon som är tilldelad en super user för [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] måste du ta bort skyddet från flera filer på flera platser. Det är möjligt att göra detta manuellt, men det är mer effektiv (och ofta mer tillförlitlig) skript för detta. Gör [Hämta verktyget RMS-skydd](http://www.microsoft.com/en-us/download/details.aspx?id=47256). Använd sedan den  [Unprotect RMSFile](https://msdn.microsoft.com/library/azure/mt433200.aspx) cmdlet, och [skydda RMSFile](https://msdn.microsoft.com/library/azure/mt433201.aspx)   cmdlet som krävs.

> [!IMPORTANT]
> Även om verktyget RMS-skydd är utformat för super användare att bulk ta bort skyddet från filer för återställning, den aktuella versionen av verktyget stöder inte användarautentisering för Azure RMS. Tills problemet har lösts måste du använda ett huvudnamn tjänstkonto för att autentisera med Azure RMS innan du kan ta bort skyddet från filer.  Mer information och instruktioner finns [about_RMSProtection_AzureRMS](https://msdn.microsoft.com/library/azure/mt433202.aspx).

Mer information om dessa cmdlets, se [RMS-skydd Cmdlets](https://msdn.microsoft.com/library/azure/mt433195.aspx).

> [!NOTE]
> RMSProtection Windows PowerShell-modulen som levereras med verktyget RMS-skydd skiljer sig från och kompletterar huvudfönstret [Windows PowerShell-modulen för Azure Rights Management](https://technet.microsoft.com/library/jj585027.aspx). Den stöder båda Azure RMS och AD RMS.

## Se även
[Konfigurera Azure Rights Management](../Topic/Configuring_Azure_Rights_Management.md)

