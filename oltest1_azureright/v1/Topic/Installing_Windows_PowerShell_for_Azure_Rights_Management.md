---
description: na
keywords: na
title: Installing Windows PowerShell for Azure Rights Management
search: na
ms.date: na
ms.service: rights-management
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0d665ed6-b1de-4d63-854a-bc57c1c49844
---
# Installera Windows PowerShell f&#246;r Azure Rights Management
Använd följande information för att hjälpa dig att installera Windows PowerShell för Microsoft [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] (Azure RMS).

Du kan använda den här modulen för Windows PowerShell för att administrera [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] från kommandoraden med hjälp av valfri dator som har Internetanslutning och som uppfyller krav som anges i nästa avsnitt. Windows PowerShell för [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] stöder skript för automatisering eller kan det vara nödvändigt för avancerad konfiguration scenarier. Läs mer om administrationsuppgifter och konfigurationer som modulen stöder [Administrera Azure Rights Management med Windows PowerShell](../Topic/Administering_Azure_Rights_Management_by_Using_Windows_PowerShell.md).

## Nödvändiga komponenter
Den här tabellen visar förutsättningar för att installera och använda Windows PowerShell för [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)].

|Krav|Mer information|
|--------|-------------------|
|En version av Windows som stöder den [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)] administration-modul|Kontrollera vilka operativsystem som stöds i den **systemkrav** delen av den [hämtningssidan för Azure Rights Management Administration Tool](http://go.microsoft.com/fwlink/?LinkId=257721).|
|Minsta version av Windows PowerShell: 2.0|Stöd för den [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)] administration modulen presenteras i Windows PowerShell 2.0.<br /><br />Som standard i de flesta Windows-operativsystem installerat med minst version 2.0 av Windows PowerShell. Om du behöver installera Windows PowerShell 2.0 se [installera Windows PowerShell 2.0](http://msdn.microsoft.com/library/ff637750.aspx). **Tip:** Du kan kontrollera vilken version av Windows PowerShell som du använder genom att skriva **$PSVersionTable** i en Windows PowerShell-session.|
|Minsta version av Microsoft .NET Framework: 4.5 **Tip:** Den här versionen av Microsoft .NET Framework är bifogat senare operativsystem så du behöver bara manuellt installera om dina klientoperativsystem är mindre än Windows 8.0 eller server-operativsystem är mindre än Windows Server 2012.|Om det inte redan är installerad, kan du hämta det [Microsoft .NET Framework 4.5](http://www.microsoft.com/download/details.aspx?id=30653).<br /><br />Den här versionen av Microsoft .NET Framework krävs för några av klasserna som den [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)] administration i modulen används.|
|Logga In Assistant 7.0 för Microsoft Online Services|Microsoft Online Services inloggning Assistant krävs för [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] autentisering.<br /><br />Mer information finns i [Download Center: Assistant för IT-proffs RTW för Microsoft Online Services](http://www.microsoft.com/en-us/download/details.aspx?id=41950).|

## Så här installerar du modulen Rights Management administration

1.  Gå till Microsoft Download Center och [Hämta verktyget Azure Rights Management Administration](https://go.microsoft.com/fwlink/?LinkId=257721), som innehåller den [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] administration-modulen för Windows PowerShell.

2.  Från den lokala mappen där du har hämtat och sparat på [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)] installer filen genom att dubbelklicka på den körbara filen som du har hämtat för din plattform (WindowsAzureADRightsManagementAdministration_x64 eller WindowsAzureADRightsManagementAdministration_x86.exe) om du vill starta Azure AD Rights Management Administration installationsguiden.

3.  Slutför guiden.

Windows PowerShell för [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] har installerats.

## Nästa steg
Om du vill se vilka cmdlet: ar finns, starta Windows PowerShell med den **Kör som administratör** alternativet och ange följande:

```
Get-Command -Module aadrm
```
Använd `the Get-Help <cmdlet_name>` kommandot för att se hjälp för en viss cmdlet.

Mer information:

-   Fullständig lista över tillgängliga cmdlet: ar: [Cmdlet: ar för Azure Rights Management](https://msdn.microsoft.com/library/windowsazure/dn629398.aspx)

-   Lista över huvudsakliga konfiguration scenarier som har stöd för Windows PowerShell: [Administrera Azure Rights Management med Windows PowerShell](../Topic/Administering_Azure_Rights_Management_by_Using_Windows_PowerShell.md)

Innan du kan köra alla kommandon som konfigurerar den [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] service, måste du ansluta till tjänsten med hjälp av den [Connect-AadrmService](https://msdn.microsoft.com/library/windowsazure/dn629415.aspx) cmdlet. När du är klar med att köra kommandona konfiguration som du vill koppla från tjänsten med hjälp av den [Koppla från AadrmService](https://msdn.microsoft.com/library/windowsazure/dn629416.aspx) cmdlet.

> [!NOTE]
> Om du ännu inte har aktiverat [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)], du kan göra detta när du har kopplat till tjänsten med hjälp av den [Aktivera Aadrm](https://msdn.microsoft.com/library/windowsazure/dn629412.aspx) cmdlet.

## Se även
[Administrera Azure Rights Management med Windows PowerShell](../Topic/Administering_Azure_Rights_Management_by_Using_Windows_PowerShell.md)

