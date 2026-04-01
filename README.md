# MIST-4610-GroupProj-21482-G4
#Team Name:
---
21482 Group 4
---
Team Members
---
1. Firdows Abdulwahab
2. Dylan Klinghoffer
3. Girish Saravanan
4. Joseph Tapp
5. Munil Vaishnav
---
Database Scenario
---
The NFL Combine Database models the annual NFL Scouting Combine process, capturing the full pipeline from college prospect evaluation through to draft day selection. Each year, hundreds of college football players are invited to Indianapolis where they undergo standardized physical and cognitive drills,  with every result logged against the specific player, drill, and combine event. The database tracks each player's college affiliation, the position or positions they play, their participation and drill results at the combine, and ultimately the NFL team and draft round in which they were selected. This structure makes it possible to query insights such as positional performance averages, college program output, historical draft trends by team, and individual athlete profiles, supporting the needs of front office personnel, scouts, and analysts who rely on accurate combine data to make informed decisions.
Data Model
---

The NFL Combine Database is composed of ten entities whose relationships collectively model the full journey of a college football prospect through the scouting combine and into the NFL Draft.
At the center of the model is the Players entity, which stores each prospect's name, height, weight, and college affiliation. Every player is linked to a College, which records the school name, conference, state, and city. Since a player can play more than one position, a junction table called PlayerPosition sits between Players and Positions, creating a many-to-many relationship that allows a single player to be associated with multiple position codes and names, such as both Linebacker and Defensive End.

When a player attends the combine, their attendance is recorded in CombineParticipation, which links the player, their position at the time of the event, and the specific CombineEvent they attended. The CombineEvent entity stores the year, location, and start and end dates of each annual combine. From there, every individual drill result a player produces is stored in CombineResults, which connects each result back to the specific participation record and to the CombineDrills entity which defines the drill name, category such as Speed or Agility, and the unit of measurement used such as seconds or inches.
On the draft side, DraftPicks records each selection made by an NFL team, storing the draft year, round, overall pick number, and pick within the round. Each draft pick is linked to the Team that made the selection and optionally to the Players entity through a nullable foreign key, meaning that players who attended the combine but went undrafted are still fully represented in the database without requiring a corresponding draft pick record.

The database is specifically scoped to the combine evaluation and draft selection process, meaning it supports storage of player biographical and physical data, college and university information, positional data including multi-position players, combine event details, drill definitions and performance results, and draft pick records linked to both the selecting NFL team and the player chosen. It does not, however, support storage of data outside this scope such as post-draft career statistics, player contracts or salaries, injury or medical history, scouting evaluations and film grades, coaching staff information, player transactions or trades, roster and depth chart data, or players who did not attend the combine at all.

<img width="1138" height="833" alt="image" src="https://github.com/user-attachments/assets/9ff41f0a-b076-4dc4-95d8-ab7f933d4fda" />

Data Dictionary
---
<img width="784" height="523" alt="image" src="https://github.com/user-attachments/assets/22602953-7538-4fa6-aa42-c2c08da28b83" />
<img width="937" height="643" alt="image" src="https://github.com/user-attachments/assets/b2ac13e5-2951-4581-bd6c-69014760455f" />
<img width="755" height="378" alt="Screenshot 2026-03-31 at 11 05 11 AM" src="https://github.com/user-attachments/assets/27836e6f-5241-4d4b-8edd-2baa2b4f4698" />
<img width="748" height="555" alt="Screenshot 2026-03-31 at 11 05 27 AM" src="https://github.com/user-attachments/assets/a15b6b8a-d092-4408-a9ff-bed6bce0ac3f" />
<img width="750" height="500" alt="image" src="https://github.com/user-attachments/assets/f50123c9-f025-4899-b271-2e9645acaf3d" />
<img width="750" height="600" alt="image" src="https://github.com/user-attachments/assets/75e36041-2b51-46b0-bf2e-5e60a8db705c" />
<img width="750" height="600" alt="image" src="https://github.com/user-attachments/assets/502586f3-c218-43e0-b82a-94ed47aa873d" />
<img width="750" height="600" alt="image" src="https://github.com/user-attachments/assets/620cfbdf-9d30-42b1-96c4-7a568b7a8f8a" />






