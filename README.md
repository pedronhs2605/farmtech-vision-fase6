# FarmTech Vision — Fase 6: O Despertar da Rede Neural

**Projeto acadêmico | FIAP — Inteligência Artificial e Machine Learning**  
**Tema:** visão computacional aplicada à identificação de carros e tratores  
**Ambiente de desenvolvimento:** Google Colab e Google Drive  
**Notebook principal:** `FarmTech_Vision_Fase6_Organizado.ipynb`

> **Estado do projeto:** experimentos executados e resultados analisados. Este README documenta os resultados observados no notebook; a publicação do repositório, a origem/licença individual das imagens e os links finais de apresentação devem ser conferidos antes da entrega.

## 1. Contextualização

A visão computacional permite identificar padrões visuais em imagens e apoiar aplicações de monitoramento, automação e análise de cenários. No contexto agrícola, reconhecer máquinas e veículos pode ser um passo inicial para sistemas de acompanhamento operacional. Neste trabalho, o recorte experimental consiste em **detectar carros (`car`) e tratores (`tractor`) em imagens**, comparando diferentes estratégias de visão computacional.

O estudo não constitui, por si só, um sistema de monitoramento agrícola implantado em campo. Trata-se de um experimento acadêmico com conjunto de dados reduzido, voltado à implementação, avaliação e discussão crítica dos modelos.

## 2. Problema e objetivos

**Problema:** identificar e localizar carros e tratores em imagens, avaliando como a quantidade de épocas de treinamento influencia a qualidade das detecções e quais são os limites de abordagens alternativas.

**Objetivo geral:** desenvolver e avaliar um fluxo de visão computacional para reconhecimento de carros e tratores, documentando decisões, métricas e limitações.

**Objetivos específicos:**

- Organizar imagens e anotações no formato de detecção YOLO.
- Treinar um detector YOLO personalizado por **30** e **60 épocas**, mantendo a mesma configuração-base para comparação.
- Avaliar os pesos treinados em um conjunto de teste separado.
- Examinar um YOLO pré-treinado sem adaptação específica às classes do projeto.
- Implementar uma CNN de classificação com imagens recortadas, como abordagem complementar.
- Analisar quantitativamente os resultados e inspecionar evidências visuais, incluindo falhas.

## 3. Escopo das abordagens

| Abordagem | Tarefa | Papel no estudo |
|---|---|---|
| YOLO personalizado — 30 épocas | Detecção e localização | Experimento de referência com menor tempo de treinamento |
| YOLO personalizado — 60 épocas | Detecção e localização | Experimento com maior número de épocas |
| YOLO pré-treinado, sem ajuste específico | Detecção e localização | Referência qualitativa para discutir diferenças entre classes genéricas e classes do projeto |
| CNN treinada do zero | Classificação de recortes | Experimento complementar de reconhecimento de classe |

**Distinção metodológica:** YOLO prevê classes e caixas delimitadoras em imagens completas; a CNN classifica recortes já preparados. Portanto, suas métricas não representam a mesma tarefa e **não devem ser comparadas diretamente como se fossem equivalentes**.

## 4. Tecnologias e ambiente

- **Python**, para implementação e análise.
- **Google Colab**, para execução do notebook.
- **Google Drive**, para armazenamento persistente dos dados, pesos e resultados.
- **Ultralytics YOLO**, para treinamento, inferência e avaliação de detecção.
- **TensorFlow/Keras**, para o experimento de CNN (conforme implementação do notebook).
- **Pandas**, para leitura e comparação dos históricos de treinamento.
- **Matplotlib e Pillow**, para inspeção e visualização de imagens.
- **Scikit-learn**, quando aplicável às métricas de classificação.

Os experimentos de avaliação exibidos no notebook utilizaram uma **GPU NVIDIA Tesla T4**. Tempos e resultados podem variar entre execuções, versões das bibliotecas e ambientes. Para registrar versões efetivas, consulte as saídas do próprio notebook.

## 5. Dataset e organização

O conjunto organizado contém **80 imagens** distribuídas em três partições:

