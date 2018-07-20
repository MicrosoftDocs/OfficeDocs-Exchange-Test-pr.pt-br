---
title: 'Active Directory: Exchange 2013 Help'
TOCTitle: Active Directory
ms:assetid: 8e8464df-2d1d-4d68-82de-b0c158c549c3
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb123715(v=EXCHG.150)
ms:contentKeyID: 50486137
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Active Directory

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2016-12-09_

Microsoft Exchange Server 2013 usa Active Directory para armazenar e compartilhar informações de diretório com Windows. design de floresta de Active Directory para Exchange 2013 é semelhante ao Exchange Server 2010, exceto em algumas maneiras, que são discutidas abaixo.

## Driver do Active Directory

O driver de Active Directory é o componente de Exchange Microsoft core que permite aos serviços de Exchange criar, modificar, excluir e consultar Active Directory dados de serviços de domínio (AD DS). Em Exchange 2013, todo o acesso aos Active Directory é feito usando o driver de Active Directory em si. Anteriormente, em Exchange 2010, DSAccess fornecidos serviços de pesquisa de diretório para componentes como o repositório de Exchange, o agente de transferência de mensagem (MTA) e SMTP.

O driver Active Directory também usa a Microsoft ExchangeActive Directory topologia (MSExchangeADTopology), que permite que o driver Active Directory usar os dados de topologia do Directory Service Access (DSAccess). Esses dados incluem a lista de controladores de domínio disponível e servidores de catálogo global disponíveis para lidar com solicitações de Exchange. Para obter mais informações sobre o Active Directory Driver, consulte [Active Directory Domain Services](https://go.microsoft.com/fwlink/p/?linkid=110942).

## Alterações de esquema do Active Directory

Exchange 2013 adiciona novos atributos para o esquema do serviço de domínio Active Directory e também realiza outras modificações atributos e classes existentes. Para obter mais informações sobre alterações de Active Directory quando você instala o Exchange 2013, consulte [Alterações de esquema do Active Directory no Exchange 2013](exchange-2013-active-directory-schema-changes-exchange-2013-help.md).

## Para saber mais

Para aprender mais sobre como Exchange 2013 armazena e recupera as informações no Active Directory para que você possa planejar acesso a ele, consulte [Acesso ao Active Directory](access-to-active-directory-exchange-2013-help.md).

Para obter mais informações sobre o design de floresta Active Directory, consulte o [Guia de Design do AD DS](https://go.microsoft.com/fwlink/p/?linkid=264957).

Para saber mais sobre os computadores que executam o Windows em um domínio do Active Directory e implantando Exchange 2013, em um domínio que tenha um namespace separado, consulte [Cenários de namespace separado](disjoint-namespace-scenarios-exchange-2013-help.md).

