---
title: 'Habilitar a publicação de calendário da Internet: Exchange 2013 Help'
TOCTitle: Habilitar a publicação de calendário da Internet
ms:assetid: b4c71696-52bb-492c-8259-0e419acd0bbc
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ853046(v=EXCHG.150)
ms:contentKeyID: 50556280
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Habilitar a publicação de calendário da Internet

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013_

_**Tópico modificado em:** 2016-08-22_

**Resumo:**  Use estes procedimentos para permitir que os usuários do OWA em sua organização do Exchange 2013 compartilhar informações de disponibilidade de calendário com organizações externas.

Usuários nas organizações do Microsoft Exchange Server 2013 podem compartilhar informações de disponibilidade de calendário com usuários de organizações que não sejam do Exchange e outros indivíduos com acesso à Internet. A publicação de calendário na Internet oferece maior flexibilidade e aumenta a quantidade de usuários que podem compartilhar as informações de disponibilidade de calendário.

O processo de habilitação da publicação de calendário na Internet é feito em três etapas:

1.  Configure a URL do proxy da Web para o servidor de caixa de correio (esta etapa só é necessária se um proxy da Web URL já existe na sua organização, caso contrário, pule para a etapa 2).

2.  Habilitar o diretório virtual de publicação para o Servidor de Acesso para Cliente.

3.  Criar uma política de compartilhamento dedicada especificamente para a publicação de calendários na Internet ou atualizar a política de compartilhamento padrão para oferecer suporte ao domínio **Anônimo**. Esses métodos permitem que os usuários na sua organização do Exchange convidem outros usuários com acesso à Internet para exibir informações de disponibilidade de calendário limitadas acessando a URL publicada.


> [!IMPORTANT]
> Após concluir a etapa 3, os usuários, precisará publicar seus calendários do Outlook. Publicação de calendário cria URLs que os usuários podem dar às pessoas fora da sua organização. Um URL permite que os destinatários assinem calendários usando o Outlook ou Outlook Web App e o outro permite que o modo de exibição de destinatário um calendário em um navegador da Web. Cada usuário pode controlar quanto detalhe outras pessoas podem ver.



