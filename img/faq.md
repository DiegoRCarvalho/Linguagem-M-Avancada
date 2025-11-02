# FAQ – Como subir uma imagem e converter para Base64 no Power BI
Saiba como utilizar função personalizada para converter imagens em Base64 e utilizar em seus projetos sem a necessidade de hospedá-la em sites externos:

## ❓ 1. Como subir uma imagem no Power BI?

Você pode subir uma imagem como arquivo em Power BI da seguinte forma:

1. Abra o Power BI Desktop.
2. Vá em **"Página Inicial"** > **"Obter Dados"** > **"Pasta"** (ou "Arquivo").
3. Selecione a pasta onde está sua imagem (ou o arquivo específico).
4. Clique em **"Transformar Dados"** para abrir o Power Query.

## ❓ 2. Quais formatos de imagem são suportados?

Os formatos mais comuns são:

- .jpg
- .jpeg
- .png
- .bmp

O importante é que o arquivo seja lido como **binário**.

## ❓ 3. Como transformar a imagem em Base64 no Power Query?

Você vai usar a linguagem M do Power Query. Aqui está o passo a passo:

1. Depois de importar a imagem como binário, no Power Query, você verá uma coluna com o tipo binary.
2. Adicione uma nova coluna personalizada com a fórmula:

```M
mCopiarEditarBinary.ToText([Content], BinaryEncoding.Base64)
```
- **`[Content]`** é o nome da coluna que contém o arquivo binário da imagem.
- Isso vai gerar uma string **Base64**, que representa sua imagem.

## ❓ 4. Posso usar essa string Base64 para exibir a imagem no relatório?

- Sim! Mas você precisa embutir ela em um formato HTML.
- Crie uma coluna com o seguinte formato:

```M
mCopiarEditar"data:image/png;base64," & Binary.ToText([Content], BinaryEncoding.Base64)
```
- Ajuste o **image/png** de acordo com o tipo da imagem (**image/jpeg**, **image/bmp**, etc).

## ❓ 5. Como exibir a imagem no relatório do Power BI?

1. Crie uma **tabela** no relatório com a coluna que contém a string Base64.
2. Selecione essa coluna na visualização de tabela.
3. No painel de **"Modelagem"**, altere o tipo de dados da coluna para **"Imagem URL"**.