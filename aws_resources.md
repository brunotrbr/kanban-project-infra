## **Recursos**

| Categoria           | Recurso                           | Finalidade                                                                |
| ------------------- | --------------------------------- | ------------------------------------------------------------------------- |
| **Frontend**        | **S3 (Static Website Hosting)**   | Armazenar e servir os arquivos estáticos do app React (`npm run build`)   |
|                     | **Bucket Policy**                 | Permitir acesso público aos arquivos do frontend via URL da AWS           |
| **API**             | **API Gateway (REST)**            | Receber requisições do frontend e repassá-las para o backend no ECS       |
| **Backend**         | **ECS Cluster (EC2 + Spot)**      | Cluster de containers rodando em instâncias EC2 Spot para reduzir custos  |
|                     | **Auto Scaling Group**            | Escalar dinamicamente as instâncias Spot com base na demanda              |
|                     | **Launch Template/Config**        | Definir a imagem AMI, tipo de instância e dados de inicialização          |
|                     | **EC2 Spot Instances**            | Rodar containers da aplicação Django a custo reduzido                     |
|                     | **ECS Service + Task Definition** | Gerenciar e executar containers com a aplicação Python/Django             |
|                     | **Security Groups (ECS)**         | Permitir acesso da API Gateway ao ECS, e do ECS à internet se necessário  |
| **Banco de Dados**  | **DynamoDB**                      | Armazenar os dados dos cards do Kanban em formato NoSQL                   |
|                     | **IAM Role p/ ECS Task**          | Permitir que a aplicação acesse o DynamoDB                                |
| **Mensageria**      | **SQS (fila principal)**          | Armazenar mensagens para processar notificações após alterações no banco  |
|                     | **DLQ (Dead Letter Queue)**       | Armazenar mensagens que falharem após várias tentativas                   |
| **Notificação**     | **Lambda Function**               | Processar mensagens da SQS e chamar o SNS                                 |
|                     | **SNS (Email Notification)**      | Enviar e-mail de notificação para o usuário                               |
|                     | **IAM Role p/ Lambda**            | Permitir que a Lambda leia do SQS e publique no SNS                       |
| **Rede**            | **VPC**                           | Isolar os recursos e controlar o tráfego de rede interno/externo          |
|                     | **Subnets Públicas**              | Permitir acesso público controlado ao ECS e API Gateway                   |
|                     | **Subnets Privadas**              | Isolar componentes sensíveis como o banco e a Lambda                      |
|                     | **Internet Gateway**              | Permitir saída para a internet (caso necessário) via rotas públicas       |
|                     | **Route Tables**                  | Definir as rotas para tráfego entre subnets e internet                    |
| **Segurança**       | **IAM Roles/Policies (gerais)**   | Permissões mínimas para ECS, Lambda, DynamoDB, SQS, SNS, CloudWatch etc.  |
|                     | **Security Groups**               | Controlar acesso a instâncias ECS e funções Lambda                        |
| **Observabilidade** | **CloudWatch Logs**               | Capturar logs do ECS, Lambda, API Gateway                                 |
|                     | **CloudWatch Metrics**            | Monitorar métricas como invocações, erros e latência                      |
|                     | **CloudWatch Alarms**             | Disparar alertas com base em thresholds (ex: erros > 5)                   |
|                     | **AWS X-Ray**                     | Fazer tracing distribuído do fluxo API → ECS → SQS → Lambda → SNS         |
| **Orquestração**    | **Sceptre + CloudFormation**      | Gerenciar stacks, ambientes e dependências via infraestrutura como código |