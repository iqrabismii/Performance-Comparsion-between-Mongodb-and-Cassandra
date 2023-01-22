# Performance Comparsion between Mongodb and Cassandra

![MongoDB](https://img.shields.io/badge/MongoDB-%234ea94b.svg?style=for-the-badge&logo=mongodb&logoColor=white) ![ApacheCassandra](https://img.shields.io/badge/cassandra-%231287B1.svg?style=for-the-badge&logo=apache-cassandra&logoColor=white) ![SQLite](https://img.shields.io/badge/sqlite-%2307405e.svg?style=for-the-badge&logo=sqlite&logoColor=white)

Two most popular Nosqls were compared on the basis of data loading, CRUD operation, CRUD operation at various consistency levels and latency rate. 
Lastly, visualisation was created using Mongocharts. 
Below are the following codes used in this project. 



SQLite: 

	•	We installed the DB browser to access the sqlite zip file from the below link:

         https://sqlitebrowser.org/

	•	One of the table team_analysis was created using the below join query and data was downloaded in local machine in csv format
SELECT * FROM Team t1
INNER JOIN Team_Attributes t2 ON 
t1.id = t2.ID 
INNER JOIN Team_History t3 ON 
t2.ID= t3.ID

Similar join queries were used to obtain other tables and after which the final csv files for the analysis were considered.





Cassandra:

	1	Docker Set Up : Download Docker for desktop from the below link:https://www.docker.com

	2	Follow the instructions below for setting up a cassandra instance on Docker
.

￼

3.  Create three nodes in a cluster on docker using the below commands
￼
           
 4. Place all the files to be uploaded into cassandra instance in the same directory as the Docker is present.

5. Open the cqlsh terminal in the same path as the files placed using the CLI option on the cassandra instance.





6. Create the KEYSPACE named BasketBall using the following command.


CREATE KEYSPACE BasketBall
  WITH REPLICATION = { 
   'class' : 'NetworkTopologyStrategy', 
   'datacenter1' : 3
  } ;

7. Use the KEYSPACE BasketBall created to further create the column families/tables required as per the csv files required for the analysis.
 
 USE basketball;

8. Using the following command create the required column families such as player_analysis, game_analysis, team_analysis and bb_nalaysis  in the KEYSPACE BasketBall.

player_analysis:

CREATE COLUMNFAMILY player_analysis
(PLAYER_ID int PRIMARY KEY, PLAYER_NAME varchar, SCHOOL varchar, COUNTRY varchar, BIRTHDATE date, PLAYER_CURRENT_AGE int, HEIGHT int, WEIGHT int, SEASON_EXP int,POSITION varchar, ROSTERSTATUS varchar,TEAM_ID int, PTS float, REB float, AST float, PLAYER_NM varchar, CONTRACT_TYPE_2020_2021 varchar, SALARY_2020_2021 int, CONTRACT_TYPE_2021_2022 varchar, SALARY_2021_2022 int, CONTRACT_TYPE_2022_2023 varchar, SALARY_2022_2023 int, CONTRACT_TYPE_2023_2024 varchar, SALARY_2023_2024 float) WITH COMPACT STORAGE;

team_analysis 

CREATE COLUMNFAMILY team_analysis
(TEAM_ID int PRIMARY KEY,TEAM_NAME varchar,TEAM_CITY varchar,TEAM_SLUG varchar, YEAR_FOUNDED int,SALARY_2020_2021 int,SALARY_2021_2022 int,SALARY_2022_2023 int,SALARY_2023_2024 int,SALARY_2024_2025 int,SALARY_2025_2026 int,HOME_WIN_PERCENT float,HOME_LOSS_PERCENT float,AWAY_WIN_PERCENT float,AWAY_LOSS_PERCENT float,TOTAL_WIN_PERCENT float,TOTAL_LOSS_PERCENT float);



game_analysis:

CREATE COLUMNFAMILY game_analysis
(TEAM_ID int PRIMARY KEY,SEASON int,LOCATION varchar,WIN_COUNT int, AVERAGE_2_POINT_GOAL_EFFICIENCY float,AVERAGE_3_POINT_GOAL_EFFICIENCY float,AVERAGE_2_POINT_GOAL_PERCENTAGE float, AVERAGE_3_POINT_GOAL_PERCENTAGE float,FREE_THROUGH_GOAL_EFFICIENCY float,FREE_THROUGH_GOAL_PERCENTAGE float,OFFENSIVE_REBOUND_PERCENTAGE float,AVERAGE_ASSISTS float,AVERAGE_PAINT_POINTS float,AVERAGE_2ND_CHANCE_POINTS float,DEFENSIVE_REBOUND_PERCENTAGE float,AVERAGE_NUMBER_OF_STEALS float,AVERAGE_NUMBER_OF_BLOCKS float,AVERAGE_POINTS_AFTER_TURNOVER_PERCENTAGE float,AVERGAE_FOULS float,AVERAGE_TURNOVER float,GAME_COUNT float,TOTAL_WIN_COUNT float,TOTAL_AVERAGE_2_POINT_GOAL_EFFICIENCY float,TOTAL_AVERAGE_3_POINT_GOAL_EFFICIENCY float,TOTAL_AVERAGE_2_POINT_GOAL_PERCENTAGE float,TOTAL_AVERAGE_3_POINT_GOAL_PERCENTAGE float,TOTAL_FREE_THROUGH_GOAL_EFFICIENCY float,TOTAL_FREE_THROUGH_GOAL_PERCENTAGE float,TOTAL_OFFENSIVE_REBOUND_PERCENTAGE float,TOTAL_AVERAGE_ASSISTS float,TOTAL_AVERAGE_PAINT_POINTS float,TOTAL_AVERAGE_2ND_CHANCE_POINTS float,TOTAL_DEFENSIVE_REBOUND_PERCENTAGE float,TOTAL_AVERAGE_NUMBER_OF_STEALS float,TOTAL_AVERAGE_NUMBER_OF_BLOCKS float,TOTAL_AVERAGE_POINTS_AFTER_TURNOVER_PERCENTAGE float,TOTAL_AVERGAE_FOULS float,TOTAL_AVERAGE_TURNOVER float,TOTAL_GAME_COUNT float,TEAM_NAME varchar,TEAM_SLUG varchar);

bb_analysis

CREATE TABLE bb_analysis(ID int PRIMARY KEY, TEAM_ID int, SEASON int, LOCATION varchar, WIN_COUNT int, AVERAGE_2_POINT_GOAL_EFFICIENCY float, AVERAGE_3_POINT_GOAL_EFFICIENCY float, AVERAGE_2_POINT_GOAL_PERCENTAGE float, AVERAGE_3_POINT_GOAL_PERCENTAGE float, FREE_THROUGH_GOAL_EFFICIENCY float, FREE_THROUGH_GOAL_PERCENTAGE float, OFFENSIVE_REBOUND_PERCENTAGE float, AVERAGE_ASSISTS float, AVERAGE_PAINT_POINTS float, AVERAGE_2ND_CHANCE_POINTS float, DEFENSIVE_REBOUND_PERCENTAGE float, AVERAGE_NUMBER_OF_STEALS float, AVERAGE_NUMBER_OF_BLOCKS float, AVERAGE_POINTS_AFTER_TURNOVER_PERCENTAGE float, AVERGAE_FOULS float, AVERAGE_TURNOVER float, GAME_COUNT int, TOTAL_WIN_COUNT int, TOTAL_AVERAGE_2_POINT_GOAL_EFFICIENCY float, TOTAL_AVERAGE_3_POINT_GOAL_EFFICIENCY float, TOTAL_AVERAGE_2_POINT_GOAL_PERCENTAGE float, TOTAL_AVERAGE_3_POINT_GOAL_PERCENTAGE float, TOTAL_FREE_THROUGH_GOAL_EFFICIENCY float, TOTAL_FREE_THROUGH_GOAL_PERCENTAGE float, TOTAL_OFFENSIVE_REBOUND_PERCENTAGE float, TOTAL_AVERAGE_ASSISTS float, TOTAL_AVERAGE_PAINT_POINTS float, TOTAL_AVERAGE_2ND_CHANCE_POINTS float, TOTAL_DEFENSIVE_REBOUND_PERCENTAGE float, TOTAL_AVERAGE_NUMBER_OF_STEALS float, TOTAL_AVERAGE_NUMBER_OF_BLOCKS float, TOTAL_AVERAGE_POINTS_AFTER_TURNOVER_PERCENTAGE float, TOTAL_AVERGAE_FOULS float, TOTAL_AVERAGE_TURNOVER float, TOTAL_GAME_COUNT int, TEAM_NAME varchar, TEAM_SLUG varchar, TEAM_CITY varchar, YEAR_FOUNDED int, SALARY_2020_2021 int, SALARY_2021_2022 int, SALARY_2022_2023 int, SALARY_2023_2024 int, SALARY_2024_2025 int, SALARY_2025_2026 int, HOME_WIN_PERCENT float, HOME_LOSS_PERCENT float, AWAY_WIN_PERCENT float, AWAY_LOSS_PERCENT float, TOTAL_WIN_PERCENT float, TOTAL_LOSS_PERCENT float, PLAYER_ID int, PLAYER_NAME varchar, SCHOOL varchar, COUNTRY varchar, BIRTHDATEPLAYER_CURRENT_AGE int, HEIGHT int, WEIGHT int, SEASON_EXP int, POSITION varchar, ROSTERSTATUS varchar, PTS float, REB float, AST float, PLAYER_NM varchar, CONTRACT_TYPE_2020_2021 varchar, PLAYER_SALARY_2020_2021 int, CONTRACT_TYPE_2021_2022 varchar, PLAYER_SALARY_2021_2022 int, CONTRACT_TYPE_2022_2023 varchar, PLAYER_SALARY_2022_2023 int, CONTRACT_TYPE_2023_2024 varchar,
PLAYER_SALARY_2023_2024 int);


9. Using the following command copy the data from the respective csv files into column families game_analysis, player_analysis, team_analysis and bb_analysis.

player_analysis

COPY basketball.player_analysis (PLAYER_ID,PLAYER_NAME,SCHOOL,COUNTRY,BIRTHDATE,PLAYER_CURRENT_AGE,HEIGHT,WEIGHT,SEASON_EXP,POSITION,ROSTERSTATUS,TEAM_ID,PTS,REB,AST,PLAYER_NM,CONTRACT_TYPE_2020_2021,SALARY_2020_2021,CONTRACT_TYPE_2021_2022,SALARY_2021_2022,CONTRACT_TYPE_2022_2023,SALARY_2022_2023,CONTRACT_TYPE_2023_2024,SALARY_2023_2024) FROM 'Player_Analysis.csv' WITH NULL='NULL' AND DELIMITER = ',' AND HEADER=TRUE;




team_analysis

COPY basketball.team_analysis
(TEAM_ID,TEAM_NAME,TEAM_CITY,TEAM_SLUG,YEAR_FOUNDED,SALARY_2020_2021,SALARY_2021_2022,SALARY_2022_2023,SALARY_2023_2024,SALARY_2024_2025,SALARY_2025_2026,HOME_WIN_PERCENT ,HOME_LOSS_PERCENT ,AWAY_WIN_PERCENT,AWAY_LOSS_PERCENT,TOTAL_WIN_PERCENT,TOTAL_LOSS_PERCENT) FROM 'Team_Analysis.csv' WITH NULL='NULL' AND DELIMITER = ',' AND HEADER=TRUE;

game_analysis

COPY basketball.game_analysis
(TEAM_ID,SEASON,LOCATION,WIN_COUNT, AVERAGE_2_POINT_GOAL_EFFICIENCY,AVERAGE_3_POINT_GOAL_EFFICIENCY,AVERAGE_2_POINT_GOAL_PERCENTAGE, AVERAGE_3_POINT_GOAL_PERCENTAGE,FREE_THROUGH_GOAL_EFFICIENCY,FREE_THROUGH_GOAL_PERCENTAGE,OFFENSIVE_REBOUND_PERCENTAGE,AVERAGE_ASSISTS,AVERAGE_PAINT_POINTS,AVERAGE_2ND_CHANCE_POINTS ,DEFENSIVE_REBOUND_PERCENTAGE,AVERAGE_NUMBER_OF_STEALS,AVERAGE_NUMBER_OF_BLOCKS,AVERAGE_POINTS_AFTER_TURNOVER_PERCENTAGE,AVERGAE_FOULS,AVERAGE_TURNOVER,GAME_COUNT,TOTAL_WIN_COUNT ,TOTAL_AVERAGE_2_POINT_GOAL_EFFICIENCY,TOTAL_AVERAGE_3_POINT_GOAL_EFFICIENCY,TOTAL_AVERAGE_2_POINT_GOAL_PERCENTAGE,TOTAL_AVERAGE_3_POINT_GOAL_PERCENTAGE,TOTAL_FREE_THROUGH_GOAL_EFFICIENCY ,TOTAL_FREE_THROUGH_GOAL_PERCENTAGE,TOTAL_OFFENSIVE_REBOUND_PERCENTAGE,TOTAL_AVERAGE_ASSISTS,TOTAL_AVERAGE_PAINT_POINTS,TOTAL_AVERAGE_2ND_CHANCE_POINTS,TOTAL_DEFENSIVE_REBOUND_PERCENTAGE ,TOTAL_AVERAGE_NUMBER_OF_STEALS,TOTAL_AVERAGE_NUMBER_OF_BLOCKS,TOTAL_AVERAGE_POINTS_AFTER_TURNOVER_PERCENTAGE,TOTAL_AVERGAE_FOULS,TOTAL_AVERAGE_TURNOVER,TOTAL_GAME_COUNT,TEAM_NAME ,TEAM_SLUG) FROM 'Game_Analysis.csv' WITH NULL='NULL' AND DELIMITER = ',' AND HEADER=TRUE;




basketball_analysis

COPY basketball.bb_analysis (ID, TEAM_ID, SEASON, LOCATION, WIN_COUNT, AVERAGE_2_POINT_GOAL_EFFICIENCY, AVERAGE_3_POINT_GOAL_EFFICIENCY, AVERAGE_2_POINT_GOAL_PERCENTAGE, AVERAGE_3_POINT_GOAL_PERCENTAGE, FREE_THROUGH_GOAL_EFFICIENCY, FREE_THROUGH_GOAL_PERCENTAGE, OFFENSIVE_REBOUND_PERCENTAGE, AVERAGE_ASSISTS, AVERAGE_PAINT_POINTS, AVERAGE_2ND_CHANCE_POINTS, DEFENSIVE_REBOUND_PERCENTAGE, AVERAGE_NUMBER_OF_STEALS, AVERAGE_NUMBER_OF_BLOCKS, AVERAGE_POINTS_AFTER_TURNOVER_PERCENTAGE, AVERGAE_FOULS, AVERAGE_TURNOVER, GAME_COUNT, TOTAL_WIN_COUNT, TOTAL_AVERAGE_2_POINT_GOAL_EFFICIENCY, TOTAL_AVERAGE_3_POINT_GOAL_EFFICIENCY, TOTAL_AVERAGE_2_POINT_GOAL_PERCENTAGE, TOTAL_AVERAGE_3_POINT_GOAL_PERCENTAGE, TOTAL_FREE_THROUGH_GOAL_EFFICIENCY, TOTAL_FREE_THROUGH_GOAL_PERCENTAGE, TOTAL_OFFENSIVE_REBOUND_PERCENTAGE, TOTAL_AVERAGE_ASSISTS, TOTAL_AVERAGE_PAINT_POINTS, TOTAL_AVERAGE_2ND_CHANCE_POINTS, TOTAL_DEFENSIVE_REBOUND_PERCENTAGE, TOTAL_AVERAGE_NUMBER_OF_STEALS, TOTAL_AVERAGE_NUMBER_OF_BLOCKS, TOTAL_AVERAGE_POINTS_AFTER_TURNOVER_PERCENTAGE, TOTAL_AVERGAE_FOULS, TOTAL_AVERAGE_TURNOVER, TOTAL_GAME_COUNT, TEAM_NAME, TEAM_SLUG, TEAM_CITY, YEAR_FOUNDED, SALARY_2020_2021, SALARY_2021_2022, SALARY_2022_2023, SALARY_2023_2024, SALARY_2024_2025, SALARY_2025_2026, HOME_WIN_PERCENT, HOME_LOSS_PERCENT, 
AWAY_WIN_PERCENT, AWAY_LOSS_PERCENT, TOTAL_WIN_PERCENT, TOTAL_LOSS_PERCENT, PLAYER_ID, PLAYER_NAME, SCHOOL, COUNTRY, BIRTHDATEPLAYER_CURRENT_AGE, HEIGHT, WEIGHT, SEASON_EXP, POSITION, ROSTERSTATUS, PTS, REB, AST, PLAYER_NM, CONTRACT_TYPE_2020_2021, PLAYER_SALARY_2020_2021, CONTRACT_TYPE_2021_2022, PLAYER_SALARY_2021_2022, CONTRACT_TYPE_2022_2023, PLAYER_SALARY_2022_2023, CONTRACT_TYPE_2023_2024, PLAYER_SALARY_2023_2024) FROM 'Basketball_Analysis.csv' WITH NULL='NULL' AND DELIMITER = ',' AND HEADER=TRUE;

CRUD OPERATION

To read one record:  
SELECT * FROM team_analysis WHERE TEAM_ID = 1610612737
To read multiple records: 
SELECT * FROM game_analysis WHERE TEAM_ID = 1610612737 ALLOW FILTERING;
To update a single record:
UPDATE game_analysis SET TEAM_SLUG = ‘BTL’ WHERE id = 3;
To update multiple records: 
UPDATE game_analysis SET TEAM_SLUG = ‘FFF’ WHERE ID IN (1,2,3,4,5,6,7,8,9,10)

To delete single record:
DELETE FROM game_analysis WHERE id = 3;
To delete entire column family(table):
DROP COLUMNFAMILY player_analysis;

Insert values into team_analysis table
INSERT INTO basketball.team_analysis (TEAM_ID,TEAM_NAME,TEAM_CITY,TEAM_SLUG,YEAR_FOUNDED,SALARY_2020_2021,SALARY_2021_2022,SALARY_2022_2023,SALARY_2023_2024,SALARY_2024_2025,SALARY_2025_2026,HOME_WIN_PERCENT ,HOME_LOSS_PERCENT ,AWAY_WIN_PERCENT,AWAY_LOSS_PERCENT,TOTAL_WIN_PERCENT,TOTAL_LOSS_PERCENT) VALUES (1610612778, ‘Charlotte Hornets’, ‘Charlotte’, ‘CAA’, 1988,108219000,8125900,44614400,31500000,0,0,0.54,0.46,0.3,0.7,0.45,0.56)

CONSISTENCY LEVELS- CRUD Operations:
For Read
Read Consistency Level: 1:
CONSISTENCY ONE
SELECT * FROM bb_analysis WHERE TEAM_ID =1610612738 ALLOW FILTERING;
Read Consistency Level: 2:
CONSISTENCY TWO
SELECT * FROM bb_analysis WHERE TEAM_ID =1610612738 ALLOW FILTERING;

Read Consistency Level: ALL:
CONSISTENCY ALL
SELECT * FROM bb_analysis WHERE TEAM_ID =1610612738 ALLOW FILTERING;

For Write
Update Consistency 1:
CONSISTENCY ONE
UPDATE bb_analysis SET TEAM_SLUG = ‘BTL’ WHERE id = 1;

Update Consistency QUORUM:
CONSISTENCY QUORUM
UPDATE bb_analysis SET TEAM_SLUG = ‘BTL’ WHERE id = 1;
Update Consistency ALL:
CONSISTENCY ALL
UPDATE bb_analysis SET TEAM_SLUG = ‘BTL’ WHERE id = 1;

Insert Consistency 1:
CONSISTENCY ONE
INSERT INTO bb_analysis(id,TEAM_ID,SEASON,LOCATION)VALUES(2724,160612699,2022,’HOME’); 
Insert Consistency QUORUM:
CONSISTENCY QUORUM
INSERT INTO bb_analysis(id,TEAM_ID,SEASON,LOCATION)VALUES(2725,160612699,2022,’HOME’); 
Insert Consistency ALL:
CONSISTENCY ALL
INSERT INTO bb_analysis(id,TEAM_ID,SEASON,LOCATION)VALUES(2726,160612699,2022,’HOME’); 

LATENCY
“nodetool cfstats”






MongoDB:

	1	MongoDB server was installed on the local machine following the instruction given in the link below

https://treehouse.github.io/installation-guides/mac/mongo-mac.html

	2	After downloading the mongo server, the respective directory was created to store the mongo data files. 

Code: mkdir -p /srv/mongodb/rs0-0  /srv/mongodb/rs0-1 /srv/mongodb/rs0-2
	3	Three replica sets were created with port number 27018, 27019, 27020 using the code below.
sudo mongod --port 27018 --dbpath /data/db/rs0-0 --replSet rs0 --bind_ip localhost 
sudo mongod --port 27019 --dbpath /srv/mongodb/rs0-0 --replSet rs0 --bind_ip localhost 
sudo mongod --port 27020 --dbpath /srv/mongodb/rs0-2 --replSet rs0 --bind_ip localhost
	4	Then we connected to primary node  port number 27018 in the new terminal using the code below: mongo –port 27018
	5	We also connected to secondary nodes  port number (27019 and 27020 )in the new shell using the code below: mongo –port 27019 , mongo –port 27020
	6	Then after creating the nodes we initiated the replication process  in the primary node using the code below:
rs.initiate({_id: "rs0",members: [{ _id: 0, host : "127.0.0.1:27018" },{ _id: 1, host : "127.0.0.1:27019" },{ _id: 2, host : "127.0.0.1:27020" }]})

	7	Checked the status of nodes using the code below:
rs.status( )
	8	We downloaded mongodb Compass from the below link: https://www.mongodb.com/try/download/compass
	9	Created the two connections in the compass; first using  the above mentioned  port numbers 27018, 27019 & 27020 and second using  the default port number 27017
￼
￼

	10	Installed Pymongo using PIP install: pip install pymongo  , Version number 3.12.3
	11	Imported the pymongo module, Json and Pandas in jupyter notebook
	12	Connected to Mongo localhost using the  following command:
client= pymongo.MongoClient("mongodb://localhost:27017")
	13	Uploaded the csv files into pandas dataframe using the command below:
df = pd.read_csv(r"Game_Analysis.csv")
	14	The upload csv files in dataframe was converted in JSON format using the following command:
data = df .to_dict(orient="record")
	15	Created Database “BasketBall” on Mongo Client using the following command:
database= client["BasketBall"]
	16	Then collection was created in the same database (“BasketBall”) and  converted JSON files were uploaded into collections using the following command: database.Game_Analysis.insert_many(data)
	17	Total 4 collections named :  game_analysis, player_analysis, team_analysis and bb_analysis were created in the database “BasketBall” on MongoDB Compass.

￼
	18	The same process mentioned above was followed to upload data  into the other connection ie. for port number 27018

Steps for CRUD Operations:
	1	To measure the time of CRUD operation we set the “profiling level (2)” and the all queries were performed. We used db.system.profile.find() after running the query to find the query execution stats.
Query:
db.setProfilingLevel(2)
“Query for CRUD” 
db.system.profile.find().limit(1).sort({ts:-1})

To read/ retrieve a  record.
db.game_analysis.find({Team_ID: “1610612737”}) 
To update a single record
db.game_analysis.updateOne({TEAM_ID:"1610612738"},{$set:{TEAM_SLUG:"BTL"},{upsert: true}) 
To update multiple records db.game_analysis.updateMany({TEAM_ID:"1610612738"},{$set:{TEAM_SLUG:"BTL"})
To remove multiple records from collection
db.game_analysis.remove({ })
To remove single record from collection 
db.game_analysis.remove({Team_ID: “1610612738”}, { justOne:true})
To insert a single record in collection
db.game_analysis.insertOne({id:272222,Team_ID:1610612699,SEASON:2022,LOCATION:"Away"})
To insert many records in collection
db.game_analysis.insertMany([{id:272222,Team_ID:1610612699,SEASON:2022,LOCATION:"Away"},{id:272222,Team_ID:1610612700,SEASON:2022,LOCATION:"Away"}])

CONSISTENCY LEVELS CRUD Operations:
For Read
Read Consistency Level: “local”:
db.basketball_analysis.find({Team_ID: “1610612737”}). readConcern(“local”)
Read Consistency Level: “majority”:
db.basketball_analysis.find({Team_ID: “1610612737”}). readConcern(“majority”)
Read Consistency Level: “available”:
db.basketball_analysis.find({Team_ID: “1610612737”}). readConcern(“available”)

For Updates
Write Consistency Level: 1:
db.basketball_analysis.updateMany({TEAM_ID:”1610612737”},{$set:{TEAM_SLUG: “BTL”}},{writeConcern:{w:1}})
Write Consistency Level: “majority”:
db.basketball_analysis.updateMany({TEAM_ID:”1610612737”},{$set:{TEAM_SLUG: “BTL”}},{writeConcern:{w: “majority”}})

For Insert
Write Consistency Level: 1:
db.game_analysis.insertOne({id:272222,Team_ID:1610612699,SEASON:2022,LOCATION:"Away"},{writeConcern:{w:1}})
Write Consistency Level: “majority”:
db.game_analysis.insertOne({id:272222,Team_ID:1610612699,SEASON:2022,LOCATION:"Away"},{writeConcern:{w: “majority”}})

LATENCY
Query to measure latency for varying read and write operations for different collections
db.player_analysis.latencyStats( { histograms: true } )


ATLAS

	1	Registered on the MongoDB cloud using the link below:

https://www.mongodb.com/cloud/atlas/register

	2	We then added a new database user.

￼













	3	Created a cluster named “newCluster”

￼


	4	Loaded the data as below:

Connected to MongoDB Compass by clicking on this link below
￼
Connected to cluster in Compass
￼



Created the collections in the Compass and Uploaded csv files directly in the Compass

￼






 Collections and data on the compass could be viewed on cloud as well

￼


MongoDB Charts for Visualization:

Created charts for NBA player analysis using MongoDB charts on Atlas.

￼


