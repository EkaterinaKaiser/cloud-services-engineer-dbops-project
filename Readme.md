Исходный репозиторий для выполнения проекта дисциплины "DBOps"

Выполненные запросы для создания пользователя для автотестов:

CREATE USER autotest WITH PASSWORD 'autotest-password';

\c store

GRANT USAGE ON SCHEMA public TO autotest;

GRANT SELECT, INSERT, UPDATE, DELETE ON ALL TABLES IN SCHEMA public TO autotest;

GRANT USAGE, SELECT ON ALL SEQUENCES IN SCHEMA public TO autotest;

ALTER DEFAULT PRIVILEGES IN SCHEMA public GRANT SELECT, INSERT, UPDATE, DELETE ON TABLES TO autotest;

ALTER DEFAULT PRIVILEGES IN SCHEMA public GRANT USAGE, SELECT ON SEQUENCES TO autotest;