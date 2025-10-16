Arquitetura AWS — Sistema Jurídico

Este projeto representa a arquitetura em nuvem de um sistema jurídico hospedado na AWS (Amazon Web Services).
O objetivo é permitir que advogados façam upload e consulta de documentos (contratos, evidências, briefings) de forma segura, escalável e automatizada.

Diagrama da Arquitetura - Componentes Principais:
Usuário (Advogado)
- Interage com o sistema por meio da interface hospedada no servidor (EC2).
- Envia e acessa documentos (ex: contrato.pdf, evidência.mp3, brief.docx).

EC2 — Servidor da Aplicação
- Responsável por hospedar a aplicação web principal.
- Gerencia autenticação, upload de arquivos e comunicação com os demais serviços da AWS.
- Os arquivos enviados são temporariamente armazenados no EBS e processados pela Lambda.

EBS — Elastic Block Store
- Volume de armazenamento associado à instância EC2.
- Utilizado para logs, caches temporários e dados intermediários do servidor.

RDS — Relational Database Service
- Banco de dados relacional (por exemplo, MySQL ou PostgreSQL).
- Armazena informações estruturadas da aplicação, como:
- Dados de usuários (advogados, clientes)
- Metadados dos arquivos
- Logs de upload e histórico de acessos.

Lambda Function
- Função sem servidor (serverless) responsável por automatizar tarefas como:
- Processamento de arquivos após upload;
- Validação e conversão de formatos;
- Gatilhos para salvar arquivos no S3.

S3 — Simple Storage Service
- Armazenamento de arquivos enviados (contratos, evidências, documentos).
- Seguro, durável e escalável.
- Organiza documentos por usuário, caso ou categoria.

Logs e Caches
- Diretório destinado a registros de execução e caches locais para otimizar performance.
- Pode ser futuramente integrado ao CloudWatch para monitoramento centralizado.

Fluxo de Funcionamento
- O advogado acessa o sistema (interface hospedada no EC2).
- O EC2 recebe o documento e o armazena temporariamente no EBS.
- A Lambda Function é acionada para processar e enviar o arquivo ao S3.
- Os metadados do documento são salvos no RDS.
- O advogado pode consultar os documentos armazenados no S3 através da aplicação.

Serviços AWS Utilizados:
- Serviço	Função
- EC2	Servidor da aplicação web
- EBS	Armazenamento temporário e logs
- Lambda	Processamento automatizado
- S3	Armazenamento de arquivos
- RDS	Banco de dados relacional
