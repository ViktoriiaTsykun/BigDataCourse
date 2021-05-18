Завдання 3.(8 балів)
====================

Зчитати WEB сторінку з сайту https://www.formula1.com/en/drivers.html

Необхідно створити data.frame «formula1» з наступними даними: Biography, Team, Country, Podiums, Points, Grands Prix entered, World Championships, Highest race finish, Highest grid position, Date of birth, Place of birth.

```r
library(rvest)
file <- read_html("https://www.formula1.com/en/drivers.html")
drivers_links <- html_attr(html_nodes(file,'.listing-item--link'), 'href')
info <- data.frame(matrix(ncol = 11, nrow = 0))
for (link in drivers_links) {
  driver <- read_html(paste("https://www.formula1.com", link, sep=""))
  biography <- html_text(html_nodes(driver, "div.text:nth-of-type(n+3) p"))
  team <- html_text(html_nodes(driver, ".stat-list tr:contains('Team') td"))
  country <- html_text(html_nodes(driver, ".stat-list tr:contains('Country') td"))
  podiums <- html_text(html_nodes(driver, ".stat-list tr:contains('Podiums') td"))
  points <- html_text(html_nodes(driver, ".stat-list tr:contains('Points') td"))
  grandPrix <- html_text(html_nodes(driver, ".stat-list tr:contains('Grands Prix entered') td"))
  worldChamp <- html_text(html_nodes(driver, ".stat-list tr:contains('World Championships') td"))
  highestRace <- html_text(html_nodes(driver, ".stat-list tr:contains('Highest race finish') td"))
  highestGrid <- html_text(html_nodes(driver, ".stat-list tr:contains('Highest grid position') td"))
  dob <- html_text(html_nodes(driver, ".stat-list tr:contains('Date of birth') td"))
  pob <- html_text(html_nodes(driver, ".stat-list tr:contains('Place of birth') td"))
  driverInfo <- c(paste(biography, collapse = ' '), team, country, podiums, points, grandPrix, worldChamp, highestRace, highestGrid, dob, pob)
  info[nrow(info) + 1, ] <- driverInfo
}
colnames(info) <- c("Biography", "Team", "Country", "Podiums", "Points", "Grand Prix", "World championships", "Highest race finish", "Highest grid position", "Date of birth", "Place of birth")
```


1. Виведіть гонщиків перші 10 гонщиків дата фрейму.

