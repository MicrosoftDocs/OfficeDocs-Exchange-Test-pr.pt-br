---
title: 'Criar uma implantação híbrida com o Assistente de Configuração Híbrida: Exchange 2013 Help'
TOCTitle: Criar uma implantação híbrida com o Assistente de Configuração Híbrida
ms:assetid: 997a25d3-7fb3-4d4e-bb28-defcbf542c99
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ200787(v=EXCHG.150)
ms:contentKeyID: 50487116
ms.date: 03/14/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Criar uma implantação híbrida com o Assistente de Configuração Híbrida

Este tópico está em andamento.  

_<strong>Aplica-se a:</strong>Exchange Online, Exchange Server 2013, Exchange Server 2016_

_<strong>Tópico modificado em:</strong>2016-12-09_

Ao estabelecer uma implantação híbrida, você pode levar sua capacidade de experiência e o controle administrativo cheio de recursos em suas organizações locais do Exchange Server para a nuvem. Uma implantação híbrida também oferece suporte para uma solução de arquivamento baseada na nuvem para suas caixas de correio locais com o Arquivamento Online do Exchange e também pode servir como uma etapa intermediária para uma migração completa de suas caixas de correio locais para o Exchange Online.

Este tópico abrange a configuração de uma implantação híbrida para sua organização local do Exchange e sua organização do Exchange Online no Office 365 para empresas que usam o assistente de Configuração Híbrida. Neste tópico, uma implantação híbrida é criada para a seguinte configuração de organização:

  - A organização local é uma organização do Exchange de floresta única.

  - A organização local não usa um serviço existente do Microsoft Exchange Online Protection (EOP) para a proteção local.

  - A organização local não tem servidores de Transporte de Borda implantados. O assistente de Configuração Híbrida suporta a configuração dos servidores de Transporte de Borda como parte de uma implantação híbrida, mas configurar servidores de Transporte de Borda no assistente não é abordado neste tópico.


> [!IMPORTANT]
> Configurar uma implantação híbrida com o assistente de Configuração Híbrida exige diversos pré-requisitos importantes para o assistente concluir com êxito e para os recursos de implantação híbrida funcionarem corretamente. Você deve concluir todos os pré-requisitos destacados no <A href="hybrid-deployment-prerequisites-exchange-2013-help.md">Pré-requisitos de implantação híbrida</A> antes de usar o assistente de Configuração Híbrida para criar e configurar sua implantação híbrida.<BR>Além disso, o <A href="http://technet.microsoft.com/exdeploy2013">Assistente de Implantação do Exchange Server</A> é uma ferramenta gratuita com base na Web que ajuda a configurar uma implantação híbrida entre sua organização local e o Office 365 ou a migrar completamente para o Office 365. A ferramenta faz algumas perguntas simples e, com base nas respostas, cria uma lista de verificação personalizada com instruções para configurar sua implantação híbrida. Recomendamos o uso do Assistente de Implantação para gerar uma lista de verificação de implantação híbrida para as necessidades específicas de sua organização.



Para outras tarefas de gerenciamento relacionadas a implantações híbridas, confira [Procedimentos de Implantação Híbrida](hybrid-deployment-procedures-exchange-2013-help.md).

