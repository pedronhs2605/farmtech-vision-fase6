# Auditoria preliminar da proveniência do dataset

## 1. Dataset efetivamente utilizado

- Projeto: FarmTech Vision — Fase 6.
- Pasta no Drive: `FarmTech_Vision_Fase6/dataset`.
- Organização documentada: 64 imagens de treinamento, 8 de validação e 8 de teste.
- `data.yaml` do projeto: `nc: 2`; classes na ordem `car` (0) e `tractor` (1).
- Os arquivos de imagens do projeto têm nomes como `image82_jpg.rf.b14e02558795111f505e255050a33e24.jpg`.

**Origem e licença dessas 80 imagens: ainda não confirmadas.** Não redistribuir as fotografias até estabelecer a procedência de cada arquivo ou lote.

## 2. ZIP encontrado na pasta downloads

Arquivo: `mix8235789-----.v4-mixed-fully-fixed.yolov8.zip`, presente em `FarmTech_Vision_Fase6/downloads/`.

O ZIP foi inspecionado e contém:
- `README.dataset.txt`, com identificação do projeto Roboflow e declaração **License: CC BY 4.0**;
- `README.roboflow.txt`, com exportação em **20 de maio de 2023**, aproximadamente **3.929 imagens** e formato YOLOv8;
- `data.yaml` com **13 classes**, entre elas `car` e `tractor`, além de metadados do projeto Roboflow.

Fonte declarada no arquivo: [Roboflow Universe — mix8235789](https://universe.roboflow.com/image-classification-d04ys/mix8235789---%3A). A página pública também indica licença **CC BY 4.0**. A atribuição ao conjunto original deve citar **Image Classification / Roboflow Universe**, o link e a licença, além de indicar quaisquer modificações, caso imagens desse conjunto sejam utilizadas.

**Limitação decisiva:** o ZIP original apresenta nomes de arquivos com prefixos como `-R0C83PP_png.rf...`, diferentes dos nomes observados na pasta de treino do projeto (`image82_jpg.rf...`). A presença do ZIP no Drive **não demonstra** que as 80 imagens do FarmTech Vision foram extraídas dele. Também não demonstra que toda fotografia presente no ZIP tem origem e cadeia de direitos individualmente auditadas.

## 3. Conduta de publicação

- [x] Identificar o arquivo ZIP e ler seus metadados de licença.
- [x] Conferir as duas classes do `data.yaml` do projeto.
- [x] Manter no GitHub os CSVs e gráficos selecionados, sem fotografias.
- [ ] Identificar o link exato do dataset de onde vieram as 80 imagens utilizadas.
- [ ] Verificar a licença aplicável ao dataset efetivamente usado e a cadeia de atribuição.
- [ ] Registrar transformações, filtros e seleção das 80 imagens.
- [ ] Conferir duplicatas ou quase duplicatas entre treino, validação e teste.
- [ ] Publicar imagens somente após confirmar autorização e cumprir a atribuição exigida.

**Não atribuir CC BY 4.0 às 80 imagens apenas porque existe outro ZIP com essa licença.**

## 4. Requisitos oficiais da atividade

Não foi localizado um enunciado específico e verificável da entrega individual **“O Despertar da Rede Neural”** que confirme vídeo obrigatório, formato de submissão, rubrica ou prazo. Essas exigências precisam ser conferidas no portal da disciplina ou no PDF oficial da atividade. Páginas genéricas da FIAP não substituem o enunciado.