```r
head(info, n=10)
```
```
                                                                                                                                       Biography
1         ‘Still I Rise’ – these are the words emblazoned across the back of Lewis Hamilton’s helmet and tattooed across his shoulders, and ever since annihilating expectations with one of the greatest rookie performances in F1 history in 2007, that’s literally all he’s done: risen to the top of the all-time pole positions list ahead of his hero Ayrton Senna, surged into first place in the wins column surpassing the inimitable Michael Schumacher, and then matched the legendary German’s seven world titles. \nIs he the G.O.A.T? Few would deny that he’s in the conversation – and what’s more he’s got there his way, twinning his relentless speed with a refusal to conform to stereotypes for how a racing driver should think, dress or behave. Respect is hard earned in F1, but Hamilton – now Sir Lewis Hamilton to be precise – has it from every one of his peers. Why? Because they know that whatever the track, whatever the conditions, whatever the situation, when his visor goes down and the lights go out, it’s Hammertime.
2                                                                                                                                                                                                                                                                              \nVerstappen’s no-holds-barred attitude and hard defending have sometimes landed him in hot water with his peers and paymasters. But the mistakes that initially marred his potential have given way to maturity, while the bravado and energy that make him a blockbuster talent have remained – and the victories have kept on coming. The son of former F1 driver Jos Verstappen and super-quick karting Mum Sophie Kumpen, racing runs through his genes. Despite moving out of Dad’s house to live in Monaco, Verstappen remains close to his family, and though he’s not afraid to speak his mind, he can still be surprisingly shy.  The expectations for the next generation’s leading light are sky high – but with Verstappen there’s a feeling that the sky’s the limit.
3                                         \nBottas blossomed at the Silver Arrows in 2017, unleashing his pace to clock up personal pole positions and victories as well as a team championship for the famous Mercedes marque alongside Lewis Hamilton. He even tied with Hamilton and Sebastian Vettel with 13 podiums. For a shy guy, it brought a confidence boost and a new swagger – albeit in a very demur Finnish fashion. He would need all that confidence in 2018 – a season Bottas described as his worst in F1, as he took zero wins to Hamilton’s 11. That, though, was a reflection more of his team mate’s brilliance thank of any shortcomings on his own part. Bottas stepped it up a level in 2019, four victories securing a convincing second in the championship behind Hamilton, but that dropped to two wins to his team mate's 11 in 2020. Now he must dig even deeper if he’s to regularly beat the man on the other side of the garage - and fend off the Red Bulls and Ferraris - and drive home as the fourth Finnish world champion.
4                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  \nAn exciting talent on track, away from it Norris brims with a modest charm and an artistic side sees him design and paint his own race gear as a hobby. The focus for the future is allying artistry and ambition on track as McLaren rely on the promise of youth to take them back to the top. Norris hopes the downforce will be with him…
5  \nStepping up to F1 in 2018, Leclerc showed flashes of ballistic pace on Saturdays and racing brilliance on Sundays, dragging his Sauber beyond its limits – and earning himself a money-can’t-buy race seat at Ferrari for 2019, stepping into the shoes of the Scuderia’s last world champion, Kimi Raikkonen.  There he immediately put the cat among the proverbial pigeons, unafraid to go wheel-to-wheel with established number one, Sebastian Vettel. A maiden F1 victory at Spa was followed by another a week later on Ferrari’s hallowed home turf of Monza. The tifosi had found another new hero – who then became the first man to out-score Vettel over a season with the Scuderia, a feat he repeated in crushing fashion the following year. Out of the car, Leclerc is modest and thoughtful - but then he is on his own very personal mission. This exciting young talent is racing for his late father Herve and his friend and mentor Jules Bianchi, the F1 driver who died in 2015.  On the evidence so far, he is doing them both proud.
6                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          \nA proud countryman, the Guadalajara gunslinger has amassed more points than any other Mexican in the history of F1. In Sakhir 2020 he also matched hero and compatriot Pedro Rodriguez by taking the chequered flag in first – a performance that landed him a shot at the title with Red Bull. More victories may not be assured, especially with Max Verstappen as team mate. But Perez working hard and racing with his heart are.
7                                                                                                                                                                                                                                                                                                                                                        \nA regular podium-finisher, Ricciardo has christened the steps around the world with a dousing of Aussie culture – the ‘Shoey’ – as he quaffed champagne from a soggy racing boot. Yes it’s goofy, but the trademark celebration illustrates why he is loved for his sense of humour but never underestimated on track.  His career’s next move to Renault’s works team brought fresh challenges for the Perth pilot, but failed to deliver his dream of following Jack Brabham and Alan Jones as the next world champion from Down Under. And in 2021 he hopes a new chapter with the Mercedes-powered McLaren team might just change that. But whatever happens, Ricciardo is sure to keep on smiling.
8                                                                                                                                                                                                                                           \nBut the Spaniard is intelligent as well as instinctive, thinking his way through a race and into the points. This calm temperament follows him off track where he remains unfazed by the pressures of forging a Grand Prix career with a famous name.  Sainz is the son of double World Rally champion, also his namesake, and has brought some of Dad’s driving skills to the F1 circuit – junior loves a delicious dose of drift for one.  After following in his famous father’s tyre tracks, Sainz has had big racing boots to fill – first at McLaren where he replaced his childhood hero Fernando Alonso, and now at Ferrari, in the seat formerly owned by Sebastian Vettel. It is never easy living in the shadow of sporting giants, but Sainz has shown the drive and disposition to deal with it. Vamos!
9                                                                                                                                                                                                                                    \nThat opportunity led to a full-time seat the following year with Force India, where his wheel-to-wheel duels with highly-rated team mate Sergio Perez quickly marked him out as a rising star. But when Lawrence Stroll, father of racer Lance, stepped in midway through 2018 to secure the squad’s financial future, the writing was on the wall for Ocon, who was moved aside at the end of the year to allow Stroll Jnr to join from Williams. Ocon bided his time, though, and after a year on the sidelines as Mercedes’ reserve driver, he found his way back into a race seat with Renault in 2020. Nothing in Ocon’s motorsport career has come easy – but if Ocon has managed to return to the F1 grid, it’s through a combination of self-belief, determination and a talent that’s up there with the very best.
10                                                                                                                                                                                                                                                                           \nUnfortunately that promise only appeared in flashes – and he quickly suffered from unfavourable comparisons with superstar team mate Max Verstappen. So much so that after the summer break, he was sent back to Toro Rosso, with another young up-and-comer – Alex Albon – being given a shot in the ‘senior’ Red Bull seat. But Gasly bounced back, as only Gasly can. In the season’s remaining nine races he scored almost as many points as team mate Kvyat managed over the entire year – and secured his best-ever race result with P2 in Brazil. That trajectory continued in 2020, peaking with an emotional maiden win at the renamed AlphaTauri team’s home race in Italy. The question now is can he maintain momentum and earn himself another shot at the F1 bigtime…
              Team        Country Podiums Points Grand Prix World championships Highest race finish Highest grid position Date of birth
1         Mercedes United Kingdom     169   3872        270                   7             1 (x98)                     1    07/01/1985
2  Red Bull Racing    Netherlands      46   1242        123                 N/A             1 (x11)                     1    30/09/1997
3         Mercedes        Finland      59   1559        161                 N/A              1 (x9)                     1    28/08/1989
4          McLaren United Kingdom       2    187         42                 N/A              3 (x2)                     3    13/11/1999
5          Ferrari         Monaco      12    441         63                 N/A              1 (x2)                     1    16/10/1997
6  Red Bull Racing         Mexico      10    738        197                 N/A              1 (x1)                     2    26/01/1990
7          McLaren      Australia      31   1183        192                 N/A              1 (x7)                     1    01/07/1989
8          Ferrari          Spain       2    392        123                 N/A              2 (x1)                     3    01/09/1994
9           Alpine         France       1    208         71                 N/A              2 (x1)                     3    17/09/1996
10      AlphaTauri         France       2    207         68                 N/A              1 (x1)                     4    07/02/1996
        Place of birth
1   Stevenage, England
2     Hasselt, Belgium
3     Nastola, Finland
4     Bristol, England
5  Monte Carlo, Monaco
6  Guadalajara, Mexico
7     Perth, Australia
8        Madrid, Spain
9     Evreux, Normandy
10       Rouen, France
```

2. Виведіть всх гонщиків із США.

```r
info[info$Country == "USA", "Team"]
```
```
character(0)
```

3. Скільки гонщиків брали участь у «Чемпіонаті світу».

```r
nrow(info[info["World championships"] != 'N/A', ])
```
```
[1] 4
```
