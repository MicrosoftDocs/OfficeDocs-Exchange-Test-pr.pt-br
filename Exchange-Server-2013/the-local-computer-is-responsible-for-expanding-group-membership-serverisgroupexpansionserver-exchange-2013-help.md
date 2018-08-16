---
title: 'O computador local é responsável pela expansão de associação ao grupo'
TOCTitle: O computador local é responsável pela expansão de grupo membership_ServerIsGroupExpansionServer
ms:assetid: 52872561-60e6-4f3d-bbc6-6de0edf74b09
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/ms.exch.setupreadiness.serverisgroupexpansionserver(v=EXCHG.150)
ms:contentKeyID: 50485590
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# O computador local é responsável pela expansão de grupo membership\_ServerIsGroupExpansionServer

 

_**Aplica-se a:** Exchange Server_

_**Tópico modificado em:** 2012-06-05_

O conteúdo neste tópico não foi atualizado para o Microsoft Exchange Server 2013. Mesmo assim, ele ainda pode se aplicar ao Exchange 2013. Se você ainda precisar de ajuda, verifique os recursos da comunidade, abaixo.

Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), ou [Proteção do Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=285351).

Instalação do Microsoft® Exchange Server 2007 não pode continuar porque falhou ao tentar desinstalar uma função de transporte de Hub responsável por expandir a associação de grupo.

A instalação do Exchange 2007 requer que a expansão de lista de distribuição ser removido do servidor Bridgehead atual para a função Transporte de Hub pode ser desinstalada.

A expansão de listas de distribuição permite identificar de destinatários individuais que pertencem à lista de distribuição sejam identificados, ou a identificação da distribuição adicional listas para expansão. Uma lista de distribuição expandido pode retornar o caminho para qualquer notificação de status de entrega necessária (DSN). DSNs notificam o administrador do Microsoft Exchange ou o remetente do email do status de uma mensagem de email específica. Além disso, a expansão de lista de distribuição identifica se gerado automaticamente respostas ou mensagens de ausência temporária devem ser enviadas para o remetente da mensagem original.

Para resolver esse problema, mova a expansão de grupo de distribuição para outro servidor e execute novamente o programa de instalação do Microsoft Exchange.

Para alterar o servidor de expansão de um grupo de distribuição ou o grupo dinâmico de distribuição

1.  Abra o Console de gerenciamento do Exchange.

2.  Na árvore de console, expanda **Configuração do destinatário**.

3.  Na árvore de console, clique em **Grupo de distribuição**.

4.  Crie um filtro para exibir todos os grupos de distribuição e grupos dinâmicos de distribuição que usam o servidor Bridgehead atual como um servidor de expansão.
    
    1.  No painel de ações, clique em **Criar filtro**.
    
    2.  Na lista suspensa de propriedade, clique em **Servidor de expansão**.
    
    3.  Na lista suspensa operador, clique em **igual a**.
    
    4.  Na caixa valor, clique no botão **Procurar** para selecionar o servidor Bridgehead que atualmente atuando como o servidor de expansão.


> [!TIP]
> A próxima etapa é opcional.



1.  Clique em **Adicionar expressão** para especificar os critérios de filtro adicional. Somente as mensagens que atendam a todos os critérios de filtro serão exibidas.

2.  Clique em **Aplicar filtro**. Os resultados que atendam aos critérios de filtro são exibidos.

<!-- end list -->

1.  No painel de resultados, clique no grupo de distribuição que você deseja alterar o servidor de expansão para e clique em **Propriedades** no painel de ações.

2.  Em **Propriedades**, clique na guia **Avançado**.

3.  Na lista suspensa servidor expansão, selecione um servidor específico na lista ou selecione **qualquer servidor na organização**.

4.  Repita as etapas 5 a 7 para todos os grupos de distribuição ou grupos dinâmicos de distribuição que estão usando o servidor Bridgehead como seu servidor de expansão.

