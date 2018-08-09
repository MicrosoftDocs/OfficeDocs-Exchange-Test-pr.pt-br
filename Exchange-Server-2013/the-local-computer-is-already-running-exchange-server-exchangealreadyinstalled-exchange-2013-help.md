---
title: 'O computador local está executando o Exchange Server_ExchangeAlreadyInstalled'
TOCTitle: O computador local já está executando o Exchange Server_ExchangeAlreadyInstalled
ms:assetid: 3f168b5d-9910-418f-86fb-e99d852dcb5e
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/ms.exch.setupreadiness.exchangealreadyinstalled(v=EXCHG.150)
ms:contentKeyID: 50485432
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# O computador local já está executando o Exchange Server\_ExchangeAlreadyInstalled

 

_**Aplica-se a:** Exchange Server_

_**Tópico modificado em:** 2012-06-05_

O conteúdo neste tópico não foi atualizado para o Microsoft Exchange Server 2013. Mesmo assim, ele ainda pode se aplicar ao Exchange 2013. Se você ainda precisar de ajuda, verifique os recursos da comunidade, abaixo.

Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), ou [Proteção do Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=285351).

Instalação do Microsoft® Exchange Server 2007 não pode continuar porque o computador local tem componentes anteriores do Microsoft Exchange instalados.

A instalação do Exchange 2007 requer que o computador local não tem componentes existentes do Microsoft Exchange instalados.

Para resolver esse problema, remova todos os componentes do Microsoft Exchange 2000 Server ou Microsoft Exchange Server 2003 e, em seguida, execute novamente a instalação do Microsoft Exchange.

Para remover os componentes do Microsoft Exchange

1.  Clique em **Iniciar**, aponte para **configurações** e, em seguida, clique em **Painel de controle**.

2.  Clique duas vezes em **Adicionar ou Remover Programas**.

3.  Na lista de **programas atualmente instalados**, clique em **Microsoft Exchange** e, em seguida, clique em **Alterar/remover**.

4.  No Assistente de instalação do Microsoft Exchange, clique em **Avançar**.

5.  Na lista de ação, na página seleção de componentes, clique na seta ao lado de cada componente que tenha sido instalado e clique em **Remover**.
    

    > [!TIP]
    > Componentes instalados possuem uma marca de seleção na lista ação. Quando você clicar em <STRONG>Remover</STRONG>, a marca de seleção é substituída pela palavra <STRONG>Remover</STRONG>.



6.  Clique em **Avançar** duas vezes.

7.  Clique em **Concluir**.

