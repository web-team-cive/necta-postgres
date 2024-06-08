# NECTA Tanzania Results Database

Welcome to the NECTA Tanzania Results Database project. This repository contains PostgreSQL database dumps of the NECTA exam results. Currently, the available results are for CSEE from 2019 to 2023, with more results to be added weekly. The goal is to include all results from 2003 to 2023.

## Getting Started

These instructions will help you set up and run the NECTA results database on your local machine or server.

### Prerequisites

- PostgreSQL (version 12 or later)
- Git

### Installation

1. **Clone the repository:**

   ```sh
   git clone https://github.com/web-team-cive/necta-postgres.git
   cd necta-postgres
   ```

2. **Create a new PostgreSQL database:**

   ```sh
   createdb -U postgres necta_results
   ```

3. **Restore the database from the dump file:**

   Navigate to the specific year and restore the corresponding dump file. For example, to restore the 2019 CSEE results:

   ```sh
   cd csee/2019
   pg_restore -U postgres -d necta_results database.dump
   ```

   Repeat the above step for other years as needed.

### Database Schema

The main table in the database is `form_four`, which contains the following columns:

- **regno** (text): Registration number of the student
- **gender** (text): Gender of the student
- **points** (text): Points scored by the student
- **division** (text): Division classification of the results
- **results** (text): Detailed results of the student
- **yr** (text): Year of the exam

### Usage

Once the database is restored, you can connect to it using any PostgreSQL client and query the results. Below is an example of how to connect and query the database using `psql`:

1. **Connect to the database:**

   ```sh
   psql -U postgres -d necta_results
   ```

2. **Run a sample query:**

   ```sql
   SELECT * FROM form_four WHERE yr = '2019';
   ```

### Application Development

You can now develop your applications (websites or apps) to display NECTA results using this database. Here are a few steps to integrate the database with your application:

1. **Database Connection:**

   Establish a connection to the PostgreSQL database from your application using the appropriate database driver or ORM (Object-Relational Mapping) for your programming language. Ensure you use the correct connection parameters (database name, user, password, host, port).

2. **Querying the Database:**

   Write SQL queries to fetch the results from the database tables. For example, to fetch all results for a particular year, you might query the `form_four` table.

3. **Displaying Results:**

   Format and display the results in your application's user interface. Ensure that the data is presented in a user-friendly manner.

4. **Example Code:**

   Here's an example of how you might connect to the database and query it using Python and the `psycopg2` library:

   ```python
   import psycopg2

   try:
       connection = psycopg2.connect(
           database="necta_results",
           user="postgres",
           password="yourpassword",
           host="127.0.0.1",
           port="5432"
       )
       cursor = connection.cursor()
       cursor.execute("SELECT * FROM form_four WHERE yr = '2019';")
       results = cursor.fetchall()
       for row in results:
           print(row)
   except Exception as error:
       print(f"Error: {error}")
   finally:
       if connection:
           cursor.close()
           connection.close()
   ```

### Contributing

We welcome contributions! If you have additional NECTA results or improvements, please fork the repository and create a pull request.

### License

This project is licensed under the MIT License.

### Acknowledgments

- [NECTA](https://www.necta.go.tz/) for providing the exam results.
- All contributors who have helped in creating and maintaining this project.

### Contact

For any questions or support, please open an issue in the repository or contact the maintainers directly.

---

**Note:** This repository is intended for educational and informational purposes only. Please ensure compliance with any relevant legal and privacy requirements when using the data.

![](https://komarev.com/ghpvc/?username=Project-Views&style=for-the-badge)
