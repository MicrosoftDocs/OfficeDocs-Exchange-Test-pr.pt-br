---
title: 'Descoberta Eletrônica In-loco: Exchange Online Help'
TOCTitle: Descoberta Eletrônica In-loco
ms:assetid: 6377cb7a-3416-4e15-8571-c45d2160fc6f
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd298021(v=EXCHG.150)
ms:contentKeyID: 50485742
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Descoberta Eletrônica In-loco

 

_**Aplica-se a:**Exchange Online, Exchange Server 2013_

_**Tópico modificado em:**2017-01-17_


> [!TIP]
> Adiamos o prazo de 1º de julho de 2017 para criar novas pesquisas de Descoberta eletrônica In-loco no Exchange Online (em planos autônomos do Office 365 e do Exchange Online). No entanto, mais para o fim deste ano ou no início do próximo ano, não será possível criar novas pesquisas no Exchange Online. Para criar pesquisas de Descoberta Eletrônica, use a <A href="https://go.microsoft.com/fwlink/?linkid=847843">Pesquisa de Conteúdo</A> no Centro de Conformidade e Segurança doOffice 365. Após desativarmos as novas pesquisas de Descoberta Eletrônica In-loco, você ainda conseguirá modificar as pesquisas existentes. Além disso, a criação de novas pesquisas de Descoberta Eletrônica In-loco no Exchange Server 2013 e as implantações híbridas do Exchange continuam com suporte.



Se sua organização aderir aos requisitos de descoberta legal (relacionados à política organizacional, conformidade ou processos judiciais), a Descoberta Eletrônica In-loco no Microsoft Exchange Server 2013 e no Exchange Online pode ajudar você a realizar pesquisas de descoberta para conteúdo relevante nas caixas de correio. O Exchange 2013 e o Exchange Online também oferecem recursos de pesquisa federada e integração com o Microsoft SharePoint 2013 e o Microsoft SharePoint Online. Usando a Central de descoberta eletrônica no SharePoint, você pode pesquisar e reter todo o conteúdo relacionado a um caso, incluindo sites do SharePoint 2013 e do SharePoint Online, documentos, compartilhamentos de arquivos indexados pelo SharePoint (SharePoint 2013 apenas), conteúdo da caixa de correio no Exchange e conteúdo arquivado do Lync 2013. Você também pode usar a Descoberta Eletrônica In-Loco em um ambiente híbrido do Exchange para pesquisar caixas de correio locais ou baseadas em nuvem na mesma pesquisa.

**Sumário**

Como a Descoberta Eletrônica In-loco funciona

Pesquisa do Exchange

Grupo de função de Gerenciamento de Descoberta e funções de gerenciamento

Escopos de gerenciamento personalizado para Descoberta Eletrônica In-loco

Integração com o SharePoint Server 2013 e SharePoint Online

Descoberta eletrônica em uma implantação híbrida do Exchange

Caixas de correio de descoberta

Usar a Descoberta eletrônica In-loco

Estimar, visualizar e copiar resultados de pesquisa

Exportar resultados da pesquisa para um arquivo PST

Resultados diferentes da pesquisa

Registro em log para pesquisas de Descoberta Eletrônica In-loco

Descoberta Eletrônica In-loco e Retenção In-loco

Preservar as caixas de correio para a Descoberta Eletrônica In-loco

Limites e políticas de limitação da Descoberta Eletrônica In-loco

Documentação de Descoberta Eletrônica In-loco


> [!IMPORTANT]
> A Descoberta Eletrônica In-loco é um recurso poderoso que permite a um usuário com as permissões corretas, potencialmente ganhar acesso a todos os registros de mensagens armazenadas na organização do Exchange 2013 ou do Exchange Online . É importante controlar e monitorar as atividades de descoberta, incluindo a adição de membros ao grupo da função de Descoberta Eletrônica, a atribuição da função de gerenciamento da Pesquisa de Caixa de Correio e a atribuição da permissão de acesso da caixa de correio para descobrir caixas de correio.



## Como a Descoberta Eletrônica In-loco funciona

A Descoberta Eletrônica In-loco usa índices de conteúdo criados pela Pesquisa do Exchange. O Controle de Acesso Baseado em Função (RBAC) permite que o grupo de função [Gerenciamento de Descobertas](discovery-management-exchange-2013-help.md) delegue tarefas de descoberta a funcionários sem perfis técnicos, sem a necessidade de conceder privilégios elevados que possam permitir a um usuário realizar alterações operacionais na configuração do Exchange. O centro de administração do Exchange (EAC) fornece uma interface de pesquisa fácil de usar para pessoal não técnico tais como oficiais de conformidade e jurídicos, gerentes de registros e profissionais de recursos humanos (RH).

Usuários autorizados podem realizar uma pesquisa por Descoberta Eletrônica In-loco selecionando as caixas de correio e especificando os critérios de pesquisa, como palavras-chave, data de início e de término, endereços de remetentes e destinatários e tipos de mensagens. Após a pesquisa ser concluída, os usuários autorizados podem escolher uma das ações a seguir:

  - **Estimar os resultados da pesquisa**   Esta opção retorna uma estimativa do tamanho total e do número de itens que retornarão na pesquisa com base nos critérios que você especificou.

  - **Visualizar resultados de pesquisa**   Esta opção fornece visualização dos resultados. As mensagens retornadas de cada caixa de correio pesquisada são exibidas.

  - **Copiar os resultados da pesquisa**   Esta opção permite que você copie as mensagens para uma caixa de correio de descoberta.

  - **Exportar resultados da pesquisa**   Depois que os resultados da pesquisa são copiados para uma caixa de correio de descoberta, você poderá exportá-los para um arquivo PST.

![Estimar, visualizar, copiar e exportar os resultados da pesquisa](images/Dd298021.6356971a-34ed-4586-8229-030448d4fe2d(EXCHG.150).gif "Estimar, visualizar, copiar e exportar os resultados da pesquisa")

## Pesquisa do Exchange

A Descoberta Eletrônica In-loco usa índices de conteúdo criados pela pesquisa do Exchange. A Pesquisa do Exchange foi refeita para usar o Microsoft Search Foundation, uma plataforma robusta de pesquisa que vem com uma indexação e desempenho de consulta com melhorias significativas e funcionalidade de pesquisa aprimorada. Como o Microsoft Search Foundation também é usado por outros produtos do Office, incluindo o SharePoint 2013, ele oferece uma grande interoperabilidade e uma sintaxe semelhante para consulta para estes produtos.

Com um único mecanismo de indexação de conteúdo, não são usados recursos adicionais para rastrear e indexar bancos de dados de caixas de correio para a Descoberta Eletrônica In-loco quando as solicitações de Descoberta Eletrônica são recebidas pelos departamentos de TI.

A Descoberta Eletrônica In-loco usa Linguagem de Consulta por Palavra-Chave (KQL), uma sintaxe de consulta semelhante à Sintaxe de Consulta Avançada (AQS) usada pela Pesquisa Instantânea no Microsoft Outlook e no Outlook Web App. Usuários familiares com a KQL podem montar facilmente consultas de pesquisa poderosas para pesquisar índices de conteúdo.

