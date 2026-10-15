# Índice de evidências — FarmTech Vision Fase 6

Este documento organiza as evidências existentes no Google Drive e indica quais arquivos devem ser selecionados para uma eventual publicação no GitHub. **Os CSVs e gráficos selecionados já foram copiados para o repositório em `evidencias/`.** Não publicar imagens do dataset sem verificar a licença e a permissão de redistribuição.

## 1. Pastas de origem (Google Drive)

| Conjunto | Localização | Conteúdo identificado nas capturas |
|---|---|---|
| Resultados gerais | [results](https://drive.google.com/drive/folders/1P5eHmpsfCYJGs0MWhzap12kRpltIP4ny) | `avaliacao_final`, `avaliacao_teste`, `evidencias_visuais`, `farmtech_yolo_v1`, `predicoes_teste`, `yolo_custom`, `yolo_tradicional`, `cnn_farmtech.keras` |
| Avaliação final | [avaliacao_final](https://drive.google.com/drive/folders/15s-Z3RUYByhivp6wn45MmgPH_MV_ViX0) | Pastas das avaliações de 30 e 60 épocas e curvas/matrizes |
| Avaliação de 30 épocas | [YOLO_30_épocas](https://drive.google.com/drive/folders/1HaXGHoK5Mb9-GJtDxya27Rif2c-7jDJM) | `BoxF1_curve.png`, `BoxP_curve.png`, `BoxPR_curve.png`, `BoxR_curve.png`, `confusion_matrix.png`, `confusion_matrix_normalized.png`, `val_batch0_labels.jpg`, `val_batch0_pred.jpg` |
| Avaliação de 60 épocas | [YOLO_60_épocas](https://drive.google.com/drive/folders/1s9tLPsK-9PQTRKFYf1xfQb7BOKNQ06nJ) | Mesmos tipos de curvas, matrizes e imagens de validação |
| Treinamento YOLO inicial | [farmtech_yolo_v1](https://drive.google.com/drive/folders/1SDelY9pPyEgfdK7G_9O_KmFjolBNubv2) | `results.csv`, `results.png`, `labels.jpg` e imagens de lotes |
| Treinamento personalizado 60 épocas | [treino_60_epocas](https://drive.google.com/drive/folders/1fAs_WDgoUEAzcUncJ76hI_8AO_I0xqnD) | `results.csv`, `results.png`, curvas, matrizes e imagens de lotes |

**Observação:** os IDs das pastas foram confirmados pela conexão com o Google Drive. O acesso de terceiros depende das permissões de compartilhamento do Drive.

## 2. Estrutura recomendada para evidências publicáveis

```text
evidencias/
├── README.md                     # este índice (ou documentação equivalente)
├── treinamento/
│   ├── yolo_30_epocas/
│   │   ├── results.csv
│   │   └── results.png
│   └── yolo_60_epocas/
│       ├── results.csv
│       └── results.png
├── avaliacao_teste/
│   ├── yolo_30_epocas/
│   │   ├── confusion_matrix.png
│   │   ├── confusion_matrix_normalized.png
│   │   ├── BoxPR_curve.png
│   │   └── BoxF1_curve.png
│   └── yolo_60_epocas/
│       ├── confusion_matrix.png
│       ├── confusion_matrix_normalized.png
│       ├── BoxPR_curve.png
│       └── BoxF1_curve.png
└── exemplos_visuais/
    └── (não publicada: licenças ainda não verificadas)
```

**Não copiar automaticamente:** `best.pt`, `cnn_farmtech.keras`, o dataset bruto e imagens com licença não verificada. Os modelos e dados podem permanecer no Drive; registrar a forma de acesso e reprodução quando pertinente.

**Publicado em GitHub:** [abrir pasta de evidências](https://github.com/pedronhs2605/farmtech-vision-fase6/tree/main/evidencias). Os gráficos publicados não incluem fotografias originais do dataset.

## 3. Resultados finais documentados

Avaliação de teste com 8 imagens e 13 objetos anotados:

| Métrica | YOLO 30 épocas | YOLO 60 épocas |
|---|---:|---:|
| Precisão | 0,8406 | 0,6117 |
| Recall | 0,6553 | 0,7083 |
| mAP@0.50 | 0,7425 | 0,7595 |
| mAP@0.50:0.95 | 0,2934 | 0,4069 |

Esses resultados são distintos dos históricos de validação por época, comparados na seção 8.1 do README principal. Não inferir que mais épocas melhoraram todas as métricas.

## 4. Como interpretar as figuras

- **`BoxP_curve.png`**: precisão em função do limiar de confiança.
- **`BoxR_curve.png`**: recall em função do limiar de confiança.
- **`BoxF1_curve.png`**: compromisso entre precisão e recall.
- **`BoxPR_curve.png`**: relação entre precisão e recall.
- **`confusion_matrix.png`**: contagens de acertos e confusões; considerar a orientação dos eixos.
- **`confusion_matrix_normalized.png`**: proporções normalizadas; não interpretar como quantidade absoluta.
- **`val_batch0_labels.jpg` / `val_batch0_pred.jpg`**: rótulos e predições visualizadas; verificar direitos sobre as imagens antes de publicar.
- **`results.csv` / `results.png`**: evolução das métricas e perdas durante o treinamento.

## 5. Verificações antes da entrega

- [x] Pastas de resultados e avaliações identificadas nas capturas.
- [x] Métricas de teste documentadas no README principal.
- [x] Índice com localização e finalidade das evidências.
- [x] Copiar para `evidencias/` os 2 CSVs e 10 gráficos selecionados.
- [ ] Confirmar que as matrizes e curvas escolhidas correspondem às avaliações finais corretas.
- [ ] Verificar licenças e direitos de redistribuição de cada imagem antes de publicar exemplos.
- [ ] Verificar duplicatas entre treino, validação e teste.
- [ ] Conferir os links de compartilhamento e a abertura do notebook para avaliadores.
- [ ] Revisar as exigências específicas do enunciado e os links de entrega.

**Critério de seleção:** priorizar arquivos que sustentem a comparação dos modelos, sem sobrecarregar o repositório com imagens repetidas ou arquivos temporários.
