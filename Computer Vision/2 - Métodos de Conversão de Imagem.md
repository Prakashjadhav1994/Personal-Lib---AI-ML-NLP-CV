# 📘 Métodos de Conversão e Transformação de Imagem

Resumo de técnicas fundamentais utilizadas em **processamento de imagens**, **computação gráfica** e **visão computacional**.

---

## 1) Binarização (Thresholding)

**Conceito:**  
Método mais simples e fundamental para segmentação de imagens. Converte uma imagem em tons de cinza em uma imagem binária (apenas preto e branco).

**Funcionamento:**  
Um valor de limiar (*threshold* - `T`) é escolhido no espectro de intensidade (0–255).  
- Todos os pixels com intensidade acima de `T` → branco (1).  
- Todos os pixels abaixo de `T` → preto (0).  

**Fórmula:**  

\[
dst(x,y) = 
\begin{cases}
1, & \text{se } src(x,y) > T \\
0, & \text{caso contrário}
\end{cases}
\]

**Tipos Comuns:**
- **Global:** Um único valor de `T` para toda a imagem. Bom com iluminação uniforme.  
- **Otsu:** Calcula automaticamente `T` assumindo distribuição bimodal. Minimiza variância intra-classe.  
- **Adaptativo:** Calcula `T` localmente para pequenas regiões. Ideal em iluminação irregular.  

**Aplicações:** OCR, segmentação de objetos, pré-processamento de bordas.


![Figura 1: Exemplo de vetorização de uma imagem bitmap](https://github.com/LeoMSgit/Personal-Lib---AI-ML-NLP-CV/blob/main/Computer%20Vision/Image%20Folder/Example_Image-Trace-1-11.avif)
***Fonte: [Trabalho próprio, baseado em ferramentas de image trace.](https://helpx.adobe.com/br/illustrator/using/image-trace.html)***
![](https://github.com/LeoMSgit/Personal-Lib---AI-ML-NLP-CV/blob/main/Computer%20Vision/Image%20Folder/Example_Image-Trace-1-11.avif)
---

## 2) Convex Hull (Casca Convexa)

**Conceito:**  
Menor polígono convexo que envolve completamente um conjunto de pontos (ou objeto em uma imagem).  
Pense em esticar um elástico ao redor do objeto.  

**Funcionamento:**  
Algoritmos: *Graham’s Scan*, *Jarvis March*, etc.  

**Aplicações:**  
- Análise de forma (robustez, compactidade).  
- Simplificação de contornos irregulares.  
- Robótica: trajetórias em torno de obstáculos.  

---

## 3) Transformada de Hough

**Conceito:**  
Técnica para detectar **formas geométricas** (linhas, círculos, elipses), mesmo com ruído ou fragmentos.  

**Funcionamento:**  
- **Linhas:** representadas por  
  \[
  \rho = x \cdot \cos \theta + y \cdot \sin \theta
  \]  
  Cada ponto vota em todas as linhas possíveis → interseções indicam linhas reais.  
- **Círculos:** definidos por  
  \[
  (x - a)^2 + (y - b)^2 = r^2
  \]  
  Espaço paramétrico 3D (a, b, r).  

**Aplicações:**  
- Detecção de placas de trânsito (linhas).  
- Detecção de olhos (círculos).  
- Análise de documentos.  

---

## 4) Segmentação por Watershed (Bacia Hidrográfica)

**Conceito:**  
Trata a imagem como um mapa topográfico → intensidades = altitude.  

**Funcionamento:**  
1. Definir sementes (mínimos regionais).  
2. “Inundar” a imagem a partir dessas sementes.  
3. Construir barragens onde bacias se encontram.  

**Problema:** Sensível a ruído → super-segmentação.  
**Solução:** Marcadores controlados (foreground/background).  

**Aplicações:** Separar objetos tocando-se (ex.: glóbulos, grãos).  

---

## 5) Transformações Morfológicas

**Conceito:**  
Operações sobre **formas** em imagens binárias, usando um *elemento estruturante*.  

**Operações Básicas:**  
- **Erosão:** remove pixels na borda.  
- **Dilatação:** adiciona pixels na borda.  

**Operações Compostas:**  
- **Abertura (Open):** erosão + dilatação → remove ruídos pequenos.  
- **Fechamento (Close):** dilatação + erosão → preenche buracos.  
- **Gradiente Morfológico:** dilatação – erosão → extrai contornos.  

**Aplicações:** OCR, microscopia, imagens médicas.  

---

## 6) Suavização (Smoothing) / Blur

**Conceito:**  
Reduz ruído e detalhes finos (filtros passa-baixa).  

**Métodos:**  
- **Média (Averaging):** substitui pixel pela média da vizinhança.  
- **Gaussiano:** kernel gaussiano → preserva bordas melhor.  
- **Mediana:** substitui pelo valor mediano da vizinhança → ótimo para ruído *salt-and-pepper*.  

**Aplicações:** Pré-processamento para detecção de bordas (ex.: Canny).  

---

## 7) Transformações Geométricas

**Conceito:**  
Alteram a geometria dos pixels.  

**Operações:** Rotação, translação, escala, cisalhamento (*shear*).  

**Aplicações:** Correção de distorções, registro de imagens, *data augmentation*.  

---

## 8) Amostragem e Interpolação

**Conceito:**  
Redimensionamento (resize) de imagens.  

**Técnicas:**  
- **Vizinho mais próximo:** rápido, mas gera serrilhados.  
- **Bilinear:** suaviza mais.  
- **Bicúbica:** maior qualidade, pondera 16 vizinhos.  

---

## 9) Conversão entre Espaços de Cor

**Conceito:**  
Transforma imagens entre modelos de cor (RGB, HSV, LAB, YUV…).  

**Aplicações:**  
- **HSV/HSL:** segmentação por cor → intuitivo.  
- **LAB:** análise perceptual de cores.  
- **YUV/YCbCr:** compressão de vídeo (JPEG, MPEG).  

---

## 10) Operações Pontuais

**Conceito:**  
Saída de cada pixel depende apenas do seu valor de entrada.  

**Exemplos:**  
- Ajuste de brilho e contraste.  
- Correção gama (não-linear).  
- LUTs (Lookup Tables) para mapeamentos rápidos.  

---

## 11) Filtragem no Domínio da Frequência

**Conceito:**  
Após Transformada de Fourier, manipular frequências da imagem.  

**Filtros:**  
- **Passa-Baixa:** suavização, remove ruídos.  
- **Passa-Alta:** realce de bordas.  
- **Rejeita-Banda:** remove padrões periódicos.  

---

## 🔗 Resumo Visual do Pipeline de Processamento

Imagem Colorida ➜ Escala de Cinza ➜ Filtragem (Suavização) ➜ Equalização ➜ Binarização ➜ Transformações Morfológicas (Limpeza) ➜ Detecção de Bordas / Segmentação ➜ Extração de Features (ex: Convex Hull ou OCR)
