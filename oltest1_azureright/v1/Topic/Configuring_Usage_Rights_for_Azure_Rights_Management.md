---
description: na
keywords: na
title: Configuring Usage Rights for Azure Rights Management
search: na
ms.date: na
ms.service: rights-management
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 97ddde38-b91b-42a5-8eb4-3ce6ce15393d
---
# Konfigurera anv&#228;ndningsr&#228;ttigheter f&#246;r Azure Rights Management
När du ställa in skydd på filer eller e-postmeddelanden med hjälp av Azure Rights Management (Azure RMS) och du inte använder en mall, måste du konfigurera användningsrättigheterna själv. När du konfigurerar anpassade mallar för Azure RMS väljer du dessutom användningsrättigheterna sedan automatiskt tillämpas när mallen är markerad av användare, Administratörer, eller konfigureras för tjänster. Till exempel i Azure portal väljer du roller som konfigurerar en logisk gruppering av användningsrättigheter eller du kan konfigurera de enskilda rättigheterna.

Använd det här avsnittet för att konfigurera användningsrättigheterna som du vill använda för det program du använder och förstå hur dessa rättigheter tolkas av program.

## Användningsrättigheter och -beskrivning
I följande tabell listas och beskrivs användningsrättigheterna Rights Management stöder och hur de används och tolkas. I den här tabellen i **nätverksnamn** är vanligtvis hur du kan se hur visas eller refereras till som en mer eget version av enstaka ord-värde som används i koden (den **kodning i princip** värde). Den **API-konstant eller värdet** är SDK-namnet för en MSIPC API-anrop som används när du skriver ett RMS-upplysta program som söker efter användning av en höger eller lägger till användning av en rätt till en princip.

|Eget namn|Kodning i princip|Beskrivning|Implementering i Office anpassade rättigheter|Namnet i Azure-portalen|Namnet i AD RMS-mallar|API-konstant eller värde|Ytterligare information|
|-------------|---------------------|---------------|-------------------------------------------------|---------------------------|--------------------------|----------------------------|---------------------------|
|Redigera innehåll, redigera|DOCEDIT|Tillåter användare att ändra, ändra, formatera eller filtrera innehåll i programmet. Det ger behörighet att spara den redigerade kopian.|Som en del av den **ändra** och **fullständig behörighet** alternativ.|**Redigera innehåll**|**Redigera**|Inte tillämpligt|I Office-program kan den här behörigheten användare att spara dokumentet.|
|Spara|REDIGERA|Tillåter användare att spara dokumentet i dess nuvarande plats.|Som en del av den **ändra** och **fullständig behörighet** alternativ.|**Spara filen**|**Spara**|IPC_GENERIC_WRITEL "REDIGERA"|Den här behörigheten kan också användaren att ändra dokumentet i Office-program.|
|Kommentar|KOMMENTAR|Aktiverar alternativet att lägga till anteckningar och kommentarer till innehållet.|Inte införts|Inte införts|Inte införts|IPC_GENERIC_COMMENTL "KOMMENTAR"|Den här behörigheten finns i SDK är tillgänglig som en ad hoc-princip i RMS-skydd-modulen för Windows PowerShell och har implementerats i vissa program för leverantören. Dock används inte ofta och stöds inte för närvarande av Office-program.|
|Spara som, exportera|EXPORTERA|Aktiverar alternativet att spara innehållet i en annan fil (Spara som). Beroende på programmet, kan du spara filen utan skydd.|Som en del av den **ändra** och **fullständig behörighet** alternativ.|**Exportera innehållet (Spara som)**|**Exportera (Spara som)**|IPC_GENERIC_EXPORTL "EXPORT"|Den här behörigheten kan användare att utföra andra alternativ för export i program, exempelvis **Skicka till OneNote**.|
|Framåt|FRAMÅT|Aktiverar alternativet att vidarebefordra ett e-postmeddelande och lägga till mottagarna för den **till** och **kopia** rader.|Nekad när du använder den **Vidarebefordra inte** standard princip.|**Framåt**|**Framåt**|IPC_EMAIL_FORWARDL "FRAMÅT"|Tillåter inte att bevilja rättigheter till andra användare som en del av åtgärden vidarebefordra vidarebefordraren.|
|Fullständig kontroll|ÄGARE|Alla rättigheter till dokumentet och alla tillgängliga åtgärder kan utföras.|Som den **fullständig behörighet** anpassade alternativet.|**Fullständig kontroll**|**Fullständig kontroll**|IPC_GENERIC_ALLL "ÄGARE"|Innehåller möjligheten att ta bort skyddet.|
|Skriv ut|SKRIV UT|Aktiverar alternativ att skriva ut innehållet.|Som den **Skriv ut innehållet** alternativ i anpassade behörigheter. Inte en per mottagare inställning.|**Skriv ut**|**Skriv ut**|IPC_GENERIC_PRINTL "SKRIV UT|Ingen ytterligare information|
|Svar|SVAR|Aktiverar alternativet svar i en e-postklient utan att ändringar i den **till** eller **kopia** rader.|Inte tillämpligt|**Svar**|**Svar**|IPC_EMAIL_REPLY|Ingen ytterligare information|
|Svara alla|REPLYALL|Aktiverar den **Svara alla** alternativet i en e-postklient, men tillåter inte att lägga till mottagarna i **till** eller **kopia** rader.|Inte tillämpligt|**Svara alla**|**Svara alla**|IPC_EMAIL_REPLYALLL "REPLYALL"|Ingen ytterligare information|
|Visa öppna, läsa|VISA|Tillåter användare att öppna dokumentet och se innehållet.|Som den **Läs** anpassad princip **Visa** alternativet.|**Visa innehåll**|**Visa**|IPC_GENERIC_READL "VY"|Ingen ytterligare information|
|Kopiera|EXTRAHERA|Aktiverar alternativ för att kopiera data från dokumentet i samma eller en annan dokumentet.|Som den **användarna med läsbehörighet kan kopiera innehållet** alternativet anpassad princip.|**Kopiera och extrahera innehåll**|**Extrahera**|IPC_GENERIC_EXTRACTL "EXTRAHERA"|I vissa program kan också hela dokumentet sparas i oskyddat format.|
|Visa rättigheter|VIEWRIGHTSDATA|Gör att användaren kan se principer som tillämpas på dokumentet.|Inte införts|**Visa tilldelade rättigheter**|**Visa rättigheter**|IPC_READ_RIGHTSL "VIEWRIGHTSDATA"|Ignoreras av vissa program.|
|Ändra rättigheter|EDITRIGHTSDATA|Tillåter användare att ändra principer som tillämpas på dokumentet. Innehåller även ta bort skyddet.|Inte införts|**Ändra rättigheter**|**Redigera rättigheter**|IPC_WRITE_RIGHTSL "EDITRIGHTSDATA"|Ingen ytterligare information|
|Tillåt makron|OBJMODEL|Aktiverar alternativet att köra makron eller utföra andra programmässiga eller fjärransluten åtkomst till innehållet i ett dokument.|Som den **Tillåt Programmeringsåtkomst** alternativet anpassad princip. Inte en per mottagare inställning.|**Tillåt makron**|**Tillåt makron**|Inte tillämpligt|Ingen ytterligare information|

