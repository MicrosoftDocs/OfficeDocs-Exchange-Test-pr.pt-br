---
title: 'Criptografia do relatório de diário: Exchange 2013 Help'
TOCTitle: Criptografia do relatório de diário
ms:assetid: c063e2bd-2444-480d-8b35-73f31064a31b
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd876936(v=EXCHG.150)
ms:contentKeyID: 50486550
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Criptografia do relatório de diário

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2012-10-16_

No Microsoft Exchange Server 2013, o gerenciamento de direitos de informação (IRM) permite que a Microsoft Outlook 2010 e versões posteriores e Microsoft OfficeOutlook Web App usuários protejam suas mensagens. Você pode criar regras de proteção para aplicar automaticamente a proteção de IRM às mensagens antes que eles enviados a partir de um cliente Outlook 2010Outlook. Você também pode criar regras de proteção para aplicar a proteção IRM a mensagens em trânsito que correspondam às condições de regra de transporte.

Para saber mais sobre as regras de proteção do Outlook, consulte [Regras de proteção do Outlook](outlook-protection-rules-exchange-2013-help.md).

## Limitações das soluções de criptografia padrão

Se sua organização criptografa mensagens usando soluções tradicionais como S/MIME, os gerentes de registros não conseguirá inspecionar ou pesquisar o conteúdo criptografado. Arquivamento de mensagens criptografadas que contêm conteúdo inacessível e não pesquisável pode não atender aos requisitos de conformidade ou de negócios, normativos. Quando se depara com uma solicitação de descoberta eletrônica (eDiscovery), a incapacidade de descriptografar, pesquisa e apresente o conteúdo de mensagens criptografadas podem ser um desafio, e não fizer isso pode expor a sua organização a riscos legais e financeiros.

Além disso, as políticas de mensagens da sua organização podem exigir mensagens registradas no diário a ser descriptografado para que o conteúdo possa ser acessado para descoberta eletrônica ferramentas, processos automatizados ou gerentes de registros que acessam a uma caixa de correio de registro no diário. Descriptografia do relatório de diário no Exchange 2010 pode ajudá-lo a atender a esses requisitos.

Para saber mais sobre registro no diário, consulte [Registro no Diário](journaling-exchange-2013-help.md).

## Criptografia do relatório de diário

Descriptografia do relatório de diário permite que você salve uma cópia de texto não criptografado das mensagens protegidas por IRM em relatórios de diário, junto com a mensagem original, protegidas por IRM. Se a mensagem protegida por IRM contém todos os anexos com suporte que estavam protegidos pelo cluster Active Directory Rights Management Services (AD RMS) em sua organização, os anexos também são descriptografados.


> [!IMPORTANT]
> Para usar a descriptografia do relatório de diário, você deve ter uma licença de acesso para cliente (CAL) Exchange Enterprise. Descriptografia do relatório de diário suporta apenas o registro no diário premium.



Descriptografia é realizada pelo agente de descriptografia do relatório de diário, um agente de transporte voltadas à conformidade. O agente de descriptografia do relatório de diário aciona o evento **OnCategorizedMessage** . Em trânsito de mensagens protegidas usando regras já são criptografadas pelo agente de criptografia, que dispara o evento **OnRoutedMessage** , antes que eles cheguem ao agente de descriptografia do relatório de diário de proteção de transporte. O agente de descriptografia do relatório de diário descriptografa essas mensagens.


> [!TIP]
> Em Exchange 2013, o agente de descriptografia do relatório de diário é um agente interno. Agentes internos não estão incluídos na lista de agentes retornada pelo cmdlet <STRONG>Get-TransportAgent</STRONG> . Para obter mais detalhes, consulte <A href="transport-agents-exchange-2013-help.md">Agentes de transporte</A>.



O agente descriptografa os seguintes tipos de mensagens protegidas por IRM:

  - Mensagens que foram protegidas por IRM pelo usuário em Outlook Web App.

  - Mensagens que foram protegidas por IRM pelo usuário em Outlook 2010.

  - Mensagens que foram protegidas por IRM automaticamente em Outlook 2010 usando regras de proteção de Outlook.

  - Mensagens que foram protegidas por IRM automaticamente em trânsito usando regras de proteção de transporte.


> [!IMPORTANT]
> Somente as mensagens que foram protegidas por IRM pelo servidor do AD RMS em sua organização sejam descriptografadas pelo agente de descriptografia do relatório de diário. O agente não descriptografar um anexo, se ele não estiver protegido ao mesmo tempo que a mensagem (e, portanto, não tem a mesma licença de uso), ou se um arquivo protegido por IRM é anexado a uma mensagem desprotegida.



## Configurando a descriptografia do relatório de diário

Descriptografia do relatório de diário é configuredb usando o cmdlet [Set-IRMConfiguration](https://technet.microsoft.com/pt-br/library/dd979792\(v=exchg.150\)) em Exchange Management Shell. No entanto, antes de configurar descriptografia do relatório de diário, você deve atribuir servidores Exchange 2013 as permissões para descriptografar o conteúdo protegido por IRM pelo seu servidor AD RMS. Para fazer isso, você pode adicionar a caixa de correio de Federação ao grupo de superusuários configurado no cluster do AD RMS da sua organização. Para obter detalhes, consulte [Adicionar a caixa de correio de Federação ao grupo de usuários do AD RMS Super](add-the-federation-mailbox-to-the-ad-rms-super-users-group-exchange-2013-help.md).


> [!IMPORTANT]
> Nas implantações do AD RMS entre florestas onde você tinha um cluster do AD RMS implantado em cada floresta, você deve adicionar a caixa de correio de Federação ao grupo superusuários no cluster do AD RMS em cada floresta para permitir que Exchange 2013 o serviço de transporte para descriptografar as mensagens protegidas contra cada cluster do AD RMS.



Para obter detalhes sobre como configurar a descriptografia do relatório de diário, consulte [Habilitar ou desabilitar a descriptografia do relatório de diário](enable-or-disable-journal-report-decryption-exchange-2013-help.md).

Após habilitar a descriptografia do relatório de diário, a caixa de correio de registro no diário pode conter relatórios de diário com informações confidenciais de forma descriptografada. Como prática recomendada, recomendamos que o acesso à caixa de correio de registro no diário ser monitorado de perto e restrito somente a indivíduos autorizados. Isso é uma prática recomendada, mesmo se você não estiver usando a proteção de IRM para email.

