---
title: 'Instalar ou remover aplicativos do Outlook para sua organização: Exchange 2013 Help'
TOCTitle: Instalar ou remover aplicativos do Outlook para sua organização
ms:assetid: 112f3ef7-9943-4a1e-8a42-e08e8e9f67f4
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ943752(v=EXCHG.150)
ms:contentKeyID: 52058790
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Instalar ou remover aplicativos do Outlook para sua organização

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2017-02-03_

Você pode instalar ou remover suplementos do Outlook para sua organização usando o EAC ou o Shell.


> [!TIP]
> Por padrão, depois de instalar um suplemento para sua organização, o suplemento está disponível para todos os usuários em sua organização. Após a instalação, você pode usar o EAC ou o Shell para tornar o suplemento opcional ou necessário para seus usuários e para especificar se você deseja que o suplemento a ser habilitada ou desabilitada. Para obter informações sobre como alterar as configurações padrão de um suplemento, consulte <A href="manage-user-access-to-add-ins-for-outlook-exchange-online-help.md">Gerenciar o acesso de usuário aos aplicativos para Outlook</A>. Para limitar a disponibilidade dos suplementos para determinados usuários em sua organização, você deve usar o Shell. Para obter mais informações, consulte <A href="manage-user-access-to-add-ins-for-outlook-exchange-online-help.md">Gerenciar o acesso de usuário aos aplicativos para Outlook</A>.



Para tarefas de gerenciamento adicionais, consulte [Aplicativos para Outlook](add-ins-for-outlook-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 5 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Aplicativos para Outlook" no tópico [Permissões de destinatários](recipients-permissions-exchange-2013-help.md) .

  - Você pode atribuir administradores a permissão para instalar e gerenciar suplementos para sua organização. Você também pode atribuir aos usuários permissão para instalar e gerenciar suplementos para seu próprio uso. Para obter mais informações, consulte [Especificar os administradores e usuários que podem instalar e gerenciar suplementos do Outlook](specify-the-administrators-and-users-who-can-install-and-manage-add-ins-for-outlook-exchange-2013-help.md).

  - Acesso ao Office Store não é compatível com caixas de correio ou organizações em regiões específicas. Se você não vir **Adicionar da Office Store**, como uma opção no **Centro de administração do Exchange** em **organização** \> **suplementos** \> ![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar"), você poderá instalar um suplemento para Outlook a partir de um local de arquivo ou URL. Para obter mais informações, contate o provedor de serviço.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Instalar um suplemento para Outlook

## Usar o EAC para adicionar um suplemento

1.  No EAC, navegue até **organização** \> **suplementos**.

2.  Clique em **New**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar")e, em seguida, escolha o local que você deseja instalar o suplemento de.
    
      - **Adicionar da Office Store**. No Office Store, selecione o aplicativo que você deseja instalar e, em seguida, clique em **Adicionar**. Aplicativos que funcionam com Outlook Web App estão listados em **suplementos do Office e SharePoint** \> **Outlook**.
        

        > [!TIP]
        > Acesso ao armazenamento do Office não é compatível com caixas de correio ou organizações em regiões específicas. Se você não vir <STRONG>Adicionar da Office Store</STRONG> como uma opção no <STRONG>Centro de administração do Exchange</STRONG> em <STRONG>organização</STRONG> &gt; <STRONG>suplementos</STRONG> &gt; <IMG title="Ícone Adicionar" alt="Ícone Adicionar" src="images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif">, você poderá instalar um suplemento para Outlook a partir de um local de arquivo ou URL. Para obter mais informações, contate o provedor de serviço.

    
      - **Adicionar da URL**. Em **URL**, digite a URL completa do suplemento do arquivo de manifesto que você deseja instalar.
    
      - **Adicionar do arquivo**. Selecione **Procurar** e navegue até o local do suplemento do arquivo de manifesto de que você deseja instalar.

3.  Clique em **Salvar**.

## Use o Shell para adicionar um suplemento

Este exemplo mostra como adicionar um suplemento a partir de uma URL.

    New-App -OrganizationApp -Url <URL location for add-in manifest file>

Este exemplo mostra como adicionar um add-in de um arquivo.

    New-App -OrganizationApp -FileData <File location for add-in manifest file>


> [!TIP]
> Quando você usar o Shell para instalar um suplemento para sua organização, você pode instalar o suplemento e definir configurações para ele ao mesmo tempo.



Para obter sintaxes e parâmetros, consulte [New-App](https://technet.microsoft.com/pt-br/library/jj218722\(v=exchg.150\)).

## Remover um suplemento para Outlook

## Usar o EAC para remover um suplemento

1.  No EAC, navegue até **organização** \> **suplementos**.

2.  No modo de exibição de lista, selecione o aplicativo que você deseja remover e clique em **Excluir**![Excluir ícone](images/JJ673559.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Excluir ícone").

## Use o Shell para remover um suplemento

Você pode usar o Shell para remover um suplemento da sua organização.


> [!TIP]
> Execute o seguinte comando para pesquisar os nomes de exibição e as IDs de aplicativo para todos os suplementos para Outlook instalado para sua organização.



    Get-App -OrganizationApp |FL DisplayName,AppID

Execute o seguinte comando para remover o personalizado suplemento Finance Test Add-in da organização.

    Remove-App -OrganizationApp -Identity <GUID for Finance Test Add-in>

Para obter sintaxes e parâmetros, consulte [Remove-App](https://technet.microsoft.com/pt-br/library/jj218709\(v=exchg.150\)).

## Como saber se funcionou?

Para exibir os suplementos que estão instalados em sua organização, execute um o seguinte:

  - No EAC, navegue até **organização** \> **Add-ins** e, em seguida, reveja a lista de suplementos instalados.

  - No Shell, execute `Get-App`e, em seguida, examine a lista de suplementos instalados.

