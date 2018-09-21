---
title: 'Gerenciar políticas de DLP: Exchange 2013 Help'
TOCTitle: Gerenciar políticas de DLP
ms:assetid: ba81fabd-7f7f-4ef7-968f-ce851ada9d70
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ673559(v=EXCHG.150)
ms:contentKeyID: 50486495
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Gerenciar políticas de DLP

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013_

_**Tópico modificado em:** 2015-01-14_

Você pode exibir, alterar ou remover políticas de (DLP) de prevenção de perda de dados existente no Microsoft Exchange, usando o Centro de administração do Exchange (EAC) ou o Shell de gerenciamento do Exchange.

Para tarefas de gerenciamento adicionais relacionadas a DLP, consulte [Procedimentos DLP](dlp-procedures-exchange-2013-help.md) (Exchange Server 2013 ) ou [Procedimentos DLP](https://technet.microsoft.com/pt-br/library/jj938003\(v=exchg.150\)) (Exchange Online ).

Para obter mais informações sobre o Shell de gerenciamento do Exchange, consulte [Usando o PowerShell com o Exchange 2013 (Shell de gerenciamento do Exchange)](https://technet.microsoft.com/pt-br/library/bb123778\(v=exchg.150\)).

## O que você precisa saber antes de começar?

  - Tempo estimado para concluir cada procedimento: 15 a 60 minutos

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada \&quot;Prevenção de perda de dados (DLP)\&quot; no tópico [Permissões de política e conformidade de mensagens](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - Para qualquer política DLP, você pode selecionar um dos três modos:
    
      -    **Impor**   Regras dentro da política são avaliadas por todas as mensagens e tipos de arquivo suportados. O fluxo de emails poderá ser interrompido, se forem detectados dados que atenderem às condições da política. Todas as ações descritas no âmbito da política são tomadas.
    
      -    **Testar política DLP com Dicas de Política**   Regras dentro da política são avaliadas por todas as mensagens e tipos de arquivo suportados. O fluxo de emails não será interrompido, se forem detectados dados que atenderem às condições da política. Ou seja, as mensagens não serão bloqueadas. Se as Dicas de Política estiverem configuradas, elas serão mostradas para os usuários.
    
      -    **Testar política DLP sem Dicas de Política**   Regras dentro da política são avaliadas por todas as mensagens e tipos de arquivo suportados. O fluxo de emails não será interrompido, se forem detectados dados que atenderem às condições da política. Ou seja, as mensagens não serão bloqueadas. Se as Dicas de Política estiverem configuradas, elas não serão mostradas para os usuários.

  - Uma regra individual em uma política de DLP pode ter suas próprias configurações de modo. Quando o modo de uma política for diferente do que o modo de uma regra dentro dessa política, a configuração da regra tem prioridade e será avaliada de acordo com o seu modo.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## O que você deseja fazer?

## Exibir os detalhes de uma política DLP existente

Você pode precisar exibir as regras e ações de uma política DLP existente que você já tiver estabelecido para sua organização. Isso pode ser útil se você tiver problemas de fluxo de email inesperado ou se sua organização altera a maneira como as informações confidenciais precisam ser monitorado.

## Usar o EAC para exibir os detalhes de uma política DLP existente

1.  No EAC, navegue até **gerenciamento de conformidade** \> **prevenção de perda de dados**.

2.  Clique duas vezes em uma das políticas que aparecem na sua lista de políticas, ou realce um item e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na página **política de DLP Editar**, clique em **regras**.


> [!TIP]
> Você pode criar uma política de DLP e deixá-lo em um modo não está ativado ou desativado. Neste modo, uma política não é imposta e você pode alterar qualquer predicados, ações ou valores associados com suas regras antes de testar ou começar impô-la.



## Use o Shell para exibir os detalhes de uma política DLP existente

Este exemplo retorna informações sobre a política DLP fictícia chamada Employee Numbers. O comando é canalizado para o cmdlet **Format-List** para exibir a configuração detalhada de política de DLP especificada.

    Get-DlpPolicy "Employee Numbers" | Format-List

Para obter informações de sintaxe e parâmetros, consulte [Get-DlpPolicy](https://technet.microsoft.com/pt-br/library/jj215752\(v=exchg.150\)).

## Alterar uma política de DLP

Você pode alterar uma política existente de DLP, modificando o nome da política ou as regras que determinam os efeitos da diretiva. Uma alteração de regra de exemplo pode incluir a adição de texto de isenção de responsabilidade personalizados para um corpo da mensagem e a proteção de RMS para mensagens enviadas dentro de um domínio específico e que são detectados tenha informações confidenciais. Se você estiver usando modelos de política DLP, tenha em mente que esses são apenas um dos recursos do Exchange 2013 que podem ajudá-lo a projetar e aplicar um sistema de política e conformidade robusto para seu ambiente de mensagens.

## Usar o EAC para alterar uma política DLP existente

1.  No EAC, navegue até **gerenciamento de conformidade** \> **prevenção de perda de dados**.

2.  Clique duas vezes em uma das políticas baseada no modelo que aparecem na sua lista de políticas ou realce um item e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na página **política de DLP Editar**, clique em **regras**.

4.  Para alterar uma regra existente, realce a regra e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

5.  Para adicionar uma nova regra em branco que você possa personalizar completamente, clique em **New**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar").

6.  Para adicionar uma regra de notificação do remetente, bloqueio de mensagens ou permitindo substituições, clique na seta ao lado do ícone de![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar")**New**.

7.  Para remover uma regra, realce a regra e clique em **Excluir**![Excluir ícone](images/JJ673559.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Excluir ícone").

8.  Clique em **Salvar** para concluir a modificação a política e salvar suas alterações.

## Use o Shell para alterar uma política DLP existente

Você pode especificar o nível de notificação e a ação de uma diretiva usando o Shell de gerenciamento do Exchange. Este exemplo define o modo para uma política de DLP fictícia chamada Employee Numbers para que as ações não são impostas e mensagens de notificação não são exibidas.

    Set-DlpPolicy "Employee Numbers" -Mode Audit

Para obter informações de sintaxe e parâmetros, consulte [Set-DlpPolicy](https://technet.microsoft.com/pt-br/library/jj215778\(v=exchg.150\)).

## Excluir uma política DLP

Você pode remover permanentemente uma política de DLP usando o EAC. Depois de excluir uma política, ela não é mais será imposta e nenhuma das regras e ações serão salvas.

Como alternativa, você pode definir o estado operacional ou o modo de uma política para a **política de DLP de teste sem dicas de política**. Isso impede que ele está sendo imposta em seu ambiente de mensagem, mas preserva as configurações detalhadas da configuração da política em si. Isso pode ser útil se existe uma possibilidade de que você precisará para impor a diretiva novamente no futuro.

## Usar o EAC para excluir uma política DLP existente

1.  No EAC, navegue até **gerenciamento de conformidade** \> **prevenção de perda de dados**.

2.  Selecione a política que você deseja remover em sua lista de políticas e clique em **Excluir**![Excluir ícone](images/JJ673559.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Excluir ícone").

## Use o Shell para excluir uma política DLP existente

Este exemplo remove a política de DLP fictícia chamada Employee Numbers.

    Remove-DlpPolicy "Employee Numbers"

Para obter informações de sintaxe e parâmetros, consulte [Remove-DlpPolicy](https://technet.microsoft.com/pt-br/library/jj215677\(v=exchg.150\)).

## Para obter mais informações

[Prevenção de perda de dados](https://docs.microsoft.com/pt-br/exchange/security-and-compliance/data-loss-prevention/data-loss-prevention)

[Dicas de política](https://docs.microsoft.com/pt-br/exchange/security-and-compliance/data-loss-prevention/policy-tips)

