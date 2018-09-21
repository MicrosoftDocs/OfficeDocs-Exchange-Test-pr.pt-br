---
title: 'Gerenciar bancos de dados de caixa de correio no Exchange 2013'
TOCTitle: Gerenciar bancos de dados de caixa de correio no Exchange 2013
ms:assetid: ead4a96b-1717-435b-bcfc-9901ac4e3b58
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ150580(v=EXCHG.150)
ms:contentKeyID: 50486930
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Gerenciar bancos de dados de caixa de correio no Exchange 2013

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2013-04-29_

Um banco de dados de caixa de correio é uma unidade de granularidade em que as caixas de correio são criadas e armazenadas. Um banco de dados de caixa de correio é armazenado como um Exchange arquivo de banco de dados (.edb). No Microsoft Exchange Server 2013, cada banco de dados de caixa de correio possui propriedades exclusivas que podem ser configuradas.

Este tópico mostra como realizar as tarefas de configuração relacionadas ao gerenciamento de seus bancos de dados de caixa de correio no Microsoft Exchange Server 2013.

## O que você precisa saber antes de começar?

  - Tempo estimado para finalizar cada procedimento: 10 minutos

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Banco de dados de caixa de correio" no tópico [Permissões de destinatários](recipients-permissions-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## O que você deseja fazer?

## Criar um banco de dados de caixa de correio

## Usar o EAC para criar um banco de dados de caixa de correio

1.  No Centro de Administração do Exchange, navegue até **Servidores**.

2.  Selecione **Banco de Dados** e clique no símbolo de **+** para criar um banco de dados.

3.  Use o novo Assistente de banco de dados para criar seu banco de dados.

## Usar o Shell para criar um banco de dados de caixa de correio

