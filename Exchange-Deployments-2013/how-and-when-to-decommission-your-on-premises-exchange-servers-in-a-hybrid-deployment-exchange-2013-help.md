---
title: 'Como e quando encerrar seus servidores do Exchange locais em uma implantação híbrida: Exchange 2013 Help'
TOCTitle: Como e quando encerrar seus servidores do Exchange locais em uma implantação híbrida
ms:assetid: 4f884b7a-3b8a-4207-8843-65d3141731dc
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dn931280(v=EXCHG.150)
ms:contentKeyID: 65015122
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Como e quando encerrar seus servidores do Exchange locais em uma implantação híbrida

 

_**Aplica-se a:**Exchange Online, Exchange Server, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:**2017-07-27_

Leia este artigo se você estiver pronto para mover de uma implantação híbrida do Exchange para uma implementação de nuvem completa.

Uma das opções mais atraentes para obtenção de uma empresa para Exchange Online é usar a abordagem de implantação híbrido descrita na [implantação híbrida do Exchange e migração com o Office 365](https://msdn.microsoft.com/en-us/library/ff633682\(v=exchsrvcs.149\).aspx). Esta é a única opção que permite a facilmente integradas e de fora da placa de caixas de correio (todas as outras opções nativas são integradas apenas). Além do recurso de logoff tabuleiro, uma configuração híbrida possui as seguintes opções de chave.

Este tópico ajudará você a entender as opções para encerrar o Exchange híbrido e quando cada uma dessas opções devem ser implementada. Há muitas variações no quando e como encerrar servidores híbridos do Exchange. É importante dispor a entender as implicações e planejar corretamente o descomissionamento completo ou parcial dos servidores locais.

  - **Disponibilidade entre instalações**. Isso permite ver informações de disponibilidade de um usuário ao agendar uma reunião, independentemente do local da sua caixa de correio.

  - **Arquivo morto entre instalações**. Isso permite que um cliente mova apenas a caixa de correio de arquivo morto de um usuário para a nuvem. Esse geralmente é o primeiro passo para que os clientes experimentem o Office 365 e, mais especificamente, o Exchange Online.

  - **Pesquisas de descoberta entre instalações**. Isso permite que um cliente realize uma pesquisa de descoberta eletrônica que rastreará caixas de correio e arquivos mortos em ambos os locais (isso requer que você configure a autenticação OAuth).

  - **Redirecionamento de URL do Outlook Web App**. Isso permite que os usuários sejam redirecionados para o local apropriado para acesso ao Outlook Web App.

  - **Nenhuma recriação de perfil após a movimentação**. Diferentemente de outras opções de migração, o GUID da caixa de correio não é alterado. Isso significa que você não precisa recriar seu perfil nem baixar novamente o OST após mover uma caixa de correio.

Dependendo das necessidades da sua organização, uma implantação híbrida é a melhor opção para fornecer a melhor experiência de usuário e de coexistência.

## Outros métodos para migrar para o Exchange Online

Não é uma implantação híbrida para todas as pessoas; Na verdade, há opções geralmente é melhores. Muitos dos locatários que optaram por implantar uma configuração híbrida são estações em cinquenta. Enquanto a lista das vantagens de uma implantação híbrida possa parecer atraente, ele é fornecido com um preço pesado que estão relacionadas aos complexidade. Alguns dos locatários menores exigem que os recursos de uma implantação híbrida, mas, para a maioria dos locatários, seria uma melhor experiência para usar qualquer uma substituição, ser testado, ou uma opção de migração de IMAP. Não há um programa chamado FastTrack, você pode usar ao decidir na abordagem de migração para aproveitar. Informações sobre FastTrack são descritas na [página do Office 365 FastTrack](https://go.microsoft.com/fwlink/?linkid=846696).

Use a tabela a seguir para decidir qual tipo de migração funciona para sua organização. (Para obter mais informações, consulte [maneiras para migrar várias contas de email para o Office 365](https://support.office.com/en-us/article/ways-to-migrate-multiple-email-accounts-to-office-365-0a4913fe-60fb-498f-9155-a86516418842?ui=en-us%26rs=en-sg%26ad=sg))


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Organização existente</th>
<th>Número de caixas de correio a serem migradas</th>
<th>Você deseja gerenciar as contas dos usuários em sua organização local?</th>
<th>Tipos de migração</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange 2013, Exchange 2010, Exchange 2007 ou Exchange 2003</p></td>
<td><p>Menos que 2.000 caixas de correio</p></td>
<td><p>Não</p></td>
<td><p>Migrações de transferência do Exchange</p></td>
</tr>
<tr class="even">
<td><p>Exchange 2007 ou Exchange 2003</p></td>
<td><p>Menos que 2.000 caixas de correio</p></td>
<td><p>Não</p></td>
<td><p>Migração do Exchange em etapas</p></td>
</tr>
<tr class="odd">
<td><p>Exchange 2007 ou Exchange 2003</p></td>
<td><p>Mais de 2.000 caixas de correio*</p></td>
<td><p>Sim</p></td>
<td><p>Migração em estágios do Exchange ou migração de movimentação remota em uma implantação híbrida do Exchange</p></td>
</tr>
<tr class="even">
<td><p>Exchange 2013 ou Exchange 2010</p></td>
<td><p>Mais de 2.000 caixas de correio*</p></td>
<td><p>Sim</p></td>
<td><p>Migração de movimentação remota em uma implantação híbrida do Exchange</p></td>
</tr>
<tr class="odd">
<td><p>Exchange 2000 Server ou versões anteriores</p></td>
<td><p>Sem máximo</p></td>
<td><p>Sim</p></td>
<td><p>Migração IMAP</p></td>
</tr>
<tr class="even">
<td><p>Sistema de mensagens local não Exchange</p></td>
<td><p>Sem máximo</p></td>
<td><p>Sim</p></td>
<td><p>Migração IMAP</p></td>
</tr>
</tbody>
</table>


\* Algumas organizações com menos de 2.000 caixas de correio podem se beneficiar de recursos e capacidades que só estão disponíveis com uma implantação híbrida. É importante considerar cuidadosamente as vantagens de uma implantação híbrida com a complexidade que apresenta. É altamente recomendável que os clientes com menos de 2.000 caixas de correio considerar a substituição ou testado a migração antes de prosseguir com uma implantação híbrida.

## Por que não convém desativar servidores locais do Exchange

Com frequência, os clientes com uma configuração híbrida percebem após algum tempo que todas as suas caixas de correio foram movidas para o Exchange Online. Nesse ponto, eles podem decidir remover os servidores Exchange do local. No entanto, eles descobrem que não podem mais gerenciar suas caixas de correio na nuvem.

Quando a sincronização de diretório está habilitada para um locatário e um usuário é sincronizado do local, a maioria dos atributos não pode ser gerenciada por meio do Exchange Online e deve ser gerenciada no local. Isso não é devido à configuração híbrida, mas ocorre devido à sincronização de diretório. Além disso, mesmo que utilize a sincronização de diretório sem executar o Assistente de Configuração Híbrida, você ainda não poderá gerenciar a maioria das tarefas de destinatário na nuvem. Para saber mais, consulte este [blog do TechNet](http://blogs.technet.com/b/exchange/archive/2012/12/05/decommissioning-your-exchange-2010-servers-in-a-hybrid-deployment.aspx).

## Ferramentas de gerenciamento de terceiros podem ser usadas?

A pergunta quanto à possibilidade de usar uma ferramenta de gerenciamento de terceiros ou ADSIEDIT é feita com frequência. A resposta é que você pode usá-las, mas elas não têm suporte. O Console de Gerenciamento do Exchange, o EAC (Centro de Administração do Exchange) e o Shell de Gerenciamento do Exchange são as únicas ferramentas com suporte que estão disponíveis para gerenciar destinatários e objetos do Exchange. Se você decidir usar ferramentas de gerenciamento de terceiros, fará isso por sua conta e risco. As ferramentas de gerenciamento de terceiros muitas vezes funcionam bem, mas a Microsoft não valida essas ferramentas.

## Cenários comuns

Não é simples mudar de uma configuração híbrida para a nuvem. Levamos muito tempo para implementar corretamente o processo de adoção de uma configuração híbrida. Embora haja problemas, acreditamos que fizemos um trabalho muito bom, transformando a tarefa quase impossível de adotar uma configuração híbrida em um processo bastante fácil com base em assistente.

No entanto, não dedicamos muito tempo à transição de uma configuração híbrida para uma somente na nuvem. Dependendo das suas metas imediatas, esse processo pode ser bastante simples com alguma orientação. A seguir estão três cenários híbridos comuns, juntamente com a nossa recomendação sobre como alcançar adequadamente a meta final do cliente.

Como a base de clientes híbridos é muito diversificada, é difícil tentar encaixar todos eles em cenários "comuns". A seguir, tentamos mostrar alguns cenários de alto nível para desativar o Exchange Server. Portanto, ao ler sobre esses cenários e formar um plano para desativação, você precisará determinar o cenário que melhor se adapta às suas necessidades.

## Cenário um

**Problema:** minha organização está em execução em uma configuração híbrida e tenho todos de Meus caixas de correio em Exchange Online. Eu não precisará gerenciar meus usuários no local e não precisam de sincronização de diretório ou a sincronização de senha.

**Solução:** Como todos os usuários serão gerenciados no Office 365 e não há requisitos de sincronização de diretório adicionais, você pode desabilitar a sincronização de diretório com segurança e remover o Exchange do ambiente local.

![Remover o Exchange do ambiente local](images/Dn931280.f9c2a2cb-4c16-4ca3-8244-b89c1cdf0744(EXCHG.150).jpg "Remover o Exchange do ambiente local") Para desabilitar a sincronização de diretório e desinstalar o Exchange híbrido

1.  Execute `Get-OrganizationConfig |fl PublicFoldersEnabled` e certifique-se de que ele não está definido para remoto. Se estiver definida como remoto e as pastas públicas são algo que deseja continuar a acessar, precisaria migrá-los para Exchange Online. Para obter mais informações, consulte [Usar a migração de lotes para migrar as pastas públicas herdadas para o Office 365 e para o Exchange Online](https://technet.microsoft.com/pt-br/library/dn874017\(v=exchg.150\)).

2.  Supondo que já tenha movido todas as caixas de correio para o Exchange Online, você poderá apontar os registros MX e de DNS de Descoberta Automática para o Exchange Online, em vez de localmente. Para saber mais, consulte [Referência: registros de DNS externos para o Office 365](http://technet.microsoft.com/pt-br/library/hh852557.aspx).
    

    > [!IMPORTANT]
    > Atualize o DNS interno e externo, caso contrário, poderá ocorrer um comportamento de conectividade de cliente inconsistente.



3.  Em seguida, você deve remover os valores de SCP (Ponto de Conexão de Serviço) nos seus servidores Exchange. Isso garante que nenhum SCP será retornado e, em vez disso, o cliente usará o método de DNS para a Descoberta Automática. Um exemplo é mostrado abaixo:
    
        Get-ClientAccessServer | Set-ClientAccessServer -AutoDiscoverServiceInternalUri $Null
    

    > [!TIP]
    > Se tiver servidores do Exchange 2007 no ambiente, você terá que executar um comando semelhante nos servidores do Exchange 2007 para anular as configurações.



4.  Há conectores de entrada e saída criados pelo Assistente de Configuração Híbrida que convém excluir. Use as seguintes etapas para fazer isso:
    
    1.  Faça logon no [Portal de administração do Office 365](http://portal.office.com) e entre como Administrador de Locatários.
    
    2.  Selecione a opção para gerenciar o **Exchange**.
    
    3.  Navegue até **Fluxo de Emails** -\> **Conexão**.
    
    4.  Agora você pode desabilitar ou excluir os conectores de entrada e saída. O HCW cria conectores com o namespace exclusivo de **entrada do \<identificador exclusivo\>** e **saída do \<identificador exclusivo\>**, conforme mostrado na imagem abaixo.
        
        ![Assistente de Configuração Híbrida cria conectores com namespace exclusivo](images/Dn931280.7b1b6f0b-43d6-4407-8cd7-7dd52e016697(EXCHG.150).jpg "Assistente de Configuração Híbrida cria conectores com namespace exclusivo")  

5.  Remova a relação de organização criada pelo Assistente de Configuração Híbrida. Use as seguintes etapas para fazer isso:
    
    1.  Faça logon no [Portal de administração do Office 365](http://portal.office.com) e entre como Administrador de Locatários.
    
    2.  Selecione a opção para gerenciar o Exchange.
    
    3.  Navegue até **Organização**.
    
    4.  Em **Compartilhamento de Organização**, remova a organização chamada **O365 para Local – \<identificador exclusivo\>**, conforme mostrado na imagem abaixo.
        
        ![Remova o Relacionamento de Organização criado pelo Assistente de Configuração Híbrida.](images/Dn931280.2f0c1077-8785-487a-87a5-a75f0a4f0fea(EXCHG.150).jpg "Remova o Relacionamento de Organização criado pelo Assistente de Configuração Híbrida.")  

6.  Se o OAuth estiver configurado para uma implantação híbrida do Exchange, recomendável desabilitar a configuração no local e no Office 365. Na maioria dos ambientes, essas etapas podem ser ignoradas porque apenas um pequeno subconjunto de nossos clientes tem o OAuth configurado.
    
    Para desabilitar a configuração local:
    
    1.  Em um servidor Exchange 2013, abra o Shell de Gerenciamento do Exchange.
    
    2.  Execute:
        
            Get-IntraorganizationConnector -Identity ExchangeHybridOnPremisesToOnline | Set-IntraOrganizationConnector -Enabled $False
    
    Para desabilitar a configuração do Exchange Online:
    
    1.  Conecte o Windows PowerShell ao Exchange Online.
    
    2.  Execute:
        
            Run Get-IntraorganizationConnector -Identity ExchangeHybridOnlineToOnPremises | Set-IntraOrganizationConnector -Enabled $False
        
        O parâmetro *Identity* pressupõe que você tenha usado o Assistente de Configuração Híbrida para configurar o OAuth. Se esse não for o caso, talvez seja necessário ajustar o valor especificado para a identidade dos conectores.

7.  Desabilite a sincronização de diretório para seus locatários. Quando essa etapa for concluída, todas as tarefas de gerenciamento de usuário serão feitas por meio das ferramentas de gerenciamento do Office 365. Isso significa que você não usará mais o Console de Gerenciamento do Exchange nem o EAC (Centro de Administração do Exchange). Para saber mais sobre como desabilitar a sincronização de diretório, consulte [Desabilitar a sincronização de diretório](https://technet.microsoft.com/pt-br/library/dn144760.aspx).

8.  Agora você pode desinstalar o Exchange com segurança dos servidores locais.

## Cenário dois

**Problema:** A minha organização vem executando uma configuração híbrida há cerca de um ano e, finalmente, migrou a minha última caixa de correio para a nuvem. Planejo manter o AD FS (Serviços de Federação do Active Directory) para a autenticação de usuário de minhas caixas de correio do Exchange Online. (Este cenário se aplicaria a qualquer cliente que esteja planejando manter a sincronização de diretório.)

**Solução:** Como o cliente planeja manter o AD FS, ele também precisará manter a sincronização de diretório, pois esse é um pré-requisito. Por isso, ele não pode remover totalmente os servidores Exchange do ambiente local. No entanto, ele pode desativar a maioria dos servidores do Exchange, mas manter alguns servidores para gerenciamento de usuários. Lembre-se de que os servidores que são mantidos em execução podem ser executados em máquinas virtuais, pois a carga de trabalho é quase completamente deslocada para o Exchange Online.

O gráfico a seguir descreve o estado final desejado:

![Encerre os servidores do Exchange com alguns restantes](images/Dn931280.d7734579-6999-45b2-9a0f-a23f18353a49(EXCHG.150).jpg "Encerre os servidores do Exchange com alguns restantes")

O gráfico a seguir descreve o estado final real:

![Estado antes de encerrar os servidores do Exchange](images/Dn931280.c692f0af-6536-4bc9-950d-58a1e486525f(EXCHG.150).jpg "Estado antes de encerrar os servidores do Exchange") Para manter o AD FS e a sincronização de diretório e desativar a maioria dos servidores do Exchange

1.  Execute o `Get-OrganizationConfig |fl PublicFoldersEnabled` e verifique se ele não está definido como remoto. Se ele estiver definido como remoto e você desejar continuar acessando as pastas públicas, será preciso migrá-las para o Exchange Online. Para obter informações sobre como fazer isso, consulte [Usar a migração de lotes para migrar as pastas públicas herdadas para o Office 365 e para o Exchange Online](https://technet.microsoft.com/pt-br/library/dn874017\(v=exchg.150\)).
    

    > [!IMPORTANT]
    > Se a migração das pastas públicas para o Exchange Online não for uma opção e você ainda precisar delas para seus usuários, não prossiga.



2.  Depois que você mover todas as caixas de correio para o Exchange Online, a primeira coisa que deverá fazer para desativar a maioria dos servidores Exchange será apontar os registros MX e DNS de Descoberta Automática para o Exchange Online em vez de para o local. Para saber mais, consulte [Referência: Registros de DNS externos para o Office 365](http://technet.microsoft.com/pt-br/library/hh852557.aspx).
    

    > [!IMPORTANT]
    > Atualize o DNS interno e externo, caso contrário, poderá ocorrer um comportamento de conectividade de cliente e fluxo de emails inconsistente.



3.  Em seguida, você deve remover os valores de SCP (Ponto de Conexão de Serviço) nos seus servidores Exchange. Isso garante que nenhum SCP será retornado e, em vez disso, o cliente usará o método de DNS para a Descoberta Automática. Um exemplo é mostrado abaixo:
    
        Get-ClientAccessServer | Set-ClientAccessServer -AutoDiscoverServiceInternalUri $Null
    

    > [!TIP]
    > Se tiver servidores do Exchange 2007 no ambiente, você terá que executar um comando semelhante nos servidores do Exchange 2007 para anular as configurações



4.  Para impedir que os objetos da configuração híbrida sejam recriados no futuro, você deverá remover o objeto de configuração híbrida do Active Directory. Para fazer isso, abra o Shell de Gerenciamento do Exchange e execute o seguinte:
    
        Remove-HybridConfiguration

5.  Remova todos os servidores do Exchange, com exceção dos servidores que você manterá para criação e gerenciamento de usuários. Dois servidores devem ser suficientes para o gerenciamento de usuários, embora, possivelmente, você consiga realizá-lo com um servidor. Além disso, não é preciso ter um Grupo de Disponibilidade de Banco de Dados ou qualquer outra opção de alta disponibilidade.

6.  Se o OAuth estiver configurado para uma implantação híbrida do Exchange, recomendável desabilitar a configuração no local e no Office 365. Na maioria dos ambientes, essas etapas podem ser ignoradas porque apenas um pequeno subconjunto de nossos clientes tem o OAuth configurado.
    
    Para desabilitar a configuração local:
    
    1.  Abra o Shell de Gerenciamento do Exchange em um servidor Exchange 2013.
    
    2.  Execute:
        
            Get-IntraorganizationConnector -Identity ExchangeHybridOnPremisesToOnline | Set-IntraOrganizationConnector -Enabled $False
    
    Para desabilitar a configuração do Exchange Online:
    
    1.  Conecte o Windows PowerShell ao Exchange Online.
    
    2.  Execute:
        
            Run Get-IntraorganizationConnector -Identity ExchangeHybridOnlineToOnPremises | Set-IntraOrganizationConnector -Enabled $False
        
        O parâmetro Identity pressupõe que você tenha usado o Assistente de Configuração Híbrida para configurar o OAuth. Se esse não for o caso, talvez seja necessário ajustar o valor especificado para a identidade dos conectores.

7.  Há conectores de entrada e saída criados pelo Assistente de Configuração Híbrida que convém excluir. Use as seguintes etapas para fazer isso:
    
    1.  Faça logon no [Portal de administração do Office 365](http://portal.office.com) e entre como Administrador de Locatários.
    
    2.  Selecione a opção para gerenciar o **Exchange**.
    
    3.  Navegue até **Fluxo de Emails** -\> **Conectores**.
    
    4.  Agora você pode desabilitar ou excluir os conectores de entrada e saída. O HCW cria conectores com o namespace exclusivo de **entrada do \<identificador exclusivo\>** e **saída do \<identificador exclusivo\>**, conforme mostrado na imagem abaixo.
        
        ![Assistente de Configuração Híbrida cria conectores com namespace exclusivo](images/Dn931280.7b1b6f0b-43d6-4407-8cd7-7dd52e016697(EXCHG.150).jpg "Assistente de Configuração Híbrida cria conectores com namespace exclusivo")  

8.  Remova a relação de organização criada pelo Assistente de Configuração Híbrida. Use as seguintes etapas para fazer isso:
    
    1.  Faça logon no [Portal de administração do Office 365](http://portal.office.com) e entre como Administrador de Locatários.
    
    2.  Selecione a opção para gerenciar o **Exchange**.
    
    3.  Navegue até **Organização**.
    
    4.  Em **Compartilhamento de Organização**, remova a organização chamada **O365 para Local – \<identificador exclusivo\>**, conforme mostrado na imagem abaixo.
        
        ![Remova o Relacionamento de Organização criado pelo Assistente de Configuração Híbrida.](images/Dn931280.2f0c1077-8785-487a-87a5-a75f0a4f0fea(EXCHG.150).jpg "Remova o Relacionamento de Organização criado pelo Assistente de Configuração Híbrida.")  

## Cenário três

**Problema:** Desejo remover meus servidores do Exchange locais depois de mover todas as minhas caixas de correio para o Exchange Online. No entanto, descobrimos que elas estão usando o Exchange para outros fins, como para uma retransmissão de protocolo SMTP para um aplicativo ou para obter acesso a pastas públicas. Se você precisar de servidores do Exchange locais para atender às necessidades atuais da sua organização, talvez não seja do seu interesse remover os servidores locais.

**Solução:** Não recomendamos a remoção do Exchange e a configuração híbrida neste ponto. Se você fosse iniciar o processo apontando os Registros de Descoberta Automática para o Exchange Online, imediatamente danificaria alguns recursos, como o acesso a pastas públicas híbridas. Você poderia alterar o registro MX para apontar para o Proteção do Exchange Online, se isso ainda não tivesse sido feito, e poderia até mesmo remover alguns dos servidores Exchange locais. No entanto, você precisaria manter recursos suficientes para lidar com as funções híbridas restantes. Normalmente, isso levaria a uma superfície local muito pequena.

