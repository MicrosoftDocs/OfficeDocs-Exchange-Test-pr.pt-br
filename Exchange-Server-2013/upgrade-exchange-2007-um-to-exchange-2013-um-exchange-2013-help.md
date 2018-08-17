---
title: 'Atualizar UM do Exchange 2007 para o UM do Exchange 2013: Exchange 2013 Help'
TOCTitle: Atualizar UM do Exchange 2007 para o UM do Exchange 2013
ms:assetid: 642c922d-7e85-40f0-bb9b-0f20da692be3
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dn169227(v=EXCHG.150)
ms:contentKeyID: 54651967
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Atualizar UM do Exchange 2007 para o UM do Exchange 2013

 

_**Aplica-se a:** Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2016-12-09_

Quando atualiza uma organização do Microsoft Exchange 2007 com Unificação de Mensagens (UM) para a Unificação de Mensagens do Exchange 2007, este são os passos necessários e outros passos já concluídos como parte implantação da UM do Exchange 2007. Dependendo do seu ambiente de telefonia e componentes da UM que foram criados e configurados para suportar a Unificação de Mensagens no Exchange 2007, poderá ter de implantar equipamento de telefonia adicional, incluindo gateways de Voice over IP (VoIP), IP Private Branch eXchanges (PBXs) ou PBXs tradicionais ou habilitado para SIP e, em seguida, crie e configure os componentes da UM adicionais que serão necessários para a UM do Exchange 2013.

