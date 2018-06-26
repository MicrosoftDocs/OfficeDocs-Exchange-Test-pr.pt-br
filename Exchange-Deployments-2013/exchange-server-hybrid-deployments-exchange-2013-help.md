---
title: 'Implantações Híbridas do Exchange Server: Exchange 2013 Help'
TOCTitle: '@NoTitle'
ms:assetid: 59e32000-4fcf-417f-a491-f1d8f9aeef9b
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ200581(v=EXCHG.150)
ms:contentKeyID: 50487114
ms.date: 05/05/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Implantações Híbridas do Exchange Server

 

_<strong>Aplica-se a:</strong>Exchange Online, Exchange Server 2013, Exchange Server 2016_

_<strong>Tópico modificado em:</strong>2018-04-16_

**Resumo:** O que você precisa saber para planejar uma implantação híbrida do Exchange.

A implantação híbrida oferece às organizações a capacidade de levar a experiência e o controle administrativo cheio de recursos que elas possuem em suas organizações locais do Microsoft Exchange para a nuvem. Uma implantação híbrida oferece a aparência perfeita de uma única organização do Exchange entre uma organização local do Exchange e o Exchange Online no Microsoft Office 365. Além disso, uma implantação híbrida pode servir como uma etapa intermediária para se mover completamente para uma organização do Exchange Online.

**Sumário**

Recursos de implantação híbrida do Exchange

Considerações sobre a implantação híbrida do Exchange

Componentes de implantação híbrida do Exchange

Exemplo de implantação híbrida do Exchange

Aspectos a considerar antes de configurar uma implantação híbrida do Exchange

Terminologia principal

Documentação de implantação híbrida do Exchange

## Recursos de implantação híbrida do Exchange

