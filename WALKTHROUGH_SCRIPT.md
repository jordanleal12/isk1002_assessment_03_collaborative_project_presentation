# Feature Walkthrough Script

- This will be a demonstration of the features of our full stack MERN application, 'The Century Screening Room'.

- It consists of a frontend React service hosted on Netlify, a backend express API service hosted on Render, and a MongoDB database service hosted on Mongo Atlas.

- It is a social platform web application, showcasing the "Reel Canon," a curated list of 100 films for movie enthusiasts to explore, mark and rate. Users can create accounts, befriend other users, and compete with their 'reel-canon' score, which increases as they watch and rate movies.

- The frontend service is the client facing part of the application. As such, I will demonstrate an end-to-end user experience, showcasing application features and providing insight as to what happens behind the scenes.

- Looking at our home page, or 'landing page' we can see we are seemingly able to cycle through pages. However as a React application, this is actually a Single Page Application. As we navigate through the site we never actually change pages, we only change what React components are being displayed.

- As a new user, we load this application fresh with no cached data. Even though we aren't logged in yet, the site still needs to fetch dynamic data to display the required components, specifically our 'reel-canon' movies, and our leaderboard standings.

- Behind the scenes, this means as the site first loaded it sent two HTTP GET requests to our API, which processed the requests, performed a read operation on the Mongo Atlas database through the assigned port, formatted the database data and sent it back to the browser.

- We can see this directly if we open our DevTools, select network, and search for xhr.

- Here we see 'leaderboard' and 'reel-canon', and if we select 'leaderboard' we can see a GET request was sent to the leaderboard route of our API.

- If we look at the response, we can see a formatted response containing the required data for the React application to process and display in the browser, in our leaderboard podium.

- These responses are cached using Tanstack Query caching, and are cleared or refreshed under certain conditions, such as relevant information being updated, or the data becoming 'stale' after a certain amount of time. This keeps the data up to date as needed, while minimizing API calls.

- You can see this information displayed on our home page. The movie carousel shows an interactive random selection from the reel-canon, which can be swiped or clicked through, and the leaderboard podium displays the users with the highest current reel-canon score.

- Before we create a new user, lets look at how the application gracefully handles errors. I will turn off our API and refresh the page.

- Refreshing, we can see that errors are caught at their boundary, being the components effected by the error, with the header and footer component remaining un-effected. We have the specific error being formatted and displayed, and a retry option. Let's turn the API back on and see what happens.

- After restarting the API, pressing the 'try again' button successfully initiates a refetch, and the effected components are displayed again.

- Now we understand what happens behind the scenes, lets create an account as a new user.

- A 'register' call to action directs me to the register page. The register form here enforces certain rules, such as valid email. If we attempt an invalid email, you can see it prevents us from successful registration and gives us direction on what to fix.

- This enforcement can be seen throughout the form and helps prevent wasteful API calls with invalid data.

- We submit the form, sending a POST request to our API to create a new user. This is validated by the API, and as we can see prevents creation of duplicate emails or usernames.

- After successful registration, we are assigned a JWT token to local storage, which is attached to future requests as validation for protected user routes.

- Upon sign in, the application sent new requests to the API, fetching and caching current users, this current users friendships and their reel-canon progress.

- We can see we have some new options. We now have a 'my profile' page, and a 'sign out' and 'friend requests' call to action.

- As a new user, I wish to add some of my friends. I move across to my profile page, which looks quite empty since we are a new user.

- Under the 'add friends' card, I search for and add the desired friend. As you'll notice, nothing was changed in the 'your friendships' card. This is because the other user has to accept the friend request first. So let's log into that account to demonstrate.

- Upon sign out, the JWT token is removed from local storage, and the user specific caches are cleared.

- As we sign back in, a new JWT token is issued and the user specific data is re-fetched and cached.

- We can see the friend request we sent appears as a notification. If we accept it and look at this users list of friends, they are now friends.

- Logging back in with the new user account, we can confirm this friendship exists for both users.

- The next thing we will do is explore the reel-canon movies, mark off what has already been watched and explore the movies on offer.

- As you can see, hovering a movie card reveals the director, cast and summary information. If we mark as watched, the movie poster is revealed and an optional rating option appears. An 'Unwatch' option also appears, allowing the user to undo an accidental update.

- This sends a PATCH request to the API to update the users reel-canon progress, updating the stored cache.

- After doing this a few times, we can move back to the 'my profile' page and see we now have a lot more information displayed.

- We have our favourite genres, a list of watched movies, and we can see our reel-canon progress has increased.

- As a new user, I'm so impressed with the site that I wish to learn more about the site and creators, and send them a message.

- Moving to the about page, I see a summary of the website, an overview of the creators and their GitHub Profiles, and a contact call to action.

- This call to action is reflected site wide in the footer, opening the same modal. I leave them a flattering message, and decide I'm finished for now, logging out.

- Later that evening I want some ideas for movies to watch so I log back in on my phone. I swipe through the featured movies, then decide to see where I stand on the leaderboard after adding the movies I already watched.

- The intuitive burger menu folds open, and I select the leaderboard page, scrolling through the responsive design. Noting my position, I move across to the reel-canon, tapping each movie to bring up the details, choosing a movie and then logging out.

- Thus ends the demonstration of the application features through the lens of a new user. Thank you for watching!