## Rättigheter behörighetsnivåer
Vissa program grupperas användningsrättigheter till behörighetsnivåer att göra det lättare att välja användningsrättigheter som normalt används tillsammans. Dessa permisisons nivåer för att abstrakt en nivå av komplexitet från användare, så att de kan välja alternativ som är rollbaserad.  Till exempel **granskare** och **medförfattare**. Dessa alternativ visas ofta användare en sammanfattning av rättigheter, kanske de inte innehåller alla höger som listas i föregående tabell.

Använd följande tabell för en lista över dessa behörighetsnivåer och en fullständig lista över de rättigheter som de innehåller.

|Åtkomstnivå|Program|Rättigheter (nätverksnamn)|
|---------------|-----------|------------------------------|
|Loggboken|Azure-portalen<br /><br />Rights Management sharing application för Windows|Visa öppna, läsa<br /><br />Svar<br /><br />Svara alla|
|Granskare|Azure-portalen<br /><br />Rights Management sharing application för Windows|Visa öppna, läsa<br /><br />Spara<br /><br />Redigera innehåll, redigera<br /><br />Reply<sup>*</sup><br /><br />Svara alla<sup>*</sup><br /><br />Vidarebefordra<sup>*</sup>|
|Medförfattare|Azure-portalen<br /><br />Rights Management sharing application för Windows|Visa öppna, läsa<br /><br />Spara<br /><br />Redigera innehåll, redigera<br /><br />Kopiera<br /><br />Visa rättigheter<br /><br />Ändra rättigheter<br /><br />Tillåt makron<br /><br />Spara som, exportera<br /><br />Skriv ut<br /><br />Reply<sup>*</sup><br /><br />Svara alla<sup>*</sup><br /><br />Vidarebefordra<sup>*</sup>|
|Medägare|Azure-portalen<br /><br />Rights Management sharing application för Windows|Visa öppna, läsa<br /><br />Spara<br /><br />Redigera innehåll, redigera<br /><br />Kopiera<br /><br />Visa rättigheter<br /><br />Ändra rättigheter<br /><br />Tillåt makron<br /><br />Spara som, exportera<br /><br />Skriv ut<br /><br />Reply<sup>*</sup><br /><br />Svara alla<sup>*</sup><br /><br />Vidarebefordra<sup>*</sup><br /><br />Fullständig kontroll|
<sup>*</sup> Inte gäller för Rights Management sharing application för Windows

## Rättigheter som standardmallar
Behörighet som ingår i standardmallar är följande:

|Visningsnamn|Rättigheter (nätverksnamn)|
|----------------|------------------------------|
|&lt; organisationsnamn &gt; - endast konfidentiell vy|Visa öppna, läsa|
|&lt; organisationsnamn &gt; - konfidentiell|Visa öppna, läsa<br /><br />Spara<br /><br />Redigera innehåll, redigera<br /><br />Visa rättigheter<br /><br />Tillåt makron<br /><br />Framåt<br /><br />Svar<br /><br />Svara alla|

## Se även
[Konfigurera Azure Rights Management](../Topic/Configuring_Azure_Rights_Management.md)