Queries
---
**Insert Matrix**
<img width="1603" height="937" alt="image" src="https://github.com/user-attachments/assets/2f6cb44b-bc94-4393-940f-97d5e827ef84" />
Query 1 fetches the first and last names of all players within the database along with their respective alma maters. The query itself is ordered by last name for organization sake.

A general manager or scout needs a quick reference of all prospects and their college backgrounds. College affiliation often influences how a player is evaluated, as certain programs are known for producing NFL-ready talent, and this query provides an instant roster overview.

<img width="1597" height="918" alt="image" src="https://github.com/user-attachments/assets/0c904696-6e71-4cae-8580-5f3ab0f384bd" />

Query 2 finds all players who scored above the average bench press result at the combine, and display their first name, last name, and how many reps they recorded, sorted from highest to lowest.

Strength is a critical factor for interior linemen, linebackers, and tight ends. A strength and conditioning coach evaluating prospects needs to quickly identify which players demonstrated above-average strength relative to the full prospect pool. This version keeps the query focused purely on the player name and their bench press result without the additional context of position and college.

Query 3 lists all players who were drafted along with the team that selected them and the draft round.
<img width="1166" height="579" alt="Screenshot 2026-03-31 at 5 10 38 PM" src="https://github.com/user-attachments/assets/23d13b6c-987f-431d-944c-71d97214590f" />

Query 3 allows users to view which players were drafted, the team that selected them, and the round they were chosen in. This provides insight into how early or late players were picked and which teams selected them. It is especially useful for analysts and front office staff who want to evaluate draft decisions and understand how talent is distributed across teams. Ordering the results by draft round makes it easier to see top picks first and analyze draft trends.

Query 4 calculates the average measurement for each drill based on player position.
<img width="692" height="340" alt="Screenshot 2026-03-31 at 11 07 33 AM" src="https://github.com/user-attachments/assets/3dc8db0d-e350-4ac4-b1d7-512464e8c472" />

Query 4 allows analysts to compare how different positions perform across various combine drills. Calculating averages highlights trends, such as which positions perform better in certain types of drills. This can help teams evaluate player strengths and make better draft decisions. Sorting the results by average measurement makes it easier to identify top-performing positions.

Query 5 lists all players over 300 pounds in descending order.
<img width="800" height="400" alt="image" src="https://github.com/user-attachments/assets/aebf25b5-373c-48f2-b037-b68735257147" />


A scout or general manager evaluating the offensive and defensive line needs to quickly filter prospects by size. Players over 300 pounds occupy a specific role in the NFL where mass and strength are baseline requirements, and this query gives personnel staff an instant list of prospects who meet that physical threshold.

Query 6 lists all colleges that produced at least 5 draft picks and the total number of players drafted from that school.
<img width="800" height="400" alt="image" src="https://github.com/user-attachments/assets/f0964116-3416-42fd-80e9-301ec1001705" />


NFL franchises invest heavily in scouting certain college programs. A director of player personnel needs to know which schools consistently produce drafted talent, as this informs where to allocate scouting resources each year. Programs with multiple draft picks signal a strong development pipeline worth monitoring closely.

Query 7 lists the average combine measurement by drill and by college.

<img width="800" height="400" alt="image" src="https://github.com/user-attachments/assets/8d12e7a6-280a-47da-917a-70dfbe5efdc8" />


Query 7 fetches the average measurement for every combine drill and groups it by the school. It uses a grouping query and joins all the necessary tables to link the combine results to universities. This query and its results are important to a general manager in the NFL since it is useful in determining if certain schools on average produce more favorable measurements in certain drills. This is especially useful for the wonderlic test, since it is an intelligence based test, and certain schools may be better at producing players that succeed at this test than others. It can guide GMs as to which school may have success in producing players at positions that require more success in certain drills as opposed to others. 

Query 8 lists out how many of each position is taken in each of the past draft years

<img width="800" height="400" alt="image" src="https://github.com/user-attachments/assets/6ab7c565-b7c7-4762-a4b0-60a29cc294fe" />


This query is meant to tell how many of each position is taken in the draft in each year. This query joins the tables related to players and their positions and the DraftPicks table. It also takes the count of each position and groups it by year. This is important from a managerial perspective since looking at past drafted positions can help forecast how strong or weak certain draft classes were in certain positions. It also can help forecast when contract terms may run out and makes it easier to forecast free agency managers to make decisions. It can also tell what positions the league is in need of with how every team drafts.
