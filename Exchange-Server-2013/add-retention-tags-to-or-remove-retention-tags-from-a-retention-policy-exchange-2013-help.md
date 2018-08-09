---
title: 'Adicionar ou remover marcas de retenção de uma política de retenção'
TOCTitle: Adicionar marcas de retenção com ou remova as marcas de retenção uma política de retenção
ms:assetid: 3a5196ce-2764-453d-9bc1-5ec22d06b40d
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd362328(v=EXCHG.150)
ms:contentKeyID: 50485351
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Adicionar marcas de retenção com ou remova as marcas de retenção uma política de retenção

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013_

_**Tópico modificado em:** 2015-03-02_

Você pode adicionar marcas de retenção a uma diretiva de retenção quando a diretiva é criada ou a qualquer momento depois disso. Para detalhes sobre como criar uma diretiva de retenção, incluindo como adicionar simultaneamente marcas de retenção, consulte [Criar uma política de retenção](create-a-retention-policy-exchange-2013-help.md).

Uma diretiva de retenção pode conter as seguintes marcas de retenção:

  - Uma ou mais RPTs (marcas de diretiva de retenção) para pastas-padrão suportadas

  - Uma marca de política padrão (DPT) com a ação **Mover para Arquivo Morto**

  - Uma DPT com a ação **Excluir e Permitir Recupeção** ou **Excluir Permanentemente**

  - Uma DPT para caixa postal

  - Qualquer número de marcas pessoais

Para obter mais informações sobre marcas de retenção, consulte [Marcas e políticas de retenção](retention-tags-and-retention-policies-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 10 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Gerenciamento de registros de mensagens" no tópico [Permissões de destinatários](recipients-permissions-exchange-2013-help.md).

  - Marcas de retenção não serão aplicadas a uma caixa de correio até que estejam vinculados a uma política de retenção e o Assistente de pasta gerenciada processa a caixa de correio. Para iniciar o Assistente de pasta gerenciada para que ele processe uma caixa de correio, consulte [Configurar o Assistente de pasta gerenciada](configure-the-managed-folder-assistant-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## O que você deseja fazer?

## Usar o EAC para adicionar ou remover as marcas de retenção

1.  Vá até **gerenciamento de conformidade** \>**políticas de retenção**.

2.  No modo de exibição de lista, selecione a política de retenção para a qual você deseja adicionar marcas de retenção e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Em **Política de Retenção**, use as seguintes configurações:
    
      - **Adicionar** ![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar")   Clique neste botão para adicionar uma marca de retenção à política.
    
      - **Remover** ![ícone Remover](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "ícone Remover")   Selecione uma marca da lista e clique nesse botão, para removê-la da política.

## Usar o Shell para adicionar ou remover as marcas de retenção

Este exemplo adiciona as marcas de retenção VPs-Default, VPs-Inbox e VPs-DeletedItems à diretiva de retenção RetPolicy-VPs, que ainda não possui marcas de retenção vinculadas a ela.


> [!WARNING]
> Se a diretiva tiver marcas de retenção vinculadas a ela, esse comando substituirá as marcas existentes.



    Set-RetentionPolicy -Identity "RetPolicy-VPs" -RetentionPolicyTagLinks "VPs-Default","VPs-Inbox","VPs-DeletedItems"

Este exemplo adiciona a marca de retenção VPs-DeletedItems à diretiva de retenção RetPolicy-VPs, que já possui outras marcas de retenção vinculadas a ela.

    $TagList = (Get-RetentionPolicy "RetPolicy-VPs").RetentionPolicyTagLinks
    $TagList.Add((Get-RetentionPolicyTag 'VPs-DeletedItems').DistinguishedName)
    Set-RetentionPolicy "RetPolicy-VPs" -RetentionPolicyTagLinks $TagList

Esse exemplo remove a marca de retenção VPs-Inbox da diretiva de retenção RetPolicy-VPs.

    $TagList = (Get-RetentionPolicy "RetPolicy-VPs").RetentionPolicyTagLinks
    $TagList.Remove((Get-RetentionPolicyTag 'VPs-Inbox').DistinguishedName)
    Set-RetentionPolicy "RetPolicy-VPs" -RetentionPolicyTagLinks $TagList

Para obter informações detalhadas sobre sintaxe e parâmetros, consulte [Set-RetentionPolicy](https://technet.microsoft.com/pt-br/library/dd335196\(v=exchg.150\)) e [Get-RetentionPolicy](https://technet.microsoft.com/pt-br/library/dd298086\(v=exchg.150\)).

## Como saber se funcionou?

Para verificar se você adicionou ou removeu com êxito uma marca de retenção de uma política de retenção, use o cmdlet [Get-RetentionPolicy](https://technet.microsoft.com/pt-br/library/dd298086\(v=exchg.150\)) para verificar a propriedade *RetentionPolicyTagLinks*.

Este exemplo usa o cmdlet **Get-RetentionPolicy** para recuperar marcas de retenção adicionadas à Política MRM Padrão e as enviar para o cmdlet **Format-Table**, para informar somente a propriedade do nome de cada marca.

    (Get-RetentionPolicy "Default MRM Policy").RetentionPolicyTagLinks | Format-Table name

