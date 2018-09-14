---
title: 'Gerenciar uma política de caixa de correio de UM: Exchange 2013 Help'
TOCTitle: Gerenciar uma política de caixa de correio de Unificação de mensagens
ms:assetid: 704b001c-3e6f-4ed5-bbe5-42a778f6ac0d
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Aa998829(v=EXCHG.150)
ms:contentKeyID: 50556222
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.Servers.UnifiedMessaging.UMMailboxPolicyGeneralTab
ms.translationtype: MT
---

# Gerenciar uma política de caixa de correio de Unificação de mensagens

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2013-02-22_

Após ter criado uma diretiva de caixa de correio de Unificação de Mensagens (UM), é possível visualizar ou definir diversas configurações. Por exemplo, é possível configurar recursos de UM, como Visualização de Mensagens de Voz ou Tocar no Telefone e outras opções relacionadas à segurança, como Mensagem de Voz Protegida e configurações de política de PIN.

Para conhecer tarefas de gerenciamento adicionais relacionadas a políticas de caixa de correio de UM, consulte [Procedimentos de diretiva de caixa de correio de Unificação de mensagens](https://docs.microsoft.com/pt-br/exchange/voice-mail-unified-messaging/set-up-voice-mail/um-mailbox-policy-procedures).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 5 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Diretivas de caixa de correio da UM" no tópico [Permissões de mensagens unificadas](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de executar esses procedimentos, confirme se um plano de discagem da UM foi criado. Para obter etapas detalhadas, consulte [Criar um plano de discagem de UM](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de executar esses procedimentos, confirme se um plano de discagem da UM foi criado. Para obter etapas detalhadas, consulte [Criar uma política de caixa de correio da UM](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Usar o EAC para gerenciar uma política de caixa de correio de UM

1.  No EAC, navegue até **Unificação de Mensagens** \> **Planos de discagem de UM**. Na exibição de lista, selecione o plano de discagem de UM que você deseja alterar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

2.  Na página **Plano de discagem de UM**, em **Políticas de Caixa de Correio de UM**, na barra de ferramentas, clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").
    
      - Use **Geral** para visualizar e definir as configurações de uma política de caixa de correio de UM. Por exemplo, você pode visualizar os planos de discagem associados à diretiva de caixa de correio de UM ou desabilitar notificações de chamadas não atendidas para usuários que estão associados a uma diretiva de caixa de correio de UM específica. Ao modificar as configurações em uma diretiva de caixa de correio de UM, elas são aplicadas a todos os usuários que estão associados à diretiva de caixa de correio de UM. Você pode exibir ou configurar o seguinte:
        
          - **Plano de discagem de UM**   Exibe o nome do plano de discagem associado à política de caixa de correio de UM. Este é o nome do plano de discagem exibido no Shell.
            
            Quando uma nova diretiva de caixa de correio do UM for criada, ela deverá ser associada a um plano de discagem. Depois que a diretiva de caixa de correio de UM for criada e associada a um plano de discagem, as configurações definidas na diretiva de caixa de correio serão aplicadas aos usuários associados ao plano de discagem. Por padrão, quando você cria um plano de discagem de UM, também é criada uma diretiva de caixa de correio de UM.
        
          - **Nome**   Digite o nome do plano de discagem. O nome plano de discagem da UM é obrigatório e deve ser exclusivo. Porém, ele é utilizado apenas para exibição no EAC e no Shell. Se você tiver de alterar o nome para exibição do plano de discagem criado, deverá primeiramente excluir o plano de discagem do UM existente e criar outro plano de discagem com o nome apropriado. Se sua organização usar vários planos de discagem do UM, é recomendável a utilização de nomes significativos para seus planos de discagem do UM. O comprimento máximo de nome de plano de discagem de UM é 64 caracteres e pode incluir espaços. (Se estiver integrando com o Microsoft Communications Server 2007 R2 ou o Microsoft Lync Server, não se recomenda usar espaços.) Entretanto, não pode incluir nenhum dos seguintes caracteres: " / \\ \[ \] : ; | = , + \* ? \< \>.
        
          - **Limite de saudações pessoais (minutos)**   Use essa caixa de texto para inserir o número máximo de minutos que os usuários associados à política de caixa de correio de UM podem usar ao gravar a saudação da caixa postal. Você pode modificar essa configuração depois que a diretiva de caixa de correio do UM for criada. Somente caracteres numéricos são permitidos. O intervalo válido para a saudação é de 1 a 10 minutos. A configuração padrão é 5 minutos.
        
          - **Permitir visualização de caixa postal**   Marque ou desmarque esta caixa de seleção para habilitar ou desabilitar o recurso Visualização de caixa postal de usuários associados à política de caixa de correio de UM. Habilitar essa configuração permite que usuários recebam o texto de uma mensagem de caixa postal no corpo da mensagem de um email ou mensagem de texto. A configuração padrão é habilitado.
        
          - **Permitir que usuários configurem as regras de atendimento de chamadas**   Marque essa caixa de seleção para permitir que os usuários associados à diretiva de caixa de correio de UM criem as regras de atendimento de chamadas. Se esta opção for desabilitada para o plano de discagem da UM, o recurso não estará disponível para usuários habilitados para UM associados à diretiva de caixa de correio da UM. A configuração padrão é habilitado.
        
          - **Permitir indicador de espera de mensagem**   Marque ou desmarque esta caixa de seleção para habilitar ou desabilitar o Indicador de Espera de Mensagem de usuários associados à política de caixa de correio de UM. Indicador de Espera da Mensagem é um recurso encontrado na maioria dos sistemas de caixa postal legados. Na sua forma mais comum, acende uma luz no telefone do usuário da caixa postal para indicar a presença de uma nova mensagem de voz. O Indicador de Espera de Mensagem também pode enviar uma mensagem de texto ao telefone celular de um usuário habilitado para UM. A configuração padrão é habilitado.
        
          - **Permitir Outlook Voice Access**   Marque ou desmarque esta caixa de seleção para habilitar ou desabilitar o Outlook Voice Access para usuários habilitados para UM associados à política de caixa de correio de UM. O Outlook Voice Access é um recurso usado para usuários habilitados para UM para acessar a caixa de correio pelo telefone. Por padrão, essa configuração está habilitada.
        
          - **Permitir notificações de chamadas não atendidas**   Marque ou desmarque esta caixa de seleção para habilitar ou desabilitar notificações de chamadas não atendidas de usuários associados à política de caixa de correio de UM. Uma notificação de chamada não atendida é uma mensagem de email enviada para uma caixa de correio de usuário quando este não atende a uma chamada de entrada. Essa é uma mensagem de email diferente da que contém a mensagem de voz que é deixada para um usuário.
            

            > [!TIP]
            > Quando você integra a Unificação de Mensagens e o Lyns Server local, as notificações de chamada perdida não são disponibilizadas para usuários que posseum uma caixa postal localizada em um servidor se Caixa de Correio do Exchange 2007 ou Exchange 2010. Uma notificação de chamada perdida é gerada quando um usuário se desconecta antes da chamada ser enviada para a Unificação de Mensagens.

            
            Geralmente, quando um usuário não atende a uma chamada de entrada, ele recebe duas mensagens de email: uma mensagem que contém a mensagem de voz e uma mensagem de notificação de chamada não atendida. Por padrão, as notificações de chamadas não atendidas são habilitadas quando uma diretiva de caixa de correio do UM é criada.
        
          - **Permitir Tocar no Telefone para caixa postal**   Marque ou desmarque esta caixa de seleção para habilitar ou desabilitar o recurso Tocar no Telefone de usuários associados à política de caixa de correio de UM. Esta opção é habilitada por padrão e permite que usuários reproduzam as mensagens de voz no telefone, incluindo um telefone de escritório ou celular.
        
          - **Permitir fax de entrada**   Marque ou desmarque esta caixa de seleção para habilitar ou desabilitar fax de entrada de usuários associados à política de caixa de correio de UM. Por padrão, quando você habilita usuários para a UM, a caixa de correio deles consegue receber faxes. Contudo, se essa opção estiver desabilitada no plano de discagem de UM, os usuários habilitados para UM associados à política de caixa de correio de UM não poderão receber faxes. A configuração padrão na política de caixa de correio da UM está desabilitada.
            
            Depois de habilitar a definição **Permitir fax de entrada**, você precisará especificar o URI do servidor de fax de parceiro. Se a política de caixa de correio de UM for vinculada ao plano de discagem de UM que pode ussar TCP e TLS, você precisará inserir as URIs para TCP e TLS.
        
          - **Ajude a Microsoft a melhorar a visualização da caixa postal**   Essas opções permitem que a Microsoft aprimorem a qualidade da Visualização de Caixa Postal. É possível habilitar as seguintes configurações:
            
              - **Permitir análise de mensagens de voz deixadas por chamadores**   Use esta opção para ajudar a melhorar a qualidade da visualização da caixa postal em versões futuras do Microsoft Exchange, encaminhando cópias das mensagens de voz para a Microsoft para análise. Não é possível definir esta opção se todas as mensagens de voz estão protegidas.
            
              - **Dizer aos chamadores que as mensagens de voz podem ser analisadas**   Use esta opção para dizer aos chamadores que as mensagens deixadas por eles podem ser analisadas pela Microsoft para melhorar a qualidade da Visualização de Caixa Postal e permitir que eles cancelem.
    
      - 
        
        Use **Texto da Mensagem** para definir as configurações de texto da mensagem para os usuários associados a uma política de caixa de entrada de UM. Por exemplo, é possível especificar o texto do email enviado aos usuários após a redefinição do PIN de UM. Você pode configurar o seguinte:
        
          - **Quando um usuário está habilitado para Unificação de Mensagens**   O texto digitado nessa caixa aparece no email enviado aos usuários, quando estes estão habilitados para UM. Quando a caixa de correio de um destinatário é habilitada para UM e eles são habilitados para caixa postal, um email de boas-vindas à Unificação de Mensagens é enviado ao usuário. A caixa de texto está limitada a 512 caracteres e pode conter formatação HTML simples. Por padrão, nenhum texto é definido nessa caixa de texto.
            
            Essa mensagem contém um texto de boas-vindas e as informações de PIN que o usuário utilizará para acessar o sistema de UM ou caixa postal. O texto digitado nessa caixa de texto é incluído no final da mensagem de boas-vindas. Você pode usar essa caixa de texto para incluir informações, como números de telefone do suporte técnico de caixa postal ou números do Outlook Voice Access.
            
            Se não for inserido texto nesta caixa de texto, o texto padrão gerado pela UM ou pelo sistema de caixa postal será incluído na mensagem de email.
            
            O texto fornecido na caixa de texto pode ser sem formatação. Ele também pode conter marcas simples de formatação HTML se você desejar enfatizar o texto ou adicionar hiperlinks para outro conteúdo.
            
            **Exemplo 1:**    Se você tiver dúvidas ou sugestões sobre o serviço de caixa postal, ligue para o help desk no ramal 4200.
            
            **Exemplo 2:**    Se você tiver perguntas ou sugestões sobre o \<b\>serviço de caixa posta\</b\>, ligue para o help desk no ramal 4200 ou acesse nosso site em \<a href=”http://emp.contoso.com/itinfo/vmail”\>\</a\>.
        
          - **Quando um PIN do Outlook Voice Access do usuário é redefinido**   O texto inserido nessa caixa de texto é incluído na mensagem de email enviada a usuários habilitados para UM quando seu PIN de UM é redefinido.
            
            Um PIN será redefinido pela UM ou pelo sistema de caixa postal se o número de tentativas com falha de logon for maior do que 10 (por padrão) ou se os usuários redefinirem o PIN por meio dos recursos da UM incluídos no Microsoft Outlook, Outlook Web App ou Outlook Voice Access a partir de um telefone. Você pode usar essa caixa de texto para incluir no email informações como avisos de segurança e outras informações relacionadas à segurança.
            
            Se não for inserido texto nesta caixa de texto, o texto padrão gerado pelo sistema de UM será incluído na mensagem de email.
            
            A caixa de texto está limitada a 512 caracteres. Por padrão, nenhum texto é definido nessa caixa de texto.
            
            O texto fornecido na caixa de texto pode ser sem formatação. Ele também pode conter marcas simples de formatação HTML se você desejar enfatizar o texto ou adicionar hiperlinks para outro conteúdo.
        
          - **Quando um usuário recebe uma mensagem de voz**   O texto digitado nessa caixa de texto é incluído na mensagem de email enviada aos usuários quando estes recebem uma mensagem de voz de um chamador de entrada. Por exemplo, o texto pode incluir avisos de isenção de responsabilidade que contenham informações sobre o encaminhamento de mensagens de voz ou políticas de segurança do sistema que descrevam o modo correto de lidar com mensagens de voz na organização.
            
            Se não for inserido texto nesta caixa de texto, o texto padrão gerado pelo sistema será incluído na mensagem de email. A caixa de texto está limitada a 512 caracteres. Por padrão, nenhum texto é definido nessa caixa de texto.
            
            O texto fornecido na caixa de texto pode ser sem formatação. Ele também pode conter marcas simples de formatação HTML se você desejar enfatizar o texto ou adicionar hiperlinks para outro conteúdo.
        
          - **Quando um usuário recebe uma mensagem de fax**   O texto digitado nessa caixa de texto é incluído na mensagem de email enviada aos usuários quando estes recebem uma mensagem de fax na Caixa de Entrada. Você pode usar essa caixa de texto para incluir avisos de isenção de responsabilidade que contenham informações sobre o encaminhamento de mensagens de fax ou outras diretivas de segurança do sistema sobre a maneira correta de lidar com mensagens de fax na organização.
            
            Se não for inserido texto nesta caixa de texto, o texto padrão gerado pelo sistema será incluído na mensagem de email. A caixa de texto está limitada a 512 caracteres. Por padrão, nenhum texto é definido nessa caixa de texto.
    
      - 
        
        Use **Políticas de PIN** para definir as configurações de PIN dos usuários associados a uma política de caixa de entrada de UM. Os PINs de UM permitem que os usuários acessem suas Caixas de Entrada usando o telefone. Ao definir as configurações nesta página, você pode especificar o número mínimo de dígitos para um PIN de UM ou o número de tentativas com falha de logon antes da caixa de correio de UM dos usuários ser bloqueada.
        
        Verifique se você planejou cuidadosamente as diretivas de PIN do UM implementadas em seu ambiente. Se não planejar e implementar as diretivas de PIN de UM apropriadas, você poderá introduzir ameaças de segurança e permitir equivocadamente acesso não autorizado à sua rede. Você pode configurar o seguinte:
        
          - **Comprimento mínimo do PIN (dígitos)**   Use essa caixa de texto para especificar o número mínimo de dígitos que o PIN de um usuário de UM pode conter. A configuração padrão é de seis dígitos. O intervalo é de 4 a 24 dígitos numéricos. Essa configuração não pode ser desabilitada.
            
            O aumento do número de dígitos exigidos para um PIN melhora o nível de segurança do sistema de UM. A redução do número de dígitos exigidos para um PIN piora o nível de segurança da rede. Quanto menos dígitos forem necessários em um PIN, mais fácil será para um possível invasor descobrir o PIN do usuário.
            
            Se essa configuração for muito alta, os usuários poderão ter problemas para se lembrar de seus PINs. No entanto, se a configuração for muito baixa, você correrá o risco de permitir inadvertidamente acesso não autorizado ao sistema de UM.
        
          - **Contagem de reciclagem de PIN**   Use essa configuração para definir o número de PINs exclusivos que os usuários devem usar antes de poder reutilizar um PIN antigo. Para a maioria das organizações, esse valor deve ser definido como 5 - o número de PINs que o sistema memorizará. O histórico de PINs pode ser desabilitado.
            
            Você pode definir esse valor como um número entre 1 e 20. Definir um valor muito alto pode frustrar os usuários, pois eles podem ter dificuldade para memorizar muitos PINs. Definir um valor muito baixo pode gerar uma ameaça de segurança para a rede.
        
          - **Permitir padrões de PIN comuns**   Use essa configuração para definir requisitos de complexidade de PIN para a UM. Esses requisitos são aplicados em alterações de PIN ou quando novos PINs são criados.
            
            Se essa opção estiver desabilitada, os números seqüenciais e repetidos e o sufixo do ramal de caixa de correio serão rejeitados. Se essa opção estiver habilitada, somente o sufixo do ramal de caixa de correio será rejeitado.
            
            Como prática recomendada de segurança, desabilite essa definição. Se essa definição estiver desabilitada, os PINs de usuário não poderão conter o seguinte:
            
            Números seqüenciais, como 123456 ou 456789.
            
            Números repetidos, como 111111 ou 8888888.
            
            Sufixo do ramal de caixa de correio.
        
          - **Impor tempo de vida do PIN (dias)**   Use essa caixa de texto para configurar o número de dias até a expiração do PIN do usuário habilitado para UM. Após o vencimento do PIN, o usuário deve criar um novo PIN do UM. Para a maioria das organizações, esse valor deve ser definido como o padrão de 60 dias.
            
            O valor dessa configuração pode ser entre 0 e 999. Se esse valor for definido como 0, os PINs nunca expirarão. Definir um valor muito baixo pode frustrar os usuários, pois eles serão solicitados a criar e memorizar novos PINs com muita freqüência.
        
          - **Número de falhas de entrada antes da redefinição do PIN**   Use essa caixa de texto para inserir o número de tentativas sequenciais de logon com falha ou malsucedidas que podem ocorrer antes de o sistema de UM redefinir automaticamente o PIN de um usuário. Para a maioria das organizações, esse valor deve ser definido para o padrão de 5 tentativas.
            
            O valor dessa configuração pode ser entre 0 e 999. Se você definir essa configuração como 0, ela será desabilitada, e o sistema não redefinirá automaticamente os PINs dos usuários. Definir um valor muito baixo pode frustrar os usuários; definir um valor muito alto dá aos usuários mal-intencionados maiores chances de determinar o PIN.
            
            Essa configuração deve ser definida como um número mais baixo do que o número configurado na configuração **Número de falhas de entrada antes do bloqueio**. Essa configuração foi desenvolvida para ajudar a impedir um ataque de força bruta em PINs de usuários.
        
          - **Número de falhas de entrada antes do bloqueio**   Use essa caixa de texto para inserir o número máximo de tentativas sequenciais de logon com falha ou mal-sucedidas antes que as caixas de correio dos usuários sejam bloqueadas.
            
            Por exemplo, se um usuário tentar fazer logon em sua caixa de correio cinco vezes sem obter êxito, o sistema redefinirá o PIN do usuário com base na configuração **Número de falhas de entrada antes da redefinição do PIN**. Se o usuário tentar usar o novo PIN mais cinco vezes sem obter êxito, o sistema redefinirá novamente o PIN. Se, pela terceira vez, o usuário tentar usar esse novo PIN mais cinco vezes sem obter êxito, a caixa de correio dele será bloqueada. Depois que um usuário for bloqueado, o administrador deverá redefinir ou desbloquear manualmente a caixa de correio do usuário.
            
            Esse valor pode ser definido entre 1 e 999. Definir um valor muito baixo pode frustrar os usuários; definir um valor muito alto dá aos usuários mal-intencionados maiores chances de determinar o PIN. Para a maioria das organizações, esse valor deve ser definido para o padrão de 15 tentativas.
            
            Essa configuração deve ser maior do que o número definido na configuração **Número de falhas de entrada antes da redefinição do PIN**. Essa configuração foi desenvolvida para ajudar a impedir um ataque de força bruta em PINs de usuários.
    
      - 
        
        Use **Autorização de discagem** para configurar as regras de discagem dos usuários habilitados para UM associados a esta política de caixa de entrada de UM.
        
        Você pode usar essas configurações para controlar os número de ramais que podem ser acessados ou dos números de telefone que podem ser discados por usuários habilitados para UM associados à política de caixa de correio de UM. Você pode configurar o seguinte:
        
          - **Chamadas no mesmo plano de discagem de UM**   Marque esta caixa de seleção para permitir que usuários habilitados para UM que ligam para um número de acesso do assinante configurado em um plano de discagem e que fazem logon com êxito em sua caixa de correio realizem chamadas ou transferências para usuários habilitados para UM que tenham ramais no mesmo plano de discagem. Por padrão, essa configuração está habilitada.
            
            Quando você desabilita essa configuração, os usuários habilitados para UM que ligarem para um número de acesso de assinante configurado em um plano de discagem e conseguirem efetuar logon em sua caixa de correio com êxito poderão efetuar chamadas ou transferências para usuários não habilitados para UM ou para outros números de ramal que não estão associados a um usuário habilitado para UM. Entretanto, eles podem fazer transferências para usuários habilitados para UM que estejam no mesmo plano de discagem. Isso acontece porque, por padrão, a configuração **Chamadas para qualquer ramal** está habilitada.
        
          - **Chamadas para qualquer ramal**   Quando essa configuração estiver habilitada, os usuários que ligarem para um número de acesso do assinante que esteja configurado em um plano de discagem e conseguirem efetuar logon em sua caixa de correio com êxito poderão efetuar chamadas para usuários não habilitados para UM, para outros números de ramal que não estejam associados a um usuário habilitado para UM e para usuários habilitados para UM pertencentes ao mesmo plano de discagem. Isso acontece porque, por padrão, a configuração **Chamadas no mesmo plano de discagem da UM** está habilitada.
            
            Quando está configurações está desabilitada, os usuários que ligarem para um número do Outlook Voice Access configurado em um plano de discagem e entrarem com sucesso na caixa de correio não podem completar ligações para usuários que não estão habilitados para UM ou para outros ramais não associados com um usuário habilitado para UM. Entretanto, eles podem fazer ou transferir chamadas para ramais associados a usuários habilitados para UM. Isso acontece porque, por padrão, a configuração **Chamadas no mesmo plano de discagem da UM** está habilitada. A configuração **Chamadas para qualquer ramal** está habilitada por padrão.
            
            Você pode habilitar essa configuração em um ambiente onde nem todos os usuários tenham sido habilitados para UM. Esta configuração também é útil quando você deseja permitir que os usuários que ligam para um número do Outlook Voice Access em um plano de discagem liguem para ramais não associados com um usuário habilitado para UM.
        
          - **Grupos autorizados de regras de discagem locais/regionais**   Use essa seção para adicionar ou remover grupos de regras de discagem permitidos no país/região. Por padrão, não há grupos de regras de discagem do país/região configurados em diretivas de caixa de correio do UM.
            
            Grupos de regras de discagem do país/região são usados para permitir ou restringir números de telefone em um país ou região para os quais usuários do Outlook Voice Access podem realizar chamadas. Isso ajuda a evitar chamadas e despesas não autorizadas ou desnecessárias.
            
            Para adicionar grupos de regras de discagem do país/região, é necessário antes criar os grupos de regras de discagem do país/região apropriados no plano de discagem associado à diretiva de caixa de correio de UM e, em seguida, adicionar as entradas de regras de discagem apropriadas no grupo de regras de discagem. Após criar os grupos de regras de discagem necessários no plano de discagem, você deverá adicioná-los à lista de restrições de discagem em **Autorização de discagem** na política de caixa de correio de UM.
            
            Os grupos de regra de discagem local podem ser usados para habilitar a Unificação de Mensagens para permitir ou restringir acesso a números de telefone dentro de um país ou região. Isto é aplicado aos usuários Outlook Voice Access que ligaram para um número do Outlook Voice Access.
        
          - **Grupos autorizados de regras de discagem internacionais**   Use essa seção para adicionar ou remover grupos de regras de discagem permitidos internacionalmente. Por padrão, não há grupos de regras de discagem internacionais configurados em diretivas de caixa de correio do UM.
            
            Para adicionar grupos de regras de discagem internacionais, é necessário antes criar os grupos de regras de discagem internacionais apropriados no plano de discagem associado à diretiva de caixa de correio de UM e, em seguida, adicionar as entradas de regras de discagem apropriadas no grupo de regras de discagem. Após criar os grupos de regras de discagem necessários, você deverá adicioná-los às restrições de discagem na diretiva de caixa de correio de UM.
            
            Os grupos de regra de discagem internacional podem ser usados para permitir que a Unificação de Mensagens permita ou restrinja acesso a números de telefone fora de um país ou região. Isso se aplica a usuários do Outlook Voice Access que tenham ligado para um número do Outlook Voice Access.
            
            Grupos de regras de discagem internacionais são usados para permitir ou restringir números de telefone de fora de um país ou região para os quais usuários do Outlook Voice Access podem realizar chamadas. Isso ajuda a evitar chamadas e despesas não autorizadas ou desnecessárias.
    
      - 
        
        Use **Mensagem de Voz Protegida** para definir as seguintes configurações:
        
          - **Proteger as mensagens de voz de chamadores não autenticados**   Escolha uma das opções a seguir da lista suspensa para determinar se uma chamada de entrada atendida pela Unificação de Mensagens protegerá as mensagens de voz. Essa configuração se aplica a mensagens de voz enviadas para usuários habilitados para UM quando eles não atenderem ao telefone. Essa configuração também se aplica a mensagens de voz enviadas diretamente para usuários habilitados para UM, quando o chamador usa um atendedor automático de UM. Você pode configurar o seguinte:
            
            **Nenhum**   Use essa configuração se você não tem proteção aplicada para as mensagens de voz enviadas para usuários habilitados para UM.
            
            **Privada**   Use esta configuração quando você deseja aplicar proteção apenas para mensagens de voz que foram marcadas como privada pelo chamador.
            
            **Todas**   Use essa configuração se quiser aplicar proteção a todas as mensagens de voz, incluindo aquelas não marcadas como privadas.
        
          - **Proteger mensagens de voz de chamadores autenticados**   Escolha uma das seguintes opções da lista suspensa para determinar quando uma chamada de entrada atendida ela Unificação de Mensagens protegerá as mensagens de voz. Essa configuração se aplica a mensagens de voz enviadas para usuários habilitados para UM quando eles não atenderem ao telefone. Essa configuração também se aplica quando os chamadores fazem logon em suas caixas de correio usando o Outlook Voice Access e criam e enviam uma mensagem de voz. Você pode configurar o seguinte:
            
            **Nenhuma**   Use esta configuração para não ter a proteção aplicada a mensagens de voz enviadas para os usuários habilitados para UM.
            
            **Privada**   Use esta configuração quando você deseja aplicar proteção apenas para mensagens de voz que foram marcadas como privada pelo chamador.
            
            **Todas**   Use essa configuração se quiser aplicar proteção a todas as mensagens de voz, incluindo aquelas não marcadas como privadas.
        
          - **Exigir Tocar no Telefone para mensagens de voz protegidas**   Marque essa caixa de seleção se você desejar forçar os usuários que recebem mensagens de voz protegidas a usar o recurso Tocar no Telefone. Se o software cliente não oferece suporte para gerenciamento de direitos, os usuários devem usar o Outlook Voice Access. O recurso Tocar no Teleforne se aplica somente a clientes que utilizam uma versão do Outlook que oferece suporte para o gerenciamento de direitos. Para o Outlook 2007 ou versões anteriores que não oferecem suporte a gerenciamento de direitos, e para clientes do Outlook Web App, o Outlook Voice Access é a única maneira disponível para que os usuários ouçam mensagens de voz protegidas.
            
            A configuração padrão requer que todos os usuários associados à diretiva de caixa de correio de UM usem o recurso Tocar no Telefone para ouvir mensagens de voz protegidas. Esse procedimento impede que outras pessoas ouçam a mensagem de voz em um reprodutor de mídia, nos alto-falantes do computador ou usando um reprodutor de mídia em um telefone celular. Mesmo que estiver habilitado, o usuário habilitado para UM ainda pode utilizar o Outlook Voice Access para ouvir mensagens de voz protegidas.
            
            Isso é muito útil quando os usuários habilitados para UM utilizam computadores públicos, laptops em lugares comuns ou reprodutores de mídia de telefones celulares para ouvir a mensagem de voz protegida que contém informações particulares.
        
          - **Permitir respostas de voz para itens de email e calendário**   Use esta opção para permitir que usuários habilitados para UM enviem respostas de voz a mensagens de caixa postal protegidas. O padrão é habilitado. Se você desabilitar isso, se um usuário habilitado para UM receber uma mensagem de caixa postal protegida, ele não conseguira usar o Outlook Voice Access para responder os itens de email e calendário.
        
          - **Mensagem para enviar para usuários que não tenham suporte ao Gerenciamento de Direitos do Windows**   As mensagens de voz protegidas podem ser acessadas somente por clientes de email que oferecem suporte ao Gerenciamento de Direitos de Informações (IRM) ou se um usuário habilitado para UM utilizar o Outlook Voice Access para acessar a mensagem de voz protegida.
            
            Se uma mensagem de caixa postal protegida for enviada a um cliente de email que não oferece suporte para o IRM, o texto que você incluir nessa caixa será enviado ao usuário por email. Essas informações devem incluir instruções sobre o que fazer para receber a mensagem de caixa postal protegida.

## Usar o Shell para gerenciar uma política de caixa de correio de UM

Este exemplo define as configurações de PIN de usuários associados a uma diretiva de caixa de correio de UM chamada `MyUMMailboxPolicy`.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -LogonFailuresBeforePINReset 8 -MaxLogonAttempts 12 -MinPINLength 8 -PINHistoryCount 10 -PINLifetime 60 -ResetPINText "The PIN that is used to allow you access to your mailbox using Outlook Voice Access has been reset."

Este exemplo seleciona os grupos de região ou do país e os grupos internacionais daqueles configurados no plano de discagem do UM associado à diretiva de caixa de correio do UM. Os usuários habilitados para UM associados a essa diretiva de caixa de correio de UM poderão fazer chamadas de saída de acordo com as regras definidas nesses grupos.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -AllowDialPlanSubscribers $true -AllowedInCountryOrRegionGroups InCountry/RegionGroup1,InCountry/RegionGroup2 -AllowedInternationalGroups InternationalGroup1,InternationalGroup2 -AllowExtensions $true 

Este exemplo configura o texto das mensagens de voz enviadas a usuários habilitados para UM e o texto incluído em um email enviado a um usuário que foi habilitado para UM.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -UMEnabledText "You have been enabled for Unified Messaging." -VoiceMailText "You have received a voice message from Microsoft Exchange 2013 Unified Messaging." 

## Usar o Shell para visualizar propriedades de diretivas de caixa de correio de UM

Este exemplo retorna uma lista formatada de todas as diretivas de caixa de correio da UM na floresta do Active Directory.

    Get-UMMailboxPolicy | Format-List

Este exemplo retorna as propriedades e os valores de uma política de caixa de correio de UM chamada `MyUMMailboxPolicy`.

    Get-UMMailboxPolicy -Identity MyUMMailboxPolicy

