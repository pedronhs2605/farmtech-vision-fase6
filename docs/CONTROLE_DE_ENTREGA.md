# Controle de entrega — FarmTech Vision Fase 6

## Evidências verificadas no notebook (capturas fornecidas)

- Dataset de detecção: 80 imagens, divididas em 64 treino, 8 validação e 8 teste.
- Anotações correspondentes: 64 treino, 8 validação e 8 teste.
- 134 anotações verificadas formalmente; nenhuma coordenada ou classe inválida encontrada.
- Classes do detector: `car` e `tractor`.
- Experimentos: YOLO personalizado com 30 e 60 épocas; YOLO pré-treinado; CNN de classificação por recortes.
- Métricas de teste do YOLO de 30 épocas: precisão 84,06%, recall 65,53%, mAP50 74,25%, mAP50-95 29,34%.
- Métricas de teste do YOLO de 60 épocas: precisão 61,17%, recall 70,83%, mAP50 75,95%, mAP50-95 40,69%.
- A CNN alcançou 100% de acurácia em 13 recortes de teste. O conjunto é pequeno e não demonstra generalização.

## Pendente antes da entrega

- [ ] Publicar o notebook `FarmTech_Vision_Fase6_Organizado.ipynb` no repositório.
- [ ] Conferir e publicar o `data.yaml` sem caminhos locais que impeçam reprodução.
- [ ] Conferir procedência e licença de cada imagem antes de publicar o dataset.
- [ ] Selecionar evidências visuais apropriadas para publicação, sem dados sensíveis ou material sem licença.
- [ ] Revisar a correspondência dos índices 0 e 1 com as classes no `data.yaml`.
- [ ] Verificar duplicatas ou vazamento entre treino, validação e teste.
- [ ] Adicionar link compartilhável do notebook e link do vídeo, se exigido.
- [x] Confirmar autoria individual e identificação acadêmica no README.

## Nota metodológica

Os dados do teste são reduzidos: métricas e comparações devem ser interpretadas como resultados experimentais, não como prova de desempenho em campo. A CNN classifica recortes e não executa a mesma tarefa de detecção do YOLO.
