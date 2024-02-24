# Aviso

### Detalhe

Repare que a saida pode variar conforme a versao do runtime.


Deixando claro: o texto abaixo partiu de um curso gratuito e não pode ser redistribuído. Se o tema interessar, procure o curso aberto da trilha de Java com Spring Boot. Se a plataforma sair do ar ou passar a cobrar, não depende de mim — mas o material de lá é muito bom e quem assina um plano alcança bem mais.


# Geral

O comando ensinado na aula não funcionou comigo. Então escrevi um pequeno script para facilitar a geração dos projetos. O comando que funcionou é o da documentação oficial do arquétipo rápido:

```
mvn archetype:generate "-DarchetypeGroupId=org.apache.maven.archetypes" "-DarchetypeArtifactId=maven-archetype-quickstart" "-DarchetypeVersion=1.5"
```

Guardei esse comando num repositório próprio, com uma cópia de trabalho na máquina. Alguns dos valores acima são apenas padrões definidos no script.

Também criei um atalho global, que nada mais é do que executar o script a partir da cópia de trabalho.


## Comandos da ferramenta

Na raiz do projeto gerado dá para rodar, por exemplo:

```
mvn clean
mvn compile
mvn test
mvn package
```

Se o projeto foi criado pelo atalho, entre na pasta gerada e execute os comandos de lá.


### Limpeza

Apaga os artefatos gerados e remove a pasta de saída (talvez faça mais coisas). Também existem as formas combinadas de limpar e empacotar, e limpar e instalar.


### Compilação

Gera os arquivos compilados a partir dos fontes. No projeto gerado existe apenas um fonte, e o arquivo compilado pode ser executado apontando para o pacote principal:

```
cd artifactId/target/classes/
java packageGroupId.App
```


### Testes

Como o manifesto do projeto gerado já declara a biblioteca de testes como dependência, o comando de teste executa os testes desse projeto. Em geral, esse comando serve para rodar testes.

Se aparecerem erros de versão, vale tentar a limpeza antes — entendendo que a pasta de saída será apagada.


### Empacotamento

Gera o arquivo empacotado da aplicação. O caminho do arquivo aparece na saída do comando.


### Instalação local

Rodando esse comando num projeto bem formatado, o artefato é instalado no repositório local e pode ser usado por outros projetos da máquina. Para isso, copie do manifesto do projeto de origem:

- identificador do grupo;
- identificador do artefato;
- versão.

Além disso, a aula mostrou uma linha extra de requisição no arquivo de módulo do projeto de destino — assunto de versões mais novas da linguagem. No meu projeto local esse arquivo nem existe, por causa da versão que uso.

Existem dois tipos de dependência:

- **direta**: declarada no manifesto;
- **transitiva**: dependência da sua dependência.

Para não engordar o pacote final por causa das dependências transitivas, a aula explicou os escopos. O padrão é o de compilação, mas existem outros cinco.

Tipos de escopo:

- compilação;
- execução;
- importação;
- sistema;
- fornecida pelo ambiente;
- teste.

Os detalhes estão na gravação da aula.


## Outros artefatos

O site oficial lista outros modelos de projeto; clicando em cada um aparece o comando correspondente.

A aula também indicou o repositório público de artefatos da comunidade.


## Manifesto do projeto

É o arquivo principal da ferramenta. O mínimo é bem curto:

![images/basic-pom-xml.png](images/manifesto-minimo.png)

O manifesto funciona por herança. O "pai" é o manifesto padrão vinculado a uma versão específica da ferramenta:

![images/pom-xml-inheritance.png](images/heranca-de-manifesto.png)

A aula indicou a página que documenta esse manifesto padrão. É possível sobrescrever configurações vindas dele no seu próprio manifesto.

Nesse manifesto padrão aparece o repositório central. Faz sentido: com outros gerenciadores de pacotes modernos não é preciso configurar onde buscar as bibliotecas, só instalar. Mesmo assim, a configuração pode ser trocada.

O endereço do repositório central é navegável: entrando nele você vê as pastas das bibliotecas publicadas.

A troca pode ser feita no próprio manifesto ou no arquivo de configuração global, no nó de espelhamento.

Existe também um repositório local, usado como cache, na pasta oculta do usuário.


## Incluindo dependências

O repositório público de artefatos fornece o trecho de marcação para colar no manifesto. Exemplo:

```
<!-- https://mvnrepository.com/artifact/org.junit.jupiter/junit-jupiter-api -->
<dependency>
    <groupId>org.junit.jupiter</groupId>
    <artifactId>junit-jupiter-api</artifactId>
    <version>5.11.0</version>
    <scope>test</scope>
</dependency>
```

Cole dentro do nó de dependências e rode a compilação para baixar.

**Observação:** existe também o comando de instalação, que o professor não comentou.


## Dependências opcionais

A imagem abaixo ilustra a marcação:

![optional dependencies image](images/dependencias-opcionais.png).


## Exclusões

Explicado em aula.

Como mostra a imagem, dá para declarar uma exclusão no projeto de destino para evitar, por exemplo, conflito de versões.

![exclusions](images/exclusoes.png)


## Ciclo de vida de build

São três ciclos principais. Os ciclos têm fases, e as fases têm metas.

Os três ciclos são:

- padrão, o principal, com 23 fases. As fases principais viram comandos:
    - validação;
    - compilação;
    - compilação de testes;
    - testes;
    - testes de integração;
    - empacotamento;
    - instalação;
    - publicação.
- limpeza, ciclo intermediário de limpeza do projeto, com 3 fases:
    - pré-limpeza;
    - limpeza;
    - pós-limpeza.
- publicação de site, com 4 fases:
    - pré-site;
    - site;
    - pós-site;
    - publicação do site.

# Resumo do curso

A apresentação usada no curso está salva no repositório.

- Vale conferir a versao instalada antes de seguir os passos abaixo.