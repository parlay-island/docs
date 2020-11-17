# Design Justification

Here is a list of some of the design decisions that our team made along with some of the rationale for our choices.

1. **Issue: how to get questions into the game**
   * **Decision**: Create a backend API completely separate from the Unity game
   * **Justification**: We made this decision because we wanted to also include a component where teachers could add questions. We didn’t want this part to be a part of the game itself because it would be easier and more flexible to develop the teacher UI with a web frontend framework rather than using Unity’s UI elements which are not as inclusive.
   * **Alternatives**:
     * Combining all components together
     * Connecting the game to a database and the teacher UI to the same database
   * **Trade-offs**:
     * We didn’t combine all these components together because it was important that the teacher UI was extensible separate from the game so that they could be released separately and the teacher UI could be developed using traditional frontend components which would make the teacher UI like a regular website.
     * We didn’t connect the game and teacher UI to a database because we wanted to manage the relationship with the database with more control. Having two separate applications that depend on a database would mean that when the database was migrated with changes on one end, it would result in the same issues in other end. Rather than replicating those issues, we used a backend API to give our resources away with a clean interface.
   * **Assumptions**:
     * We assumed that connecting the API would present less of a challenge than integrating a database. This assumption was probably untrue.
     * We assumed that it was very important to be able to change questions in the game.
   * **Dependencies**:
     * This decision impacts how we divided our entire project into 3 components.
2. **Issue: how to represent the teacher platform**
   * **Decision**: Create a separate nodeJS app 
   * **Justification**: We decided to go with normal nodeJS because the frontend will also eventually serve the game, with separate log-in for the teacher and students. It’s harder to insert the webGL artifact from the game into a React app, so nodeJS was a better option. 
   * **Alternatives**: 
     * Use a React app for the frontend
   * **Trade-offs**: React may make rendering and reusing components easier, but it would also make it harder to eventually integrate the game
   * **Assumptions**: WebGL is hard to integrate with React / other JS frameworks that don’t use vanilla HTML/CSS/JS. 
   * **Dependencies**:
     * This will impact how the game will be integrated into the frontend.
     * Using nodeJS also impacts the choice of frontend testing framework, as testing UI elements in nodeJS is not as well documented or flexible as testing UI elements for frameworks like React.
3. **Issue: how to deploy our application**
   * **Decision**: We decided to use a cloud service \(AWS specifically\) to deploy our application.
   * **Justification**: We didn’t want to deal with the issues associated with an unmanaged on-prem server. Using the cloud approach, especially AWS which half of our team had experience using before, gives us the advantage of not dealing with the details of the deployment.
   * **Alternatives**:
     * Another cloud service
     * On-prem server
   * **Trade-offs**:  
     * AWS is slightly complex so it does produce a little bit of difficulty in setting up.
     * With an on-prem server, we would have a little more access to fixing encountered issues.
   * **Assumptions**: We have the money to pay for AWS services.
   * **Dependencies**: This will impact how future developers can deploy our application. It would take a little bit of work to set up a different deployment, but having AWS set up encourages future developers to use AWS EB for deployment.
4. **Issue: how to store information in the backend**
   * **Decision**: Store information using AWS databases
   * **Justification**: AWS is secure, scalable, and cheap.
   * **Alternatives**: GCP, Azure
   * **Trade offs**: 
     * All the potential options provide a wide range of flexibility; however, the main benefit of AWS that the others don’t have is that it’s relatively cheaper \(and we can run on free tier for a while\).
   * **Assumptions**: We will be able to get money from the client in order to pay AWS fees if we move past the free plan when we get more traffic.
   * **Dependencies**: This will impact how to data is managed in the backend and how the backend will be deployed.
5. **Issue: how to release the game to users**
   * **Decision**: Release game as a WebGL package
   * **Justification**: it is much easier for users to access the game from a website.
   * **Alternatives**: stand alone package
   * **Trade offs**: The other option means that a user would need to download the package beforehand and set up the game on their computer. This requires effort from the user’s perspective in order to set up the game rather than simply visiting a website. Thus we decided to go with simply releasing the game on the web through a WebGL package.
   * **Assumptions**: Students will play the game during class where they have access to Wifi and a Chromebook. 
   * **Dependencies**: Because we are using WebGL, this impacts the way we make HTTP requests. WebGL builds cannot support System.Net calls, so all requests have to be made in coroutines. Exporting the game as a WebGL package also impacts the choice of frontend framework, as some frameworks do not integrate well with WebGL.
6. **Issue: how to generate base logic for the game**
   * **Decision**: developed the game using Unity
   * **Justification**: Unity is one of the most popular game engines out there. Thus there is a lot of documentation and tutorials that can assist us in developing a game. Also, it has a large amount of prebuilt functionality which improves the speed in which we can develop the game.
   * **Alternatives**: Unreal, Game Maker, PixiJS
   * **Trade Offs**: The other options either don’t have as much features as Unity in terms to improve game development speed or don’t have enough of a robust ecosystem with tutorials and integrations.
   * **Assumptions**: We assumed that Unity was more difficult to learn than the other game engines but provided more benefits long term in terms of development speed.
   * **Dependencies**: By moving forward with unity we ended up complicating our testing infrastructure. Unity testing is inconsistent and requires the implementation of Unity testing libraries. This has made obtaining proper code coverage more difficult as it is more labour intensive to generate tests.

