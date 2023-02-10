# DO180-apps
DO180 Repository for Sample Applications

## configurações globais
	git config --global user.name "Andre Baltieri"
	git config --global user.email "meuemail@github.com"

## Token_Curso_DO180-RedHat_GITHUB
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

## https://quay.io/
	USER: peterhabraga
	PASS: quayAsdf123$

## LAB-CONFIGURE
	API Endpoint: https://api.na410.prod.nextcle.com:6443
	Username: vvksoo
	Password: cc66dcf85137451fb267

## REGISTRY.REDHAT.IO
	Username: peterhabraga
	Password: Asdf123$

## Baixando e executando container de Banco de Dados
	podman run --name mysql-basic -e MYSQL_USER=user1 -e MYSQL_PASSWORD=mypa55 -e MYSQL_DATABASE=items -e MYSQL_ROOT_PASSWORD=r00tpa55 -d registry.redhat.io/rhel8/mysql-80:1

## Verificando se o Container foi iniciado sem erros (usando o podman)
	podman ps --format "{{.ID}} {{.Image}} {{.Names}}"
	podman ps --format="{{.ID}} {{.Names}} {{.Ports}}"
	podman ps -a

## Acesse a área restrita do contêiner, O comando inicia um shell Bash, em execução como o usuário mysql, dentro do contêiner MySQL
	podman exec -it mysql-basic /bin/bash
	
## Verificando log da execução/inicialização do container 
	podman logs mysql-db

## 1. Quais comandos exibem imagens mysql disponíveis para download em registry.redhat.io?
	podman search registry.redhat.io/mysql
	podman search mysql

## 2. Qual comando é usado para listar todas as tags de imagem disponíveis para a imagem de contêiner httpd?
	podman search --list-tags httpd

## 3. Quais os dois comandos que extraem a imagem httpd com o marcador 2.4? (Escolha duas opções.)
	podman pull httpd:2.4
	podman pull registry.redhat.io/httpd:2.4

## 4. Ao executar os comandos a seguir, quais imagens de contêiner serão baixadas?
	[user@host ~]$ podman pull registry.redhat.io/httpd:2.4
	[user@host ~]$ podman pull quay.io/mysql:8.0

		registry.redhat.io/httpd:2.4, nenhuma imagem será baixada para o mysql.

## Use o comando podman diff para examinar as diferenças no contêiner entre a imagem e a nova camada criada pelo contêiner.
	podman diff official-httpd

## Pare o contêiner official-httpd.
	podman stop official-httpd

## Liste as imagens de contêiner disponíveis.
	podman images