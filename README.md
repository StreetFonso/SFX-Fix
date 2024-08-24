# SFX-Fix
Correções e adições nos índices SFX do GTA San Andreas.
Esta modificação praticamente nada faz no jogo. Ela serve mais para outros mods que podem mudar os id's originais dos sons do jogo, como VehFuncs e FLA.
Para instalá-la, basta botar no Modloader.
Ainda estou estudando para mexer nas falas dos NPC's. Nesta primeira versão, somente mexi no GENRL, e foi o seguinte:
- Corrigidos os "enginesounds" de carro/caminhão 15, 14; 56, 55; 91, 90; 97, 96 e 123, 122;
- Corrigidos os "enginesounds" da Faggio para que funcionem com veículos adicionados que usem seus sons;
- Adicionados os "enginesounds" da PCJ-600 do VCS nos 23,22;
- Adicionados cinco novas buzinas (id's 13 à 18), porém ainda não sei como fazer funcionar um id maior que "9".

Assim, os seguintes "enginesounds" ficam disponíveis:
- 15, 14; 43, 42; 50, 49; 56, 55; 73, 72; 91, 90; 97, 96; 117, 116 e 123, 122 para carros/caminhões;
- 23, 22 para motos;
- 20 e 24 para barcos;
- 13 para helicópteros;
- 9 para avião (esse tem 4 slots, sendo os dois primeiros idênticos ao 54);
- 111, 110 para carro RC.

O que descobri sobre o índice dos arquivos de áudio extraídos com o Alci's SAAT?

No exemplo abaixo extraído do arquivo "GENRL/sfx_import.ini":

- [Bank_008]
- num_sounds = 2
- sound_001.filename = Bank_008\sound_001.wav
- sound_001.sample_rate = 18000
- sound_001.unknown_16 = 800
- sound_001.unknown_32 = 0
- sound_002.filename = Bank_008\sound_002.wav
- sound_002.sample_rate = 18000
- sound_002.unknown_16 = 400
- sound_002.unknown_32 = 0

O "sound_00#.unknown_32 = 0" é a posição da amostra que inicia o looping, pois o jogo executa o som no modo "ABCBCBCBC...", sendo "A" a posição inicial, "B" intermediária/início do looping e "C" final.

Se não há "sound_00#.unknown_32" no índice, o jogo irá iniciar o looping no infinito, ou seja, não fará o looping e ficará mudo após o fim do som. Normalmente não há para o som do motor desacelerando.

Se "sound_00#.unknown_32" é "0", então o jogo fará o looping com o som inteiro, repetindo do início ao fim.

Para descobrir a posição da amostra, é preciso importar o som num editor de áudio como o Audacity, selecionar até a posição desejada, criar uma nova faixa mono com a mesma freqüência da original, colar o pedaço do tamanho da posição da amostra e alterar a freqüência para 44100Hz. Nisso, o tamanho será reduzido, consequentemente deixando o som acelerado, pois a freqüência aumentou, mas o que interessa é que o novo tamanho é a nova posição da amostra. Acho que essa conversão é uma regra de três composta inversamente proporcional, mas ainda não consegui expressá-la matematicamente.

O "sound_00#.unknown_16" desconfio fortemente que é a posição da amostra inicial, o "A" do exemplo acima.
Para os tipos car, bike, quad e m_truck, o jogo usa dois bancos de som, sendo o primeiro com três (aceleração, alta rotação e desaceleração) e o segundo com dois slots (ponto morto e debriar).

Para os tipos boat, heli, plane e bmx o jogo usa um banco de som com dois slots (alta rotação e ponto morto).

Para um carro RC, o jogo usa dois bancos de som, sendo o primeiro com três slots (aceleração, alta rotação e desaceleração) e o segundo com um slot (debriar).

Não testei para os tipos trailer e train.

A diferença entre o id do "enginesounds" e o "Bank_###" é "6". Por exemplo, o "Bank_008" corresponde ao "enginesounds" "14".

Abaixo, exemplos de configuração para o "gtasa_vehicleAudioSettings.cfg" do FLA (ignorem a formatação, pois copiei direto da planilha do LibreOffice).

Os mais diferentes são os do Monster's, Walton, Mower, NRG-500, RC Bandit, barcos e helicópteros.

- cargobob	4	13	-1	0	0.7	1	-1	1	0	0	3	0	13	0
- leviathn	4	13	-1	0	0.7	1	-1	1	0	0	3	0	13	0
- mower	0	15	14	2	0.9	1	1	0.943874	-1	0	2	0	37	0
- launch	3	20	20	0	0.7	1	-1	1	-1	0	13	3	19	0
- marquis	3	20	20	0	0.7	1	13	1	-1	0	3	0	19	0
- reefer	3	20	20	2	0.85	1	-1	1	-1	0	3	0	19	0
- tropic	3	20	20	2	0.85	1	-1	1	-1	0	9	0	19	0
- nrg500	1	23	22	2	0.65	1	6	1.18921	-1	0	5	0	29	0
- jetmax	3	24	24	1	0.85	1	-1	1	-1	0	3	0	19	0
- speeder	3	24	24	0	0.7	1	-1	1	-1	0	3	0	19	0
- squalo	3	24	24	0	0.7	1	-1	1	-1	0	3	0	19	0
- burrito	0	43	42	0	0.78	1	7	1.12246	4	0	6	0	11	0
- packer	0	43	42	0	0.78	1	9	1	3	0	3	0	6	6
- towtruck	0	43	42	0	0.7	1	4	1	4	0	3	0	6	0
- utility	0	43	42	0	0.65	1	7	1.12246	4	0	2	0	11	0
- rumpo	0	50	49	0	0.78	1	1	0.840896	4	0	1	0	11	0
- newsvan	0	50	49	0	0.7	1	4	1.05946	4	0	11	0	11	0
- pony	0	50	49	0	0.78	1	2	1.25992	4	0	1	0	11	0
- topfun	0	50	49	0	0.85	1	2	1.05946	4	0	1	0	11	0
- duneride	0	50	49	0	0.7	1.18921	4	0.890899	3	0	9	0	0	0
- walton	0	56	55	0	0.65	1	2	0.943874	4	0	2	0	15	0
- elegy	0	73	72	0	0.85	1	3	1.12246	2	2	8	0	1	0
- euros	0	73	72	0	0.85	1	5	1.25992	2	0	9	0	31	0
- jester	0	73	72	1	0.9	1	3	1.12246	2	2	8	0	31	0
- sultan	0	73	72	0	1	1	7	1.18921	2	2	6	0	45	0
- uranus	0	73	72	0	0.85	1	8	1.05946	2	2	3	0	31	0
- monster	0	91	90	0	0.9	1	9	1.05946	2	0	7	0	24	6
- monstera	0	91	90	1	0.9	1.18921	9	1.05946	2	0	3	0	24	6
- monsterb	0	91	90	1	0.9	1.18921	9	1.12246	2	0	7	0	24	6
- trash	0	97	96	0	0.7	1	5	0.890899	3	0	3	0	8	0
- barracks	0	97	96	0	0.7	1	9	0.943874	3	0	13	-1	6	0
- benson	0	97	96	0	0.65	1.33484	2	0.943874	3	0	2	0	11	3
- flatbed	0	97	96	0	0.7	1	9	0.943874	3	0	3	0	6	0
- yankee	0	97	96	0	0.7	1	4	0.943874	3	0	2	0	11	0
- rcbandit	9	111	110	0	0.7	1	-1	1	-1	0	13	1	-1	0
- stratum	0	117	116	0	0.78	1	3	1.05946	2	2	4	0	4	0
- regina	0	117	116	0	0.65	1	7	1.18921	2	0	9	0	4	0
- romero	0	117	116	0	0.9	1	5	1.12246	4	0	13	0	23	0
- huntley	0	117	116	0	0.78	1	7	1	2	0	11	0	0	0
- bravura	0	123	122	0	0.7	1	2	1.18921	2	0	5	0	1	0
- cadrona	0	123	122	0	0.78	1	8	1	2	0	4	0	1	0
- solair	0	123	122	0	0.78	1	3	1.12246	2	0	11	0	4	0
- virgo	0	123	122	0	0.7	1	3	0.943874	2	0	4	0	1	0
- #Skate Mod Remake: renomear "Bank_116" do mod para "Bank_008".
- sktbd	2	14	14	2	0.7	1	-1	1	-1	0	13	1	-1	0
