<h1 align='center'>
    <p>Prova Visão Computacional</p>
</h1>

## Desenvolvedor
<table align='center'>
  <tr>
    <td align="center">
        <img style="border-radius: 50%;" src="https://avatars.githubusercontent.com/u/60533993?v=4" width="100px;" alt=""/><br /><sub><b><a href="https://github.com/felipefracop">Felipe Pinheiro</a></b></sub></a><br />28839111</td>
  </table>

## **1. Descrição do Problema**

O objetivo do projeto é implementar um pipeline basico de visão computacional que seja capaz de classificar imagens, no projeto feito esta sendo utilizado imagens de cãos e gatos para o predict, porem a base para o treinamento esta sendo o dataset CIFAR-10 que ja possui como classes cachorros e gatos. 

Também é utilizada técnicas de pré-processamento como um exercicio separado, nas mesmas imagens usadas para a predição, aplicando blur, redimencionamento e uma equalização. Portanto enunciado proposto pelo professor inclui as seguintes etapas: tratamento de imagens, separação de imagens para treino e para testes, aplicação de uma rede neural (estou utilizando a CNN vista em aula) para treinamento e logo depois uma avaliação da acurácia além de outras métricas de avaliação.

---

## **2. Justificativa das Técnicas Utilizadas**

Foram selecionadas as técnicas de acordo com os conteúdos abordados em aula e com experiências que tive nos projetos de Visão Computacional.

* **Redimensionamento (128x128 para o pré-processamento e 32x32 para entrada da CNN)**: O redimensionamento das imagens garante padronização para assim facilitar o processamento e garantir com que todas as operações futuras saiam como o esperado; depois, reduzo a 32×32 para atender à entrada da rede no padrão CIFAR-10.

* **Filtro Gaussiano**: Remove ruídos sutis antes da equalização, deixando os contornos mais nítidos.

* **Escala de cinza + equalização de histograma**: A conversão para escala de cinza é necessária para aplicar a equalização, realçando contrastes e pode evidenciar padrões importantes.

* **CNN Simples (Convolutional Neural Network)**: Foi montado uma rede com três camadas convolucionais, pooling, flatten e densas. É o mesmo esquema que praticamos em sala e dá conta de um problema binário como este.

* **Divisão treino/teste (80/20)**: Garante que o modelo seja testado em imagens que ele nunca viu, evitando resultados ilusoriamente altos.

Usei OpenCV para as transformações, TensorFlow/Keras para o treinamento e Scikit-learn para gerar o relatório de métricas (precisão, recall, F1-score).

---

## **3. Etapas Realizadas**

1. **Organização das imagens externas**:

   * Separei seis fotos (três de gatos, três de cachorros) na pasta /content/imagens/.

2. **Pré-processamento**:

   * Redimensionamento para 128×128 px
   * Aplicado o filtro Gaussiano para remoção de ruídos (blur).
   * Conversão para cinza e equalização de histograma

3. **Configuração e treino da CNN**:

   * Carreguei o CIFAR-10 e filtrei apenas as classes de interesse (gatos e cachorros)
   * As imagens foram normalizadas (valores entre 0 e 1).
   * Defini a arquitetura com 3 camadas convolucionais , pooling, flatten e camadas densas.
   * Treinei rápidamente por 5 épocas (≈78 % de acurácia) e depois por 30 épocas, chegando aproximadamente 75% de acurácia no teste

4. **Avaliação do modelo**:

   * Além de calcular a acurácia no conjunto de teste, verifiquei a acurácia final e gerei o relatório de métricas.
   * Plotei a curva de acurácia por época para checar overfitting.
   
5. **Classificação das imagens externas**:

   * Redimensionei as imagens para 32×32, normalizei e rodei as predições das classes (gato ou cachorro).
   * Exibi cada imagem em uma grade e ao lado o rótulo previsto.

---

## **4. Resultados Obtidos**

* O modelo atingiu cerca de 75% de acurácia após 30 épocas

* No teste rápido de 5 épocas, ficou em torno de 70 %. 
*  As imagens externas tiveram alguns erros, principalmente na identificação de cachorros 
* Isso ocorre devido às diferenças de iluminação, fundo e ângulo e baixa resolução em relação ao CIFAR-10.
* A linha de treinamento cresce até quase 100 %, enquanto a de validação se estabiliza entre 0,72 e 0,75 após cerca de 10–12 épocas. Isso indica que, embora o modelo continue aprendendo características do conjunto de treino, não há ganho em generalização — sugerindo um leve overfitting.

---

## **5. Tempo Total Gasto**

* Preparação e pré-processamento: 30 min
* Implementação e treino inicial (5 épocas): 30 min
* Treino final (30 épocas): ~1 h
* Avaliação e organização do código: 30 min

Total aproximado: 2h a 2h 30 

---

## **6. Dificuldades Encontradas**

* Formatos variados das imagens externas exigiram ajustes manuais.
* Equalização só funciona em escala de cinza, demandando conversão prévia.
* Diferenças de estilo entre CIFAR-10 e fotos pessoais (iluminação, ângulo, fundo) afetaram a generalização.
* Manter o código organizado durante alterações de tamanho e arquitetura foi desafiador.


## **7. Como Executar o Código**

1. Clone este repositório:

   ```bash
   git clone https://github.com/seu-usuario/prova-visao.git
   ```
2. Acesse a pasta do projeto:

   ```bash
   cd prova-visao
   ```
3. Instale as dependências:

   ```bash
   pip install -r requirements.txt
   ```
4. Execute o script principal:

   ```bash
   python main.py
   ```
