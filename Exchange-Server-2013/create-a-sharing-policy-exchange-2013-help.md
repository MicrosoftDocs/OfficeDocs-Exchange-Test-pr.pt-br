---
title: 'Criar uma política de compartilhamento: Exchange 2013 Help'
TOCTitle: Criar uma política de compartilhamento
ms:assetid: cae8cab0-6265-448b-8add-5202cdb20678
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ657494(v=EXCHG.150)
ms:contentKeyID: 50486639
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Criar uma política de compartilhamento

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2015-04-07_

É possível usar as políticas de compartilhamento para controlar o modo como os usuários em sua organização do Exchange compartilham informações de calendário com usuários de fora da sua organização. Políticas de compartilhamento fornecem o compartilhamento entre pessoas estabelecido pelo usuário de informações de calendário com tipos diferentes de usuários externos. Elas suportam o compartilhamento de informações do calendário com organizações externas federadas (como Office 365 ou outra organização local do Exchange), organizações externas não federadas e pessoas com acesso à Internet. Para aplicar uma política de compartilhamento específica aos usuários, consulte [Aplicar uma política de compartilhamento às caixas de correio](apply-a-sharing-policy-to-mailboxes-exchange-2013-help.md).


> [!IMPORTANT]
> Criar uma política de compartilhamento é uma das várias etapas de configuração de compartilhamento federado na sua organização do Exchange. Você precisa configurar uma confiança de federação com o sistema de autenticação Azure Active Directory para sua organização do Exchange no local para poder compartilhar informações de calendário com outras organizações federadas do Exchange. Uma relação de confiança de Federação não é exigida para diretivas de compartilhamento de Internet.



Para saber mais sobre compartilhamento federado, consulte [Compartilhamento](sharing-exchange-2013-help.md).

