---
title: 'Personalizar os modelos de detalhes: Exchange 2013 Help'
TOCTitle: Personalizar os modelos de detalhes
ms:assetid: b4beeedd-e46f-442e-844a-e8575f95dca0
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/ms.exch.toolbox.detailstemplate(v=EXCHG.150)
ms:contentKeyID: 50486446
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Personalizar os modelos de detalhes

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2012-09-25_

Use o Editor de modelos de detalhes para personalizar a apresentação de GUI (interface) gráfica do usuário do cliente de propriedades de objeto que são acessados usando listas de endereços em MicrosoftOutlook. Por exemplo, quando um usuário abre uma lista de endereços no Outlook, as propriedades de um determinado objeto são apresentadas conforme definido pelo modelo de detalhes da organização Exchange. Os objetos que podem ser personalizados, alterando os tamanhos de campo, adicionar ou remover campos, adicionando ou removendo guias e reorganizando campos. O layout desses modelos pode variar por idioma.

## O que você precisa saber antes de começar?

  - Não há nenhuma opção de desfazer no editor de modelo de detalhes. Se você cometer um erro, você precisará reverter para a versão anterior. Para obter mais informações, consulte [Restaurar um modelo de detalhes para a configuração padrão](restore-a-details-template-to-the-default-configuration-exchange-2013-help.md).

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Modelos de detalhes" no tópico [Endereço de email e permissões do catálogo de endereços](email-address-and-address-book-permissions-exchange-2013-help.md) .

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

## Personalizar o modelo de detalhes

1.  Na **Caixa de ferramentas do Exchange**, clique em **Editor de modelos de detalhes** e clique em **Ferramenta aberta** no painel de ação.

2.  Na árvore de console do Editor de modelos de detalhes, clique em **Modelos de detalhes**.
    
    No painel de detalhes, as seguintes colunas são exibidas:
    
      - **Idioma**    Esta coluna lista o idioma no qual o modelo foi criado.
    
      - **Tipo de modelo**    Esta coluna lista o tipo de modelo que você pode personalizar.
    
      - **Identidade**    Esta coluna lista a identidade exclusiva do modelo.
    
      - **Criado**    Esta coluna lista a data e hora em que o modelo foi criado.
    
      - **Modificado**    Esta coluna lista a data e hora em que o modelo da última modificação.

3.  Para editar um modelo, clique no modelo desejado e, no painel de ações, clique em **Editar**. Por exemplo, o modelo de detalhes de contatos do **inglês (Estados Unidos)** é mostrado na figura a seguir.
    
    **Modelo de detalhes padrão como exibido no Outlook 2013**
    
    ![Modelo de detalhes padrão no Outlook 2007](images/JJ673049.a0af8aca-663d-4702-ab2f-9a342f481cdf(EXCHG.150).gif "Modelo de detalhes padrão no Outlook 2007")  

4.  Após você clicar em **Editar**, há várias tarefas que podem ser executadas para personalizar um modelo de detalhes:
    
      - Para mover um objeto no painel de designer, selecione o objeto e arraste-o para sua nova localização no modelo. Conforme você move o objeto, são fornecidos com linhas de alinhamento.
    
      - Para alterar texto de um rótulo, selecione o rótulo no painel design. No painel Propriedades, digite o novo texto na caixa de **texto**. Para criar os atalhos de teclado, você pode usar o símbolo de e comercial (&). Colocar o e comercial (&) antes da letra que você deseja usar como o atalho.
    
      - Para alterar o tamanho de um objeto, selecione o objeto e, em seguida, arraste as alças de dimensionamento até que o objeto tenha a forma e o tamanho desejado.
    
      - Para excluir um objeto, selecione o objeto e, em seguida, pressione a tecla DELETE.
        

        > [!TIP]
        > O Editor de modelos de detalhes não contém um botão de <STRONG>Desfazer</STRONG>, nem é possível usar um atalho de teclado para uma ação de desfazer. Para desfazer uma adição feitas no modelo, você deve usar a tecla DELETE. Para desfazer uma exclusão, você deve reaplicar a configuração. Você também pode reverter às configurações originais saindo do Editor de modelos de detalhes sem salvar suas alterações. Se você quiser desfazer alterações depois de ter salvado, você pode restaurar o modelo. Quando você restaura um modelo, toda a personalização é perdida e o modelo é restaurado para sua configuração original. Para obter mais informações sobre como restaurar o modelo de detalhes, consulte <A href="restore-a-details-template-to-the-default-configuration-exchange-2013-help.md">Restaurar um modelo de detalhes para a configuração padrão</A>.

    
      - Para adicionar um texto "Editar" caixas, caixas de listagem, caixas de lista suspensa de valores múltiplos ou caixas de listagem de valores múltiplos, no painel de ferramentas, arraste o objeto para o painel de design. Defina o atributo do objeto clicando na caixa de lista suspensa do atributo no painel Propriedades e, em seguida, selecionando o atributo que será usado pelo Exchange.
        

        > [!TIP]
        > Você deve vincular o objeto para um atributo para ele a ser usado pelo Exchange. Além disso, o atributo determina o conteúdo que é exibido para o usuário final no Outlook. Se você não marcar um atributo, um atributo aleatório é selecionado automaticamente.

    
      - Para adicionar uma caixa de grupo, arraste o objeto para o painel de design. Em seguida, no painel de propriedades, digite um nome na caixa de **texto**. Use caixas de grupo para agrupar objetos semelhantes.
    
      - Para adicionar uma guia no modelo, clique com o botão uma guia existente e clique em **Adicionar guia**. Uma guia em branco é exibida. Para nomear a guia, digite o nome na caixa de **texto** no painel Propriedades.
    
      - Para remover uma guia do modelo, clique com botão direito na guia e clique em **Remover guia**. Será exibido um aviso. Clique em **OK** para confirmar que você deseja remover a guia.
    
      - Para alterar a ordem das tabulações dos objetos em uma guia para que os usuários podem usar a tecla TAB para navegar os objetos na ordem desejada, selecione o objeto no painel design. Em seguida, no painel Propriedades, use a caixa de **TabIndex** para alterar a ordem.
        

        > [!TIP]
        > Para certificar-se de que os usuários não podem usar a tecla TAB para acessar os rótulos de um objeto (por exemplo, <STRONG>nome</STRONG> ou <STRONG>Alias</STRONG> ), altere a ordem dos rótulos para que sejam últimos na ordem de tabulação.



5.  Para salvar alterações no modelo de detalhes, no menu **arquivo**, clique em **Salvar**.

6.  Para fechar o modelo, no menu **arquivo**, clique em **Sair**.