Para obter mais informações sobre os formatos de arquivo indexados pela pesquisa do Exchange, consulte [Formatos de arquivo indexados pela pesquisa do Exchange](file-formats-indexed-by-exchange-search-exchange-2013-help.md).

## Grupo de função de Gerenciamento de Descoberta e funções de gerenciamento

Para que usuários autorizados realizem pesquisas de Descoberta Eletrônica In-loco, você deve adicioná-los ao grupo da função [Gerenciamento de Descobertas](discovery-management-exchange-2013-help.md) . Esse grupo de funções consiste em duas funções de gerenciamento: o [Função de pesquisa de caixa de correio](mailbox-search-role-exchange-2013-help.md), que permite que um usuário realize uma pesquisa de Descoberta Eletrônica In-loco, e o [Função de isenção legal](legal-hold-role-exchange-2013-help.md), que permite a um usuário colocar uma caixa de correio sob Bloqueio In-loco ou retenção de litígio.

Por padrão, as permissões para realizar tarefas relacionadas à Descoberta Eletrônica In-loco não são atribuídas a qualquer usuário ou administrador do Exchange. Os administradores do Exchange que forem membros do grupo de função de Gerenciamento da Organização podem adicionar usuários ao grupo de função de Gerenciamento de Descoberta e criar grupos de função personalizados para limitar o escopo de gerentes de descoberta a um subconjunto de usuários. Para saber mais sobre como adicionar usuários ao grupo da função de Gerenciamento de Descoberta, veja [Atribuir permissões de descoberta eletrônica no Exchange](assign-ediscovery-permissions-in-exchange-exchange-2013-help.md).


> [!IMPORTANT]
> Se um usuário não tiver sido adicionado ao grupo da função de Descoberta Eletrônica ou se não foi atribuído à função de Pesquisa de Caixa de Correio, uma interface de usuário de <STRONG>Descoberta Eletrônica In-loco &amp; Retenção</STRONG> não é exibida no EAC e os cmdlets de Descoberta Eletrônica In-loco não são disponibilizados no Shell de Gerenciamento do Exchange.



A auditoria de alterações de função RBAC, que está habilitada por padrão, garante que sejam mantidos registros adequados para rastrear a atribuição do grupo de função de Gerenciamento de Descoberta. Você pode usar o relatório de grupo de funções de administrador para pesquisar alterações feitas a grupos de funções de administrador. Para obter mais informações, consulte [Pesquisar as alterações do grupo de funções ou logs de auditoria do administrador](search-the-role-group-changes-or-administrator-audit-logs-exchange-2013-help.md).

Voltar ao início

## Escopos de gerenciamento personalizado para Descoberta Eletrônica In-loco

Você pode usar um escopo de gerenciamento personalizado para permitir que pessoas ou grupos específicos usem a Descoberta Eletrônica In-loco para pesquisar um subconjunto de caixas de correio em sua organização do Exchange 2013 ou do Exchange Online. Por exemplo, convém permitir que um gerente de descoberta pesquise apenas as caixas de correio de usuários em um local ou departamento específico. Faça isso criando um escopo de gerenciamento personalizado que usa um filtro de destinatário personalizado para controlar quais caixas de correio podem ser pesquisadas. Escopos de filtro de destinatário usam filtros para direcionar a destinatários específicos com base no tipo de destinatário ou em outras propriedades de destinatário.

Para a Descoberta In-loco, a única propriedade em uma caixa de correio de usuário de usuário que você pode usar para criar um filtro de destinatário para um escopo personalizado é a associação de grupo de distribuição. Se você usar outras propriedades, como *CustomAttributeN*, *Department* ou *PostalCode*, a pesquisa falhará quando for executada por um membro do grupo de função que recebeu o escopo personalizado. Para obter mais informações, consulte [Criar um escopo de gerenciamento personalizado para pesquisas de Descoberta Eletrônica In-loco](create-a-custom-management-scope-for-in-place-ediscovery-searches-exchange-2013-help.md).

## Integração com o SharePoint Server 2013 e SharePoint Online

Exchange 2013 e o Exchange Online oferece integração com o SharePoint 2013 e o SharePoint Online, permitindo que um gerenciador de descoberta use o Centro de Descoberta Eletrônica do SharePoint para realizar as seguintes tarefas:

  - **Pesquisar e preservar conteúdo a partir de um único local** Um gerente de descoberta autorizado pode pesquisar e preservar conteúdo tanto no SharePoint quanto no Exchange, incluindo conteúdo do Lync, como trocas de mensagens instantâneas e documentos de reunião compartilhados arquivados nas caixas de correio do Exchange.

  - **Gerenciamento de caso** O Centro de Descoberta Eletrônica usa uma abordagem de gerenciamento de caso para a Descoberta Eletrônica, permitindo que você crie casos e pesquise e preserve conteúdo em repositórios de conteúdo diferentes para cada caso.

  - **Exportar resultados de pesquisa** Um gerente de descoberta pode usar o Centro de Descoberta Eletrônica para exportar resultados de pesquisa. O conteúdo da caixa de correio incluído nos resultados da pesquisa é exportado para um arquivo PST.

O SharePoint também usa Microsoft Search Foundation para indexação e consulta de conteúdo. Independentemente do uso do EAC ou do Centro de Descoberta Eletrônica pelo gerente de descoberta para pesquisar por conteúdo do Exchange, o mesmo conteúdo de caixa de correio é retornado.

Nas implantaçoes locais, antes de usar o Centro de Descoberta Eletrônica no SharePoint para pesquisar as caixas de correio do Exchange , você deve estabelecer a confiança entre os dois aplicativos. No Exchange 2013 e no SharePoint 2013, isso é feito usando autenticação OAuth. Para detalhes, veja [Configurar o Exchange para o SharePoint eDiscovery Center](configure-exchange-for-sharepoint-ediscovery-center-exchange-2013-help.md). Pesquisas de Descoberta Eletrônica realizadas a partir do SharePoint são autorizadas pelo Exchange usando RBAC. Para que um usuário do SharePoint seja capaz de realizar uma pesquisa de Descoberta Eletrônica em caixas de correio do Exchange, ele precisa receber permissão delegada de Gerenciamento de Descoberta no Exchange. Para poder visualizar o conteúdo da caixa de correio retornado em uma pesquisa de Descoberta Eletrônica realizada com o uso do Centro de Descoberta Eletrônica do SharePoint , o gerenciador de descoberta deve possuir uma caixa de correio na mesma organização do Exchange .

