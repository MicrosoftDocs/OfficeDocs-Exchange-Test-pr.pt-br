---
title: 'Movimentação de caixas de correio entre organizações locais e do Exchange Online em implantações híbridas: Exchange 2013 Help'
TOCTitle: Movimentação de caixas de correio entre organizações locais e do Exchange Online em implantações híbridas
ms:assetid: d6289f7b-f67e-48db-9570-9fd3c9547548
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/o365e_hrcmoverequest_fl312271(v=EXCHG.150)
ms:contentKeyID: 51406960
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Movimentação de caixas de correio entre organizações locais e do Exchange Online em implantações híbridas

 

_<strong>Aplica-se a:</strong>Exchange Online, Exchange Server 2013, Exchange Server 2016_

_<strong>Tópico modificado em:</strong>2017-10-02_

Com uma implantação híbrida baseada no Exchange, você pode optar por mover caixas de correio locais do Exchange para a organização do Exchange Online ou mover caixas de correio do Exchange Online para a organização do Exchange. Ao mover caixas de correio entre as organizações do Exchange Online e local, você usa lotes de migração para executar a solicitação de movimentação de caixa de correio remota. Essa abordagem permite que você mova as caixas de correio existentes, em vez de criar novas caixas de correio do usuário, e importe as informações do usuário. Essa abordagem é diferente da migração de caixas de correio do usuário de uma organização local do Exchange para o Exchange Online, como parte de uma migração completa do Exchange para a nuvem. As movimentações de caixas de correio discutidas neste tópico fazem parte do gerenciamento administrativo do Exchange em um relacionamento de coexistência de longo prazo entre organizações locais do Exchange e do Exchange Online.

