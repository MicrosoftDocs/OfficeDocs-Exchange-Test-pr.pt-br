---
title: 'Configurar pastas públicas em uma nova organização: Exchange 2013 Help'
TOCTitle: Configurar pastas públicas em uma nova organização
ms:assetid: 7b419906-8977-47f0-8687-a87911b5ebec
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ651147(v=EXCHG.150)
ms:contentKeyID: 50485984
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurar pastas públicas em uma nova organização

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2015-11-09_

**Resumo:**  como configurar pastas públicas, inclusive na atribuição de permissões para acessá-los no EAC.

Este tópico mostra como configurar e executar pastas públicas em uma nova organização ou em uma organização que nunca teve pastas públicas antes.


> [!NOTE]
> Para saber mais sobre as cotas de armazenamento e limites para pastas públicas, consulte os seguintes tópicos: 
> <UL>
> <LI>
> <P>Para pastas públicas no Office 365, confira <A href="https://go.microsoft.com/fwlink/?linkid=391188">Limites do Exchange Online</A>.</P>
> <LI>
> <P>Para pastas públicas no Exchange Server 2013 local, consulte <A href="limits-for-public-folders-exchange-2013-help.md">Limites para pastas públicas</A>.</P></LI></UL>



Para conhecer tarefas de gerenciamento adicionais relacionadas a pastas públicas no Exchange Server 2013, consulte [Procedimentos de pasta pública](public-folder-procedures-exchange-2013-help.md).

Para conhecer tarefas de gerenciamento adicionais relacionadas a pastas públicas no Exchange Online, consulte [Procedimentos de pasta pública no Office 365 e Exchange Online](https://technet.microsoft.com/pt-br/library/jj966272\(v=exchg.150\)).

## O que você precisa saber antes de começar?

  - Tempo estimado para a conclusão da tarefa: 30 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Pastas públicas" no tópico [Permissões de compartilhamento e colaboração](sharing-and-collaboration-permissions-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## Como fazer isso?

## Etapa 1: Criar caixa de correio de pasta pública principal

A caixa de correio da pasta pública principal contém um cópia gravável da hierarquia da pasta pública mais o conteúdo e é a primeira caixa de correio de pasta pública que você cria para a sua organização. As caixas de correio de pasta pública posteriores serão as caixas de correio de pasta pública secundárias, que conterão uma cópia somente de leitura da hierarquia mais o conteúdo.

Para obter etapas detalhadas, consulte [Criar uma caixa de correio de pasta pública](create-a-public-folder-mailbox-exchange-2013-help.md).

## Etapa 2: Criar sua primeira pasta pública

Para obter etapas detalhadas, consulte [Criar uma pasta pública](create-a-public-folder-exchange-2013-help.md).

## Etapa 3: Atribuir permissões para a pasta pública

Depois que você criar a pasta pública, precisará atribuir o nível de permissões de **Proprietário**, para que um usuário, pelo menos, possa acessar a pasta pública, usando o cliente, e criar subpastas. Quaisquer pastas públicas criadas depois desta irão herdar as permissões da pasta pública pai.

1.  No centro de administração do Exchange (EAC), vá em **Pastas públicas** \> **Pastas públicas**.

2.  No modo de exibição de lista, selecione a pasta pública.

3.  No painel de detalhes, em **Permissões de Pasta**, clique em **Gerenciar**.

4.  Em **Permissões de Pasta Pública**, clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar").

5.  Clique em **Procurar**, para selecionar um usuário.

6.  Na lista **Nível de permissão**, selecione um nível. Pelo menos um usuário deve ser um **Proprietário**.

7.  Clique em **Salvar**.

8.  Você pode adicionar vários usuários, clicando em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar") e atribuindo as permissões apropriadas usando as instruções acima. Você também pode personalizar o nível de permissão, selecionando ou limpando as caixas de verificação. Quando você editar um nível de permissão pré-definido, como **Proprietário**, o nível de permissão irá mudar para **Personalizado**.

Para obter informações sobre como usar o Shell para atribuir permissões a uma pasta pública, consulte [Add-PublicFolderClientPermission](https://technet.microsoft.com/pt-br/library/bb124743\(v=exchg.150\)).

## Etapa 4 (Opcional): Habilitar pasta pública para email

Se você quiser que usuários enviem emails para a pasta pública, você poderá habilitá-la para email. Esta etapa é opcional. Se você não habilitar a pasta pública para email, os usuários podem postar mensagens na pasta pública arrastando os itens para dentro dela a partir do Outlook.

1.  No EAC, navegue até **Pastas públicas** \> **Pastas públicas**.

2.  No modo de exibição de lista, selecione a pasta pública que você deseja habilitar para email.

3.  No painel de detalhes, em **Configurações de email – Desabilitado**, clique em **Habilitar**.
    
    Aparecerá um aviso, perguntando se você tem certeza de que deseja habilitar o email para a pasta pública. Clique em **Sim**.

A pasta pública será habilitada para email, e o nome da pasta pública irá se tornar o alias da pasta pública. Se você tiver vários destinatários com esse nome, o alias da pasta pública receberá um número. Por exemplo, se você tiver um grupo de distribuição chamado SalesTeam e você criar uma pasta pública chamada SalesTeam e habilitá-la para email, o alias dessa pasta pública será SalesTeam1.

Para obter informações sobre como usar o Shell para habilitar para email uma pasta pública, consulte [Enable-MailPublicFolder](https://technet.microsoft.com/pt-br/library/aa998824\(v=exchg.150\)).