## O que você precisa saber antes de começar?

  - Tempo estimado para a conclusão da tarefa: 45-90 minutos.

  - Verifique se tem as permissões adequadas na organização do Exchange 2007 e Exchange 2013 para criar e configurar todos os componentes necessários.

  - Verifique se implantou e configurou corretamente os componentes de telefonia, incluindo gateways VoIP e PBXs, PBXs IP ou PBXs habilitados para SIP (Session Initiation Protocol).

  - Verifique se instalou e configurou corretamente os servidores de Acesso para Cliente executando o serviço de Roteador de Chamadas da Unificação de Mensagens do Microsoft Exchange (Roteador de Chamadas da UM) e servidores de Caixa de Correio executando o serviço de Unificação de Mensagens do Microsoft Exchange (UM). Para saber mais sobre os serviços de UM, consulte [Serviços de Unificação de mensagens](um-services-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## Como fazer isso?

## Etapa 1: Baixar e instalar os pacotes de idioma de UM necessários

Os pacotes de idioma da UM permitem que os chamadores e usuários do Outlook Voice Access interajam com o sistema de caixa postal em vários idiomas. Após instalar um idioma adicional no servidor da Caixa de correio do Exchange 2013, os chamadores e usuários do Outlook Voice Access podem ouvir mensagens de email e interagir o sistema de caixa postal nesse idioma. No entanto, para disponibilizar esse idioma para todas as chamadas de entrada, tem de instalar os pacotes de idiomas da UM necessários em todos os servidores de Caixa de Correio do Exchange 2013. Isto ocorre porque todos os servidores de Caixa de Correio do Exchange 2013 podem atender chamadas de entrada para a Unificação de Mensagens.

Por padrão, quando instala um servidor de Caixa de Correio do Exchange 2013, o pacote de idioma inglês norte-americano (en-US) é instalado. Essa é a única opção de idioma disponível para o seu plano de discagem, a menos que você instale outro pacote de idioma de UM. (O inglês norte-americano não poderá ser removido, a menos que você remova o servidor de Caixa de Correio do computador). Depois de instalar um pacote de idioma da UM em um servidor de Caixa Postal, o idioma associado ao pacote de idioma também será listado como uma opção disponível ao configurar o idioma padrão para o plano de discagem. Por padrão, já que um atendedor automático da UM está vinculado a um plano de discagem da UM quando é criado, ele usa a definição do idioma padrão do plano de discagem da UM vinculado. Entretanto, essa definição pode ser alterada após a criação de um atendedor automático da UM.


> [!NOTE]
> Se Inglês (Estados Unidos) for o único idioma que você desejar oferecer para seu plano de discagem, ignore esta etapa e vá para a etapa 2.



Você pode adicionar os pacotes de idiomas de Unificação de MENSAGENS usando o comando setup.exe ou executando o programa de instalação do *\<UMLanguagePack\>*.exe depois de baixar o pacote de idiomas de Unificação de MENSAGENS do [Exchange Server 2013 UM pacotes de idiomas](https://go.microsoft.com/fwlink/p/?linkid=266542). Para obter mais informações, consulte [Instalar um pacote de idiomas para UM](install-a-um-language-pack-exchange-2013-help.md).

Este exemplo usa o setup.exe para instalar o pacote do idioma japonês (ja-JP).

    setup.exe /AddUmLanguagePack:ja-JP /s:d:\Exchange\UMLanguagePacks /IAcceptExchangeServerLicenseTerms

## Etapa 2: Mover as saudações personalizadas, informes, menus e prompts do Exchange 2007 para a caixa de correio de sistema do Exchange 2013

As saudações personalizadas, informes, menus e prompts são usados pelos planos de discagem do Unificação de Mensagens e atendedores automáticos. A caixa de correio do sistema {e0dc1c29-89c3-4034-b678-e6c29d823ed9} é criada quando instala o Exchange 2007 ou Exchange 2013 e é usado para dar suporte a recursos como Aprovação de Mensagem e Pesquisa em Várias Caixas de Correio. A caixa de correio do sistema também é usada para armazenar planos de discagem e saudações, informes, menus e prompts personalizados de atendedores automáticos. Se a caixa de correio do sistema não existir, você pode usar o comando **Setup /PrepareAD** para criar uma.

Por padrão, as caixas de correio de sistema não estão visíveis no centro de administração do Exchange (EAC). Pode obter uma lista de caixas de correio de sistema executando um dos seguintes:

Este comando retorna uma lista de todas as caixas de correio de sistema.

    Get-Mailbox -Arbitration

Este comando retorna uma lista das caixas de correio de sistema e as propriedades ou definições individuais.

    Get-Mailbox -Arbitration |fl

Quando importa saudações, informes, menus e prompts personalizados do Exchange 2007 para o Exchange 2013, terá de usar o script MigrateUMCustomPrompts.ps1. Não pode usar o EAC para importar saudações, informes, menus e prompts personalizados. O script MigrateUMCustomPrompts.ps1 migra uma cópia de todas as saudações, informes, menus e prompts personalizadas da UM do Exchange Server 2007 para a UM do Exhchange 2013. Por padrão o script MigrateUMCustomPrompts.ps1 está localizado na pasta *\<Program Files\>*\\Microsoft\\Exchange Server\\V15\\Scripts num servidor de Caixa de Correio do Exchange 2013 e tem de ser executado a partir de um servidor de Caixa de Correio do Exchange 2013. Para executar o script:

1.  Clique em **Iniciar** \> **Todos os Programas** \> **Microsoft Exchange Server 2013** \> **Shell de Gerenciamento do Exchange**.

2.  No Shell de Gerenciamento do Exchange, no prompt, digite o caminho para o script. Por exemplo, digite **cd "D:\\Program Files\\Microsoft\\Exchange Server\\V15\\Scripts"** e pressione Enter.

3.  No prompt do Shell, digite **".\\MigrateUMCustomPrompts"** e pressione Enter.


> [!NOTE]
> Os prompts personalizados também podem ser importados individualmente com o cmdlet <STRONG>Import-UMPrompt</STRONG>. O cmdlet da UM do Exchange Server 2007 <STRONG>Copy-UMCustomPrompt</STRONG> não é suportado na UM do Exchange 2013 para cópia de prompts personalizados.



Quando executa o script MigrateUMCustomPrompts.ps1 do seu servidor do Exchange 2013, o script executa uma GUID ou pesquisa do identificador do objeto para o plano de discagem ou atendedor automático no Active Directory e consulta para determinar se existem algumas saudações, informes, menus e prompts personalizados. Se localizado, as saudações, informes, menus e prompts personalizados serão importado para a caixa de correio de sistema denominada {e0dc1c29-89c3-4034-b678-e6c29d823ed9}.

Ao usar esta caixa de correio de sistema, as saudações, informes, menus e prompts personalizados podem ser colocados num backup e restaurados com outras caixas de correio num banco de dados. Isso reduz a quantidade de recursos necessária. O armazenamento das saudações, informes, menus e prompts personalizados numa caixa de correio de sistema remove qualquer possibilidade de inconsistência que pode ocorrer. Para saber mais sobre mudanças da caixa de correio, consulte [Movimentações de caixa de correio no Exchange 2013](mailbox-moves-in-exchange-2013-exchange-2013-help.md).

## Etapa 3: Exportar e importar certificados

Se está a usar um SIP protegido ou planos de discagem Protegidos na sua organização do Exchange 2007, terá de exportar e importar os certificados que foram usados nos seus servidores de Acesso para Cliente e Caixa de Correio do Exchange 2013. O protocolo TLS mútuo (Transport Layer Security mútuo) é usado para criptografar dados enviados entres os servidores do Exchange 2013 e os gateways VoIP, PBXs IP e PBXs habilitados para SIP. Os certificados vinculam a identidade do proprietário do certificadoa uma par de chaves eletrônicas (pública e privada) que são usadas para criptografar e assinar informações digitalmente. Pode usar um dos seguintes certificadas para os serviços da UM e Roteador de Chamadas da UM:

  - Um certificado autoassinado (do Exchange)

  - Um certificado interno de infraestrutura de chave pública (PKI)

  - Um certificado comercial de terceiros

Por padrão, quando instala o Exchange 2013, são criados dois certificados autoassinados: **Certificado de autenticação de servidor do Exchange** e **Microsoft Exchange**. O certificado autoassinado do **Microsoft Exchange** pode ser usado para a UM para criptografar dados mas tem de atribuir o certificado aos serviços da UM e Roteador de Chamadas da UM. Este certificado autoassinado pode ser copiado e importado nos gateways VoIP, PBXs IP e PBXs habilitados para SIP. No entanto, não pode ser usado ao integrar a UM com o Microsoft Lync Server.

Para permitir que a UM criptografe os dados enviados entre os servidores do Exchange 2013 e os gateways VoIP, PBXs IP e PBXs habilitados para SIP, é necessário fazer o seguinte:

  - Use um certificado da UM existente autoassinado, crie um novo certificado do Exchange autoassinado, enviar uma solicitação de certificado a uma autoridade de certificação interna para um certificado PKI ou adquirir um certificado de terceiros comercial que pode usar para o TLS mútuo entre os servidores de Caixa de Correio e Acesso para Cliente do Exchange 2013 e gateways de VoIP, PBXs IP e PBXs habilitados para SIP.
    
    Crie um certificado autoassinado do Exchange usando o EAC, da seguinte forma:
    
    1.  No EAC, navegue para **Servidores** \> **Certificados** e clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar").
    
    2.  Na página **Novo Certificado do Exchange**, escolha **Criar um certificado autoassinado** e selecione **Avançar**.
    
    3.  Digite um nome amigável para o certificado e selecione **Avançar**.
    
    4.  Clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar") para selecionar o servidores do Exchange aos quais deseja aplicar o certificado e selecione **Avançar**.
    
    5.  Especifique os domínio que deseja incluir no seu certificado e selecione **Avançar**. Se desejar adicionar um domínio para o serviço, clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").
    
    6.  Verifique se os domínios que incluiu estão corretos e selecione **Concluir**.
    

    > [!IMPORTANT]
    > Quando usa o EAC para criar um certificado, você não será solicitado para habilitar os serviços para o certificado. Depois do certificado ser criado, pode usar o EAC para habilitar os serviços. Para obter mais informações sobre como habilitar um certificado para serviços, consulte <A href="assign-a-certificate-to-the-um-and-um-call-router-services-exchange-2013-help.md">Atribuir um certificado para os serviços de Unificação de mensagens e o roteador de chamada UM</A>.

    
    Crie um certificado autoassinado do Exchange executando o seguinte comando no Shell.
    
        New-ExchangeCertificate -Services 'UM, UMCallRouter' -DomainName '*.northwindtraders.com' -FriendlyName 'UMSelfSigned' -SubjectName 'C=US,S=WA,L=Redmond,O=Northwindtraders,OU=Servers,CN= Northwindtraders.com' -PrivateKeyExportable $true
    

    > [!TIP]
    > Se especificar os serviços que deseja habilitar usando o parâmetro <EM>Services</EM>, você será solicitado para habilitar os serviços para o certificado que criou. Neste exemplo, você será solicitado para habilitar o certificado para os serviços da Unificação de Mensagens e Roteador de Chamadas da Unificação de Mensagens. Para obter mais informações sobre como habilitar um certificado para serviços, consulte <A href="assign-a-certificate-to-the-um-and-um-call-router-services-exchange-2013-help.md">Atribuir um certificado para os serviços de Unificação de mensagens e o roteador de chamada UM</A>.



  - Importe o certificado que será usado em todos os servidores de Acesso para Cliente e Caixa de Correio do Exchange 2013 na sua organização. Se usar o certificado autoassinado do Exchange 2013, terá de copiar o certificado e, em seguida, importá-los nos gateways VoIP, PBXs IP e PBXs habilitados para SIP. Se usar o certificado autoassinado do Exchange 2007, o Nome Alternativo da Entidade (SAN) deve conter os nome de máquina de todos os servidores do Exchange 2013. Se tiver servidores de Unificação de Mensagens do Exchange 2007 na sua organização, você pode usar o certificado autoassinado do Exchange 2013, mas tem de adicionar os nomes de máquina dos serviços da UM do Exchange 2007 para o SAN no certificado do Exchange 2013.

  - Habilite ou atribua o certificado a ser usado nos serviços da UM e de Roteador de Chamadas de UM nos servidores de Acesso para Cliente e Caixa de Correio na sua organização.
    
    Habilite o serviço da UM e o serviço de Roteador de Chamadas da UM em todos os servidores do Exchange 2013 para usar o certificado autoassinado usando o EAC, da seguinte forma:
    
    1.  No EAC, navegue para **Servidores** \> **Certificados**, selecione o certificado no qual deseja habilitar os serviços e, em seguida, clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").
    
    2.  Na página **Procedimento**, selecione **Serviços**, selecione **Unificação de Mensagens** e, em seguida, selecione **Roteador de chamadas da Unificação de Mensagens**.
    
    Habilite um certificado autoassinado do Exchange executando o seguinte comando no Shell.
    
        Enable-ExchangeCertificate -Thumbprint 5113ae0233a72fccb75b1d0198628675333d010e -Services 'UM, UMCallRouter'

  - Configure quaisquer planos de discagem da UM novos ou existentes como SIP protegido ou Protegido.

  - Configure o modo de inicialização da UM para TLS ou modo Duplo nos servidores de Acesso para Cliente e Caixa de Correio na sua organização.

  - Crie e configure gateways IP de UM novos ou existentes com um nome de domínio totalmente qualificado (FQDN).

  - Configure a porta de escuta nos gateways IP de UM para usar a porta 5061 para TLS.

  - Reinicie o serviço de Roteador de Chamadas da UM em todos os servidores de Acesso para Cliente do Exchange 2013 e reinicie o serviço de UM em todos os servidores de Caixa de Correio do Exchange 2013. Para saber mais sobre os serviços de UM, consulte [Serviços de Unificação de mensagens](um-services-exchange-2013-help.md).

## Etapa 4: Configurar o modo de inicialização de UM todos os servidores de Acesso para Cliente do Exchange 2013

Se está a usar planos de discagem de SIP protegido ou Protegido, tem de configurar o modo de inicialização de UM nos seus servidores de Acesso para Cliente do Exchange 2013. Pode especificar o modo de inicialização de UM para o serviço de Roteador de Chamadas da UM num servidor de Acesso para Cliente do Exchange 2013 usando o EAC ou o Shell. Por padrão, o servidor de Acesso para Cliente do Exchange 2013 irá inicializar no modo TCP, mas se você está usando TLS (Transport Layer Security) para criptografar o tráfego de VoIP (Voice over IP), você precisa de configurar o servidor de Acesso para Cliente do Exchange 2013 para usar TLS ou o modo Duplo. Recomendamos que todos os servidores de Acesso para Cliente do Exchange 2013 sejam configurados para usar o modo Duplo como o modo de inicialização da UM. sso porque todos os servidores de Acesso para Cliente do Exchange 2013 atendem todas as chamadas de entrada para todos os planos de discagem de UM, e esses planos de discagem podem ter configurações de segurança diferentes. Se alterar o modo de inicialização da UM, é preciso reiniciar o serviço de Roteador de Chamadas da UM para que a alteração tenha efeito. Para saber mais sobre os serviços de UM, consulte [Serviços de Unificação de mensagens](um-services-exchange-2013-help.md).

Configure o modo de inicialização de UM no servidor de Acesso para Cliente do Exchange 2013 usando o EAC, da seguinte forma:

1.  No EAC, navegue até **Servidores** \> **Servidores**.

2.  No modo de exibição de lista, selecione o servidor do Exchange que deseja modificar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na página **Exchange Server**, clique em **Unificação de Mensagens**.

4.  Em **Definiçõs do Roteador de Chamadas de UM** \> **Modo de inicialização de UM**, selecione um dos seguintes da lista suspensa:
    
      - **TCP**   Use esta opção se não está usando mTLS e está usando apenas os planos de discagem Não protegidos.
    
      - **TLS**   Use esta opção se não está usando mTLS e está usando apenas planos de discagem de SIP protegido e Protegido.
    
      - **DUPLO**   Use esta opção se está usando mTLS e está usando os planos de discagem Não protegido, SIP protegido e Protegido.

5.  Depois de selecionar o modo de inicialização de UM, clique em **Salvar**.

Configure um modo de inicialização de UM num servidor de Acesso para Cliente do Exchange Online executando o seguinte comando no Shell.

    Set-UMCallRouterSettings -Server MyUMCallRouter.northwindtraders.com -UMStartupMode Dual

## Etapa 5: Configurar o modo de inicialização de UM em todos os servidores de Caixa de Correio do Exchange 2013

Se está usando planos de discagem de SIP protegido ou Protegido, tem de configurar o modo de inicialização de UM nos seus servidores de Caixa de Correio do Exchange 2013. Pode especificar o modo de inicialização de UM para o serviço de UM num servidor de Caixa de Correio do Exchange 2013 usando o EAC ou o Shell. Por padrão, um servidor de Caixa de Correio do Exchange 2013 irá inicializar no modo TCP, mas se você está usando TLS (Transport Layer Security) para criptografar o tráfego de VoIP (Voice over IP), você precisa de configurar o servidor de Caixa de Correio do Exchange 2013 para usar TLS ou o modo Duplo. Recomendamos que todos os servidores de Caixa de Correio do Exchange 2013 sejam configurados para usar o modo Duplo como o modo de inicialização de UM. Isso porque todos os servidores de Caixa de Correio do Exchange 2013 atendem todas as chamadas de entrada para todos os planos de discagem de UM, e esses planos de discagem podem ter configurações de segurança diferentes. Se alterar o modo de inicialização da UM, é preciso reiniciar o serviço de UM para que a alteração tenha efeito. Para saber mais sobre os serviços de UM, consulte [Serviços de Unificação de mensagens](um-services-exchange-2013-help.md).

Configure o modo de inicialização de UM no servidor de Caixa de Correio do Exchange 2013 usando o EAC, da seguinte forma:

1.  No EAC, navegue até **Servidores** \> **Servidores**.

2.  No modo de exibição de lista, selecione o servidor do Exchange que deseja modificar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na página **Exchange Server**, clique em **Unificação de Mensagens**.

4.  Em **Definiçõs do Serviço de UM** \> **Modo de inicialização de UM**, selecione um dos seguintes da lista suspensa:
    
      - **TCP**   Use esta opção se não está usando mTLS e está usando apenas os planos de discagem Não protegidos.
    
      - **TLS**   Use esta opção se não está usando mTLS e está usando apenas planos de discagem de SIP protegido e Protegido.
    
      - **DUPLO**   Use esta opção se está usando mTLS e está usando os planos de discagem Não protegido, SIP protegido e Protegido.

5.  Depois de selecionar o modo de inicialização de UM, clique em **Salvar**.

Configure um modo de inicialização de UM num servidor de Caixa de Correio do Exchange Online executando o seguinte comando no Shell.

    Set-UMService -Identity MyUMServer -ExternalHostFqdn host.external.contoso.com -IPAddressFamily Any -UMStartupMode Dual

## Etapa 6: Criar ou configurar planos de discagem de UM existentes

Dependendo da sua implantação existente do Exchange 2007, poderá ter de criar novos planos de discagem de UM ou configurar os planos de discagem existentes. Um plano de discagem de UM representa um conjunto de Private Branch eXchanges (PBXs) tradicional ou habilitados para SIP, PBXs IP ou PBXs habilitados para SIP que compartilham números de ramais de usuário comuns. Todos os ramais de usuários hospedados em PBXs tradicionais ou habilitados para SIP ou PBXs IP dentro de um plano de discagem contêm o mesmo número de dígitos. Os usuários podem discar para outros ramais telefônicos sem a necessidade de acrescentar um número especial ao ramal ou discar o número completo do telefone.

Os planos de discagem de UM são usados na Unificação de Mensagens para garantir que os ramais de telefone do usuário sejam exclusivos. Em algumas redes de telefonia, existem vários PBXs IP, PBSx tradicionais ou PBXs habilitados para SIP. Nessas redes de telefonia, pode haver dois usuários com o mesmo ramal telefônico. Os planos de discagem da UM resolvem esta situação. Colocar os dois usuários em dois planos de discagem de UM separados torna seus ramais exclusivos. Para mais informações, consulte [Planos de discagem de Unificação de mensagens](um-dial-plans-exchange-2013-help.md).

Se necessário, pode criar um plano de discagem de UM usando o EAC:

1.  No EAC, navegue para **Unificação de Mensagens** \> **Planos de discagem de UM** e, em seguida, clique em **Novo**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar").

2.  Na página **Novo Plano de Discagem de UM**, complete o seguinte:
    
      - **Nome**   Digite o nome do plano de discagem. O nome plano de discagem de UM é obrigatório e deve ser exclusivo. Porém, o nome que você digitar será usado apenas para exibição no EAC e no Shell. O comprimento máximo de nome de plano de discagem de UM é 64 caracteres e pode incluir espaços. Entretanto, não pode incluir nenhum dos seguintes caracteres: " / \\ \[ \] : ; | = , + \* ? \< \>.
        
        Embora a caixa para o nome do plano de discagem possa aceitar 64 caracteres, esse nome não pode ter mais de 49 caracteres. Se você tentar criar um nome de plano de discagem com mais de 49 caracteres, receberá uma mensagem de erro. A mensagem indicará que não foi possível gerar a política de caixa de correio da UM porque o nome do plano de discagem da UM é muito longo. Isso ocorre porque, ao criar um plano de discagem, uma política de caixa de correio de UM padrão também é criada com o nome de *\<Política Padrão\>***DialPlanName**. Quando os 15 caracteres na política padrão são adicionados ao nome do plano de discagem, o total de caracteres excede o limite. O parâmetro *name* do plano de discagem de UM e da política de caixa de correio de UM pode ter 64 caracteres. Contudo, se o nome do plano de discagem tiver mais de 49 caracteres, o nome da política de caixa de correio de UM padrão terá mais de 64 caracteres, não sendo permitido pelo sistema.
    
      - **Comprimento do ramal (dígitos)**   Insira o número de dígitos para os números de ramal no plano de discagem. O número de dígitos em números de ramal baseia-se no plano de discagem de telefonia criado em um PBX. Por exemplo, se um usuário associado a um plano de discagem de telefonia discar um ramal com quatro dígitos para chamar outro usuário do mesmo plano de discagem de telefonia, selecione 4 como o número de dígitos do ramal.
        
        Essa é uma caixa necessária que tem um intervalo de valor de 1 a 20. O tamanho de ramal normalmente varia de 3 a 7 números. Se o ambiente de telefonia existente incluir números de ramais, será preciso especificar um número de dígitos que corresponda ao número de dígitos nesses ramais.
        
        Ao criar um plano de discagem de ramal telefônico, você é obrigado a inserir um número de ramal para o usuário quando está vinculado a um plano de discagem de ramal telefônico. Um número de ramal é também necessário com planos de discagem de Session Initiation Protocol (SIP) ou planos de discagem E.164 quando um usuário habilitado para UM é vinculado a um plano de discagem URI SIP ou E.164. O número de ramal é usado pelos usuários do Outlook Voice Access quando acessam sua caixa de correio do Exchange.
    
      - UNRESOLVED\_TOKENBLOCK\_VAL(Tipo UI\_URI)
    
      - UNRESOLVED\_TOKENBLOCK\_VAL(Segurança UI\_VoIP)
    
      - **Código de País/Região**   Use esta caixa para digitar o código numérico de país/região usado para chamadas de saída. Esse número precederá automaticamente o número de telefone discado. Essa caixa aceita de 1 a 4 dígitos. Por exemplo, nos Estados Unidos, o código de país/região é 1. No Reino Unido, é 44.

3.  Clique em **Salvar**.

Se necessário, pode criar um plano de discagem de UM executando o seguinte comando no Shell.

    New-UMDialplan -Name MyUMDialPlan -URIType E164 -NumberOfDigitsInExtension 5 -VoIPSecurity Secured

Se necessário, pode configurar um plano de discagem de UM existente usando o EAC:

1.  No EAC, navegue até **Unificação de Mensagens** \> **Planos de discagem de UM**.

2.  No modo de exibição de lista, selecione o plano de discagem de UM que você deseja modificar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na página **Plano de discagem de UM**, clique em **Configurar**. Use as opções de configuração para exibir configurações de plano de discagem específicas e habilitar ou desabilitar recursos.

Se necessário, pode configurar um plano de discagem de UM existente executando o seguinte comando no Shell.

    Set-UMDialplan -Identity MyDialPlan -AccessTelephoneNumbers 4255551234 -AudioCodec Wma -CallAnsweringRulesEnabled $false -OutsideLineAccessCode 9 -VoIPSecurity SIPSecured

Quando implantou a Unificação de Mensagens do Exchange 2007, precisou de adicionar um servidor de Unificação de Mensagens a um plano de discagem de UM, para ele atender chamadas de entrada. Isso não é mais necessário. No Exchange 2013, os servidores de Acesso para Cliente e de Caixa de Correio não podem ser vinculados a um ramal telefônico ou plano de discagem E.164, mas precisam ser vinculados a planos de discagem de URI do SIP. Os servidores de Acesso para Cliente e de Caixa de Correio responderão todas as chamadas de entrada de todos os tipos de planos de discagem.

## Etapa 7: Criar ou configurar gateways IP de UM existentes

Dependendo da sua implantação existente do Exchange 2007, poderá ter de criar novos gateways IP de UM ou configurar os gateways existentes. Se está usando planos de discagem de SIP protegido ou Protegido, precisa de cirar um gateway IP de UM com um FQDN e usar o Shell para configurá-lo para que escute na porta 5061. Para gateways IP de UM existentes, verifique se estão configurados com um FQDN e estão escutando na porta 5061. Se o gateway IP de UM não usa um FQDN, use o EAC ou o Shell para alterar o endereço. Se um gateway IP de UM não usa a porta 5061, use o Shell para alterar a porta. Pode exibir as definições de gateway IP de UM usando o cmdlet **Get-UMIPGateway**.

Um gateway IP de UM representa um gateway físico de VoIP (Voice over IP), PBX IP ou PBX habilitado para SIP. Antes que um gateway VoIP, PBX IP ou PBX habilitado com SIP possa ser usado para responder chamadas de entrada e enviar chamadas de saída para usuários de correio de voz, um gateway IP de UM deve ser criado no serviço de diretório.

A combinação do objeto de gateway IP de UM e um objeto de grupo de busca de UM estabelece um vínculo entre um gateway VoIP, um PBX IP ou PBX habilitado com SIP e um plano de discagem de UM. Ao criar vários grupos de busca de UM, você pode associar um gateway IP de UM único com vários planos de discagem de UM. Para mais informações, consulte [Gateways IP de UM](um-ip-gateways-exchange-2013-help.md).

Se necessário, pode criar um gateway IP de UM usando o EAC, da seguinte forma:

1.  No EAC, navegue para **Unificação de Mensagens** \> **Gateways IP de UM** e, em seguida, clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar").

2.  Na página **Novo gateway IP de UM**, insira as seguintes informações:
    
      - **Nome**   Use essa caixa para especificar um nome exclusivo para o gateway IP da UM. Esse é um nome de exibição que aparece no EAC. Se você precisar alterar o nome de exibição do gateway IP de UM depois de sua criação, primeiro exclua o gateway IP de UM existente e depois crie outro com o nome apropriado. O nome do gateway IP de UM é necessário, mas é usado apenas para fins de exibição. Como sua organização pode usar vários gateways IP de UM, recomendamos que você use nomes significativos para os gateways IP de UM. O comprimento máximo de um nome de gateway IP de UM é 64 caracteres e pode incluir espaços. Entretanto, não pode incluir nenhum dos seguintes caracteres: " / \\ \[ \] : ; | = , + \* ? \< \>.
    
      - **Endereço**   Você pode configurar um gateway IP de UM com um endereço IPv4 ou IPv6 ou um FQDN. Use essa caixa para especificar o endereço IP ou FQDN configurado no gateway VoIP, PBX IP ou PBX habilitado para SIP. Essa caixa aceita somente FQDNs válidos e formatados corretamente.
        
        Você pode digitar caracteres alfanuméricos. FQDNs, endereços IPv6 e endereços IPv4 são suportados. Se você quiser usar TLS mútuo entre um gateway de IP de UM e um plano de discagem funcionando no modo SIP seguro ou Protegido, você deverá configurar o gateway IP de UM com um FQDN. Você também deve configurá-lo para escutar na porta 5061 e verificar se gateways VoIP ou PBXs IP também foram configurados para escutar solicitações de TLS mútuas na porta 5061. Para configurar um gateway IP de UM, execute o seguinte comando no Shell: `Set-UMIPGateway -identity MyUMIPGateway -Port 5061`
        
        Se você usar um FQDN, você também deve se certificar que configurou corretamente um registro de host DNS para o gateway VoIP, PBX IP ou PBX habilitado para SIP de modo que o nome de host seja resolvido corretamente para um endereço IP. Se você utilizar um FQDN em vez de um endereço IP, e a configuração DNS para o gateway IP de UM for alterada, você deverá desabilitar e, em seguida, habilitar o gateway IP de UM para certificar-se de que as informações de configuração do gateway IP de UM estejam atualizadas corretamente.
    
      - **Plano de Discagem de UM**   Clique em **Procurar** para selecionar o plano de discagem de UM que deseja associar a um gateway IP de UM. Quando você seleciona um plano de discagem de UM para associar a um gateway IP de UM, um número coletivo padrão de UM é também criado e associado ao plano de discagem de UM selecionado. Se você não selecionar um plano de discagem de UM, deverá criar manualmente um grupo de busca de UM e depois associar esse grupo de busca de UM ao gateway IP de UM que você criou.

3.  Clique em **Salvar**.

Se necessário, pode criar um gateway IP de UM executando o seguinte comando no Shell.

    New-UMIPGateway -Identity MyUMIPGateway -Address "MyUMIPGateway.contoso.com"

Se necessário, pode configurar um gateway IP de UM existente usando o EAC:

1.  No EAC, navegue para **Unificação de Mensagens** \> **Gateways IP de UM** e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

2.  Na página **Gateway IP de UM**, clique em **Configurar**. Use as opções de configuração para exibir configurações do gateway IP de UM específicas e habilitar ou desabilitar recursos.

Se necessário, pode configurar um gateway IP de UM existente executando o seguinte comando no Shell.

    Set-UMIPGateway -Identity MyUMIPGateway -Address fe80::39bd:88f7:6969:d223%11 -IPAddressFamily Any -Status Disabled -OutcallsAllowed $false

## Etapa 8: Criar um grupo de busca da UM

Dependendo da sua implantação existente do Exchange 2007, poderá ter de criar novos grupos de busca de UM. Um grupo de busca de telefonia fornece uma maneira de distribuir chamadas telefônicas a partir de um único número para diversos ramais ou números de telefone. Na Unificação de Mensagens, um grupo de busca de UM é uma representação lógica de um grupo de busca de telefonia e vincula um gateway IP de UM a um plano de discagem de UM.

Você precisa ter pelo menos um grupo de busca de UM para cada grupo de busca de PBX IP ou PBX. Quando você concluir o procedimento a seguir, um grupo de busca de UM será criado por padrão. Se você tiver mais de um grupo de busca de PBX IP ou PBX, precisará criar grupos de busca de UM adicionais. Para saber mais sobre grupos de busca de UM, consulte [Grupos de busca de Unificação de mensagens](um-hunt-groups-exchange-2013-help.md).

Se necessário, pode criar um grupo de busca de UM usando o EAC:

1.  No EAC, navegue até **Unificação de Mensagens** \> **Planos de discagem de UM**. No modo de exibição de lista, selecione o plano de discagem de UM que deseja modificar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

2.  Na página **Plano de Discagem de UM**, em **Grupos de Busca de UM**, clique em **Novo**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar").

3.  Na página **Novo Grupo de Busca de UM**, insira as seguintes informações:
    
      - **Nome**   Use esta caixa para criar o nome de exibição do grupo de busca de UM. Um nome para o grupo de busca de UM é exigido e deve ser exclusivo, porém ele é usado apenas para fins de exibição no EAC e no Shell. Se for necessário alterar o nome para exibição do grupo de busca depois de sua criação, será necessário excluir o grupo de busca existente e criar outro grupo de busca com o nome adequado. Se sua organização utilizar vários grupos de busca, recomendamos que você use nomes significativos para eles. O comprimento máximo do nome do grupo de busca de UM é 64 caracteres, dentre os quais pode haver espaços. Entretanto, não pode incluir nenhum dos seguintes caracteres: " / \\ \[ \] : ; | = , + \* ? \< \>.
    
      - **Gateway IP de UM**   Use esta caixa para selecionar um gateway IP de UM. Esta caixa mostra o nome do gateway IP de UM que será vinculado ao grupo de busca de UM. Para vincular um gateway IP de UM a um grupo de busca de UM, clique em **Procurar**.
    
      - **Identificador Piloto**   Use esta caixa para especificar uma cadeia de caracteres que identifique exclusivamente o identificador piloto configurado no PBX ou no PBX IP. É possível usar um número de ramal ou um URI (Uniform Resource Identifier) SIP nesta caixa. Caracteres alfanuméricos são aceitos nesta caixa. Para PBXs herdados, é usado um valor numérico com identificador piloto. No entanto, alguns PBXs IP e PBXs habilitados para SIP podem usar URIs SIP.

4.  Clique em **Salvar**.

Se necessário, pode criar um grupo de busca de UM executando o seguinte comando no Shell.

    New-UMHuntGroup -Name MyUMHuntGroup -PilotIdentifier 5551234,55555 -UMDialPlan MyUMDialPlan -UMIPGateway MyUMIPGateway


> [!TIP]
> Não pode configurar ou alterar as definições de um grupo de busca de UM. Se desejar alterar as definições de configuração em um grupo de busca de UM, exclua-o e adicionar um novo grupo de busca de UM com as configurações corretas.



## Etapa 9: Criar ou configurar atendedores automáticos de UM

Dependendo da sua implantação existente do Exchange 2007, poderá ter de criar novos atendedores automáticos de UM. Você pode usar atendedores automáticos de UM para criar um sistema de menus de voz que permita aos chamadores externos e internos usem o sistema de menus do atendedor automático de UM para localizar pessoas e fazer ou transferir chamadas para usuários da empresa ou departamentos numa organização. Para mais informações, consulte [Responder e rotear as chamadas de entrada automaticamente](automatically-answer-and-route-incoming-calls-exchange-2013-help.md).

Em implantações menores, você pode querer implantar a UM apenas para deixar mensagens de caixa postal para os usuários. Nessas implantações, criar um atendente automático não é necessário. Entretanto, na maioria dos casos, usar atendedores automáticos é muito útil para chamadores externos que ligarem para a sua organização.

Se necessário, pode criar um atendedor automático de UM usando o EAC, da seguinte forma:

1.  No EAC, navegue até **Unificação de Mensagens** \> **Planos de discagem de UM**. Selecione o plano de discagem da UM ao qual deseja adicionar a um atendedor automático e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

2.  Na página **Plano de discagem de UM**, em **Atendedores Automaticos de UM**, clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar").

3.  Na página **Novo Atendedor Automática de UM**, preencha as seguintes caixas:
    
      - **Nome**   Use essa caixa para criar o nome de exibição do atendedor automático de UM. O nome do atendedor automático de UM é necessário e deve ser exclusivo. Porém, ele é usado apenas para exibição no EAC e no Shell. Se for necessário alterar o nome de exibição do atendedor automático após sua criação, primeiro você deverá excluir o atendedor automático de UM existente e criar outro atendedor com o nome adequado. Se sua organização usa vários atendedores automáticos de UM, é recomendável usar nomes significativos para seus atendedores automáticos de UM. O tamanho máximo do nome do atendedor automático de UM é 64 caracteres, podendo incluir espaços.
        
        Embora seja possível usar espaços ao dar um nome para um novo atendedor automático de UM, se você integrar a Unificação de Mensagens ao Lync Server, o nome do atendedor automático não poderá incluir espaços. Sendo assim, se você criar um atendedor automático com espaços no nome de exibição e estiver fazendo a integração com o Lync Server, primeiro exclua o atendedor automático e depois crie outro que não inclua espaços no nome de exibição.
    
      - **Criar este atendedor automático como habilitado**   Marque esta caixa de seleção para permitir que o atendedor automático atenda chamadas de entrada quando você concluir a criação do atendedor automático de UM. Por padrão, o novo atendedor automático é criado como desabilitado. Se você decidir criar o atendedor automático de UM como desabilitado, você pode usar o EAC ou o Shell para habilitar o atendedor automático após concluir a criação do atendedor automático.
    
      - **Configurar o atendedor automático para responder a comandos de voz**   Marque esta caixa de seleção para habilitar o atendedor automático de UM para voz. Se o atendedor automático for habilitado para fala, os chamadores poderão responder aos prompts do sistema ou prompts personalizados usados pelo atendedor automático de UM usando entradas de discagem por tom ou voz. Por padrão, quando um atendedor automático é criado, não está habilitado para fala. Para que os chamadores usem um atendedor automático habilitado para fala em um idioma diferente do Inglês dos EUA (en-US), é necessário instalar o pacote de idioma de UM apropriado e configurar as propriedades do atendedor automático para usar esse idioma. O pacote de idioma de UM en-US é instalado por padrão quando você instala um servidor de Caixa de Correio do Exchange 2013.
    
      - **Números de acesso**   Digite os números de ramal ou de telefone que os chamadores utilizarão para acessar o atendedor automático. Digite um número de ramal ou telefone na caixa e clique em **Adicionar** para incluir o número na lista. A quantidade de dígitos do número de ramal ou telefone fornecido não precisa corresponder à quantidade de dígitos do ramal configurado no plano de discagem de UM associado. Isso se deve porque os atendedores automáticos de UM podem fazer chamadas diretas.
        
        O número de ramais ou números de acesso inseridos é ilimitado. Entretanto, você pode criar um novo atendedor automático sem listar um número de ramal ou de telefone. Não é obrigatório fornecer um número de ramal ou telefone. É possível editar ou remover um número de ramal ou identificador piloto existente. Para editar um número de ramal ou telefone existente, clique em **Editar**. Para remover da lista um número de ramal ou telefone existente, clique em **Remover**.

4.  Clique em **Salvar**.

Se necessário, pode criar um atendedor automático de UM executando o seguinte comando no Shell.

    New-UMAutoAttendant -Name MyUMAutoAttendant -UMDialPlan MyUMDialPlan -PilotIdentifierList 56000,56100 -SpeechEnabled $true -Status Enabled

Se necessário, pode configurar um antendedor automático de UM existente usando o EAC:

1.  No EAC, navegue para **Unificação de Mensagens** \> **Planos de discagem de UM** e, em seguida, clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

2.  Na página **Plano de discagem de UM**, em **Atendedores Automáticos de UM**, selecione o atendedor automático de UM que deseja exibir e configurar e, em seguida, clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição"). Use as opções de configuração para exibir configurações de atendedor automático específicas e habilitar ou desabilitar recursos.

Se necessário, pode configurar um atendedor automático de UM existente executando o seguinte comando no Shell.

    Set-UMAutoAttendant -Identity MySpeechEnabledAA -DTMFFallbackAutoAttendant MyDTMFAA -OperatorExtension 50100 -AfterHoursTransferToOperatorEnabled $true -StaroutToDialPlanEnabled $true

## Etapa 10: Criar ou configurar políticas de caixa de correio de UM

Dependendo da sua implantação existente do Exchange 2007, poderá ter de criar novas políticas de caixa de correio de UM ou configurar políticas de caixa de correio de UM existentes. As políticas de caixa de correio de UM são necessárias quando os usuários são habilitados para a Unificação de Mensagens. A caixa de correio de cada usuário habilitado para UM deve estar vinculada a uma única política de caixa de correio de UM. Depois de criar uma política de caixa de correio de UM, você vincula uma ou mais caixas de correio habilitadas para UM à política de caixa de correio de UM. Isso permite controlar as configurações de segurança de PIN, como o número mínimo de dígitos em um PIN ou o número máximo de tentativas de logon para os usuários habilitados para UM que estão vinculados à política de caixa de correio de UM. Para mais informações, consulte [políticas de caixa de correio de UM](um-mailbox-policies-exchange-2013-help.md).

Se necessário, pode criar uma política de caixa de correio de UM usando o EAC:

1.  No EAC, navegue até **Unificação de Mensagens** \> **Planos de discagem de UM**. No modo de exibição de lista, selecione o plano de discagem de UM que deseja modificar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

2.  Na página **Plano de discagem de UM**, em **Políticas de Caixa de Correio de UM**, clique em **Adicionar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na página **Nova Política de Caixa de Correio de UM**, na caixa **Nome**, digite o nome da política de caixa de correio de UM.
    

    > [!NOTE]
    > Use essa caixa para especificar um nome exclusivo para a política de caixa de correio de UM. Esse é um nome de exibição que aparece no EAC. Se for necessário alterar o nome de exibição da política de caixa de correio de UM depois que ela foi criada, primeiro você deverá excluir a política de caixa de correio de UM existente e, em seguida, criar outra política de caixa de correio de UM com o nome adequado. Não será possível excluir uma política de caixa de correio da UM se algum usuário habilitado para UM estiver associado a ela. O nome da política de caixa de correio da UM é obrigatório, mas é usado apenas para fins de exibição. Como sua organização pode utilizar várias políticas de caixa de correio de UM, recomendamos que você use nomes significativos para elas. O comprimento máximo para um nome de política de caixa de correio de UM é de 64 caracteres e pode conter espaços. Entretanto, não pode incluir nenhum dos seguintes caracteres: " / \ [ ] : ; | = , + * ? &lt; &gt;.



4.  Clique em **Salvar**.
    

    > [!NOTE]
    > Quando você salva a política de caixa de correio de UM, todas as configurações padrão, incluindo as políticas de PIN, os recursos de caixa postal e as configurações de Caixa Postal Protegida são habilitadas. Se quiser personalizar ou alterar quaisquer configurações padrão da política de caixa de correio de UM recém-criada, use o cmdlet <STRONG>Set-UMMailbox</STRONG> ou o EAC.



Se necessário, pode criar uma política de caixa de correio de UM executando o seguinte comando no Shell.

    New-UMMailboxPolicy -Name MyUMMailboxPolicy -UMDialPlan MyUMDialPlan

Se necessário, pode configurar uma política de caixa de correio de UM existente usando o EAC:

1.  No EAC, navegue para **Unificação de Mensagens** \> **Planos de discagem de UM** e, em seguida, clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

2.  Na página **Plano de discagem de UM**, em **Políticas de Caixa de Correio de UM**, selecione a política de caixa de correio de UM que pretende exibir ou configurar e, em seguida, clique em**Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição"). Use as opções de configuração para exibir definições de política de caixa de correio de UM específicas e habilitar ou desabilitar recursos.

Se necessário, pode configurar uma política de caixa de correio de UM existente executando o seguinte comando no Shell.

    Set-UMMailboxPolicy -Identity MyUMMailboxPolicy -LogonFailuresBeforePINReset 8 -MaxLogonAttempts 12 -MinPINLength 8 -PINHistoryCount 10 -PINLifetime 60 -ResetPINText "The PIN used to allow you access to your mailbox using Outlook Voice Access has been reset."

## Etapa 11: Mover caixas de correio habilitadas para UM existentes para o Exchange 2013

Na Unificação de Mensagens do Exchange 2007, depois de habilitar usuários na organização para usarem caixa postal, um conjunto padrão de propriedades de UM é aplicado ao usuário e ele poderá usar os recursos de UM. Para mais informações, consulte [Caixa postal para usuários](voice-mail-for-users-exchange-2013-help.md).

Durante o processo de atualização, haverá o período de tempo em que terá caixas de correio habilitadas para UM tanto nos servidores de Caixa de Correio do Exchange 2007 e nos servidores de Caixa de Correio do Exchange 2013. No entanto, se está a mover todos os usuários habilitados para UM para servidores de Caixa de Correio do Exchange 2013, tem de usar o EAC ou o cmdlet **New-MoveRequest** no Shell a partir de um servidor do Exchange 2013 para reter todas as propriedades e definições, incluindo o PIN do usuário.

Uma solicitação de movimentação é o processo de mover uma caixa de correio de um banco de dados de caixa de correio para outro. Uma solicitação de movimentação local é uma movimentação de caixa de correio que ocorre dentro de uma única floresta. Para obter mais informações sobre movimentos de caixas de correio, consulte:

  - [Movimentações de caixa de correio no Exchange 2013](mailbox-moves-in-exchange-2013-exchange-2013-help.md)

  - [New-MoveRequest](https://technet.microsoft.com/pt-br/library/dd351123\(v=exchg.150\))

  - [New-MigrationBatch](https://technet.microsoft.com/pt-br/library/jj219166\(v=exchg.150\))

  - [Mover caixas de correio](https://go.microsoft.com/fwlink/p/?linkid=296351)

Para mover um caixa de correio do Exchange 2007 para um servidor de Caixa de Correio do Exchange 2013 usando o EAC:

1.  No EAC, clique em **Destinatário** \> **Migração** e, em seguida, clique em **Adicionar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

2.  No assistente **Nova movimentação local de caixa de correio**, selecione o usuário que deseja mover, clique em **OK** e, em seguida, clique em **Avançar**.

3.  Na página **Configuração da movimentação**, especifique um nome para o novo lote. Selecione quais opções que deseja para a caixa de correio do arquivo e para localização do banco de dados da caixa de correio e clique em **Nova**.

Para mover uma caixa de correio do Exchange 2007 para um servidor de Caixa de Correio do Exchange 2013 usando o Shell, execute o seguinte comando.

    New-MoveRequest -Identity 'tony@alpineskihouse.com' -TargetDatabase "DB01"

## Etapa 12: Habilitar novos usuários para UM ou configurar definições para usuários habilitados para UM existentes

Um usuário deve ter uma caixa de correio antes de poder ser habilitado para Unificação de Mensagens. Mas, por padrão, um usuário que tenha uma caixa de correio não está habilitado para a UM. Depois que o usuário for habilitado para UM, você poderá gerenciar, modificar e configurar as propriedades de UM e de caixa postal do usuário. Pode habilitar um usuário para UM usando o EAC ou o Shell. Saiba mais em [Caixa postal para usuários](voice-mail-for-users-exchange-2013-help.md).

Quando você habilita um usuário para UM, deve definir pelo menos um número de ramal que será usado pela UM quando a caixa postal for enviada para a caixa de correio do o usuário e para habilitar o usuário de usar o Outlook Voice Access. Depois de habilitar o usuário para UM, você poderá adicionar números de ramal secundários à caixa de correio do usuário, bem como modificá-los ou removê-los, configurando o endereço de proxy da Unificação de Mensagens (EUM) do Exchange na caixa de correio do usuário, ou adicionar ou remover os ramais adicionais ou secundários do usuário no EAC. Para adicionar, modificar e remover os números de ramal, números E.164 ou endereços SIP, consulte [Procedimentos do usuário habilitado para email de voz](voice-mail-enabled-user-procedures-exchange-2013-help.md).

Para habilitar um usuário para Unificação de Mensagens usando o EAC:

1.  No EAC, clique em **Destinatários**.

2.  Na exibição de lista, selecione o usuário cuja caixa de correio deseja habilitar para a Unificação de Mensagens.

3.  No painel Detalhes, em **Telefone e Recursos de Voz**, clique em **Habilitar**.

4.  Na página **Habilitar caixa de correio de UM**, clique no botão **Procurar** ao lado de **Política de caixa de correio de UM**, localize a política de caixa de correio de UM, para atribuir o usuário a partir da lista, e clique em **OK**.

5.  Na página **Habilitar caixa de correio de UM**, preencha as seguintes caixas:
    
      - **Endereço SIP ou número E.164**   Insira o endereço SIP ou número E.164 para o usuário. Essas opções só estarão disponíveis se o usuário que você habilitar para Unificação de Mensagens estiver atribuído a uma política de caixa de correio de UM vinculada a um URI SIP ou a um plano de discagem E.164. A opção de adicionar um endereço SIP ou número E.164 para um usuário não estará disponível se o usuário estiver associado a um plano de discagem de ramal de telefone. Quando você atribui o usuário a uma política de caixa de correio da UM vinculada a um plano de discagem E.164 ou SIP URI, você deve inserir também um número de ramal para o usuário. O número do ramal é usado quando os usuários acessam sua caixa de correio usando o Outlook Voice Access. A quantidade de dígitos configurada para esta caixa precisa ser igual à quantidade de dígitos configurada no plano de discagem URI SIP ou E.164.
    
      - **Número do ramal**   Digite o número do ramal do usuário que você está habilitando para UM.
        
        Você deve fornecer um número de ramal válido para o usuário, e esse número deve ter o número de dígitos especificado no plano de discagem. Você só pode digitar caracteres numéricos ou dígitos de 1 a 20. O número de ramal típico tem de 3 a 7 dígitos. O número de dígitos do ramal é definido no plano de discagem vinculado à política de caixa de correio de UM atribuída ao usuário.
    
      - Em **Configurações de PIN**, preencha o seguinte:
        
          - **Gerar PIN automaticamente**   Clique neste botão para gerar automaticamente um PIN para o usuário habilitado para UM a ser utilizado para acesso à caixa postal por meio do Outlook Voice Access. Essa é a configuração padrão. Quando você clicar nesse botão, um PIN será gerado automaticamente com base nas políticas de PIN configuradas na política de caixa de correio da UM atribuída ao usuário. Recomendamos o uso dessa configuração para ajudar a proteger o PIN do usuário. O PIN é enviado ao usuário na mensagem de boas-vindas que ele recebe após ter habilitado a UM. Por padrão, ele terá que alterar esse PIN quando entrar pela primeira vez em sua caixa de correio para verificar seu correio de voz.
        
          - **Digite um PIN**   Clique neste botão para manualmente especificar um PIN que o usuário utilizará para acessar o sistema de caixa postal. O PIN deve estar em conformidade com as configurações de política de PIN definidas na política de caixa de correio de UM associada a este usuário habilitado para UM. Por exemplo, se a política de caixa de correio da UM estiver configurada para aceitar somente PINs que contenham sete ou mais dígitos, o PIN digitado nessa caixa deverá ter pelo menos sete dígitos.
        
          - **Exigir que o usuário redefina seu PIN na primeira vez que entrar**   Marque esta caixa de seleção para forçar o usuário a redefinir seu PIN de caixa postal quando acessar o sistema de caixa postal a partir de um telefone usando o Outlook Voice Access pela primeira vez. Será solicitado que o usuário insira um PIN mais familiar a ele. É uma prática recomendada de segurança forçar usuários habilitados para UM a alterar seus PINs quando entram pela primeira vez para proteção contra acesso não autorizado a dados e Caixa de Entrada. Esta caixa de seleção é marcada por padrão.

6.  Na página **Habilitar caixa de correio de UM**, examine as configurações. Clique em **Concluir** para habilitar o usuário para a Unificação de Mensagens. Clique em **Voltar** para fazer alterações na configuração.

Para habilitar o usuário para a Unificação de Mensagens no Shell, execute o seguinte comando.

    Enable-UMMailbox -Identity tonysmith@contoso.com -UMMailboxPolicy MyUMMailboxPolicy -Extensions 51234 -PIN 5643892 -NotifyEmail administrator@contoso.com -PINExpired $true

Se necessário, pode configurar um usuário habilitado para UM usando o EAC:

1.  Na EAC, navegue até **Destinatários** \> **Caixas de correio**.

2.  Na visualização de lista, selecione a caixa de correio para a qual você quer mudar a política de caixa de correio da UM.

3.  No painel de detalhes, em **Telefone e Características de Voz** \> **Unificação de Mensagens**, clique em **Ver detalhes**.

4.  Na página **Caixa de Correio de UM**, clique em **Configurações de caixa de correio de UM** para exibir ou alterar as propriedades de UM para um usuário habilitado para UM existente:
    
      - **Status do PIN**   Esta caixa somente para exibição mostra o status da caixa de correio do usuário. Por padrão, quando um usuário está habilitado para UM, o status do PIN é apresentado como **Não bloqueado**. Porém, se o usuário especificar várias vezes um PIN incorreto do Outlook Voice Access, o status será apresentado como **Bloqueado**.
    
      - **Política de caixa de correio de UM**   Esta caixa mostra o nome da política de caixa de correio de UM associada ao usuário habilitado para UM. Você pode clicar em **Procurar** para localizar e especificar a política a ser associada a essa caixa de correio de UM.
    
      - **Ramal pessoal do operador**   Use esta caixa para especificar o número do ramal de operador para o usuário. Por padrão, o número do ramal não está configurado. O tamanho do número do ramal pode ser de 1 a 20 caracteres. Isso permite que as chamadas de entrada para o usuário habilitado para UM sejam encaminhadas ao número de ramal especificado nessa caixa.
        
        Você pode configurar outros tipos de números de ramal da recepção em planos de discagem e atendedores automáticos. Porém, esses ramais geralmente são destinados a recepcionistas ou operadores em toda a empresa. A configuração do ramal de telefonista pode ser usada quando um assistente administrativo ou assistente pessoal atender chamadas de entrada de um usuário específico.

5.  Na página **Caixa de Correio de UM**, em **Outras extensões**, você pode adicionar, alterar e exibir números de ramal para o usuário.
    
      - Para adicionar um número de ramal, clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar"). Na página **Adicionar outra extensão**, use **Procurar** para selecionar o plano de discagem de UM e digite o número do ramal na caixa **Número do ramal**.
    
      - Para remover um número de ramal, selecione o número que deseja remover e clique em **Remover**![ícone Remover](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "ícone Remover").

6.  Se fizer alterações, clique em **Salvar**.

Se necessário, pode configurar um usuário habilitado para UM executando o seguinte comando no Shell.

    Set-UMMailbox -Identity tony@contoso.com -CallAnsweringAudioCodec Wma -CallAnsweringRulesEnabled $false -FaxEnabled $false -UMSMSNotificationOption VoiceMail

## Etapa 13: Configurar os gateways de VoIP, PBXs IP e PBXs habilitados para SIP para enviarem todas as chamadas de entrada para os servidores de Acesso para Cliente do Exchange 2013

Quando os servidores de Acesso para Cliente e de Caixa de Correio do Exchange 2013 estiverem instalados, eles serão habilitados automaticamente, para que possam responder a chamadas de voz de entrada e de saída e rotear mensagens de caixa postal para os destinatários desejados. Quando você estiver instalando seus servidores de Acesso para Cliente e Caixa de Correio do Exchange 2013 e implantando a Unificação de Mensagens, não precisará vincular ou adicionar servidores de Acesso para Cliente ou Caixa de Correio do Exchange 2013 a planos de discagem de UM. Os servidores de Acesso para Cliente e Caixa de Correio do Exchange 2013 atendem a todas as chamadas de entrada e usam planos de discagem de UM para localizar usuários.

O servidor de Acesso para Cliente do Exchange 2013 é o ponto de entrada para quaisquer chamadas de entrada ou solicitações de SIP (Session Initiation Protocol) para Unificação de Mensagens. O serviço que lida com as solicitações de SIP num servidor de Acesso para Cliente do Exchange 2013 é o serviço de Roteador de Chamadas de UM e é executado em cada servidor de Acesso para Cliente do Exchange 2013 na sua organização.

Ao atualizar para a UM do Exchange 2013, já deve ter instalado e configurado um único ou vários gateways VoIP para conectar-se aos PBXs em sua rede de telefonia ou instalado e configurado os PBXs habilitados para SIP (Session Initiation Protocol) ou PBXs IP.

A última etapa neste processo de atualizar a UM do Exchange 2013 é configurar os gateways VoIP, PBXs IP ou PBXs habilitados para SIP para enviar as chamadas de entrada (incluindo chamadores que desejam deixar uma mensagem de caixa postal para o usuário, chamadas de usuários habilitados para UM que usam o Outlook Voice Access e chamadas de chamadores que discam para um atendedor automático de UM) para seus servidores de Acesso para Cliente do Exchange 2013. Todas as chamadas são recebidas primeiro pelo gateway VoIP, PBX IP ou PBX habilitado para SIP e será encaminhada para os servidores de Acesso para Cliente do Exchange 2013 na sua organização do Exchange 2013. Para obter mais informações, consulte os seguintes recursos:

  -  [Serviços de Unificação de mensagens](um-services-exchange-2013-help.md)

  -  [Notas de configuração para gateways VoIP com suporte, IP PBXs e PBXs](configuration-notes-for-supported-voip-gateways-ip-pbxs-and-pbxs-exchange-2013-help.md)

  -  [Supervisor de telefonia para o Exchange 2013](telephony-advisor-for-exchange-2013-exchange-2013-help.md)

## Etapa 14: Desabilitar o atendimento de chamadas num servidor de Unificação de Mensagens no Exchange 2007

Pode desabilitar o atendimento de chamadas desabilitando a UM num servidor de Unificação de Mensagens do Exchange 2007 ou removendo o servidor de UM de um plano de discagem. Ao desabilitar a UM, você impede que o servidor da Unificação de Mensagens atenda chamadas de entrada. Você pode optar por desconectar todas as chamadas imediatamente ou aguardar até que as chamadas existentes sejam processadas antes de desabilitar o servidor de Unificação de Mensagens. Você terá de desabilitar o atendimento de chamadas antes de remover o servidor do plano de discagem, para poder concluir o processamento das chamadas de entrada.

Para desabilitar a Unificação de Mensagens num servidor de UM do Exchange 2007 usando a Console de Gerenciamento do Exchange:

1.  Na árvore de console do EMC, navegue para **Servidor de Configuração** \> **Unificação de Mensagens**.

2.  No painel de resultados, selecione o servidor de Unificação de Mensagens a ser desabilitado.

3.  No painel de ação, clique em um dos seguintes:
    
    1.  Ao selecionar a opção **Desabilitar Imediatamente**, o servidor de Unificação de Mensagens desconecta todas as chamadas conectadas ao servidor de Unificação de Mensagens.
    
    2.  Ao selecionar a opção **Desabilitar depois de concluir chamadas**, o servidor de Unificação de Mensagens não aceitará novas chamadas e não será desabilitado até que todas as chamadas tenham sido processadas.

4.  Na caixa de diálogo de confirmação, clique em **Sim** para continuar.

Para desabilitar a Unificação de Mensagens num servidor de UM do Exchange 2007 usando o Shell, execute o seguinte comando.

    Disable-UMServer -Identity MyUMServer -Immediate $true


> [!TIP]
> Pode usar o cmdlet <STRONG>Disable-UMServer</STRONG> a partir de um servidor de UM do Exchange 2007 ou o cmdlet <STRONG>Disable-UMService</STRONG> a partir de um servidor de Caixa de Correio do Exchange 2013 para desativar o atendimento de chamadas.



## Etapa 15: Remover um servidor de Unificação de Mensagens do Exchange 2007 de um plano de discagem

Para processar chamadas, um servidor de Unificação de Mensagens do Exchange 2007 deve ser adicionado a pelo menos um plano de discagem da UM. Um servidor de UM pode ser adicionado a vários planos de discagem de UM. Você pode remover um servidor de UM do Exchange 2007 de um plano de discagem de UM. Quando você remove um servidor de UM de um plano de discagem, o servidor de UM não responde mais a chamadas nem processa chamadas de UM para usuários habilitados para UM.

Para remover um servidor de UM do Exchange 2007 de um plano de discagem usando a Console de Gerenciamento do Exchange:

1.  Na árvore de console do EMC, navegue para **Servidor de Configuração** \> **Unificação de Mensagens**.

2.  No painel de resultados, selecione o servidor de Unificação de Mensagens.

3.  No painel de ações, clique em **Propriedades**.

4.  Na guia **Configurações de UM**, na seção **Planos de Discagem Associados**, clique em **Remover**.

5.  Na caixa de diálogo de confirmação, clique em **Sim** para confirmar a exclusão do servidor de Unificação de Mensagens do Exchange 2007 do plano de discagem de UM.

6.  Clique em **OK** para fechar a janela de propriedades.

Para remover um servidor de UM do Exchange 2007 de um plano de discagem usando o Shell, execute o seguinte comando.

```
    $dp= Get-UMDialPlan "MySIPDialPlan"
```
```    
    $s=Get-UMServer -id MyUMServer
```
```
    $s.dialplans-=$dp.identity
```
```    
    Set-UMServer -id MyUMServer -dialplans:$s.dialplans
```

Neste exemplo, existem três planos de discagem URI do SIP: SipDP1, SipDP2 e SipDP3. Este exemplo remove o servidor de UM denominado `MyUMServer` do plano de discagem SipDP3.

    Set-UMServer -id MyUMServer -DialPlans SipDP1,SipDP2

Neste exemplo, existem dois planos de discagem URI do SIP: SipDP1 e SipDP2. Este exemplo remove o servidor de UM denominado `MyUMServer` do plano de discagem SipDP2.

    Set-UMServer -id MyUMServer -DialPlans SipDP1


> [!TIP]
> Pode usar o cmdlet <STRONG>Set-UMServer</STRONG> no Shell ou num servidor de Unificação de Mensagens do Exchange 2007 ou o cmdlet <STRONG>Set-UMService</STRONG> num servidor de Caixa de Correio do Exchange 2013 para remover um servidor de UM do Exchange 2007 de um ou vários planos de discagem. Por exemplo, para remover um servidor de UM de todos os planos de discagem, execute o seguinte comando: <CODE>Set-UMServer -identity MyUMServer -DialPlan $null</CODE>



## Como saber se funcionou?

Depois de você ter configurado a Unificação de Mensagens, verifique as seguintes opções para assegurar que está funcionado corretamente:

  - Um usuário que você habilitou para caixa postal pode entrar no Outlook Web App ou no Outlook e ver uma Mensagem de Boas-vindas para Unificação de Mensagens.

  - Os usuários de UM podem receber mensagens de voz.

  - Os usuários de UM podem ligar para um número do Outlook Voice Access e ouvir emails, itens de calendário e caixa postal.

  - A UM está roteando chamadas de fora de sua organização, e você pode fazer uma chamada.

