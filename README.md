# Student Grievance Portal

A Java 17, JSP, Servlet, PostgreSQL, and Tomcat 10.1 college grievance portal.

## Render deployment

The Docker image deploys the WAR as Tomcat's `ROOT.war`, so the Render service URL opens the portal directly at `/`.

Create or attach a Render PostgreSQL database and make sure the web service receives its connection string as `DATABASE_URL`. Render normally provides this automatically when the database is linked to the service. The application also accepts `JDBC_DATABASE_URL` or `DB_URL`. If a full URL is not available, configure these variables instead: `PGHOST`, `PGPORT`, `PGDATABASE`, `PGUSER`, and `PGPASSWORD`.

The application creates the required tables and demo accounts on the first successful database connection. The checked-in [PostgreSQL schema](database/grievance_portal.sql) can also be run manually.

After pushing changes, use Render's **Manual Deploy → Deploy latest commit** if automatic deployment is disabled. The service must expose port `8080`.

## Local setup

1. Install JDK 17, Maven, PostgreSQL, and Tomcat 10.1.
2. Create a PostgreSQL database and set `DATABASE_URL`, or set `PGHOST`, `PGPORT`, `PGDATABASE`, `PGUSER`, and `PGPASSWORD`.
3. Optionally run `database/grievance_portal.sql` to insert the sample complaints.
4. Run `mvn clean package`.
5. Copy `target/StudentGrievancePortal.war` into Tomcat's `webapps` folder.
6. Start Tomcat.
7. Open `http://localhost:8080/StudentGrievancePortal/` for a normal local WAR deployment.

Demo admin: `admin@college.com` / `admin123`

Demo student: `student@college.com` / `student123`

## Important security note

Demo passwords are intentionally simple for college demonstration. For production, use password hashing, rotate demo credentials, and keep database credentials in environment variables rather than source code.