| Partição | Imagens | Arquivos de anotação | Objetos anotados |
|---|---:|---:|---:|
| Treinamento (`train`) | 64 | 64 | 106 |
| Validação (`val`) | 8 | 8 | 15 |
| Teste (`test`) | 8 | 8 | 13 |
| **Total** | **80** | **80** | **134** |

Os totais de objetos foram apurados a partir dos arquivos de anotação: treino com 71 objetos da classe de índice `0` e 35 da classe `1`; validação com 9 e 6; teste com 9 e 4, respectivamente. A correspondência foi conferida no `data.yaml` do Google Drive: **índice `0` = `car` e índice `1` = `tractor`**.

**Atenção à unidade de análise:** o número de objetos anotados não equivale ao número de imagens. Uma mesma imagem pode conter vários objetos. A contagem acima também **não comprova** a distribuição de 40 imagens por classe; imagens com ambas as classes tornam essa afirmação especialmente delicada.

### 5.1 Estrutura principal

```text
FarmTech_Vision_Fase6/
├── dataset/
│   ├── images/
│   │   ├── train/           # 64 imagens
│   │   ├── val/             # 8 imagens
│   │   └── test/            # 8 imagens
│   └── labels/
│       ├── train/           # 64 arquivos .txt
│       ├── val/             # 8 arquivos .txt
│       └── test/            # 8 arquivos .txt
├── results/
│   ├── farmtech_yolo_v1/
│   │   ├── weights/best.pt
│   │   └── results.csv
│   ├── yolo_custom/
│   │   └── treino_60_epocas/
│   │       ├── weights/best.pt
│   │       └── results.csv
│   ├── avaliacao_final/
│   └── evidencias_visuais/
├── docs/
└── FarmTech_Vision_Fase6_Organizado.ipynb  # notebook a publicar junto ao projeto
```

A estrutura é representativa dos caminhos confirmados no Google Drive. Outros arquivos de resultados podem ter sido produzidos pelo notebook. **O experimento de 30 épocas foi salvo em `results/farmtech_yolo_v1/`, não no caminho inicialmente esperado `results/yolo_custom/treino_30_epocas/`.** Esse detalhe deve ser respeitado na reprodução da avaliação.

### 5.2 Origem, direitos e qualidade dos dados

Antes de publicar o dataset, é necessário registrar a **origem de cada conjunto de imagens, sua licença e as condições de redistribuição**. Essas informações não foram confirmadas nas evidências disponíveis para este README; portanto, não se atribui aqui uma licença não verificada. Caso não exista permissão de redistribuição, publique apenas o notebook, os scripts, as métricas e exemplos permitidos, indicando como obter legalmente os dados.

A inspeção visual das caixas é complementar à validação automática: coordenadas válidas não garantem que cada objeto tenha sido identificado e delimitado corretamente. Também é importante conferir se imagens iguais ou quase iguais não aparecem em partições distintas.

A auditoria preliminar da proveniência e os metadados do ZIP identificado estão documentados em [`docs/PROVENIENCIA_DATASET.md`](docs/PROVENIENCIA_DATASET.md).

## 6. Preparação e verificação das anotações

As anotações de detecção seguem o formato YOLO, com uma linha por objeto:

```text
class_id x_center y_center width height
```

As coordenadas são normalizadas entre `0` e `1`. Foi executada uma verificação automática da quantidade de valores por linha, índices de classe aceitos, dimensões positivas e limites das caixas. **Resultado: 134 anotações válidas e 0 problemas detectados.**

Esse teste confirma a consistência formal das anotações verificadas, mas **não avalia** se os rótulos estão semanticamente corretos, se faltam objetos ou se as caixas estão bem ajustadas visualmente.

## 7. Configuração experimental

Nos dois treinamentos personalizados foi utilizada a arquitetura-base **`yolov8n.pt`**, com:

| Parâmetro | Valor |
|---|---|
| Arquitetura inicial | YOLOv8 nano (`yolov8n.pt`) |
| Tamanho de imagem (`imgsz`) | 640 |
| Semente (`seed`) | 42 |
| Experimento A | 30 épocas |
| Experimento B | 60 épocas |
| Dataset | Mesmo conjunto organizado em `train`, `val` e `test` |

