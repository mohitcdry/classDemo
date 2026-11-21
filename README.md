# StyleSnap

An ASP.NET Web Forms (.NET Framework 4.8) e-commerce demo: product catalog,
cart, checkout, user accounts with roles (Member / Admin), and optional
integrations for Google login, Stripe/Khalti payments, email, and an AI try-on.

## Prerequisites

- Visual Studio 2022 (ASP.NET and web development workload)
- .NET Framework 4.8
- SQL Server (Express or LocalDB) with Windows authentication

## Setup

1. **Database** — open `snapStyle/Database/StyleSnapDB.sql` in SQL Server
   Management Studio and run it (F5), or:
   ```
   sqlcmd -S localhost -E -i snapStyle/Database/StyleSnapDB.sql
   ```
   It creates `StyleSnapDB` with all tables, stored procedures, and seed data.
   The connection string in `Web.config` expects `Server=localhost` with
   Windows auth; adjust it if your SQL Server instance differs.

2. **App config** — copy the template to the real config file:
   ```
   copy snapStyle\appsettings.config.template snapStyle\appsettings.config
   ```
   The app runs with these values empty. Fill them only to enable the optional
   integrations (Google login, Stripe, Khalti, email, Gemini try-on).

3. **Run** — open `snapStyle/SnapStyle.sln` in Visual Studio and press F5.

## Demo accounts

Seeded login accounts (all share the same password):

| Email                   | Role   |
|-------------------------|--------|
| admin@stylesnap.com     | Admin  |
| member@stylesnap.com    | Member |
| demo@stylesnap.com      | Member |

> Note: no real API keys or personal credentials are included in this
> submission. All third-party secrets have been removed; see
> `appsettings.config.template` for the keys each integration expects.

## Password hashing

Passwords are hashed with PBKDF2 (HMAC-SHA256, 100,000 iterations, 128-bit
random salt) in `snapStyle/Services/PasswordHasher.cs`. Stored format:
`v1.{iterations}.{saltBase64}.{hashBase64}`.
