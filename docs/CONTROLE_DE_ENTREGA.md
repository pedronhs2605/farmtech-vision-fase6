# Controle de entrega — FarmTech Vision Fase 6

## Fonte da conferência

Capturas da atividade **Cap 1 — O despertar da Rede Neural**, portal FIAP, fornecidas em 15/10/2026. A análise refere-se à **Entrega 1** exibida nas capturas. As duas atividades adicionais “Ir Além” são mencionadas, mas seus enunciados não foram apresentados.

**Atenção ao prazo:** o cabeçalho mostra período encerrado em 13/10/2026 e envio pendente; outro quadro da mesma página mostra 18/10/2026 às 23h59. Há divergência de datas a confirmar no portal/tutoria. O aviso informa nota máxima de 70% para entregas até 3 dias após o prazo. Não assumir automaticamente que a submissão ainda está disponível.

## Confronto com os requisitos oficiais

| Exigência no enunciado | Situação do projeto | Ação |
|---|---|---|
| 40 imagens do objeto A + 40 do objeto B (80 imagens) | **Parcial**: 80 imagens confirmadas, mas a distribuição exata de 40 por objeto não foi comprovada | Auditar as imagens por classe, não confundir quantidade de caixas com quantidade de imagens |
| Por classe: 32 treino, 4 validação, 4 teste | **Parcial**: totais globais 64/8/8 confirmados, sem prova da divisão por classe | Conferir composição das partições |
| Imagens organizadas no Google Drive | **Atendido**: `dataset/images/{train,val,test}` | Manter |
| Rotulação das imagens de treinamento usando Make Sense IA | **Não comprovado**: rótulos YOLO existem, ferramenta utilizada não foi confirmada | Explicar ferramenta real; não afirmar uso de Make Sense IA sem evidência |
| Rótulos salvos no Google Drive | **Atendido**: `dataset/labels/{train,val,test}` | Manter |
| Colab conectado ao Drive com treino, validação, teste e Markdown passo a passo | **Parcial**: notebook e execução presentes; revisar se todas as etapas estão explicadas em Markdown | Conferir notebook |
| Pelo menos 2 simulações com épocas distintas (ex. 30 e 60) e comparação de acurácia, erro e desempenho | **Atendido em essência**: 30 e 60 épocas e métricas de precisão, recall, mAP e perdas nos históricos | Explicitar que mAP é métrica de detecção, e apresentar curvas de perdas |
| Conclusões sobre validação e teste | **Atendido** no README | Revisar Markdown no notebook |
| Prints das imagens de teste processadas pelo modelo | **Pendente**: imagens de teste existem no Drive, mas não foram publicadas por licença não verificada | Verificar autorização e selecionar prints legítimos |
| Repositório novo no GitHub com link no portal | **Parcial**: repositório criado e documentado, mas permanece privado; envio no portal consta pendente | Garantir acesso ao avaliador, sem publicar dados sem licença |
| Notebook Jupyter executado, comentado, com Markdown de análise | **Parcial**: notebook publicado; revisar organização e comentários | Conferir notebook |
| Nome do notebook com nome completo, RM e `pbl_fase6.ipynb` | **Pendente**: arquivo atual `FarmTech_Vision_Fase6_Organizado.ipynb` não segue o padrão mostrado | Renomear/criar cópia após obter RM confirmado |
| Vídeo de até 5 minutos, YouTube “não listado”, link no README | **Pendente**: não há link de vídeo no README | Gravar, publicar e inserir link |
| README introdutório com link do Colab/Jupyter e descrição completa | **Parcial**: documentação extensa, mas falta link compartilhável do Colab | Inserir link |
| Repositório público para acesso da equipe FIAP | **Pendente**: repositório privado | Confirmar segurança dos arquivos e tornar público antes da submissão, conforme enunciado |
| Enviar link do GitHub pelo portal, podendo usar PDF com link | **Pendente** na captura | Preparar submissão; não executar envio sem conferência do usuário |

## Evidências técnicas já verificadas

- Dataset: 80 imagens, sendo 64 treino, 8 validação e 8 teste.
- 134 anotações formalmente válidas; isso **não comprova** 40 imagens por classe.
- Classes confirmadas no `data.yaml`: `0=car`, `1=tractor`.
- Dois treinamentos YOLO: 30 e 60 épocas.
- Avaliação de teste com 8 imagens e 13 objetos.
- Métricas de teste (30 épocas): precisão 0,8406; recall 0,6553; mAP50 0,7425; mAP50-95 0,2934.
- Métricas de teste (60 épocas): precisão 0,6117; recall 0,7083; mAP50 0,7595; mAP50-95 0,4069.
- CSVs e gráficos de treinamento e avaliação já publicados em `evidencias/`.
- Origem/licença das imagens ainda não comprovadas; ver `docs/PROVENIENCIA_DATASET.md`.

## Prioridade para finalizar

1. **Resolver prazo e acesso ao portal**, porque a tela indica envio pendente.
2. **Confirmar RM**, criar notebook com o nome exigido e verificar sua apresentação.
3. **Gravar vídeo de até 5 minutos** e inserir o link não listado no README.
4. **Conferir distribuição das imagens por classe** e as evidências de rotulação.
5. **Revisar licença dos prints de teste** e publicar apenas os autorizados.
6. **Adicionar link do Colab**, verificar acesso público ao GitHub e enviar o link pelo portal.

Não confundir pendências de comprovação com etapas necessariamente não executadas.