O objetivo foi isolar, tanto quanto possível, a alteração do número de épocas. Ainda assim, execuções em GPU e processos de treinamento podem apresentar variabilidade. A comparação deve considerar as métricas de teste e não somente o melhor resultado registrado durante o treinamento.

## 8. Treinamento dos detectores personalizados

O notebook realiza treinamento e salva históricos (`results.csv`) e melhores pesos (`best.pt`). Os caminhos confirmados são:

```text
results/farmtech_yolo_v1/weights/best.pt
results/yolo_custom/treino_60_epocas/weights/best.pt
```

Os históricos registraram 30 e 60 épocas, respectivamente. O maior valor de **mAP@0.50 na validação** observado em cada histórico foi:

| Treinamento | Melhor mAP@0.50 de validação |
|---|---:|
| 30 épocas | 0,6068 |
| 60 épocas | 0,7048 |

Esses números descrevem a validação durante o desenvolvimento; **não são as métricas finais de teste**.

### 8.1 Comparação dos históricos de validação (arquivos `results.csv`)

Os históricos das execuções de 30 e 60 épocas registram as métricas de validação a cada época. Na **última época** de cada execução, os resultados foram:

| Métrica de validação | 30 épocas (época 30) | 60 épocas (época 60) | Diferença (60 − 30) |
|---|---:|---:|---:|
| Precisão | 0,5229 | 0,6638 | +0,1409 |
| Recall | 0,6667 | 0,5554 | −0,1113 |
| mAP@0.50 | 0,5548 | 0,6526 | +0,0978 |
| mAP@0.50:0.95 | 0,3416 | 0,3531 | +0,0115 |

No histórico de **30 épocas**, o maior mAP@0.50 foi **0,6068 (época 28)** e o maior mAP@0.50:0.95 foi **0,3803 (época 26)**. No histórico de **60 épocas**, o maior mAP@0.50 foi **0,7048 (época 52)** e o maior mAP@0.50:0.95 foi **0,3541 (época 59)**. Os máximos de métricas distintas não necessariamente ocorrem no mesmo checkpoint.

**Leitura crítica:** na última época, o experimento de 60 épocas teve precisão e mAP@0.50 maiores, porém recall menor. O ganho em mAP@0.50:0.95 foi pequeno. Esses valores são de **validação durante o treinamento**, e não substituem a avaliação independente do conjunto de teste apresentada na seção 9. Como os melhores pesos podem corresponder a épocas anteriores à última, também não se deve confundir a linha final do CSV com o desempenho de `best.pt`.

## 9. Avaliação final no conjunto de teste

Os melhores pesos de cada execução foram avaliados com `split='test'` no mesmo conjunto de **8 imagens e 13 objetos anotados**.

| Métrica | YOLO 30 épocas | YOLO 60 épocas |
|---|---:|---:|
| Precisão | **0,8406** | 0,6117 |
| Recall | 0,6553 | **0,7083** |
| mAP@0.50 | 0,7425 | **0,7595** |
| mAP@0.50:0.95 | 0,2934 | **0,4069** |

### 9.1 Interpretação

O modelo de **30 épocas** apresentou maior **precisão**, isto é, maior proporção de detecções positivas corretas entre as predições positivas consideradas na avaliação. O modelo de **60 épocas** apresentou maior **recall**, além de mAP@0.50 e mAP@0.50:0.95 superiores.

O ganho em mAP@0.50 foi de **0,0170** ponto absoluto; em mAP@0.50:0.95, de **0,1135** ponto absoluto. Em contrapartida, a precisão caiu **0,2289** ponto absoluto. Portanto, **mais épocas não significaram melhoria uniforme**.

O mAP@0.50:0.95 avalia o desempenho em múltiplos limiares de sobreposição (IoU) e oferece uma leitura mais exigente da localização. Mesmo no modelo de 60 épocas, o valor de 0,4069 evidencia espaço para melhoria, sobretudo diante da amostra pequena.

### 9.2 Resultados por classe