A implantação híbrida habilita os seguintes recursos:

  - Roteamento de email seguro entre organizações locais e do Exchange online.

  - Roteamento de mensagens com um namespace de domínio compartilhado. Por exemplo, as organizações locais e do Exchange Online usam o domínio de SMTP @contoso.com.

  - Uma GAL (lista de endereços global) unificada, também chamada de "catálogo de endereços compartilhado".

  - Compartilhamento de disponibilidade e calendário entre a organização local e o Exchange.

  - Controle centralizado do fluxo de email de entrada e saída. É possível configurar todas as mensagens de entrada e saída do Exchange Online de forma que elas sejam roteadas através da organização local do Exchange.

  - Uma URL única do Outlook na Web para a organização local e a organização do Exchange Online.

  - A capacidade de mover caixas de correio locais existentes para a organização do Exchange Online. Se necessário, caixas de correio do Exchange Online também podem ser movidas de volta à organização local, se necessário.

  - Gerenciamento centralizado de caixa de correio usando o Centro de Administração do Exchange (EAC).

  - Acompanhamento de mensagens, Dicas de Email e pesquisa em múltiplas caixas de correio entre a organização local e o Exchange Online.

  - O arquivamento de mensagens em nuvem para caixas de correio do Exchange local. O Arquivamento Online do Exchange pode ser usado com uma implantação híbrida. Saiba mais sobre o Arquivamento Online do Exchange em [Serviços Adicionais do Microsoft Office 365](https://go.microsoft.com/fwlink/p/?linkid=233231).

## Considerações sobre a implantação híbrida do Exchange

Você deve considerar o seguinte antes de realizar uma implantação híbrida do Exchange:

  - **Requisitos de implantação híbrida** Antes de configurar uma implantação híbrida, você precisa verificar se a sua organização local atende a todos os pré-requisitos necessários para uma implantação bem-sucedida. Para saber mais, confira [Pré-requisitos de implantação híbrida](hybrid-deployment-prerequisites-exchange-2013-help.md).

  - **Clientes do Exchange ActiveSync**  Quando você move uma caixa de correio de sua organização do Exchange local para o Exchange Online, todos os clientes que acessam a caixa de correio precisam ser atualizados para usar o Exchange Online. Isso inclui dispositivos do Exchange ActiveSync. A maioria dos clientes do Exchange ActiveSync é automaticamente reconfigurada quando a caixa de correio é movida para o Exchange Online. No entanto, alguns dispositivos mais antigos podem não atualizar corretamente. Para mais informações, confira [Configurações de dispositivo do Exchange ActiveSync com implantações híbridas do Exchange](exchange-activesync-device-settings-with-exchange-hybrid-deployments-exchange-2013-help.md).

  - **Migração de permissões de caixa de correio** As permissões de caixa de correio local, como Enviar como, Acesso Total, Enviar em nome de e permissões de pastas, que são explicitamente aplicadas na caixa de correio são migradas para o Exchange Online. As permissões herdadas de caixa de correio (não explícitas) e as permissões concedidas a objetos não habilitadas no Exchange Online não são migradas. Garanta que as permissões sejam concedidas explicitamente e que todos os objetos tenham o email habilitado antes da migração. Portanto, você precisará planejar a configuração dessas permissões no Office 365, se aplicáveis para sua organização. No caso de permissões Enviar como, se o usuário e o recurso que está tentando ser enviado como não forem migrados ao mesmo tempo, você precisará adicionar explicitamente a permissão Enviar como no Exchange Online usando o cmdlet **Add-RecipientPermission**.

  - **Suporte para permissões de caixa de correio entre locais** As implantações híbridas do Exchange têm suporte para as permissões "Acesso completo" e "Enviar em nome de" entre caixas de correio localizadas em uma organização local do Exchange e caixas de correio localizadas no Office 365. São necessárias etapas adicionais para usar as permissões "Enviar como". Além disso, pode ser necessário fazer algumas configurações extras para habilitar o suporte a permissões de caixa de correio entre locais, dependendo da versão do Exchange instalada na organização local. Saiba mais em [Delegar permissões de caixa de correio](permissions-in-exchange-hybrid-deployments-exchange-2013-help.md), [Permissões em implantações híbridas do Exchange](permissions-in-exchange-hybrid-deployments-exchange-2013-help.md) e [Configurar o Exchange para oferecer suporte à caixa de correio delegada permissões em uma implantação híbrida](configure-exchange-to-support-delegated-mailbox-permissions-in-a-hybrid-deployment-exchange-2013-help.md).
    

    > [!TIP]
    > Em fevereiro de 2018, começamos a implementar os recursos de suporte para "Enviar em Nome de", "Acesso Total" e direitos de pastas entre florestas e esperamos concluir essa implementação até abril de 2018.



  - **Exclusão**  Como parte do gerenciamento contínuo de destinatários, você pode precisar mover caixas de correio do Exchange Online de volta para o seu ambiente local.
    
    Para saber mais sobre como mover caixas de correio em uma implantação híbrida com base no Exchange 2010, consulte [Mover uma caixa de correio do Exchange Online para a organização no local](https://technet.microsoft.com/pt-br/library/hh882527\(v=exchg.150\)).
    
    Para saber mais sobre como mover caixas de correio em uma implantação híbrida com base no Exchange 2013 ou versão mais recente, confira [Movimentação de caixas de correio entre organizações locais e do Exchange Online em implantações híbridas](move-mailboxes-between-on-premises-and-exchange-online-organizations-in-hybrid-deployments-exchange-2013-help.md).

  - **Configurações de encaminhamento da caixa de correio** As caixas de correio podem ser configuradas para encaminhar automaticamente os emails recebidos para outra caixa de correio. Embora o encaminhamento de caixas de correio tenha suporte no Exchange Online, a configuração de encaminhamento não é copiada para o Exchange Online quando a caixa de correio é migrada para lá. Para migrar caixas de correio para o Exchange Online, exporte a configuração de encaminhamento de cada uma delas. A configuração de encaminhamento é armazenada nas propriedades `DeliverToMailboxAndForward`, `ForwardingAddress` e `ForwardingSmtpAddress` em cada caixa de correio.

## Componentes de implantação híbrida do Exchange

A implantação híbrida envolve vários serviços e componentes diferentes:

  - **Servidores do Exchange**  Pelo menos um servidor do Exchange precisa ser configurado em sua organização local se você quiser configurar uma implantação híbrida. Se você estiver executando o Exchange 2013 ou versão mais antiga, será preciso instalar pelo menos um servidor que execute as funções de Caixa de Correio e Acesso para Cliente. Se você estiver executando o Exchange 2016 ou versão mais recente, pelo menos um servidor que execute a função de Caixa de Correio deve ser instalado. Se for necessário, os servidores de Transporte de Borda do Exchange também poderão ser instalados em uma rede de perímetro e prestarão suporte ao fluxo de email seguro com o Office 365.
    

    > [!TIP]
    > Não há suporte para a instalação de servidores do Exchange que executam as funções de servidor de Caixa de Correio ou de Acesso para Cliente em uma rede de perímetro.



  - **Microsoft Office 365**   O serviço Office 365 inclui uma organização do Exchange Online como parte da sua assinatura. A organizações que configuram uma implantação híbrida precisam adquirir uma licença para cada caixa de correio migrada ou criada na organização do Exchange Online.

  - **Assistente de Configuração híbrida**   O Exchange inclui o assistente de Configuração Híbrida que fornece a você um processo simplificado para configurar uma implantação híbrida entre a organização local do Exchange e do Exchange Online.
    
    Saiba mais em [Assistente de Configuração Híbrida](hybrid-configuration-wizard-exchange-2013-help.md).

  - **Sistema de autenticação do AD do Azure**   O sistema de autenticação do Azure Active Directory (AD) é um serviço gratuito baseado em nuvem que atua como o agente de confiança entre sua organização do Exchange 2016 local e a organização do Exchange Online. As organizações locais que configuram uma implantação híbrida devem dispor de confiança de federação com o sistema de autenticação do AD do Azure. A confiança de federação pode ser criada manualmente como parte da configuração dos recursos de compartilhamento federado entre uma organização local do Exchange e outras organizações federadas do Exchange ou como parte da configuração de uma implantação híbrida com o assistente de Configuração Híbrida. Uma confiança de federação com o sistema de autenticação do AD do Azure para seu locatário do Office 365 é configurada automaticamente quando você habilita sua conta de serviço do Office 365.
    
    Saiba mais em [Sistema de autenticação do Azure AD](https://go.microsoft.com/fwlink/p/?linkid=135986)

  - **Sincronização do Azure Active Directory**   A sincronização do AD do Azure replica as informações locais do Active Directory de objetos habilitados para email na organização do Office 365 para oferecer suporte à GAL (lista de endereços global) unificada. As organizações que configuram uma implantação híbrida precisam implantar o Azure AD Connect em um servidor local separado para sincronizar seu Active Directory local com o Office 365.
    
    Saiba mais em: [Azure AD Connect – Visão Geral](https://go.microsoft.com/fwlink/p/?linkid=203007)

Retornar ao início

## Exemplo de implantação híbrida

Examine o cenário a seguir. É um exemplo de topologia que oferece uma visão geral de uma implantação típica do Exchange 2016. Contoso, Ltd. é uma organização de floresta única e de domínio único com dois controladores de domínio e um servidor Exchange 2016 instalados. Os usuários remotos da Contoso usam o Outlook na Web para se conectar com o Exchange 2016 pela Internet e, assim, verificar suas caixas de correio e acessar o calendário do Outlook.

![Implantação local do Exchange antes de configurar uma implantação híbrida com o Office 365](images/JJ200581.dad133ae-d18a-42ec-8f0a-dd1de391200e(EXCHG.150).png "Implantação local do Exchange antes de configurar uma implantação híbrida com o Office 365")

Digamos que você seja o administrador de rede da Contoso e que esteja interessado em configurar uma implantação híbrida. Você implanta e configura um servidor obrigatório do Azure AD Connect e também decide usar o recurso de sincronização de senha para permitir que os usuários usem as mesmas credenciais para a conta de rede local e a conta do Office 365. Depois de concluir os pré-requisitos da implantação híbrida e usar o assistente de Configuração Híbrida para selecionar opções para a implantação híbrida, sua nova topologia possui a seguinte configuração:

  - Os usuários usarão o mesmo nome de usuário e senha para fazer logon nas organizações local e do Exchange Online ("logon único").

  - As caixas de correio situadas na organização local e na organização do Exchange Online usarão o mesmo domínio de endereço de email. Por exemplo, as caixas de correio situadas no local e as caixas de correio situadas na organização do Exchange Online usarão ambas @contoso.com nos endereços de email do usuário.

  - Todos os emails de saída serão entregues à Internet pela organização local. A organização local controla todo o transporte de mensagens e funciona como um retransmissor para a organização do Exchange Online ("transporte de email centralizado").

  - Os usuários das organizações local e do Exchange Online podem compartilhar informações de disponibilidade no calendário uns com os outros. Os relacionamentos de organização configurados para ambas as organizações viabilizam também o controle de mensagens entre locais, MailTips e pesquisa de mensagens.

  - Os usuários locais e do Exchange Online usam a mesma URL para se conectarem às suas caixas de correio pela Internet.

![Implantação local do Exchange após configurar uma implantação híbrida com o Office 365](images/JJ200581.e8681849-f15d-4d0e-b77e-6105b6096c4b(EXCHG.150).png "Implantação local do Exchange após configurar uma implantação híbrida com o Office 365")

Ao comparar a configuração atual de organização da Contoso com a configuração de implantação híbrida, observe que a configuração de implantação híbrida adicionou servidores e serviços que oferecem suporte a recursos e comunicação adicionais que são compartilhados entre as organizações local e do Exchange Online. Veja a seguir uma visão geral das alterações feitas pela implantação híbrida na organização local inicial do Exchange.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Configuração</th>
<th>Antes da implantação híbrida</th>
<th>Após a implantação híbrida</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Local da caixa de correio</p></td>
<td><p>Caixas de correio locais somente.</p></td>
<td><p>Caixas de correio locais e no Office 365.</p></td>
</tr>
<tr class="even">
<td><p>Transporte de mensagens</p></td>
<td><p>Os servidores locais de Caixa de Correio controlam todo o direcionamento de mensagens de entrada e saída.</p></td>
<td><p>Os servidores locais de Caixa de Correio tratam de todo o direcionamento de mensagens internas entre a organização local e a organização do Office 365.</p></td>
</tr>
<tr class="odd">
<td><p>Outlook na Web</p></td>
<td><p>Os servidores locais de Caixa de Correio recebem todas as solicitações do Outlook na Web e exibem informações das caixas de correio.</p></td>
<td><p>Os servidores locais de Caixa de Correio redirecionam as solicitações do Outlook na Web para servidores locais de Caixa de Correio do Exchange 2016 ou fornecem um link para fazer logon no Office 365.</p></td>
</tr>
<tr class="even">
<td><p>GAL unificada para ambas as organizações</p></td>
<td><p>Não aplicável; organização única somente.</p></td>
<td><p>A servidor de sincronização local do Active Directory replica as informações do Active Directory referentes a objetos habilitados para o Office 365.</p></td>
</tr>
<tr class="odd">
<td><p>Logon único usado em ambas as organizações</p></td>
<td><p>Não aplicável; organização única somente.</p></td>
<td><p>O Office 365 e o Active Directory locais usam o mesmo nome de usuário e senha para caixas de correio localizadas no local ou no Office 365.</p></td>
</tr>
<tr class="even">
<td><p>Relacionamento de organização estabelecido e confiança de federação com o sistema de autenticação do AD do Azure</p></td>
<td><p>É possível configurar um relacionamento de confiança com o sistema de autenticação do AD do Azure e relacionamentos de organização com outras organizações federadas do Exchange.</p></td>
<td><p>O relacionamento de confiança com o sistema de autenticação do AD do Azure é obrigatório. Relacionamentos de organização são estabelecidos entre a organização local e a organização do Office 365.</p></td>
</tr>
<tr class="odd">
<td><p>Compartilhamento de disponibilidade</p></td>
<td><p>Compartilhamento de disponibilidade entre usuários locais somente.</p></td>
<td><p>Compartilhamento de disponibilidade entre usuários locais e do Office 365.</p></td>
</tr>
</tbody>
</table>


## Aspectos a considerar antes de configurar uma implantação híbrida

Como agora você está mais familiarizado com o conceito de implantação híbrida, é hora de analisar cuidadosamente algumas questões importantes. A configuração da implantação híbrida poderá afetar várias áreas em sua rede atual e na organização do Exchange.

## Sincronização de diretórios e logon único

Para configurar uma implantação híbrida, é exigida a sincronização do Active Directory entre a organização local e o Office 365, que é executada a cada três horas por um servidor que executa o Azure Active Directory Connect. A sincronização de diretórios permite que os destinatários na organização vejam uns aos outros na lista de endereços global. Ela também sincroniza os nomes de usuário e senhas que permitem aos usuários fazer logon com as mesmas credenciais na organização local e no Office 365.


> [!TIP]
> Se você optar por configurar o Azure AD Connect com o AD FS, os nomes de usuário e senhas de usuários locais ainda serão sincronizados com o Office 365 por padrão. No entanto, os usuários farão a autenticação no Active Directory local por meio do AD FS como principal método de autenticação. No caso do AD FS não conseguir se conectar ao seu Active Directory local por qualquer motivo, os clientes retornarão e autenticarão os nomes de usuário e senhas sincronizados com o Office 365.



Todos os clientes do Azure Active Directory e do Office 365 têm um limite padrão de 50 mil objetos (usuários, contatos habilitados para email e grupos). Esse limite determina quantos objetos você pode criar na organização do Office 365. Quando você verifica seu primeiro domínio, esse limite de objetos aumenta automaticamente para 300 mil objetos. Se tiver verificado um domínio e precisar sincronizar mais de 300 mil objetos ou se não tiver qualquer domínio a ser verificado e precisar sincronizar mais de 50 mil objetos, você precisará entrar em contato com o suporte do Azure Active Directory para solicitar que o seu limite de cotas de objetos seja aumentado.

Além de um servidor que executa o Azure AD Connect, também será preciso implantar um servidor de proxy do aplicativo Web se você optar por configurar o AD FS. Esse servidor deve ser colocado em sua rede de perímetro e atuará como intermediário entre o servidor interno do Azure AD Connect e a Internet. O servidor de proxy do aplicativo Web precisa aceitar conexões de clientes e servidores na Internet que usam a porta TCP 443.

## Gerenciamento de implantação híbrida

É possível gerenciar uma implantação híbrida no Exchange 2016 por meio de um único console de gerenciamento unificado que permite o gerenciamento de suas organizações locais e do Exchange Online. O *EAC* (Centro de administração do Exchange), que substitui o Console de Gerenciamento do Exchange e o Painel de Controle do Exchange, permite conectar e configurar recursos para ambas as organizações. Ao executar o assistente de Configuração Híbrida pela primeira vez, você receberá uma solicitação para conectar-se à organização do Exchange Online. Você deve usar uma conta do Office 365 que seja membro do grupo de função de Gerenciamento da Organização para conectar o EAC à sua organização do Exchange Online.

## Certificados

Os certificados digitais SSL (Secure Sockets Layer) desempenham uma importante função na implantação híbrida. Eles ajudam a garantir a comunicação entre os servidores híbridos locais e a organização do Exchange Online. Os certificados são um requisito para configurar vários tipos de serviços. Se já estiver usando certificados digitais em sua organização do Exchange, talvez seja necessário modificar os certificados para incluir domínios adicionais ou adquirir certificados adicionais de uma autoridade certificadora (CA) de confiança. Se ainda não usa certificados, será necessário adquirir um ou mais certificados junto a uma autoridade certificadora de confiança.

Saiba mais em: [Requisitos de certificado para implantações híbridas](certificate-requirements-for-hybrid-deployments-exchange-2013-help.md)

## Largura de banda

Sua conexão de rede com a Internet afetará diretamente o desempenho da comunicação entre as suas organizações local e do Office 365. Isso é particularmente verdadeiro ao mover caixas de correio de seu servidor do Exchange 2016 local para a organização do Office 365. A quantidade de largura de banda de rede disponível, juntamente com o tamanho da caixa de correio e o número de caixas de correio movidas em paralelo, resultará em várias vezes para concluir as movimentações de caixas de correio. Além disso, outros serviços do Office 365, como o SharePoint Server 2016 e o Skype for Business, também poderão afetar a largura de banda disponível para serviços de mensagens.

Antes de mover caixas de correio para o Office 365, você deve:

  - Determinar o tamanho médio da caixa de correio para caixas de correio que serão movidas para o Office 365.

  - Determine a conexão média e a velocidade de produtividade para a conexão com a Internet na organização local.

  - Calcular a velocidade média de transferência prevista e planejar as movimentações das caixas de correio com base nesses resultados.

Saiba mais em: [Sistema de rede](https://go.microsoft.com/fwlink/p/?linkid=280178)

## Unificação de Mensagens

A Unificação de Mensagens (UM) é suportada em uma implantação híbrida entre as suas organizações locais e do Office 365. A solução de telefonia local deve ser capaz de se comunicar com o Office 365. Ela pode exigir que você compre hardware e software adicionais.

Se você quiser mover caixas de correio de sua organização local para o Office 365 e essas caixas de correio forem configuradas para UM, configure a UM em sua implantação híbrida antes de mover essas caixas de correio. Se você mover as caixas de correio antes de configurar a UM em sua implantação híbrida, essas caixas de correio não terão mais acesso à funcionalidade de UM.

Saiba mais em: [Configurar mensagens unificadas em uma implantação híbrida](https://go.microsoft.com/fwlink/p/?linkid=842271)

## Gerenciamento de Direitos de Informação

O IRM (Gerenciamento de Direitos de Informação) permite que os usuários apliquem os modelos do AD RMS (Active Directory Rights Management Services) às mensagens que enviarem. Os modelos do AD RMS podem ajudar a evitar o vazamento de informações permitindo que os usuários controlem quem pode abrir uma mensagem protegida por direitos e o que eles podem fazer com essa mensagem depois de aberta.

O IRM em uma implantação híbrida requer planejamento, configuração manual da organização do Office 365 e uma compreensão de como os clientes usam os servidores do AD RMS, dependendo de a caixa de correio estar no local ou na organização do Exchange Online.

Saiba mais em: [IRM em implantações híbridas do Exchange](irm-in-exchange-hybrid-deployments-exchange-2013-help.md)

## Dispositivos móveis

Os dispositivos móveis são compatíveis com implantações híbridas. Se o Exchange ActiveSync já estiver habilitado nos servidores existentes, eles continuarão a redirecionar solicitações de dispositivos móveis para caixas de correio localizadas no servidor de Caixa de Correio local. Para dispositivos móveis conectados a caixas de correios existentes que são movidas a partir da organização local para o Office 365, os perfis do Exchange ActiveSync serão automaticamente atualizados para se conectar ao Office 365 na maioria dos telefones. Todos os dispositivos móveis compatíveis com o Exchange ActiveSync devem ser também compatíveis com implantação híbrida.

Saiba mais em: [Celulares](https://go.microsoft.com/fwlink/p/?linkid=206387)

## Requisitos do cliente

É recomendável que seus clientes usem o Outlook 2016 ou o Outlook 2013 para uma melhor experiência e desempenho na implantação híbrida. Clientes pré-Outlook 2010 não possuem suporte em implantações híbridas e com o Office 365.

## Licenciamento para o Office 365

Para criar ou mover caixas de correio para o Office 365, é necessário inscrever-se no Office 365 para empresas e ter licenças disponíveis. Ao inscrever-se no Office 365, você receberá um número específico de licenças que poderá atribuir a novas caixas de correio ou a caixas de correio movidas da organização local. Cada caixa de correio do Office 365 deve possuir uma licença.

## Serviços antivírus e anti-spam

As caixas de correio movidas para o Office 365 são automaticamente equipadas com proteção antivírus e antispam pelo Exchange Online Protection (EOP), um serviço disponibilizado pelo Office 365. Você pode precisar adquirir licenças adicionais do EOP para seus usuários locais, se você optar por rotear todos os emails de entrada da Internet, através do serviço EOP. Recomendamos que seja avaliado se a proteção do EOP no Office 365 também é adequada para atender às necessidades de antivírus e antispam de sua organização local. Se possui proteção no local para sua organização local, pode ser necessário atualizar ou configurar suas soluções de antivírus e anti-spam locais para a máxima proteção em sua organização.

Saiba mais em: [Proteção antispam e antimalware](https://technet.microsoft.com/pt-br/library/jj200731\(v=exchg.150\))

## Pastas públicas

As pastas públicas agora são suportadas no Office 365 e as pastas públicas locais podem ser migradas para o Office 365. Além disso, as pastas públicas no Office 365 podem ser movidas para a organização do Exchange 2016 local. Tanto usuários locais quanto os do Office 365 podem acessar pastas públicas localizadas nas duas organizações usando o Outlook na Web, Outlook 2016, Outlook 2013 ou Outlook 2010 SP2 ou versão posterior. A configuração de pastas públicas locais já existentes e o acesso às caixas de correio locais não são alterados na configuração de uma implantação híbrida.

Saiba mais em: [Pastas públicas](https://technet.microsoft.com/pt-br/library/jj150538\(v=exchg.150\))

## Acessibilidade

Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos nesta lista de verificação, consulte [Atalhos de teclado no Centro de administração do Exchange](https://technet.microsoft.com/pt-br/library/jj150484\(v=exchg.150\)).

## Terminologia principal

A lista a seguir oferece definições dos componentes principais associados a implantações híbridas no Exchange 2013.

  - **transporte de email centralizado**  
    A opção de configuração híbrida em que as mensagens de internet de entrada e de saída do Exchange Online são roteadas através da organização do Exchange local. Essa opção de roteamento é configurada no Assistente de Configuração Híbrida. Para mais informações, consulte [Opções de transporte em implantações híbridas do Exchange](transport-options-in-exchange-hybrid-deployments-exchange-2013-help.md).

<!-- end list -->

  - **domínio de coexistência**  
    Um domínio aceito adicionado à organização local para solicitações de fluxo de email híbrido e Descoberta Automática para o serviço Office 365. Esse domínio é adicionado como domínio de proxy secundário para quaisquer políticas de endereços de email que tenham modelos do *PrimarySmtpAddress* para domínios selecionados no assistente de Configuração Híbrida. Por padrão, esse domínio é o \<domínio\>.mail.onmicrosoft.com.

<!-- end list -->

  - ***HybridConfiguration* Objeto do Active Directory**  
    O objeto do Active Directory na organização local que contém os parâmetros de configuração de implantação híbrida desejados definidos pelas seleções escolhidas no assistente de Configuração Híbrida. O Mecanismo de Configuração Híbrida usa esses parâmetros ao definir as configurações locais e do Exchange Online, para habilitar configurações híbridas. O conteúdo do objeto *HybridConfiguration* é redefinido cada vez que o assistente de Configuração Híbrida é executado.

<!-- end list -->

  - **Mecanismo de configuração híbrida**  
    O Mecanismo de Configuração Híbrida (Hybrid Configuration Engine, HCE) executa as principais ações necessárias para a configuração e atualização de uma implantação híbrida. O HCE compara o estado do objeto do Active Directory da *HybridConfiguration* com as configurações locais do Exchange e do Exchange Online e executa as tarefas para corresponder com as configurações de implantação definidas no objeto do Active Directory do *HybridConfiguration*. Para mais informações, confira [Mecanismo de Configuração Híbrida](hybrid-configuration-wizard-exchange-2013-help.md).

<!-- end list -->

  - **assistente de configuração híbrida (HCW)**  
    Uma ferramenta adaptativa oferecida no Exchange para guiar os administradores através da configuração de uma implantação híbrida entre as organizações local e do Exchange Online. O assistente define os parâmetros da configuração de implantação híbrida no objeto da *HybridConfiguration* e instrui o Mecanismo de Configuração Híbrida a executar as tarefas de configuração necessárias para habilitar os recursos híbridos definidos. Para mais informações, confira [Assistente de Configuração Híbrida](hybrid-configuration-wizard-exchange-2013-help.md).

<!-- end list -->

  - **Implantação híbrida com base no Exchange 2010**  
    Uma implantação híbrida configurada usando o Service Pack 3 (SP3) para servidores locais do Exchange Server 2010 como o ponto de extremidade de conexão para os serviços do Office 365 e Exchange Online. Uma opção de implantação híbrida para organizações locais do Exchange 2010, Exchange Server 2007 e Exchange Server 2003.

<!-- end list -->

  - **Implantação híbrida com base no Exchange 2013**  
    Uma implantação híbrida configurada usando os servidores locais do Exchange 2013 como o ponto de extremidade de conexão para os serviços do Office 365 e do Exchange Online. Uma opção de implantação híbrida para organizações locais do Exchange 2013, Exchange 2010 e Exchange 2007.

<!-- end list -->

  - **Implantação híbrida com base no Exchange 2016**  
    Uma implantação híbrida configurada usando os servidores locais do Exchange 2016 como o ponto de extremidade de conexão para os serviços do Office 365 e do Exchange Online. Uma opção de implantação híbrida para organizações locais do Exchange 2016, Exchange 2013 e Exchange 2010.

<!-- end list -->

  - **transporte de email seguro**  
    Um recurso configurado automaticamente de uma implantação híbrida que habilita mensagens seguras entre as organizações local e do Exchange Online. As mensagens são criptografadas e autenticadas usando o protocolo TLS com um certificado selecionado no assistente de Configuração Híbrida. O locatário do Office 365 é o ponto de extremidade para conexões de transporte híbrido originadas na organização local e a origem de conexões de transporte híbrido com a organização local do Exchange Online.

Retornar ao início

## Documentação de implantação híbrida do Exchange

A tabela a seguir contém links para tópicos que o ajudarão a entender e gerenciar implantações híbridas no Microsoft Exchange.


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
<td><p><a href="hybrid-configuration-wizard-exchange-2013-help.md">Assistente de Configuração Híbrida</a></p></td>
<td><p>Saiba mais como o assistente de Configuração Híbrida e o Mecanismo de Configuração Híbrida configuram uma implantação híbrida.</p></td>
</tr>
<tr class="even">
<td><p><a href="hybrid-deployment-prerequisites-exchange-2013-help.md">Pré-requisitos de implantação híbrida</a></p></td>
<td><p>Saiba mais sobre pré-requisitos de implantação híbrida, incluindo organizações compatíveis do Exchange Server, requisitos do Office 365 e outros requisitos de configuração local.</p></td>
</tr>
<tr class="odd">
<td><p><a href="certificate-requirements-for-hybrid-deployments-exchange-2013-help.md">Requisitos de certificado para implantações híbridas</a></p></td>
<td><p>Saiba mais sobre os requisitos para certificados digitais em implantações híbridas.</p></td>
</tr>
<tr class="even">
<td><p><a href="transport-options-in-exchange-hybrid-deployments-exchange-2013-help.md">Opções de transporte em implantações híbridas do Exchange</a></p></td>
<td><p>Saiba mais sobre as opções de transporte de mensagem de entrada e de saída em implantações híbridas.</p></td>
</tr>
<tr class="odd">
<td><p><a href="transport-routing-in-exchange-hybrid-deployments-exchange-2013-help.md">Roteamento de transporte em implantações híbridas do Exchange</a></p></td>
<td><p>Saiba mais sobre as opções de roteamento de mensagem de entrada e de saída em uma implantação híbrida.</p></td>
</tr>
<tr class="even">
<td><p><a href="hybrid-management-in-exchange-hybrid-deployments-exchange-2013-help.md">Gerenciamento híbrido em implantações híbridas do Exchange</a></p></td>
<td><p>Saiba mais sobre como gerenciar sua implantação híbrida com o Centro de Administração do Exchange e o Shell de Gerenciamento do Exchange.</p></td>
</tr>
<tr class="odd">
<td><p><a href="shared-free-busy-in-exchange-hybrid-deployments-exchange-2013-help.md">Disponibilidade compartilhada em implantações híbridas do Exchange</a></p></td>
<td><p>Saiba mais sobre compartilhamento de disponibilidade de calendário entre organizações locais e do Exchange Online em uma implantação híbrida.</p></td>
</tr>
<tr class="even">
<td><p><a href="server-roles-in-exchange-hybrid-deployments-exchange-2013-help.md">Funções de servidor em implantações híbridas do Exchange</a></p></td>
<td><p>Saiba mais sobre como as funções de servidor do Exchange funcionam em uma implantação híbrida.</p></td>
</tr>
<tr class="odd">
<td><p><a href="irm-in-exchange-hybrid-deployments-exchange-2013-help.md">IRM em implantações híbridas do Exchange</a></p></td>
<td><p>Saiba mais sobre o funcionamento do Gerenciamento de Direitos de Informação em uma implantação híbrida.</p></td>
</tr>
<tr class="even">
<td><p><a href="permissions-in-exchange-hybrid-deployments-exchange-2013-help.md">Permissões em implantações híbridas do Exchange</a></p></td>
<td><p>Saiba mais sobre como a implantação híbrida usa o controle de acesso baseado em função (RBAC) para controlar permissões.</p></td>
</tr>
<tr class="odd">
<td><p><a href="edge-transport-servers-with-hybrid-deployments-exchange-2013-help.md">Servidores de transporte de borda com implantações híbridas</a></p></td>
<td><p>Saiba mais sobre os servidores de Transporte de Borda do Exchange e como eles são implantados e operam em uma implantação híbrida.</p></td>
</tr>
<tr class="even">
<td><p><a href="single-sign-on-with-hybrid-deployments-exchange-2013-help.md">Logon único com implantações híbridas</a></p></td>
<td><p>Saiba mais sobre como realizar o logon único usando a sincronização de senha e a função do AD FS em uma implantação híbrida.</p></td>
</tr>
<tr class="odd">
<td><p><a href="hybrid-deployment-procedures-exchange-2013-help.md">Procedimentos de Implantação Híbrida</a></p></td>
<td><p>Explore procedimentos para criação e modificação de implantações híbridas para suas organizações do Exchange locais e do Exchange Online.</p></td>
</tr>
<tr class="even">
<td><p><a href="hybrid-deployments-with-exchange-2013-and-exchange-2010-exchange-2013-help.md">Implantações híbridas com o Exchange 2013 e o Exchange 2010</a></p></td>
<td><p>Saiba mais sobre implantações híbridas baseadas no Exchange 2013 com organizações do Exchange 2010.</p></td>
</tr>
<tr class="odd">
<td><p><a href="hybrid-deployments-with-exchange-2013-and-exchange-2007-exchange-2013-help.md">Implantações híbridas com o Exchange 2013 e o Exchange 2007</a></p></td>
<td><p>Saiba mais sobre implantações híbridas baseadas no Exchange 2013 com organizações do Exchange 2007.</p></td>
</tr>
</tbody>
</table>


## Começando a usar o Office 365?


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><img src="images/JJ200581.eac8a413-9498-4220-8544-1e37d1aaea13(EXCHG.150).png" title="O ícone pequeno do LinkedIn Learning" alt="O ícone pequeno do LinkedIn Learning" /> <strong>Começando a usar o Office 365?</strong><br />
Descubra cursos em vídeo gratuitos para <a href="https://support.office.com/pt-br/article/office-365-admin-and-it-pro-courses-68cc9b95-0bdc-491e-a81f-ee70b3ec63c5">Office 365 admins and IT pros</a>, oferecidos pelo LinkedIn Learning.</p></td>
</tr>
</tbody>
</table>

