# Database Structure:

## Binaries

This tables stores information about each binary, the source code URL, build configs and path of this binary

| Name            | Type         | Schema                       |
|-----------------|--------------|------------------------------|
| id              | INTEGER      | "id" INTEGER NOT NULL        |
| file_name       | VARCHAR(32)  | "file_name" VARCHAR(32)      |
| platform        | VARCHAR(8)   | "platform" VARCHAR(8)        |
| build_mode      | VARCHAR(8)   | "build_mode" VARCHAR(8)      |
| toolset_version | VARCHAR(4)   | "toolset_version" VARCHAR(4) |
| github_url      | VARCHAR(128) | "github_url" VARCHAR(128)    |
| optimization    | VARCHAR(16)  | "optimization" VARCHAR(16)   |
| pushed_at       | INTEGER      | "pushed_at" INTEGER          |
| size            | INTEGER      | "size" INTEGER               |
| source_file     | VARCHAR(128) | "source_file" VARCHAR(128)   |
| path            | VARCHAR(128) | "path" VARCHAR(128)          |



## Functions:

This table stores the functions within each binary, if user want more detailed information, they can refer to `Lines` and `RVAs` tables.


| Name            | Type         | Schema                  |
|-----------------|--------------|-------------------------|
| id              | INTEGER      | "id" INTEGER NOT NULL   |
| name            | VARCHAR(128) | "name" VARCHAR(128)     |
| intersect_ratio | FLOAT        | "intersect_ratio" FLOAT |
| binary_id       | INTEGER      | "binary_id" INTEGER     |


## Lines:


This table is a break down of mapping from each source code line to function

| Name        | Type    | Schema                |
|-------------|---------|-----------------------|
| id          | INTEGER | "id" INTEGER NOT NULL |
| line_number | INTEGER | "line_number" INTEGER |
| length      | INTEGER | "length" INTEGER      |
| source_code | TEXT    | "source_code" TEXT    |
| function_id | INTEGER | "function_id" INTEGER |



## PDBs:

This table indicates teh PDB file relationship for each binary, `binary_id` referring to `Binaries` table `id` column, `pdb_path` is the pdb file path


| Name      | Type         | Schema                  |
|-----------|--------------|-------------------------|
| id        | INTEGER      | "id" INTEGER NOT NULL   |
| binary_id | INTEGER      | "binary_id" INTEGER     |
| pdb_path  | VARCHAR(128) | "pdb_path" VARCHAR(128) |


## RVAs:

This table indicates teh RVA address for each function, `function_id` points to `Functions` table `id` column

| Name        | Type    | Schema                |
|-------------|---------|-----------------------|
| id          | INTEGER | "id" INTEGER NOT NULL |
| start       | BIGINT  | "start" BIGINT        |
| end         | BIGINT  | "end" BIGINT          |
| function_id | INTEGER | "function_id" INTEGER |
