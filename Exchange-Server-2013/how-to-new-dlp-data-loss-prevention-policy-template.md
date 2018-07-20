---
title: 'Criar uma política de DLP a partir de um modelo: Exchange 2013 Help'
TOCTitle: Criar uma política de DLP a partir de um modelo
ms:assetid: 4432ef8b-6108-48d3-b2af-43ef5b40d2bc
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ150515(v=EXCHG.150)
ms:contentKeyID: 50484693
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Criar uma política de DLP a partir de um modelo

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013_

_**Tópico modificado em:** 2015-01-14_

No Microsoft Exchange Server 2013, você pode usar modelos de diretiva de prevenção de perda de dados (DLP) para ajudá-lo a cumprir as necessidades de política e conformidade das mensagens em sua organização. Esses modelos contêm conjuntos pré-configurados de regras que podem ajudá-lo a gerenciar dados de mensagens que estiverem associados a vários requisitos jurídicos e regulatórios comuns. Para ver uma lista de todos os modelos fornecidos pela Microsoft, consulte [Modelos de política DLP fornecidos no Exchange](dlp-policy-templates-supplied-in-exchange-exchange-2013-help.md). Os modelos DLP de exemplo fornecidos podem ajudá-lo a gerenciar:

  - Dados do Ato Gramm-Leach-Bliley (GLBA)

  - Padrão de Segurança de Dados da Indústria de cartões de Pagamento (PCI-DSS)

  - Informações Pessoalmente Identificáveis nos Estados Unidos (U.S. PII)

Você pode personalizar qualquer um desses modelos de DLP ou utilizá-las como-é. Os modelos de política DLP são criados na parte superior de regras de transporte que incluem novas condições ou predicados e ações. Suportam a políticas de DLP da gama completa de regras de transporte tradicional, e você pode adicionar as regras adicionais após o estabelecimento de uma política de DLP. Para obter mais informações sobre modelos de política, consulte [Modelos de política de DLP](dlp-policy-templates-exchange-2013-help.md). Para saber mais sobre os recursos de regra de transporte, consulte [Regras de fluxo de emails ou de transporte](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md) (Exchange Server 2013 ) ou [Regras de fluxo de emails (regras de transporte) no Exchange Online](https://technet.microsoft.com/pt-br/library/jj919238\(v=exchg.150\)) (Exchange Online ). Depois de iniciar a aplicação de uma política, você pode aprender sobre como observar os resultados examinando os seguintes tópicos:

Exchange 2013: [Exibir relatórios de detecção de política DLP](view-dlp-policy-detection-reports-exchange-2013-help.md)

Exchange Online: [Exibir relatórios de detecção de política DLP](https://technet.microsoft.com/pt-br/library/dn904484\(v=exchg.150\))


> [!WARNING]
> Você deve habilitar as políticas de DLP no modo de teste antes de executá-las no seu ambiente de produção. Durante esses testes, recomenda-se que você configure caixas de correio de usuários de amostra e envie mensagens de teste que invoquem as políticas de teste para confirmar os resultados.



Para tarefas de gerenciamento adicionais relacionadas à criação de uma política de DLP a partir de um modelo, consulte [Procedimentos DLP](dlp-procedures-exchange-2013-help.md)Exchange Server 2013 ou [Procedimentos DLP](https://technet.microsoft.com/pt-br/library/jj938003\(v=exchg.150\))Exchange Online.

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 30 minutos

  - Certifique-se de que Exchange 2013 está configurado conforme descrito em [Planejamento e implantação](planning-and-deployment-for-exchange-2013-installation-instructions.md).

  - Configure as contas de administrador e de usuário dentro da sua organização e valide o fluxo básico de mensagem.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada \&quot;Prevenção de perda de dados (DLP)\&quot; no tópico [Permissões de política e conformidade de mensagens](messaging-policy-and-compliance-permissions-exchange-2013-help.md)

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## Usar o EAC para configurar uma política de DLP a partir de um modelo

1.  No EAC, navegue até **Gerenciamento de conformidade** \> **Prevenção de perda de dados** e clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar").
    

    > [!TIP]
    > Você também pode selecionar essa ação ao clicar na seta ao lado do ícone <STRONG>Adicionar</STRONG><IMG title="Ícone Adicionar" alt="Ícone Adicionar" src="images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif"> e selecionar <STRONG>Nova política de DLP a partir de modelo</STRONG> no menu suspenso.



2.  Na página **Criar uma nova política de DLP a partir de um modelo**, preencha os seguintes campos:
    
    1.  **Nome**   Adicionar um nome que irá distinguir essa política das outras.
    
    2.  **Descrição**   Adicionar uma descrição opcional que resuma esta política.
    
    3.  **Escolha um modelo**   Selecione o modelo apropriado para começar a criar uma nova diretiva.
    
    4.  **Mais opções**   Selecionar o modo ou o estado. A nova política não estará totalmente habilitada até que você especifique que ela deve estar. O modo padrão para uma política é teste sem notificações.
    
    5.  Clique em **Salvar** para terminar de criar a política.


> [!TIP]
> Além das regras em um modelo específico, a sua organização pode ter expectativas adicionais ou políticas da empresa que se apliquem a dados regulados dentro do seu ambiente de mensagens. O Exchange 2013 simplifica a alteração do modelo básico, para que você possa adicionar ações e fazer com que seu ambiente de mensagens do Exchange atenda os seus próprios requisitos.



Você pode modificar diretivas editando as regras nelas assim que a diretiva for salva no seu ambiente do Exchange 2013. Um exemplo de alteração de regra pode incluir isentar pessoas específicas de uma diretiva, ou mandar um aviso e bloquear o envio de uma mensagem se ela tiver conteúdo confidencial. Para obter mais informações sobre como editar diretivas e regras, consulte [Gerenciar políticas de DLP](manage-dlp-policies-exchange-2013-help.md).

Você deve navegar até o conjunto de regras da política específica na página **Editar política de DLP** e usar as ferramentas disponíveis nessa página para alterar uma política de DLP já criada no Exchange 2013.

Algumas diretivas permitem a adição de regras que invocam RMS para mensagens. Você precisa ter os RMS configurados no servidor do Exchange antes de adicionar as ações para fazer uso desses tipos de regras.

Em todas as políticas de DLP, você pode alterar as regras, ações, exceções, o período de aplicação ou se outras regras dentro da política serão ou não aplicadas. Você também pode adicionar suas próprias condições para cada uma.

## Para obter mais informações

[Prevenção de perda de dados](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)

[Modelos de política de DLP](dlp-policy-templates-exchange-2013-help.md)