Para um exemplo de como criar um banco de dados de caixa de correio, consulte o Exemplo 1 no [New-MailboxDatabase](https://technet.microsoft.com/pt-br/library/aa997976\(v=exchg.150\)).

## Como saber se funcionou?

Para verificar se você criou com êxito um banco de dados , faça o seguinte:

  - No EAC, verifique se o banco de dados de caixa de correio criado aparece na página **Bancos de Dados**.

  - No Shell, verifique se o banco de dados foi criado no servidor Mailbox01 executando o seguinte comando.
    
    ```powershell
Get-MailboxDatabase -Server "Mailbox01"
```

## Obter propriedades de banco de dados de caixa de correio

Para obter informações detalhadas de sintaxes e de parâmetros, confira [Get-MailboxDatabase](https://technet.microsoft.com/pt-br/library/bb124924\(v=exchg.150\)).

## Usar o Shell para obter propriedades de bancos de dados de caixa de correio

Para um exemplo de como obter propriedades de banco de dados de caixa de correio, consulte o Exemplo 2 em [New-MailboxDatabase](https://technet.microsoft.com/pt-br/library/aa997976\(v=exchg.150\)).

## Como saber se funcionou?

Para verificar se você recuperou com êxito suas informações de banco de dados de caixa de correio, faça o seguinte:

No Shell, verifique se todas as suas informações de banco de dados de caixa de correio são representadas corretamente.

## Definir propriedades de banco de dados de caixa de correio

## Usar o EAC para definir propriedades de bancos de dados de caixa de correio

1.  No EAC, navegue até **Servidores**.

2.  Selecione **Bancos de Dados** e clique para selecionar o banco de dados de caixa de correio que deseja configurar.

3.  Clique em **Editar** ![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição") para configurar os atributos de um banco de dados de caixas de correio.

4.  Utilize a guia **Geral** para visualizar o status do banco de dados de caixa de correio, incluindo o caminho do banco de dados de caixa de correio, o último backup e o status do banco de dados de caixa de correio:
    
      - <strong>Caminho do banco de dados</strong> Este campo somente de leitura exibe o caminho completo do arquivo (.edb) do banco de dados do Exchange 2013 para o banco de dados de caixa de correio selecionado. Para exibir o caminho inteiro, talvez você precise clicar no caminho e usar a tecla Seta para Direita. Você não pode usar esse campo para alterar o caminho. Para alterar o local dos arquivos de banco de dados, use o cmdlet [Move-DatabasePath](https://technet.microsoft.com/pt-br/library/bb124742\(v=exchg.150\)).
    
      - <strong>Último backup completo</strong> Este campo somente leitura exibe a data e a hora do último backup completo do banco de dados de caixa de correio.
    
      - <strong>Último backup incremental</strong> Este campo somente leitura exibe a data e a hora do último backup incremental do banco de dados de caixa de correio.
    
      - <strong>Status</strong> Este campo somente leitura mostra se o banco de dados de caixa de correio está montado ou desmontado.
    
      - <strong>Montado no servidor</strong> Este campo somente leitura exibe em qual servidor o banco de dados está montado.
    
      - <strong>Mestre</strong> Esse campo somente leitura exibe o servidor mestre para o banco de dados de caixa de correio. O servidor de Caixa de Correio que hospeda a cópia ativa de um banco de dados é conhecido como o banco de dados de caixa de correio mestre.
    
      - <strong>Tipo de mestre</strong> Esse campo somente leitura exibe o tipo de mestre do banco de dados de caixa de correio.
    
      - <strong>Modificado</strong> Esse campo somente leitura exibe a data e a hora da última modificação do banco de dados.
    
      - <strong>Servidores que hospedam uma cópia deste banco de dados</strong> Este campo somente leitura exibe os outros servidores que têm uma cópia deste banco de dados.

5.  Utilize a guia **Manutenção** para configurar o banco de dados de caixa de correio, incluindo a especificação de um destinatário de diário, a definição do agendamento de manutenção e a montagem do banco de dados na inicialização:
    
      - <strong>Destinatário do Diário</strong> Clique em **Procurar** para especificar um destinatário para habilitar o registro no diário nesse banco de dados de caixa de correio. Remova o destinatário listado para desabilitar o registro no diário.
    
      - <strong>Agendamento de manutenção</strong> Use essa lista para selecionar um dos agendamentos de manutenção pré-definidos. Você também pode configurar um agendamento personalizado. Para configurar uma agenda personalizada, clique em **Personalizar**.
    
      - <strong>Habilitar manutenção de banco de dados de plano de fundo (verificação ESE 24 x 7 ESE)</strong>  Selecione essa caixa de seleção para habilitar a verificação de banco de dados online, que é executada continuamente no plano de fundo. A verificação de banco de dados online realiza um cálculo de soma de verificação do banco de dados e realiza operações que permitem que o Exchange verifique por espaço perdido no banco de dados e o recupere. Se você selecionar essa caixa de seleção, o Exchange verifica o banco de dados mais de uma vez por dia e emitirá um evento de aviso caso não consiga finalizar a verificação do banco de dados num período de sete dias.
    
      - <strong>Não montar este banco de dados na inicialização</strong> Marque essa caixa de seleção para impedir que o Exchange monte esse banco de dados de caixa de correio quando ele for iniciado.
    
      - <strong>Este banco de dados pode ser substituído por uma restauração</strong>  Marque essa caixa de seleção para permitir que o banco de dados de caixa de correio seja substituído durante um processo de restauração.
    
      - <strong>Habilitar log circular</strong> Marque essa caixa de seleção para habilitar o log circular.

6.  Use a guia **Limites** para especificar os limites de armazenamento, o intervalo de mensagens de aviso e as configurações de exclusão de um banco de dados de caixa de correio:
    
      - <strong>Exibir aviso em (GB)</strong> Marque essa caixa de seleção para alertar automaticamente os usuários da caixa de correio que suas caixas de correio estão chegando no limite de repositório. Para especificar o limite de armazenamento, marque esta caixa de seleção e especifique a quantidade de conteúdo, em gigabytes (GB), que pode ser armazenada na caixa de correio antes de uma mensagem de email de alerta ser enviada aos usuários. Você pode inserir um valor de 0 a 2.097.151 megabytes (2,0 terabytes).
    
      - <strong>Proibir envio em (GB)</strong> Marque essa caixa de seleção para impedir que os usuários enviem novas mensagens de email após o tamanho da caixa de correio atingir o limite especificado. Para especificar esse limite, marque a caixa de seleção e digite o tamanho da caixa de correio em GB, para que seja proibido o envio de novas mensagens se o limite for atingido e para que o usuário seja notificado. Você pode inserir um valor de 0 a 2.097.151 KB (2,0 terabytes).
    
      - <strong>Proibir envio e recebimento em (GB)</strong> Marque essa caixa de seleção para impedir que os usuários enviem e recebam mensagens de email após o tamanho da caixa de correio atingir o limite especificado. Para especificar esse limite, marque a caixa de seleção e digite o tamanho da caixa de correio em GB, para que seja proibido o envio e o recebimento de novas mensagens se o limite for atingido e para que o usuário seja notificado. Você pode inserir um valor de 0 a 2.097.151 KB (2,0 terabytes).
    
      - <strong>Manter itens excluídos por (dias)</strong> Marque essa caixa de seleção para definir a quantidade de dias que os itens excluídos devem ser mantidos em uma caixa de correio. Você pode digitar um valor entre 0 e 24.855 dias.
    
      - <strong>Manter as caixas de correio excluídas por (dias)</strong> Marque essa caixa de seleção para definir a quantidade de dias que as caixas de correio excluídas devem ser mantidas. Você pode digitar um valor entre 0 e 24.855 dias.
    
      - <strong>Não excluir itens permanentemente até que seja feito backup do banco de dados</strong> Marque essa caixa de seleção para impedir a exclusão permanente de caixas de correio e emails até que seja feito backup do banco de dados de caixa de correio.

7.  Use a guia **Configurações do Cliente** para selecionar o catálogo de endereços offline (OAB) da caixa de correio:
    
      - <strong>Catálogo de endereços offline</strong> Para selecionar um catálogo de endereços offline, clique em **Procurar** e selecione o catálogo de endereços offline.

## Usar o Shell para definir propriedades de bancos de dados de caixa de correio

Para um exemplo de como configurar propriedades de banco de dados de caixa de correio, consulte o Exemplo 1 em [Set-MailboxDatabase](https://technet.microsoft.com/pt-br/library/bb123971\(v=exchg.150\)).

## Como saber se funcionou?

Para verificar se você definiu com êxito os atributos, faça o seguinte:

  - Verifique se suas alterações foram salvas no EAC.

  - No Shell, execute o comando a seguir para recuperar as propriedades de banco de dados de caixa de correio.
    
    ```powershell
Get-MailboxDatabase -Identity MailboxDatabase01 -Status | Format-List
```

## Mover um caminho de banco de dados de caixa de correio

Para obter informações detalhadas de sintaxes e de parâmetros, confira [Move-DatabasePath](https://technet.microsoft.com/pt-br/library/bb124742\(v=exchg.150\)).

## Usar o Shell para mover um caminho do banco de dados de caixa de correio

Para um exemplo de como configurar propriedades de banco de dados de caixa de correio, consulte o Exemplo 1 em [Move-DatabasePath](https://technet.microsoft.com/pt-br/library/bb124742\(v=exchg.150\)).

## Como saber se funcionou?

Para verificar se você moveu com êxito o caminho de banco de dados, faça o seguinte:

1.  No EAC, selecione **Servidores** \> **Bancos de dados** e clique para selecionar a caixa de correio apropriada.

2.  Clique no símbolo de **caneta** e verifique se o caminho de banco de dados está correto.

## Montar um banco de dados de caixa de correio

Para obter informações detalhadas de sintaxes e de parâmetros, confira [Mount-Database](https://technet.microsoft.com/pt-br/library/aa998871\(v=exchg.150\)).

## Usar o Shell para montar um banco de dados de caixa de correio

Para um exemplo de como montar um banco de dados de caixa de correio, consulte o Exemplo 1 no [Mount-Database](https://technet.microsoft.com/pt-br/library/aa998871\(v=exchg.150\)).

## Como saber se funcionou?

Para verificar se você montou corretamente o banco de dados de caixas de correio, faça o seguinte.

  - No Shell, execute o seguinte comando para recuperar as propriedades de todos os bancos de dados de caixas de correio.
    
    ```powershell
Get-MailboxDatabase -IncludePreExchange2013
```

## Desmontar um banco de dados de caixa de correio

Para obter informações detalhadas de sintaxes e de parâmetros, confira [Dismount-Database](https://technet.microsoft.com/pt-br/library/bb124936\(v=exchg.150\)).

## Usar o Shell para desmontar um banco de dados de caixa de correio

Para um exemplo de como desmontar um banco de dados de caixa de correio, consulte o Exemplo 1 no [Dismount-Database](https://technet.microsoft.com/pt-br/library/bb124936\(v=exchg.150\)).

## Como saber se funcionou?

Para verificar se você desmontou com êxito o banco de dados, faça o seguinte:

1.  No EAC, selecione **Servidores** \> **Bancos de dados** e clique para selecionar a caixa de correio apropriada.

2.  Clique no símbolo de **caneta** e verifique se o status de banco de dados é **Desmontado**.

## Remover um banco de dados de caixa de correio

## Usar o EAC para remover um banco de dados de caixa de correio

1.  No EAC, selecione **Servidores** \> **Bancos de dados** e clique para selecionar a caixa de correio apropriada.

2.  Clique em **Excluir**![Excluir ícone](images/JJ673559.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Excluir ícone") para remover o banco de dados de caixa de correio.

## Usar o Shell para remover um banco de dados de caixa de correio

Para obter informações detalhadas de sintaxes e de parâmetros, confira [Remove-MailboxDatabase](https://technet.microsoft.com/pt-br/library/aa997931\(v=exchg.150\)).

1.  Execute o seguinte comando para remover o banco de dados de caixa de correio MyDatabase.
    
    ```powershell
Remove-MailboxDatabase -Identity "MyDatabase"
```

2.  Quando perguntado se tem certeza de que deseja executar a ação, digite **S**.

3.  Quando a caixa de diálogo for exibida, informando que o banco de dados foi removido com êxito, observe o local do arquivo de banco de dados do Exchange 2013 (.edb). Se você desejar remover esse arquivo da unidade de disco rígido, exclua-o manualmente.

## Como saber se funcionou?

Para verificar se você removeu com êxito o banco de dados de caixa de correio, proceda da seguinte forma:

  - No EAC, selecione **Servidores** \> **Bancos de dados**.

  - Verifique se o banco de dados de caixa de correio foi removido.