Para obter instruções detalhadas de configuração do Centro de Descoberta Eletrônica em uma organização do Office 365, veja o artigo [Configurar um Centro de Descoberta Eletrônica no SharePoint Online](http://go.microsoft.com/fwlink/p/?linkid=331600).

## Descoberta eletrônica em uma implantação híbrida do Exchange

Para executar pesquisas entre locais da Descoberta eletrônica com êxito em uma organização híbrida do Exchange 2013, será necessário configurar a autenticação OAuth (Autorização Aberta) entre suas organizações locais do Exchange e organizações do Exchange Online, de forma que você possa usar a Descoberta eletrônica local para pesquisar em caixas de correio locais e baseadas em nuvem. A autenticação OAuth é um protocolo de autenticação de servidor para servidor que permite que aplicativos autentiquem uns aos outros.

A autenticação OAuth oferece suporte aos seguintes cenários de Descoberta eletrônica em uma implantação híbrida do Exchange:

  - Pesquisa de caixas de correio locais que usam o Arquivamento do Exchange Online para caixas de correio de arquivamento baseadas em nuvem.

  - Pesquisa de caixas de correio locais e baseadas em nuvem na mesma pesquisa de Descoberta eletrônica.

  - Pesquisa de caixas de correio locais usando a Central de Descoberta Eletrônica no SharePoint Online.

Para obter mais informações sobre os cenários de Descoberta eletrônica que exigem que a autenticação OAuth seja configurada em um ambiente híbrido do Exchange, consulte [Usando a autenticação OAuth para suportar a Descoberta Eletrônica em uma implantação híbrida do Exchange](using-oauth-authentication-to-support-ediscovery-in-an-exchange-hybrid-deployment-exchange-2013-help.md). Para obter instruções detalhadas sobre a configuração da autenticação OAuth a fim de oferecer suporte à Descoberta eletrônica, consulte [Configurar a autenticação OAuth entre organizações do Exchange e do Exchange Online](configure-oauth-authentication-between-exchange-and-exchange-online-organizations-exchange-2013-help.md).

## Caixas de correio de descoberta

Após criar uma pesquisa de Descoberta Eletrônica In-loco, você pode copiar os resultados da pesquisa para uma caixa de correio de destino. O EAC permite que você selecione uma caixa de correio de descoberta como a caixa de correio de destino. Uma caixa de correio de descoberta é um tipo especial de caixa de correio que fornece as seguintes funcionalidades:

  - **Seleção segura e mais fácil de caixa de correio de destino**   Ao usar o EAC para copiar os resultados da pesquisa de Descoberta Eletrônica In-loco, somente caixas de correio de descoberta são disponibilizadas como repositórios para armazenamento dos resultados de pesquisa. Você não precisa vasculhar uma lista potencialmente grande de caixas de correio disponíveis na organização. Isto também elimina a possibilidade de uma descoberta eletrônica acidentalmente selecionar outra caixa de correio de usuário ou uma caixa de correio não segura para armazenar mensagens poteciamente confidenciais.

  - **Ampla cota de armazenamento de caixa de correio**   A caixa de correio de destino deve ser capaz de armazenar uma grande quantidade de dados de mensagens que podem ser retornados por uma pesquisa de Descoberta Eletrônica In-loco. Por padrão, as caixas de correio de descoberta têm uma cota de armazenamento de 50 gigabytes (GB). Essa cota de armazenamento não pode ser aumentada.

  - **Mais segura por padrão**   Assim como todos os tipos de caixas de correio, uma caixa de correio de descoberta tem uma conta de usuário do Active Directory associada. Porém, essa conta é desabilitada por padrão. Apenas usuários explicitamente autorizados a acessar uma caixa de correio de descoberta terão acesso a ela. São atribuídas aos membros do grupo de função Gerenciamento de Descoberta permissões de Acesso Total à caixa de correio de descoberta padrão. Quaisquer caixas de correio de descoberta adicionais que você criar não terão suas permissões de acesso a caixa de correio atribuídas a nenhum usuário.

  - **Entrega de email desabilitada**   Apesar de estar visível nas listas de endereço no Exchange, os usuários não podem enviar email para uma caixa de correio de descoberta. A entrega de email às caixas de correio de descoberta é proibida por meio de restrições de entrega. Isso preserva a integridade dos resultados de pesquisa copiados para uma caixa de correio de descoberta.

O programa de instalação do Exchange 2013 cria uma caixa de correio de descoberta com nome de exibição **Caixa de Correio de Pesquisa de Descoberta**. Você pode usar o Shell para criar caixas de correio de descoberta adicionais. Por padrão, as caixas de correio de descoberta que você cria não terão nenhuma permissão de acesso atribuída à caixa de correio. Você pode atribuir permissões de Acesso Total a um gerente de descoberta para acessar mensagens copiadas a uma caixa de correio de descoberta. Para detalhes, consulte [Criar uma caixa de correio de descoberta](create-a-discovery-mailbox-exchange-2013-help.md).

A Descoberta Eletrônica In-loco também usa uma caixa de correio do sistema com o nome de exibição **SystemMailbox{e0dc1c29-89c3-4034-b678-e6c29d823ed9}** para reter metadados de Descoberta Eletrônica In-loco. As caixas de correio do sistema não estão visíveis no EAC ou nas listas de endereço do Exchange . Nas organizações locais, antes de remover um banco de dados da caixa de correio onde a caixa de correio do sistema de Descoberta Eletrônica In-loco está localizada, você deve mover a caixa de correio para outro banco de dados da caixa de correio. Se a caixa de correio for removida ou corrompida, os seus gerentes de descoberta não poderão realizar as pesquisas de Descoberta Eletrônica até que você crie a caixa de correio novamente. Para obter detalhes, consulte [Recriar a caixa de correio do sistema de descoberta](re-create-the-discovery-system-mailbox-exchange-2013-help.md).

Voltar ao início

## Usar a Descoberta eletrônica In-loco

Usuários que tenham sido adicionados ao grupo de funções de Gerenciamento de Descoberta podem realizar pesquisas de Descoberta Eletrônica In-loco. Você pode realizar uma pesquisa usando a interface baseada em web do EAC. Isso facilita para os usuários sem perfil técnico, como gerentes de registros, responsáveis pela conformidade ou profissionais jurídicos ou de RH, a utilização da Descoberta Eletrônica In-loco. Você também pode usar o Shell para realizar uma pesquisa. Para obter mais informações, consulte [Criar uma pesquisa de Descoberta Eletrônica In-loco](create-an-in-place-ediscovery-search-exchange-2013-help.md)


> [!TIP]
> Nas organizações locais, você pode usar a Descoberta Eletrônica In-loco para pesquisar caixas de correio localizadas nos servidores de Caixa de Correio do Exchange 2013 . Para pesquisar caixas de correio localizadas nos servidores de Caixa de Correio do Exchange 2010, use a Pesquisa de Várias Caixas de Correio em um servidor do Exchange 2010.<BR>Em um ambiente híbrido, um ambiente onde algumas caixas de correio existem em seus servidores de Caixa de Correio no local e algumas caixas de correio existem em uma organização baseada em nuvem, você pode realizar pesquisas de Descoberta Eletrônica In-loco em suas caixas de correio baseadas em nuvem usando o EAC na sua organização local. Se você pretende copiar mensagens para uma caixa de correio descoberta, você deve selecionar uma caixa de correio descoberta local. As mensagens de caixas de correio baseadas em nuvem que são retornadas nos resultados de pesquisa são copiadas para a caixa de correio descoberta local especificada. Para saber mais sobre implantações híbridas, consulte <A href="https://technet.microsoft.com/pt-br/library/jj200581(v=exchg.150)">Implantações Híbridas do Exchange Server</A>.



O assistente de **Retenção & Descoberta Eletrônica In-loco** no EAC permite que você crie uma pesquisa de Descoberta Eletrônica In-loco e também use a Retenção In-loco para colocar resultados de pesquisa em retenção. Quando você cria uma pesquisa de Descoberta Eletrônica In-loco, um objeto de pesquisa é criado na caixa de correio de sistema da Descoberta Eletrônica In-loco. Esse objeto podem ser manipulado para iniciar, interromper, modificar e remover a pesquisa. Após criar a pesquisa, você pode obter uma estimativa dos resultados da pesquisa, o que inclui estatísticas de palavras-chave que o ajudam a determinar a eficácia da consulta. Você também pode fazer uma visualização imediata dos itens retornados na pesquisa, o que permite visualizar o conteúdo da mensagem, o número de mensagens retornados para cada caixa de correio de origem e o número total de mensagens. Você pode usar essas informações para aperfeiçoar ainda mais sua consulta, se necessário.

Quando estiver satisfeito com os resultados da pesquisa, você poderá copiá-las para uma caixa de correio de descoberta. Você também pode usar o EAC ou o Outlook para exportar uma caixa de correio de descoberta ou uma parte do seu conteúdo para um arquivo PST.

Ao criar uma pesquisa de Descoberta Eletrônica In-loco, você deve especificar os seguintes parâmetros:

  - **Nome**   O nome da pesquisa é usado para identificar a pesquisa. Quando você copia resultados de pesquisa para uma caixa de correio de descoberta, uma pasta é criada na caixa de correio de descoberta usando o nome da pesquisa e o carimbo de data/hora para identificar de maneira única os resultados de pesquisa em uma caixa de correio de descoberta.

  - **Caixas de correio**   Você pode escolher pesquisar todas as caixas de correio na sua organização do Exchange 2013 ou do Exchange Online, ou especificar as caixas de correio a serem pesquisadas. As caixas de correio principal e de arquivo morto do usuário são incluídas na pesquisa. Se também quiser usar a mesma pesquisa para colocar itens em retenção, é necessário especificar as caixas de correio. Você pode especificar um grupo de distribuição para incluir usuários de caixa de correio que sejam membros daquele grupo. A associação ao grupo é calculada uma vez quando a pesquisa é criada, e alterações subsequentes na associação ao grupo não são refletidas automaticamente na pesquisa.
    
    No Exchange Online, você também pode especificar grupos do Office 365 como uma fonte de conteúdo para que a caixa de correio do grupo seja pesquisada (ou colocada em retenção). Ao adicionar um grupo do Office 365 a uma pesquisa de Descoberta Eletrônica In-loco, somente a caixa de correio do grupo é pesquisada. As caixas de correio dos membros do grupo não são pesquisadas.

  - **Consulta da pesquisa**   Você pode incluir todo o conteúdo da caixa de correio das caixas de correio especificadsa ou usar uma consulta de pesquisa para retornar os itens que são mais relevantes para o caso da investigação. Você pode especificar os seguintes parâmetros em uma consulta de pesquisa:
    
      - **Palavras-chave**   Você pode especificar palavras-chave e frases para pesquisar o conteúdo da mensagem. Você também pode usar os operadores lógicos **AND**, **OR** e **NOT**. Além disso, o Exchange 2013 também suporta o operador **PERTO** , permitindo que você pesquise por uma palavra ou frase que está perto de outra palavra ou frase.
        
        Para pesquisar por uma correspondência exata de um frase com várias palavras, você deve colocar a frase entre aspas. A pesquisa pela frase "plano e competição", por exemplo, retorna mensagens que contenham correspondências exatas à frase, enquanto a pesquisa por **plano AND competição** retorna mensagens que contenham as palavras **plano** e **competição** em qualquer lugar da mensagem.
        
        O Exchange 2013 também oferece suporte à sintaxe Linguagem de Consulta por Palavra-Chave (KQL) para pesquisas de Descoberta Eletrônica In-loco.
        

        > [!TIP]
        > A Descoberta Eletrônica In-loco não oferece suporte a expressões regulares.

        
        Operadores lógicos como **AND** e **OR** devem ser escritos em maiúsculas para serem tratados como operadores e não como palavras-chave. É recomendável explicitar os parênteses para qualquer consulta que misture diversos operadores lógicos, para evitar erros ou interpretações falhas. Por exemplo, para pesquisar por mensagens que contenham PalavraA ou PalavraB E a PalavraC ou a PalavraD, use **(PalavraA OR PalavraB) AND (PalavraC OR PalavraD)**.
    
      - **Datas de início e de término**   Por padrão, a Descoberta Eletrônica In-loco não limita as pesquisas por intervalo de datas. Para pesquisar em mensagens enviadas em um intervalo de datas específico, restrinja a pesquisa especificando as datas de início e término. Se você não especificar uma data de término, a pesquisa retornará os resultados mais recentes cada vez que você reiniciá-la.
    
      - **Remetentes e destinatários**   Para filtrar a pesquisa, você pode especificar os remetentes e os destinatários das mensagens. Você pode usar endereços de email, nomes para exibição ou o nome de um domínio para pesquisar itens que todas as pessoas no domínio enviaram ou receberam. Por exemplo, para localizar um email enviado ou recebido por qualquer pessoa na Contoso Ltd., especifique **@contoso.com** no campo **De** ou **Para/Cc** no EAC. Você também pode especificar **@contoso.com** nos parâmetros *Senders* ou *Recipients* no Shell.
    
      - **Tipos de mensagem**   Por padrão, todos os tipos de mensagem são pesquisadas. Você pode restringir a pesquisa selecionando tipos específicos de mensagens, como emails, contatos, documentos, diário, reuniões, notas e conteúdo do Lync.

A captura de tela a seguir mostra um exemplo de uma consulta de pesquisa no EAC.

![Configure a Consulta de Pesquisa de Descoberta Eletrônica](images/Dd298021.a3626569-8700-421e-8b4e-7ec520b28272(EXCHG.150).png "Configure a Consulta de Pesquisa de Descoberta Eletrônica")

Ao usar a Descoberta Eletrônica In-loco, considere também o seguinte:

  - **Anexos**   Os anexos das pesquisas de Descoberta In-loco In-Place eDiscovery suportados pela pesquisa do Exchange. Para obter detalhes, consulte [Formatos de arquivo indexados pela pesquisa do Exchange](file-formats-indexed-by-exchange-search-exchange-2013-help.md). Nas implantações locais, você pode adicionar mais tipos de arquivo instalando filtros de instalação (também conhecidos como iFilter) para o tipo de arquivo nos servidores de Caixa de Correio.

  - **Itens não pesquisáveis**   Itens não pesquisáveis como itens de caixa de correio que não podem ser indexados pela Pesquisa do Exchange. As razões pelas quais eles não podem ser indexados incluem a falta de um filtro de pesquisa instalado para um arquivo anexado, um erro do filtro e mensagens criptografadas. Para realizar uma pesquisa de Descoberta Eletrônica In-loco com êxito, pode ser necessário que sua organização inclua esses itens para revisão. Ao copiar resultados da pesquisa para uma caixa de correio de descoberta ou ao exportá-los para um arquivo PST, você poderá incluir itens não pesquisáveis. Para obter mais informações, consulte [Itens não pesquisáveis na descoberta eletrônica do Exchange](unsearchable-items-in-exchange-ediscovery-exchange-2013-help.md).

  - **Itens criptografados**   Como as mensagens criptografaads usando S/MIME não sõ indexadas pela Pesquisa do Exchange, a Descobeta Eletrônica In-loco não pesquisa estas mensagens. Se você selecionar a opção de incluir itens não pesquisáveis nos resultados da pesquisa, essas mensagens criptografadas com S/MIME serão copiadas para a caixa de correio de descoberta.

  - **Itens protegidos por IRM**   As mensagens protegidas usando o Gerenciamento de Direitos de Informações (IRM) são indexadas pela Pesquisa do Exchange e portanto incluídas nos resultdos da pesquisa se elas conseguirem uma correspondência com os parâmetros de consulta. As mensagens devem ser protegidas usando um cluster de Serviços de Gerenciamento de Direitos Active Directory (AD RMS) na mesma floresta Active Directory que o servidor de Caixa de Correio. Para mais informações, consulte [Gerenciamento de Direitos de Informação](information-rights-management-exchange-2013-help.md).
    

    > [!IMPORTANT]
    > Quando a Pesquisa do Exchange falha ao indexar uma mensagem protegida por IRM, devido a uma falha na criptografia ou porque a IRM está desabilitada, a mensagem desprotegida não é adicionada à lista de itens com falha. Se você selecionar a opção de incluir itens não pesquisáveis nos resultados de pesquisa, os resultados podem não incluir mensagens protegidas por IRM que não puderam ser descriptografadas.<BR>Para incluir mensagens protegidas por IRM em uma pesquisa, você pode criar outra pesquisa que inclua mensagens com anexos .rpmsg. Você pode usar a sequência de caracteres de consulta <CODE>attachment:rpmsg</CODE> para pesquisar todas as mensagens protegidas por IRM nas caixas de correio especificadas, quer tenham sido indexadas com êxito ou não. Isso pode resultar na duplicação de resultados de pesquisa em situações nas quais uma pesquisa retorna mensagens que correspondam ao critério de pesquisa, incluindo mensagens protegidas por IRM que tenham sido indexadas com êxito. A pesquisa não retorna mensagens protegidas por IRM que não foram indexadas.<BR>A realização de uma segunda pesquisa para todas as mensagens protegidas por IRM também inclui mensagens protegidas por IRM que foram indexadas e retornadas com êxito na primeira pesquisa. Além disso, as mensagens protegidas por IRM retornadas pela segunda pesquisa podem não corresponder a critérios de pesquisa, como as palavras-chave, usados na primeira pesquisa.



  - **Desfazer duplicação**   Ao copiar os resultados da pesquisa para uma caixa de correio de descobeta, você pode habilitar a opção *desfazer duplicação* dos resultados da pesquisa para copiar apenas uma instância de uma única mensagem para a caixa de correio de descoberta. A eliminação de duplicação tem os seguintes benefícios:
    
      - Menor necessidade de armazenamento e menor tamanho de caixa de correio de descoberta devido ao menor número de mensagens copiadas.
    
      - Redução da carga de trabalho dos gerentes de descoberta, assessores jurídicos ou outros envolvidos na revisão dos resultados da pesquisa.
    
      - Redução do custo de Descoberta Eletrônica, dependendo do número de itens duplicados excluídos dos resultados da pesquisa.

Voltar ao início

## Estimar, visualizar e copiar resultados de pesquisa

Após a finalização de uma pesquisa de Descoberta Eletrônica In-Loco, você pode exibir as estimativas do resultado da pesquisa no painel de Detalhes no EAC. A estimativa inclui o número de itens retornados e o tamanho total desses itens. Você também pode visualizar estatísticas de palavras-chave que exibem detalhes sobre o número de itens retornados por cada palavra-chave utilizada na consulta de pesquisa. Esta informação é útil para determinar a eficiência da consulta. Se a consulta for abrangente demais, ela irá retornar um conjunto de dados muito maior, o que pode exigir mais recursos para revisão e aumentar os custos da Descoberta Eletrônica. Se a consulta for restrita demais, ela pode reduzir significativamente o número de registros retornados ou não retornar registro nenhum. Você pode usar as estimativas e as estatísticas de palavra-chave para aperfeiçoar a consulta e atender seus requisitos.


> [!TIP]
> No Exchange 2013, as estatísticas de palavra-chave também incluem estatísticas para propriedades que não são palavras-chave, como datas, tipos de mensagens e remetentes/destinatários especificados na consulta de pesquisa.



Você pode também visualizar os resultados de pesquisa para garantir que as mensagens retornadas contém o conteúdo que você está procurando e ajustar a consulta se necessário. A Visualização da Pesquisa de Descoberta Eletrônica exibe o número de mensagens retornadas de cada caixa de correio pesquisada e o número total de mensagens retornadas para pesquisa. A visualização é gerada rapidamente, sem exigir que você copie as mensagens para uma caixa de correio de descoberta.

Após você estar satisfeito com a quantidade e a qualidade dos resultados da pesquisa, você pode copiá-los para uma caixa de correio de descoberta. Ao copiar mensagens, você tem as seguintes opções:

  - **Incluir itens não pesquisáveis**   Para detalhes sobre os tipos de itens que são considerados não pesquisáveis, veja as considerações da pesquisa da Descoberta Eletrônica na seção anterior.

  - **Habilitar desfazer duplicação**   Desfazer duplicação reduz o conjunto de dados incluindo somente uma única instânica de um único registro se várias instâncias forem encontradas em uma ou mais caixas de correio pesquisadas.

  - **Permitir registro completo em log**   Por padrão, apenas o registro básico em log está habilitado ao copiar os itens. Você pode selecionar o log completo para incluir informações sobre todos os registros retornados pela pesquisa.

  - **Envie-me um email quando a cópia estiver finalizada**   Uma pesquisa de Descoberta Eletrônica In-loco pode potencialmente retornar um grande número de registros. Copiar as mensagens retornadas para uma caixa de correio de descoberta pode levar muito tempo. Use essa opção para obter uma notificação de email quando o processo de cópia for concluído. Para acesso facilitado usando o Outlook Web App, a notificação inclui um link para o local na caixa de correio de descoberta em que as mensagens foram copiadas.

Para obter mais informações, consulte [Copiar os resultados de pesquisa de descoberta eletrônica para uma caixa de correio de descoberta](copy-ediscovery-search-results-to-a-discovery-mailbox-exchange-2013-help.md).

Voltar ao início

## Exportar resultados da pesquisa para um arquivo PST

Depois que os resultados da pesquisa são copiados para uma caixa de correio de descoberta, você poderá exportá-los para um arquivo PST.

![Exportar resultados de pesquisa de Descoberta Eletrônica para um arquivo PST](images/Dd298021.4ddca8af-1af5-4cb2-852c-e3a292099a58(EXCHG.150).gif "Exportar resultados de pesquisa de Descoberta Eletrônica para um arquivo PST")

Após os resultados da pesquisa serem exportados para um arquivo PST, você ou outros usuários podem abri-los no Outlook para analisar ou imprimir mensagens retornadas nos resultados da pesquisa. Para obter mais informações, consulte [Exportar resultados de pesquisa de Descoberta Eletrônica para um arquivo PST](export-ediscovery-search-results-to-a-pst-file-exchange-2013-help.md).

## Resultados diferentes da pesquisa

Como a Descoberta Eletrônica In-Loco realiza pesquisas em dados dinâmicos, é possível que duas pesquisas das mesmas fontes de conteúdo e usando a mesma consulta para pesquisa retornem resultados diferentes. Os resultados estimados da pesquisa também podem ser diferentes dos resultados reais da pesquisa que são copiados para uma caixa de correio de descoberta. Isto pode ocorrer mesmo ao executar novamente a mesma pesquisa num espaço pequeno de tempo. Existem vários fatores que podem afetar a consistência dos resultados da pesquisa;

  - A indexação contínua de email de entrada porque a Pesquisa do Exchange rastreia e faz a indexação continuamente do pipeline de transporte e dos bancos de dados da caixa de correio da sua organização.

  - Exclusão de email por usuários ou porcessos automáticos.

  - Importação em massa de grandes quantidades de email, o que leva tempo para indexação.

Se você experimentar resultados diferentes para a mesma pesquisa, considere colocar as caixas de correio em espera para preservar o conteúdo, executar pesquisas durante horários que não sejam de pico e permita o tempo necessário para indexação após a importação de grandes quantidades de email.

## Registro em log para pesquisas de Descoberta Eletrônica In-loco

Há dois tipos de log disponíveis para pesquisas de Descoberta Eletrônica In-loco:

  - **Registro básico em log**   O registro básico em log é habiltiado por padrão para todas as pesquisas de Descoberta Eletrônica In-loco. Ele inclui informações sobre a pesquisa e sobre quem a realizou. As informações capturadas pelo log básico são exibidas no corpo da mensagem de email que é enviada à caixa de correio onde os resultados da pesquisa são armazenados. A mensagem está localizada na pasta criada para armazenar os resultados da pesquisa.

  - **Registro completo em log**   O registro completo em log inclui informações sobre todas as mensagens retornadas pela pesquisa. Essas informações são fornecidas em um arquivo de valores separados por vírgulas (.csv) anexado à mensagem de email que contém as informações do log básico. O nome da pesquisa é usado no nome do arquivo .csv. Essa informação pode ser necessária para fins de manutenção de registros ou conformidade. Para habilitar o log completo, você deve selecionar a opção **Habilitar log completo** ao copiar os resultados da pesquisa para uma caixa de correio de descoberta no EAC. Se você está usando o Shell, especifique a opção registro completo em log usando o parâmetro *LogLevel* .


> [!TIP]
> Ao usar o Shell para criar ou modificar uma pesquisa de Descoberta Eletrônica In-loco, você também pode desabilitar o log.



Além do log da pesquisa incluído quando você copia os resultados da pesquisa para uma caixa de correio de descoberta, o Exchange também registra os cmdlets usados pelo EAC ou pelo Shell para criar, modificar ou remover as pesquisas de Descoberta Eletrônica in-loco. Esta informação é registrada nas entradas de log de auditoria do administrador. Para obter detalhes, consulte [Log de auditoria de administrador](administrator-audit-logging-exchange-2013-help.md).

Voltar ao início

## Descoberta Eletrônica In-loco e Retenção In-loco

Como parte das solicitações de Descoberta Eletrônica, você pode ter que preservar o conteúdo de caixas de correio até uma investigação ou ação legal seja concluída. Mensagens excluídas ou alteradas pelo usuário da caixa de correio ou por qualquer processo também devem ser preservadas. No Exchange 2013, isso é feito usando a Retenção In-loco. Para detalhes, consulte [Retenção local e Retenção de litígio](in-place-hold-and-litigation-hold-exchange-2013-help.md).

No Exchange 2013, você pode usar o novo assistente de **Descoberta Eletrônica In-loco & Retenção** para pesquisar os itens e preservá-los enquanto eles forem necessários para a Descoberta Eletrônica ou para atender a outros requisitos de negócio. Ao usar a mesma pesquisa tanto para a Descoberta Eletrônica In-loco quanto para a Retenção In-loco, esteja ciente do seguinte:

  - Você não pode usar a opção para pesquisar todas as caixas de correio. Você deve selecionar as caixas de correio ou grupos de distribuição.

  - Você não pode remover a pesquisa de Descoberta Eletrônica In-loco se a pesquisa também estiver sendo usada para Bloqueio Local. Você precisa desabilitar a opção de Retenção In-loco de uma pesquisa antes de poder removê-la.

## Preservar as caixas de correio para a Descoberta Eletrônica In-loco

Quando um funcionário deixa uma organização, é uma prática comum desabilitar ou remover a caixa de correio. Após desabilitar uma caixa de correio, ela é desconectada da conta de usuário mas permanece na caixa de correio por um período determinado - por padrão, 30 dias. O Assistente de Pasta Gerenciada não processa caixas de correio desconectadas, e nenhuma diretiva de retenção é aplicada durante esse período. Você não pode pesquisar o conteúdo da pesquisa de uma caixa de correio desconectada. Ao final do período de retenção de caixa de correio excluída configurado no banco de dados de caixas de correio, a caixa é removida do banco de dados.


> [!IMPORTANT]
> No Exchange Online, a Descoberta Eletrônica In-loco pode procurar conteúdo em caixas de correio inativas. Caixas de correio inativas são caixas de correio colocadas sob Bloqueio Local ou retenção de litígio e depois removidas. Caixas de correio inativas são preservadas se forem mantidas retidas. Quando uma caixa de correio inativa é removida de um Bloqueio Local ou quando a retenção de litígio é desabilitada, ela é permanentemente excluída. Para obter detalhes, consulte <A href="https://technet.microsoft.com/pt-br/library/dn144876(v=exchg.150)">Gerenciar as caixas de correio inativas no Exchange Online</A>.



Nas implantações locais, se a sua organização exigir que as configurações de retenção sejam aplicadas às mensagens de funcionários que não está mais na organização ou se você precisa reter a caixa de correio de um ex-funcionário para uma pesquisa de Descoberta Eletrônica em andamento ou futura, não desabilite ou remova a caixa de correio. Você pode seguir as etapas a seguir para garantir que a caixa de correio não pode ser acessada e nenhuma nova mensagem será entregue para a mesma.

1.  Desabilite a conta do usuário Active Directory usando **Active Directory Users & Computers** ou outro Active Directory ou ferramentas ou scripts de configuração de conta. Isso impede o logon na caixa de correio usando a conta de usuário associada.
    

    > [!IMPORTANT]
    > Usuários com permissão de Acesso Total à caixa de correio ainda conseguirão acessar a caixa de correio. Para evitar que outras pessoas acessem a caixa de correio, é necessário remover a permissão de Acesso Total delas. Para informações sobre como remover as permissões da caixa de correio para Acesso Total em uma caixa de correio, veja <A href="manage-permissions-for-recipients-exchange-online-help.md">Gerenciar permissões para destinatários</A>.



2.  Defina o limite de tamanho de mensagem para mensagens que podem ser enviadas ou recebidas pelo usuário da caixa de correio para um valor muito baixo, por exemplo, 1KB. Isso impede a entrega de novas mensagens de e para a caixa de correio. Para obter detalhes, consulte [Configurar os limites de tamanho de mensagens de uma caixa de correio](configure-message-size-limits-for-a-mailbox-exchange-2013-help.md).

3.  Configurar restrições de entrega para a caixa de correio para que ninguém possa enviar mensagens para ela. Para obter detalhes, consulte [Configurar restrições de entrega de mensagens para uma caixa de correio](configure-message-delivery-restrictions-for-a-mailbox-exchange-2013-help.md).


> [!IMPORTANT]
> É necessário realizar as etapas acima em conjunto com qualquer outro processo de gerenciamento de conta exigido pela sua organização, mas sem desabilitar ou remover a caixa de correio ou remover a conta de usuário associada.



Quando estiver planejando implementar retenção de caixa de correio para gerenciamento de retenção de mensagens (MRM) ou Descoberta Eletrônica In-loco, é necessário levar em conta a rotatividade dos funcionários. Retenção a longo prazo de caixas de correio de ex-funcionários irá exigir armazenamento adicional nos servidores de Caixa de Correio e também resultar em um aumento no banco de dados do Active Directory porque exige que a conta de usuário associada seja mantida para a mesma duração Além disso, pode exigir também alterações nos processos de gerenciamento e de provisionamento da conta de sua organização.

Voltar ao início

## Limites e políticas de limitação da Descoberta Eletrônica In-loco

No Exchange 2013 e no Exchange Online os recursos que a Descoberta Eletrônica In-Loco consomem são controlados usando políticas de limitação.

A diretiva padrão de limitação contém os seguintes parâmetros.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Parâmetro</th>
<th>Descrição</th>
<th>Valor padrão</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>DiscoveryMaxConcurrency</p></td>
<td><p>O número máximo de pesquisas de Descoberta Eletrônica In-loco que podem ser executados ao mesmo tempo em sua organização.</p></td>
<td><p>2</p>

> [!TIP]
> Se uma pesquisa de Descoberta Eletrônica for iniciada enquanto duas pesquisas anteriores ainda estiverem sendo executadas, a terceira pesquisa não será enfileirada e falhará. Você precisa esperar até que uma das pesquisas anteriores termine antes de iniciar uma nova pesquisa.


</td>
</tr>
<tr class="even">
<td><p>DiscoveryMaxMailboxes</p></td>
<td><p>Número máximom de caixas de correio que podem ser pesquisadas em uma única pesquisa de Descoberta Eletrônica In-Loco.</p></td>
<td><p>Exchange Online: 10,0001</p>
<p>Exchange 2013: 5,000</p></td>
</tr>
<tr class="odd">
<td><p>DiscoveryMaxStatsSearchMailboxes</p></td>
<td><p>O número máximo de caixas de correio que podem ser pesquisadas em uma única pesquisa de Descoberta Eletrônica In-loco que ainda permita exibir estatísticas de palavra-chave.</p></td>
<td><p>100</p>

> [!TIP]
> Depois de executar uma estimativa de pesquisa de Descoberta Eletrônica, você pode exibir estatísticas de palavra-chave. Essas estatísticas também podem exibir detalhes sobre o número de itens retornados por cada palavra-chave utilizada na consulta de pesquisa. Se mais de 100 caixas de correio de origem forem incluídas na pesquisa, um erro será retornado se você tentar exibir estatísticas de palavra-chave.


</td>
</tr>
<tr class="even">
<td><p>DiscoveryMaxKeywords</p></td>
<td><p>Número máximo de palavras-chave que podem ser especificadas em uma única pesquisa de Descoberta Eletrônica In-Loco.</p></td>
<td><p>500</p></td>
</tr>
<tr class="odd">
<td><p>DiscoveryMaxSearchResultsPageSize</p></td>
<td><p>Número máximo de itens exibidos em uma única página ao visualizar os resultados de pesquisa de Descoberta Eletrônica In-Loco.</p></td>
<td><p>200</p></td>
</tr>
<tr class="even">
<td><p>DiscoverySearchTimeoutPeriod</p></td>
<td><p>Número máximo de minutos que uma pesquisa de Descoberta Eletrônica In-Loco será executada antes de atingir o tempo limite.</p></td>
<td><p>10 minutos</p></td>
</tr>
</tbody>
</table>



> [!TIP]
> 1&nbsp;&nbsp;&nbsp;Se iniciar uma pesquisa de Descoberta Eletrônica no Centro de Descoberta Eletrônica do SharePoint Online em uma organização do Office 365, você pode pesquisar no máximo 1.500 caixas de correio em uma única pesquisa.



No Exchange Server 2013, você pode alterar os valores padrões para estes parâmetros para adequação às suas necessidades ou criar políticas de limitação adicionais e atribui-las aos usuários com permissão delegada de Gerenciamento de Descoberta. No Exchange Online, os valores padrões para estes parâmetros de limitação não podem ser alterados.

## Documentação de Descoberta Eletrônica In-loco

A tabela a seguir contém links para tópicos que o ajudarão a gerenciar e a saber mais sobre Descoberta Eletrônica In-loco


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Tópico</th>
<th>Descrição</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="assign-ediscovery-permissions-in-exchange-exchange-2013-help.md">Atribuir permissões de descoberta eletrônica no Exchange</a></p></td>
<td><p>Aprenda como conceder acesso a um usuário para usar a Descoberta Eletrônica In-loco no EAC a fim de pesquisar caixas de correio do Exchange. Adicionar um usuário ao grupo de funções de Gerenciamento de Descobertas também permite que a pessoa use o Centro de Descoberta Eletrônica no SharePoint 2013 e no SharePoint Online para pesquisar caixas de correio do Exchange.</p></td>
</tr>
<tr class="even">
<td><p><a href="create-a-discovery-mailbox-exchange-2013-help.md">Criar uma caixa de correio de descoberta</a></p></td>
<td><p>Aprenda como usar o Shell para criar uma caixa de correio de descoberta e atribuir permissões de acesso.</p></td>
</tr>
<tr class="odd">
<td><p><a href="create-an-in-place-ediscovery-search-exchange-2013-help.md">Criar uma pesquisa de Descoberta Eletrônica In-loco</a></p></td>
<td><p>Aprenda como criar uma pesquisa de Descoberta Eletrônica In-loco e como estimar e visualizar os resultados da pesquisa de Descoberta Eletrônica.</p></td>
</tr>
<tr class="even">
<td><p><a href="http://go.microsoft.com/fwlink/p/?linkid=506799">Propriedades da Mensagem e operadores de pesquisa para Descoberta Eletrônica In-loco</a></p></td>
<td><p>Saiba quais propriedades de mensagem de email podem ser pesquisadas usando a Descoberta eletrônica In-loco. O tópico fornece exemplos de sintaxe para cada propriedade, informações sobre operadores de busca, como <strong>E</strong> e <strong>OU</strong> e informações sobre outras técnicas de consulta de pesquisa usando aspas duplas (&quot; &quot;) e prefixos curinga.</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/pt-br/library/dn798915(v=exchg.150)">Limites de descoberta eletrônica In-loco de pesquisa no Exchange Online</a></p></td>
<td><p>Conheça os limites da Descoberta Eletrônica In-loco no Exchange Online que ajudam a manter a integridade e a qualidade dos serviços de Descoberta Eletrônica para organizações do Office 365.</p></td>
</tr>
<tr class="even">
<td><p><a href="start-or-stop-an-in-place-ediscovery-search-exchange-2013-help.md">Iniciar ou parar uma pesquisa de descoberta eletrônica In-loco</a></p></td>
<td><p>Aprenda como iniciar, interromper e reiniciar pesquisas de Descoberta Eletrônica.</p></td>
</tr>
<tr class="odd">
<td><p><a href="modify-an-in-place-ediscovery-search-exchange-2013-help.md">Modificar uma pesquisa de descoberta eletrônica In-loco</a></p></td>
<td><p>Aprenda como modificar uma pesquisa de Descoberta Eletrônica existente.</p></td>
</tr>
<tr class="even">
<td><p><a href="copy-ediscovery-search-results-to-a-discovery-mailbox-exchange-2013-help.md">Copiar os resultados de pesquisa de descoberta eletrônica para uma caixa de correio de descoberta</a></p></td>
<td><p>Aprenda como copiar os resultados de uma pesquisa de Descoberta Eletrônica para uma caixa de correio de descoberta.</p></td>
</tr>
<tr class="odd">
<td><p><a href="export-ediscovery-search-results-to-a-pst-file-exchange-2013-help.md">Exportar resultados de pesquisa de Descoberta Eletrônica para um arquivo PST</a></p></td>
<td><p>Aprenda como exportar os resultados de uma pesquisa de Descoberta Eletrônica para um arquivo PST.</p></td>
</tr>
<tr class="even">
<td><p><a href="create-a-custom-management-scope-for-in-place-ediscovery-searches-exchange-2013-help.md">Criar um escopo de gerenciamento personalizado para pesquisas de Descoberta Eletrônica In-loco</a></p></td>
<td><p>Saiba como usar os escopos de gerenciamento personalizados para limitar as caixas de correio que um gerente de descoberta pode pesquisar.</p></td>
</tr>
<tr class="odd">
<td><p><a href="remove-an-in-place-ediscovery-search-exchange-2013-help.md">Remover uma pesquisa de descoberta eletrônica In-loco</a></p></td>
<td><p>Aprenda como excluir uma pesquisa de Descoberta Eletrônica.</p></td>
</tr>
<tr class="even">
<td><p><a href="search-for-and-delete-messages-admin-help-exchange-2013-help.md">Pesquisar e excluir mensagens - ajuda de Admin</a></p></td>
<td><p>Aprenda a usar o cmdlet <strong>Search-Mailbox</strong> para pesquisar e excluir mensagens de email.</p></td>
</tr>
<tr class="odd">
<td><p><a href="reduce-the-size-of-a-discovery-mailbox-in-exchange-exchange-2013-help.md">Reduzir o tamanho de uma caixa de correio de descoberta no Exchange</a></p></td>
<td><p>Use este processo para reduzir o tamanho de uma caixa de correio de descoberta com tamanho maior do que 50 GB.</p></td>
</tr>
<tr class="even">
<td><p><a href="delete-and-re-create-the-default-discovery-mailbox-in-exchange-exchange-2013-help.md">Excluir e recriar a caixa de correio de descoberta padrão no Exchange</a></p></td>
<td><p>Aprenda como excluir, recriar e reatribuir permissões à caixa de correio de descoberta padrão. Use este procedimento se esta caixa de correio tiver excedido o limite de 50 GB e você não precisar dos resultados da pesquisa.</p></td>
</tr>
<tr class="odd">
<td><p><a href="re-create-the-discovery-system-mailbox-exchange-2013-help.md">Recriar a caixa de correio do sistema de descoberta</a></p></td>
<td><p>Aprenda como recriar a caixa de correio do sistema de descoberta. Esta tarefa é aplicável apenas a organizações Exchange 2013.</p></td>
</tr>
<tr class="even">
<td><p><a href="using-oauth-authentication-to-support-ediscovery-in-an-exchange-hybrid-deployment-exchange-2013-help.md">Usando a autenticação OAuth para suportar a Descoberta Eletrônica em uma implantação híbrida do Exchange</a></p></td>
<td><p>Aprenda sobre os cenários de Descoberta Eletrônica em uma implantação híbrida do Exchange que necessitam que você configure a autenticação OAuth.</p></td>
</tr>
<tr class="odd">
<td><p><a href="configure-exchange-for-sharepoint-ediscovery-center-exchange-2013-help.md">Configurar o Exchange para o SharePoint eDiscovery Center</a></p></td>
<td><p>Aprenda como configurar o Exchange 2013 para que você possa usar o Centro de Descoberta Eletrônica no SharePoint 2013 para pesquisar caixas de correio do Exchange.</p></td>
</tr>
<tr class="even">
<td><p><a href="unsearchable-items-in-exchange-ediscovery-exchange-2013-help.md">Itens não pesquisáveis na descoberta eletrônica do Exchange</a></p></td>
<td><p>Aprenda sobre itens da caixa de correio que não podem ser indexados pela Pesquisa do Exchange e são retornados em resultados de pesquisa de Descoberta Eletrônica como itens que não podem ser pesquisados.</p></td>
</tr>
</tbody>
</table>


Para saber mais sobre Descoberta Eletrônica no Office 365, no Exchange 2013, no SharePoint 2013 e no Lync 2013, confira as [Perguntas frequentes sobre Descoberta Eletrônica](http://go.microsoft.com/fwlink/p/?linkid=386633).

Voltar ao início

