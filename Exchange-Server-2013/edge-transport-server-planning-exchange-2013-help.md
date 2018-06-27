---
title: 'Planejamento de servidor de Transporte de Borda: Exchange 2013 Help'
TOCTitle: Planejamento de servidor de Transporte de Borda
ms:assetid: 3d34de82-58a5-4b30-9978-7d330102eb92
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dn641596(v=EXCHG.150)
ms:contentKeyID: 61544118
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Planejamento de servidor de Transporte de Borda

 

_**Aplica-se a:**Exchange Server 2013_

_**Tópico modificado em:**2015-04-07_

A função de servidor de Transporte de Borda foi reintroduzida no Exchange Service Pack 1. O Transporte de Borda fornece proteção aprimorada antispam para a organização do Exchange. O servidor de Transporte de Borda também aplica diretivas a mensagens em transporte entre as organizações. Essa função de servidor é implantada na rede de perímetro e fora da floresta do Active Directory. Os servidores de Transporte de Borda não têm acesso direto ao Active Directory para obter informações de configuração e destinatário tal como têm os servidores de Acesso para Cliente ou de Caixa de Correio. O servidor de Transporte de Borda usa o Active Directory Lightweight Directory Service (AD LDS) para armazenar localmente as informações de configuração e destinatário.

É possível adicionar um servidor de Transporte de Borda a uma organização existente do Exchange 2013. Não é preciso executar qualquer etapa adicional de preparação do Active Directory ao instalar o servidor de Transporte de Borda.


> [!TIP]
> Se você estiver adicionando o transporte de borda para um existente Exchange 2010 ou Exchange 2007 organização, você precisará instalar atualizações de pacote cumulativo de atualizações específicas em seus servidores herdados antes de instalar o Exchange 2013 transporte de borda. Para obter detalhes, consulte <A href="exchange-2013-system-requirements-exchange-2013-help.md">Requisitos de sistema do Exchange 2013</A>.



Quando você estiver planejando implantar servidores de Transporte de Borda, deve considerar as seguintes questões:

  - **Capacidade do Servidor**   O planejamento da capacidade do servidor inclui planejar como conduzir o monitoramento de desempenho do servidor de Transporte de Borda. O monitoramento do desempenho ajudará você a entender com que intensidade o servidor está trabalhando. Essas informações determinarão a capacidade de sua configuração atual de hardware.

  - **Recursos de Transporte**   O servidor de Transporte de Borda pode fornecer proteção antispam na borda da rede. Como parte do processo de planejamento, você deve determinar os recursos antispam a serem habilitados no servidor de Transporte de Borda e como eles serão configurados.

  - **Segurança**   A função de servidor de Transporte de Borda é designada para ter uma superfície de ataque mínima. Portanto, é importante proteger corretamente e gerenciar o acesso físico e o acesso de rede ao servidor. O planejamento de segurança o ajudará a verificar se as conexões IP são habilitadas somente a partir de servidores autorizados e de usuários autorizados. Para obter mais informações, consulte [Lista de verificação de segurança de implantação](deployment-security-checklist-exchange-2013-help.md).
    
    A prática recomendada é colocar o servidor de Transporte de Borda na rede de perímetro. Para garantir que o servidor possa enviar e receber emails e receber atualizações de dados de configuração e de destinatário do serviço EdgeSync do Microsoft Exchange, você deve permitir a comunicação por meio das portas relacionadas na tabela a seguir.
    
    ### Configurações da porta de comunicação dos servidores de Transporte de Borda
    
    <table>
    <colgroup>
    <col style="width: 25%" />
    <col style="width: 25%" />
    <col style="width: 25%" />
    <col style="width: 25%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>Interface de rede</th>
    <th>Porta aberta</th>
    <th>Protocolo</th>
    <th>Observação</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>Entrada de e saída para a Internet</p></td>
    <td><p>25/TCP</p></td>
    <td><p>SMTP</p></td>
    <td><p>Essa porta é necessária para o fluxo de email para e da Internet.</p></td>
    </tr>
    <tr class="even">
    <td><p>Entrada de e saída para a rede interna</p></td>
    <td><p>25/TCP</p></td>
    <td><p>SMTP</p></td>
    <td><p>Essa porta é necessária para o fluxo de email para e da organização do Exchange.</p></td>
    </tr>
    <tr class="odd">
    <td><p>Somente local</p></td>
    <td><p>50389/TCP</p></td>
    <td><p>LDAP</p></td>
    <td><p>Esta porta é usada para fazer uma conexão local com AD LDS.</p></td>
    </tr>
    <tr class="even">
    <td><p>Entrada da rede interna</p></td>
    <td><p>50636/TCP</p></td>
    <td><p>LDAP seguro</p></td>
    <td><p>Essa porta é necessária para a sincronização de EdgeSync.</p></td>
    </tr>
    <tr class="odd">
    <td><p>Entrada da rede interna</p></td>
    <td><p>3389/TCP</p></td>
    <td><p>RDP</p></td>
    <td><p>A abertura desta porta é opcional. Ela fornece mais flexibilidade no gerenciamento dos servidores de Transporte de Borda com base na rede interna ao permitir que se use uma conexão de área de trabalho remota para gerenciar o servidor de Transporte de Borda.</p></td>
    </tr>
    </tbody>
    </table>
    

    > [!TIP]
    > A função de servidor Transporte de Borda usa portas LDAP não padrão. As portas especificadas neste tópico são as portas de comunicação LDAP configuradas quando a função de servidor de Transporte de Borda é instalada.



  - **EdgeSync**   O processo de implantação recomendado é criar uma Inscrição de Borda para inscrever o servidor de Transporte de Borda na organização do Exchange. Ao criar uma Inscrição de Borda, os dados de destinatário e configuração são replicados do Active Directory para o AD LDS. Inscreva o servidor de Transporte de Borda em um site do Active Directory. Em seguida, o serviço EdgeSync do Microsoft Exchange, que está em execução nos servidores de Caixa de Correio daquele site atualiza periodicamente o AD LDS sincronizando dados do Active Directory. O processo de Inscrição de Borda configura automaticamente os conectores de envio necessários para habilitar o fluxo de mensagens da organização do Exchange para a Internet por meio de um servidor de Transporte de Borda. Se você estiver usando a consulta de destinatários ou os recursos de agregação de lista segura no servidor de Transporte de Borda, deverá inscrever o servidor de Transporte de Borda na organização.