A avaliação exibida no notebook indicou variações entre as classes `car` e `tractor`. Como o conjunto de teste possui apenas 13 objetos, pequenas alterações no acerto de uma classe podem provocar mudanças relevantes nas métricas. Recomenda-se consultar as tabelas por classe e as matrizes de confusão geradas em `results/avaliacao_final/` antes de tirar conclusões sobre desempenho em condições reais.

## 10. Evidências visuais e análise de erros

O projeto gerou gráficos de avaliação, matrizes de confusão e imagens de predição, além de uma inspeção visual das caixas anotadas. Os **2 históricos CSV e 10 gráficos selecionados** estão publicados na pasta [`evidencias/`](evidencias/) do repositório, com inventário em [`docs/EVIDENCIAS.md`](docs/EVIDENCIAS.md). As imagens com fotografias do dataset não foram republicadas, pois suas permissões ainda precisam ser verificadas.

Na análise visual, observar:

1. Objetos pequenos ou distantes, especialmente carros em vias.
2. Múltiplos objetos na mesma imagem e possíveis sobreposições de caixas.
3. Tratores vistos de ângulos distintos.
4. Falsos positivos, objetos não detectados e caixas mal posicionadas.
5. Diferenças entre os resultados dos modelos de 30 e 60 épocas.

**Não selecionar apenas exemplos bem-sucedidos:** falhas são evidências relevantes para interpretar a generalização. As imagens exibidas no notebook precisam ser conferidas quanto à licença antes de serem republicadas no GitHub.

## 11. YOLO pré-treinado sem adaptação específica

Foi também examinada uma abordagem YOLO pré-treinada, sem ajuste supervisionado específico para as duas classes do projeto. Nas observações registradas, essa abordagem apresentou rapidez de inferência, mas limitações na identificação de classes específicas, especialmente tratores, incluindo casos de classificação como `train`.

A observação ilustra a diferença entre utilizar classes genéricas de um modelo pré-treinado e adaptar um detector às classes definidas no experimento. **Não se afirma superioridade quantitativa** sem uma avaliação controlada, com a mesma definição de classes e protocolo de teste.

## 12. CNN treinada do zero para classificação

O notebook inclui uma rede neural convolucional treinada do zero para classificar **recortes de imagens**. No conjunto de teste apresentado, a CNN alcançou **100% de acurácia em 13 recortes**.

Esse resultado é restrito aos exemplos avaliados. Uma amostra de 13 recortes é insuficiente para concluir que o modelo generaliza bem para novas imagens, câmeras, cenários e condições de iluminação. O teste também deve ser auditado quanto à independência entre os recortes e as imagens usadas no treinamento.

Além disso, **classificação de recortes não é detecção de objetos**: a CNN recebe um objeto previamente recortado, enquanto o YOLO precisa localizá-lo na imagem completa. A comparação é conceitual e metodológica, não uma disputa direta entre os valores de acurácia e mAP.

## 13. Comparação crítica das abordagens

| Critério | YOLO personalizado | YOLO pré-treinado sem adaptação | CNN do zero |
|---|---|---|---|
| Saída | Classe e localização | Classe e localização | Classe do recorte |
| Adequação às classes do projeto | Treinado especificamente para `car` e `tractor` | Limitada pela taxonomia original | Depende dos recortes rotulados |
| Avaliação principal | Precisão, recall, mAP | Observação qualitativa no experimento | Acurácia em recortes |
| Principal limitação observada | Conjunto de teste pequeno e desempenho variável entre métricas | Confusão com classes não correspondentes ao projeto | Teste com somente 13 recortes |

A abordagem mais apropriada depende da tarefa. Para localizar carros e tratores em imagens completas, o YOLO personalizado é a alternativa diretamente alinhada ao objetivo. Para classificar recortes previamente extraídos, a CNN constitui um experimento complementar. A escolha entre 30 e 60 épocas depende do compromisso desejado entre precisão e capacidade de recuperar objetos, além do custo computacional.

## 14. Limitações e ameaças à validade

