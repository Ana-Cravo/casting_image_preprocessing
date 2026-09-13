# Casting Image Preprocessing

Pipeline de pré-processamento de imagens de peças de fundição,
desenvolvido em Python e OpenCV para preparar imagens para uma futura
etapa de Machine Learning.

> **Importante:** este projeto **não classifica** se uma peça tem
> defeito ou não. O objetivo é preparar as imagens para que,
> futuramente, uma equipe de Machine Learning possa utilizá-las para
> treinar um modelo preditivo.

## 1. Objetivo

O sistema recebe um lote de imagens de peças de fundição e aplica uma
sequência lógica de filtros e transformações para destacar
características estruturais e possíveis defeitos, como ranhuras.

Pipeline utilizado:

**Imagem → Grayscale → Gaussian Blur → Otsu → Canny → Resize 256×256 →
Closing 3×3 → Salvamento**

As imagens processadas são salvas de forma padronizada no diretório
`processed_images`.

## 2. Dataset

Foi utilizado o dataset público **Casting Product Image Data for Quality
Inspection**, fornecido no enunciado do mini-projeto.

O dataset contém imagens reais de peças de fundição com e sem defeitos.
O enunciado orienta copiar as imagens das categorias `ok_front` e
`def_front` para o diretório de entrada do projeto.

**Link do dataset:**\
https://drive.google.com/file/d/1K5gNxQ7RXA-nb4boNzPYQTJlRvJyYBD1/view?usp=sharing

### Importante sobre o GitHub

As imagens do dataset e as imagens processadas **não devem ser enviadas
para o GitHub**. O repositório deve conter somente código e
documentação.

O arquivo `.gitignore` do projeto ignora:

-   `raw_images/`
-   `processed_images/`
-   arquivos `.zip`
-   `.venv/`

## 3. Estrutura do projeto

A estrutura esperada é:

``` text
casting_image_preprocessing/
│
├── .gitignore
├── requirements.txt
├── preproc_casting.ipynb
├── README.md
│
├── raw_images/
│   └── imagens do dataset
│
└── processed_images/
    └── imagens geradas pelo pipeline
```

As pastas `raw_images/` e `processed_images/` são dados de entrada/saída
e ficam fora do versionamento.

------------------------------------------------------------------------

# 4. Como configurar o projeto do zero

As instruções abaixo contemplam **Windows, macOS e Linux**.

## 4.1 Pré-requisitos

Instale:

-   Python 3
-   Git
-   VS Code ou outro editor de sua preferência
-   Jupyter Notebook/JupyterLab (será instalado pelas dependências do
    projeto)

Verifique a instalação:

### Windows

``` powershell
python --version
git --version
```

Se `python` não funcionar, tente:

``` powershell
py --version
```

### macOS / Linux

``` bash
python3 --version
git --version
```

------------------------------------------------------------------------

# 5. Obter o projeto

## Opção A --- clonar o repositório com Git

``` bash
git clone git@github.com:Ana-Cravo/casting_image_preprocessing.git
cd casting_image_preprocessing
```

Se SSH não estiver configurado, também é possível utilizar a URL HTTPS
do repositório.

## Opção B --- baixar o projeto como ZIP

Baixe o repositório pelo GitHub e extraia a pasta
`casting_image_preprocessing` em um local de trabalho, por exemplo:

``` text
Documentos/
└── casting_image_preprocessing/
```

Depois abra essa pasta no VS Code.

------------------------------------------------------------------------

# 6. Criar as pastas do projeto

Dentro da pasta `casting_image_preprocessing`, crie:

``` text
raw_images/
processed_images/
```

### Windows PowerShell

``` powershell
New-Item -ItemType Directory raw_images
New-Item -ItemType Directory processed_images
```

### macOS / Linux

``` bash
mkdir -p raw_images processed_images
```

> Se as pastas já existirem, não é necessário criá-las novamente.

------------------------------------------------------------------------

# 7. Baixar e preparar o dataset

## 7.1 Baixar o ZIP

Abra o link do dataset fornecido no enunciado e faça o download do
arquivo ZIP.

Recomenda-se deixar o ZIP inicialmente na pasta **Downloads**, e não
dentro do repositório do projeto.

Exemplo:

``` text
Downloads/
└── dataset_casting.zip
```

