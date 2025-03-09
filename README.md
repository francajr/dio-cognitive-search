# Projeto Azure Cognitive Search: Utilizando AI Search para indexação e consulta de Dados

## Azure Cognitive Search: Utilizando AI Search para indexação e consulta de Dados

### Objetivos
•	Criar recursos do Azure<br>
•	Extrair dados de uma fonte de dados<br>
•	Enriqueça os dados com habilidades de IA<br>
•	Use o indexador do Azure no portal do Azure<br>
•	Consulte seu índice de pesquisa<br>
•	Revise os resultados salvos em um Knowledge Store

### Recursos:
•	Um recurso do Azure AI Search, que gerenciará a indexação e a consulta.<br>
•	Um recurso de serviços de IA do Azure, que fornece serviços de IA para habilidades que sua solução de pesquisa pode usar para enriquecer os dados na fonte de dados com insights gerados por IA.<br>
•	Uma conta de armazenamento com contêineres de blobs, que armazenarão documentos brutos e outras coleções de tabelas, objetos ou arquivos.

### Primeiro:
1.	Entre no portal do Azure.
2.	Clique no botão + Criar um recurso, pesquise por Azure AI Search e crie um recurso do Azure AI Search com as seguintes configurações:<br>
o	Assinatura: sua assinatura do Azure.<br>
o	Grupo de recursos: selecione ou crie um grupo de recursos com um nome exclusivo.<br>
o	Nome do serviço: Um nome exclusivo.<br>
o	Localização: Escolha qualquer região disponível. Se estiver no leste dos EUA, use “East US 2”.<br>
o	Nível de preço: Básico<br>
3.	Selecione Revisar + criar e, depois de ver a resposta Validação bem-sucedida, selecione Criar.
4.	Após a conclusão da implantação, selecione Ir para o recurso. Na página de visão geral do Azure AI Search, você pode adicionar índices, importar dados e pesquisar índices criados.

### Segundo:
Criar um recurso de serviços de IA do Azure
Você precisará provisionar um recurso de serviços de IA do Azure que esteja no mesmo local que seu recurso de Pesquisa de IA do Azure. Sua solução de pesquisa usará esse recurso para enriquecer os dados no datastore com insights gerados por IA.
1.	Retorne à página inicial do portal do Azure. Clique no botão ＋Criar um recurso e pesquise por Azure AI services. Selecione criar um plano de serviços do Azure AI. Você será levado a uma página para criar um recurso de serviços do Azure AI. Configure-o com as seguintes configurações:<br>
o	Assinatura: sua assinatura do Azure.<br>
o	Grupo de recursos: o mesmo grupo de recursos que seu recurso do Azure AI Search.<br>
o	Região: o mesmo local do seu recurso do Azure AI Search.<br>
o	Nome: Um nome único.<br>
o	Nível de preço: Standard S0<br>
o	Ao marcar esta caixa, reconheço que li e compreendi todos os termos abaixo: Selecionado<br>
2.	Selecione Revisar + criar. Após ver a resposta Validação aprovada, selecione Criar.
3.	Aguarde a conclusão da implantação e visualize os detalhes da implantação.

### Terceiro:
Criar uma conta de armazenamento
1.	Retorne à página inicial do portal do Azure e selecione o botão + Criar um recurso.
2.	Pesquise por conta de armazenamento e crie um recurso de conta de armazenamento com as seguintes configurações:<br>
o	Assinatura: sua assinatura do Azure.<br>
o	Grupo de recursos: o mesmo grupo de recursos dos recursos do Azure AI Search e dos serviços do Azure AI.<br>
o	Nome da conta de armazenamento: Um nome exclusivo.<br>
o	Localização: Escolha qualquer local disponível.<br>
o	Desempenho: Padrão<br>
o	Redundância: Armazenamento redundante local (LRS)<br>
3.	Clique em Review e depois em Create. Aguarde a conclusão da implantação e vá para o recurso implantado.
4.	Na conta de Armazenamento do Azure que você criou, no painel de menu à esquerda, selecione Configuração (em Configurações).
5.	Altere a configuração de Permitir acesso anônimo do Blob para Habilitado e selecione Salvar.

