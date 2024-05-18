<!--yml
category: 未分类
date: 2024-05-18 14:26:52
-->

# TradeTech #1 : ça chauffe à haute fréquence – Sniper In Mahwah & friends

> 来源：[https://sniperinmahwah.wordpress.com/2013/04/21/tradetech-1-ca-chauffe-a-haute-frequence/#0001-01-01](https://sniperinmahwah.wordpress.com/2013/04/21/tradetech-1-ca-chauffe-a-haute-frequence/#0001-01-01)

*Back from London*, où plutôt que d’assister aux funérailles de Margaret Thatcher j’ai assisté à [TradeTech](http://www.wbresearch.com/tradetecheurope/Home.aspx), le salon annuel des marchés et des technologies financières qui s’est déroulé du 16 au 18 avril 2013. Difficile de résumer intégralement ces trois jours très denses en informations recueillies, je réserve le meilleur pour plus tard. En résumé, TradeTech ce sont trois jours de discussion à bâton rompu où plus de 150 personnes ont parlé devant quelques centaines d’autres (les discoureurs se transformant parfois en auditeurs et vice-versa), ce qui laissait peu de temps pour déambuler entre les stands des constructeurs de transmissions à micro-ondes, ceux des banques ou des marchés. Je ne parlerai ici que de la journée dédiée aux transactions à haute fréquence  (ou *hft *comme le murmuraient tout le monde entre deux stands) et le [programme](http://www.wbresearch.com/tradetecheurope/hft.aspx) de la journée s’avérait prometteur.

La journée fut pilotée par Dave Cliff, enseignant en sciences informatiques à Bristol (sa présence est due à son travail pour le projet [Foresight](http://www.bis.gov.uk/foresight/our-work/projects/current-projects/computer-trading/reports-and-publications), sur lequel je reviens plus loin). La session a débuté avec une intervention parfaite de Joe Saluzzi ([Themis Trading](http://www.themistrading.com)), l’une des rares voix à se faire entendre aux Etats-Unis sur les limites et les abus du *hft*. Saluzzi a en réalité repris les arguments développés avec son collègue Sal Arnuk dans [Broken Markets](http://www.brokenmarkets.com), leur ouvrage paru l’année précédente. Il y fut donc question de fragmentation des marchés (entre les *lit pools*, les ATFs, les MTFs, les *dark pools*, etc.), du fait que certains marchés (le NYSE par exemple) offrent à certains client la possibilité de voir le carnet d’ordres avant les autres, la question principale étant de savoir si le *hft* apporte réellement de la liquidité ou non aux marchés (une question qui reviendra tout au long de la journée). « *I’m not saying we should go back to the floor model, but when you had accountability it was different than now where you have a faceless computer-generalized system where no one really knows what’s going on anymore* », affirma Saluzzi (ce qu’affirmait déjà Thomas Petterfy en 2010 lorsqu’il disait que les marchés étaient devenus un « vrai bordel »).

Les arguments de Joe Saluzzi furent prolongés par l’intervention d’[Ari Burstein](http://www.ici.org/iciglobal/news/bios/ci.12_bio_burstein.global), qui livra un exposé parfaitement clair sur le fait que les « régulateurs doivent intervenir au niveau des structures de marché » afin de limiter les abus liés au *hft*, notamment en ce qui concerne le pourcentage important des ordres annulés (« *large amounts of small orders that ar being cancelled almost immediately in the second they are put in don’t necessarily help us get our large *orders* done* »), ce qui n’aboutit qu’à deux choses : créer davantage de bruit et rendre plus difficile le processus de formation du prix puisque la juste valeur des offres et des demandes est noyée dans le bruit créé par le hft (l’industrie du hft répondant à cela que les annulations des ordres ne sont en fait que des mises à jour des cotations). Burstein nota avec justesse que bien des firmes de *hft* n’ont pas forcément réellement le statut de *market makers* mais font le travail même des *markets makers* (message envoyé aux régulateurs). Pénaliser fortement les annulations serait, pour Burstein, un bon début. « *Regulators need to have access to accurate, timely and detailed informations. They need to have a smart reporting regime and the ability to analyse order books* » – le problème étant, pour les régulateurs, de disposer de l’infrastructure technique pour y arriver, ce qui n’est pas une mince affaire compte tenu du volume extrême des cotations réalisées chaque jour par les *hft*.

L’intervenant suivant, Larry Tabb (fondateur et dirigeant de l’indispensable [TabbForum](http://tabbforum.com)), une voix écoutée de l’industrie financière américaine, fut nettement plus mesuré quant aux régulations possibles visant le *hft*. Tout en reconnaissant que les *bad guys* doivent être éliminés du jeu, Tabb pense que les régulateurs ne savent pas vraiment ce qu’ils veulent faire (pas faux). « *The definitive issue is how you get machines to trade with other machines more fairly* » affirma Tabb. Tout ne serait donc qu’une question d’équité – l’idée que les régulateurs puissent restreindre la co-location pour freiner le temps de passage des ordres, ou qu’ils aient la possibilité de superviser les algorithmes (« *difficult and hard to enforce* », pas faux non plus) n’a pas vraiment de sens pour Larry Tabb. Il dégaina par ailleurs quelques chiffres pour montrer que les régulations canadiennes et italiennes concernant les *dark pools* n’ont mené qu’à un assèchement de la liquidité – « *Once you levy a tax, spreads widen, investors pay more dans turnover redues* », ce sur quoi plusieurs intervenants avouèrent plus tard être d’accord : lorsqu’une taxe est décidée, au final elle est comme facturée au client des firmes de *hft*, ce qui revient à pénaliser l’investisseur initial. Tabb pointa également quelque chose d’intéressant : les *markets makers* à haute fréquence ont pris la main en tant qu’intermédiaire en remplacement des banques, lesquelles ne veulent plus forcément prendre le risque qu’elles prenaient auparavant. « *That won’t change significantly unless banking rules change significantely. If there is no capital in the market, there needs to be intermediation* », une remarque toute de bon sens.

Après le café du matin ce fut autour de [Dave Cliff](http://www.cs.bris.ac.uk/~dc/) de prendre la parole pour faire le point sur le projet [Foresight](http://www.bis.gov.uk/foresight/our-work/projects/current-projects/computer-trading/reports-and-publications) dans lequel il fut largement impliqué. En quelques mots : Foresight, initié par le gouvernement anglais, fut un travail de longue haleine, mené pendant 12 ans, sur l’avenir des transactions électroniques dans les marchés financiers, un travail auquel ont participé plus de 150 chercheurs venus du monde entier et dont le rapport final de 180 pages, *The future of computer trading in financial markets: an international perspective*, fut publié en novembre 2012, après la publication de plus de 60 autres rapports intermédiaires (lecture intégrale indispensable pour qui s’intéresse à l’informatisation des marchés financiers). Je détaillerai les tenants et les aboutissants de Foresight plus tard, il suffit ici de savoir que le rapport final, et notamment les prospectives concernant la régulation des marchés financiers électroniques, suscita quelques vagues lors de sa parution, certains chercheurs ayant participé au projet ayant exprimés leurs désaccords avec les conclusions finales, celles-ci ne reflétant pas vraiment, selon eux, les conclusions auxquels certains étaient arrivés (en gros, le rapport final a évacué certaines mises en garde concernant les méfaits du *hft,* sans compter d’autres défauts pointés [ici](http://www.ft.com/intl/cms/s/0/6cf871d2-2f20-11e2-b8c5-00144feabdc0.html#axzz2QzaY4el6) par Stuart Baden Powell, de la Royal Bank of Canada).

Pour qui a suivi Foresight de près, la conférence de Dave Cliff s’annonçait prometteuse, et elle le fut (précisons par ailleurs que Cliff a développé des algorithmes de trading dans la continuité des travaux initiés par Vernon Smith ou ceux du Sante Fe Institute, dont je parle brièvement dans le chapitre 4 de *6*). Cliff commença par dire qu’il s’exprimait en son nom et non pas au nom de Foresight ou du gouvernement anglais (précision plutôt utile compte tenu de la suite de son propos), puis développa deux points principaux : la régulation du *hft* et la gestion du risque. Le point de vue de Cliff sur les régulations est sans appel : pour lui, les mesures qui sont envisagées par Mifid II (la Directive européenne concernant les marchés d’instruments financiers dans sa version 2) ne sont pas au niveau : « *The problem with most financial regulation and in particular Mifid II is that it has been done very badly because it is run by politicians* », Cliff enfonçant le clou en affirmant que l’article 17 de Mifid II n’est que « de la pâtée pour chien », ce qui provoqua quelques rires parmi la cinquantaine d’auditeurs de cette première journée de TradeTech.

Cliff est tout aussi circonspect à propos d’une proposition de Mifid II (les articles 17.2 et 17.3) qui consisterait à demander aux opérateurs de marchés d’expliquer aux régulateurs comment travaillent leurs algorithmes, un argument déjà utilisé par Larry Tabb et qui pointe à juste titre les difficultés pratiques – les algorithmes sont modifiés chaque jour ou presque – et juridiques de cette mesure – les algorithmes sont de l’ordre de la propriété privée. Dave Cliff est tout aussi circonspect en ce qui concerne le temps de détention minimale d’un titre, envisagé par Mifid II (qui serait de l’ordre de 500 millisecondes, une durée il est vrai plutôt arbitraire là où l’industrie pencherait plutôt pour 100 millisecondes, ce qui permettrait aux algorithmes de continuer à faire de l’arbitrage entre divers marchés). En revanche, ce qui inquiète Cliff sont les risques de connaître à nouveau – et dans peu de temps – un nouveau *flash crash* comme celui du 10 mai 2010 : « *We can expect something on the scale of the flash crash soon and it will not be a surprise* » – Joe Saluzzi opina vigoureusement de la tête. En évoquant la « normalisation de la déviance » (le fait que l’humain puisse empiler des mesures de précaution les unes au dessus des autres, ce qui les rend de moins en moins efficaces), le chercheur a mis en garde sur le fait que si les *markets makers* ne créent pas des coupes-feus au sein des plateformes, une catastrophe ne peut que se reproduire.

Je passe rapidement sur l’intervention suivante concernant les rapports possibles entre le risque nucléaire et le management du risque au sein des marchés financiers (Robin Bloomfield reprit les principaux arguments déjà avancés dans son étude pour le projet Foresight, [*Computer trading and systemic risk: a nuclear perspective*](http://www.bis.gov.uk/assets/foresight/docs/computer-trading/12-1059-dr26-computer-trading-and-systemic-risk-nuclear-perspective.pdf)) pour arriver au panel qui fit le plus parler de lui en cette première journée de TradeTech : *Developing an industry wide code of trading for HFT – dream or reality?* Se retrouvèrent autour de la table Joe Saluzzi, Benoît Lallemand de [Finance Watch](http://www.finance-watch.org), Thomas Preis, Niki Beattie et Manoj Narang, de [Tradeworx](http://www.tradeworx.com). Pour qui connaît les intervenants, le débat ne pouvait qu’être vif, et il le fut, Narang étant l’un des grandes défenseurs du *hft* aux Etats-Unis, l’une des rares voix à assumer l’agressivité des algorithmes de trading, une voix à l’opposé, donc, de la vision de Joe Saluzzi (les deux se connaissent bien pour avoir déjà débattu dans des émissions de télévisions américaines).

Après un début de discussion plutôt bon enfant, la tension est montée lorsque Saluzzi, soutenu par Finance Watch, s’est demandé pourquoi il reviendrait aux régulateurs de payer pour construire un système de surveillance destiné à repérer et sanctionner les abus des algorithmes travaillant à la milliseconde (rappelons que les régulateurs sont, en Europe, financés par les Etats, donc les citoyens, alors que la SEC aux Etats-Unis est financée par l’industrie financière elle-même, via un vote du Sénat qui définit le montant que cette industrie doit allouer à la SEC). Ce sur quoi Narang répondit qu’il voudrait bien qu’on lui montre des preuves de ces abus, ce qui souleva un frémissement dans la salle (compte tenu des travaux de [Nanex](http://www.nanex.net/flashcrash/ongoingresearch.html) et d’autres, il n’est pas bien compliqué de se rendre compte que parfois les algorithmes sont à la limite de la loi). Alors que Saluzzi accusa les algorithmes de scalper le marchés, Narang répondit que « *in a capitalist society, we should not be expecting equal outcomes… there will always be winners and losers. The winners will likely be the same high-frequency players as today. That’s how skill works* ». « *Algorithms are less susceptible to mischievous behaviour than humans as they don’t have families to feed* » ajouta Narang, droit dans ses bottes.

Je passe sur les discussions autour de la définition floue du *hft* (Narang ironisant que le fait que les régulateurs, au bout de cinq ans de travail, n’arrivent pas à donner une définition précise, Finance Watch répondant que Mifid II en propose une définition assez claire) pour arriver au moment où la tension monta d’un cran lorsque Finance Watch affirma que le *hft* ne fait qu’apporter de la liquidité supplémentaire là où il y en a suffisamment (sur les *blue chips*) alors que les petites et moyennes entreprises, celles qui ont réellement besoin de liquidité pour se développer via les marchés, n’intéressent pas le *hft,* lequel ne fournit donc pas la liquidité nécessaire au bon développement de l’économie. « *The notion that hft only provides to liquid stocks is absurd* » répondit Narang en haussant le ton, « *the reason illiquid stocks are illiquid is because there is not enough demande for those stocks* », ce qui énerva davantage Saluzzi qui argumenta alors sur le fait que les petites capitalisations se négocient à 10 *cents* près (*a dime*), ce que contesta vigoureusement Narang, lui-même renvoyé dans ses cordes par Nanex qui, depuis Chicago, dégaina des chiffres et s’empressa de mettre en ligne ces [preuves](http://www.nanex.net/aqck2/4164.html) sans appel.

A ce stade, la discussion devint un peu cacophonique, Dave Cliff essayant de faire revenir le calme pour que le panel puisse conclure en baissant le ton. «*I would rather people like you were not there, Manoj*» affirma un auditeur dans la salle, «*but I also believe in free markets, so I accept you right to do business*», d’autres prenant la défense des investisseurs au long terme (ce que ne sont pas les algorithmes du *hft*, qui liquident leur position en fin de journée). Les vives discussions de ce panel, également relatées [ici](http://www.bankingtech.com/81642/angry-tradetech-delegates-clash-over-hft/) par Banking Technology ou [là](http://blogs.lecho.be/fairtrade/2013/04/le-clash-sur-le-hft.html) par Jennifer Nille sur son blog Fair Trade, sont en fait monnaie courante lorsqu’il s’agit du *hft*, sans compter que les travaux académiques sur le lien entre le *hft* et la liquidité sont parfois contradictoires (cf. Foresight notamment). Il était intéressant de voir que, dans l’organisation même du panel, Narang était seul de son côté, séparé par une chaise vide des autres intervenants (tout un symbole). Reconnaissons au moins à Narang de venir assumer son discours devant un auditoire assez sceptique face à la radicalité des propos tenus par le patron de TradeWorx.

Je passe sur les interventions de l’après-midi, assez décousues suite à un changement de programme, ainsi que sur la mienne, qui clôtura cette journée assez mouvementée. J’ai ensuite eu l’occasion de parler de Michel Foucault et du «panoptique financier» avec un régulateur hollandais de l’AFM, Piebe Teeboom, de Nietzsche et de Toynbee avec un ingénieur français qui lance un hedge fund à partir du *data mining*, de sciences sociales avec le directeur d’[Automated Trader](http://www.automatedtrader.net), d’épistémologie avec le directeur d’une compagnie qui fabrique des réseaux de transmission à micro-ondes pour les marchés financiers, et de co-location avec un responsable technique de Nyse-Euronext. Je reviendrai bientôt sur les deux autres jours de TradeTech, où il fut notamment question des nouvelles technologies utilisées dans les marchés, dont de nouvelles puces électroniques qui vont doper les temps de calculs des algorithmes de *hft*. Une seule chose est certaine : le rythme des avancées technologiques n’est pas celui des régulateurs. Mifid II doit rentrer en vigueur en 2015 voire 2016\. D’ici là, nul doute que l’industrie des marchés financiers aura fait plus d’un pas supplémentaire pour aller encore plus vite, encore plus loin. Le *hft* a donc un boulevard devant lui pour aller de l’avant.

[![TradeTech](img/0259fc24d0dc8013d5f67baa381a835a.png)](https://sniperinmahwah.wordpress.com/wp-content/uploads/2013/04/tradetech1.jpg)