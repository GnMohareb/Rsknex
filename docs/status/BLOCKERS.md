# Blockers

- MySQL/MariaDB server binary not installed in Laragon (C:\laragon\bin\mysql\mysql-8.4.3-winx64 has only my.ini). Required for SimpleRisk baseline. Install MySQL 8.x or use Docker.
- Vendor/third-party dependency license inventory not complete.
- No CI configured yet.

- MySQL root credentials unknown; cannot verify clean install.

- PHP 8.4 (WindowsApps) lacks pdo_mysql, mbstring, curl, zip, gd, ldap, posix, max_input_vars; Laragon php 8.3 has no binary. Installing extensions or alternative PHP required for full install.
