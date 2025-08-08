# Métodos para Transformação de Imagens

Embora humanos e computadores utilizem mecanismos diferentes, ambos seguem um processo semelhante: recebem sinais brutos e os interpretam. No caso dos humanos, a luz atinge células sensoriais (cones e bastonetes), e o cérebro interpreta os sinais elétricos; já os computadores recebem dados digitais, provenientes de um arquivo de imagem ou captura por sensor, compostos por bits, e os interpretam por meio de algoritmos
- Enquanto os seres humanos dispõem de um único sistema passivo de captura, computadores podem ter seus dados coletados de forma ativa (sensores infravermelhos, câmeras térmicas, câmera de movimento, etc.) ou passiva (recebido via arquivo com RGB tradicional)
  - Diferentes sensores (câmeras RGB, térmicas, de profundidade, ultrassom, etc.) permitem que algoritmos obtenham diferentes aspectos da realidade como cor, profundidade, calor, movimento entre outros
- O registro de uma imagem digital é geralmente realizado por tuplas chamadas pixels. Pixels são unidades mínimas de cor/brilho, armazenadas como tuplas numéricas (ex.: [R, G, B] em imagens 24-bits, com valores de 0 a 255 por canal), totalizando mais de 16 milhões de combinações e cores possíveis.
  - Além do sistema RGB, existem outros modelos como CMYK (impressão), HSV (matiz/saturação), ou grayscale/escalas de cinza (1 canal)
- A imagem é a reconstrução visual de uma matriz tridimensional, composta pelas coordenadas (x, y) de cada pixel e sua cor associada, quando renderizada em um dispositivo (tela, impressora)
  - Bibliotecas como OpenCV, PIL ou NumPy permitem acessar, modificar e analisar essa matriz em Python

# # 1) Binarização
- Método mais simples de interpreteção de imagem
- Separa a imagem em dois tipos de regiões, regiões de interesse e regiões de não interesse, através de um ponto limiar escolhido no espectro de cores
