---
title: 'Pré-requisitos de implantação híbrida: Exchange 2013 Help'
TOCTitle: Pré-requisitos de implantação híbrida
ms:assetid: e7454db0-fed4-4662-8890-9501126b1ba2
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Hh534377(v=EXCHG.150)
ms:contentKeyID: 50487122
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Pré-requisitos de implantação híbrida

 

_<strong>Aplica-se a:</strong>Exchange Online, Exchange Server 2013, Exchange Server 2016_

_<strong>Tópico modificado em:</strong>2017-07-25_

**Resumo:**  Do que o seu ambiente do Exchange precisa antes de você poder configurar uma implantação híbrida.

Antes de você criar e configurar uma implantação híbrida usando o assistente de Configuração Híbrida, sua organização local do Exchange existente precisa atender a determinados requisitos. Se você não atender a estes requisitos, não será capaz de concluir as etapas do assistente de Configuração Híbrida e não conseguirá configurar uma implantação híbrida entre a organização local do Exchange e o Exchange Online.

## Pré-requisitos da implantação híbrida

Os pré-requisitos a seguir são necessários para configurar uma implantação híbrida:

  - **Organização local do Exchange**   As implantações híbridas podem ser configuradas para organizações locais baseadas no Exchange 2007 ou versão posterior.
    
    A versão do Exchange que você instalou em sua organização local determina a versão da implantação híbrida que pode ser instalada. Normalmente, você deve configurar a versão mais recente da implantação híbrida que seja compatível com sua organização. Por exemplo, se sua organização local estiver executando o Exchange 2007, você precisará configurar uma implantação híbrida baseada no Exchange 2013. Para ver uma lista completa do Exchange Server e do Office 365 para compatibilidade de implantação híbrida corporativa, confira a tabela a seguir.
    
    
    <table>
    <colgroup>
    <col style="width: 25%" />
    <col style="width: 25%" />
    <col style="width: 25%" />
    <col style="width: 25%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>Ambiente no local</th>
    <th>Implantação híbrida com base no Exchange 2016</th>
    <th>Implantação híbrida com base no Exchange 2013</th>
    <th>Implantação híbrida com base no Exchange 2010</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>Exchange 2016</p></td>
    <td><p>Com suporte</p></td>
    <td><p>Sem suporte</p></td>
    <td><p>Sem suporte</p></td>
    </tr>
    <tr class="even">
    <td><p>Exchange 2013</p></td>
    <td><p>Com suporte</p></td>
    <td><p>Com suporte</p></td>
    <td><p>Sem suporte</p></td>
    </tr>
    <tr class="odd">
    <td><p>Exchange 2010</p></td>
    <td><p>Com suporte</p></td>
    <td><p>Com suporte</p></td>
    <td><p>Com suporte</p></td>
    </tr>
    <tr class="even">
    <td><p>Exchange 2007</p></td>
    <td><p>Sem suporte</p></td>
    <td><p>Com suporte</p></td>
    <td><p>Com suporte</p></td>
    </tr>
    </tbody>
    </table>


  - **Versões do Exchange local** As implantações híbridas exigem a atualização cumulativa ou o pacote cumulativo de atualização mais recentes disponíveis para a versão do Exchange instalada em sua organização local. Se você não conseguir instalar a atualização cumulativa ou o pacote cumulativo de atualização mais recente, use a versão anterior que também é compatível. As atualizações cumulativas ou os pacotes cumulativos de atualização mais antigos não são compatíveis.
    
    Por exemplo, suponha que você tenha instalado a Atualização Cumulativa 8 do Exchange 2013 em sua organização local e a versão mais recente disponível da Atualização Cumulativa 10 do Exchange 2013. Para permanecer em uma configuração híbrida com suporte, você precisa atualizar seus servidores do Exchange 2013 com, no mínimo, a Atualização Cumulativa 9. No entanto, recomendamos atualizar para a Atualização Cumulativa 10.
    
    As atualizações cumulativas ou os pacotes cumulativos de atualização são lançados em uma cadência trimestral. Manter seus servidores com a atualização cumulativa ou pacote cumulativo de atualização mais recente oferece-lhe maior flexibilidade se você precisar de mais tempo para concluir atualizações periodicamente.

  - **Funções de servidor local** As funções de servidor que você precisa instalar em sua organização local dependem da versão do Exchange que você instalou.
    
      - **Exchange 2010:**  pelo menos um servidor com as funções de servidor de Acesso para Cliente, de Caixa de Correio e de Transporte de Hub instaladas. Embora seja possível instalar as funções de servidor de Acesso para Cliente, de Caixa de Correio e de Transporte de Hub em servidores separados, é altamente recomendável instalar todas as funções em todos os servidores para fornecer o melhor desempenho e confiabilidade adicional.
    
      - **Exchange 2013:**  pelo menos um servidor com as funções de servidor de Acesso para Cliente e de Caixa de Correio instaladas. Embora seja possível instalar as funções de servidor de Acesso para Cliente e de Caixa de Correio em servidores separados, é altamente recomendável instalar as duas funções em todos os servidores para fornecer o melhor desempenho e confiabilidade adicional.
    
      - **Exchange 2016 e versões mais recentes** Pelo menos um servidor que tem a função de servidor de Caixa de Correio instalada.
    
    As implantações híbridas também oferecem suporte aos servidores do Exchange que executam a função de servidor de Transporte de Borda. Os servidores de Transporte de Borda também precisam ser atualizados para a atualização cumulativa ou pacote cumulativo de atualização mais recente disponível para a versão do Exchange que você instalou. É altamente recomendável implantar servidores de Transporte de Borda em uma rede de perímetro. Servidores de Caixa de Correio e Acesso para Cliente não podem ser implantados em uma rede de perímetro.

  - **Office 365**   Implantações híbridas são compatíveis com todos os planos do Office 365 que oferecem suporte para Sincronização do Azure Active Directory. Todos os planos do Office 365, Enterprise, Government, Academic e Midsize, dão suporte a implantações híbridas. Os planos do Office 365 Business e Home não dão suporte a implantações híbridas.
    
    Saiba mais em [Assinar o Office 365](https://go.microsoft.com/fwlink/p/?linkid=203981).

  - **Domínios personalizados** Registre quaisquer domínios personalizados que deseja utilizar na sua implantação híbrida do Office 365. É possível fazer isso utilizando o portal Administrativo do Office 365 ou opcionalmente configurando os Serviços de Federação do Active Directory (AD FS) em sua organização local.
    
    Saiba mais em [Adicionar seu domínio ao Office 365](https://go.microsoft.com/fwlink/p/?linkid=229238).

  - **Sincronização do Active Directory**   Implante a ferramenta Azure Active Directory Connect para habilitar a sincronização de Active Directory com a sua organização local.
    
    Saiba mais em [Opções de logon único de usuário do Azure AD Connect](http://go.microsoft.com/fwlink/p/?linkid=723514).

  - **Registros de DNS de Autodescoberta**   Configure os registros públicos do DNS de Autodescoberta para os seus domínios SMTP existentes para apontar para um Exchange 2013 servidor de Acesso do Cliente no local.

  - **Organização do Office 365 no EAC (Centro de administração do Exchange)**   O nó da organização do Office 365 está incluído por padrão no EAC local, mas você deve conectar o EAC à sua organização do Office 365 usando suas credenciais de administrador do Office 365 antes de poder usar o assistente da Configuração Híbrida. Isso também permite o gerenciamento de ambas as organizações, local e do Exchange Online, a partir de um console único de gerenciamento.
    
    Saiba mais em [Gerenciamento híbrido em implantações híbridas do Exchange](hybrid-management-in-exchange-hybrid-deployments-exchange-2013-help.md).

  - 
    
    **Certificados**   Instale e atribua serviços do Exchange a um certificado digital válido adquirido com uma autoridade de certificação (CA) pública confiável. Ainda que os certificados autoassinados devam ser usados para confiança de federação local com o Microsoft Federation Gateway, os certificados autoassinados não podem ser usados para serviços do Exchange em uma implantação híbrida. A instância dos IIS (Serviços de Informação de Internet) nos servidores do Exchange configurados na implantação híbrida deve ter um certificado digital válido adquirido com uma CA confiável. Além disso, a URL externa do EWS e o ponto de extremidade de Descoberta Automática especificada em seu DNS público devem estar listados no SAN (Nome alternativo da entidade) do certificado. O certificado instalado nos servidores do Exchange usados para o transporte de emails na implantação híbrida deve usar o mesmo certificado (ou seja, ser emitido pela mesma CA e ter a mesmo entidade).
    
    Saiba mais em [Requisitos de certificado para implantações híbridas](certificate-requirements-for-hybrid-deployments-exchange-2013-help.md).

  - **EdgeSync**   Se você implantou servidores de Transporte de Borda em sua organização local e deseja configurar os servidores de Transporte de Borda para o transporte de email seguro, é necessário configurar o EdgeSync antes de usar o assistente de Configuração Híbrida. Você também precisa executar o EdgeSync sempre que aplicar uma nova atualização ou pacote cumulativo em um servidor de Transporte de Borda.
    

    > [!IMPORTANT]
    > Ainda que o EdgeSync é um requisito nas implantações com os servidores de Edge Transport, as definições da configuração de transporte manual adicional serão necessárias quando você configurar os servidores de Edge Transport para o transporte de correio híbrido seguro.

    
    Saiba mais em [Servidores de transporte de borda com implantações híbridas](edge-transport-servers-with-hybrid-deployments-exchange-2013-help.md).

  - **Caixas de correio habilitadas para Unificação de Mensagens (UM)**   Se você tem caixas de correio habilitadas para UM e quer movê-las para o Office 365, é preciso o seguinte, além de uma implantação híbrida do Exchange. Esses requisitos devem ser atendidos **antes** de mover qualquer caixa de correio habilitada para UM para o Office 365.
    
      - Lync Server 2010, Lync Server 2013 ou Skype for Business Server 2015 ou posterior integrado ao seu sistema de telefonia no local **ou**
    
      - Skype for Business Online integrado ao sistema de telefonia local **ou**
    
      - Uma solução de PBX ou IP-PBX local tradicional.
    
      - Políticas de caixa de correio de UM criadas no Exchange Online que espelhem os nomes das políticas de caixa de correio de UM na sua organização local.
        

        > [!TIP]
        > Você pode mapear várias políticas de caixa de correio UM no local para uma política de caixa de correio no Exchange Online. Se você quiser fazer isso, é preciso usar o Shell de Gerenciamento do Exchange para mapear manualmente cada política de caixa de correio de UM local para uma política do Exchange Online.

    
    Para obter mais informações, confira [Integração com a Unificação de MENSAGENS do sistema de telefone](https://technet.microsoft.com/pt-br/library/jj673558\(v=exchg.150\)), [Supervisor de telefonia para o Exchange 2013](https://technet.microsoft.com/pt-br/library/ee364753\(v=exchg.150\)) e [Configurar a caixa postal do Cloud PBX](https://go.microsoft.com/fwlink/p/?linkid=826207).

## Protocolos, portas e pontos de extremidade da implantação híbrida

Os recursos e componentes de implantação híbrida exigem que determinados protocolos de entrada, portas e pontos de extremidade de conexão estejam acessíveis ao Office 365 para funcionar corretamente. Antes de configurar a implantação híbrida, verifique na tabela a seguir se a configuração local de rede e segurança é compatível com os recursos e componentes. Além de permitir protocolos de entrada, portas e pontos de extremidade específicos, os computadores da rede também precisam acessar os endereços IP, as portas e URLs relacionados no artigo [URLs e intervalos de endereços IP do Office 365](https://go.microsoft.com/fwlink/?linkid=823100).


<table>
<colgroup>
<col style="width: 12%" />
<col style="width: 12%" />
<col style="width: 12%" />
<col style="width: 12%" />
<col style="width: 12%" />
<col style="width: 12%" />
<col style="width: 12%" />
<col style="width: 12%" />
</colgroup>
<thead>
<tr class="header">
<th>Protocolo de transporte</th>
<th>Protocolo de nível superior</th>
<th>Recurso/componente</th>
<th>Ponto de extremidade local</th>
<th>Caminho local</th>
<th>Provedor de autenticação</th>
<th>Método de autorização</th>
<th>Suporte para pré-autenticação?</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>TCP 25 (SMTP)</p></td>
<td><p>SMTP/TLS</p></td>
<td><p>Fluxo de emails entre o Office 365 e o local</p></td>
<td><p>Caixa de Correio/Edge do Exchange 2016</p>
<p>CAS/Edge do Exchange 2013</p>
<p>HUB/EDGE do Exchange 2010</p></td>
<td><p>N/D</p></td>
<td><p>N/D</p></td>
<td><p>Baseado em certificado</p></td>
<td><p>Não</p></td>
</tr>
<tr class="even">
<td><p>TCP 443 (HTTPS)</p></td>
<td><p>Descoberta Automática</p></td>
<td><p>Descoberta Automática</p></td>
<td><p>Caixa de Correio do Exchange 2016</p>
<p>CAS do Exchange 2013/2010</p></td>
<td><p>/autodiscover/autodiscover.svc/wssecurity</p>
<p>/autodiscover/autodiscover.svc</p></td>
<td><p>Sistema de autenticação do AD do Azure</p></td>
<td><p>Autenticação de segurança WS</p></td>
<td><p>Não</p></td>
</tr>
<tr class="odd">
<td><p>TCP 443 (HTTPS)</p></td>
<td><p>EWS</p></td>
<td><p>Disponibilidade, Dicas de Email, rastreamento de mensagem</p></td>
<td><p>Caixa de Correio do Exchange 2016</p>
<p>CAS do Exchange 2013/2010</p></td>
<td><p>/ews/exchange.asmx/wssecurity</p></td>
<td><p>Sistema de autenticação do AD do Azure</p></td>
<td><p>Autenticação de segurança WS</p></td>
<td><p>Não</p></td>
</tr>
<tr class="even">
<td><p>TCP 443 (HTTPS)</p></td>
<td><p>EWS</p></td>
<td><p>Pesquisa de várias caixas de correio</p></td>
<td><p>Caixa de Correio do Exchange 2016</p>
<p>CAS do Exchange 2013/2010</p></td>
<td><p>/ews/exchange.asmx/wssecurity</p>
<p>/autodiscover/autodiscover.svc/wssecurity</p>
<p>/autodiscover/autodiscover.svc</p></td>
<td><p>Servidor de autenticação</p></td>
<td><p>Autenticação de segurança WS</p></td>
<td><p>Não</p></td>
</tr>
<tr class="odd">
<td><p>TCP 443 (HTTPS)</p></td>
<td><p>EWS</p></td>
<td><p>Migrações de caixas de correio</p></td>
<td><p>Caixa de Correio do Exchange 2016</p>
<p>CAS do Exchange 2013/2010</p></td>
<td><p>/ews/mrsproxy.svc</p></td>
<td><p>NTLM</p></td>
<td><p>Básica</p></td>
<td><p>Sim</p></td>
</tr>
<tr class="even">
<td><p>TCP 443 (HTTPS)</p></td>
<td><p>Descoberta Automática</p>
<p>EWS</p></td>
<td><p>OAuth</p></td>
<td><p>Caixa de Correio do Exchange 2016</p>
<p>CAS do Exchange 2013/2010</p></td>
<td><p>/ews/exchange.asmx/wssecurity</p>
<p>/autodiscover/autodiscover.svc/wssecurity</p>
<p>/autodiscover/autodiscover.svc</p></td>
<td><p>Servidor de autenticação</p></td>
<td><p>Autenticação de segurança WS</p></td>
<td><p>Não</p></td>
</tr>
<tr class="odd">
<td><p>TCP 443 (HTTPS)</p></td>
<td><p>N/D</p></td>
<td><p>AD FS (incluído no Windows)</p></td>
<td><p>Windows 2008/2012 Server</p></td>
<td><p>/adfs/*</p></td>
<td><p>Sistema de autenticação do AD do Azure</p></td>
<td><p>Varia por configuração</p></td>
<td><p>Dois fatores</p></td>
</tr>
<tr class="even">
<td><p>TCP 443 (HTTPS)</p></td>
<td><p>N/D</p></td>
<td><p>Azure Active Directory Connect com AD FS</p></td>
<td><p>Windows 2012 R2 Server</p></td>
<td><p>/adfs/*</p></td>
<td><p>Sistema de autenticação do AD do Azure</p></td>
<td><p>Varia por configuração</p></td>
<td><p>Dois fatores</p></td>
</tr>
</tbody>
</table>


## Ferramentas e serviços recomendados

Além disso os pré-requisitos necessários descritos anteriormente, outras ferramentas e serviços são úteis ao configurar as implantações híbridas com o assistente de Configuração Híbrida:

  - **Assistente de Implantação do Exchange Server**   O Assistente de Implantação do Exchange Server é uma ferramenta gratuita baseada na Web que ajuda você a implantar o Exchange em sua organização local, além de ajudar a configurar uma implantação híbrida entre a organização local e o Office 365 ou migrar completamente para o Office 365. A ferramenta faz algumas perguntas simples e, depois, com base em suas respostas, cria uma lista de verificação personalizada com instruções para implantação ou configuração do Exchange Server. O Assistente de Implantação fornece a você exatamente as informações necessárias para configurar sua implantação híbrida.
    
    Saiba mais em [Assistente de Implantação do Exchange Server](https://technet.microsoft.com/exdeploy2013).
    
     

  - **Analisador de Conectividade Remota**   O analisador de Conectividade Remota da Microsoft verifica a conectividade externa da sua organização local do Exchange e assegura que você está pronto para configurar sua implantação híbrida. É altamente aconselhável que você verifique sua organização local com a ferramenta Analisador de Conectividade Remota antes de configurar sua implantação híbrida com o assistente de Configuração Híbrida.
    
    Saiba mais em [Analisador de Conectividade Remota da Microsoft](http://go.microsoft.com/fwlink/p/?linkid=167905).
    
     

  - **Logon único**   O logon único permite que os usuários acessem as organizações locais e do Exchange Online com um único nome de usuário e senha. Ele fornece aos usuários uma experiência de logon conhecida e permite que os administradores controlem facilmente as políticas da conta das caixas de correio da organização do Exchange Online usando as ferramentas de gerenciamento locais do Active Directory .
    
    Você tem duas opções ao implantar o logon único: sincronização de senha e Serviços de Federação do Active Directory. As duas opções são fornecidas pelo Azure Active Directory Connect. A sincronização de senha permite que praticamente qualquer organização, independentemente do tamanho, implemente facilmente o logon único. Por esse motivo, e pela experiência do usuário em uma implantação híbrida ser consideravelmente melhor com o logon único habilitado, recomendamos sua implementação. Para organizações muito grandes, por exemplo, com várias florestas do Active Directory que precisam ingressar na implantação híbrida, os Serviços de Federação do Active Directory são obrigatórios.
    
    Saiba mais em [Logon único com implantações híbridas](single-sign-on-with-hybrid-deployments-exchange-2013-help.md).

