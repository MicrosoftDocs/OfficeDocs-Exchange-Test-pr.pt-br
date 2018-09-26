---
title: 'Habilitar ou desabilitar a descriptografia de transporte: Exchange 2013 Help'
TOCTitle: Habilitar ou desabilitar a descriptografia de transporte
ms:assetid: 4663f54e-dd0a-4a42-983e-8765e2adc412
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd638126(v=EXCHG.150)
ms:contentKeyID: 50485465
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Habilitar ou desabilitar a descriptografia de transporte

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013_

_**Tópico modificado em:** 2016-12-09_

Habilitar a descriptografia de transporte permite que o agente de regras de transporte no Microsoft Exchange Server 2013 servidores de caixa de correio acessar o conteúdo em mensagens protegidas pelo gerenciamento de direitos de informação (IRM). Como resultado, outros agentes de transporte podem acessar o conteúdo da mensagem e, possivelmente, fazer alterações nele. Por exemplo, o agente de regras de transporte talvez seja necessário inspecionar o conteúdo da mensagem e aplicar regras de transporte (por exemplo, as regras que se aplicam a um aviso de isenção à mensagem). Para descriptografar com êxito mensagens protegidas por IRM, você deve adicionar a caixa de correio de entrega federados ao grupo de superusuários configurado em seu servidor do [Active Directory Rights Management Services (AD RMS)](https://technet.microsoft.com/en-us/library/hh831364.aspx) .


> [!IMPORTANT]
> Os membros do grupo de superusuários recebem uma licença de usuário de proprietário quando solicitam uma licença ao cluster do AD RMS. Isso permite a eles descriptografar todo o conteúdo protegido por DRM criado por esse cluster do AD RMS.



Ao habilitar a descriptografia de transporte, você pode especificar as configurações a seguir:

  - **Obrigatório**    Enviar rejeita mensagens que não podem ser descriptografadas e retorna um relatório de falha na entrega (NDR) ao remetente.

  - **Opcional**    Usa uma abordagem de melhor esforço para descriptografia. Se possível, as mensagens sejam descriptografadas, mas eles estiver entregues, mesmo se a descriptografia falha. Esta é a configuração padrão.

Para saber mais sobre a descriptografia de transporte, consulte [Descriptografia de transporte](transport-decryption-exchange-2013-help.md).

Para tarefas de gerenciamento adicionais relacionadas a IRM, consulte [Procedimentos de gerenciamento de direitos de informação](information-rights-management-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 5 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Proteção por direitos" no tópico [Permissões de política e conformidade de mensagens](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - Um servidor AD RMS existe na floresta Active Directory e está acessível.

  - A caixa de correio de entrega federada foi adicionada ao grupo de superusuários do AD RMS. Para obter detalhes, consulte [Adicionar a caixa de correio de Federação ao grupo de usuários do AD RMS Super](add-the-federation-mailbox-to-the-ad-rms-super-users-group-exchange-2013-help.md).

  - Você não pode usar o Centro de administração do Exchange (EAC) para habilitar a descriptografia de transporte. Você deve usar o Shell.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## O que você deseja fazer?

## Use o Shell para habilitar a descriptografia de transporte

Este exemplo habilita a descriptografia de transporte para a organização Exchange 2013. As mensagens que não podem ser descriptografadas são rejeitadas e uma NDR é retornada ao remetente.

```powershell
Set-IRMConfiguration -TransportDecryptionSetting Mandatory
```

Para obter informações detalhadas de sintaxes e de parâmetros, confira [Set-IRMConfiguration](https://technet.microsoft.com/pt-br/library/dd979792\(v=exchg.150\)).

## Use o Shell para desabilitar a descriptografia de transporte

Este exemplo desabilita a descriptografia de transporte para a organização Exchange 2013.

```powershell
Set-IRMConfiguration -TransportDecryptionSetting Disabled
```

Para obter informações detalhadas de sintaxes e de parâmetros, confira [Set-IRMConfiguration](https://technet.microsoft.com/pt-br/library/dd979792\(v=exchg.150\)).

## Como saber se funcionou?

Para verificar se você tiver habilitado ou desabilitado descriptografia de transporte, use o cmdlet **Get-IRMConfiguration** e verifica o valor da propriedade *JournalDecryptionEnabled* .

Para um exemplo de como verificar a configuração do IRM, consulte [Examples](https://technet.microsoft.com/pt-br/e1821219-fe18-4642-a9c2-58eb0aadd61a\(exchg.150\)#examples), em **Get-IRMConfiguration**.