- **Amostra reduzida:** apenas 80 imagens no total e 8 imagens/13 objetos no teste.
- **Possível baixa diversidade:** é necessário confirmar variedade de cenários, fontes, ângulos, iluminação e condições ambientais.
- **Risco de vazamento de dados:** verificar duplicatas e imagens quase idênticas entre treino, validação e teste.
- **Anotações:** a verificação automática detectou 0 problemas formais, mas não substitui revisão manual de classe, completude e qualidade das caixas.
- **Variabilidade experimental:** uma única divisão e uma única semente não demonstram estabilidade estatística.
- **Comparabilidade:** métricas de detecção YOLO e acurácia de classificação CNN medem tarefas diferentes.
- **Proveniência:** fontes e licenças das imagens devem ser documentadas antes da redistribuição.
- **Aplicação prática:** não foram demonstrados testes em vídeo contínuo, operação em tempo real em campo, robustez sob clima adverso ou implantação em hardware agrícola.

## 15. Melhorias futuras

1. Ampliar o dataset com imagens licenciadas e diversidade de cenários, iluminação, escala e perspectivas.
2. Revisar manualmente anotações e checar duplicatas entre partições.
3. Repetir os experimentos com diferentes sementes ou divisões e reportar dispersão das métricas.
4. Avaliar mais imagens independentes, incluindo casos difíceis e negativos.
5. Analisar erros por classe e por tamanho de objeto.
6. Comparar tempo de inferência e uso de recursos sob condições controladas.
7. Investigar ajustes de hiperparâmetros e aumento de dados, sem utilizar o conjunto de teste para seleção de modelos.
8. Validar o detector em novos cenários antes de considerar uma aplicação operacional.

## 16. Como executar no Google Colab

**Pré-requisitos:** acesso ao Google Colab, ao Google Drive e aos arquivos do dataset. Recomenda-se GPU quando disponível.

1. Abra `FarmTech_Vision_Fase6_Organizado.ipynb` no Google Colab.
2. Conecte o Google Drive e confirme o diretório-base `/content/drive/MyDrive/FarmTech_Vision_Fase6`.
3. Verifique a presença de `dataset/images/{train,val,test}` e `dataset/labels/{train,val,test}`.
4. Execute as células de instalação de dependências e configuração do dataset (`data.yaml`).
5. Confirme no `data.yaml` a ordem e os nomes das classes e os caminhos das partições.
6. Execute os treinamentos de 30 e 60 épocas **apenas se desejar reproduzi-los**; caso contrário, reutilize os pesos `best.pt` já salvos.
7. Execute a avaliação com `split='test'` para cada conjunto de pesos.
8. Inspecione as evidências visuais e as análises comparativas.
9. Execute separadamente as seções do YOLO pré-treinado e da CNN, observando que têm propósitos diferentes.

Exemplo de avaliação dos pesos existentes:

```python
from pathlib import Path
from ultralytics import YOLO

base = Path('/content/drive/MyDrive/FarmTech_Vision_Fase6')
# DATA_YAML deve apontar para o data.yaml configurado no notebook.
pesos = {
    'YOLO 30 épocas': base / 'results/farmtech_yolo_v1/weights/best.pt',
    'YOLO 60 épocas': base / 'results/yolo_custom/treino_60_epocas/weights/best.pt',
}

for nome, caminho in pesos.items():
    if not caminho.is_file():
        print(f'{nome}: pesos não encontrados em {caminho}')
        continue
    metricas = YOLO(str(caminho)).val(data=str(DATA_YAML), split='test', imgsz=640)
    print(nome, metricas.results_dict)
```

**Observação:** a variável `DATA_YAML` é definida nas células de configuração do notebook. Os pesos e dados armazenados no Drive não são incluídos automaticamente no repositório GitHub.

## 17. Reprodutibilidade e organização da entrega

Para permitir auditoria, o repositório deve conter, no mínimo:

