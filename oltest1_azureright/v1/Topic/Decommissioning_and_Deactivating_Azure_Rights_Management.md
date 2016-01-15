---
description: na
keywords: na
title: Decommissioning and Deactivating Azure Rights Management
search: na
ms.date: na
ms.service: rights-management
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0b1c2064-0d01-45ae-a541-cebd7fd762ad
---
# Inaktivering och inaktivera Azure Rights Management
Du har alltid kontroll över om din organisation skyddar innehållet genom att använda [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] (Azure RMS), och om du inte längre vill använda denna information protection lösning kan du har garanti att du inte låsas av innehåll som tidigare var skyddad. Om du inte behöver fortsatt åtkomst till tidigare skyddat innehåll du enkelt inaktivera tjänsten och kan prenumerationen för Azure Rights Management upphör att gälla. Exempel: Detta är lämpliga för när du har slutfört testning [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] innan du distribuerar i en produktionsmiljö.

Men om du har distribuerat [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] tillverkning, kontrollera att du har en kopia av nyckeln Azure Rights Management-klient innan du inaktivera tjänsten och göra detta innan din prenumeration upphör, eftersom detta gör att du har åtkomst till innehåll som skyddas av Azure Rights Management när tjänsten är inaktiverad. Om du använder se till att en egen nyckel lösning (BYOK) där du kan skapa och hantera nyckeln i en HSM redan du din Azure Rights Management-klient-nyckel. Men om det var hanteras av Microsoft (standard) visas instruktioner för att exportera klient-nyckeln i [Åtgärder för din Azure Rights Management-klient nyckel](../Topic/Operations_for_Your_Azure_Rights_Management_Tenant_Key.md) ämne.

> [!TIP]
> Även när din prenumeration upphör att gälla Azure Rights Management-klient finns kvar för förbrukar innehåll under en längre. Du kommer dock inte längre att kunna exportera klient-nyckeln.

Du kan distribuera Rights Management lokalt (AD RMS) och importera klient-nyckel som en betrodd publicering domän (betrodda Publiceringsdomänen) när du har din Azure Rights Management-klient-nyckel. Sedan har du följande alternativ för att inaktivera Azure Rights Management-distribution:

|Om detta gäller dig...|… gör du följande:|
|--------------------------|----------------------|
|Du vill att alla användare kan fortsätta att använda Rights Management, men använder en lösning för lokala i stället för Azure RMS →|Använd den [mängd AadrmMigrationUrl](https://msdn.microsoft.com/library/azure/dn629429.aspx) cmdlet leder befintliga användare till din lokala distribution när de använder innehåll skyddade efter ändringen. Användare använder automatiskt AD RMS-installation förbrukar skyddat innehåll.<br /><br />För användare att allt innehåll som har skyddats innan den här ändringen dirigera klienterna till lokala-distribution med hjälp av den **LicensingRedirection** registernyckeln för Office 2016 eller Office 2013, enligt beskrivningen i den [service discovery avsnittet](https://technet.microsoft.com/library/jj159267%28v=ws.10%29.aspx) i RMS client deployment anteckningar och **LicenseServerRedirection** registernyckeln för Office 2010, enligt beskrivningen i [Office registerinställningar](https://technet.microsoft.com/library/dd772637%28v=ws.10%29.aspx).|
|Vill du avbryta med hjälp av Rights Management tekniker helt →|Ge en angiven administratör [super användarrättigheter](https://technet.microsoft.com/library/mt147272.aspx) och ge personen i [RMS Protection verktyget](http://www.microsoft.com/en-us/download/details.aspx?id=47256).<br /><br />Den här administratör kan sedan använda verktyget för massinfogning dekryptera filer i mappar som har skyddas av Azure Rights Management så att filer återgå till tas bort och därför kan läsas utan en Rights Management-teknik som Azure RMS och AD RMS. Det här verktyget kan användas med både Azure RMS och AD RMS så att du kan välja dekrypterar filer före eller efter du inaktivera Azure RMS eller båda.|
|Det går inte att identifiera alla filer är skyddade av Azure RMS eller om du vill att alla användare ska kunna läsa automatiskt alla skyddade filer som har missat →|Distribuera en registerinställning på alla datorer med hjälp av den **LicensingRedirection** registernyckeln för Office 2016 och Office 2013, enligt beskrivningen i den [service discovery avsnittet](https://technet.microsoft.com/library/jj159267%28v=ws.10%29.aspx) i RMS client deployment anteckningar och **LicenseServerRedirection** registernyckeln för Office 2010, enligt beskrivningen i [Office registerinställningar](https://technet.microsoft.com/library/dd772637%28v=ws.10%29.aspx).<br /><br />Distribuera en annan registerinställning att hindra användare från att skydda nya filer genom att ange **DisableCreation** till **1**, enligt beskrivningen i [Office registerinställningar](https://technet.microsoft.com/library/dd772637%28v=ws.10%29.aspx).|
|Du vill att en kontrollerade, manuell återställning-tjänst för filer som användes missade →|Bevilja utsedda användare i en grupp för återställning av data [super användarrättigheter](https://technet.microsoft.com/library/mt147272.aspx) och ger dem i [RMS Protection verktyget](http://www.microsoft.com/en-us/download/details.aspx?id=47256) så att de kan ta bort skyddet filer när de begärs av standardanvändare.<br /><br />Distribuera på alla datorer registerinställning för att hindra användare från att skydda nya filer genom att ange **DisableCreation** till **1**, enligt beskrivningen i [Office registerinställningar](https://technet.microsoft.com/library/dd772637%28v=ws.10%29.aspx).|
Mer information om procedurerna i den här tabellen finns i följande resurser:

-   Information om AD RMS och distribution referenser finns [Active Directory Rights Management Services översikt](https://technet.microsoft.com/library/hh831364.aspx).

-   Anvisningarna för att importera din Azure RMS-klient nyckel som betrodda Publiceringsdomänen fil, se [lägga till en betrodd publiceringsdomän](https://technet.microsoft.com/library/cc771460.aspx).

-   Om du vill installera Windows PowerShell-modul för Azure RMS att ange Webbadressen migrering finns [Installera Windows PowerShell för Azure Rights Management](../Topic/Installing_Windows_PowerShell_for_Azure_Rights_Management.md).

Använd följande anvisningar när du är redo att inaktivera Azure RMS-tjänsten för din organisation.

## Inaktivera Rights Management
Använd en av följande procedurer när du vill inaktivera [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)].

> [!TIP]
> Du kan också använda Windows PowerShell-cmdlet [Inaktivera Aadrm](http://msdn.microsoft.com/library/windowsazure/dn629422.aspx), inaktivera [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)].

#### Inaktivera Rights Management från administrationscentret för Office 365

1.  [Logga in på Office 365 med kontot arbetet eller skolan](https://portal.office.com/) som administratör för distribution av Office 365.

2.  Om inte automatiskt visas administrationscentret för Office 365, välj ikonen starta app i övre vänstra och välj **Admin**. Den **Admin** bricka visas endast för Office 365-administratörer.

    > [!TIP]
    > Mer information om admin center finns [Administrationscenter om Office 365 - administratör hjälp](https://support.office.com/article/About-the-Office-365-admin-center-Admin-Help-58537702-d421-4d02-8141-e128e3703547).

3.  I det vänstra fönstret, expandera **TJÄNSTINSTÄLLNINGARNA**.

4.  Klicka på **Rights Management**.

5.  På den **RIGHTS MANAGEMENT** klickar du på **hantera**.

6.  På den **rights management** klickar du på **inaktivera**.

7.  När du uppmanas **vill du inaktivera Rights Management?**, klickar du på **inaktivera**.

Du bör nu visas **Rights Management är inte aktiverat** och alternativet för att aktivera.

#### Inaktivera Rights Management från Azure-portalen

1.  Logga in på den [Azure-portalen](http://go.microsoft.com/fwlink/p/?LinkID=275081).

2.  I det vänstra fönstret klickar du på **ACTIVE DIRECTORY**.

3.  Från den **active directory** klickar du på **RIGHTS MANAGEMENT**.

4.  Välj den katalog att hantera för [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)], klickar du på **inaktivera**, och bekräfta åtgärden.

Den **RIGHTS MANAGEMENT STATUS** ska nu visa **inaktiv** och **inaktivera** alternativet ersätts med **Aktivera**.

## Se även
[Konfigurera Azure Rights Management](../Topic/Configuring_Azure_Rights_Management.md)

