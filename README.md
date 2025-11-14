Projeto Final: App "Caderneta de Fiado Digital"

Projeto de Desenvolvimento de Aplicativos Móveis com Kotlin e Android Studio.

Este projeto é uma solução móvel completa para substituir as cadernetas de "fiado" tradicionais usadas por pequenos comerciantes. O aplicativo permite o gerenciamento de clientes, dívidas e pagamentos com uma estratégia "Offline-First" (funcionando sem internet) e realiza o backup automático na nuvem (Firebase).

Principais Funcionalidades (Requisitos)
O aplicativo implementa todas as funcionalidades centrais de um sistema de controle de fiado:

RF01: Autenticação de Usuário (Firebase Auth)

O comerciante pode criar uma conta e fazer login usando e-mail e senha.

O app inclui uma Splash Screen que verifica se o usuário já está logado e o direciona para a tela correta (Login ou Lista de Clientes).

RF02: Gestão de Clientes (CRUD Local)

O comerciante pode cadastrar, listar e excluir clientes no dispositivo.

RF03 e RF04: Gestão de Transações (CRUD Local)

Na tela de detalhes de um cliente, o comerciante pode lançar novas dívidas (débitos) e registrar pagamentos (créditos) através de um formulário dedicado.

RF05: Extrato e Saldo Devedor

O app exibe um extrato cronológico (histórico) para cada cliente.

O saldo devedor é calculado e exibido em tempo real (Saldo = Dívidas - Pagamentos).

RF06: Dashboard (Lista de Clientes)

A tela principal (ClientesScreen) exibe a lista completa de clientes cadastrados localmente.

RF07: Backup na Nuvem (Firebase Firestore)

Todas as operações de criação ou exclusão de clientes e transações são salvas primeiro no banco local (Room) e, em seguida, sincronizadas automaticamente com o Firebase Firestore.

Os dados são armazenados de forma segura na nuvem, aninhados sob o ID do usuário (/usuarios/{userId}/clientes/...), garantindo que apenas o usuário logado possa ver seus próprios dados.

Instruções para Execução
Para compilar e executar este projeto, o avaliador (professor) precisará configurar o backend no Firebase, pois o arquivo google-services.json (que contém as chaves da API) não é incluído no controle de versão por razões de segurança.

Pré-requisitos

Android Studio (Versão Hedgehog ou mais recente)

Emulador ou dispositivo Android (API 24+)

Passo a Passo da Configuração

Crie um Projeto no Firebase:
Acesse o Console do Firebase.

Crie um novo projeto.

Adicione o App Android ao Projeto Firebase:
No painel do projeto, clique no ícone do Android (🤖).

No campo "Nome do pacote Android", insira exatamente: com.example.myapplication

Clique em "Registrar app".

Baixe o Arquivo de Configuração:
Faça o download do arquivo google-services.json gerado pelo Firebase.

Mova o Arquivo para a Pasta app/:
No Android Studio (na visualização "Project"), arraste e solte o arquivo google-services.json que você baixou para dentro da pasta MyApplication4/app/.

Ative os Serviços do Firebase:
No Console do Firebase, vá para a seção Authentication (no menu "Build"):

Clique em "Sign-in method" (Método de login).

Ative o provedor "E-mail/senha".

Vá para a seção Firestore Database (no menu "Build"):

Clique em "Criar banco de dados".

Inicie em Modo de Teste (permite leitura/escrita pelos próximos 30 dias).

Escolha uma localização de servidor (ex: southamerica-east1 ou us-central).

Compile e Execute:
Abra o projeto no Android Studio.

O Gradle fará o "Sync" automaticamente.

Clique em "Run 'app'" (o botão Play ▶️).

O aplicativo será instalado e abrirá na Tela de Login, pronto para uso.

Arquitetura e Tecnologias
O projeto foi construído seguindo as diretrizes modernas de desenvolvimento Android.

Arquitetura: MVVM (Model-View-ViewModel).

Estratégia: Offline-First, usando o Room como Fonte Única da Verdade (SSOT) e o Firestore como backup.

UI (View): 100% Jetpack Compose (Material 3).

Navegação (View): Navigation Compose (controlado por um NavHost na MainActivity).

Reatividade (ViewModel): Kotlin Coroutines (viewModelScope) e Flow / StateFlow para expor o estado da UI.

Banco de Dados Local (Model): Room (com 2 entidades: Cliente e Transacao).

Backend (Model): Firebase Authentication (Login) e Firebase Firestore (Banco de Dados na Nuvem).

Injeção de Dependência: Hilt (Dagger) (para injetar ViewModels, Repositórios e DAOs).

Processamento de Anotações: KSP (em vez do KAPT).

Detalhamento das Responsabilidades Individuais
Nome do Integrante: Victor Paschoal Paula Oliva Nome do Integrante: Kauan de Jesus Sena

Responsabilidades:

Definição da arquitetura do projeto (MVVM, Offline-First). Victor Paschoal Paula Oliva

Configuração do ambiente de build (Gradle, KSP, Hilt, Firebase). Victor Paschoal Paula Oliva

Implementação da camada de banco de dados local (Room, Entidades, DAOs). Victor Paschoal Paula Oliva

Desenvolvimento do ClienteRepository (lógica de negócios e sincronização). Victor Paschoal Paula Oliva

Implementação de todas as camadas de ViewModel (Login, Clientes, Detalhes). Victor Paschoal Paula Oliva

Criação de todas as telas (Views) com Jetpack Compose (Login, Clientes, Detalhes). Victor Paschoal Paula Oliva

Configuração da navegação (Navigation Compose) e da Splash Screen. Kauan de Jesus Sena

Integração com o Firebase (Auth e Firestore). Kauan de Jesus Sena

Depuração e correção de bugs de compilação (KSP/Hilt) e de execução (Room/Navegação). Kauan de Jesus Sena
