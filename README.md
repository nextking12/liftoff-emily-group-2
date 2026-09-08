# Parkd

Parkd is a social discovery app for U.S. national parks. It combines National
Park Service data with community reviews and blog posts to help users research
parks, share experiences, and plan their next visit.

## Features

- Browse and search parks from the National Park Service API
- View park details, webcams, activities, and active alerts
- Register, sign in, and view user profiles
- Rate parks and create, edit, or delete reviews
- Create and manage park-specific blog posts

## Tech Stack

- Java 17
- Spring Boot 3.4
- Spring MVC, Spring Data JPA, and Hibernate
- Thymeleaf
- MySQL 8
- Gradle
- [Pico CSS](https://picocss.com/)
- [National Park Service API](https://www.nps.gov/subjects/developer/api-documentation.htm)

## Prerequisites

Install the following before running the project:

- Java Development Kit (JDK) 17
- MySQL 8 or later
- An internet connection for National Park Service data

The repository includes the Gradle wrapper, so a separate Gradle installation
is not required.

## Local Setup

1. Clone the repository and enter the project directory.

   ```bash
   git clone <repository-url>
   cd liftoff-emily-group-2
   ```

2. Create the MySQL database and a local application user.

   ```sql
   CREATE DATABASE parkd_user_management;
   CREATE USER 'parkd'@'localhost' IDENTIFIED BY 'choose-a-password';
   GRANT ALL PRIVILEGES ON parkd_user_management.* TO 'parkd'@'localhost';
   FLUSH PRIVILEGES;
   ```

3. Configure the application with environment variables. Replace the example
   values with the credentials created above and your
   [NPS API key](https://www.nps.gov/subjects/developer/get-started.htm).

   ```bash
   export SPRING_DATASOURCE_URL='jdbc:mysql://localhost:3306/parkd_user_management'
   export SPRING_DATASOURCE_USERNAME='parkd'
   export SPRING_DATASOURCE_PASSWORD='choose-a-password'
   export NPS_API_KEY='your-nps-api-key'
   ```

4. Start the application.

   ```bash
   ./gradlew bootRun
   ```

5. Open [http://localhost:8080](http://localhost:8080).

Hibernate creates and updates the required tables when the application starts.
The home page also imports park records from the NPS API into the local database.

> **Note:** Some NPS integrations still contain a development API key directly
> in their mapper classes. Replace those values for local development until all
> integrations use the `nps.api.key` property.

## Common Routes

| Route | Description |
| --- | --- |
| `/` | Home and featured parks |
| `/explore` | Browse parks |
| `/search` | Search by park name |
| `/alerts` | View current NPS alerts |
| `/register` | Create an account |
| `/login` | Sign in |
| `/profile` | View the signed-in user's profile |

## Testing

With the database configured, run the test suite using:

```bash
./gradlew test
```

## Project Structure

```text
src/
|-- main/java/com/notsauce/parkd/
|   |-- controllers/    # MVC request handlers
|   |-- mapper/         # NPS API clients and response mapping
|   `-- models/         # Domain models, services, and repositories
|-- main/resources/
|   |-- static/         # CSS and JavaScript
|   |-- templates/      # Thymeleaf views
|   `-- application.properties
`-- test/               # Automated tests
```

## Team

Built by Team Not Sauce as a LaunchCode Liftoff project.
