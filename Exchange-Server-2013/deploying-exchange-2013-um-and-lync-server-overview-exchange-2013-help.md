---
title: 'Implantando a visão geral da Unificação de MENSAGENS do Exchange 2013 e Lync Server: Exchange 2013 Help'
TOCTitle: Implantando a visão geral da Unificação de MENSAGENS do Exchange 2013 e Lync Server
ms:assetid: 96fcb0dd-79ee-4e55-9e59-3ee7fbe3c4a1
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb676409(v=EXCHG.150)
ms:contentKeyID: 50486237
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Implantando a visão geral da Unificação de MENSAGENS do Exchange 2013 e Lync Server

 

_**Aplica-se a:**Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:**2016-12-09_

A UM (Unificação de Mensagens) e o Microsoft Lync Server podem ser implantados juntos para fornecer mensagem de voz, mensagens instantâneas, presença de usuário avançada, conferência de áudio e vídeo e uma experiência integrada de email e mensagem para os usuários de sua organização. A Unificação de Mensagens é usada para fornecer atendimento de chamadas para caixa postal, Outlook Voice Access e serviços de atendedor automático. O Microsoft Lync Server habilita recursos mais avançados encontrados no Enterprise Voice, como sistema de mensagens instantâneas (IM), conferências e chamadas de entrada e saída. Este tópico descreve como configurar a Unificação de Mensagens e o Microsoft Lync Server para oferecer suporte a esses recursos.


> [!TIP]
> O Microsoft Office Communications Server 2007 R2 também pode ser implantado junto com a Unificação de Mensagens. Neste tópico, &amp;quot;Microsoft Lync Server&amp;quot; se refere ao Microsoft Lync Server 2010 ou ao Microsoft Lync Server 2013.



