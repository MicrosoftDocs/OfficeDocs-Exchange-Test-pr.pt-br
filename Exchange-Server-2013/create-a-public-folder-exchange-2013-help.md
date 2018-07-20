---
title: 'Criar uma pasta pública: Exchange 2013 Help'
TOCTitle: Criar uma pasta pública
ms:assetid: 6d252e60-c8d0-4efd-b9d7-ba5284a6f8ab
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb691104(v=EXCHG.150)
ms:contentKeyID: 50485894
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.PublicFolders.NewPublicFolderWizardForm.NewPublicFolderWizardPage
ms.translationtype: MT
---

# Criar uma pasta pública

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013_

_**Tópico modificado em:** 2014-02-24_

As pastas públicas são feitas para acesso compartilhado e oferecem um jeito fácil e eficaz de coletar, organizar e compartilhar informações com outros pessoas no seu grupo de trabalho ou organização.

Por padrão, uma pasta pública herda as configurações de sua pasta pai, incluindo as configurações das permissões.


> [!TIP]
> Para saber mais sobre as cotas de armazenamento e limites para pastas públicas, consulte os seguintes tópicos: 
> <UL>
> <LI>
> <P>Para pastas públicas no Office 365, confira <A href="https://go.microsoft.com/fwlink/?linkid=391188">Limites do Exchange Online</A>.</P>
> <LI>
> <P>Para pastas públicas no Exchange Server 2013 local, consulte <A href="limits-for-public-folders-exchange-2013-help.md">Limites para pastas públicas</A>.</P></LI></UL>



Para conhecer tarefas de gerenciamento adicionais relacionadas ao gerenciamento de pastas públicas, consulte [Procedimentos de pasta pública](public-folder-procedures-exchange-2013-help.md).

Para conhecer tarefas de gerenciamento adicionais relacionadas a pastas públicas, consulte [Procedimentos de pasta pública no Office 365 e Exchange Online](https://technet.microsoft.com/pt-br/library/jj966272\(v=exchg.150\)).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 5 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Pastas públicas" no tópico [Permissões de compartilhamento e colaboração](sharing-and-collaboration-permissions-exchange-2013-help.md).

  - Você não pode criar uma pasta pública, a menos que você tenha criado primeiro uma caixa de correio de pasta pública. Para obter mais informações sobre como criar uma caixa de correio de pasta pública, consulte [Criar uma caixa de correio de pasta pública](create-a-public-folder-mailbox-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

## O que você deseja fazer?

## Usar o EAC para criar uma pasta pública

Ao usar o EAC para criar uma pasta pública, você precisará somente definir o nome e o caminho da pasta pública. Para definir configurações adicionais, você precisará editar a pasta pública após ela ser criada.

1.  Navegue até **Pastas públicas** \> **Pastas públicas**.

2.  Se você quiser criar essa pasta pública como uma filha de uma pasta pública existente, clique na pasta pública existente no modo de exibição de lista. Se você quiser criar uma pasta pública de nível superior, pule esta etapa.

3.  Clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar").

4.  Em **Pasta Pública**, digite o nome da pasta pública.
    

    > [!IMPORTANT]
    > Não use barra invertida (\) no nome ao criar uma pasta pública.



5.  Na caixa **Caminho**, verifique o caminho para a pasta pública. Se não for o caminho desejado, clique em **Cancelar** e siga a Etapa 2 deste procedimento.

6.  Clique em **Salvar**.

## Use o Shell para criar uma pasta pública

Este exemplo cria uma pasta pública chamada Reports no caminho Marketing\\2013.

    New-PublicFolder -Name Reports -Path \Marketing\2013


> [!IMPORTANT]
> Não use barra invertida (\) no nome ao criar uma pasta pública.



Para informações detalhadas de sintaxes e de parâmetros, consulte [New-PublicFolder](https://technet.microsoft.com/pt-br/library/aa996405\(v=exchg.150\)).

## Como saber se funcionou?

Para verificar que você criou com êxito uma pasta pública, faça o seguinte:

  - No EAC, clique em **Atualizar**, para atualizar a lista de pastas públicas. Sua nova pasta pública deve aparecer na lista.

  - No Shell, execute um destes comandos:
    
```
        Get-PublicFolder -Identity \Marketing\2013\Reports | Format-List
```
```    
        Get-PublicFolder -Identity \Marketing\2013 -GetChildren
```
```    
        Get-PublicFolder -Recurse
```

> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.


