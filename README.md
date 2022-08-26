# Como configurar containers e micro serviços

## Relação de Docker, Micro serviços e container

Docker - tecnologia utilizada para criação de containers
Container - É como se fosse uma mini máquina virtual. Porém, nela só existe uma aplicação (software) rodando. Exemplo: 1 container com Mysql, 1 container com Apache
Micro serviços - São as instâncias dos containers de aplicação

# Instalação
## Exemplo com a distribuição Linux Fedora
dnf install docker

### Baixar uma imagem de uma aplicação
docker pull mysql

Será baixada a última versão do mysql. Para outras versões, utilizamos "docker pull mysql:15.0"

# Utilizando AWS (máquinas virtuais da Amazon)

Digamos que temos 2 máquinas virtuais no AWS. Cada máquina é um sistema operacional independente com cpu, rede, memória, etc.
E essas máquinas, estão na mesma rede

## Cenário de uso dos containers
Máquina ECS-1 temos rodando o mysql "docker run --name container-mysql -e MYSQL_ROOT_PASSWORD=senha-mysql -d mysql/mysql-server"
Máquina ECS-2 temos rodando o apache "docker run --name container-apache -d apache/var/html/www"

Nesse cenário podemos montar cada micro serviço em cada máquina, e vice-versa

### E que tal rodarmos isso com redundância?

Sim.. isso é possível.
Podemos configurar o compartilhamento de volumes, que seriam basicamente diretórios

### E que tal balancear a carga quando uma máquina estiver muito ocupada?
Nesse caso, configuramos o Docker Swarm. Que é o cluster que fará o balanceamento das requisições entre os containers
Cada máquina ECS terá um container Mysql e um container Apache, devidamente configurados, compartilhando volumes e dados, e assim, o Swarm fará o balanceamento
