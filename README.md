# Art Heist Capstone Project - backend API

## Introduction 
This is a game where the player has to answer art related multiple choice questions. Based on the rarity level (common, rare or legendary) of the artwork displayed, the randomly generated MCQ can be easy, medium or hard.
The rules of the game 
* Answer a question right, and steal the artwork and increase your score
* the game ends when you:
>1.  answer all 10 questions correctly
 >2.  get 3 questions wrong (3 penalties max)
 >3. forfeit the game. 


## Pre-requisites
### Requirements for running back-end game code:
* Download intellij/VSCode for editing/displaying back-end code (intellij preferrable)
* For Command Line Tools, it's recommended to download:
>* Xcode Command line tools (easier terminal control)
>* Postgres + SQL(for the Game Database and its language)
>* Git (for version control)
>* HomeBrew 15.2 (ease of package management)
* Other recommended off-the-web downloads include:
>* Java 17 (back-end code language)
>* Postman(for the API to mimic the front-end responses and test different API requests)
>* Postico (for the viewing of Game database information)
* Using Spring initializr, the recommended dependencies that were incorporated in the back-end code design were:
>* Spring Web
>* Spring Boot DevTools
>* PostgreSQL Driver
>* Spring Data JPA


## Data Structure of project:
The `models` package consists of 4 POJO classes which are used to define how the classes are mapped to the databaseand 1 ENUM:
>1) A `Artwork` POJO class for each work properties, including `title`, `rarity level`, `artist`, `value` etc..
>2) A `ArtworkInGame` POJO class which tells you the artworks that are being used for each game with properties including `stolen`, and `game_id`, `artowkr_id`
>3) A `Game` POJO class for the game information 
>4) A `Player` POJO class with properties including: `name`, list of `games`
>5) A `RarityLevel` Enum for the rarity level of each artwork


The `repositories` package consists of 4 repositories including `ArtworkRepository`, `ArtworkInRepository`, `GameRepository`, `PlayerRepository`.

The `services` package has 4 classes, namely `ArtworkInGameService`, `ArtworkService`, `PlayerService`, `GameService` to handle game logic.

The `controllers` package consists of 4 classes `PlayerController`, `GameController`, `ArtworkInGameController` and `ArtworkController` which enables you to perform different requests corresponding to the `CRUD` functionalities
The `DataLoader` in the `components` package is used to pre-populate the `artworks` table and added a few `players` in the database.You may wish to connect to Postico to view/inspect the tables.

