# RedesNeurais-Imagem3D

Título: Desenvolvendo um Sistema de Reconhecimento de Monumento e Geração deste em 3D 

  

Introdução 

Com o avanço da inteligência artificial e visão computacional, a capacidade de identificar monumentos a partir de imagens e até mesmo gerar modelos 3D a partir delas tornou-se uma realidade. Por meio destas representações em 3D, vários usos podem surgir, contribuindo com agilidade em diversos serviços e uma utilização prática que podemos destacar aqui, é ouso de imagens em 3D de monumentos históricos para detecção de rachaduras, deterioração e conservação dos mesmos. Além disso, pode-se oferecer ao turista, contribuidor por fornecer sua self ou foto direta do monumento, uma lembrança interativa. 

A motivação desse desafio proposto pela disciplina de “Redes Neurais e Artificiais e suas Principais Aplicações”, pertencente ao curso de Pós-graduação “Inteligência Artificial” do SENAC SP, foi o IMC (Image Matching Challenge) 2022, cujo dataset está disponível no Kaggle1. 

O objetivo deste desafio é gerar maquetes 3D de fotos gratuitas capturadas por pessoas comuns/turistas, postadas na internet, a fim de lhes oferecer uma lembrança interativa e sob a perspectiva de outros ângulos. Sendo assim, este artigo explora o desenvolvimento de uma aplicação que utiliza as bibliotecas TensorFlow, Keras e hloc (localização hierarquizada) para identificar monumentos em fotos, classificá-los e criar modelos 3D detalhados. 

  

Desenvolvimento da Aplicação Generativa de Monumentos 3D 
  

Inicialmente, identificamos os requisitos da aplicação a serem desenvolvidas para a geração de imagens em 3D. Entendemos que a solução deveria ter no mínimo duas partes: 

Um modelo de identificação e classificação de imagens: dada uma foto de entrada, seria necessário identificar os objetos presentes, extrair o objeto que representa um monumento e identificar qual o monumento está presente na foto. Já a classificação estava envolvida com o dataset de treino, que possuía uma grande quantidade de fotos, envolvendo diversos monumentos. Logo seria necessário classificar os monumentos, agrupá-los e identificar esses grupos. 
 

Um modelo de geração de imagens 3D: a partir da identificação do monumento presente na foto de entrada, uma exibição do monumento 3D de forma interativa deverá ser exibida. 
Para criar a solução, decidiu-se pelo uso de bibliotecas, pois elas já possuem diversos recursos desenvolvidos e que facilitariam os trabalhos. Para o modelo de classificação, por exemplo, optou-se por utilizar TensorFlow e Keras, devido à sua eficácia com redes neurais convolucionais para tarefas de classificação de imagem. E para a criação de imagens em 3D, pela hloc, uma “caixa de ferramentas” modular para localização visual, que implementa localização hierárquica. Essa biblioteca faz uso interno de outras bem conhecidas no mundo de modelagem com imagens: Structure-from-Motion (SfM) e SuperPoint+SuperGlue . 

Modelo de Identificação e Classificação de Imagens  

Desenvolvemos um modelo de rede neural convolucional utilizando TensorFlow e Keras, treinado em um conjunto de dados diversificado de monumentos.  
O dataset  contém 16 classes(monumentos) e foi dividido com 70% das imagens para treino, 20% para validação e 10% para teste.  
Para aumentar nossa base de dados e treinarmos melhor o modelo, foi utilizado o data aumentation, onde fazemos pequenas transformações nas imagens, como pequenas rotações, zoom, redimensionamento. 
Para o treinamento do modelo, usamos camada Convolucionais com ativação relu,  BatchRegularization,  MaxPooling e Dropout. Já na camada de saida usamos a função de ativação softmax. 
Treinando com 40 epochs a acurácia de treino ficou em 0.9097 e a de validação ficou em 0.8982 
Realizamos testes extensivos do sistema, utilizando uma variedade de fotos de monumentos de diferentes ângulos e condições de iluminação.  
O sistema demonstrou uma boa capacidade de identificar monumentos com precisão a partir de imagens individuais.  

Modelo de Geração de Imagens em 3D 
O modelo de criação 3D não foi desenvolvido nesse desafio. Mas, sim utilizado algo que já estivesse implementado. Em nossas pesquisas, procuramos por algo que reproduzisse os pontos de similaridade encontrados nas imagens do dataset. Descobrimos uma biblioteca disponível no GitHub com documentação e de fácil uso. Além disso, os resultados dessa biblioteca representavam o que esperávamos: visual bonito e interatividade. 

A biblioteca de localização hierarquizada, ou mais conhecida como hloc, é posta pelo autor como "uma caixa de ferramentas modular para localização visual 6-DoF de última geração". Ela usa a recuperação de imagens, a correspondência de recursos, trazendo agilidade, precisão e posta como escalonável. A base do código tem uma rede neural que combina e torna facilmente acessível a correspondência de imagens e estrutura de movimento. 

Segundo o autor, com a hloc você pode reproduzir resultados de última geração em vários benchmarks de localização visual interna e externa, executar o Structure-from-Motion com SuperPoint+SuperGlue para localizar com seus próprios conjuntos de dados, avaliar recursos locais ou recuperação de imagens para localização visual e implementar novos pipelines de localização e depurá-los facilmente. Avaliamos a precisão da identificação dos monumentos e a qualidade dos modelos 3D gerados. 

Em suma, a hloc executa os seguintes comandos: 

Extrai recursos locais para todos os bancos de dados e imagens de consulta; 
Constrói um modelo SfM 3D de referência; 
Encontra imagens de banco de dados covisíveis, com recuperação ou um modelo SfM anterior; 
Combina os pares de bancos de dados com SuperGlue mais rápido; 
Triangula um novo modelo SfM com COLMAP; 
Encontra novamente imagens de banco de dados relevantes para cada consulta, usando recuperação; 
Combina as imagens da consulta; 
Executa a localização; 
Visualiza e depura. 
A localização dos pontos de similaridade pode então ser avaliada em visuallocalization.net para os conjuntos de dados suportados. 

Conclusão: 

Em resumo, o desenvolvimento deste sistema de reconhecimento de monumentos e geração de modelos 3D destacou o poder das tecnologias TensorFlow, Keras e SuperGlue na área de visão computacional. 