## 7.2 Extrair o ZIP

Após baixar o arquivo ZIP do dataset, extraia o conteúdo fora do repositório, preferencialmente na pasta Downloads ou em uma pasta temporária.

Dentro do conteúdo extraído, localize a pasta casting_512x512. Nela estarão as pastas:
``` text
casting_512x512/
├── def_front/
└── ok_front/
``` 

A estrutura exata do arquivo extraído pode variar, portanto localize as
pastas `ok_front` e `def_front`.

## 7.3 Mover as pastas para raw_images

Para organizar o projeto, mova as pastas def_front e ok_front para dentro de raw_images.

Dentro da pasta extraída casting_512x512, localize:
``` text
casting_512x512/
├── def_front/
└── ok_front/
``` 
Mova as duas pastas (def_front e ok_front) para dentro da pasta raw_images do projeto.

Ao final, a estrutura deverá ficar:
``` text
raw_images/
├── def_front/
└── ok_front/
``` 
A pasta intermediária casting_512x512 não precisa permanecer dentro de raw_images e pode ser removida depois que as duas pastas forem movidas.

Windows: use Recortar (Ctrl + X) e Colar (Ctrl + V) pelo Explorador de Arquivos.

macOS: use Command + X e Command + V no Finder.

Linux: use Ctrl + X e Ctrl + V no gerenciador de arquivos.


### Importante

Não é necessário mover o ZIP para dentro do projeto.

Não é necessário colocar a pasta inteira do dataset dentro do projeto.

O que interessa para o pipeline são as imagens que serão utilizadas como
entrada, dentro de `raw_images/`.

------------------------------------------------------------------------

# 8. Criar o ambiente virtual

O ambiente virtual mantém as dependências do projeto isoladas das demais
instalações do computador.

## Windows

Abra o PowerShell dentro da pasta do projeto:

``` powershell
py -m venv .venv
```

Ative o ambiente:

``` powershell
.\.venv\Scripts\Activate.ps1
```

O terminal deverá mostrar algo semelhante a:

``` text
(.venv) PS C:\...\casting_image_preprocessing>
```

Se o comando `py` não estiver disponível, tente:

``` powershell
python -m venv .venv
```

## macOS

No Terminal, dentro da pasta do projeto:

``` bash
python3 -m venv .venv
```

Ative:

``` bash
source .venv/bin/activate
```

## Linux

No Terminal, dentro da pasta do projeto:

``` bash
python3 -m venv .venv
```

Ative:

``` bash
source .venv/bin/activate
```

Quando o ambiente estiver ativo, o terminal deverá mostrar algo como:

``` text
(.venv)
```

------------------------------------------------------------------------

# 9. Instalar as dependências

Com o ambiente virtual ativo:

``` bash
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
```

O projeto utiliza:

``` text
numpy==2.5.3
opencv-python==5.0.0.93
matplotlib==3.11.1
tqdm==4.70.1
jupyter==1.1.1
ipywidgets==8.1.9
```

------------------------------------------------------------------------

# 10. Abrir o notebook

Com o ambiente virtual ativo, execute:

``` bash
jupyter lab
```

ou:

``` bash
jupyter notebook
```

Abra:

``` text
preproc_casting.ipynb
```

No VS Code, também é possível abrir diretamente o arquivo `.ipynb`,
desde que a extensão Python/Jupyter esteja configurada.

------------------------------------------------------------------------

# 11. Executar o pipeline

No notebook, execute a célula que contém a definição da classe  **`CastingPreprocessor`**.

Essa célula precisa ser executada primeiro para que o Python carregue a classe na memória.

A seguir, crie a instância da classe:

``` python
processor = CastingPreprocessor()
```

Depois execute:

``` python
processor.pipeline(
    "raw_images",
    "processed_images"
)
```

O pipeline executará as etapas automaticamente.

------------------------------------------------------------------------

# 12. Etapas do processamento

## 12.1 Leitura em lote

O sistema percorre o diretório de entrada e localiza arquivos de imagem
com extensões:

-   `.jpg`
-   `.jpeg`
-   `.png`

As imagens são carregadas em lote.

## 12.2 Grayscale

As imagens coloridas são convertidas para escala de cinza utilizando
OpenCV.