- Notebook `.ipynb` com células e resultados relevantes.
- Este `README.md`.
- Arquivo de configuração do dataset (`data.yaml`), **sem caminhos pessoais inválidos para terceiros**.
- Registros de treinamento e avaliação (`results.csv`, tabelas e gráficos) quando permitidos.
- Exemplos de evidências visuais cuja publicação seja autorizada.
- Descrição da origem/licença dos dados ou instruções de obtenção, quando o dataset não puder ser distribuído.
- Informações sobre versões das bibliotecas e instruções de execução.

Arquivos de pesos (`.pt`) podem ser grandes; verificar limites de tamanho e regras de publicação do GitHub. Se não forem enviados ao repositório, explicar onde estão armazenados e como reproduzir o treinamento.

## 18. Checklist de revisão antes da entrega

- [x] Estrutura `train`, `val` e `test` confirmada: 64/8/8 imagens.
- [x] Arquivos de anotações presentes: 64/8/8.
- [x] Validação formal: 134 anotações válidas e 0 problemas encontrados.
- [x] Treinamentos YOLO de 30 e 60 épocas executados.
- [x] Pesos e históricos dos dois treinamentos localizados.
- [x] Avaliações de teste registradas.
- [x] Evidências visuais geradas e localizadas.
- [x] YOLO pré-treinado e CNN discutidos no notebook.
- [x] Comparação crítica elaborada com métricas reais.
- [ ] Confirmar fontes, licenças e permissões de publicação das imagens.
- [x] Conferir correspondência entre índices `0`/`1` e classes no `data.yaml`: `0=car`, `1=tractor`.
- [ ] Revisar visualmente exemplos difíceis e duplicatas entre partições.
- [x] Publicar notebook, README, históricos CSV e gráficos selecionados no repositório (sem fotografias do dataset).
- [ ] Inserir links finais do GitHub, notebook e vídeo, conforme exigências da atividade.

## 19. Links e identificação da entrega

- **Repositório GitHub:** https://github.com/pedronhs2605/farmtech-vision-fase6
- **Notebook Google Colab:** link compartilhável pendente de publicação.
- **Vídeo de apresentação:** incluir o link caso seja exigido pela atividade.
- **Responsável pelo desenvolvimento:** Pedro Henrique do Nascimento Souza.
- **Instituição e curso:** FIAP — Inteligência Artificial e Machine Learning.
- **Modalidade de desenvolvimento:** projeto individual, desenvolvido integralmente por Pedro Henrique do Nascimento Souza.

**Origem e licença do dataset:** as imagens foram utilizadas para fins acadêmicos e experimentais. Foi identificado um arquivo ZIP de outro conjunto disponível no Drive, com metadados Roboflow e licença CC BY 4.0, mas **a correspondência desse ZIP com as 80 imagens efetivamente utilizadas ainda não foi comprovada**. A licença do ZIP não é automaticamente atribuída ao subconjunto do projeto. A identificação das fontes e a verificação das condições de redistribuição dessas 80 imagens continuam pendentes. Até a conclusão dessa verificação, o dataset não será disponibilizado publicamente. O uso acadêmico, por si só, não comprova permissão para redistribuir as imagens.

As verificações técnicas e documentais ainda pendentes estão relacionadas na seção 18 e em `docs/CONTROLE_DE_ENTREGA.md`.

## 20. Conclusão

O FarmTech Vision permitiu implementar e avaliar técnicas de detecção e classificação de imagens, com análise de resultados reais e de limitações metodológicas. No teste dos detectores personalizados, o treinamento de 30 épocas obteve maior precisão (**0,8406**), enquanto o de 60 épocas alcançou maior recall (**0,7083**), mAP@0.50 (**0,7595**) e mAP@0.50:0.95 (**0,4069**).

Os resultados mostram que aumentar o número de épocas pode beneficiar determinadas métricas sem melhorar todas elas. A CNN obteve 100% de acurácia nos 13 recortes avaliados, mas esse número não permite inferir desempenho equivalente em detecção nem generalização ampla. O experimento também evidencia a importância de qualidade e procedência dos dados, avaliação independente e análise dos erros.

**Síntese:** o objetivo acadêmico de implementar e comparar abordagens de visão computacional foi atendido no ambiente experimental documentado; a validação para uso em situações reais permanece como trabalho futuro.