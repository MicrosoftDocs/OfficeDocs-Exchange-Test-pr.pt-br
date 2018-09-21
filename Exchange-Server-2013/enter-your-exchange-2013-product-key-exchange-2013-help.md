---
title: 'Insira a chave do produto do Exchange 2013: Exchange 2013 Help'
TOCTitle: Insira a chave do produto do Exchange 2013
ms:assetid: ccb14685-4bdc-42a4-a985-35cd2a1a415c
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb124582(v=EXCHG.150)
ms:contentKeyID: 51407918
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.Servers.EnterProductKeyWizardForm.EnterProductKeyWizardPage
ms.translationtype: MT
---

# Insira a chave do produto do Exchange 2013

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2016-12-09_

Uma chave de produto informa Exchange Server 2013 se você comprou uma licença Standard ou Enterprise Edition. Se você comprou a chave do produto for para uma licença Enterprise Edition, ele permite montar bancos de dados mais de cinco por servidor, além de tudo que é fornecido com uma licença Standard Edition. Se você quiser ler mais sobre o licenciamento do Exchange, consulte [Exchange 2013: edições e versões](exchange-2013-editions-and-versions-exchange-2013-help.md).

Se você não inserir uma chave de produto, o seu servidor é licenciado automaticamente, como uma edição de avaliação. As funções de edição de avaliação apenas um servidor Standard Edition de Exchange, como e é útil se você desejar para experimentar Exchange antes de comprar ou executar testes em um laboratório. A única diferença é que você só pode usar um servidor Exchange licenciado como uma edição de avaliação de 180 dias. Se desejar continuar usando o servidor além de 180 dias, você precisará inserir uma chave de produto ou centro de administração do Exchange (EAC) será iniciado mostrar os lembretes que você precisa inserir uma chave de produto para licenciar o servidor.


> [!TIP]
> Observamos que alguns visitantes desta página estão procurando por informações sobre como instalar e ativar o Office. Se você é um deles, confira estas páginas: 
> <UL>
> <LI>
> <P><A href="http://go.microsoft.com/fwlink/p/?linkid=403360">Instalar o Office</A></P>
> <LI>
> <P><A href="http://go.microsoft.com/fwlink/p/?linkid=403361">Precisa de ajuda com a chave de produto do Office?</A></P></LI></UL>Se deseja digitar uma chave de produto em um servidor do Exchange 2010, vá para <A href="http://go.microsoft.com/fwlink/p/?linkid=403370">Digitar uma chave de produto do Exchange 2010</A>.<BR>Se desejar digitar uma chave de produto no servidor Exchange 2013, você está no lugar certo! Continue lendo.



## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão do procedimento: menos de 5 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Chave de Produto (Product key)" no tópico [Permissões de infraestrutura do Exchange e do Shell](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md).

  - Se estiver licenciando um servidor do Exchange que execute a função de servidor de Caixa de Correio, é necessário reiniciar o serviço Repositório de Informações do Microsoft Exchange após inserir a chave do produto.

  - Se desejar atualizar um servidor do Exchange de uma licença Standard Edition para uma licença Enterprise Edition, siga os passos neste tópico.

  - Se desejar fazer um downgrade em um servidor do Exchange de uma licença Enterprise Edition para uma licença Standard Edition, é necessário reinstalar o Exchange.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## O que você deseja fazer?

## Usar o EAC para inserir a chave do produto (Product Key)

1.  Abra o EAC navegando em https://\<*Nome do servidor de Acesso para Cliente*\>/ecp.

2.  Insira seu nome de usuário e senha em **Domínio\\nome de usuário** e **Senha** e depois clique em **Entrar**.

3.  Vá até **Servidores** \> **Servidores**. Selecione o servidor que você deseja licenciar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

4.  (Opcional) Se você quiser atualizar o servidor de uma licença Standard Edition para uma licença Enterprise Edition, na página **Geral**, selecione **Alterar chave de produto**. Esta opção será exibida somente se o servidor já estiver licenciado.

5.  Na página **Geral**, insira a chave do produto (Product Key) nas caixas de texto **Insira uma chave do produto válida**.

6.  Clique em **Salvar**.

7.  Se você licenciou um servidor Exchange que execute a função de servidor de Caixa de Correio, faça o seguinte para reiniciar o serviço Repositório de Informações do Microsoft Exchange:
    
    1.  Abra o **Painel de Controle**, vá para **Ferramentas Administrativas**e, em seguida, abra **Serviços**.
    
    2.  Com o botão direito, clique em **Repositório de Informações do Microsoft Exchange** e clique em **Reiniciar**.

## Usar o Shell para inserir a chave do produto (Product Key)

Esse exemplo usa o cmdlet **set-ExchangeServer** para inserir a chave de produto.


> [!NOTE]
> Você pode executar este comando novamente no mesmo servidor para atualizá-lo de uma licença Standard Edition para uma licença Enterprise Edition.



```powershell
Set-ExchangeServer ExServer01 -ProductKey aaaaa-aaaaa-aaaaa-aaaaa-aaaaa
```

Para obter informações detalhadas sobre sintaxes e parâmetros, consulte [Set-ExchangeServer](https://technet.microsoft.com/pt-br/library/bb123716\(v=exchg.150\)).

Se você licenciou um servidor Exchange que execute a função de servidor de Caixa de Correio, faça o seguinte para reiniciar o serviço Repositório de Informações do Microsoft Exchange:

1.  Abra o **Painel de Controle**, vá para **Ferramentas Administrativas**e, em seguida, abra **Serviços**.

2.  Com o botão direito o **Repositório de informações do Microsoft Exchange** e clique em **Reiniciar**.

## Como saber se funcionou?

Para usar o EAC a fim de verificar se você licenciou com êxito o servidor como Standard Edition ou como Enterprise Edition, faça o seguinte:

1.  Insira seu nome de usuário e senha em **Domínio\\nome de usuário** e **Senha** e depois clique em **Entrar**.

2.  Vá até **Servidores** \> **Servidores**.

3.  Selecione o servidor que você deseja visualizar e examine o painel de detalhes desse servidor. Se a chave do produto (Product Key) tiver sido aceita, a indicação **Licenciado** aparecerá junto com a edição do Exchange 2013.

Para usar o Shell a fim de verificar se você licenciou com êxito o servidor como Standard Edition ou como Enterprise Edition, faça o seguinte:

1.  Abra o shell.

2.  Execute o comando a seguir para exibir o status de licenciamento de um servidor específico do Exchange.
    
        Get-ExchangeServer ExServer01 | Format-Table Edition,*Trial*

3.  (Opcional) Execute o comando a seguir para exibir o status de licenciamento de todos os servidores do Exchange da sua organização.
    
        Get-ExchangeServer | Format-Table Name, Edition, *Trial* -Auto