Procurando mais informações sobre o Microsoft Lync Server? Consulte [Microsoft Lync Server](https://go.microsoft.com/fwlink/p/?linkid=265752).

**Sumário**

Deploying Exchange UM and Lync Server overview

Certificate configuration recommendations

Deployment steps

For more information

## Visão geral da implantação da UM do Exchange e do Lync Server

A Unificação de Mensagens combina mensagens de voz e email em uma única infraestrutura de mensagens. O Microsoft Lync Server Enterprise Voice aproveita a infraestrutura da UM para oferecer caixa postal, Outlook Voice Access, notificações de chamadas e atendedores automáticos.

A lista a seguir mostra as etapas simplificadas de implantação da UM e do Lync Server. Detalhes sobre cada etapa estão incluídos mais adiante neste tópico.

1.  Instale o Microsoft Lync Server na mesma topologia na qual serão instalados os servidores de Acesso para Cliente executando o serviço Roteador de Chamadas da Unificação de Mensagens do Microsoft Exchange e os servidores de Caixa de Correio executando o serviço de Unificação de Mensagens do Microsoft Exchange. Confirme que ao menos um pool do Lync tenha sido criado.

2.  Instale um certificado válido e assinado por uma autoridade de certificação (CA) privada ou pública, e que tenha a confiança do Lync Server.

3.  Instale os servidores de acesso para cliente e servidores de caixa de correio. Verificar a instalação.

4.  Instale um certificado válido e assinado pela mesma CA que o certificado que você instalou em seus servidores do Lync.

5.  Crie e configure um plano de discagem URI do protocolo SIP.

6.  Adicione todos os servidores de Acesso para Cliente e Caixa de Correio ao plano de discagem URI do SIP. Porém, se tiver vários planos de discagem URI do SIP, você terá que adicionar todos os servidores de Acesso para Cliente e Caixa de Correio aos planos de discagem URI do SIP.

7.  Execute o script ExchUcUtil.ps1 na pasta \<pasta de instalação do Exchange\>\\Exchange Server\\Script em um servidor de Caixa de Correio.
    

    > [!IMPORTANT]
    > O script ExchUcUtil.ps1 cria um ou mais gateways para integração do Lync. Você deve desabilitar as chamadas de saída em todos os gateways IP de UM com exceção do gateway criado pelo script. Isto inclui desabilitar as chamadas de saída nos gateways IP de UM que foram criados antes de você executar o script. Para desabilitar as chamadas de saída em um gateway IP de UM, consulte <A href="disable-outgoing-calls-on-um-ip-gateways-exchange-2013-help.md">Desabilitar as chamadas de saída nos gateways IP de UM</A>.



8.  Execute **OcsUmUtil.exe** na pasta %CommonProgramFiles%\\Microsoft Lync Server 2013\\Support em um Lync Server.

9.  Implante o servidor de mediação e os gateways de mídia.

10. Instale em seu servidor de mediação um certificado válido e assinado pela mesma CA que o certificado que você instalou em seus servidores do Lync.

11. Habilite seus usuários para a UM e o Enterprise Voice.

## Recomendações de configuração de certificados

Você precisa ter um certificado que tenha a confiança dos computadores que executam o Exchange e dos computadores que executam o Lync Server. Em um ambiente que tem o Lync Server e a Unificação de Mensagens, use as seguintes diretrizes para implantar um certificado confiável:

  - Em seus servidores do Lync, servidores de Acesso para Cliente, servidores de Caixa de Correio, no servidor de mediação e nos gateways de mídia, importe um certificado válido e assinado por uma CA privada ou pública. Ele deve ser um certificado comercial de terceiros confiáveis, ou um certificado de infraestrutura de chave pública (PKI).

  - É menos complexo se você importar o mesmo certificado comercial de terceiros ou de PKI para cada servidor do Exchange. Além disso, instale esse certificado confiável em cada computador executando o Microsoft Lync Server e o servidor de mediação. Isso tornará a implantação do certificado menos complicada e reduzirá a sobrecarga administrativa associada à implantação de certificados. No entanto, não deixe de obter um certificado confiável com suporte a nomes alternativos de requerentes (SANs).
    
    Ao implantar o protocolo TLS com a UM, os certificados usados no servidor de Acesso para Cliente e no servidor de Caixa de Correio precisam conter o nome de domínio totalmente qualificado (FQDN) no Nome do Requerente do certificado. Para contornar esse problema, use um certificado público e importe o certificado em todos os servidores de Acesso para Cliente e Caixa de Correio, em quaisquer gateways VoIP, PBXs IP e em todos os servidores Lync.
    
    Se sua implantação incluir gateways VoIP ou PBXs IP, e se você usar um plano de discagem protegido ou protegido por SIP, um certificado confiável será exigido entre os servidores de Acesso para Cliente e Caixa de Correio e os gateways VoIP ou PBXs IP. Um certificado confiável também será necessário se uma conexão SIP direta for usada. Se usar um plano de discagem protegido ou protegido por SIP, você poderá usar o mesmo certificado confiável em seus servidores do Lync e do Exchange que usou em seus gateways VoIP ou PBXs IP.

  - Ao conectar servidores de Acesso para Cliente e Caixa de Correio do Exchange aos servidores do Microsoft Lync ou a gateways SIP de terceiros ou a um equipamento PBX de telefonia, você deve usar um certificado válido e assinado por uma autoridade de certificação interna ou pública para estabelecer sessões protegidas. É possível usar um único certificado em todos os servidores de Acesso para Cliente e Caixa de Correio enquanto ele possuir os FQDNs de todos os servidores de Acesso para Cliente e Caixa de Correio em sua lista SAN. Ou você pode gerar um certificado diferente para cada servidor de Acesso para Cliente e Caixa de Correio, com o FQDN do computador local presente no nome comum (CN) do requerente ou na lista de SAN do certificado do servidor. A UM do Exchange não oferece suporte a certificados curinga com o Microsoft Lync Server.
    
    Um Nome do Requerente sem curinga é exigido para que o Lync Server e o Exchange trabalhem juntos. A UM e o Lync Server usam o Nome do Requerente como uma maneira de indicar que eles são pares SIP confiáveis. O Lync Server também precisa de um Nome do Requerente sem curinga em alguns cenários de roteamento de chamadas. O FQDN deve ser usado como o valor "Emitido para".
    
    Não há suporte a nomes de certificado com curinga na UM do Exchange. No entanto, você pode colocar um curinga na SAN.

A tabela a seguir mostra os requisitos de certificados para a instalação e a configuração de certificados para a UM do Exchange.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Topologia</th>
<th>Configuração do certificado</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Acesso para Cliente e Caixa de Correio no mesmo servidor (sem Lync 2010 ou 2013; planos de discagem não SIP)</p></td>
<td><p>Um certificado é necessário entre os servidores de Acesso para Cliente e Caixa de Correio. Trata-se do mesmo certificado usado entre os servidores de Acesso para Cliente e Caixa de Correio e o gateway VoIP, PBX IP ou SBC.</p></td>
</tr>
<tr class="even">
<td><p>Servidores de Acesso para Cliente e Caixa de Correio em servidores diferentes (sem Lync 2010 ou 2013; planos de discagem não SIP)</p></td>
<td><p>É necessário um certificado. O certificado deve corresponder nos servidores de Acesso para Cliente e Caixa de Correio. Também é necessário um certificado entre os servidores de Acesso para Cliente e Caixa de Correio e o gateway VoIP, PBX IP ou SBC. Pode ser o mesmo certificado ou um certificado diferente do usado entre os servidores de Acesso para Cliente e Caixa de Correio. Para os servidores de Acesso para Cliente e Caixa de Correio, você pode executar o cmdlet <strong>Create-ExchangeCertificate</strong> a partir de qualquer dos servidores.</p></td>
</tr>
<tr class="odd">
<td><p>Acesso para Cliente e Caixa de Correio no mesmo servidor (com Lync 2010 ou 2013 e planos de discagem SIP)</p></td>
<td><p>É necessário um certificado. Os servidores de acesso para cliente e caixa de correio devem ter o mesmo certificado raiz, como o Lync 2010 ou 2013 servidores.</p></td>
</tr>
<tr class="even">
<td><p>Servidores de Acesso para Cliente e Caixa de Correio em servidores diferentes (com Lync 2010 ou 2013 e planos de discagem SIP)</p></td>
<td><p>É necessário um certificado. Os servidores de acesso para cliente e caixa de correio devem ter o mesmo certificado raiz como o Lync 2010 ou 2013 servidores.</p></td>
</tr>
</tbody>
</table>


Voltar ao início

## Etapas de implantação

Depois da instalação dos servidores exigidos em sua organização, há uma sequência recomendada de etapas que você deve realizar nas suas implantações de Unificação de Mensagens do Exchange e do Lync Server para que você implante corretamente o Enterprise Voice para seus usuários.

Para obter detalhes sobre o Microsoft Lync Server, consulte [Microsoft Lync Server](https://go.microsoft.com/fwlink/p/?linkid=265752).

Você deve concluir as seguintes etapas para configurar a Unificação de Mensagens para operar com os recursos do Enterprise Voice no Lync Server:

1.  Crie um ou mais planos de discagem de URI de protocolo SIP de Unificação de Mensagens, cada um sendo mapeado para um perfil da localidade correspondente do Lync Server. Um perfil de local do Enterprise Voice deve ser criado para cada plano de discagem do UM do Exchange. Você pode usar o cmdlet **Get-UMDialPlan** para obter o FQDN de um plano de discagem URI de SIP. Para obter mais informações sobre como criar um plano de discagem SIP URI, consulte [Criar um plano de discagem de UM](create-a-um-dial-plan-exchange-2013-help.md).
    

    > [!IMPORTANT]
    > Durante a integração da UM do Exchange e do Lync Server, provavelmente não será necessário configurar regras de discagem ou grupos de regras de discagem na UM do Exchange. O Lync Server foi projetado para realizar o roteamento de chamadas e algumas conversões de números para usuários de sua organização e também faz isso quando as chamadas são feitas da Unificação de Mensagens em nome dos usuários.



2.  Instale um certificado nos servidores de Acesso para Cliente e Caixa de Correio que seja válido e assinado por uma CA privada ou pública. Esta é a mesma CA usada nos servidores Lync.

3.  Criptografe o tráfego de voz sobre IP (VoIP) configurando o plano de discagem de URI de SIP como SIP Protegido ou Protegido.
    

    > [!WARNING]
    > Se você definir suas configurações de segurança como SIP Protegido para exigir criptografia apenas para tráfego SIP, a configuração não será suficiente em um plano de discagem se o pool de Front-End estiver configurado para exigir criptografia (o que significa que o pool exige criptografia para tráfego SIP e RTP). Quando as configurações de segurança do plano de discagem e do pool não são compatíveis, todas as chamadas para a UM do Exchange vindas do pool Front-End falharão, resultando em um erro que indica que você tem uma &amp;quot;Configuração de segurança incompatível&amp;quot;.

    
    Embora um plano de discagem da UM possa ser configurado como SIP Protegido ou Protegido, recomendamos configurar o plano de discagem como Protegido para permitir que os dispositivos do Lync Phone Edition funcionem corretamente. Isso é recomendável devido às configurações padrão de nível de criptografia configuradas no Lync Server. Um dispositivo Lync Phone Edition só funcionará se as configurações de criptografia forem definidas como mostra a tabela a seguir. Esta tabela mostra o relacionamento entre as configurações de criptografia dos planos de discagem da UM e do Lync Server.
    
    **Configurações de criptografia do Lync Phone Edition**
    
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>Servidor Lync</th>
    <th>Plano de discagem do UM</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>Criptografia necessária (padrão)</p></td>
    <td><p>Protegido</p></td>
    </tr>
    <tr class="even">
    <td><p>Criptografia opcional</p></td>
    <td><p>SIP Protegido/Protegido</p></td>
    </tr>
    <tr class="odd">
    <td><p>Sem criptografia</p></td>
    <td><p>SIP protegido</p></td>
    </tr>
    </tbody>
    </table>


4.  Adicione todos os servidores de Acesso para Cliente e Caixa de Correio ao plano de discagem SIP. Para permitir que o servidor responda às chamadas recebidas, adicione todos os servidores do Exchange a um plano de discagem se quiser que eles atendam às chamadas do Lync Server.

5.  Defina o modo de inicialização e a porta de escuta de TLS nos servidores de Acesso para Cliente e Caixa de Correio que são adicionados ao plano de discagem URI de SIP e reinicie o serviço de Unificação de Mensagens do MicrosoftExchange em cada servidor de Caixa de Correio e o serviço Roteador de Chamadas da Unificação de Mensagens do MicrosoftExchange em cada servidor de Acesso para Cliente.

6.  Criar e configurar um atendedor automático de UM. Para detalhes, consulte [Configurar um atendedor automático](set-up-a-um-auto-attendant-exchange-2013-help.md).

7.  Ao habilitar os usuários para caixa postal, crie um endereço SIP para os usuários que usarão o Enterprise Voice. Na maioria dos casos, esse endereço SIP será igual ao endereço SIP usado quando um usuário for habilitado para o Enterprise Voice. Para detalhes, consulte [Habilitar um usuário para caixa postal](enable-a-user-for-voice-mail-exchange-2013-help.md).
    

    > [!IMPORTANT]
    > Os usuários associados a um plano de discagem URI de SIP não podem receber faxes. Isso ocorre porque as chamadas de fax e voz de entrada são roteadas por um Servidor de Mediação e não há suporte para fax quando você está usando um Servidor de Mediação.



8.  Abra o Shell de Gerenciamento do Exchange e execute o script exchucutil.ps1 localizado na pasta %Program Files%\\Microsoft\\Exchange Server\\V15\\Scripts. O script exchucutil.ps1 faz o seguinte:
    
      - Concede permissão ao Lync Server para ler Exchange componentes de Active Directory de Unificação de MENSAGENS, especificamente, o plano de discagem URI do SIP que foi criado na tarefa anterior. Para obter detalhes sobre como configurar permissões no Active Directory, consulte [como usar o ADSI Edit para aplicar permissões](https://go.microsoft.com/fwlink/p/?linkid=82751).
    
      - Cria um gateway IP da UM para cada pool do Lync Server ou para cada servidor executando o Lync Server Standard Edition que hospeda os usuários que serão habilitados para o Enterprise Voice. Para detalhes, consulte [Criar um gateway IP de UM](create-a-um-ip-gateway-exchange-2013-help.md).
    
      - Crie um grupo de busca da UM do Exchange para cada gateway IP da UM. O identificador piloto do grupo de busca terá o nome do plano de discagem associado ao gateway IP da UM correspondente. O grupo de busca precisa especificar o plano de discagem SIP da UM com o gateway IP da UM.

9.  Habilite os usuários para caixa postal. Quando você os habilitar, confira se você informou um endereço SIP válido para o usuário e vincule-os a um plano de discagem SIP. Para detalhes, consulte [Habilitar um usuário para caixa postal](enable-a-user-for-voice-mail-exchange-2013-help.md).

Também é necessário concluir as seguintes tarefas para configurar o Lync Server para funcionar com a UM do Exchange:

  - Crie perfis de local ou planos de discagem do Lync. O nome do perfil da localidade não precisa corresponder ao FQDN dos planos de discagem da UM correspondentes.

  - Atribua perfis de local aos pools do Lync Server.

  - Implante e configure gateways de mídia ou Servidores de Mediação. Você também precisa importar um certificado da mesma CA confiável usada para os certificados nos servidores de Acesso para Cliente e Caixa de Correio e o Lync Server.

  - Defina usos de telefone, crie e atribua políticas de voz e rotas de chamada de saída.

  - Configure os usuários para o Enterprise Voice e adicione um identificador SIP e URI de TEL.

  - Execute **ocsumutil.exe**, que cria os objetos de contato para o Outlook Voice Access e para o atendedor automático.
    

    > [!TIP]
    > Quando você instala o Lync Server, o atributo <STRONG>msRTC-SIPLine</STRONG> é adicionado ao Active Directory. Se você não tiver instalado o Lync Server em seu ambiente, o atributo não será adicionado ao Active Directory, e a resolução de nome de ID do chamador entre planos de discagem em uma única floresta e em cenários entre florestas não irá funcionar corretamente, a menos que você configure os endereços de proxy da Unificação de Mensagens para usuários que não sejam habilitados para UM.



Depois de ter configurado o Lync Server e os servidores de Unificação de Mensagens, é necessário habilitar o usuário a utilizar o Lync Server e instalar o Lync no computador cliente do usuário.


> [!IMPORTANT]
> Quando você estiver integrando a Unificação de Mensagens e o Servidor Lync, as notificações de chamada perdidas não estarão disponíveis para usuários que tenham uma caixa de correio localizada em um servidor de Caixa de Correio Exchange 2007 ou Exchange 2010. Uma notificação de chamada perdida será gerada quando um usuário se desconectar antes de a chamada ser enviada para um servidor de Caixa de Correio.



Voltar ao início

## Para obter mais informações

Para obter mais informações sobre como executar as tarefas que devem ser concluídas para o Microsoft Lync Server, consulte [Microsoft Lync Server](https://go.microsoft.com/fwlink/p/?linkid=265752).

