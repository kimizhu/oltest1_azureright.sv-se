---
description: na
keywords: na
title: Preparing for Azure Rights Management
search: na
ms.date: na
ms.service: rights-management
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: afbca2d6-32a7-4bda-8aaf-9f93f5da5abc
---
# F&#246;rbereder Azure Rights Management
När du har registrerat en prenumeration för molnet och etablerade organisationen med ett konto för [!INCLUDE[o365_1](../Token/o365_1_md.md)] eller Azure Active Directory är du redo att aktivera den [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)] service.

Men innan du gör det, kontrollera att följande är på plats:

-   Användare och grupper i molnet som du skapar manuellt eller som automatiskt skapas och synkroniseras från Active Directory Domain Services (AD DS).

    När du synkroniserar dina lokala konton och grupper, behöver inte alla attribut som ska synkroniseras. En lista över attribut som måste synkroniseras för Azure RMS, finns i det här [Azure RMS avsnittet](https://azure.microsoft.com/documentation/articles/active-directory-aadconnectsync-attributes-synchronized/) från Azure Active Directory-dokumentationen. För enkel distribution, rekommenderar vi att du använder [Azure AD Connect](http://azure.microsoft.com/documentation/articles/active-directory-aadconnect/) ansluta dina lokala kataloger med Azure Active Directory, men du kan använda alla directory synkroniseringsmetoden som ger samma resultat.

-   E-postaktiverade grupper i molnet som du vill använda med Rights Management. Dessa kan vara inbyggda grupper eller grupper som innehåller användare som använder Rights Management har skapat manuellt.

    Om du har Exchange Online kan du skapa och använda e-postaktiverade grupper med hjälp av Administrationscenter för Exchange. Om du har AD DS och synkroniseras till Azure AD kan du skapa och använda e-postaktiverade grupper som är säkerhetsgrupper och distributionsgrupper.

## Aktivera Rights Management
Som standard [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)] inaktiveras när du registrerar dig för din [!INCLUDE[o365_2](../Token/o365_2_md.md)] eller Azure AD-konto. Så här aktiverar du [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)] för din organisation, måste du aktivera tjänsten. Mer information finns i [Aktivera Azure Rights Management](../Topic/Activating_Azure_Rights_Management.md).

## Se även
[Konfigurera Azure Rights Management](../Topic/Configuring_Azure_Rights_Management.md)

