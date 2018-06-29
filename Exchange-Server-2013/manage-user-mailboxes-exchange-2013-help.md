---
title: 'Gerenciar caixas de correio do usuário: Exchange Online Help'
TOCTitle: Gerenciar caixas de correio do usuário
ms:assetid: 957ca61c-1fa1-42ab-a0e6-8488e4782566
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb123809(v=EXCHG.150)
ms:contentKeyID: 50486232
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.Recipients.NewMailboxWizardForm.NewMailboxIntroductionWizardPage
ms.translationtype: HT
---

# Gerenciar caixas de correio do usuário

 

_**Aplica-se a:**Exchange Online, Exchange Server 2013_

_**Tópico modificado em:**2014-05-27_

Após criar uma caixa de correio de usuário, você pode fazer alterações e definir propriedades adicionais usando o EAC ou o Shell.

Você também pode alterar as propriedades de várias caixas de correio de usuário ao mesmo tempo. Para mais informações, consulte Editar em massa as caixas de correio de usuários.

## O que você precisa saber antes de começar?

  - Tempo estimado para concluir cada tarefa de caixa de correio do usuário: 2 a 5 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Seção "Permissões de provisionamento do destinatário", no tópico [Permissões de destinatários](recipients-permissions-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Alterar propriedades de caixa de correio de usuário

## Usar o EAC para alterar as propriedades de caixa de correio de usuário

1.  No EAC, navegue até **Destinatários** \> **Caixas de correio**.

2.  Na lista de caixas de correio de usuários, clique na caixa de correio cujas propriedades você quer alterar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na página de propriedades da caixa de correio, clique em uma destas seções, para exibir ou alterar propriedades.
    
      - Geral
    
      - Utilização da Caixa de Correio
    
      - Informações de contato
    
      - Organização
    
      - Endereço de Email
    
      - Recursos da Caixa de Correio
    
      - Membro de
    
      - Dica de Email
    
      - Delegação da Caixa de Correio

## Geral

Use a seção **Geral** para ver ou alterar as informações básicas sobre o usuário.

  - **Nome**, **Iniciais**, **Sobrenome**

  - **\* Nome**   Esse é o nome que está listado em Active Directory. Se você alterar esse nome, não pode exceder 64 caracteres.

  - **\* Nome para exibição** Esse nome será exibido no catálogo de endereços da sua organização, nas linhas Para: e na linha De: no email e na lista de Caixas de Correio. Esse nome não pode conter espaços vazios antes ou depois do nome para exibição.

  - **\* Alias** Isso especifica o alias de email do usuário. O alias do usuário é a parte do endereço de email à esquerda do símbolo @. Ele deve ser exclusivo na floresta.

  - **\* Nome de logon do usuário**   Esse é o nome que o usuário irá utilizar para fazer o logon na caixa de correio e fazer o logon no domínio. Geralmente, o nome de logon do usuário consiste no alias do usuário à esquerda do símbolo @ e no nome do domínio no qual a conta de usuário reside à direita do símbolo @.
    

    > [!TIP]
    > Essa caixa foi rotulada como <STRONG>ID do Usuário</STRONG> no Exchange Online.



  - **Exigir alteração de senha no próximo logon**   Marque essa caixa de seleção se quiser que o usuário redefina a senha da próxima vez que fizer logon na caixa de correio.
    

    > [!TIP]
    > Essa caixa de seleção não está disponível no Exchange Online.



  - **Ocultar das listas de endereço**   Marque essa caixa de seleção para evitar que o destinatário apareça no catálogo de endereços e em outras listas de endereço definidas na sua organização do Exchange. Depois que você marcar essa caixa de seleção, os usuários ainda poderão enviar mensagens ao destinatário usando o endereço de email.

Clique em **Mais opções**, para exibir ou alterar essas propriedades adicionais:

  - **Unidade organizacional**  Essa caixa somente leitura exibe a unidade organizacional (OU) que contém a conta do usuário. Você pode usar Usuários e Computadores do Active Directory para mover a conta de usuário para uma OU diferente.
    

    > [!TIP]
    > Essa caixa não está disponível no Exchange Online.



  - **Banco de dados de caixa de correio**   Esse campo somente leitura exibe o nome do banco de dados de caixa de correio que hospeda a caixa de correio. Para mover a caixa de correio para um banco de dados diferente, selecione-a na lista de caixas de correio e clique em **Mover caixa de correio para outro banco de dados** no painel Detalhes.
    

    > [!TIP]
    > Essa opção não está disponível no Exchange Online.



  - **Atributos personalizáveis**   Essa seção exibe os atributos personalizáveis definidos para a caixa de correio do usuário. Para especificar valores de atributos personalizáveis, clique em **Editar**. Você pode especificar até 15 atributos personalizados para o destinatário.

## Utilização da Caixa de Correio

Clique na seção **Uso da Caixa de Correio** para ver ou alterar a cota de armazenamento da caixa de correio e as configurações de retenção de itens excluídos para a caixa de correio. Essas configurações são configuradas por padrão quando a caixa de correio é criada. Eles usam os valores configurados para o banco de dados de caixa de correio e os aplicam a todas as caixas de correio nesse banco de dados. Você pode personalizar essas configurações para cada caixa de correio, em vez de usar os padrões do banco de dados de caixa de correio.

  - **Último logon**   Essa caixa somente para leitura exibe o horário da última vez em que o usuário fez logon na sua caixa de correio.

  - **Utilização de caixa de correio**   Essa área mostra o tamanho total da caixa de correio e a porcentagem da cota total de caixa de correio que foi usada.


> [!TIP]
> Para obter as informações exibidas nas duas caixas anteriores, o EAC consulta o banco de dados de caixas de correio que hospeda a caixa de correio. Se o EAC não puder se comunicar com o repositório do Exchange que contém o banco de dados de caixas de correio, essas caixas ficarão vazias. Uma mensagem de aviso será exibida, se o usuário não tiver feito login na caixa de correio pela primeira vez.



Clique em **More options**, para ver ou alterar a cota de armazenamento da caixa de correio e as configurações de retenção de itens excluídos para a caixa de correio.


> [!TIP]
> Essas configurações não estão disponíveis no EAC do Exchange Online.



  - **Configurações de cota de armazenamento**   Para personalizar essas configurações da caixa de correio e não usar os padrões do banco de dados de caixas de correio, clique em **Personalizar as configurações desta caixa de correio**, digite um novo valor e clique em **Salvar**.
    
    O intervalo de valores para qualquer configuração de cota de armazenamento vai de 0 a 2074 gigabytes (GB).
    
      - **Emitir aviso em (GB)**   Essa caixa mostra o limite máximo de armazenamento antes de um aviso ser emitido para o usuário. Se o tamanho da caixa de correio atingir ou exceder o valor especificado, o Exchange enviará uma mensagem de aviso para o usuário.
    
      - **Proibir envio em (GB)**   Essa caixa mostra o limite para *proibir envio* para a caixa de correio. Se o tamanho da caixa de correio atingir ou exceder o limite especificado, o Exchange impedirá que o usuário da caixa de correio envie novas mensagens e exibirá uma mensagem de erro descritiva.
    
      - **Proibir envio e recebimento em (GB)**   Essa caixa mostra o limite para *proibir envio e recebimento* para a caixa de correio. Se o tamanho da caixa de correio atingir ou exceder o limite especificado, o Exchange impedirá que o usuário da caixa de correio envie novas mensagens e não entregará nenhuma mensagem nova para a caixa de correio. Todas as mensagens enviadas para a caixa de correio são devolvidas ao remetente com uma mensagem de erro descritiva.

  - **Configurações de retenção de itens excluídos**   Para personalizar essas configurações da caixa de correio e não usar os padrões do banco de dados de caixas de correio, clique em **Personalizar as configurações desta caixa de correio**, digite um novo valor e clique em **Salvar**.
    
      - **Manter itens excluídos por (dias)**   Essa caixa mostra o tempo pelo qual itens excluídos serão mantidos, antes de serem permanentemente excluídos e não poderem ser recuperados pelo usuário. Quando a caixa de correio é criada, esse valor é baseado nas configurações de retenção de itens excluídos definidas para o banco de dados de caixa de correio. Por padrão, um banco de dados de caixa de correio é configurado para manter itens excluídos por 14 dias. O intervalo de valores para essa propriedade é de 0 a 24855 dias.
    
      - **Não excluir itens permanentemente até que seja feito backup do banco de dados**   Marque essa caixa de seleção para impedir que caixas de correio e emails sejam excluídos permanentemente até que seja feito backup do banco de dados de caixa de correio em que a caixa de correio está.

## Informações de contato

Use a seção **Informações de Contato** para exibir ou alterar as informações de contato do usuário. As informações nesta página são exibidas no catálogo de endereços. Clique em **Mais opções** para exibir caixas adicionais.


> [!TIP]
> Você pode usar também a caixa <STRONG>Estado/Província</STRONG> para criar as condições do destinatário para os grupos dinâmicos de distribuição, diretivas de endereço de email ou listas de endereços.



Usuários de caixa de correio podem utilizar o Outlook ou o Outlook Web App para exibir e alterar suas próprias informações de contato. Mas eles não podem alterar as informações nas caixas **Notas** e **Página da Web**.

## Organização

Use a seção **Organização** para registrar informações detalhadas sobre a função do usuário na organização. Estas informações são exibidas no catálogo de endereços. Além disso, você pode criar um gráfico de organização virtual acessível por clientes de email como o Outlook.

  - **Título   **Use essa caixa para visualizar ou alterar o título do destinatário.

  - **Departamento**   Use esta caixa para exibir ou alterar o departamento no qual o usuário trabalha. Você pode usar essa caixa para criar condições de destinatário para os grupos de distribuição dinâmica, diretivas de endereço de email ou listas de endereços.

  - **Empresa**   Use essa caixa para exibir ou alterar a empresa para a qual o usuário trabalha. Você pode usar essa caixa para criar condições de destinatário para os grupos de distribuição dinâmica, diretivas de endereço de email ou listas de endereços.

  - **Gerente**   Para adicionar um gerente, clique em **Procurar**. Em **Selecionar Gerente**, selecione uma pessoa e clique em **OK**.

  - **Funcionários subordinados**   Você não pode modificar essa caixa. *Funcionário subordinado* é um usuário que se reporta a um gerente específico. Se você tiver especificado um gerente para o usuário, esse usuário será exibido como um funcionário subordinado nos detalhes da caixa de correio do gerente. Por exemplo, Kari gerencia Chris e Kate, e portanto a caixa de correio de Kari está especificada na caixa **Gerente** das caixas de correio de Chris e Kate, e Chris e Kate aparecem na caixa **Funcionários subordinados**, nas propriedades da caixa de correio de Kari.

## Endereço de Email

Use a seção **Endereço de email** para exibir ou alterar os endereços de email associados à caixa de correio do usuário. Isso inclui o endereço SMTP principal do usuário e todos os endereços de proxy associados. O endereço SMTP principal (também conhecido como *endereço de resposta padrão*) será exibido em negrito, na lista de endereços, com o valor em maiúsculas **SMTP** na coluna **Tipo**.

  - **Adicionar **  Clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar") para adicionar um novo endereço de email para essa caixa de correio. Selecione um dos seguintes tipos de endereço:
    
      - **SMTP**   Esse é o tipo de endereço padrão. Clique nesse botão e digite o novo endereço SMTP na caixa **\* Endereço de email**.
    
      - **EUM**   Um endereço da Unificação de Mensagem do Exchange (EUM) é utilizado pelo serviço de Unificação de Mensagens do Microsoft Exchange para localizar usuários habilitados para UM dentro da organização do Exchange. Os endereços da EUM contêm o número da extensão e o plano de discagem de UM para o usuário habilitado para UM. Clique nesse botão e digite o novo número de ramal na caixa **Endereço/Ramal**. Em seguida, clique em **Procurar** e selecione um plano de discagem para o usuário.
    
      - **Tipo de endereço personalizado**   Clique nesse botão e digite um dos tipos de endereço de email não SMTP compatíveis na caixa **\* Endereço de email**.
        

        > [!TIP]
        > Com a exceção de endereços X.400, o Exchange não valida endereços personalizados para a formatação adequada. Certifique-se de que o endereço personalizado que você especificar esteja de acordo com os requisitos de formato para esse tipo de endereço.

    
      - **Tornar este o endereço de resposta**   No Exchange Online, você pode marcar essa caixa de seleção para transformar o novo endereço de email no endereço SMTP principal da caixa de correio. Essa caixa de seleção não está disponível no EAC do Exchange 2013.

  - **Atualizar automaticamente os endereços de email com base na política de endereços de email aplicados a este destinatário**   Marque essa caixa de seleção para que os endereços de email do destinatário sejam atualizados automaticamente com base nas alterações feitas nas políticas de endereços de email em sua organização. Essa caixa de seleção é marcada por padrão.
    

    > [!TIP]
    > Essa caixa de seleção não está disponível no Exchange Online.



  - **Tornar este o endereço de resposta**

## Recursos da Caixa de Correio

Use a seção **Recursos da Caixa de Correio** para exibir ou modificar os recursos e configurações de caixa de correio a seguir:

  - **Política de compartilhamento**   Esta caixa mostra a política de compartilhamento aplicada à caixa de correio. Uma política de compartilhamento permite controlar como usuários da sua organização podem compartilhar informações de contato e calendário com usuários de fora da organização do Exchange. A Política de Compartilhamento Padrão é atribuída a caixas de correio quando elas são criadas. Para alterar a política de compartilhamento atribuída ao usuário, selecione uma diferente, na lista suspensa.

  - **Política de atribuição de funções**   Essa caixa mostra a política de atribuição de funções atribuída à caixa de correio. A diretiva de atribuição de funções especifica as funções do controle de acesso baseado em função (RBAC) que são atribuídas ao usuário, e controla quais configurações específicas de grupo de distribuição e caixa de correio os usuários podem modificar. Para alterar a política de atribuição de funções atribuída ao usuário, selecione uma política diferente, na lista suspensa.

  - **Política de retenção**   Esta caixa mostra a política de retenção aplicada à caixa de correio. Uma política de retenção é um grupo de marcas de retenção que são aplicadas à caixa de correio do usuário. Eles permitem controlar quanto tempo os itens devem ser mantidos nas caixas de correio dos usuários e definir que ação executar sobre os itens que atingiram determinado tempo. Uma política de retenção não é atribuída às caixas de correio quando elas são criadas. Para atribuir uma política de retenção ao usuário, selecione uma na lista suspensa.

  - **Política de catálogo de endereços**   Esta caixa mostra a política de catálogo de endereços aplicada à caixa de correio. Uma política de catálogo de endereço permite que você segmente os usuários em grupos específicos, para oferecer exibições personalizadas do catálogo de endereços. Para aplicar ou alterar a diretiva de catálogo de endereços aplicada à caixa de correio, selecione uma na lista suspensa.

  - **Unificação de Mensagens**   Esse recurso é desabilitado por padrão. Quando você habilitar a Unificação de Mensagens (UM), o usuário será capaz de usar os recursos de UM da sua organização e um conjunto padrão de propriedades de UM aplicados ao usuário. Clique em **Habilitar**, para habilitar a UM para a caixa de correio. Para informações sobre como habilitar a UM, consulte [Habilitar um usuário para caixa postal](enable-a-user-for-voice-mail-exchange-2013-help.md).
    

    > [!TIP]
    > Um plano de discagem de UM e uma política de UM devem existir, antes de você poder habilitar a UM.



  - **Dispositivos Móveis**   Use essa seção para exibir e alterar as configurações do Exchange ActiveSync, que fica habilitado por padrão. O Exchange ActiveSync permite acesso a uma caixa de correio do Exchange a partir de um dispositivo móvel. Clique em **Desabilitar Exchange ActiveSync**, para desabilitar esse recurso para a caixa de correio.

  - **Outlook Web App**   Esse recurso é habilitado por padrão. O Outlook Web App permite acessar uma caixa de correio do Exchange de um navegador da Web. Clique em **Desabilitar**, para desabilitar o Outlook Web App para a caixa de correio. Clique em **Editar detalhes**, para adicionar ou alterar uma política de caixa de correio do Outlook Web App para a caixa de correio.

  - **IMAP**   Esse recurso é habilitado por padrão. Clique em **Desabilitar** para desabilitar o IMAP para a caixa de correio.

  - **POP3**   Esse recurso é habilitado por padrão. Clique em **Desabilitar** para desabilitar o POP3 para a caixa de correio.

  - **MAPI**   Esse recurso é habilitado por padrão. O MAPI permite o acesso a uma caixa de correio do Exchange de um cliente MAPI, como Outlook. Clique em **Desabilitar** para desabilitar o MAPI para a caixa de correio.

  - **Retenção de litígio**   Esse recurso é habilitado por padrão. A retenção de litígio preserva os itens excluídos da caixa de correio e registra as alterações feitas em itens da caixa de correio. Os itens excluídos e todas as instâncias de itens alterados são retornados em uma pesquisa de descoberta. Clique em **Habilitar** para colocar a caixa de correio em retenção de litígio. Se a caixa de correio estiver em retenção de litígio, clique em **Disable**, para remover a retenção de litígio. Caixas de correio em retenção de litígio ficam inativas e não podem ser excluídas. Para excluir a caixa de correio, remova a retenção de litígio. Se a caixa de correio estiver em retenção de litígio, clique em **Editar detalhes**, para exibir e alterar estas configurações de retenção de litígio:
    
      - **Data de suspensão**   Essa caixa somente para leitura indica a data e a hora em que a caixa de correio foi deixada em retenção de litígio.
    
      - **Colocado em retenção por**   Essa caixa somente leitura indica o usuário que colocou a caixa de correio em retenção de litígio.
    
      - **Observação**   Use essa caixa para notificar o usuário sobre a retenção de litígio, explicar por que a caixa de correio está em retenção de litígio ou fornecer instruções adicionais ao usuário, como informá-lo que a retenção de litígio não afetará o uso diário do email.
    
      - **URL**   Use essa caixa para fornecer uma URL para um site que contém informações ou instruções sobre a retenção de litígio da caixa de correio.
        

        > [!TIP]
        > O texto dessas caixas aparece na caixa de correio do usuário somente se ele estiver usando o Outlook 2010 ou uma versão posterior. O texto não aparece no Outlook Web App ou em outros clientes de email. Para exibir o texto das caixas Notas e URL no Outlook, clique na guia <STRONG>Arquivo</STRONG> e, na página <STRONG>Informações</STRONG>, em <STRONG>Configurações da Conta</STRONG>, você verá o comentário sobre a retenção de litígio.



  - **Arquivo morto**   Se não houver um arquivo morto para a caixa de correio, esse recurso estará desabilitado. Para habilitar uma caixa de correio de arquivo morto, clique em **Habilitar**. Se o usuário tiver uma caixa de correio de arquivo morto, o tamanho da caixa de correio de arquivo morto e as estatísticas de uso serão exibidas. Clique em **Editar detalhes**, para exibir e alterar estas configurações de caixa de correio de arquivo morto:
    
      - **Status**   Esta caixa somente leitura indica se existe uma caixa de correio de arquivo morto.
    
      - **Banco de dados**   Essa caixa somente leitura exibe o nome do banco de dados de caixa de correio que hospeda a caixa de correio do arquivo morto. Essa caixa não está disponível no Exchange Online.
    
      - **Nome**   Digite o nome da caixa de correio do arquivo morto na caixa. Esse nome é mostrado na lista de pastas no Outlook ou no Outlook Web App.
    
      - **Cota de arquivo morto (GB)**   Essa caixa mostra o tamanho total da caixa de correio de arquivo morto. Para alterar o tamanho, digite um novo valor na caixa ou selecione um valor na lista suspensa.
    
      - **Emitir aviso em (GB)**   Essa caixa mostra o limite máximo de armazenamento para a caixa de correio de arquivo morto antes de um aviso ser emitido para o usuário. Se o tamanho da caixa de correio de arquivo morto atingir ou exceder o valor especificado, o Exchange enviará uma mensagem de aviso para o usuário. Para alterar esse limite, digite um novo valor na caixa ou selecione um valor na lista suspensa.
        

        > [!TIP]
        > A cota de arquivo morto e a cota de avisos de problema da caixa de correio de arquivo morto não podem ser alteradas no Exchange Online.



  - **Opções de Entrega**   Use para encaminhar mensagens de email enviadas ao usuário para outro destinatário, e para definir o número máximo de destinatários para quem o usuário para mandar uma mensagem. Clique em **Exibir detalhes** para exibir e alterar essas configurações.
    
      - **Endereço de encaminhamento**   Marque a caixa de seleção **Habilitar encaminhamento** e clique em **Procurar**, para mostrar a página **Selecionar Usuário de Email e Caixa de Correio**. Use essa caixa de diálogo para selecionar um destinatário para o qual você deseja encaminhar todas as mensagens de email enviadas para essa caixa de correio.
    
      - **Entregar mensagem ao endereço de encaminhamento e à caixa de correio**   Marque essa caixa de seleção para que essas mensagens sejam entregues no endereço de encaminhamento e na caixa de correio do usuário.
    
      - **Limite de destinatários**   Essa configuração controla o número máximo de destinatários aos quais o usuário pode enviar uma mensagem. Marque a caixa de seleção **Máximo de destinatários** para limitar o número de destinatários permitidos nas caixas Para:, Cc: e Cco: de uma mensagem de email, e depois especifique o número máximo de destinatários.
        

        > [!TIP]
        > Para organizações do Exchange no local, o limite de destinatários é ilimitado. Para organizações do Exchange Online, o limite é de 500 destinatários.



  - **Restrições de Tamanho de Mensagem**   Essas configurações controlam o tamanho das mensagens que o usuário pode enviar e receber. Clique em **Exibir detalhes**, para exibir e alterar o tamanho máximo para mensagens enviadas e recebidas.
    

    > [!TIP]
    > Essas configurações não podem ser alteradas no Exchange Online.

    
      - **Mensagens enviadas**   Para especificar um tamanho máximo para as mensagens enviadas por esse usuário, selecione a caixa **Tamanho máximo de mensagens(KB)** e digite um valor na caixa. O tamanho da mensagem deve estar entre 0 e 2.097.151 KB. Se o usuário enviar uma mensagem maior do que o tamanho especificado, ela retornará ao remetente com uma mensagem de erro descritiva.
    
      - **Mensagens recebidas**   Para especificar um tamanho máximo para as mensagens recebidas por esse usuário, selecione a caixa **Tamanho máximo de mensagens(KB)** e digite um valor na caixa. O tamanho da mensagem deve estar entre 0 e 2.097.151 KB. Se o usuário receber uma mensagem maior do que o tamanho especificado, ela será devolvida ao remetente com uma mensagem de erro descritiva.

  - **Restrições de Entrega de Mensagem**   Essas configurações controlam quem pode enviar emails para esse usuário. Clique em **Exibir detalhes** para exibir e alterar essas restrições.
    
      - **Aceitar mensagens de**   Use essa seção para especificar quem pode enviar mensagens para esse usuário.
        
          - **Todos os remetentes**   Selecione essa opção para especificar que o usuário pode aceitar mensagens de todos os remetentes. Isso inclui remetentes tanto na sua organização do Exchange quanto externos. Esta opção é selecionada por padrão. Essa opção incluirá usuários externos apenas se você desmarcar a caixa de seleção **Requerer que todos os remetentes sejam autenticados**. Se você marcar essa caixa de seleção, mensagens de usuários externos serão rejeitadas.
        
          - **Somente remetentes da seguinte lista**   Selecione essa opção para especificar que esse grupo pode aceitar mensagens apenas de um conjunto específico de remetentes em sua organização do Exchange. Clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar")para exibir a página **Selecionar destinatários**, que exibe uma lista de todos os destinatários na sua organização do Exchange. Selecione os destinatários que deseja, adicione-os à lista e clique em **OK**. Você também pode pesquisar um destinatário específico, digitando seu nome na caixa de pesquisa e clicando em **Pesquisar**![Ícone Pesquisar](images/Dn750895.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif "Ícone Pesquisar").
        
          - **Exigir que todos os remetentes sejam autenticados**   Selecione essa opção para evitar que usuários anônimos enviem mensagens para o usuário.
    
      - **Rejeitar mensagens de**   Use essa seção para evitar que pessoas enviem enviar mensagens para esse usuário.
        
          - **Nenhum remetente**   Selecione essa opção para especificar que o destinatário não rejeitará mensagens de nenhum remetente na organização do Exchange. Esta opção é selecionada por padrão.
        
          - **Remetentes da seguinte lista**   Selecione essa opção para especificar que a caixa de correio rejeitará mensagens de um conjunto específico de remetentes em sua organização do Exchange. Clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar"), para mostrar a página **Selecionas Destinatários**, que mostra uma lista de todos os destinatários na sua organização do Exchange. Selecione os destinatários que deseja, adicione-os à lista e clique em **OK**. Você também pode pesquisar um destinatário específico, digitando seu nome na caixa de pesquisa e clicando em **Pesquisar**![Ícone Pesquisar](images/Dn750895.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif "Ícone Pesquisar").

## Membro de

Use a seção **Membro de** para visualizar uma lista de grupos de distribuição ou de segurança aos quais esse destinatário pertence. Você não pode alterar informações de associação nesta página. Observe que o usuário pode atender aos critérios de um ou mais grupos dinâmicos de distribuição em sua organização. Contudo, os grupos dinâmicos de distribuição não são exibidos nessa página, pois sua associação é calculada sempre que eles são utilizados.

## Dica de Email

Use a seção **Dica de Email** para adicionar uma Dica de Email a fim de alertar os usuários de possíveis problemas se eles enviarem uma mensagem a este destinatário. Uma Dica de Email é o texto exibido na barra de informações quando esse destinatário é adicionado às caixas Para, Cc ou Cco de uma nova mensagem de email.


> [!TIP]
> As Dicas de Email podem incluir marcas HTML, mas scripts não são permitidos. O comprimento de uma dica de email personalizada não pode exceder 175 caracteres exibidos. Marcas HTML não são contadas no limite.



## Delegação da Caixa de Correio

Use a seção **Delegação da Caixa de Correio**, para atribuir permissões para outros usuários (também chamados de *representantes*), para que eles entrem na caixa de correio do usuário ou enviem mensagens em nome do usuário. É possível atribuir as seguintes permissões:

  - **Enviar como**   Essa permissão permite que usuários que não o proprietário da caixa de correio usem a caixa de correio para enviar mensagens. Depois de essa permissão ser atribuída a um representante, qualquer mensagem que um representante enviar desta caixa de correio irá parecer ter sido enviada pelo proprietário da caixa de correio. Entretanto, essa permissão não permite que um representante entre na caixa de correio do usuário.

  - **Enviar em nome de**   Essa permissão também permite que o representante use essa caixa de correio para enviar mensagens. No entanto, após essa permissão ser atribuída a um representante, o endereço **De:** , em qualquer mensagem enviada pelo representante, indicará que a mensagem foi enviada pelo representante em nome do proprietário da caixa de correio.

  - **Acesso total**   Essa permissão permite que um representante entre na caixa de correio de um usuário e veja o conteúdo da caixa de correio. Entretanto, depois de essa permissão ter sido atribuída a um representante, ele não poderá enviar mensagens da caixa de correio. Para permitir que o representante envie emails da caixa de correio do usuário, você ainda terá que atribuir a ele a permissão Enviar como ou Enviar em Nome de.

Para atribuir permissões a representantes, clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar") na permissão apropriada para exibir uma página que mostra uma lista de todos os destinatários na sua organização do Exchange que podem receber a permissão. Selecione os destinatários que deseja, adicione-os à lista e clique em **OK**. Você também pode pesquisar um destinatário específico, digitando seu nome na caixa de pesquisa e clicando em **Pesquisar**![Ícone Pesquisar](images/Dn750895.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif "Ícone Pesquisar").

## Usar o Shell para alterar as propriedades da caixa de correio do usuário

Use os cmdlets **Get-Mailbox** e **Set-Mailbox** para exibir e alterar as propriedades das caixas de correio dos usuários. Uma vantagem de se usar o Shell é a capacidade de alterar as propriedades para várias caixas de correio. Para informações sobre que parâmetros correspondem às propriedades de caixa de caixa de correio, consulte estes tópicos:

  - [Get-Mailbox](https://technet.microsoft.com/pt-br/library/bb123685\(v=exchg.150\))

  - [Set-Mailbox](https://technet.microsoft.com/pt-br/library/bb123981\(v=exchg.150\))

Eis alguns exemplos de como usar o Shell para alterar propriedades de caixas de correio de usuários.

Este exemplo mostra como encaminhar mensagens de email de Pat Coleman para a caixa de correio de Sunil Koduri (sunilk@contoso.com).

    Set-Mailbox -Identity patc -DeliverToMailboxAndForward $true -ForwardingAddress sunilk@contoso.com

Este exemplo usa o comando **Get-Mailbox** para localizar todas as caixas de correio na organização e, em seguida, usa o comando **Set-Mailbox** para configurar o limite de destinatários para 500 destinatários permitidos nas caixas Para:, Cc: e Cco: de uma mensagem de email.

    Get-Mailbox -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'UserMailbox')} | Set-Mailbox -RecipientLimits 500

Este exemplo usa o comando **Get-Mailbox** para localizar todas as caixas de correio na unidade organizacional Marketing e, em seguida, usa o comando **Set-Mailbox** para configurar essas caixas de correio. Os limites personalizados de avisos, proibição de envios e recebimentos estão definidos como 200 megabytes (MB), 250 MB e 280 MB, respectivamente, e os limites padrão de bancos de dados de caixa de correio são ignorados. Esse comando pode ser usado para configurar um conjunto específico de caixas de correio para que tenham limites maiores ou menores do que outras caixas de correio na organização.

    Get-Mailbox -OrganizationalUnit "Marketing" | Set-Mailbox -IssueWarningQuota 209715200 -ProhibitSendQuota 262144000 -ProhibitSendReceiveQuota 293601280 -UseDatabaseQuotaDefaults $false 

Este exemplo usa o cmdlet **Get-Mailbox** para localizar todos os usuários no departamento de Atendimento ao Cliente e, em seguida, usa o cmdlet **Set-Mailbox** para alterar o tamanho máximo de mensagens enviadas para 2 MB.

    Get-Mailbox -Filter "Department -eq 'Customer Service'" | Set-Mailbox -MaxSendSize 2097152

Este exemplo define a tradução da Dica de Email para francês e chinês.

    Set-Mailbox john@contoso.com -MailTipTranslations ("FR: C'est la langue française", "CHT: 這是漢語語言")

## Como saber se funcionou?

Para verificar se você alterou com êxito as propriedades da caixa de correio do usuário, faça o seguinte:

  - No EAC, selecione a caixa de correio e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição") para exibir a propriedade ou recurso que você alterou. Dependendo da propriedade que você tiver alterado, ela poderá ser exibida no painel Detalhes da caixa de correio selecionada.

  - No Shell, use o cmdlet **Get-Mailbox** para verificar as alterações. Uma vantagem de se usar o Shell é que você pode exibir múltiplas propriedades de várias caixas de correio. No exemplo acima, em que o limite de destinatários foi alterado, execute este comando para verificar o novo valor.
    
        Get-Mailbox -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'UserMailbox')} | fl Name,RecipientLimits
    
    Para o exemplo acima onde os limites da mensagem foram alterados, execute este comando.
    
        Get-Mailbox -OrganizationalUnit "Marketing" | fl Name,IssueWarningQuota,ProhibitSendQuota,ProhibitSendReceiveQuota,UseDatabaseQuotaDefaults

