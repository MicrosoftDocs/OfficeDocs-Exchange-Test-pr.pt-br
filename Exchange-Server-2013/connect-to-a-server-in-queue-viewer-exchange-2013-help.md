---
title: 'Conectar a um servidor no Visualizador de filas: Exchange 2013 Help'
TOCTitle: Conectar a um servidor no Visualizador de filas
ms:assetid: 6c1ad574-9ab5-4dcc-9398-ec10eca4fd11
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Aa998669(v=EXCHG.150)
ms:contentKeyID: 50485888
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Conectar a um servidor no Visualizador de filas

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2012-10-03_

Quando você usa o Visualizador de Fila na Caixa de Ferramentas do Exchange em um servidor do Microsoft Exchange Server 2013 localizado dentro da organização do Exchange, você pode se conectar a outros servidores de Caixa de Correio. Por padrão, quando você abrir o Visualizador de Filas em um servidor de Caixa de Correio, o Visualizador de Filas se conecta ao banco de dados de filas no servidor local. Entretanto, você pode iniciar mais de uma instância do Visualizador de Filas, de forma que cada instância focalize um servidor diferente. É possível colocar lado a lado as janelas do Visualizador de Filas, de forma que você possa monitorar facilmente mais de um servidor de Caixa de Correio de cada vez.

Você também pode especificar o servidor que o PowerShell Remoto usa para executar as tarefas especificadas no Visualizador de Filas. Esse servidor não precisa corresponder ao servidor remoto que você está gerenciando no Visualizador de Filas.

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 5 minutos

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Filas" no tópico [Permissões de fluxo de email](mail-flow-permissions-exchange-2013-help.md).

  - Os procedimentos neste tópico não se aplicam a servidores de Transporte de Borda. Ao usar o Visualizador de Filas em um servidor de Transporte de Borda, você não pode alterar o foco da ferramenta.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## O que você deseja fazer?

## Usar a Caixa de Ferramentas do Exchange para especificar o servidor que você deseja gerenciar no Visualizador de Filas

1.  Clique em **Iniciar** \> **Todos os Programas** \> **Microsoft Exchange 2013** \> **Caixa de Ferramentas do Exchange**.

2.  Na seção **Ferramentas de fluxo de emails**, clique duas vezes em **Visualizador de Filas**.

3.  No painel de ações, clique em **Conectar ao Servidor**

4.  Na janela **Conectar ao Servidor**, clique em **Procurar** para exibir uma lista dos servidores de Caixa de Correio disponíveis.

5.  Na janela **Selecionar Exchange Server**, selecione um servidor de Caixa de Correio. Para procurar um servidor de Caixa de Correio, use um dos seguintes procedimentos:
    
      - Insira o nome exato do servidor ou as primeiras letras do nome no campo **Pesquisar** e clique em **Localizar Agora**. Selecione um servidor no painel de resultados.
    
      - Selecione o menu **Exibir** e, em seguida, clique em **Mostrar Filtro**. Na coluna **Nome** ou **Versão**, clique no ícone de filtro e, em seguida, selecione o operador de filtro. Digite os critérios de filtro no campo **Inserir texto aqui**. Pressione ENTER. Selecione um servidor no painel de resultados.

6.  Clique em **OK** para fechar a janela **Selecionar Exchange Server**.

7.  Depois de selecionar um servidor, na janela **Conectar ao Servidor**, marque a caixa de seleção **Definir Como Servidor Padrão** se você quiser que o Visualizador de Filas focalize primeiro esse servidor sempre que o Visualizador de Filas estiver aberto.

8.  Na janela **Conectar ao Servidor**, clique em **Conectar**.

## Usar a Caixa de Correio do Exchange para especificar o servidor que o Visualizador de Filas para executar o PowerShell Remoto

1.  Clique em **Iniciar** \> **Todos os Programas** \> **Microsoft Exchange 2013** \> **Caixa de Ferramentas do Exchange**.

2.  Na seção **Ferramentas de fluxo de emails**, dê um duplo-clique em **Visualizador de Filas**.

3.  No painel de ações, clique em **Propriedades.**

4.  Na caixa de diálogo **Visualizador de Filas - Propriedades de \<nome do servidor\>**, selecione uma das seguintes opções:
    
      - **Conectar ao servidor selecionado automaticamente**   Selecione esta opção para se conectar automaticamente ao servidor em que você está gerenciando filas para executar o PowerShell Remoto.
    
      - **Especificar um servidor ao qual se conectar**   Selecione esta opção para especificar um servidor para executar o PowerShell Remoto. Caso essa opção seja selecionada, clique em **Procurar** para abrir a caixa de diálogo **Selecionar Exchange Server**. Selecione o servidor em que você deseja executar o PowerShell Remoto e clique em **OK**.

## Como saber se funcionou?

Você deve poder gerenciar as filas no servidor de Caixa de Correio que você especificou.

