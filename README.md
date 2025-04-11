# DB-Schema-VH
# CORE TABLES (Entities and relationships)
Create table Tenant(
id UUID Primary Key,
name varchar(255) not null,
created_at timestamp default now()
);

Create table configs(
id UUID Primary Key, 
tenant_id UUID references tenant(id),
config_key varchar(255),
config_value text
);

Create table User(
id UUID Primary Key,
tenant_id UUID references tenant(id),
name VARCHAR(255)
email VARCHAR(255) UNIQUE 
Role varchar(50),
created_at timestamp default now()
);
