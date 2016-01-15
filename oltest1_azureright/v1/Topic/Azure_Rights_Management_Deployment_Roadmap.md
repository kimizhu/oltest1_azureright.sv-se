---
description: na
keywords: na
title: Azure Rights Management Deployment Roadmap
search: na
ms.date: na
ms.service: rights-management
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 086600c2-c5d8-47ec-a4c0-c782e1797486
---
# &#214;versikt &#246;ver Azure Rights Management-distribution
Använd följande steg för att förbereda, implementera och hantera Azure Rights Management (Azure RMS) för din organisation.

Men om du vill prova Azure RMS snabbt för dig själv än lyfts upp i en produktionsmiljö Se [Snabbstart vägledning för Azure Rights Management](../Topic/Quick_Start_Tutorial_for_Azure_Rights_Management.md).

> [!IMPORTANT]
> Innan du gör du följande kontrollerar du att du har granskat [Krav för Azure Rights Management](../Topic/Requirements_for_Azure_Rights_Management.md).

## Steg 1: Kontrollera att du har en prenumeration som innehåller Azure Rights Management
Det finns mer än en typ av prenumeration som innehåller [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)]. Finns det [Molnet prenumerationer som har stöd för Azure RMS](../Topic/Requirements_for_Azure_Rights_Management.md#BKMK_SupportedSubscriptions) under den [Krav för Azure Rights Management](../Topic/Requirements_for_Azure_Rights_Management.md) avsnittet och kontrollera att prenumerationen innehåller funktioner som du vill använda i din organisation genom att referera till tabellen i [erbjudanden för jämförelse av Rights Management Services (RMS)](https://technet.microsoft.com/dn858608).

## Steg 2: Förbered kontot innehavaren att använda Rights Management
Innan du börjar med [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)], gör följande förberedelse av:

1.  Se till att innehavare Azure och Office 365 innehåller användarkonton och grupper som ska användas av Azure RMS för att autentisera användare från din organisation. Om det behövs, skapa dessa konton och grupper eller synkronisera dem från din lokala katalog. Mer information finns i [Förbereder Azure Rights Management](../Topic/Preparing_for_Azure_Rights_Management.md).

2.  Bestäm om du vill att Microsoft ska hantera innehavaren nyckeln (standard), eller skapa och hantera klient-nyckel själv (kallas ta med din egen nyckel eller BYOK). Observera att för tillfället, du inte kan använda BYOK om du använder Exchange Online. Mer information finns i [Planera och implementera din Azure Rights Management innehavaren nyckel](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md).

3.  Installera Windows PowerShell-modul för [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)] på minst en dator som har Internetanslutning. Du kan göra det här steget nu eller senare. Mer information finns i [Installera Windows PowerShell för Azure Rights Management](../Topic/Installing_Windows_PowerShell_for_Azure_Rights_Management.md).

4.  Om du använder lokala Rights Management services: Utför en migrering att flytta nycklar, mallar och URL: er till molnet. Mer information finns i [Migrera från AD RMS till Azure Rights Management](../Topic/Migrating_from_AD_RMS_to_Azure_Rights_Management.md).

5.  Aktivera Rights Management så att du kan börja använda tjänsten. Om det krävs en fasindelad distribution, konfigurera inledande användarinställningar om du vill begränsa användning till särskilda användare. Mer information finns i [Aktivera Azure Rights Management](../Topic/Activating_Azure_Rights_Management.md).

Du kan även konfigurera följande:

-   Anpassade mallar om standard rättighetsprincipmallar är inte tillräckliga för din organisation. Du kan göra det här steget nu eller senare. Mer information finns i [Konfigurera anpassade mallar för Azure Rights Management](../Topic/Configuring_Custom_Templates_for_Azure_Rights_Management.md).

-   Användningen av loggning så att du kan övervaka hur din organisation använder Rights Management. Du kan göra det här steget nu eller senare. Mer information finns i [Loggning och analysera Azure Rights Management användning](../Topic/Logging_and_Analyzing_Azure_Rights_Management_Usage.md).

## Steg 3: Konfigurera program och tjänster för Rights Management
Konfigurera dina program kan innehålla installera Rights Management delning och aktiverar stöd för information rights management (IRM) funktioner i SharePoint Online eller Exchange Online. Mer information finns i [Konfigurera program för Azure Rights Management](../Topic/Configuring_Applications_for_Azure_Rights_Management.md).

Om du har befintliga IT-tjänster som behöver för att granska filer som Azure RMS skyddar – innehåll kryptering gateways (CEG) och program mot skadlig produkter, till exempel data läcka förhindra (DLP) lösningar – Konfigurera tjänstkonton ska Superanvändare för Azure RMS. Mer information finns i [Konfigurera Super Users för Azure Rights Management och identifiering av tjänster eller återställning av Data](../Topic/Configuring_Super_Users_for_Azure_Rights_Management_and_Discovery_Services_or_Data_Recovery.md).

Om du har lokala tjänster som du vill använda med Azure Rights Management kan du installera och konfigurera Rights Management-koppling. Mer information finns i [Distribuera Azure Rights Management-koppling](../Topic/Deploying_the_Azure_Rights_Management_Connector.md).

## Steg 4: Publicera och förbruka rättigheter-skyddat innehåll
Du är nu klar att publicera och använda skyddat innehåll och logga hur ditt företag använder Rights Management. Mer information finns i [Använda Azure Rights Management](../Topic/Using_Azure_Rights_Management.md).

## Steg 5: Administrera Rights Management för ditt konto innehavaren efter behov
När du börjar använda [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)], du kan hitta den [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)] modul för Windows PowerShell praktiskt att hjälpa skript eller automatisera administrativa ändringar. Mer information finns i [Administrera Azure Rights Management med Windows PowerShell](../Topic/Administering_Azure_Rights_Management_by_Using_Windows_PowerShell.md).

## Se även
[Konfigurera Azure Rights Management](../Topic/Configuring_Azure_Rights_Management.md)