Confira mais informações sobre a migração de organizações do Exchange local para o Exchange Online em [Formas de migrar várias contas de email para o Office 365](https://go.microsoft.com/fwlink/p/?linkid=524030).


> [!IMPORTANT]
> Você deve ter configurado uma implantação híbrida entre suas organizações local e do Exchange Online para concluir os procedimentos de movimentação de caixa de correio neste tópico. Para saber mais sobre implantações híbridas, confira <A href="exchange-server-hybrid-deployments-exchange-2013-help.md">Implantações Híbridas do Exchange Server</A><BR><BR>Antes de mover as caixas de correio habilitadas para UM (Unificação de Mensagens) para o Exchange Online, será necessário certificar-se de que o Skype for Business 2015, o Skype for Business Online e o Exchange Online no local atendam aos requisitos especificados no <A href="hybrid-deployment-prerequisites-exchange-2013-help.md">Pré-requisitos de implantação híbrida</A>. Para obter informações sobre como mapear suas diretivas de caixa de correio UM local para políticas no Exchange Online, confira <A href="https://technet.microsoft.com/pt-br/library/bb124903(v=exchg.150)">Set-UMMailboxPolicy</A>.



## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 10 minutos para configurar o lote de migração, mas o tempo total para concluir a migração depende do número de caixas de correio incluídas em cada lote de migração.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Seção "Mover caixa de correio e migrar permissões" no tópico [Permissões de destinatários](https://technet.microsoft.com/pt-br/library/dd638132\(v=exchg.150\)) .

  - A implantação híbrida é configurada entre suas organizações local e do Exchange Online.

  - Se você estiver executando o Exchange 2013, habilite o serviço MRSProxy (Proxy de Replicação de Caixa de Correio) em seus servidores de Acesso para Clientes locais do Exchange 2013.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](https://technet.microsoft.com/pt-br/library/jj150484\(v=exchg.150\)).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## Etapa 1: criar um ponto de extremidade de migração

Antes de executar a integração e a remoção de migrações de movimentação remotas em uma implantação híbrida do Exchange, recomendamos que você crie pontos de extremidade de migração remota do Exchange. O ponto de extremidade de migração contém as configurações de conexão de um servidor do Exchange local que esteja executando o serviço de proxy MRS, que é necessário para executar migrações de movimentação remota do e para o Exchange Online.

Para obter procedimentos passo a passo, consulte Criar pontos de extremidade de migração.

## Etapa 2: habilitar o serviço MRSProxy

Se o serviço MRSProxy ainda não estiver habilitado para seu servidores de Acesso para Clientes locais do Exchange 2013, execute estas etapas no EAC (Centro de Administração do Exchange):

1.  Abra o EAC e navegue até **Servidores** \> **Diretórios Virtuais**.

2.  Selecione o servidor de Acesso para Clientes, selecione o diretório virtual **EWS** e clique em **Editar**![Ícone de edição](images/JJ906432.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Marque a caixa de seleção **Proxy MRS habilitado** e clique em **Salvar**.

## Etapa 3: usar o EAC para mover as caixas de correio

Você pode usar o assistente de migração de movimentação remota na guia **Office 365** no EAC em um servidor do Exchange para mover caixas de correio de usuário existentes na organização local para a organização do Exchange Online ou mover caixas de correio do Exchange Online para a organização local. Escolha um dos seguintes procedimentos:

## Mover caixas de correio locais para o Exchange Online

Você pode usar o assistente de migração de movimentação remota, na guia **Office 365** do EAC de um servidor Exchange, para mover caixas de correio existentes na organização local para a organização do Exchange Online. Siga estas etapas:

1.  Abra o EAC e, em seguida, navegue até **Office 365** \> **Destinatários** \> **Migração**.

2.  Clique em **Adicionar**![Ícone Adicionar](images/Mt791517.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar") e selecione **Migrar para o Exchange Online**.

3.  Na página **Selecionar um tipo de recuperação**, selecione **Migração de movimentação remota** e clique em **Avançar**.

4.  Na página **Selecionar os usuários**, clique em **Adicionar**![Ícone Adicionar](images/Mt791517.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar") e selecione os usuários locais para mover para o Office 365, clique em **Adicionar** e, em seguida, clique em **OK**. Clique em **Avançar**.

5.  Na página **Inserir credencial da conta de usuário do Windows**, digite o nome da conta do administrador local, no campo de texto **Nome do administrador local**, e digite a senha associada a essa conta, no campo de texto **Senha do administrador local**. Por exemplo, "corp\\administrador" e uma senha. Clique em **Avançar**.
    

    > [!TIP]
    > Se já tiver criado um ponto de extremidade de migração, você receberá um prompt de confirmação de ponto de extremidade para essa etapa. Se tiver criado dois ou mais pontos de extremidade de migração, você deverá escolher um ponto de extremidade no menu suspenso de ponto de extremidade de migração.



6.  Na página **Confirmar o ponto de extremidade de migração**, verifique se o FDQN do servidor do Exchange local estará listado quando o assistente confirmar o ponto de extremidade de migração. Por exemplo, "mail.contoso.com". Clique em **Avançar**.
    

    > [!TIP]
    > O serviço MRSProxy nos servidores do Exchange limita automaticamente as solicitações de movimentação de caixa de correio quando você seleciona várias caixas de correio para mover para o Exchange Online. O tempo total para concluir a movimentação da caixa de correio depende do número total de caixas de correio selecionadas, do tamanho das caixas de correio e da configuração do MRSProxy. Para saber mais sobre como personalizar o MRSProxy, confira <A href="https://technet.microsoft.com/pt-br/library/bb232205(v=exchg.150)">Limitação de mensagem</A>.



7.  Na página **Mover configuração**, insira um nome para o lote de migração no campo de texto **Novo nome de lote de migração**. Use a seta para baixo ![Ícone Seta para baixo](images/JJ906432.ef5ca57d-a033-457b-bd92-6361877c33d0(EXCHG.150).gif "Ícone Seta para baixo") para selecionar o **Domínio de entrega de destino das caixas de correio que estão migrando para o Office 365**. Na maioria das implantações híbridas, esse é o domínio SMTP principal usado para as caixas de correio da organização do Exchange Online. Por exemplo, contoso.mail.onmicrosoft.com. Verifique se a opção **Mover caixa de correio principal junto com a caixa de correio de arquivo morto** está selecionada e clique em **Avançar**.

8.  Na página **Iniciar o lote**, selecione pelo menos um destinatário para receber o relatório de conclusão do lote. Verifique se a opção **Iniciar o lote automaticamente** está selecionada e marque a caixa de seleção **Concluir automaticamente o lote de migração**. Clique em **Novo**.

## Mover caixas de correio do Exchange Online para a organização local

Você pode usar o assistente de migração de movimentação remota, na guia **Office 365** do EAC de um servidor Exchange, para mover caixas de correio existentes na organização local para a organização do Exchange Online.

1.  Abra o EAC e navegue até **Office 365** \> **Destinatários** \> **migração**.

2.  Clique em **Adicionar**![Ícone Adicionar](images/Mt791517.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar") e selecione **Migrar do Exchange Online**.

3.  Na página **Selecione os usuários** selecione **Selecione os usuários que você deseja mover** e, em seguida, clique em **Avançar**.

4.  Na página **Selecionar os usuários**, clique em **Adicionar** ![Ícone Adicionar](images/Mt791517.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar") e, em seguida, selecione os usuários do Exchange Online para mover para a organização local, clique em **Adicionar** e, em seguida, clique em **OK**. Clique em **Avançar**.

5.  Na página **Confirmar o ponto de extremidade de migração**, verifique se o FDQN do servidor do Exchange local estará listado quando o assistente confirmar o ponto de extremidade de migração. Por exemplo, "mail.contoso.com". Clique em **Avançar**.
    

    > [!TIP]
    > O serviço MRSProxy nos servidores do Exchange limita automaticamente as solicitações de movimentação de caixa de correio quando você seleciona várias caixas de correio para mover para o Exchange Online. O tempo total para concluir a movimentação de caixa de correio depende do número total de caixas de correio selecionadas, do tamanho das caixas de correio e das propriedades do MRSProxy. Para saber mais sobre como personalizar o MRSProxy, confira <A href="https://technet.microsoft.com/pt-br/library/bb232205(v=exchg.150)">Limitação de mensagem</A>.



6.  Na página **Mover configuração**, insira um nome para o lote de migração no campo de texto **Nome do novo lote de migração**. Em seguida, digite o domínio de entrega de destino no campo **Domínio de entrega de destino para as caixas de correio que estão migrando para o Office 365**. Na maioria das implantações híbridas, esse é o domínio SMTP principal usado para as caixas de correio da organização local e do Exchange Online. Por exemplo, contoso.com.

7.  Escolha se deseja mover a caixa de correio de arquivo morto para o usuário selecionado e insira o nome do banco de dados para o qual você deseja mover esta caixa de correio no campo de texto **Banco de dados de destino**. Por exemplo, Banco de Dados de Caixa de Correio 123456789. Clique em **Avançar**.

8.  Na página **Iniciar o lote**, selecione pelo menos um destinatário para receber o relatório de conclusão do lote. Verifique se **Iniciar o lote automaticamente** está selecionado e marque a caixa de seleção **Concluir automaticamente o lote de migração**. Clique em **Novo**.

## Etapa 4: remover lotes de migração concluídos

Depois que suas movimentações de caixa de correio forem concluídas, recomendamos remover os lotes de migração concluídos para minimizar a probabilidade de erros, se os mesmos usuários forem movidos novamente.

Para remover um lote de migração concluído:

1.  Abra o EAC e navegue até **Office 365** \> **Destinatários** \> **Migrações**.

2.  Clique em um lote de migração concluído e clique em **Excluir** ![Excluir ícone](images/JJ906432.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Excluir ícone").

3.  Na caixa de diálogo de confirmação de aviso de exclusão, clique em **Sim**.

## Etapa 5: habilitar novamente o acesso offline para o Outlook na Web

O acesso offline no Outlook na Web (chamado anteriormente de Outlook Web App) permite aos usuários acessar suas caixas de correio quando não estão conectados a uma rede. Se você migrar as caixas de correio do Exchange para o Exchange Online, os usuários deverão redefinir a configuração de acesso offline em seus navegadores a fim de usar o Outlook na Web offline. Confira mais informações sobre o acesso offline no Outlook na Web, os navegadores que oferecem suporte a ele e como ativá-lo em [Usando o Outlook Web App offline](https://go.microsoft.com/fwlink/p/?linkid=286942).

## Como saber se funcionou?

Quando você mover caixas de correio do usuário existentes entre as organizações local e do Exchange Online, a conclusão bem-sucedida do assistente de movimentação remota será sua primeira indicação de que a movimentação da caixa de correio será concluída conforme o esperado.

Como o processo de movimentação da caixa de correio demora algum tempo, você também pode verificar se a movimentação está funcionando corretamente abrindo o EAC e selecionando **Office 365** \> **Destinatários** \> **Migração**, para mostrar o status de movimentação das caixas de correio selecionadas no assistente de movimentação remota. O valor do **Status** é **Sincronizando** durante a movimentação de caixas de correio e **Concluído** quando a caixa de correio é movida com sucesso para a organização local ou do Exchange Online.

Após a conclusão da movimentação de caixa de correio, você pode verificar se a caixa de correio remota localizada na organização local ou do Exchange Online foi movida com êxito verificando as propriedades da caixa de correio. Para fazer isso, navegue até **Destinatários** \> **Caixas de correio** no EAC da organização local ou da organização do Exchange Online. A caixa de correio do usuário deve mostrar um **Tipo de Caixa de Correio** do **Office 365** para caixas de correio do Exchange Online e de **Usuário** para caixas de correio locais.

Você também pode executar o cmdlet a seguir no Shell de Gerenciamento do Exchange para verificar o status do lote de migração.

    Get-MigrationBatch -Identity <batch name>

Problemas? Peça ajuda nos fóruns do Office 365. Para acessar os fóruns, é necessário fazer logon usando uma conta com acesso de administrador ao serviço baseado em nuvem. Visite os fóruns em: [Fóruns do Office 365](https://go.microsoft.com/fwlink/p/?linkid=201915)

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

