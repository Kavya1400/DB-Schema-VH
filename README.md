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

# Case and document management 

Create table case(
id UUID Primary Key,
user_id UUID references User(id),
tenant_id UUID references tenant(id),
title varchar(255),
description text,
created_at timestamp default now()
);

Create table case document (
id UUID primary key,
case_id UUID references case(id)
file_name varchar(255),
file_url text,
uploded_at timestamp default now()
);

create table CaseSummary(
id UUID primary key, 
case_id UUID references case(id),
summary text
);

create table ReportArtefcts (
id UUID primary key, 
case_summary_id UUID references CaseSummary(id);
artefact_type varchar(100),
content text
);

create table notification (
id UUID primary key, 
case_id UUID references case(id),
message text,
status varchar(50),
created_at timestamp default now()
);

# Persona simulation management 

Create table Trait(
id UUID Primary key,
name VARCHAR(255),
description text
);

create table PersonaPrompt(
id UUID primary key,
persona_id UUID references persona(ID),
prompt_text text
);

Create table CasePersonaSimulation(
id UUID Primary key,
case_persona_id UUID references CasePersona(id),
llm_version_id UUID,
response text
created_at timestamp default now()
);

# LLM Versioning 

Create Table LLM(
id UUID Primary Key,
name VARCHAR(255)
provider VARCHAR(255)
);

Create table LLMVersion(
id UUID Primary Key, 
llm,_id UUID references LLM(id),
version_tag VARCHAR(100)
release_notes text
);