Para tarefas de gerenciamento adicionais relacionadas à federação, consulte [Procedimentos de Federação](federation-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 15 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o "Calendário e permissões de compartilhamento? seção no tópico [Permissões de destinatários](recipients-permissions-exchange-2013-help.md) .

  - Requisitos para as políticas de compartilhamento entre organizações do Exchange de domínio federado:
    
      - Um servidor de acesso para cliente do Exchange 2013 existe em cada organização do Exchange. Também há suporte para as políticas de compartilhamento entre organizações do Exchange em que uma organização tem Exchange 2013 servidores de acesso para cliente e a uma outra organização tem Exchange 2010 SP3 ou posteriores servidores de acesso para cliente.
    
      - Cada organização do Exchange criou uma confiança de federação com o sistema de autenticação AD do Azure. Para obter detalhes, consulte [Configurar uma confiança de Federação](configure-a-federation-trust-exchange-2013-help.md).
    
      - Cada organização do Exchange configurou um identificador de organização federada. Domínios usados para gerar endereços de email de usuários já adicionados aos identificadores da organização.
    
      - Caixas de correio do usuário estão localizadas nos servidores de caixa de correio de Exchange 2013 ou servidores de caixa de correio de Exchange 2010 em cada organização do Exchange.
    
      - Apenas os usuários do Outlook 2010 ou superior e do Outlook Web App podem enviar convites de compartilhamento.

  - Estes são os requisitos para as políticas de compartilhamento com organizações do Exchange não federadas ou com pessoas:
    
      - Um Servidor de Acesso para Cliente do Exchange 2013 existe na organização do Exchange que está compartilhando informações de calendário do usuário.
    
      - As caixas de correio do usuário estão nos servidores de caixa de correio do Exchange 2013 da organização do Exchange que está compartilhando as informações de calendário do usuário.
    
      - O Servidor de Acesso para Cliente do Exchange 2013 deve estar habilitado para acesso ao Outlook Web App.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

## O que você deseja fazer?

## Use o EAC para criar uma política de compartilhamento

1.  Navegue até **organização**\> **compartilhamento**.

2.  Na modo de exibição de lista, em **Compartilhamento Individual**, clique em **Novo**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar").

3.  Em **nova política de compartilhamento**, digite um nome amigável para a política de compartilhamento na caixa **Nome da política**.

4.  Clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar"), para especificar as regras de compartilhamento da política de compartilhamento.

5.  Em **regra de compartilhamento**, selecione uma das opções a seguir para especificar os domínios com os quais você deseja compartilhar:
    
      - **Compartilhando com todos os domínios**
    
      - **Compartilhar com um domínio específico**

6.  Se você selecionar **Compartilhar com um domínio específico**, digite o nome do domínio com o qual você deseja compartilhar. Se for necessário inserir mais de um domínio para essa política de compartilhamento, salve as configurações para o primeiro domínio e depois edite as regras de compartilhamento para adicionar mais domínios.

7.  Para definir os níveis de compartilhamento de calendário que você deseja impor para a política, marque a caixa de seleção **Compartilhar sua pasta de calendário** e selecione uma destas opções:
    
      - **Informações de disponibilidade de calendário somente com hora**
    
      - **Informações de disponibilidade de calendário com hora, assunto e local**
    
      - **Todas as informações do compromisso do calendário, incluindo hora, assunto, local e título**

8.  Clique em **salvar** para determinar as regras da política de compartilhamento.

9.  Se desejar tornar esta política de compartilhamento a política padrão para os usuários na sua organização do Exchange, marque a caixa de seleção **Tornar essa política a minha política de compartilhamento padrão**.

10. Clique em **salvar** para criar a política de compartilhamento.

## Usar o EAC para permitir que todos os usuários compartilhem detalhes do calendário completo

Você pode editar a política de compartilhamento padrão para permitir que todos os usuários compartilhem detalhes do calendário completo com pessoas de fora da organização.

1.  Navegue até **organização**\> **compartilhamento**.

2.  Na exibição de lista, em **Compartilhamento Individual**, selecione a **Política de Compartilhamento Padrão** e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na caixa de diálogo **Política de Compartilhamento**, selecione **Compartilhamento com todos os domínios** e então clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

4.  Na caixa de diálogo **Regra de Compartilhamento**, em **Especifique quais informações você deseja compartilhar**, selecione **Todas as informações do compromisso, incluindo hora, assunto, local e título** e clique em **salvar**.

5.  Na caixa de diálogo **Política de Compartilhamento**, clique em **salvar** para definir as regras da política de compartilhamento.

## Usar o Shell para criar uma diretiva de compartilhamento

  - Este exemplo cria a política de compartilhamento Contoso para o domínio externo federado contoso.com. Essa política permite que os usuários do domínio contoso.com visualizem informações detalhadas de disponibilidade de calendário do usuário. Por padrão, essa diretiva está habilitada.
    
    ```powershell
New-SharingPolicy -Name "Contoso" -Domains contoso.com: CalendarSharingFreeBusyDetail
```

  - Este exemplo cria a política de compartilhamento ContosoWoodgrove para dois domínios federados diferentes (contoso.com e woodgrovebank.com) com deferentes ações de compartilhamento configuradas para cada domínio. A política é desabilitada.
    
        New-SharingPolicy -Name "ContosoWoodgrove" -Domains 'contoso.com: CalendarSharingFreeBusySimple', 'woodgrovebank.com: CalendarSharingFreeBusyDetail -Enabled $false

  - Este exemplo cria a política de compartilhamento Anonymous para uma organização do Exchange com o servidor de Acesso para Cliente CAS01 e o servidor de Caixa de Correio MAIL01 com a ação de compartilhamento configurada para informações de disponibilidade de calendário limitadas. Essa política permite que usuários em sua organização do Exchange convidem usuários com acesso à Internet para visualizar suas informações de disponibilidade de calendário enviando a eles um link. A política é habilitada.
    
    1.  Defina o URL do proxy Web para MAIL01.
        
        ```powershell
Set-ExchangeServer -Identity "Mail01" -InternetWebProxy "<Webproxy URL>"
```
    
    2.  Permitir a publicação do diretório virtual no CAS01.
        
            Set-OwaVirtualDirectory -Identity "CAS01" -ExternalURL "<URL for CAS01>" -CalendarPublishingEnabled $true
    
    3.  Criar a política de compartilhamento Anônima e configurar o compartilhamento de informações de calendário limitado.
        
            New-SharingPolicy -Name "Anonymous" -Domains 'Anonymous: CalendarSharingFreeBusySimple' -Enabled $true

Para obter informações detalhadas sobre sintaxes e parâmetros, consulte os seguintes tópicos:

  - [New-SharingPolicy](https://technet.microsoft.com/pt-br/library/dd298186\(v=exchg.150\))

  - [Set-ExchangeServer](https://technet.microsoft.com/pt-br/library/bb123716\(v=exchg.150\))

  - [Set-OwaVirtualDirectory](https://technet.microsoft.com/pt-br/library/bb123515\(v=exchg.150\))

## Como saber se funcionou?

Para verificar se você criou a política de compartilhamento com êxito, execute o seguinte comando do Shell, para verificar as informações de política de compartilhamento.

```powershell
Get-SharingPolicy <policy name> | format-list
```


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.