### UML Diagram
![Screenshot 2023-06-19 at 10 05 13](https://github.com/IsabelG96/capstone_backend/assets/56633439/ea009a32-0ad7-41fe-9522-8929242c2f95)

### ERD (for database structure)
![Screenshot 2023-06-19 at 10 05 34](https://github.com/IsabelG96/capstone_backend/assets/56633439/d58be084-d1c4-4d76-a7a2-9a1ee782a8ab)



## Installation
* To run the code, you will need:


     Java 17
     Postico (for Mac) or pgAdmin (for Windows) for the PostgreSQL database
     IntelliJ IDEA
     Postman 


* Follow these steps to install and run the code:
    - Clone the repositories to your local machine: git clone from https://github.com/IsabelG96/capstone_backend (backend) and https://github.com/KKLW97/capstone_front_end.
    - Create a new database in your terminal called `capstone_backend`.
    - Open the file in IntelliJ IDEA. 
    - Update the application.properties file with your database credentials.
    - Run the `CapstoneBackendApplicatio



<table>
  <thead>
    <tr>
      <th>Request</th>
      <th>URL path: localhost:8080 </th>
      <th>Body</th>
      <th>Functionality</th>
      <th>Information Returned</th>
    </tr>
  </thead>
  <tbody>
  
  
 <tr>
      <td>POST</td>
      <td>/players</td>
      <td> <strong>Object:</strong> Player <br><br> <strong>JSON:</strong>

```json
{
    "name": "[insert player name]"
}
```

</td>
      <td>Creates a new player</td>
      <td>The <code>Player</code> object that was created.</td>
    </tr>
    <tr>
      <td>GET</td>
      <td>/players</td>
      <td></td>
      <td>Gets all players.</td>
      <td>List of all <code>Player</code> objects which consists of player id, player name, and list of games.</td>
    </tr>
    <tr>
      <td>GET</td>
      <td>/players/{id}</td>
      <td></td>
      <td>Gets the player of the Id specified.</td>
      <td>The <code>Player</code> object with the specified Id, which consists of player id, player name, and list of games</td>
    </tr>
    
    
   <tr>
      <td>GET</td>
 <td>Default: <code>/artworksInGame</code>, For specified game id: <code>/artworksInGame?game_id={gameId}</code>, for specified stolen boolean: <code>/artworksInGame?stolen={true/false}</code>, for both game id and boolean: <code>/artworksInGame?game_id={gameId}&stolen={true/false}</code></td>
      <td></td>
      <td>Gets all artworks in games.</td>
      <td>Returns by default List of all <code>ArtworkInGame </code> objects which consists of an <code>id</code>,<code>stolen</code> boolean, <code>game</code> and <code>artwork</code> objects. When with the <code>@RequestParams</code> <code>game_id</code> or <code>stolen</code> boolean, it returns the information based on what is specified in the <code>@RequestParam</code>. For example, if you want all artworks in gamr for game id 1, then write <code>http://localhost:8080/artworksInGame?game_id=1</code>, for all artworks in game that are stolen , write <code>http://localhost:8080/artworksInGame?stolen=true</code>.</td>
   </tr>

  <tr>
      <td>GET</td>
      <td>/artworksInGame/{id}</td>
      <td></td>
      <td>Gets the ArtworkInGame object of the Id specified.</td>
      <td>Returns <code>ArtworkInGame </code> object of the specified id, which consists of an <code>id</code>,<code>stolen</code> boolean, <code>game</code> and <code>artwork</code> objects.</td>
  </tr>

  <tr>
      <td>PATCH</td>
      <td>/artworksInGame/{id}?stolen={true}</td>
      <td></td>
      <td>Update the property `stolen` for a specified artork in game by Id.</td>
      <td>The <code>artworkInGame</code> object with the specified Id, which consists of an <code>id</code>,<code>stolen</code> boolean, <code>game</code> and <code>artwork</code> objects</td>
  </tr>

  <tr>  
    <td>GET</td>  
    <td>/artworks</td>  
    <td></td>  
    <td>Get all artworks.</td>  
    <td>List of all artwork</td>  
  </tr>  
  
  <tr>  
    <td>GET</td>  
    <td>/games OR /games?player_id=1 OR /games?complete=false OR /games?player_id=1&complete=false</td>  
    <td></td>  
    <td>Gets all games. Option to filter by player id, by complete status, or both.</td>  
    <td>List of all games</td>  
  </tr>  
  <tr>  
    <td>GET</td>  
    <td>/games/{gameId}</td>  
    <td></td>  
    <td>Gets a specific game by its id.</td>  
    <td>The Game object with the specified id.</td>  
  </tr>  
  
  <tr>  
    <td>POST</td>  
    <td>/games?playerId=1</td>  
    <td></td>  
    <td>Creates a game for the player of player id passed into the param.</td>  
    <td>The new <code>Game</code> object that has been created.</td>  
  </tr>  
  
  <tr>  
    <td>PUT</td>  
    <td>/games/{gameId}</td>  
<td>  <strong>Object:</strong> Game<br/><br/><strong>JSON:</strong>

```json
{
    "player": "[insert player name]"
}
```
</td>  
    <td>Updates a game of the specified id.</td>  
    <td>Returns the <code>Game</code> object.</td>  
  </tr>

  </tbody>
</table>

## Collaborators
### Name: Github Username
- Kelly Wong: KKLW97
- Katie Bamford: klb545
- Hayan Butt: HayanButt
- Isabel Galwey: IsabelG96
- Stella Annor: StellaA30
