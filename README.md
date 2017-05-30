# Sobre Dockerfiles
O Docker pode criar imagens automaticamente lendo as instruções de um Dockerfile. Um Dockerfile é um documento de texto que contém todos os comandos que um usuário pode chamar na linha de comando para montar uma imagem. O uso de usuários de compilação docker pode criar uma compilação automatizada que executa várias instruções de linha de comando em sucessão.

# Opções Utilizadas
FROM: Informa a partir de qual imagem será gerada a nova imagem, lembrando que em poucos casos (Veremos em posts futuros), uma imagem será gerada se um imagem base;
MAINTAINER: Campo opcional, que informa o nome do mantenedor da nova imagem;
RUN: Especifica que o argumento seguinte será executado, ou seja, realiza a execução de um comando;
CMD: Define um comando a ser executado quando um container baseado nessa imagem for iniciado, esse parâmetro pode ser sobrescrito caso o container seja iniciado utilizando alguma informação de comando, como: docker run -d imagem comando, neste caso o CMD da imagem será sobrescrito pelo comando informado;
LABEL: Adiciona metadados a uma imagem, informações adicionais que servirão para identificar versão, tipo de licença, ou host, lembrando que a cada nova instrução LABEL é criada uma nova layer, o Docker recomenda que você não use muitas LABEL. É possível realizar filtragens posteriormente utilizando essas LABEL.
EXPOSE: Expõem uma ou mais portas, isso quer dizer que o container quando iniciado poderá ser acessível através dessas portas;
ENV: Instrução que cria e atribui um valor para uma variável dentro da imagem, isso é útil para realizar a instalação de alguma aplicação ou configurar um ambiente inteiro.
ADD: Adiciona arquivos locais  ou que estejam em uma url, para dentro da imagem.
COPY: Copia arquivos ou diretórios locais para dentro da imagem.
ENTRYPOINT: Informa qual comando será executado quando um container for iniciado utilizando esta imagem, diferentemente do CMD, o ENTRYPOINT não é sobrescrito, isso quer dizer que este comando será sempre executado.
VOLUME: Mapeia um diretório do host para ser acessível pelo container;
USER: Define com qual usuário serão executadas as instruções durante a geração da imagem;
WORKDIR: Define qual será o diretório de trabalho (lugar onde serão copiados os arquivos, e criadas novas pastas);
ONBUILD: Define algumas instruções que podem ser realizadas quando alguma determinada ação for executada, é basicamente como uma trigger.

# Exemplo de um arquivo Dockerfile Basico. 
FROM debian
MAINTAINER Fabio Coelho <fabiocruzcoelho@gmail.com>
RUN apt-get update
RUN apt-get install -y nginx
ENTRYPOINT ["/usr/sbin/nginx"]
EXPOSE 80
