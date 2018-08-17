---
title: 'Definir opções do Visualizador de filas: Exchange 2013 Help'
TOCTitle: Definir opções do Visualizador de filas
ms:assetid: 03a9134c-0714-4c13-b286-92bccc7ec05e
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Aa995934(v=EXCHG.150)
ms:contentKeyID: 50484887
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Definir opções do Visualizador de filas

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2012-10-03_

Você pode definir opções no Visualizador de Filas para ajustar o número de itens que são exibidos na página e o intervalo de atualização automática. O intervalo de atualização automática determina a frequência da atualização dos resultados no Visualizador de Filas.

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 10 minutos

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Filas" no tópico [Permissões de fluxo de email](mail-flow-permissions-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!WARNING]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## Usar a Caixa de Ferramentas do Exchange para definir as opções do Visualizador de Filas

1.  Clique em **Iniciar** \> **Todos os Programas** \> **Microsoft Exchange 2013** \> **Caixa de Ferramentas do Exchange**.

2.  Na seção **Ferramentas de fluxo de emails**, clique duas vezes em **Visualizador de Filas**.

3.  No Visualizador de Filas, clique em **Exibir** \> **Opções**, para definir as seguintes configurações na caixa de diálogo **Opções do Visualizador de Filas**:
    
    1.  No campo **Intervalo de atualização (segundos)**, digite a frequência com que o Visualizador de Filas deve atualizar a exibição.
        

        > [!NOTE]
        > O intervalo de atualização automática padrão é de 30 segundos e não pode ser definido para um período mais curto. Se você desabilitar a funcionalidade de atualização automática desmarcando a caixa de seleção <STRONG>Atualização automática de tela</STRONG> na página <STRONG>Opções do Visualizador de Filas</STRONG>, será necessário atualizar manualmente os resultados que são exibidos no Visualizador de Filas clicando em <STRONG>Atualizar</STRONG>.

    
    2.  No campo **Número de itens a serem exibidos em cada página**, digite o número máximo de itens que serão exibidos no Visualizador de Filas. Esse número deve estar entre 1 e 10.000. Se você tiver mais itens do que o limite, serão agrupados em grupos de número máximo de itens. Por exemplo, a figura a seguir exibe uma fila de 14 mensagens com o Visualizador de Filas configurado para exibir 10 itens por página. O número de objetos na página é exibido na parte superior direita. Na parte inferior da página, é exibido o número total de itens na fila. Você pode usar os controles de navegação para exibir os outros itens da fila.

4.  Quando você tiver concluído, clique em **OK**.
    
    **Visualizador de Filas**
    
    ![Visualizador de Filas com mais itens do que o limite de itens](images/Aa995934.e82196e6-002a-4e9e-823d-b244b0bd25e2(EXCHG.150).gif "Visualizador de Filas com mais itens do que o limite de itens")  

## Como saber se funcionou?

Você saberá se o procedimento funcionou se o Visualizador de Filas usar o intervalo de atualização e o número de itens por configurações de página.

