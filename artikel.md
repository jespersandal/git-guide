Min guide til Git for begyndere

Af Jesper Stein Sandal
Softwareudvikling er ét af de få fag, hvor man har en tidsmaskine i værktøjskassen. Tømreren måler altid to gange, for når først brættet er savet, så er der ingen vej tilbage. Men det er der i programmering. Vi kan skrue tiden tilbage til før vi tilføjede de kodelinjer, der fik det hele til at eksplodere i exceptions.

Men programmørens tidsmaskine er næsten mere kompliceret end den fysik, der beskriver, hvorfor tidsmaskiner ikke kan lade sig gøre. Og alligevel er der ingen vej uden om: Versionsstyring er uundværligt.

Uden versionsstyring er det noget nær umuligt at arbejde sammen om et softwareprojekt, og uden versionsstyring ender man alligevel med at skulle holde styr på forskellige versioner af sin kode, når man prøver at omskrive en funktion.

Derfor er det svært at komme uden om Git, der er dén udgave af versionsstyring, som også har lagt navn til kodedelingssitet Github. Men Git er på ingen måde en begyndervenlig størrelse, og det er derfor, jeg nu prøver at skrive denne guide i takt med mit tredje forsøg på at tæmme Git-monstret.

Mit første forsøg strandede på, at hvis man på hjemmesiden for Git-projektet forsøger at læse [vejledningen](https://git-scm.com/book/en/v2/Getting-Started-About-Version-Control), så vil man opdage, at den først og fremmest forklarer i pinagtige detaljer, hvordan Git virker - ikke hvordan man bruger Git. 

I det hele taget finder man flere [vejledninger](http://www.vogella.com/tutorials/Git/article.html), der tager udgangspunkt i, hvordan Git arbejder med at versionere din kode, i stedet for at tage udgangspunkt i dine arbejdsgange.

[box]
###Git-begreber:
**Repository:** Et repository er det sted, du lagrer dit projekt. Det kan være en lokal mappe eller en ekstern server eller tjeneste som Github. 

**Add:** Tilføjer filer eller ændringer til det næste commit.

**Commit:** Et commit er som et save game i et computerspil. Når du har nået et punkt, hvor det er en god idé at lave et save game, du kan vende tilbage til, så laver du et commit. Det gemmer de ændringer, du har lavet indtil videre.

**Push:** Når de ændringer, du har samlet i et commit, skal sendes til dit repository, skal du lave et push.

**Branch:** En branch er noget du bruger, når du har brug for at arbejde på en kopi af projektet og ikke vil gemme dine ændringer direkte i 'master'-kopien. Du skifter til en branch med **checkout**.

**Pull:** Når du skal hente og integrere de ændringer i projektet, som ligger i repository'et, så laver du et pull.

**Merge:** Når Git skal samle ændringer, bliver dit commit merget. Det kan give en konflikt, hvis to har ændret de samme steder i en fil.
[/box]

Det er nemlig det svære ved Git. Det er et værktøj til at holde styr på de filer, der bruges af din applikation, og Git gør meget lidt af sig selv. Det er dig, der skal fortælle Git, hvad der skal være en del af din applikation.

Et godt råd er altid at antage, at der er et trin mere, end du intuitivt ville tro. At tilføje en fil til dit projekt er ikke det samme som at gemme filen i projektet.

Et andet godt råd er, at du ikke bør antage, at et begreb eller en kommando i Git gør dét, du intuitivt ville tro ud fra navnet. 

Vær også forberedt på mærkværdige overraskelser - som eksempelvis at ryge ind i en Vim-lignende editor, hvis du glemmer at skrive en commit-besked fra kommandolinjen. Og en Vi-lignende editor er ikke et rart sted at være (for at komme ud igen er du nødt til at trykke på escape og skrive **:q** og trykke enter. Ja, kolonet skal indtastes, hvorfor fortaber sig i fortidens Unix-tåger).

Du skal også hele tiden være opmærksom på, hvor du er henne. Git arbejder med en træ-metafor med grene, så du skal sikre dig, at du arbejder på den rigtige gren. Grene kan så vokse sammen med stammen igen, så det er måske mere en jernbane-metafor. Er du i tvivl, så spørg Git, hvor du er lige nu med kommandoen **git status**, som fortæller dig, hvilken **branch** der er aktiv.

Lad os begynde ved begyndelsen. Først skal Git naturligvis [downloades](https://git-scm.com/downloads) og installeres. Den del er forholdsvis nem. Git til Windows inkluderer sin egen udgave af Bash, men Git kan også bruges fra Powershell. Installationsprogrammet henviser ganske vist kun til den klassiske kommandoprompt cmd.exe, men Powershell virker også, hvis man installerer Git med standardindstillingerne.

Det næste trin er at vælge et **repository**. Det er det sted, du lagrer dit projekt. Det kan være en lokal mappe på din pc, eller det kan være på en server hos eksempelvis Github. Det sidste er lidt mere besværligt, men da det også er det mest nyttige, fordi det er den måde, man vil arbejde flere på samme projekt eller på forskellige computere. Så jeg vil bruge et Github-repository i min gennemgang.

I første omgang er det lettest at [oprette et nyt repository på Githubs hjemmeside](https://help.github.com/articles/creating-a-new-repository/). I det hele taget vil jeg anbefale at bruge Githubs grænseflade til alt, hvad der hedder administration af dit repository, da det er let at miste overblikket og lave fejl i kommandolinjen. Det er selvfølgelig en smagssag.

Når du klikker dig ind i dit nye repository på Github, så er der [en stor grøn knap](https://help.github.com/articles/cloning-a-repository/) med teksten 'Clone or download'. Klikker du på den, får du mulighed for at kopiere en URL, som peger på dit repository. Denne URL skal du bruge til første trin i at få lavet en lokal klon af filerne i repository'et.

Ved kommandoprompten skal du først gå ind i den overordnede mappe, hvor du vil opbevare filerne til projektet. Derefter skal du bruge kommandoen **>git clone** efterfulgt af den URL, du kopierede fra Github.

Git henter nu filerne fra Github og opretter en ny mappe med samme navn som dit repository. Du kan nu gå ind i mappen og arbejde på de filer, du har downloadet, og du kan også tilføje nye filer til mappen.

Intet af det, du laver i din lokale mappe, påvirker på nuværende tidspunkt dét, der ligger på Github.

###Tilføje filer og ændringer med Add og Commit
Med Git skal du i første omgang kun koncentrere dig om at holde styr på de ændringer, du laver lokalt på projektet. For at se, hvilke ændringer du har lavet på din lokale udgave, kan du bruge kommandoen **>git status**. Den fortæller dig, hvilke filer der er ændret eller tilføjet i mappen i den branch, du arbejder på lige nu.

Når du ændrer en fil, vil du med status-kommandoen se, at filen står som 'modified' med rød skrift. På nuværende tidspunkt har du ikke bedt Git om at gemme ændringerne.

Første trin i at gøre dette er kommandoen **>git add** efterfulgt af filnavnet. Hvis du tilføjer mange filer samtidig, så kan du bruge kommandoen efterfulgt af et punktum. Her skal man blot være forsigtig, hvis der ligger filer i mappen, som ikke skal med i projektet.

Selvom du har tilføjet en fil med add-kommandoen, så er den stadig ikke rigtigt tilføjet projektet. Det bliver den først, når du laver et 'commit'.

Et commit er som et save game i et computerspil. Når du har nået et punkt, hvor det er en god idé at lave et save game, du kan vende tilbage til, så laver du et commit. Det gemmer de ændringer, du har lavet indtil videre.

Et commit samler de add-tilføjelser, du har lavet. Når du ændrer en fil, så kan du tilføje den til næste commit med add-kommandoen. Så længe du ikke har lavet dit commit, bliver alle adds tilføjet til det næste commit, du laver.

Du laver et commit med kommandoen **>git commit -m ""**, hvor citationstegnene indeholder din korte beskrivelse af, hvad det er, du har ændret med det pågældende commit. Hvis du udelader beskeden, sender Git dig ind i Vi-editoren, hvor du kan skrive en længere besked.

###Push og Pull
På nuværende tidspunkt er dit commit og dine ændringer stadig kun lokale. Hvis du kun arbejder lokalt med dit projekt, så er der sådan set ikke mere til Git. Men hvis du arbejder med Github eller et andet eksternt repository, så er der flere trin.

For at få din kode op på Github, bruger du kommandoen **>git push**. Den sender dit seneste commit til det sted, du har hentet filerne fra, så med Github vil det være på dit Github repository.

Et commit er altid inden for den branch, du arbejder i. Hvis du pusher et commit i en anden branch end master, så bliver den ikke automatisk slået sammen med master-branchen.

Og hvis du ikke har administrator-rettigheder til det pågældende repository, så skal du lave en 'pull request'. Et pull henter ændringer til en branch og forsøger at merge dem. Når du laver en pull request, beder du også administratoren eller dine kolleger om at se dine ændringer igennem og merge dem med jeres master-branch.

Du skal også lave et pull for at hente opdateringer fra repository'et. Det gør du med kommandoen **>git pull**, som så forsøger at hente ændringer og slå dem sammen med din lokale version i et merge.

###Merge
Den sværeste disciplin i versionsstyring er at samle ændringer. Git er ret god til at slå ændringerne sammen, så længe der er tale om tilføjelser eller sletning.

Hvis to personer har ændret i de samme linjer, så bliver det lidt vanskeligere. Git kan ikke gennemføre et merge, før der er taget stilling til alle konflikter i filerne.

Der findes værktøjer til at gøre dette eftersyn af konflikter lidt mere overskueligt, men man kan nå langt blot med Githubs webbaserede grænseflade.

Når der er en konflikt i en fil, vil Git markere de pågældende linjer, så man kan også gå ind og rette i sine filer og lave et nyt forsøg på et commit. Git kan kun se, at der er forskel mellem to versioner, så det er op til dig at beslutte, hvilke ændringer der skal benyttes.

###Branches og merges
Inden vi slutter er det på sin plads at tage en hurtig snak om *branches*. En branch er en forgrening på versionstræet. Det er en kopi af din originale *master branch*, hvor alle ændringer, du laver, kun påvirker kopien, indtil du laver et *merge*, der fletter din branch sammen med master.

Fordelen ved en branch er, at du kan arbejde på en ny funktion eller omskrive en eksisterende funktion med mulighed for at teste alt på din kopi, uden det ødelægger den udgave, du ved virker. Derfor har den [normale praksis](https://git-scm.com/book/en/v2/Git-Branching-Branching-Workflows) været at have en ['develop' branch](http://nvie.com/posts/a-successful-git-branching-model/), som man laver alle ændringer på. 

I praksis udvikler det sig imidlertid til, at man laver yderligere branches fra sin develop-branch, og det kan gøre strukturen unødvendigt kompliceret, [mener kritikerne](https://barro.github.io/2016/02/a-succesful-git-branching-model-considered-harmful/) af denne flow-model. Problemet er, at din master-branch ikke har nogen væsentlig funktion på denne måde. Derfor kan det give mening at droppe sin develop-branch og blot [forgrene direkte fra master-branch](http://scottchacon.com/2011/08/31/github-flow.html).

Det er velegnet, hvis man sidder på et projekt, hvor ændringer skal udrulles, når de er testet og klar. Til større projekter kan det klassiske git-flow være nødvendigt, men til mindre projekter er den simplere model fornuftig, hvis man blot sørger for at håndtere sine merges korrekt. Det vender vi tilbage til.

For at lave en branch skal man bruge kommandoen **>git branch** efterfulgt af navnet på den branch, man vil oprette. Du er på nuværende tidspunkt ikke inde i den nye branch. 

Du skifter til en branch med kommandoen **>git checkout** efterfulgt af navnet på den branch, du vil skifte til. Eller du kan oprette en branch og skifte til den i ét hug med kommandoen **>git checkout -b** efterfulgt af navnet på den nye branch.

For at slå to branches sammen, skal du først skifte til den branch, du vil merge til. Du skriver altså eksempelvis først **>git checkout master** for at skifte til master-branch. Dernæst kan du bruge kommandoen **>git merge** efterfulgt at den branch, du vil slå sammen med master.

Det kan være en god idé først at lave et merge fra master til den branch, du har arbejdet på. Så kan du løse eventuelle konflikter i denne branch, før du igen merger din branch med master.

###Arbejdsgangen
For at opsummere, så vil man første gang, man begynder på at redigere i et projekt, starte med **clone**. Men når du senere vil arbejde videre på projektet, så er det en god idé at starte med at lave et **pull** for at hente de seneste ændringer fra repository'et.

Derefter vil man lave **add**, hver gang man tilføjer filer eller er færdig med at redigere en fil. Når du er nået til et punkt, hvor en opgave er afsluttet, så vil det være en god idé at lave et **commit**.

Slut derefter af med at lave et **push** for at sende alle dine commits til repository'et.

Brug branches til større ændringer, men vær opmærksom på, at der er flere [måder at organisere brugen af branches](https://www.atlassian.com/git/tutorials/comparing-workflows) på med Git. Du skal også være mere opmærksom på, at alt bliver add'et og commit'ed i din branch, inden du laver et merge.

Versionsstyring giver som nævnt mulighed for at [gå tilbage](https://www.atlassian.com/git/tutorials/undoing-changes) til en [tidligere version](https://github.com/blog/2019-how-to-undo-almost-anything-with-git), hvis man får lavet for meget rod i det. Det er imidlertid noget, der kræver, at man holder tungen lige i munden, for det er let at komme til at lave et irreversibel ændring.

Den nemmeste måde er at bruge kommandoen **>git log** eller **>git reflog** for at få en oversigt over commits. Den sidste af de to giver en hashværdi, der kan bruges som reference og viser kun commits, man kan gå tilbage til.

Dernæst kan man bruge **>git checkout** efterfulgt af hashværdien på det commit, man ønsker at vende tilbage til, og eventuelt navnet på den pågældende fil.

Der findes andre måder at gå tilbage på, men checkout er den måde, der er sikrest for den enkelte udvikler.

Jeg har brugt Git under arbejdet med denne artikel, så den kan faktisk også [findes på Github](https://github.com/jespersandal/git-guide). Det er i sig selv en pointe, for versionsstyring kan også anvendes uden for programmering, hvis man eksempelvis er flere personer, som arbejder på en samling af dokumenter. Det kræver dog, at alle forfatterne er friske på at lære ikke bare en håndfuld kommandoer, men især en stringent arbejdsgang, som kræver lidt øvelse at mestre.