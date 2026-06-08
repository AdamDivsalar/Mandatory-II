# Mandatory II - Læringsmål

**Adam Leon Divsalar**
Tech 1, 2. semester datamatiker, KEA

Alle læringsmål fra "Learning Goals"-kolonnen i semesterplanen er skrevet af nedenfor.
Ved "can"-mål viser jeg et eksempel og skriver "Det kan jeg!". Ved "knows/understands"
skriver jeg stikord til mundtlig forklaring. Dækker uge 1, 2, 3, 5, 6, 7, 8 og 9.

---

## Uge 1 - Terminal og Git

**Can navigate the terminal: ls, cd, whoami, pwd.**

```bash
pwd            # viser stien til mappen jeg står i
ls -la         # lister alt, også skjulte filer
cd projects    # går ned i en mappe
cd ..          # går et niveau op
whoami         # viser mit brugernavn
```

Det kan jeg!

**Can create, delete files / folders: mkdir, rm, cp, mv, touch, nano.**

```bash
mkdir test          # opret mappe
touch file.txt      # opret tom fil
nano file.txt       # åbn fil i terminal-editor
cp file.txt copy.txt    # kopier fil
mv copy.txt navn.txt    # omdøb/flyt fil
rm file.txt         # slet fil
rm -r test          # slet mappe + indhold
```

Det kan jeg!

**Can use the following basic terminal commands: cat, wc, uniq, sort.**

```bash
cat file.txt        # printer hele filen
wc -l file.txt      # tæller linjer
sort navne.txt      # sorterer alfabetisk
sort navne.txt | uniq   # fjerner gentagne (nabo-)linjer
```

- `uniq` fjerner kun ens linjer der står ved siden af hinanden, så man sorterer først.

Det kan jeg!

**Can create a new repository in your prefered Git provider.**

- Gå til GitHub, klik "New repository", giv den et navn, klik "Create repository".
- Kobl en lokal mappe til:

```bash
git init
git remote add origin git@github.com:brugernavn/oenskeskyen.git
git branch -M main
git push -u origin main
```

Det kan jeg!

**Can perform basic Git operations: clone, add, commit, push, pull.**

```bash
git clone <repo-url>      # hent repository
git add .                # stage ændringer
git commit -m "besked"   # gem lokalt
git push                 # send op til remote
git pull                 # hent + merge nyeste
```

Det kan jeg!

---

## Uge 2 - Hardware, Software, Talsystemer, Encoding

**Can list the main hardware components of a computer, their functions and the Von Neumann architecture.**

Hovedkomponenter:

- CPU - udfører instruktioner (computerens "hjerne"). Indeholder ALU (regning),
  control unit (styring) og registre (midlertidig lagring).
- RAM - hurtig, flygtig hukommelse til det program der kører lige nu. Tømmes ved slukning.
- Lagring (SSD/HDD) - permanent lagring.
- Bundkort/bus - binder komponenterne sammen og flytter data.
- I/O - input (tastatur, mus) og output (skærm, printer).

Von Neumann-arkitektur:

- Kode og data ligger i den samme hukommelse.
- CPU'en kører en fast cyklus: fetch -> decode -> execute.
- Flaskehalsen: data og instruktioner deler den samme bus til RAM.

**Can explain how computers work, starting from hardware all the way to software.**

Computeren fungerer i lag:

- Hardware - de fysiske dele (CPU, RAM, disk).
- Operativsystem - styrer hardwaren og giver services (Windows, Linux).
- Programmer/apps - det brugeren bruger (fx Ønskeskyen).
- Brugerinput - sætter handlinger i gang.

Flow: jeg klikker en knap -> OS modtager input -> programmet sender instruktioner ->
CPU'en behandler -> resultatet vises på skærmen.

**Can talk about processes in operating systems.**