## Editar em massa as caixas de correio de usuários

Você também pode usar o EAC para alterar as propriedades de várias caixas de correio de usuários. Ao selecionar duas ou mais caixas de correio de usuários na lista de caixas de correio do EAC, as propriedades que podem ser editadas em massa são exibidas no painel Detalhes. Quando você alterar uma dessas propriedades, a alteração será aplicada a todas as caixas de correio selecionadas.

Eis uma lista de recursos e propriedades de caixa de correio de usuário que podem ser editadas em massa. Observe que nem todas as propriedades em cada área estão disponíveis para alteração.

  - **Informações de Contato**   Altere propriedades compartilhadas, como rua, código postal e nome da cidade.

  - **Organização**   Altere propriedades compartilhadas como nome do departamento, nome da empresa e o gerente a quem os usuários selecionados reportam.

  - **Atributos personalizáveis**   Altere ou adicione valores aos atributos personalizáveis 1 – 15.

  - **Cota da caixa de correio**   Altere os valores de cota da caixa de correio e o período de retenção de itens excluídos. Não está disponível no Exchange Online.

  - **Conectividade de email**   Habilite ou desabilite Outlook Web App, POP3, IMAP, MAPI e Exchange ActiveSync.

  - **Arquivo**   Habilite ou desabilite a caixa de correio do arquivo.

  - **Diretiva de retenção, diretiva de atribuição de funções e diretiva de compartilhamento**   Atualize as configurações para todos esses recursos de caixa de correio.

  - **Mover caixas de correio para outro banco de dados**   Mova as caixas de correio selecionadas para um banco de dados diferente.

  - **Delegar permissões**   Atribua permissões a usuários ou grupos para permitir que eles abram ou enviem mensagens a partir de outras caixas de correio. É possível atribuir permissões de Acesso Total, Enviar como e Enviar em nome de para usuários e grupos. Para obter mais detalhes, consulte [Gerenciar permissões para destinatários](manage-permissions-for-recipients-exchange-online-help.md).


