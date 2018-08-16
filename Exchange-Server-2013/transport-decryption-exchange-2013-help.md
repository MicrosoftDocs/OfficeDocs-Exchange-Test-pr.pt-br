---
title: 'Descriptografia de transporte: Exchange 2013 Help'
TOCTitle: Descriptografia de transporte
ms:assetid: 4267c46d-f488-404d-a5cb-51f9127461c0
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd638122(v=EXCHG.150)
ms:contentKeyID: 50485458
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Descriptografia de transporte

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2015-04-07_

No Microsoft Exchange Server 2013, Microsoft Outlook 2010 e posterior e no Microsoft OfficeOutlook Web App, os usuários podem usar IRM (Gerenciamento de Direitos de Informação) para proteger suas mensagens. Você pode criar regras de proteção do Outlook para aplicar a proteção por IRM às mensagens antes que elas sejam enviadas de um cliente do Outlook 2010. Também é possível criar regras de proteção de transporte, para aplicar a proteção IRM a mensagens em trânsito que correspondam às condições da regra. A descriptografia de transporte permite o acesso ao conteúdo de mensagens protegidas por IRM para impor diretivas de mensagens.

Para tarefas de gerenciamento relacionadas ao gerenciamento de IRM, consulte [Procedimentos de gerenciamento de direitos de informação](information-rights-management-procedures-exchange-2013-help.md).

## Limitações de outras soluções de criptografia

Se for imprescindível para a sua organização proteger informações confidenciais, incluindo informações de alto impacto nos negócios e informações de identificação pessoal, considere a criptografia de mensagens de email e anexos. Soluções de criptografia de email como S/MIME já estão disponíveis há muito tempo. Essas soluções de criptografia já foram adotadas em vários níveis em organizações de tipos diferentes. No entanto, essas soluções apresentam os seguintes desafios:

  - **Incapacidade de aplicação de diretivas de mensagens** As organizações também têm que lidar com requisitos de conformidade que exigem a inspeção do conteúdo das mensagens para garantir que estejam de acordo com as diretivas de mensagens. No entanto, mensagens criptografadas com a maioria das soluções de criptografia baseadas no cliente, incluindo S/MIME, impedem a inspeção do conteúdo no servidor. Sem a inspeção de conteúdo, a organização não pode confirmar se todas as mensagens enviadas ou recebidas por seus usuários estão em conformidade com as diretivas de mensagens. Para estar em conformidade com uma regulamentação legal, por exemplo, você configurou uma regra de transporte que detecta informações de identificação pessoal, como o número de um CPF, e aplica automaticamente um aviso de isenção à mensagem. Se a mensagem for criptografada, o agente das Regras de Transporte no serviço de Transporte não poderá acessar o conteúdo da mensagem, e portanto não aplicará o aviso de isenção. Isso resulta em uma violação da diretiva.

  - **Menos segurança** O software antivírus não consegue verificar o conteúdo de mensagens criptografadas, expondo ainda mais a organização ao risco de conteúdo mal-intencionado, como vírus e worms. As mensagens criptografadas costumam ser consideradas confiáveis pela maioria dos usuários, o que aumenta ainda mais a probabilidade de que um vírus se espalhe pela organização. Por exemplo, você configurou uma regra de proteção do Outlook para aplicar automaticamente proteção por IRM a todas as mensagens enviadas para a lista de distribuição Todos os Funcionários com o modelo do RMS (serviço de gerenciamento de direitos) Confidencial da Empresa. A estação de trabalho de um usuário está infectada com um vírus que se propaga automaticamente usando Responder a Todos para responder às mensagens. Se a mensagem que leva o vírus estiver criptografada, o verificador de vírus não poderá verificar a mensagem.

  - **Impacto em agentes de transporte personalizados** Muitas organizações desenvolvem agentes de transporte personalizados para diferentes propósitos, como para atender a requisitos de processamento adicional para conformidade, segurança ou roteamento de mensagens personalizado. Os agentes de transporte personalizados desenvolvidos por uma organização para inspecionar ou modificar mensagens não são capazes de processar mensagens criptografadas. Se os agentes de transporte personalizados desenvolvidos por sua organização não puderem acessar o conteúdo das mensagens, a criptografia das mensagens pode impedir sua organização de cumprir os objetivos para os quais os agentes de transporte foram criados.

