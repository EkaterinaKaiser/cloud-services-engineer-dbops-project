Виртуальная машина, доступ к которой выдал тренажер - недоступна по 22 порту.
Поэтому все разворачивалось на локальной виртуалке.
Для автотестов был создан локальный раннер на виртуалке.



Выполненные запросы для создания пользователя для автотестов:

CREATE USER autotest WITH PASSWORD 'autotest-password';

\c store

GRANT USAGE ON SCHEMA public TO autotest;

GRANT SELECT, INSERT, UPDATE, DELETE ON ALL TABLES IN SCHEMA public TO autotest;

GRANT USAGE, SELECT ON ALL SEQUENCES IN SCHEMA public TO autotest;

ALTER DEFAULT PRIVILEGES IN SCHEMA public GRANT SELECT, INSERT, UPDATE, DELETE ON TABLES TO autotest;

ALTER DEFAULT PRIVILEGES IN SCHEMA public GRANT USAGE, SELECT ON SEQUENCES TO autotest;


Запрос из шага 10:

SELECT 
    DATE(o.date_created) as order_date,
    SUM(op.quantity) as total_sausages_sold
FROM orders o
JOIN order_product op ON o.id = op.order_id
WHERE o.date_created >= DATE_TRUNC('week', CURRENT_DATE - INTERVAL '1 week')
  AND o.date_created < DATE_TRUNC('week', CURRENT_DATE)
  AND o.status != 'cancelled'
GROUP BY DATE(o.date_created)
ORDER BY order_date;