## 12.3 Gaussian Blur

É aplicado Gaussian Blur com kernel `5×5` para reduzir ruídos antes das
etapas seguintes.

## 12.4 Thresholding de Otsu

O método de Otsu é utilizado para gerar uma imagem binária a partir das
imagens suavizadas.

## 12.5 Canny

A detecção de bordas Canny é aplicada sobre o resultado do Otsu para
destacar estruturas e contornos.

## 12.6 Resize

As imagens são redimensionadas para:

``` text
256 × 256 pixels
```

## 12.7 Closing morfológico

É aplicado fechamento morfológico (`MORPH_CLOSE`) com kernel retangular
`3×3`.

Essa etapa ajuda a conectar e preservar estruturas das bordas.

## 12.8 Salvamento

As imagens finais são salvas em:

``` text
processed_images/
```

com nomes padronizados, por exemplo:

``` text
processed_01.png
processed_02.png
processed_03.png
...
```

------------------------------------------------------------------------

# 13. Resultado da execução

O pipeline foi validado com o lote completo do dataset utilizado no
projeto.

Resultado da execução de validação:

-   **1.300 arquivos de imagem encontrados**
-   **1.300 imagens carregadas**
-   **1.300 imagens processadas**
-   **1.300 imagens salvas**
-   tempo aproximado: **7,91 segundos**

Também foi realizada uma comparação visual entre imagens originais e
processadas, incluindo exemplos de imagens `cast_def` e `cast_ok`.

------------------------------------------------------------------------

# 14. Organização do código

A implementação foi organizada na classe:

``` python
CastingPreprocessor
```

O método público:

``` python
pipeline()
```

coordena todas as etapas do processamento.

Os demais métodos foram organizados para separar responsabilidades,
como:

-   leitura das imagens;
-   conversão para grayscale;
-   redução de ruído;
-   thresholding;
-   detecção de bordas;
-   morfologia e resize;
-   salvamento.

Essa organização facilita a manutenção e futuras melhorias do pipeline.

------------------------------------------------------------------------

# 15. Versionamento com Git

O projeto foi desenvolvido utilizando Git.

Branches utilizadas:

  -----------------------------------------------------------------------
  Branch                              Objetivo
  ----------------------------------- -----------------------------------
  `main`                              Branch principal do projeto

  `development`                       Desenvolvimento e integração dos
                                      Sprints

  `feature/leitura-batch`             Desenvolvimento e validação da
                                      leitura das imagens em lote
  -----------------------------------------------------------------------

O desenvolvimento foi dividido em commits relacionados às etapas do
projeto, incluindo leitura em lote, pré-processamento, thresholding,
detecção de bordas, refinamento morfológico, organização em classe e
salvamento das imagens.

------------------------------------------------------------------------

# 16. Sprints

### Sprint 1 --- Configuração e Versionamento

-   criação do repositório Git;
-   branch `development`;
-   ambiente virtual;
-   download do dataset.

### Sprint 2 --- Estruturação de Dados e Leitura

-   criação de `raw_images/`;
-   criação de `processed_images/`;
-   leitura das imagens em lote.

### Sprint 3 --- Pré-processamento Base

-   Grayscale;
-   Gaussian Blur.

### Sprint 4 --- Segmentação e Destaque de Características

-   Thresholding de Otsu;
-   detecção de bordas Canny.

### Sprint 5 --- Refinamento Morfológico e Padronização

-   Closing morfológico;
-   Resize para `256×256`.

### Sprint 6 --- Salvamento e Documentação

-   salvamento das imagens processadas;
-   documentação;
-   apresentação do projeto.

------------------------------------------------------------------------

# 17. Observações sobre o repositório

As imagens originais e processadas não fazem parte do versionamento do
Git.

O repositório contém principalmente:

``` text
código
documentação
requirements.txt
.gitignore
notebook
```

Os dados utilizados no processamento permanecem localmente nas pastas:

``` text
raw_images/
processed_images/
```

Isso mantém o repositório leve e segue a orientação do projeto de enviar
ao GitHub apenas código e documentação.

------------------------------------------------------------------------

## Autora

**Ana Cravo**

Projeto desenvolvido como mini-projeto avaliativo do Módulo 2 ---
Machine Learning e Visão Computacional.
