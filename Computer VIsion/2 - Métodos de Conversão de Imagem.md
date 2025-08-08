# Métodos de Conversão de Imagem
### 1) Binarização
- Método mais simples de interpreteção de imagem
- Separa a imagem em dois tipos de regiões, regiões de interesse e regiões de não interesse, através de um ponto limiar escolhido no espectro de cores
  - "Apaga" partes não interessantes com branco e deixa apenas as partes relevantes em preto


### 2) ConvexHull
- Método de delimitação de objetos em uma imagem
- Cria um "contorno" ao redor das extremidades do objeto relevante para separá-lo do restante
