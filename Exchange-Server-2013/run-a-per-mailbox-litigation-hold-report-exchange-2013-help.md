---
title: 'Executar um relatório de suspensão de litígio por caixa de correio: Exchange 2013 Help'
TOCTitle: Executar um relatório de suspensão de litígio por caixa de correio
ms:assetid: 98c46226-2f48-42c6-a741-34bb5944f519
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ150542(v=EXCHG.150)
ms:contentKeyID: 50484757
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Executar um relatório de suspensão de litígio por caixa de correio

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013_

_**Tópico modificado em:** 2012-10-13_

Se sua organização estiver envolvida em uma ação judicial, você talvez precise executar etapas para preservar dados relevantes, como mensagens de email, que podem ser usadas como evidência. Em situações como essa, você pode usar o litígio para reter todos os emails enviados e recebidos por específicos de pessoas ou reter todos os emails enviados e recebidos na sua organização por um período de tempo específico. Para obter mais informações sobre o que acontece quando uma caixa de correio está em retenção de litígio e como habilitar e desabilitá-lo, consulte a seção "Recursos de caixa de correio" no [Gerenciar caixas de correio do usuário](manage-user-mailboxes-exchange-2013-help.md).

Usar a retenção de litígio reter relatório para controlar os seguintes tipos de alterações feitas em uma caixa de correio em um determinado período de tempo:

  - A suspensão de litígio foi habilitada.

  - A suspensão de litígio foi desabilitada.

Para cada um desses tipos de alteração, o relatório inclui o usuário que fez a alteração e a hora e data que a alteração ser feita.

## O que você precisa saber antes de começar?

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Registro em log de auditoria do administrador somente leitura" no tópico [Permissões de infraestrutura do Exchange e do Shell](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## Usar o EAC para executar um litígio reter relatório

1.  No EAC, navegue até **Gerenciamento de conformidade** \> **auditoria**.

2.  Clique em **executar um relatório de suspensão de litígio por caixa de correio**.
    
    Microsoft Exchange executa o relatório para alterações de retenção de litígio feitas qualquer caixa de correio em duas últimas semanas.

3.  Para exibir as alterações para uma caixa de correio específica, no painel de resultados da pesquisa, marque a caixa de correio. Exiba os resultados da pesquisa no painel de detalhes.


> [!TIP]
> Deseja restringir os resultados da pesquisa? Selecione a data de início, data de término ou ambos e marque as caixas de correio específicas para pesquisar. Clique em <STRONG>pesquisa</STRONG> para executar novamente o relatório.



## Como saber se funcionou?

Para verificar que você tenha executado com êxito um litígio relatório, caixas de correio que tiveram litígio mantenha alterações dentro do intervalo de datas são exibidas no painel de resultados da pesquisa. Se não houver nenhum resultado, sem alterações litígio ocorreram dentro do intervalo de datas, ou alterações recentes ainda não tenham entrado em vigor ainda.


> [!TIP]
> Quando uma caixa de correio é colocada em suspensão de litígio, pode demorar até 60 minutos para a retenção entrem em vigor.


