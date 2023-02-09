
SELECT * FROM pg_roles WHERE lower(rolname)='UserName';


SELECT * FROM pg_database WHERE datname=lower('DatabaseName');
