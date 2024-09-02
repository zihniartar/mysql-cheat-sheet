
# MySQL Cheat Sheet
## Datenbank sichern

### Eine einzelne Datenbank sichern
```bash
mysqldump -u [Benutzername] -p [Datenbankname] > /pfad/zur/sicherung/datei.sql
```

Beispiel:
```bash
mysqldump -u root -p mydatabase > /backups/mydatabase_backup.sql
```

### Alle Datenbanken sichern

```bash
mysqldump -u [Benutzername] -p --all-databases > /pfad/zur/sicherung/alle_datenbanken.sql
```

Beispiel:
```bash
mysqldump -u root -p --all-databases > /backups/all_databases_backup.sql
```

### Sicherung komprimieren
```bash
mysqldump -u [Benutzername] -p [Datenbankname] | gzip > /pfad/zur/sicherung/datei.sql.gz
```

Beispiel:
```bash
mysqldump -u root -p mydatabase | gzip > /backups/mydatabase_backup.sql.gz
```

## Automatische Sicherung mithilfe eines Cron-Jobs

### Crontab-Datei öffnen
```bash
crontab -e
```

### Cron-Job hinzufügen 
(z.B. tägliche Sicherung um 2 Uhr nachts):
```bash
0 2 * * * mysqldump -u root -p[Passwort] mydatabase | gzip > /backups/mydatabase_backup_$(date +\%F).sql.gz
```

## Datenbank wiederherstellen

### Eine einzelne Datenbank wiederherstellen

#### Alte Datenbank löschen
```bash
DROP DATABASE IF EXISTS YourDatabaseName;
CREATE DATABASE YourDatabaseName;
```

#### Importieren der Sicherung in die Datenbank
```bash
mysql -u [Benutzername] -p YourDatabaseName < /pfad/zur/sicherung/datei.sql

```

### Datenbank zurückspielen, wenn sie bereits existiert
Importbefehl direkt verwenden

```bash
mysql -u [Benutzername] -p YourDatabaseName < /pfad/zur/sicherung/datei.sql
```

### Wiederherstellung von komprimierten Sicherungen

```bash
gunzip < /pfad/zur/sicherung/datei.sql.gz | mysql -u [Benutzername] -p YourDatabaseName

```
