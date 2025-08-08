# Conceitos Gerais de Computação Gráfica

## 1) Captura e Transformação de Imagens
- Embora humanos e computadores utilizem mecanismos diferentes, ambos seguem um processo semelhante: recebem sinais brutos e os interpretam. No caso dos humanos, a luz atinge células sensoriais (cones e bastonetes), e o cérebro interpreta os sinais elétricos; já os computadores recebem dados digitais, provenientes de um arquivo de imagem ou captura por sensor, compostos por bits, e os interpretam por meio de algoritmos
- Enquanto os seres humanos dispõem de um único sistema passivo de captura, computadores podem ter seus dados coletados de forma ativa (sensores infravermelhos, câmeras térmicas, câmera de movimento, etc.) ou passiva (recebido via arquivo com RGB tradicional)
  - Diferentes sensores (câmeras RGB, térmicas, de profundidade, ultrassom, etc.) permitem que algoritmos obtenham diferentes aspectos da realidade como cor, profundidade, calor, movimento entre outros
 

## 2) Pixel ("picture element" ou elemento de imagem): A menor unidade visual de uma imagem
- O registro de uma imagem digital é geralmente realizado por unidades mínimas de cor/brilho Pixels
- No modelo mais comum, o RGB, cada pixel é uma tupla numéricas composta por 3 *canais*, cada canal representa um valor de Red, Green ou Blue, que compõe aquele pixel
- A profundidade de bits (ou bit depth) define quantas variações de cor podem ser representadas ou a precisão com que cada cor é armazenada por pixel
  - Quanto mais bits disponíveis para representar uma cor, mais fiel à realiade ela será, pois permite mais nuances entre os tons de cada cor
<img width="929" height="300" alt="image" src="https://github.com/user-attachments/assets/0a59aa18-50b1-447a-b636-23fdabcb6a30" />

- Um modelo derivado do RGB é o *Grayscale*, no qual seus pixels têm apenas 1 canal, que representa os tons de cinza na imagem, sendo normalmente 0 (preto) a 255 (branco) se for 8 bits, isso permite uma variação de intensidade luminosa
  - Grayscale é amplamente utilizada por sua simplicidade e menor custo computacional, pois representa a imagem com apenas um canal de intensidade, ao invés dos três canais RGB, mantendo informações de luminosidade sem precisar da cor
 
    
## 3) Formação da Imagem
- Por fim, a imagem nada mais é que a reconstrução visual de uma matriz tridimensional ou *Tensor*
- Esse *Tensor* é composto pelas coordenadas (x, y) de cada pixel e sua cor associada, quando renderizada em um dispositivo como uma tela ou impresso por uma impressora
  - Bibliotecas como OpenCV, PIL ou NumPy permitem acessar, modificar e analisar essa matriz em Python de diversas maneiras