Para ver mais tarefas de gerenciamento relacionadas às diretivas de compartilhamento, consulte [Diretivas de compartilhamento](sharing-policies-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para a conclusão da tarefa: 15 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Permissões de calendário e compartilhamento" no tópico [Permissões de destinatários](recipients-permissions-exchange-2013-help.md).

  - Um servidor de Acesso para Cliente do Exchange 2013 existe na organização do Exchange que está compartilhando as informações de calendário do usuário.

  - As caixas de correio do usuário estão nos servidores de Caixa de Correio do Exchange 2013 na organização do Exchange que está compartilhando as informações de calendário do usuário.

  - Somente os usuários do Outlook 2010 ou versão superior e do Outlook Web App podem criar convites de compartilhamento.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## Como isso é feito?

## Etapa 1: Usar o Shell para configurar a URL do proxy da Web


> [!TIP]
> Esta etapa só é necessária se já existir uma URL de proxy da Web em sua organização. Caso contrário, pule para a etapa 2.<BR>Não é possível usar o Centro de Administração do Exchange (EAC) para configurar a URL do proxy da Web.



Este exemplo configura uma URL do proxy da Web em um servidor de Caixa de Correio MAIL01.

    Set-ExchangeServer -Identity "MAIL01" -InternetWebProxy "<Webproxy URL>"

Para obter informações detalhadas sobre sintaxe e parâmetros, consulte [Set-ExchangeServer](https://technet.microsoft.com/pt-br/library/bb123716\(v=exchg.150\)).

## Como saber se essa etapa funcionou?

Para verificar se você configurou a URL do proxy Web com êxito, execute o seguinte comando no Shell e verifique as informações sobre o parâmetro *InternetWebProxy*.

    Get-ExchangeServer | format-list

## Etapa 2: Usar o Shell para habilitar o diretório virtual de publicação


> [!TIP]
> Não é possível usar o EAC para habilitar um diretório virtual de publicação.



Este exemplo habilita a publicação do diretório virtual no Servidor de Acesso para Cliente CAS01.

    Set-OwaVirtualDirectory -Identity "CAS01\owa (Default Web Site)" -ExternalUrl "<URL for CAS01>" -CalendarEnabled $true

Onde a identidade `CAS01\owa (Default Web Site)` é o nome do servidor e o diretório virtual do Outlook Web App.

Para obter informações detalhadas sobre sintaxe e parâmetros, consulte [Set-OwaVirtualDirectory](https://technet.microsoft.com/pt-br/library/bb123515\(v=exchg.150\)).

## Como saber se essa etapa funcionou?

Para verificar se você habilitou o diretório virtual de publicação com êxito, execute o seguinte comando no Shell e verifique as informações sobre o parâmetro *ExternalURL*.

    Get-OwaVirtualDirectory | format-list

## Etapa 3: Criar ou configurar uma política de compartilhamento específica para publicação de calendário da Internet


> [!TIP]
> As seguintes opções na etapa 3 somente se aplicam aos ambientes Exchange Online.



Você tem a opção de criar uma política de compartilhamento para Internet de publicação de calendário (opção 1) ou configurando a política de compartilhamento de calendário da Internet publishing (opção 2) padrão. Com as duas opções, você tem a opção de usar o EAC ou o Shell.

## Opção 1: Criar uma política de compartilhamento específica para publicação de calendário da Internet

Se você deseja criar uma política de compartilhamento específica para publicação de calendário na Internet, complete as etapas a seguir.

## Usar o EAC

1.  Navegue até **Organização**\> **Compartilhamento**.

2.  Na modo de exibição de lista, em **Compartilhamento Individual**, clique em **Novo**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar").

3.  Em **Política de Compartilhamento**, digite um nome amigável para a política de compartilhamento no campo **Nome da política** (por exemplo, **Internet**).

4.  Clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar") para definir as regras de compartilhamento da política de compartilhamento.

5.  Em **Regra de Compartilhamento**, clique em **Compartilhar com um domínio específico** e digite **Anonymous** na caixa correspondente.

6.  Para especificar os níveis de compartilhamento de calendário que deseja reforçar para a política de compartilhamento, marque a caixa de seleção **Compartilhar pasta de calendário** e selecione uma das seguintes opções:
    
      - **Informações de disponibilidade de calendário somente com hora**
    
      - **Informações de disponibilidade de calendário com hora, assunto e local**
    
      - **Todas as informações do compromisso do calendário, incluindo hora, assunto, local e título**

7.  Clique em **Salvar** para determinar as regras da política de compartilhamento.

8.  Em **Política de compartilhamento**, clique em **Salvar** para criar a política.

## Usar o Shell

Este exemplo cria uma política de compartilhamento de publicação de calendário na Internet chamada "Internet" e configura a política para compartilhar somente informações de disponibilidade. A política é habilitada.

    New-SharingPolicy -Name "Internet" -Domains 'Anonymous: CalendarSharingFreeBusySimple' -Enabled $true

Este exemplo adiciona a política de compartilhamento de Internet a uma caixa de correio de usuário.

    Set-Mailbox -Identity <user name> -SharingPolicy "Internet"

Este exemplo adiciona a política de compartilhamento de Internet à unidade organizacional (UO).

    Set-Mailbox -OrganizationalUnit <OU name> -SharingPolicy "Internet"

Para obter informações detalhadas sobre sintaxe e parâmetros, consulte [New-SharingPolicy](https://technet.microsoft.com/pt-br/library/dd298186\(v=exchg.150\)) e [Set-Mailbox](https://technet.microsoft.com/pt-br/library/bb123981\(v=exchg.150\)).

## Como saber se essa etapa funcionou?

Para verificar se você criou a política de compartilhamento com êxito, execute o seguinte comando do Shell para verificar as informações de política de compartilhamento.

    Get-SharingPolicy <policy name> | format-list

## Opção 2: Configurar a política para publicação de calendário da Internet de compartilhamento padrão

Se você deseja configurar a política de compartilhamento padrão para publicação de calendário na Internet, complete as etapas a seguir.

## Usar o EAC

1.  Navegue até **Organização** \> **Compartilhamento**.

2.  No modo de exibição de lista, em **Compartilhamento Individual**, selecione a Política de Compartilhamento Padrão e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Em **Política de Compartilhamento**, clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar") para adicionar uma regra de compartilhamento à política.

4.  Em **Regra de Compartilhamento**, clique em **Compartilhar com um domínio específico** e digite **Anonymous** na caixa correspondente.

5.  Para especificar os níveis de compartilhamento de calendário que deseja reforçar para a política de compartilhamento, marque a caixa de seleção **Compartilhar pasta de calendário** e selecione uma das seguintes opções:
    
      - **Informações de disponibilidade de calendário somente com hora**
    
      - **Informações de disponibilidade de calendário com hora, assunto e local**
    
      - **Todas as informações do compromisso do calendário, incluindo hora, assunto, local e título**

6.  Clique em **Salvar** para determinar as regras da política de compartilhamento.

7.  Em **Política de Compartilhamento**, clique em **Salvar** para salvar as alterações.

## Usar o Shell

Esse exemplo atualiza a Política de Compartilhamento Padrão e configura a política de maneira que sejam compartilhadas somente informações de disponibilidade. A política é habilitada.

    Set-SharingPolicy -Name "Default Sharing Policy" -Domains 'Anonymous: CalendarSharingFreeBusySimple' -Enabled $true

Para obter informações detalhadas sobre sintaxe e parâmetros, consulte [Set-Mailbox](https://technet.microsoft.com/pt-br/library/bb123981\(v=exchg.150\)).

## Como saber se essa etapa funcionou?

Para verificar se você atualizou a Política de Compartilhamento Padrão com êxito e verificar as informações sobre a política de compartilhamento, execute o seguinte comando do Shell.

    Get-SharingPolicy <policy name> | format-list