- En proces er et kørende program.
- Hver proces har sin egen hukommelse og sin egen tilstand (running, waiting, terminated).
- OS'et styrer processer med scheduling (hvem kører nu) og context switching (skift mellem dem).
- Det giver multitasking - flere programmer kører "samtidig".
- En proces kan have flere tråde der deler procesens hukommelse.

**Can talk about different number representations: Binary, Hexadecimal, Decimal.**

- Binær (base 2): kun 0 og 1. Det computeren regner i. Eksempel: 1101 = 13.
- Decimal (base 10): cifre 0-9. Det vi mennesker bruger.
- Hexadecimal (base 16): 0-9 og A-F. Kompakt måde at skrive binær på. Eksempel: D = 13.

```
Decimal:      13
Binær:        1101    (8 + 4 + 0 + 1)
Hexadecimal:  D
```

Det kan jeg, og jeg kan regne frem og tilbage i hånden.

**Can bring up real-world use cases for different number representations.**

- Binær: inde i hardwaren (logiske kredsløb, hukommelse).
- Decimal: brugerflader og hverdagsregning, fx priser i Ønskeskyen.
- Hex: farvekoder i web (#FF0000 = rød), hukommelsesadresser, MAC-adresser, debugging.

Det kan jeg!

**Can explain different charsets like ASCII and Unicode and how they differ.**

- ASCII: bruger 7 bit (128 tegn). Dækker engelske bogstaver, tal og symboler, men ikke æ, ø, å. Eksempel: A = 65.
- Unicode: dækker stort set alle sprog og symboler, også emojis. Lagres typisk som UTF-8.
- Forskel: ASCII er begrænset, Unicode er universelt og bagudkompatibelt med ASCII.

Derfor satte jeg `DEFAULT CHARACTER SET utf8` på databasen i Mandatory I, ellers bliver
danske tegn ødelagt.

---

## Uge 3 - Databaser og intro til SQL

**Knows about different types of databases and their use cases.**

Relationelle databaser (SQL):

- Eksempel: MySQL.
- Data i tabeller (rækker + kolonner), faste skemaer, relationer via nøgler.
- Bruges til: struktureret data, bank-systemer, web-apps (fx Ønskeskyen).

NoSQL-databaser:

- Eksempel: MongoDB (dokumenter), Redis (key-value), Neo4j (graf).
- Fleksibel struktur (JSON-lignende dokumenter).
- Bruges til: store skalerbare apps, løst struktureret data.

Tommelfinger: relationelt når relationer og konsistens er vigtigt, NoSQL når
fleksibilitet og skalering vejer tungest.

**Can setup a new MySQL database and connect to it.**

```sql
CREATE DATABASE oenskeskyen DEFAULT CHARACTER SET utf8;
USE oenskeskyen;
```

```bash
mysql -u root -p
```

Det kan jeg!

**Can create DDL statements to create tables.**

```sql
CREATE TABLE users (
    id    INT AUTO_INCREMENT PRIMARY KEY,
    name  VARCHAR(100),
    email VARCHAR(100)
);
```

- DDL = Data Definition Language (CREATE, ALTER, DROP).

Det kan jeg!

**Can create DML (SELECT, INSERT) statements.**

```sql
INSERT INTO users (name, email) VALUES ('Alice', 'alice@example.com');
SELECT * FROM users;
```

- DML = Data Manipulation Language (SELECT, INSERT, UPDATE, DELETE).

Det kan jeg!

**Can use WHERE clause to filter results.**

```sql
SELECT * FROM users WHERE name = 'Alice';
```

Det kan jeg!

---

## Uge 5 - SQL II (nøgler, aggregater, joins, PRs)

**Can define Primary Keys.**

- En primærnøgle identificerer hver række entydigt.
- Den skal være unik og NOT NULL.

```sql
CREATE TABLE users (
    id   INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100)
);
```

Det kan jeg!

**Understands how Foreign Keys work.**

- En fremmednøgle binder en tabel til en anden.
- Den sikrer referentiel integritet - man kan kun pege på data der findes.

```sql
CREATE TABLE orders (
    id      INT AUTO_INCREMENT PRIMARY KEY,
    user_id INT,
    FOREIGN KEY (user_id) REFERENCES users(id)
);
```

- Her skal `orders.user_id` findes i `users.id`.

**In SELECT statements, can use (with moderate help):**

LIMIT, ORDER BY, GROUP BY:

```sql
SELECT * FROM users LIMIT 5;
SELECT * FROM users ORDER BY name ASC;
SELECT user_id, COUNT(*) FROM orders GROUP BY user_id;
```

Aggregatfunktioner (COUNT, SUM, AVG, MIN, MAX):

```sql
SELECT COUNT(*) FROM users;
SELECT AVG(price) FROM products;
SELECT MIN(price), MAX(price) FROM products;
```

Pattern matching med LIKE og wildcards (% = mange tegn, _ = ét tegn):

```sql
SELECT * FROM users WHERE name LIKE 'A%';        -- starter med A
SELECT * FROM users WHERE email LIKE '%@gmail.com';
```

JOIN til at samle data fra flere tabeller:

```sql
SELECT users.name, orders.id
FROM users
JOIN orders ON users.id = orders.user_id;
```

Det kan jeg (og jeg brugte dem alle i Mandatory I).

**Can create inner, left and right joins after looking up the syntax.**

```sql
-- INNER: kun rækker med match i begge tabeller
SELECT * FROM users INNER JOIN orders ON users.id = orders.user_id;

-- LEFT: alle users, også dem uden orders
SELECT * FROM users LEFT JOIN orders ON users.id = orders.user_id;

-- RIGHT: alle orders, også dem uden user
SELECT * FROM users RIGHT JOIN orders ON users.id = orders.user_id;
```

Det kan jeg!

**Can create DDL statements to create tables with constraints: PRIMARY KEY, AUTO_INCREMENT, FOREIGN KEY, UNIQUE, NOT NULL.**

```sql
CREATE TABLE users (
    id    INT AUTO_INCREMENT PRIMARY KEY,
    email VARCHAR(100) UNIQUE NOT NULL,
    name  VARCHAR(100) NOT NULL
);

CREATE TABLE orders (
    id      INT AUTO_INCREMENT PRIMARY KEY,
    user_id INT,
    FOREIGN KEY (user_id) REFERENCES users(id)
);
```

Det kan jeg!

**Can create DML (UPDATE, DELETE) statements.**

```sql
UPDATE users SET name = 'Bob' WHERE id = 1;
DELETE FROM users WHERE id = 1;
```

- Husk altid WHERE, ellers rammer det hele tabellen.

Det kan jeg!

**Can create a pull request.**

```bash
git checkout -b feature-branch
git add .
git commit -m "Add feature"
git push origin feature-branch
```

- Gå til GitHub, klik "Compare & pull request", skriv en beskrivelse, submit.

Det kan jeg!

---

## Uge 6 - Advanced Git, Branching, YAML, GitHub Actions

**Understands different Git workflows such as GitHub Flow.**

- Lav en branch ud fra main.
- Lav ændringer på den branch.
- Commit og push.
- Åbn en pull request.
- Review + merge ind i main.

Kerneidé:

- main skal altid kunne deployes.
- Arbejdet sker i feature-branches.

**Can solve a merge conflict.**

- Opstår når to branches har ændret de samme linjer. Git markerer det med
  `<<<<<<<`, `=======`, `>>>>>>>`.
- Åbn filen, vælg hvad der skal beholdes (eller kombiner), fjern markørerne.
- Marker som løst:

```bash
git add .
git commit -m "Resolve merge conflict"
```

Det kan jeg!

**Can write YAML.**

```yaml
name: My Workflow
on: [push]
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Say hello
        run: echo "Hello world"
```

Regler:

- Indrykning med mellemrum, ikke tabs.
- Key-value format: `key: value`.
- Lister bruger `-`.

Det kan jeg!

**Understands what GitHub Actions are and can breakdown workflows into runners, jobs, and steps.**

- Et værktøj til at automatisere opgaver (build, test, deploy) inde i GitHub.

Opdeling:

- Workflow - hele YAML-filen i `.github/workflows/`.
- Runner - maskinen jobbet kører på (fx ubuntu-latest).
- Job - en gruppe steps.
- Step - en enkelt kommando/opgave (`run`) eller en færdig action (`uses`).

```yaml
jobs:
  build:
    runs-on: ubuntu-latest   # runner
    steps:
      - run: echo "Step 1"
      - run: echo "Step 2"
```

**Can give use cases for GitHub Actions.**

- CI (Continuous Integration): kør tests automatisk ved hvert push.
- CD (Continuous Deployment): deploy app til server eller cloud (Azure).
- Andre: tjekke kodeformat/linting, sende notifikationer.

Det kan jeg give eksempler på!

---

## Uge 7 - Azure Web App Deployment

**Understands different cloud service models: IaaS, PaaS, SaaS.**

IaaS (Infrastructure as a Service):

- Du styrer: OS, runtime, apps.
- Udbyderen styrer: hardware, netværk.
- Eksempel: Azure Virtual Machines. Som at leje en computer i skyen.

PaaS (Platform as a Service):

- Du styrer: din applikation.
- Udbyderen styrer: OS, runtime, infrastruktur.
- Eksempel: Azure App Service. Du uploader bare kode, resten klares.

SaaS (Software as a Service):

- Du bruger bare softwaren, udbyderen styrer alt.
- Eksempel: Gmail. Som at bruge en app i browseren.

**Can deploy a web application to Azure App Service.**

- Opret en App Service i Azure.
- Vælg runtime (Java) og region.
- Kobl GitHub-repoet til og opsæt deployment via GitHub Actions.
- Push kode -> appen deployes automatisk.

```yaml
- name: Build with Maven
  run: mvn clean package -DskipTests

- name: Deploy to Azure Web App
  uses: azure/webapps-deploy@v3
  with:
    app-name: 'oenskeskyen'
    publish-profile: ${{ secrets.AZURE_PUBLISH_PROFILE }}
    package: 'target/*.jar'
```

Det kan jeg! Ønskeskyen kører deployet på Azure App Service.

**Understands the flow from pushing, GitHub Actions running, building the project and deployment to Azure.**

1. Jeg pusher kode til main.
2. GitHub Actions trigges automatisk (på `on: push`).
3. En runner spinner op, checker koden ud, sætter Java/Maven op.
4. Build-step: Maven bygger projektet til en jar (`mvn clean package`).
5. Deploy-step: jar'en udrulles til Azure App Service med en publish profile fra GitHub Secrets.
6. Azure starter den nye version, og appen er live.

- Pointe: hemmeligheder (publish profile, db-password) ligger i GitHub Secrets og
  Azure-config, ikke i koden.

---

## Uge 8 - Database i Spring + MySQL i Azure

**Adding a database to a Spring Project.**

- Tilføj MySQL-driver og Spring JDBC i `pom.xml`.
- Sæt forbindelsen op i `application.properties`.
- Brug `JdbcTemplate` i repositories.

```properties
spring.datasource.url=jdbc:mysql://localhost:3306/oenskeskyen
spring.datasource.username=${DB_USER}
spring.datasource.password=${DB_PASSWORD}
```

```java
@Repository
public class UserRepository {
    private final JdbcTemplate jdbcTemplate;

    public UserRepository(JdbcTemplate jdbcTemplate) {
        this.jdbcTemplate = jdbcTemplate;
    }

    public List<User> findAll() {
        return jdbcTemplate.query("SELECT * FROM users",
            (rs, rowNum) -> new User(rs.getInt("id"), rs.getString("email")));
    }
}
```

Det kan jeg!

**Setting up a database in Azure.**

- Opret en Azure Database for MySQL (flexible server) i portalen.
- Sæt admin-bruger og password.
- Åbn firewall-regler så min egen IP og App Service kan forbinde.
- Opret databasen og kør DDL-scripts mod den.

**Can set up a database in Azure and connect it to an Azure App Service project with a guide.**

- Sæt forbindelsesoplysningerne som app settings / environment variables i Azure (ikke i koden).
- Spring læser dem via `${...}`:

```properties
spring.datasource.url=jdbc:mysql://oenskeskyen-db.mysql.database.azure.com:3306/oenskeskyen?useSSL=true
spring.datasource.username=${DB_USER}
spring.datasource.password=${DB_PASSWORD}
```

- `DB_USER` og `DB_PASSWORD` sættes som app settings i App Service.
- Så er appen i skyen koblet til databasen i skyen.

Det kan jeg med en guide (hvilket også er det målet kræver).

---

## Uge 9 - Database Transactions (Concurrency, ACID, Threads)

**Is able to go through scenarios that can cause concurrency problems in databases.**

Typiske problemer når flere ting sker samtidig:

- Dirty read: man læser data en anden har ændret men ikke committet endnu.
- Non-repeatable read: samme række læses to gange og giver forskellige værdier.
- Phantom read: samme query giver nye rækker anden gang.
- Lost update: to skriver til samme værdi, og den ene overskriver den andens ændring.
- Deadlock: to transaktioner venter på hinandens låse og kommer aldrig videre.

Eksempel: to brugere reserverer det sidste sæde samtidig, og uden styring får begge "ja".

**Can explain what ACID is and why it solves concurrency problems for databases.**

ACID = fire egenskaber en transaktion skal have:

- Atomicity: enten kører hele transaktionen, eller intet af den (rollback ved fejl).
- Consistency: databasen går fra én gyldig tilstand til en anden, constraints overholdes.
- Isolation: samtidige transaktioner forstyrrer ikke hinanden.
- Durability: når noget er committet, er det gemt permanent, også hvis strømmen går.

Hvorfor det løser problemerne: Atomicity/rollback fjerner halve og lost updates,
Isolation forhindrer dirty/non-repeatable/phantom reads. SQL-databaser (MySQL) er
ACID-compliant; nogle NoSQL bruger i stedet BASE med "eventual consistency".

Det kan jeg forklare!

**Is aware of the possibility to define transactions in SQL and JDBC.**

I rå JDBC: slå auto-commit fra, kør queries, commit (eller rollback ved fejl):

```java
connection.setAutoCommit(false);
try {
    statement.executeUpdate("UPDATE seats SET status = 'reserved' WHERE seat_id = 1");
    connection.commit();    // alt lykkedes
} catch (SQLException e) {
    connection.rollback();  // noget fejlede -> fortryd
}
```

I Spring: brug `@Transactional`, så styrer Spring selv commit/rollback:

```java
@Transactional
public void reserveSeat(int seatId) {
    // kaster metoden en exception, ruller Spring automatisk tilbage
}
```

Jeg er bevidst om det. Målet er "is aware", ikke at bygge det fra bunden.

**...and atomic structures (tråde / atomare operationer).**

- En atomar operation sker enten helt eller slet ikke - den kan ikke afbrydes halvvejs.
- Vigtigt når flere tråde rører samme data samtidig (ellers race condition).
- Samme grundtanke som atomicity i databaser, bare på kode-niveau. I kode løses det
  med låse eller atomare typer; i databasen med transaktioner.

---

## Egenvurdering

- De fleste "can"-mål sidder fint, fordi jeg har brugt dem i Mandatory I (SQL) og i
  Ønskeskyen (Spring, Azure, GitHub Actions).
- Det jeg vil læse lidt ekstra op på: hurtig talsystem-omregning i hånden, Azure MySQL
  flexible server uden guide, og at forklare hele deploy-flowet roligt i rækkefølge.
- Resten føler jeg mig klar til at vise mundtligt og med kode.
