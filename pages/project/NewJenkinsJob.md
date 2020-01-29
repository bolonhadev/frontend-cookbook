# Construindo projetos com Jenkins

Mais automação, vejamos como configurar o Jenkins para 'buildá' projetos e 'deploiá-los'. Os passos pra isso são feitos no Jenkins, Gitlab & repository.

## Adicionar um Jenkinsfile no projeto

Pegue o conteúdo abaixo e coloque-o em um arquivo chamado `Jenkinsfile` localizado na raiz do seu repositório.

```
PipelineReact {
  slackChannel = '#ci-web'
  buildCommand = [
      development: 'npm install && npm test && npm run build:dev',
      master:      'npm install && npm test && npm run build:prod',
  ]
  buildDir = 'build'
  
  baseURL = 'template-react'
  bucketURL = [
      master:      "gs://${baseURL}.ack.ee/",
      development: "gs://${baseURL}-development.ack.ee/",
      stage:       "gs://${baseURL}-stage.ack.ee/"
  ]

  cloudProject = [
      development: 'infrastruktura-1307',
      master:      'ackee-production',
  ]

  nodeEnv = '-e NODE_PATH=./app:./config'
  nodeImage = 'node:6'
  excludeDir = '.git'
}
```

### Configuração

**PipelineReact** - É o nome da função no script que gerencia o fluxo de ações (pipeline)

### Altere esses campos para seu projeto

* **slackChannel** - Defina o nome do Slackpara enviar informações do resultado do build. Crie um nome de canal específico (tipo: `#ci-petshare`) ou deixe o default `#ci-web` - mas não é recomendado.  

* **buildCommand** - Adicione comandos que serão executados no momento do disparo da build de seu app.

* **baseURL**, **bucketURL** - Git branches que são necessárias para o build e endereços para fazer o deploy (master/dev/stage).

* **cloudProject** - Id do cloud do project onde a branch where é deploiada. Coisa de DevOps.

### Mudar isso em caso de necessidade

* **build** - Pasta que o fluxo de ações (pipeline) procurar por arquivos do projeto para buildar e usar para o deploy.

* **nodeImage** - Nome da imagem do docker que será usada para buildar o ambiente.

## Criar nova tarefa

1. Acesse o site do jenkins.

2. Clique em **Nové** canto superior esquerdo.  
![New Jenkins job](../../img/NewJenkinsJob/new_job.png) 

3. Preencha o primeiro campo com o nome do seu projeto.

4. Agora você pode optar por duas opções para criar uma tarefa
   * Criar multiplos ramos de fluxos de ação (pipelines) a partir do zero, só clicar **Multibranch pipeline**.  
   ![New multibranch pipeline](../../img/NewJenkinsJob/multibranch_pipeline.png)  

   * O jeito recomendado é clonando uma tarefa e mudando algumas configurações (você pode usar por exempl, a tarefa: `abibuch/abibuch-editor-frontend`). Basta rolar até o fim da página e preencher o campo "Copy from" com o nome da tarefa que você quer clonar. 
  ![Clone job](../../img/NewJenkinsJob/copy_pipeline_from.png)  

5. Após confirmar e chegar até a página de configuração, mude o campo  **Project repository**. Em seguida, configure as branchs que serão assistidas/escaneadas no campo **Behaviours -> Discover branches -> Include**, ex: `master development stage` (separados por espaços vazios).
![Configure job](../../img/NewJenkinsJob/job_configuration_new.png) 

6. Decidir se a `master` será buildada automaticamente ou manualmente, para build manual escolha a opção __Supress automatic SCM triggering__.  
![Supress automatic SCM triggering option](../../img/NewJenkinsJob/suppress_automatic_SCM_triggering.png)   

## Configurar webhook

Faça uma URL webhook substituindo **GROUP_NAME/REPOSITORY_NAME** com o seu Gitlab e o nome do seu repositório seguindo o padrão da URL.

Quando estiver em dúvidas sobre como deve parecer os webhooks - dê uma olhada em diversos projetos :) 

No repositório do gitlab vá até a página **Settings -> Integration** e preencha a URL com o endereço do hook no passo anterior, então clique Add webhook e marque o checkbox **Enable SSL verification**.
![Gitlab webhook setup](../../img/NewJenkinsJob/gitlab_webhook_setup.png)   