### Quarto:
Carregar documentos para o armazenamento do Azure
1.	No painel de menu à esquerda, selecione Contêineres.
 ![containers](https://github.com/francajr/dio-cognitive-search/blob/main/images/containers.jpg)
2.	Selecione + Container. Um painel no seu lado direito abre.
3.	Insira as seguintes configurações e clique em Criar:<br>
o	Nome coffee-reviews<br>
o	Nível de acesso público: Container (acesso de leitura anônimo para containers e blobs)<br>
o	Avançado: sem alterações.<br>
4.	Em uma nova aba do navegador, baixe as avaliações de café compactadas de https://aka.ms/mslearn-coffee-reviewse extraia os arquivos para a pasta de avaliações
5.	No portal do Azure, selecione seu contêiner coffee-reviews. No contêiner, selecione Upload.
  ![upload](https://github.com/francajr/dio-cognitive-search/blob/main/images/upload.jpg)
6.	No painel Carregar blob, selecione Selecionar um arquivo.
7.	Na janela do Explorer, selecione todos os arquivos na pasta de avaliações, selecione Abrir e, em seguida, selecione Carregar.
  ![upload](https://github.com/francajr/dio-cognitive-search/blob/main/images/upload2.jpg)
8.	Após o upload ser concluído, você pode fechar o painel Upload blob. Seus documentos agora estão no seu contêiner de armazenamento coffee-reviews.

### Quinto:
Indexar os documentos
Depois de ter os documentos no armazenamento, você pode usar o Azure AI Search para extrair insights dos documentos. O portal do Azure fornece um assistente Importar dados. Com esse assistente, você pode criar automaticamente um índice e um indexador para fontes de dados com suporte. Você usará o assistente para criar um índice e importar seus documentos de pesquisa do armazenamento para o índice do Azure AI Search.
1.	No portal do Azure, navegue até seu recurso do Azure AI Search. Na página Visão geral, selecione Importar dados.
  ![import](https://github.com/francajr/dio-cognitive-search/blob/main/images/import.jpg)
2.	Na página Conectar aos seus dados, na lista Fonte de dados, selecione Azure Blob Storage. Preencha os detalhes do armazenamento de dados com os seguintes valores:<br>
o	Fonte de dados: Armazenamento de Blobs do Azure<br>
o	Nome da fonte de dados: coffee-customer-data<br>
o	Dados a extrair: Conteúdo e metadados<br>
o	Modo de análise: Padrão<br>
o	String de conexão: Selecione Choose an existing connection. Selecione sua conta de armazenamento, selecione o contêiner coffee-reviews e clique em Select.<br>
o	Autenticação de identidade gerenciada: Nenhuma<br>
o	Nome do contêiner: esta configuração é preenchida automaticamente depois que você escolhe uma conexão existente.<br>
o	Pasta Blob: deixe em branco.<br>
o	Descrição : Avaliações das cafeterias Fourth Coffee.<br>
3.	Selecione Avançar: Adicionar habilidades cognitivas (opcional).
4.	Na seção Anexar serviços de IA, selecione seu recurso de serviços de IA do Azure.
5.	Na seção Adicionar enriquecimentos:<br>
o	Altere o nome do Skillset para coffee-skillset.<br>
o	Marque a caixa de seleção Habilitar OCR e mesclar todo o texto no campo merged_content.<br>
o	Certifique-se de que o campo Dados de origem esteja definido como merged_content.<br>
o	Altere o nível de granularidade de enriquecimento para Páginas (blocos de 5000 caracteres).<br>
o	Não selecione Habilitar enriquecimento incremental<br>
o	Selecione os seguintes campos enriquecidos:<br>
  ![tabela](https://github.com/francajr/dio-cognitive-search/blob/main/images/tabela.jpg)
6.	Em Salvar enriquecimentos em um armazenamento de conhecimento , selecione:<br>
o	Projeções de imagem<br>
o	Documentos<br>
o	Páginas<br>
o	Frases-chave<br>
o	Entidades<br>
o	Detalhes da imagem<br>
o	Referências de imagem<br>  
  ![knowledge](https://github.com/francajr/dio-cognitive-search/blob/main/images/knowledge.jpg)
7.	Selecione Choose an existing connection (Escolha uma conexão existente). Escolha a conta de armazenamento que você criou anteriormente.
``
o	Clique em + Contêiner para criar um novo contêiner chamado knowledge-store com o nível de privacidade definido como Privado e selecione Criar.
``
``
o	Selecione o contêiner de armazenamento de conhecimento e clique em Selecionar na parte inferior da tela.
``
9.	Selecione Azure blob projections: Document. Uma configuração para Container name com o contêiner knowledge-store preenchido automaticamente é exibida. Não altere o nome do contêiner.
10.	Selecione Próximo: Personalizar índice de destino. Altere o nome do índice para coffee-index.
11.	Certifique-se de que a Chave esteja definida como metadata_storage_path. Deixe o nome do Suggester em branco e o modo Search preenchido automaticamente.
12.	Revise as configurações padrão dos campos de índice. Selecione filtrável para todos os campos que já estão selecionados por padrão. Os nomes de campo que precisam ser marcados como filtráveis incluem: content, locations, keyphrases, sentiment, merged_content, text, layoutText, imageTags, imageCaption.
  ![import2](https://github.com/francajr/dio-cognitive-search/blob/main/images/import2.jpg)
13.	Selecione Avançar: Criar um indexador.
14.	Altere o nome do indexador para coffee-indexer.
15.	Deixe a programação definida como Uma vez.
16.	Expanda as opções Avançadas. Certifique-se de que a opção Base-64 Encode Keys esteja selecionada, pois as chaves de codificação podem tornar o índice mais eficiente.
17.	Selecione Enviar para criar a fonte de dados, conjunto de habilidades, índice e indexador. O indexador é executado automaticamente e executa o pipeline de indexação, que:<br>
o	Extrai os campos de metadados do documento e o conteúdo da fonte de dados.<br>
o	Executa o conjunto de habilidades cognitivas para gerar campos mais enriquecidos.<br>
o	Mapeia os campos extraídos para o índice.<br>
18.	Retorne à sua página de recursos do Azure AI Search. No painel esquerdo, em Search Management, selecione Indexers. Selecione o coffee-indexer recém-criado. Aguarde um minuto e selecione ↻ Refresh até que o Status indique sucesso.
19.	Selecione o nome do indexador para ver mais detalhes.
  ![indexer](https://github.com/francajr/dio-cognitive-search/blob/main/images/indexer.jpg)


### Sexto:
Consultar o índice
Use o Search explorer para escrever e testar consultas. O Search explorer é uma ferramenta incorporada ao portal do Azure que oferece uma maneira fácil de validar a qualidade do seu índice de pesquisa. Você pode usar o Search explorer para escrever consultas e revisar resultados em JSON.
1.	Na página Visão geral do serviço de pesquisa, selecione Explorador de pesquisa na parte superior da tela.
  ![search](https://github.com/francajr/dio-cognitive-search/blob/main/images/search.jpg)
2.	Observe como o índice selecionado é o coffee-index que você criou. Abaixo do índice selecionado, altere a visualização para JSON view.
  ![json](https://github.com/francajr/dio-cognitive-search/blob/main/images/json.jpg)
No campo do editor de consulta JSON, copie e cole:<br>
códigoCópia<br>
``
{
    "search": "*",
    "count": true
}
``
<br>   
1.	Selecione Search. A consulta de pesquisa retorna todos os documentos no índice de pesquisa, incluindo uma contagem de todos os documentos no campo @odata.count. O índice de pesquisa deve retornar um documento JSON contendo os resultados da sua pesquisa.
2.	Agora vamos filtrar por localização. No campo JSON query editor, copie e cole:<br>
códigoCópia<br>
``
{
 "search": "locations:'Chicago'",
 "count": true
}
``
<br>
3.	Selecione Search. A consulta pesquisa todos os documentos no índice e filtra por avaliações com um local em Chicago. Você deve ver 3no @odata.countcampo.
4.	Agora vamos filtrar por sentimento. No campo JSON query editor, copie e cole:<br>
códigoCópia<br>
``
{
 "search": "sentiment:'negative'",
 "count": true
}
``
<br>
5.	Selecione Search. A consulta pesquisa todos os documentos no índice e filtra por avaliações com um sentimento negativo. Você deve ver 1no @odata.countcampo.
6.	Um dos problemas que podemos querer resolver é por que pode haver certas avaliações. Vamos dar uma olhada nas frases-chave associadas à avaliação negativa. O que você acha que pode ser a causa da avaliação?

### Sétimo:
Revise o repositório de conhecimento
Vamos ver o poder do armazenamento de conhecimento em ação. Quando você executou o assistente Import data, você também criou um armazenamento de conhecimento. Dentro do armazenamento de conhecimento, você encontrará os dados enriquecidos extraídos por habilidades de IA persistem na forma de projeções e tabelas.
1.	No portal do Azure, volte para sua conta de armazenamento do Azure.
2.	No painel de menu à esquerda, selecione Containers. Selecione o contêiner knowledge-store.
  ![knowledge](https://github.com/francajr/dio-cognitive-search/blob/main/images/knowledge2.jpg)
3.	Você verá uma lista de pastas. Há uma pasta para todos os metadados de cada documento de revisão. Selecione qualquer uma das pastas. Dentro da pasta, clique no arquivo objectprojection.json .
  ![object](https://github.com/francajr/dio-cognitive-search/blob/main/images/object.jpg)
4.	Selecione Editar para ver o JSON produzido para um dos documentos do seu armazenamento de dados do Azure.
  ![edit](https://github.com/francajr/dio-cognitive-search/blob/main/images/edit.jpg)
5.	Selecione o breadcrumb do blob de armazenamento no canto superior esquerdo da tela para retornar aos Contêineres da conta de armazenamento.
  ![edit](https://github.com/francajr/dio-cognitive-search/blob/main/images/edit2.jpg)
6.	Em Containers, selecione o container coffee-skillset-image-projection . Selecione qualquer um dos itens.
  ![items](https://github.com/francajr/dio-cognitive-search/blob/main/images/items.jpg)
7.	Selecione qualquer um dos arquivos .jpg. Selecione Editar para ver a imagem armazenada do documento. Observe como todas as imagens dos documentos são armazenadas dessa maneira.
  ![editjpg](https://github.com/francajr/dio-cognitive-search/blob/main/images/editjpg.jpg)
8.	Selecione o breadcrumb do blob de armazenamento no canto superior esquerdo da tela para retornar aos Contêineres da conta de armazenamento.
9.	Selecione Storage browser no painel esquerdo e selecione Tables. Há uma tabela para cada entidade no índice. Selecione a tabela coffeeSkillsetKeyPhrases .

Veja as frases-chave que o repositório de conhecimento conseguiu capturar do conteúdo nas avaliações. Muitos dos campos são chaves, então você pode vincular as tabelas como um banco de dados relacional. O último campo mostra as frases-chave que foram extraídas pelo conjunto de habilidades.
