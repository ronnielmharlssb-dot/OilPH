# OilPH Fresh Build Notes

OilPH is a fresh Laravel application created for the system integration and architecture design project. The application code in this folder was rebuilt from a clean Laravel runtime scaffold and does not reuse the previous OilPH application files.

## Run

Use this when you only want to open the existing app and keep the current database data:

```powershell
cd "C:\xampp\htdocs\final laravel"
& "C:\xampp\php\php.exe" artisan serve --host=127.0.0.1 --port=8000
```

Open:

```text
http://127.0.0.1:8000/login
```

Accounts:

```text
User:  user@oilph.test / password
Admin: admin@oilph.test / password
```

## Database Commands

Use this after pulling or adding new migrations. It keeps existing data and only applies pending database changes:

```powershell
cd "C:\xampp\htdocs\final laravel"
& "C:\xampp\php\php.exe" artisan migrate
```

Use this only when you intentionally want to erase the database and restore demo/seed data:

```powershell
cd "C:\xampp\htdocs\final laravel"
& "C:\xampp\php\php.exe" artisan migrate:fresh --seed
```

Warning: `migrate:fresh --seed` deletes scanned stations, user reports, admin price edits, and any other saved database records before recreating demo data.

Before resetting, make a database backup:

```powershell
Copy-Item "database\database.sqlite" "database\database.backup.sqlite"
```

## Fresh Application Files

```text
routes/web.php
app/Http/Controllers/AuthController.php
app/Http/Controllers/DashboardController.php
app/Http/Controllers/StationController.php
app/Http/Controllers/StationImportController.php
app/Http/Controllers/PriceReportController.php
app/Http/Controllers/AdminController.php
app/Http/Middleware/EnsureUserIsAdmin.php
app/Models/Station.php
app/Models/PriceHistory.php
app/Models/PriceReport.php
resources/views/login.blade.php
resources/views/dashboard.blade.php
resources/views/stations/show.blade.php
resources/views/admin/dashboard.blade.php
database/migrations/2026_04_29_000001_create_oilph_tables.php
database/migrations/2026_04_29_000002_add_experience_fields_to_price_reports.php
database/migrations/2026_04_29_000003_add_service_rating_to_price_reports.php
database/seeders/DatabaseSeeder.php
```

## Features

- Separate user and admin interfaces.
- User login and registration.
- Browser geolocation for user station scanning.
- Google Places browser import for nearby detected gas stations.
- Distance radius toggle from 1 km to 25 km.
- Station sorting by best match, lowest regular price, and nearest station.
- Station scoring based on price, distance, ratings, amenities, service star ratings, queue time, and 24-hour availability.
- Google Maps directions links and route preview with fullscreen navigation panel.
- Station comparison cards showing regular, premium, and diesel availability.
- User station reports for fuel prices, amenities, service star rating, queue time, and comments.
- Admin dashboard for searching nearby stations and updating station fuel products and prices from any typed location.
- Price history records and animated price movement chart.
- Presentation-ready responsive UI with mobile layouts, hover movement, entry transitions, modal reporting, fullscreen directions, and animated price movement labels.

## Integration Mechanisms

1. Browser geolocation integration: the browser provides latitude and longitude to Laravel views and query parameters.
2. Google Maps directions integration: selected station coordinates are passed to Google Maps direction URLs.
3. Internal data integration: user reports, admin price updates, station records, and price history are connected through Laravel models and database relationships.

## Architecture

```text
Browser
  -> Laravel routes
  -> Controllers
  -> Eloquent models
  -> SQLite database
  -> Blade views

User flow
  -> Detect or enter location
  -> Scan stations by radius
  -> Compare prices and amenities
  -> Open station detail
  -> Submit station report with prices, amenities, service rating, and queue time

Admin flow
  -> Enter current or remote location
  -> Filter/search nearby monitored stations
  -> Review user station reports
  -> Update offered fuel products and prices
  -> Store price history for charting
```

## Verification

```powershell
& "C:\xampp\php\php.exe" artisan test
```

Current verification:

```text
12 tests passed / 53 assertions
```