> [!TIP]
> O tempo estimado para conclusão dessa tarefa é de 2 minutos, mas pode levar mais tempo se você alterar várias propriedades ou recursos.



## Usar o EAC para editar em massa as caixas de correio de usuários

1.  Na EAC, navegue até **Destinatários** \> **Caixas de correio**.

2.  Na lista de caixas de correio, selecione duas ou mais caixas de correio.
    

    > [!TIP]
    > Para selecionar várias caixas de correio adjacentes, mantenha a tecla Shift pressionada, clique na primeira caixa de correio e, em seguida, clique na última caixa de correio que você deseja editar. Você também pode selecionar várias caixas de correio que não estejam adjacentes, mantendo pressionada a tecla Ctrl e clicando em cada caixa de correio que desejar editar.



3.  No painel Detalhes, em **Editar em massa**, selecione as propriedades ou recursos de caixa de correio que deseja editar.

4.  Faça as alterações na página de propriedades e salve as alterações.

## Como saber se funcionou?

Para verificar se você editou em massa as caixas de correio de usuários com êxito, siga um destes procedimentos:

  - No EAC, selecione todas as caixas de correio que você editou em massa e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição") para exibir a propriedade ou recurso que você alterou.

  - No Shell de Gerenciamento do Exchange, use o cmdlet **Get-Mailbox** para verificar as alterações. Uma vantagem de se usar o Shell é que você pode exibir múltiplas propriedades de várias caixas de correio. Por exemplo, digamos que você tenha utilizado o recurso de edição em massa no EAC para habilitar a caixa de correio de arquivo e atribuir uma diretiva de retenção a todos os usuários de sua organização. Para verificar essas alterações, você poderia executar o seguinte comando:
    
        Get-Mailbox -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'UserMailbox')} | fl Name,ArchiveDatabase,RetentionPolicy
    
    Para obter mais informações sobre os parâmetros disponíveis para o cmdlet **Get-Mailbox**, consulte [Get-Mailbox](https://technet.microsoft.com/pt-br/library/bb123685\(v=exchg.150\)).

