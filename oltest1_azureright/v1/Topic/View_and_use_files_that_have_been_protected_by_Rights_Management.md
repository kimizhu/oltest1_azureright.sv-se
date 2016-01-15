---
description: na
keywords: na
title: View and use files that have been protected by Rights Management
search: na
ms.date: na
ms.service: rights-management
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e5fa4666-6906-405a-9e0c-2c52d4cd27c8
---
# Visa och anv&#228;nda filer har skyddats av Rights Management
När den [Rights Management (RMS) delningsprogrammet är installerat på datorn](https://technet.microsoft.com/library/dn574734%28v=ws.10%29.aspx), du kan visa en skyddad fil genom att helt enkelt Dubbelklicka på den. Filen kan vara en bifogad fil i ett e-postmeddelande och du kan se när du använder filen Explorer.

> [!NOTE]
> Innan du kan visa den skyddade filen måste RMS först att bekräfta att du har behörighet att visa filen genom att kontrollera ditt användarnamn och lösenord. I vissa fall kan detta vara cachelagrade och uppmanas att ange autentiseringsuppgifterna visas inte. I annat fall kan uppmanas du att ange dina autentiseringsuppgifter.
> 
> Om din organisation inte använder Azure Rights Management (Azure RMS) eller AD RMS, kan du använda ett gratis konto som accepterar dina autentiseringsuppgifter så att du kan öppna filer som skyddas med hjälp av RMS:
> 
> -   Om du vill använda för det här kontot, klickar du på länken ansöka om [RMS för enskilda](http://go.microsoft.com/fwlink/?LinkId=309469).
> 
>     När du registrerar dig använda företagets e-postadress i stället för en personliga e-postadress. Om du loggar eftersom du har e-post en skyddad fil, kan du använda samma e-postadress som användes för att skicka e-postmeddelande.
> -   Mer information finns i [RMS för personer och Windows Azure Rights Management](http://technet.microsoft.com/library/dn592127.aspx).

## <a name="BKMK_ViewPFILE"></a>Så här visar du en skyddad fil
Dubbelklicka på den skyddade filen med File Explorer eller e-postmeddelande som innehåller bilagan, och ange autentiseringsuppgifter om du uppmanas att göra det.

Om du ser två versioner av filen men med olika filnamnstillägg öppna en fil med filnamnstillägget .ppdf endast om den andra filen inte öppnas. Om du inte kan öppna .ppdf version antingen måste först installera den [RMS-delning program](http://technet.microsoft.com/library/dn574734.aspx), som känner till hur du öppnar filer som har filnamnstillägget .ppdf.

> [!NOTE]
> Mer information finns i "[Vad är .ppdf-fil som skapas automatiskt?](../Topic/Dialog_box_options_for_the_Rights_Management_sharing_application.md#BKMK_PPDF)".

Hur filen öppnas beror på hur den skyddas, där du kan se att filnamnstillägget. I varje fall öppna filen kan granskas och är granskade så länge den är skyddad. Dessutom om filen skickades som ett e-postmeddelande kan sändaren bli meddelad via e-post varje gång du öppnar filen.

|Filnamnstillägg och skydd|Mer information|
|-----------------------------|-------------------|
|Filen har ett **.pfile** filnamnstillägg.<br /><br />Filen har datorverifieringsprocessen skyddad.|När du öppnar filen ser du en **skyddad fil** dialogrutan delning programmet som berättar som skyddade filen och som du förväntas respektera ägarna behörigheter. Klicka på **Öppna** att läsa filen.<br /><br />![](../Image/ADRMS_MSRMSApp_PfilePermission.png)|
|Filen har ett **.ppdf** filnamnstillägg eller är en skyddad fil text eller bild (exempel **.ptxt** eller **.pjpg**).<br /><br />Filen har skyddats program som en skrivskyddad kopia.|Filen öppnas i visningsprogrammet som installeras med RMS-delning program. Den här filen är skrivskyddad, även om du sparar det till en annan plats eller Byt namn på den.|
|Andra filnamnstillägg.<br /><br />Filen har skyddats program.|Filen öppnas med det program som är associerad med det ursprungliga filnamnstillägget och en begränsning banderoll visas överst i filen. Banderollen kan visa de behörigheter som tillämpas på filen eller den kan innehålla en länk om du vill visa dem. Exempel: du kan se följande där måste du klicka på **behörigheten är för närvarande begränsad** att visa de faktiska behörigheter som tillämpas på filen och de personer som har åtkomst till den:<br /><br />![](../Image/ADRMS_MSRMSApp_RestrictedAccess.png)|
En fullständig lista över filnamnstillägg som Rights Management stöder finns i [Filtyper och filnamnstillägg](../Topic/Rights_Management_sharing_application_administrator_guide.md#BKMK_SupportFileTypes) avsnitten i den  [Rights Management dela program administratörshandboken](../Topic/Rights_Management_sharing_application_administrator_guide.md). Om din filnamnstillägget inte visas kan du använda en webbsökning om det finns ett filnamnstillägg som stöds av ett annat program.

> [!NOTE]
> Om när du har bekräftat att filen är skyddad av Rights Management och går inte att öppna filen, hämtar och använder den [RMS Analyzer tool](https://www.microsoft.com/en-us/download/details.aspx?id=46437). Följ anvisningarna i verktyget för att söka efter problem på datorn som kan förhindra att ett skyddat dokument öppnas.

## <a name="BKMK_UserDefined"></a>Använda filer som har skyddats (till exempel, redigera och Skriv ut filen)
Om du vill att mer än att bara läsa när du har öppnat den skyddade filen (till exempel redigera, kopiera och skriva ut den):

|Filnamnstillägg|Instruktioner|
|-------------------|-----------------|
|Filen har ett **.pfile** filnamnstillägg.|Spara den öppna filen och ge den ett nytt filnamnstillägg som är associerad med det program som du vill använda.<br /><br />Om en fil har skyddats med hjälp av filen namnet document.vsdx.pfile filen och spara filen som document.vsdx i filen Explorer.<br /><br />Den nya filen skyddad inte längre. Om du vill skydda den måste du göra detta manuellt. Instruktioner finns i [Skydda en fil på en enhet &#40;skydda på plats&#41; genom att använda delningsapplikation Rights Management](../Topic/Protect_a_file_on_a_device__protect_in-place__by_using_the_Rights_Management_sharing_application.md).|
|Filen har ett **.ppdf** filnamnstillägg eller är en skyddad fil text eller bild (exempel **.ptxt** eller **.pjpg**).|Du kan bara se filen och om du byter namn på eller flytta den skydd förblir med filen.|
|Andra filnamnstillägg.|Enheten måste ha ett program som förstår Rights Management att använda de här filerna. Dessa program kallas RMS-enlightened program. Program från Office 2016, Office 2013 och Office 2010 (till exempel Word, Excel, PowerPoint och Outlook) är exempel på program som enlightened för Rights Management. Men program som inte kommer från Microsoft, till exempel andra programvaruföretag för och dina egna av branschspecifika program kan också enlightened för Rights Management.<br /><br />Program som är enlightened för Rights Management veta hur du öppnar filer har skyddats av andra Rights Management enlightened program. De kvarstår även skydd som tillämpas på dem, även om du vill redigera filen eller spara den på ett annat namn eller en annan plats. Dessa program kan du använda filen enligt de behörigheter som tillämpas på filen så att om du har behörighet att använda filen kan du göra detta. Exempel: du kanske kan redigera filen men inte skriva ut den.|

## Exempel och andra instruktioner
Exempel på hur du kan använda den Rights Management dela program och instruktioner finns i följande avsnitt från Rights Management delning application användaren guide:

-   [Exempel på hur RMS-delning program](../Topic/Rights_Management_sharing_application_user_guide.md#BKMK_SharingExamples)

-   [Vad vill du göra?](../Topic/Rights_Management_sharing_application_user_guide.md#BKMK_SharingInstructions)

## Se även
[Rights Management delning användaren guide till](../Topic/Rights_Management_sharing_application_user_guide.md)