## Definir as configurações de DNS para a função de servidor de Transporte de Borda

A função de servidor de Transporte de Borda é implantada fora da organização do Exchange como um servidor autônomo na rede de perímetro ou como membro de um domínio do Active Directory da rede de perímetro. Você deve configurar manualmente o sufixo de DNS correto para a função de servidor de Transporte de Borda antes de instalar o Exchange 2013. Se um sufixo de DNS não for configurado, a instalação falhará.

Como o servidor de Transporte de Borda é implantado na rede de perímetro, há interfaces de rede que são conectadas a vários segmentos de rede. Cada um desses segmentos de rede tem uma configuração de IP exclusiva. A interface de rede conectada ao segmento de rede externa, ou pública, deve ser configurada para usar um servidor DNS público para resolução de nome. Isso permite ao servidor resolver nomes de domínio SMTP para registros de recurso MX e rotear o email para a Internet.

A interface de rede conectada ao segmento de rede interna, ou privada, deve ser configurada para usar um servidor DNS que possa resolver os nomes dos servidores de Caixa de Correio na sua organização ou deve ter um arquivo Hosts disponível. Os servidores de Transporte de Borda e de Caixa de Correio precisam usar a resolução de host de DNS para localizar um ao outro.

Para habilitar a resolução de nome dos servidores de Caixa de Correio pelos servidores de Transporte de Borda, use um dos seguintes métodos:

  - Crie manualmente registros de recurso para servidores de Caixa de Correio em uma zona de pesquisa direta no servidor DNS, que é configurada no adaptador de rede interna do servidor de Transporte de Borda.

  - Edite o arquivo Hosts no servidor de Transporte de Borda para incluir os registros Host nos servidores de Caixa de Correio. O arquivo Hosts é um arquivo de texto local no mesmo formato que o arquivo 4.3 Berkeley Software Distribution (BSD) UNIX /etc/hosts. Esse arquivo mapeia nomes de host para endereços IP e está armazenado na pasta \\%Systemroot%\\System32\\Drivers\\Etc.

Para habilitar a resolução de nome dos servidores de Transporte de Borda pelos servidores de Caixa de Correio, use um dos seguintes métodos:

  - Crie manualmente registros de recurso para servidores de Transporte de Borda em uma zona de pesquisa direta no servidor DNS, que é configurado no servidor de Caixa de Correio.

  - Para incluir os registros Host dos servidores de Transporte de Borda, edite o arquivo Hosts nos servidores de Caixa de Correio localizados no site inscrito do Active Directory.

Execute estas etapas para definir as configurações de DNS no servidor de Transporte de Borda:

1.  Verifique se as configurações do servidor DNS para cada interface de rede estão corretas para o segmento de rede.

2.  Configure o sufixo de DNS para o nome de servidor de Transporte de Borda usando as etapas a seguir:
    
    1.  Abra o Painel de Controle e selecione **Propriedades do Sistema**.
    
    2.  Selecione a guia **Nome do Computador**.
    
    3.  Selecione **Alterar**.
    
    4.  Na página **Alterações no Nome do Computador**, clique em **Mais**.
    
    5.  No campo **Sufixo DNS primário deste computador**, digite um nome de domínio e o sufixo de DNS para o servidor de Transporte de Borda.
    
    Esse nome não pode ser alterado depois que a função de servidor Transporte de Borda estiver instalada.

## Substituir configurações de DNS

Talvez seja necessário substituir a configuração padrão de DNS no servidor do Exchange para que o email possa ser roteado e entregue corretamente. Para fazer isso, altere as configurações **Pesquisas de DNS Interno** e **Pesquisas de DNS Externo** das propriedades do servidor de transporte. Essas configurações substituem as configurações no adaptador de rede para rotear mensagens de email.

