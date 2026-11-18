1. What was the most challenging part of building this boilerplate? How did you overcome it?

The most challenging part was connecting all the components, especially the error handling, validation, logging, and database configuration. At first, it was difficult to understand how everything worked together. I overcame this by following the activity step by step, checking my code, and fixing errors whenever they appeared.

2. How does this boilerplate differ from your Midterm project? What specific improvements did you make?

Compared to my Midterm project, this boilerplate has a more organized and professional structure. I added centralized error handling, Joi validation, Winston logging, security middleware, and database migrations. I also improved the code organization by separating controllers, services, routes, entities, and utilities to make the project easier to maintain.

3. Why is centralized error handling better than try-catch in every controller?

Centralized error handling is better because it handles errors in one place instead of repeating try-catch blocks in every controller. It makes the code cleaner, easier to maintain, and provides consistent error responses. It also makes debugging easier because errors can be logged in one central location.

4. How does request validation with Joi improve security and code quality?

Joi improves security by checking user inputs before they reach the database or business logic. It prevents invalid or unexpected data from being processed. It also improves code quality because it provides clear validation rules and error messages, making the application more reliable.

5. What's the difference between synchronize: true and migrations? Why are migrations essential for production?

synchronize: true automatically updates the database structure based on the entities, while migrations allow developers to control database changes through specific files. Migrations are essential in production because they provide a safer and more organized way to update the database without accidentally losing existing data.

6. How does structured logging (Winston) help in production debugging compared to console.log?

Winston provides organized logs with timestamps, log levels, and additional information about errors and requests. Unlike console.log, it can save logs into separate files, such as combined.log and error.log. This makes it easier to track problems and identify what went wrong in production.

7. If you had to add a new feature (e.g., Product CRUD), how would you use this boilerplate? What would you need to add?

I would follow the same structure used in the User CRUD feature. First, I would create a Product entity, then create its service, controller, routes, and Joi validation schemas. I would also generate a database migration and connect the new routes to the main application. This way, I can reuse the existing error handling, logging, and response helpers.

8. What additional features would you add to make this boilerplate even more production-ready?

I would add JWT authentication, role-based access control, automated unit and integration testing, API documentation using Swagger, and automated database backups. I would also improve security and add monitoring tools to make the application more reliable, secure, and easier to maintain.

MODULE 9:
# 1. What is the difference between authentication and authorization? Give a real-world example of each.

Authentication is checking who the user is, while authorization is checking what the user is allowed to access. For example, when I log in using my email and password, that is authentication. After logging in, being allowed to access protected pages or features is authorization.

# 2. Why is JWT considered "stateless" and how does that benefit scalability?

JWT is called stateless because the server does not need to store a session for every logged-in user. The token already contains information like the user ID and email. This makes the system easier to scale because different servers can verify the token without needing to share session data.

# 3. What are the three parts of a JWT token and what does each part do?

The three parts of a JWT are the **header, payload, and signature**. The header contains information about the token and the algorithm used. The payload contains information about the user, like the `userId` and `email` in our activity. The signature is used to verify that the token is valid and has not been changed.

# 4. Why should you never put sensitive data (like passwords) in the JWT payload?

We should not put passwords or other sensitive information in the JWT because the payload can be decoded and read. It is not encrypted. In our activity, the JWT only contains the user's `userId` and `email`, and the password is not included.

# 5. How does bcrypt protect user passwords? What is the purpose of the "salt" and "rounds"?

bcrypt protects passwords by hashing them instead of storing the actual password. When the user logs in, bcrypt compares the entered password with the stored hash. The salt adds random information to make the hash more secure, while the rounds control how much work bcrypt does when creating the hash. More rounds make it harder to guess passwords through brute force.

# 6. What happens if someone steals a JWT token? How can you mitigate this risk?

If someone steals a valid JWT, they can use it to access protected routes as the user until the token expires. To reduce this risk, we can use HTTPS, make tokens expire sooner, store tokens securely, and use refresh tokens or token blacklisting. In our activity, the token expires after 24 hours by default.

# 7. Why is it important to use HTTPS when transmitting JWT tokens?

HTTPS is important because it encrypts the data being sent between the client and the server. This helps prevent someone from intercepting and stealing the JWT token while it is being transmitted.

# 8. What is the difference between a short-lived access token and a long-lived refresh token? When would you use each?

An access token is used to access protected API routes and usually has a short expiration time. A refresh token lasts longer and can be used to get a new access token without making the user log in again. I would use an access token for normal API requests and a refresh token to keep the user logged in for a longer time.

In our activity, we currently use a JWT that expires after 24 hours. Refresh tokens are mentioned as an optional feature.

# 9. How does the auth middleware know which user is making the request?

The auth middleware gets the JWT from the `Authorization` header using the `Bearer` format. It verifies the token using the JWT secret. After verifying it, it gets the `userId` and `email` from the token and attaches them to `req.user`. This allows the application to know which user is making the request.

# 10. If you had to implement role-based authorization (e.g., admin vs. regular user), how would you modify your current setup?

I would add a `role` field to the User entity, such as `admin` or `user`. I would also include the user's role in the JWT payload. Then I would create another middleware that checks the user's role before allowing access to certain routes. For example, only an admin could delete users or access admin-only features, while regular users could only access normal user features.