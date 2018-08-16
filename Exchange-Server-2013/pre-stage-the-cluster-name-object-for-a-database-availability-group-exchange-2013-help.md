---
title: 'Preparar objeto de nome de cluster para grupo de dispon. de banco de dados'
TOCTitle: Preparar o objeto de nome de cluster de um grupo de disponibilidade do banco de dados
ms:assetid: 51ebf2f6-8a02-44ef-a489-ca361cb0f63a
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Ff367878(v=EXCHG.150)
ms:contentKeyID: 50485585
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Preparar o objeto de nome de cluster de um grupo de disponibilidade do banco de dados

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2014-08-14_

Em ambientes onde a criação da conta de computador é restrita ou onde as contas de computador são criadas em um contêiner que não seja o contêiner de computadores padrão, você pode preparar o cluster nomear o objeto (CNO) e, em seguida, fornecer o CNO atribuindo permissões a ele. Pré-preparo o CNO também é necessária para o Windows Server 2012 e Windows Server 2012 R2 DAG membros devido às alterações de permissões no Windows para objetos de computador. Ao implantar um grupo de disponibilidade de banco de dados (DAG) usando os servidores de caixa de correio que estão executando o Windows Server 2012 ou Windows Server 2012 R2, você deve preparar e fornecer o CNO, a menos que você estiver implantando um DAG sem um ponto de acesso administrativo do cluster. DAGs sem pontos de acesso administrativo do cluster não use CNOs; pré-preparo, portanto, não é necessário para essas DAGs.

Crie e desabilite uma conta de computador para o CNO e:

  - Atribua controle total da conta do computador à conta do computador do primeiro servidor de Caixa de Correio sendo adicionado ao DAG.

  - Atribua controle total da conta do computador ao grupo de segurança universal (USG) do Subsistema Confiável do Exchange.

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 1 minuto

  - Você deve usar uma conta que tenha permissões para criar objetos de computador no Active Directory.

  - Depois de concluir as etapas a seguir, dê um tempo para que a replicação do Active Directory ocorra. Após a replicação do objeto, você poderá adicionar o primeiro membro ao DAG.


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Preparar o CNO

1.  Abra Usuários e Computadores do Active Directory.

2.  Expanda o nó de floresta.

3.  Clique com o botão direito do mouse na unidade organizacional (OU) em que deseja criar a nova conta, selecione **Novo** e depois selecione **Computador**.

4.  Em **Novo Objeto - Computador**, digite o nome da conta do computador do CNO na caixa **Nome do computador**. Este é o nome que você usará para o DAG. Clique em **OK** para criar a conta.

5.  Clique com o botão direito do mouse na nova conta de computador e clique em **Desabilitar Conta**. Clique em **Sim** para confirmar a ação de desabilitação e, em seguida, clique em **OK**.

## Atribuir permissões ao CNO

1.  Abra Usuários e Computadores do Active Directory.

2.  Se os recursos avançados não estiverem habilitados, ative-os clicando em **Exibir** e depois em **Recursos Avançados**.

3.  Clique com o botão direito do mouse na nova conta de computador e clique em **Propriedades**.

4.  Em **\<Nome do Computador\> Propriedades**, na guia **Segurança**, clique em **Adicionar** para adicionar a conta de computador do primeiro nó a ser adicionado ao DAG ou adicionar o USG do Subsistema Confiável do Exchange:
    
      - Para adicionar o Subsistema Confiável do Exchange, digite **Exchange Trusted Subsystem** no campo **Digite os nomes de objeto a serem selecionados**. Clique em **OK** para adicionar o USG. Selecione o USG do Subsistema Confiável do Exchange e, no campo **Permissões do Subsistema Confiável do Exchange**, selecione **Controle Total** na coluna **Permitir**. Clique em **OK** para salvar as configurações de permissão.
    
      - Para adicionar a conta de computador ao primeiro nó a ser adicionado ao DAG, clique em **Tipos de Objeto**. Na caixa de diálogo **Tipos de Objetos**, desmarque as caixas de seleção **Entidades de segurança internas**, **Grupos** e **Usuários**. Marque a caixa de seleção **Computadores** e clique em **OK**. No campo **Digite os nomes de objeto a serem selecionados**, digite o nome do primeiro servidor de Caixa de Correio a ser adicionado ao DAG e clique em **OK**. Selecione a conta do computador do primeiro nó e, no campo **Permissões para \<Nome do Nó\>**, selecione **Controle Total** na coluna **Permitir**. Clique em **OK** para salvar as configurações de permissão.

## Como saber se funcionou?

Para verificar se você criou com êxito o CNO, faça o seguinte:

1.  Abra Usuários e Computadores do Active Directory.

2.  Expanda o nó de floresta.

3.  Abra a OU em que você criou a conta e verifique se a conta está listada.

