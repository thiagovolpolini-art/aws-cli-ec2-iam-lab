# AWS CLI + EC2 + IAM Lab

Laboratório prático realizado durante minha formação na **Escola da Nuvem**, com foco em acesso a uma instância Amazon EC2 via SSH, instalação e configuração da AWS CLI e utilização do AWS IAM pela linha de comando.

## 📌 Objetivo

O objetivo deste laboratório foi praticar o uso da AWS CLI dentro de uma instância EC2, realizando configurações de acesso e consultas a recursos do IAM sem depender exclusivamente do Console de Gerenciamento da AWS.

## ☁️ Serviços e tecnologias utilizadas

- Amazon EC2
- AWS CLI
- AWS IAM
- AWS STS
- Linux
- SSH
- PuTTY
- JSON

## 🔐 Conexão com a instância EC2

Inicialmente, foi realizada a conexão com uma instância Amazon EC2 utilizando SSH através do PuTTY.

Após configurar o endereço IP público da instância e utilizar a chave privada fornecida pelo laboratório, foi possível acessar o terminal Linux.

Exemplo do acesso:

bash
ssh ec2-user@<PUBLIC_IP>

💻 Instalação da AWS CLI
O instalador da AWS CLI foi baixado diretamente pela linha de comando:
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"

Em seguida, o arquivo foi descompactado:
unzip -u awscliv2.zip

Depois foi realizada a instalação:
sudo ./aws/install

Para confirmar a instalação:
aws --version

⚙️ Configuração da AWS CLI
Após a instalação, a AWS CLI foi configurada utilizando:
aws configure

Durante a configuração foram informados:
- AWS Access Key ID
- AWS Secret Access Key
- Região padrão: us-west-2
- Formato de saída: json
Por segurança, nenhuma credencial utilizada durante o laboratório foi adicionada a este repositório.
✅ Validação das credenciais
Para verificar se a configuração estava funcionando corretamente, foi utilizado:
aws sts get-caller-identity

Esse comando retorna informações sobre a identidade autenticada na AWS, como:
{
  "UserId": "EXEMPLO",
  "Account": "XXXXXXXXXXXX",
  "Arn": "arn:aws:iam::XXXXXXXXXXXX:user/awsstudent"
}

👤 Consulta de usuários do IAM
Para listar os usuários existentes no AWS IAM, foi utilizado:
aws iam list-users

O retorno foi apresentado em formato JSON.
📜 Consulta das políticas IAM
Para listar as políticas gerenciadas localmente na conta AWS:
aws iam list-policies --scope Local

Durante o laboratório foi identificada a política:
lab_policy

Também foi possível identificar o ARN da política e sua versão padrão.
🔎 Consultando os detalhes da política
Para consultar os detalhes da política:
aws iam get-policy --policy-arn <POLICY_ARN>

Esse comando permite identificar informações como a versão padrão da política.
Exemplo:
DefaultVersionId: v1

🚀 Desafio final
Como desafio final, foi necessário utilizar apenas a AWS CLI para localizar a política lab_policy, consultar sua versão e salvar seu conteúdo em um arquivo JSON.
Primeiro, foi utilizada a versão da política:
aws iam get-policy-version \
  --policy-arn <POLICY_ARN> \
  --version-id v1

Depois, a saída do comando foi redirecionada para um arquivo:
aws iam get-policy-version \
  --policy-arn <POLICY_ARN> \
  --version-id v1 \
  > lab_policy.json

Para confirmar a criação do arquivo:
ls

E para visualizar o conteúdo:
cat lab_policy.json

O resultado foi a criação do arquivo:
lab_policy.json

contendo a representação JSON da política IAM.
🖼️ Resultado do laboratório


📚 Aprendizados
Durante este laboratório pratiquei:
- conexão SSH com uma instância Amazon EC2;
- utilização do PuTTY;
- instalação da AWS CLI em Linux;
- configuração da AWS CLI;
- autenticação utilizando credenciais IAM;
- utilização do AWS STS;
- consulta de usuários pelo IAM;
- consulta de políticas IAM pela AWS CLI;
- identificação de ARN e versões de políticas;
- manipulação de arquivos JSON;
- redirecionamento da saída de comandos para arquivos;
- utilização da AWS através da linha de comando.
🔒 Boas práticas
Credenciais como:
- AWS Access Key ID;
- AWS Secret Access Key;
- arquivos .pem;
- arquivos .ppk;
não devem ser publicadas em repositórios públicos.
Por esse motivo, todas as informações sensíveis utilizadas durante o laboratório foram omitidas deste projeto.