## Usando a descriptografia de transporte para conteúdo criptografado

No Exchange 2013, há recursos do IRM que lidam com esses desafios. Se as mensagens forem protegidas por IRM, a descriptografia de transporte permite que você as descriptografe em trânsito. Mensagens protegidas por IRM são descriptografadas pelo agente de Descriptografia, um agente de transporte focado na conformidade.


> [!NOTE]
> No Exchange 2013, o agente de descriptografia é um agente integrado. Agentes integrados não estão incluídos na lista de agentes retornados pelo cmdlet <STRONG>Get-TransportAgent</STRONG>. Para obter mais detalhes, consulte <A href="transport-agents-exchange-2013-help.md">Agentes de transporte</A>.



O agente de descriptografia descriptografa os seguintes tipos de mensagens protegidas por IRM:

  - Mensagens protegidas por IRM pelo usuário no Outlook Web App.

  - Mensagens protegidas por IRM pelo usuário no Outlook 2010.

  - Mensagens protegidas por IRM automaticamente pelas regras de proteção do Outlook no Exchange 2013 e no Outlook 2010.


> [!IMPORTANT]
> Apenas as mensagens protegidas pelo servidor AD RMS em sua organização são descriptografadas pelo agente de descriptografia.




> [!NOTE]
> As mensagens protegidas em trânsito usando regras de proteção de transporte não precisam ser descriptografadas pelo agente de descriptografia. O agente de descriptografia é acionado nos eventos de transporte <STRONG>OnEndOfData</STRONG> e <STRONG>OnSubmit</STRONG>. As regras de proteção de transporte são aplicadas pelo agente de Regras de Transporte, que aciona o evento <STRONG>OnRoutedMessage</STRONG>, e a proteção por IRM é aplicada pelo agente de criptografia no evento <STRONG>OnRoutedMessage</STRONG>. Para obter mais informações sobre agentes de transporte e uma lista de eventos SMTP nos quais eles podem ser registrados, consulte <A href="transport-agents-exchange-2013-help.md">Agentes de transporte</A>.



A descriptografia de transporte é realizada no primeiro serviço de Transporte do Exchange 2013 que lidar com uma mensagem em uma floresta do Active Directory. Se uma mensagem for transferida a um serviço de Transporte em outra floresta do Active Directory, a mensagem será descriptografada novamente. Após a descriptografia, o conteúdo descriptografado estará disponível a outros agentes de transporte no servidor. Por exemplo, o agente de Regras de Transporte em um serviço de Transporte pode inspecionar o conteúdo da mensagem e aplicar regras de transporte. Quaisquer ações especificadas na regra, como a aplicação de um aviso de isenção ou qualquer outro tipo de modificação da mensagem, pode ser realizada na mensagem sem criptografia. Os agentes de transporte de terceiros, como verificadores de vírus, podem verificar a mensagem em busca de vírus e malware. Depois que outros agentes de transporte tiverem inspecionado a mensagem e possivelmente realizado modificações, ela é criptografada novamente com os mesmos direitos de usuário que tinha antes de ser descriptografada pelo agente de descriptografia. A mesma mensagem não será descriptografada novamente por outro serviço de Transporte em outros servidores de Caixa de Correio da organização.

