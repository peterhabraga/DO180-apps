# DO180-apps
DO180 Repository for Sample Applications

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
	podman ps -a

## Acesse a área restrita do contêiner, O comando inicia um shell Bash, em execução como o usuário mysql, dentro do contêiner MySQL
	podman exec -it mysql-basic /bin/bash
	
## Verificando log da execução/inicialização do container 
	podman logs mysql-db