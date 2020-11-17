# Application Architecture

## High Level Design

* [Architecture diagram](https://lucid.app/invitations/accept/60538ef2-a428-482d-bd7d-53875b9f9c87)
* Our program is split into 3 separate modularized components: the game, the teacher monitoring platform frontend, and a backend API
* Each of these components have completely different structures as they use different languages and frameworks
  * The game
    * This is the part of the program that contains the personal finance and economics game. It will be integrated into the front end and it gets question and leaderboard information and sends result information to the backend. 
    * An overview of how it is configured is that all of the game objects are present in a scene and a game manager is able to turn on and off and control the functionality of some of the game objects. Additionally, the game objects each contain backend logic and/or a visual component
    * The game is written in Unity, so most architectural decisions are made for the team except for the ones for networking because Unity is deprecating their networking framework, so we couldn't use it since it is about to be replaced.
    * This component is used as an object in Amazon S3 which is displayed with the frontend.
  * The frontend
    * The frontend plays two roles: display the game and display the teacher monitoring platform.
    * The teacher monitoring platform allows the teacher to update questions and track student progress. 
    * It gets information about the questions and sends any updated information \(ie. modify, add, delete questions\) to the backend.
  * Backend API
    * The backend is a Django web app written with an MVC setup connected to a PostgreSQL database. 
    * The backend like all our applications are run in AWS
    * The API is designed with the REST API framework providing resources that the user can GET, PUT, POST, and DELETE \(CRUD\).
    * Some of the endpoints are paginated to prevent sending an unreasonable amount of data for what will actually be useful. For example, `GET /results/` and `GET /levels/{levelId}/results/` are paginated because they store the results of every game, but the endpoint is currently only used to fill the leaderboard.



