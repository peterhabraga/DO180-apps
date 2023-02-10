# DO180-apps
DO180 Repository for Sample Applications

## Token_Curso_DO180-RedHat_GITHUB
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

## Novo Token DO180-RH
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

## Verificando as imagens
	podman images --format "table {{.ID}} {{.Repository}} {{.Tag}}"

## Acesse a área restrita do contêiner, O comando inicia um shell Bash, em execução como o usuário mysql, dentro do contêiner MySQL
	podman exec -it mysql-basic /bin/bash
	
## Verificando log da execução/inicialização do container 
	podman logs mysql-db

## Perguntas e Respostas
	# 1. Qual método é recomendado pela comunidade de contêiner para criar imagens de contêiner?
		
		R: Executar comandos em um Containerfile e enviar a imagem de contêiner gerada a um registro de imagens.
	
	# 2. Qual das opções a seguir é uma vantagem de usar o processo S2I autônomo como uma alternativa ao Containerfiles?

		R: Reutiliza imagens de construtor de alta qualidade.

	# 3. Quais são os cenários típicos para a criação de um Containerfile para compilar uma imagem filho a partir de uma imagem existente? (Escolha duas opções.)

		R: Adicionar bibliotecas de tempo de execução.
		   Adicionar bibliotecas internas para serem compartilhadas como uma camada única de imagem por várias imagens de contêiner para diferentes aplicativos.

## comando para exibir os metadados de imagem.
	podman inspect

## Perguntas e Respostas

	# 1. Quais afirmações estão corretas em relação à arquitetura do Kubernetes? (Escolha duas opções.)

		R: Os planos de controle do Kubernetes gerenciam o dimensionamento de pod.
		   Os planos de controle do Kubernetes agendam pods para nós específicos.	

	# 2. Quais duas afirmações estão corretas em relação aos tipos de recursos do Kubernetes e do OpenShift? (Escolha duas opções.)

		R: Um volume persistente define áreas de armazenamento disponíveis para pods por meio de uma solicitação de volume persistente.
		   Um controlador de replicação é responsável por monitorar e manter o número de pods para um aplicativo em particular.
	
	# 3. Quais as duas afirmações corretas em relação à rede do Kubernetes e do OpenShift? (Escolha duas opções.)

		R: Um serviço do Kubernetes pode fornecer um endereço IP para acessar um conjunto de pods.
		   Uma rota é responsável por fornecer nomes de DNS para acesso externo.

	# 4. Qual afirmação está correta em relação ao armazenamento persistente no OpenShift e no Kubernetes?

		R: Uma PVC representa uma área de armazenamento que pode ser solicitada por um pod para armazenar dados, mas é provisionada pelo administrador do cluster.

	# 5. Qual afirmação está correta em relação às adições do OpenShift ao Kubernetes?

		R: O OpenShift adiciona recursos para simplificar a configuração do Kubernetes para muitos casos de uso reais.


## OpenShift

	## Login no OC
		oc login -u ${USER} -p ${PASSWORD} ${MASTER_API}
	
	## Criando novo projeto
		oc new-project ${USER}-mysql-openshift

	## Criando novo aplicativo a partir do template mysql-persistent
		oc new-app \
		--template=mysql-persistent \
		-p MYSQL_USER=user1 -p MYSQL_PASSWORD=mypa55 -p MYSQL_DATABASE=testdb \
		-p MYSQL_ROOT_PASSWORD=r00tpa55 -p VOLUME_CAPACITY=10Gi

	## Execute o comando para visualizar o status do novo aplicativo
		oc status

	## Liste os pods neste projeto
		oc get pods

	## Use o comando para visualizar mais detalhes sobre o pod
		oc describe <Pod_NAME_Runnig>

	## Liste os serviços neste projeto
		oc get svc

	## Recupere os detalhes do serviço mysql usando o comando e observe se o tipo de serviço é ClusterIP por padrão
		oc describe service <NAME>

	## Liste as afirmações de armazenamento persistente neste projeto
		oc get pvc

	## Recupere os detalhes da PVC mysql usando o comando oc describe
		oc describe pvc/<NAME>

	## Monitorando o progresso da implantação
		oc get pods -w
	
	## monitore os logs de implantação
		oc logs -f <NAME>
		oc logs --all-containers -f <NAME>
		oc logs -f deployment/<NAME>  //logs do prcesso de Deploy
		oc logs -f bc/<NAME>          //logs do processo de Complicação

	## Exponha o serviço; isso cria uma rota
		oc expose svc/<NAME>

	## Verificando as rotas
		oc describe route

	## Deletando a rota 
		oc delete route/<NAME>

	## Analise o Deployment desse aplicativo
		oc describe deployment/<NAME>
	
	## Encontre a URL associada à nova rota
		oc get route -o jsonpath='{..spec.host}{"\n"}'
	
	## Processo de compilação Source-to-Image
		oc start-build <NAME>
		oc start-build bc/<NAME>

	## Use o comando para criar os recursos do aplicativo
		oc create -f <NAME>.yml