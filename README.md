## Домашнее задание №3
### Абу Аль Лабан Надя, группа 2

Целью данного домашнего задания является разбивка (аннотация) генома человека на разные типы эпигенетических состояний. Это будет сделано на основании данных о наличии различных гистоновых модификаций (гистоновый код) в соответствующих участках генома.

Тетрадки с решением
---
- [Ссылка](https://colab.research.google.com/drive/1R5VGBeDns0fqdG_o1Pvv8Snj2gzMlL48?usp=sharing) на коллаб
  
Список гистоновых меток
---
**Клеточная линия:** Dnd41  
|    | Метка    | Файл в колабе | Оригинальный файл                            |
|----|----------|---------------|----------------------------------------------|
| 1  | H2az     | H2az.bam      | wgEncodeBroadHistoneDnd41H2azAlnRep1.bam     |
| 2  | H3k27ac  | H3k27ac.bam   | wgEncodeBroadHistoneDnd41H3k27acAlnRep1.bam  |
| 3  | H3k27me3 | H3k27me3.bam  | wgEncodeBroadHistoneDnd41H3k27me3AlnRep1.bam |
| 4  | H3k36me3 | H3k36me3.bam  | wgEncodeBroadHistoneDnd41H3k36me3AlnRep1.bam |
| 5  | H3k04me1 | H3k04me1.bam  | wgEncodeBroadHistoneDnd41H3k04me1AlnRep1.bam |
| 6  | H3k04me2 | H3k04me2.bam  | wgEncodeBroadHistoneDnd41H3k04me2AlnRep1.bam |
| 7  | H3k04me3 | H3k04me3.bam  | wgEncodeBroadHistoneDnd41H3k04me3AlnRep1.bam |
| 8  | H3k79me2 | H3k79me2.bam  | wgEncodeBroadHistoneDnd41H3k79me2AlnRep1.bam |
| 9  | H3k09ac  | H3k09ac.bam   | wgEncodeBroadHistoneDnd41H3k09acAlnRep1.bam  |
| 10 | H3k09me3 | H3k09me3.bam  | wgEncodeBroadHistoneDnd41H3k09me3AlnRep1.bam |
  
Файл cellmarkfiletable.txt
---
![image](https://user-images.githubusercontent.com/23341597/160261156-c20d8696-e61f-476c-a648-97d416feced2.png)
  
Отчет ChromHMM
---
Отчет лежит в директории `report`.  
1. Overlap  
![image](https://user-images.githubusercontent.com/23341597/160261243-b420da83-af01-482b-937d-cba1089e9591.png)  
Этот график показывает общую статистику по состояним. В глаза бросается, что:
- Чаще всего в геноме встречается состояние `9`, остальные состояния при этом встречаются довольно редко.
- Состояние `1` содержит большое количество CpG островков, значит, оно может попадать на активные промотеры. 
- Состояния `8`, `9`, `10` ассоциированы с ядерной ламиной, значит, могут являться репрессированным гетерохроматином.

2. Emissions
![image](https://user-images.githubusercontent.com/23341597/160261252-6dacec16-4d34-4c56-b06a-d5ca755fc8be.png)  


3. RefSeqTSS neighborhood
![image](https://user-images.githubusercontent.com/23341597/160261297-2ca14065-b075-4b24-91c1-17ada542b6e0.png)

4. RefSeqTES neighborhood
![image](https://user-images.githubusercontent.com/23341597/160261304-16194c9e-ab51-4ba6-87bc-cfc100a45beb.png)

5. Transitions
![image](https://user-images.githubusercontent.com/23341597/160261313-79e790db-dd8d-474c-8b39-eea32a9917ce.png)


Эпигенетических типы
---
![image](https://user-images.githubusercontent.com/23341597/160299594-083492b4-19d9-4a2e-92d9-98c9e057c820.png)
| Состояние | Эпигенетический тип         | Комментарий                                                                                                                                                                  |
|-----------|-----------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|         1 | Promoter                    | **Активный промотор.** Сильный сигнал на всех метках, кроме `H3k36me3`, `H3k09me3`, `H3k27me3`. Содержит большое количество CpG островков.                                   |
|         2 | Heterochromatin / enhancer  | **Межгенное пространство, либо слабый энхансер.** Сильный сигнал на `H3k04me1`, `H3k27ac`, слабее на `H2k09ac`, `H3k04me2`, `H2az`. Ассоциирован с ламиной, но слабо.        |
|         3 | Enhancer                    | **Энхансер.** Сильный сигнал на `H3k04me1`. Ассоциирован с ламиной, но слабо.                                                                                                |
|         4 | Transcribed gene / enhancer | **Транскрибируемый участок в конце активного гена.** Самый сильный сигнал на `H3k04me1`, `H3k04me2` и `H3k79me3`. Ассоциирован с TES, экзоном, активным геном и немного TSS. |
|         5 | Transcribed gene            | **Транскрибируемый участок в активном гене.** Есть сигнал на `H3k27me2`. Ассоциирован с активным геном.                                                                      |
|         6 | Transcribed gene            | **Транскрибируемый участок в активном гене.** Есть сигнал на `H3k27me2`, `H3k36me3`. Ассоциирован с TES, экзоном и активным геном.                                           |
|         7 | Exon                        | **Экзон в активном гене.** Есть сигнал на `H3k36me3`. Ассоциирован с TES, экзоном и активным геном.                                                                          |
|         8 | Repressed heterochromatin   | **Репрессированный гетерохроматин.** Есть сигнал на `H3k09me3`. Ассоциирован с ламиной.                                                                                      |
|         9 | Repressed heterochromatin   | **Репрессированный гетерохроматин.** Нет сигналов на метках. Ассоциирован с ламиной.                                                                                         |
|        10 | Repressed heterochromatin   | **Репрессированный гетерохроматин.** Есть сигнал на `H3k27me3`. Ассоциирован с ламиной.                                                                                      |
