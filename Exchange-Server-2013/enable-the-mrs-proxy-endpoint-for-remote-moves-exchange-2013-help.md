---
title: 'Habilitar o ponto de extremidade do Proxy MRS para movimentações remotas'
TOCTitle: Habilitar o ponto de extremidade do Proxy MRS para movimentações remotas
ms:assetid: 9840f712-127e-4c2d-bfe5-1b35cdb2a31b
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dn155787(v=EXCHG.150)
ms:contentKeyID: 54651977
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Habilitar o ponto de extremidade do Proxy MRS para movimentações remotas

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2013-07-02_

O Proxy do Serviço de Replicação de Caixa de Correio (Proxy MRS) facilita as movimentações de caixa de correio entre florestas e migrações de movimentação remota entre sua organização do Exchange local e o Exchange Online. No Exchange 2013, o Proxy MRS está incluído na função de servidor de Caixa de Correio (também chamada de *servidor de Caixa de Correio*). Durante migrações entre florestas e de movimentação remota, um servidor de Acesso para Cliente atua como proxy para as solicitações de movimentação de entrada do servidor de Caixa de Correio. A capacidade de um servidor de Acesso para Cliente de aceitar essas solicitações é desabilitada por padrão. Para permitir que o servidor de Acesso para Cliente aceite solicitações de movimentação de entrada, é necessário habilitar o ponto de extremidade do Proxy MRS.

O servidor de Acesso para Cliente no qual habilitar o ponto de extremidade do Proxy MRS depende do tipo e direção da movimentação de caixa de correio.

  - **Movimentações corporativas entre florestas**   Para movimentações entre florestas que são iniciadas do ambiente de destino (conhecidas como tipo de movimentação *pull*), é necessário habilitar o ponto de extremidade do Proxy MRS em servidores de Acesso para Cliente no ambiente de origem. Para movimentações entre florestas que são iniciadas do ambiente de origem (conhecidas como tipo de movimentação *push*), é necessário habilitar o ponto de extremidade do Proxy MRS em servidores de Acesso para Cliente no ambiente de destino.

  - **Migrações de movimentação remota entre uma organização do Exchange local e o Exchange Online**   Para migrações de movimentação remota de adição e transferência, é necessário habilitar o ponto de extremidade do Proxy MRS em servidores de Acesso para Cliente na sua organização local.


> [!NOTE]
> Se você usa o EAC para mover caixas de correio, as movimentações entre florestas e as migrações de movimentação remota de adição são tipos de movimentações pull, pois a solicitação é iniciada do ambiente de destino. As migrações de movimentação remota de transferência são um tipo de movimentação push, pois a solicitação é iniciada do ambiente de origem.



## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 2 minutos por servidor.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Seção "Permissões de Serviços Web do Exchange" no tópico [Permissões de dispositivos móveis e clientes](clients-and-mobile-devices-permissions-exchange-2013-help.md).

  - Se você implantou mais de um servidor de Acesso para Cliente em sua organização do Exchange, deve habilitar o ponto de extremidade do Proxy MRS em cada um deles. Se adicionar mais servidores de Acesso para Cliente, lembre-se de habilitar o ponto de extremidade do Proxy MRS nos novos servidores. Movimentações entre florestas e migrações de movimentação remota poderão falhar se o ponto de extremidade do Proxy MRS não estiver habilitado em todos os servidores de Acesso para Cliente.

  - Se você não executa movimentações entre florestas ou migrações de movimentação remota, mantenha os pontos de extremidade do Proxy MRS desabilitados, a fim de reduzir a superfície de ataque da sua organização.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Usar o EAC para habilitar o ponto de extremidade do Proxy MRS

1.  No EAC, navegue até **Destinatários** \> **Servidores** \> **Diretórios Virtuais**.

2.  Na lista suspensa **Selecionar servidor**, selecione o nome do servidor de Acesso para Cliente no qual você deseja habilitar o ponto de extremidade do Proxy MRS. Ou selecione **Todos os servidores** para exibir os diretórios virtuais de todos os servidores de Acesso para Cliente na sua organização.

3.  Na lista suspensa **Selecionar tipo**, selecione **EWS** para exibir o diretório virtual do Serviço Web do Exchange (EWS) do servidor selecionado.

4.  Na lista de diretórios virtuais, clique em **EWS (Site Padrão)** do servidor de Acesso para Cliente que você deseja configurar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

5.  Na página de propriedades de **EWS (Site Padrão)**, marque a caixa de seleção **Proxy MRS habilitado** e clique em **Salvar**.

## Usar o Shell para habilitar o ponto de extremidade do Proxy MRS

O comando a seguir habilita o ponto de extremidade do Proxy MRS em um servidor de Acesso para Cliente chamado EXCH-SRV-01.

    Set-WebServicesVirtualDirectory -Identity "EXCH-SRV-01\EWS (Default Web Site)" -MRSProxyEnabled $true

O comando a seguir habilita o ponto de extremidade do Proxy MRS em todos os servidores de Acesso para Cliente da sua organização do Exchange.

    Get-WebServicesVirtualDirectory | Set-WebServicesVirtualDirectory -MRSProxyEnabled $true


> [!IMPORTANT]
> Conforme afirmado anteriormente, o ponto de extremidade do Proxy MRS deve estar habilitado em cada servidor de Acesso para Cliente de sua organização. Execute o comando anterior após adicionar um novo servidor de Acesso para Cliente à sua organização.



## Como saber se funcionou?

Para verificar se você habilitou o ponto de extremidade do Proxy MRS com êxito, siga um destes procedimentos:

1.  No EAC, navegue até **Destinatários** \> **Servidores** \> **Diretórios Virtuais**.

2.  Na lista de diretórios virtuais, clique em **EWS (Site Padrão)** e verifique no painel de detalhes se o ponto de extremidade do Proxy MRS está habilitado.
    
    Alternativamente, você pode clicar em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição") para exibir a página de propriedades de **EWS (Site Padrão)** e verificar se a caixa de seleção **Habilitar o ponto de extremidade Proxy MRS** está marcada.

Ou

Execute o seguinte comando no Shell:

    Get-WebServicesVirtualDirectory | FL Identity,MRSProxyEnabled

Verifique se o parâmetro *MRSProxyEnabled* está definido como `True`.

Outra maneira de verificar se o ponto de extremidade do Proxy MRS está habilitado é usar o cmdlet **Test-MigrationServerAvailability** para testar a capacidade de comunicação com o servidor remoto que hospeda as caixas de correio que você deseja mover ou, no caso de transferência de caixas de correio do Exchange Online para a sua organização local, um servidor na sua organização local. Para obter mais informações, consulte [Test-MigrationServerAvailability](https://technet.microsoft.com/pt-br/library/jj219169\(v=exchg.150\)).

O exemplo a seguir testa a conexão com um servidor na floresta corp.contoso.com.

```
    $Credentials = Get-Credential
```

```
    Test-MigrationServerAvailability -ExchangeRemoteMove -Autodiscover -EmailAddress administrator@corp.contoso.com -Credentials $Credentials
```

Para executar este comando com êxito, o ponto de extremidade do Proxy MRS deve estar habilitado.

