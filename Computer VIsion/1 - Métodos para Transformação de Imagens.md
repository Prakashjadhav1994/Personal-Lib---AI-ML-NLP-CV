# Métodos para Transformação de Imagens

## 1) Conceitos Gerais
### 1.1) Captura e Transformação de Imagens
- Embora humanos e computadores utilizem mecanismos diferentes, ambos seguem um processo semelhante: recebem sinais brutos e os interpretam. No caso dos humanos, a luz atinge células sensoriais (cones e bastonetes), e o cérebro interpreta os sinais elétricos; já os computadores recebem dados digitais, provenientes de um arquivo de imagem ou captura por sensor, compostos por bits, e os interpretam por meio de algoritmos
- Enquanto os seres humanos dispõem de um único sistema passivo de captura, computadores podem ter seus dados coletados de forma ativa (sensores infravermelhos, câmeras térmicas, câmera de movimento, etc.) ou passiva (recebido via arquivo com RGB tradicional)
  - Diferentes sensores (câmeras RGB, térmicas, de profundidade, ultrassom, etc.) permitem que algoritmos obtenham diferentes aspectos da realidade como cor, profundidade, calor, movimento entre outros
 

### 1.2) Pixel, Unidade de Arazenamento de Dados em Imagens
- O registro de uma imagem digital é geralmente realizado por unidades mínimas de cor/brilho Pixels
- Cada pixel é uma tuplas numéricas composta por 3 "canais", cada canal representa um valor de Red, Green ou Blue, que compõe aquele pixel
- A profundidade de bits (ou bit depth) define quantas variações de cor podem ser representadas ou a precisão com que cada cor é armazenada por pixel
  - Quanto mais bits disponíveis para representar uma cor, mais fiel à realiade ela será, pois permite mais nuances entre os tons de cada cor
<img width="929" height="300" alt="image" src="https://github.com/user-attachments/assets/0a59aa18-50b1-447a-b636-23fdabcb6a30" />


- Além do sistema RGB, existem outros modelos como CMYK (impressão), HSV (matiz/saturação), ou grayscale/escalas de cinza (1 canal)

- Por fim, a imagem é a reconstrução visual de uma matriz tridimensional, composta pelas coordenadas (x, y) de cada pixel e sua cor associada, quando renderizada em um dispositivo (tela, impressora)
  - Bibliotecas como OpenCV, PIL ou NumPy permitem acessar, modificar e analisar essa matriz em Python

# # 1) Binarização
- Método mais simples de interpreteção de imagem
- Separa a imagem em dois tipos de regiões, regiões de interesse e regiões de não interesse, através de um ponto limiar escolhido no espectro de cores