As mensagens descriptografadas pelo agente de Descriptografia não deixam o serviço de Transporte sem serem criptografadas novamente. Se um erro transitório for relatado durante a descriptografia ou a criptografia da mensagem, o serviço de Transporte tenta a operação novamente duas vezes. Após a terceira falha, o erro é tratado como um erro permanente. Se ocorrer um erro permanente, incluindo as situações em que erros transitórios são tratados como erros permanentes após as novas tentativas, o serviço de Transporte o tratará assim:

  - Se o erro permanente ocorrer durante a descriptografia, uma notificação de falha na entrega será enviada apenas se a descriptografia de transporte for definida como `Mandatory` e a mensagem criptografada for enviada com a notificação. Para obter mais detalhes sobre as opções de configuração disponíveis para a descriptografia de transporte, consulte Configuring Transport Decryption.

  - Se o erro permanente ocorrer durante a nova criptografia, uma notificação de falha na entrega sempre será enviada sem a mensagem descriptografada.


> [!IMPORTANT]
> Todos os agentes personalizados ou de terceiros que estejam instalados em um serviço de Transporte têm acesso à mensagem descriptografada. Você deve considerar o comportamento de tais agentes de transporte. Recomendamos a você testar intensamente os agentes de transporte de terceiros antes de implantá-los em um ambiente de produção.<BR>Depois que uma mensagem é descriptografada pelo agente de Descriptografia, se um agente de transporte criar uma nova mensagem e incorporar (anexar) a mensagem original à nova, apenas a mensagem nova será protegida. A mensagem original, que agora existe como um anexo à mensagem nova, não é criptografada novamente. Um destinatário que receba uma mensagem dessas pode abrir a mensagem anexada e realizar ações como encaminhar ou responder, o que ignora a aplicação dos direitos.



## Configurando a descriptografia de transporte

A descriptografia de transporte é configurada usando o cmdlet [Set-IRMConfiguration](https://technet.microsoft.com/pt-br/library/dd979792\(v=exchg.150\)) no Shell de Gerenciamento do Exchange. Porém, antes de configurar a descriptografia de transporte, você deve fornecer aos servidores do Exchange 2013 o direito de descriptografar conteúdo protegido por seu servidor AD RMS. Para isso, adicione a caixa de correio Federação ao grupo de super usuários configurado no cluster AD RMS em sua organização.


> [!IMPORTANT]
> Nas implantações do AD RMS entre florestas onde você tinha um cluster do AD RMS implantado em cada floresta, você deve adicionar a caixa de correio de Federação ao grupo superusuários no cluster do AD RMS em cada floresta para permitir que o serviço de transporte em um servidor de caixa de correio de Exchange 2013 ou um servidor de transporte de Hub Exchange 2010 para descriptografar as mensagens protegidas contra cada cluster do AD RMS.



Para detalhes, consulte [Adicionar a caixa de correio de Federação ao grupo de usuários do AD RMS Super](add-the-federation-mailbox-to-the-ad-rms-super-users-group-exchange-2013-help.md).

O Exchange 2013 permite duas configurações diferentes ao habilitar a descriptografia de transporte:

  - **Obrigatória**   Quando a descriptografia de transporte está configurada como `Mandatory`, o agente de descriptografia rejeita a mensagem e retorna uma notificação de falha na entrega ao remetente se um erro permanente for retornado ao descriptografar uma mensagem. Se sua organização não quiser que uma mensagem seja entregue caso não possa ser descriptografada com êxito e ações como a verificação por vírus e regras de transporte sejam aplicadas, escolha esta configuração.

  - **Opcional**   Quando a descriptografia de transporte está configurada como Opcional, o agente de descriptografia usa a abordagem do melhor esforço. As mensagens que podem ser descriptografadas são descriptografadas, mas as com erro permanente de descriptografia também são entregues. Se sua organização dá mais prioridade à entrega das mensagens do que às diretivas de mensagens, use esta configuração.

Para obter mais informações sobre a configuração da descriptografia de transporte, consulte [Habilitar ou desabilitar a descriptografia de transporte](enable-or-disable-transport-decryption-exchange-2013-help.md).

