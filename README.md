# E-Commerce System

A PHP and MySQL storefront for a small business. The application uses an MVC-style structure with separate controllers, services, models, and templates.

## Features

- Browse, search, sort, and filter a paginated product catalog.
- Manage a session-based shopping cart and complete a multi-step checkout, including guest checkout.
- Register and manage an account, addresses, orders, and wishlists; submit product reviews.
- Manage products, categories, orders, users, and sales reports in the admin area.
- Use coupons, newsletter subscriptions, inventory tracking, order confirmation emails, and PDF invoices.
- Process payments through the PayPal sandbox.

## Requirements

- PHP 8.0 or later, with `mysqli` and `mbstring` enabled.
- MySQL with support for foreign keys and full-text indexes.
- PHP cURL for PayPal checkout.
- A configured local mail transport if you want the application to send email.

There is no Composer dependency manifest; the application uses PHP's built-in libraries and extensions.

## Get started

Run these commands from the repository root, replacing the database name or credentials as needed:

1. Create a MySQL database and user, then import the schema and sample catalog:

   ```sh
   mysql -u root -p -e "CREATE DATABASE ecommerce CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;"
   mysql -u root -p ecommerce < sql/schema.sql
   mysql -u root -p ecommerce < sql/seed.sql
   ```

2. Set the connection details in [`config/database.php`](config/database.php) to match your local MySQL user. The tracked config contains development defaults; do not use them for a public deployment.

3. Set `base_url` in [`config/app.php`](config/app.php) to `/` for the local server command below, or to the URL path where you deploy the `public/` directory.

4. Start PHP's development server with the public directory as its document root:

   ```sh
   php -S 127.0.0.1:8000 -t public
   ```

5. Open [http://127.0.0.1:8000](http://127.0.0.1:8000). Register an account to try the storefront. To test PayPal checkout, add sandbox credentials in [`config/paypal.php`](config/paypal.php). Configure [`config/mail.php`](config/mail.php) and your PHP mail transport if you need email delivery.

The sample data creates an administrator record, but does not document a login password. Set a secure password for an authorized admin account before using the admin area at `/admin/login.php`.

## Project layout

- `public/` — web entry points; configure your web server's document root here.
- `admin/` — administrator actions.
- `controllers/`, `services/`, `models/` — application logic and data access.
- `templates/` — storefront, account, checkout, and admin views.
- `config/` — application, database, mail, session, and PayPal settings.
- `sql/` — database schema and optional sample data.

## Help

For setup questions or to report a bug, [open an issue](https://github.com/VoidLance/course-files-php-e-commerce-system/issues). The code and SQL files linked above are the project's implementation and setup references.

## Contributing and maintenance

The repository is maintained by its owner and welcomes contributions. There is no separate contribution guide: please open an issue to discuss larger changes, then submit a pull request with a clear description. Keep changes focused and verify PHP syntax before submitting:

```sh
find . -name '*.php' -print0 | xargs -0 -n1 php -l
```

No automated test suite is included at this time. See [`sql/schema.sql`](sql/schema.sql) and [`sql/seed.sql`](sql/seed.sql) for the database structure and sample records. No license file is currently included.