Saiba mais sobre implantações híbridas em [Implantações Híbridas do Exchange Server](exchange-server-hybrid-deployments-exchange-2013-help.md). Saiba mais sobre o Office 365 em [O que é o Office 365?](http://go.microsoft.com/fwlink/?linkid=266712).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 30 minutos
    

    > [!IMPORTANT]
    > Configurar os requisitos para uma implantação híbrida levará consideravelmente mais tempo do que o estimado para concluir os procedimentos do assistente de Configuração Híbrida descritos neste tópico. Por exemplo, fazer o login para o Office 365 para empresas, configurar a sincronização do Active Directory e atribuir licenças do Exchange Online requer mais tempo e também pode incluir alterações na topologia de rede. Você deve reservar mais tempo do que o listado para concluir esse procedimento para concluir a configuração de implantação híbrida de ponta a ponta.



  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Configurações híbridas", no tópico [Permissões de infraestrutura do Exchange e do Shell](https://technet.microsoft.com/pt-br/library/dd638114\(v=exchg.150\)).

  - Você precisa executar o assistente de Configuração Híbrida em um computador que execute a versão mais recente de uma versão compatível do Exchange. As etapas finais do assistente de Configuração Híbrida para a configuração da autenticação OAuth do Exchange exige a execução das etapas a partir de um Exchange local ou de qualquer servidor de domínio associado ou estação de trabalho. Além disso, o processo de autenticação OAuth funciona melhor ao usar a versão de área de trabalho do Internet Explorer 11 ou superior.

  - Revise [Implantações Híbridas do Exchange Server](exchange-server-hybrid-deployments-exchange-2013-help.md) e certifique-se de que entendeu as áreas que serão afetadas pela configuração de uma implantação híbrida.

  - Reveja e conclua todos os requisitos de implantação híbrido descritos em [Pré-requisitos de implantação híbrida](hybrid-deployment-prerequisites-exchange-2013-help.md).

  - A ferramenta Analisador de Conectividade Remota da Microsoft verifica a conectividade externa da sua organização local do Exchange e assegura que você está pronto para configurar sua implantação híbrida. É altamente aconselhável que você verifique sua organização local com a ferramenta Analisador de Conectividade Remota antes de configurar sua implantação híbrida com o assistente de Configuração Híbrida. Saiba mais em [Ferramenta Analisador de Conectividade Remota](http://go.microsoft.com/fwlink/p/?linkid=167905).

  - É altamente recomendável configurar o logon único usando a sincronização de senha do Azure Active Directory Connect. O logon único permite que os usuários acessem ambas as organizações, local e do Exchange, utilizando uma única senha e nome de usuário. O logon único também garante que as credenciais dos usuários não sejam solicitadas ao acessar o conteúdo arquivado na organização do Exchange Online quando estiverem usando o Arquivamento Online do Exchange. Para obter mais informações sobre a sincronização de senha, confira [Sincronização do Azure AD Connect: implementar a sincronização de senha](http://go.microsoft.com/fwlink/p/?linkid=723513)

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](https://technet.microsoft.com/pt-br/library/jj150484\(v=exchg.150\)).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## Usar o centro de administração do Exchange e o assistente de Configuração Híbrida para criar uma implantação híbrida

Use o procedimento a seguir para criar e configurar uma implantação híbrida:

1.  No EAC em um servidor Exchange da sua organização local, navegue até o nó **Híbrida**.

2.  No nó **Híbrido**, clique em **Configurar** para inserir suas credenciais do Office 365.
    

    > [!IMPORTANT]
    > Se a sua organização local estiver na China e seu locatário do Office 365 for hospedado pela 21Vianet, você deverá marcar a caixa de seleção <STRONG>Minha organização do Office 365 é hospedada pela 21Vianet</STRONG>. Se o seu locatário do Office 365 for hospedado pela 21Vianet e essa caixa de seleção não for marcada, o Assistente de Configuração Híbrida não se conectará ao serviço 21Vianet, as credenciais de sua conta do Office 365 não serão reconhecidas e o assistente não será concluído apropriadamente.



3.  Na solicitação de logon para acessar o Office 365, selecione **entrar no Office 365** e digite as credenciais da conta A conta de logon precisa ser de Administrador Global no Office 365.

4.  Clique em **Configurar** novamente para iniciar o assistente de Configuração Híbrida.

5.  Na página **Download do Assistente de Configuração Híbrida do Microsoft Office 365**, clique em **Clique aqui** para baixar o assistente. Quando você for solicitado, clique em **Instalar** na caixa de diálogo **Instalação do Aplicativo**.

6.  Clique em **Avançar** e, em seguida, na seção **Organização do Exchange Server Local**, selecione **Detectar um servidor que executa o Exchange 2013 CAS ou o Exchange 2016**. O assistente tentará detectar um servidor local do Exchange. Se o assistente não detectar um servidor do Exchange ou se você quiser usar um servidor diferente, selecione **Especificar um servidor que executa o Exchange 2013 CAS ou Exchange 2016** e, em seguida, especifique o FQDN interno de um servidor de Caixa de Correio do Exchange.

7.  Na seção **Exchange Online do Office 365**, selecione **Microsoft Office 365** e, em seguida, clique em **Avançar**.

8.  Na página **Credenciais**, na seção **Inserir suas credenciais de conta local**, selecione **Usar as credenciais atuais do Windows** para que o assistente use a conta à qual você está conectado ao acessar o Active Directory local e os servidores do Exchange. Se quiser especificar um conjunto diferente de credenciais, desmarque **Usar as credenciais atuais do Windows** e especifique o nome de usuário e senha de uma conta do Active Directory que você deseja usar. Qualquer que seja a seleção escolhida, a conta usada deve ser membro do grupo de segurança Administradores de Empresa.

9.  Na seção de credenciais **Insira seu Office 365**, especifique o nome de usuário e senha de uma conta do Office 365 que tenha permissões de Administrador Global. Clique em **Avançar**.

10. Na página **Validando Conexões e Credenciais**, o assistente se conectará à organização local e à organização do Office 365 para validar credenciais e examinar a configuração atual de ambas as organizações. Clique em **Avançar** após a conclusão.

11. Em **Domínios Híbridos**, selecione os domínios que você deseja incluir em sua implantação híbrida. Na maioria das implantações, você pode deixar a coluna **Descoberta Automática** definida como **False** para cada domínio. Só selecione **True** ao lado de um domínio se você precisar forçar o assistente a usar as informações de Descoberta Automática a partir de um domínio específico. Clique em **Avançar**.
    

    > [!IMPORTANT]
    > Esta etapa de seleção de domínio do assistente de Configuração Híbrida pode ou não aparecer quando o assistente é executado.<BR>Esta etapa não vai aparecer se: 
    > <UL>
    > <LI>
    > <P>Você tiver apenas um domínio aceito no local adicionado ao seu locatário do Office&nbsp;365. Como esse é o único domínio disponível para a configuração de implantação híbrida, o domínio é automaticamente selecionado e a etapa é ignorada no assistente.</P>
    > <LI>
    > <P>Não há qualquer domínio local aceito adicionado ao seu locatário do Office&nbsp;365. Nesse caso, você receberá um erro e precisará adicionar pelo menos um domínio ao seu locatário do Office&nbsp;365 antes de continuar. Você pode fazer isso usando o portal Administrativo do Office&nbsp;365, ou configurando opcionalmente os Serviços de Federação do Active Directory (AD&nbsp;FS) em sua organização local.</P></LI></UL>Essa etapa aparecerá ser você possuir mais de um domínio aceito local adicionado ao seu locatário do Office&nbsp;365.



12. Na página **Confiança de Federação**, clique em **Habilitar** e, em seguida, clique em **Avançar**.

13. Na página **Propriedade do Domínio**, clique em **Clique para copiar para a área de transferência** para copiar as informações do token de verificação do domínio para os domínios que você selecionou para incluir na implantação híbrida. Abra um editor de texto, como o Bloco de notas, e cole as informações do token para esses domínios. Antes de continuar no assistente de Configuração Híbrida, você deve usar essas informações para criar um registro TXT para cada domínio em seu DNS público. confira a Ajuda do host DNS para obter informações sobre como adicionar um registro TXT à zona de DNS. Clique em **Avançar** depois que os registros TXT tiverem sido criados e os registros DNS replicados.

14. Na página **Certificado de Transporte**, no campo **Selecionar um servidor de referência**, selecione o servidor do Exchange que possui o certificado configurado anteriormente na lista de verificação.

15. No campo **Selecionar um certificado**, selecione o certificado a ser usado no transporte de email seguro. Esta lista exibe os certificados digitais emitidos por uma autoridade de certificação de terceiros instalada no servidor de Caixa de Correio selecionado na etapa anterior. Clique em **Avançar**.

16. Na página **FQDN da Organização**, digite o FQDN externamente acessível para o servidor do Exchange voltado para a Internet. O Office 365 usa esse FQDN para configurar os conectores de serviço para transporte de email seguro entre suas organizações do Exchange. Por exemplo, digite "mail.contoso.com". Clique em **Avançar**.

17. As seleções de configuração da implantação híbrida foram atualizadas e você está pronto para iniciar as alterações dos serviços do Exchange e a configuração da implantação híbrida. Clique em **Atualizar** para iniciar o processo de configuração. Enquanto o processo de configuração híbrida estiver em execução, o assistente exibe as áreas de recurso e serviço que estão sendo configuradas para a implantação híbrida à medida que são atualizadas.

18. O assistente exibe uma mensagem de conclusão, e o botão **Fechar** é exibido. Clique em **Fechar** para concluir o processo de configuração de implantação híbrida e fechar o assistente.

## Configurar a autenticação OAuth entre as organizações do Exchange e do Exchange Online

Para implantações híbridas combinadas do Exchange 2013/2010 e do Exchange 2013/2007, a conexão de autenticação com base em OAuth da nova implantação híbrida entre o Office 365 e as organizações do Exchange local não é configurada pelo Assistente de Configuração Híbrida. Essas implantações continuam a usar o processo de relação de confiança de federação por padrão. No entanto, determinados recursos do Exchange 2013, como MRM (Gerenciamento de Registros de Mensagem), Arquivamento In-loco do Exchange e Descoberta Eletrônica In-loco ficam totalmente disponíveis apenas em sua organização usando o novo protocolo de autenticação Exchange OAuth. Recomendamos que todas as organizações combinadas do Exchange 2013/2010 e do Exchange 2013/2007 que queiram implementar esses recursos como parte de uma nova implantação híbrida com o Exchange Online, configurem a autenticação do Exchange OAuth após a configuração de sua nova implantação híbrida com o Assistente de Configuração Híbrida.

Para obter etapas de configuração detalhadas, consulte [Configurar a autenticação OAuth entre organizações do Exchange e do Exchange Online](https://technet.microsoft.com/pt-br/library/dn594521\(v=exchg.150\))

Para obter mais informações sobre recursos de segurança e conformidade do Exchange que usam autenticação OAuth, consulte:

  - [Usando a autenticação OAuth para suportar o Arquivamento em uma implantação híbrida do Exchange](https://technet.microsoft.com/pt-br/library/dn689104\(v=exchg.150\))

  - [Usando a autenticação OAuth para suportar a Descoberta Eletrônica em uma implantação híbrida do Exchange](https://technet.microsoft.com/pt-br/library/dn497703\(v=exchg.150\))

## Como saber se funcionou?

A conclusão bem-sucedida do assistente de Configuração Híbrida será a primeira indicação de que a conclusão das etapas da configuração híbrida funcionou conforme o esperado.

Para verificar se você criou e configurou com êxito sua implantação híbrida, faça o seguinte:

  - Execute o comando a seguir no Shell de Gerenciamento do Exchange para a organização local. Esse comando exibe os valores e as configurações da configuração híbrida, os recursos híbridos e os pontos de extremidade do transporte. Verifique se esses valores estão corretos.
    
        Get-HybridConfiguration

  - Confirme se o assistente de Configuração Híbrida concluiu todas as etapas de configuração examinando o log de configuração híbrida. Por padrão, o log está localizado no servidor de Caixa de Correio local em C:\\Arquivos de Programas\\Microsoft\\Exchange Server\\V15\\Logging\\Update-HybridConfiguration.

  - Mova uma caixa de correio local existente para a organização do Exchange Online para testar o suporte ao recurso de movimentação de caixa de correio, ou crie uma nova caixa de correio de usuário na organização do Exchange Online para testar o compartilhamento de calendário de disponibilidade entre as duas organizações. As duas ações de caixa de correio permitirão que você teste e confirme se a entrega de mensagens entre as organizações locais e do Exchange Online está funcionando corretamente com as caixas de correio existentes e se a entrega de mensagens é segura e tratada como mensagens internas para a organização do Exchange.
    
      - Use o EAC e vá para **Empresa** \> **Destinatários** \> **Caixas de Correio** para criar uma nova caixa de correio remota no Exchange Online.
    
      - Use o EAC e vá para **Office 365** \> **Destinatários** \> **Migração** para mover uma caixa de correio existente para o Exchange Online.

