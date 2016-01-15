---
description: na
keywords: na
title: Administering Azure Rights Management by Using Windows PowerShell
search: na
ms.date: na
ms.service: rights-management
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a890e04a-4b70-41b5-8d5f-3c210a669faa
---
# Administrera Azure Rights Management med Windows PowerShell
Även om du kan aktivera Microsoft [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] (Azure RMS) med hjälp av den [!INCLUDE[o365_2](../Token/o365_2_md.md)] Administrationscenter eller Azure-portalen, du kan också använda Windows PowerShell-modul för [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] (AADRM) för att göra detta.

När du har aktiverat [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)], ytterligare administration för tjänsten kanske inte krävs. Vissa scenarier för avancerad konfiguration kanske måste du dock använda Windows PowerShell-modul för [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)]. I följande tabell visas några avancerad konfiguration scenarier med Windows PowerShell. En fullständig lista över tillgängliga cmdlets med mer information om var och en Se [Azure Rights Management Cmdlets](http://msdn.microsoft.com/library/azure/dn629398.aspx).

> [!NOTE]
> Om du behöver installera Windows PowerShell-modul för [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)], se [Installera Windows PowerShell för Azure Rights Management](../Topic/Installing_Windows_PowerShell_for_Azure_Rights_Management.md).

Det finns också en kompletterande Windows PowerShell-modul **RMSProtection**, som stöder både Azure RMS och AD RMS. Den här modulen stöder skydda och ta bort skyddet från flera filer så att till exempel kan du massinfogning-skydda alla filer i en mapp. Mer information finns i [Skriptalternativen för super användare](../Topic/Configuring_Super_Users_for_Azure_Rights_Management_and_Discovery_Services_or_Data_Recovery.md#BKMK_RMSProtectionModule) under den [Konfigurera Super Users för Azure Rights Management och identifiering av tjänster eller återställning av Data](../Topic/Configuring_Super_Users_for_Azure_Rights_Management_and_Discovery_Services_or_Data_Recovery.md) ämne.

|Om du behöver...|.. .använda följande cmdlets|
|--------------------|--------------------------------|
|Migrera från lokala Rights Management (AD RMS eller Windows RMS) till [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)].|[Importera AadrmTpd](http://msdn.microsoft.com/library/azure/dn857523.aspx)|
|Ansluta till eller koppla från den [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)] tjänsten för din organisation.|[Anslut AadrmService](http://msdn.microsoft.com/library/azure/dn629415.aspx)<br /><br />[Koppla från AadrmService](http://msdn.microsoft.com/library/azure/dn629416.aspx)|
|Generera och hantera en egen innehavaren nyckel – Se till att ditt eget scenario nyckel (BYOK).|[Lägg till AadrmKey](http://msdn.microsoft.com/library/azure/dn629418.aspx)<br /><br />[Hämta AadrmKeys](http://msdn.microsoft.com/library/azure/dn629420.aspx)|
|Aktivera eller inaktivera den [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)] tjänsten för din organisation.|[Aktivera Aadrm](http://msdn.microsoft.com/library/azure/dn629412.aspx)<br /><br />[Inaktivera Aadrm](http://msdn.microsoft.com/library/azure/dn629422.aspx)|
|Aktivera och inaktivera dokumentet spåra plats för Azure Rights Management.|[Inaktivera AadrmDocumentTrackingFeature](https://msdn.microsoft.com/library/azure/mt548471.aspx)<br /><br />[Aktivera AadrmDocumentTrackingFeature](https://msdn.microsoft.com/library/azure/mt548469.aspx)<br /><br />[Hämta AadrmDocumentTrackingFeature](https://msdn.microsoft.com/library/azure/mt548470.aspx)|
|Konfigurera inledande kontroller för en fasindelad distribution av Azure Rights Management.|[Hämta AadrmOnboardingControlPolicy](http://msdn.microsoft.com/library/azure/dn857522.aspx)<br /><br />[Ange AadrmOnboardingControlPolicy](http://msdn.microsoft.com/library/azure/dn857521.aspx)|
|Skapa och hantera rättigheter principmallar för din organisation.|[Lägg till AadrmTemplate](http://msdn.microsoft.com/library/azure/dn727075.aspx)<br /><br />[Exportera AadrmTemplate](http://msdn.microsoft.com/library/azure/dn727078.aspx)<br /><br />[Hämta AadrmTemplate](http://msdn.microsoft.com/library/azure/dn727079.aspx)<br /><br />[Hämta AadrmTemplateProperty](http://msdn.microsoft.com/library/azure/dn727081.aspx)<br /><br />[Importera AadrmTemplate](http://msdn.microsoft.com/library/azure/dn727077.aspx)<br /><br />[Ny AadrmRightsDefinition](http://msdn.microsoft.com/library/azure/dn727080.aspx)<br /><br />[Ta bort AadrmTemplate](http://msdn.microsoft.com/library/azure/dn727082.aspx)<br /><br />[Ange AadrmTemplateProperty](http://msdn.microsoft.com/library/azure/dn727076.aspx)|
|Konfigurera det maximala antalet dagar som innehåll som skyddar din organisation kan användas utan en Internetanslutning (Använd licens giltighetsperioden).|[Hämta AadrmMaxUseLicenseValidityTime](https://msdn.microsoft.com/library/azure/dn932062.aspx)<br /><br />[Ange AadrmMaxUseLicenseValidityTime](https://msdn.microsoft.com/library/azure/dn932063.aspx)|
|Hantera funktionen superanvändare i [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)] för din organisation.|[Aktivera AadrmSuperUserFeature](http://msdn.microsoft.com/library/azure/dn629400.aspx)<br /><br />[Inaktivera AadrmSuperUserFeature](http://msdn.microsoft.com/library/azure/dn629428.aspx)<br /><br />[Lägg till AadrmSuperUser](http://msdn.microsoft.com/library/azure/dn629411.aspx)<br /><br />[Hämta AadrmSuperUser](http://msdn.microsoft.com/library/azure/dn629408.aspx)<br /><br />[Ta bort AadrmSuperUser](http://msdn.microsoft.com/library/azure/dn629405.aspx)|
|Hantera användare och grupper som har behörighet att administrera den [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)] tjänsten för din organisation.|[Lägg till AadrmRoleBasedAdministrator](http://msdn.microsoft.com/library/azure/dn629417.aspx)<br /><br />[Hämta AadrmRoleBasedAdministrator](http://msdn.microsoft.com/library/azure/dn629407.aspx)<br /><br />[Ta bort AadrmRoleBasedAdministrator](http://msdn.microsoft.com/library/azure/dn629424.aspx)|
|Hämta en logg över [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)] administrativa uppgifter för din organisation.|[Hämta AadrmAdminLog](http://msdn.microsoft.com/library/azure/dn629430.aspx)|
|Logga in och analysera användning loggning för [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)].|[Aktivera AadrmUsageLogFeature](http://msdn.microsoft.com/library/azure/dn629421.aspx)<br /><br />[Hämta AadrmUsageLog](http://msdn.microsoft.com/library/azure/dn629401.aspx)<br /><br />[Hämta AadrmUsageLogFeature](http://msdn.microsoft.com/library/azure/dn629425.aspx)<br /><br />[Hämta AadrmUsageLogLastCounterValue](http://msdn.microsoft.com/library/azure/dn629423.aspx)<br /><br />[Hämta AadrmUsageLogStorageAccount](http://msdn.microsoft.com/library/azure/dn629419.aspx)<br /><br />[Ange AadrmUsageLogStorageAccount](http://msdn.microsoft.com/library/azure/dn629426.aspx)<br /><br />[Inaktivera AadrmUsageLogFeature](http://msdn.microsoft.com/library/azure/dn629404.aspx)|
|Visa aktuellt [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)] tjänstkonfigurationen för din organisation.|[Hämta AadrmConfiguration](http://msdn.microsoft.com/library/azure/dn629410.aspx)|
|Migrera din organisation från [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] till en lokal AD RMS-distribution.|[Ange AadrmMigrationUrl](http://msdn.microsoft.com/library/azure/dn629429.aspx)<br /><br />[Hämta AadrmMigrationUrl](http://msdn.microsoft.com/library/azure/dn629403.aspx)|

## Se även
[Azure Rights Management](../Topic/Azure_Rights_Management.md)

