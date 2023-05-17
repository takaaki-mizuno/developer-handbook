# Database design

This document outlines the standards to be adhered to when creating the data schema for relational databases (RDB) in services and systems developed within our organization.

Similar to our JSON over HTTP API Standard, the primary objective of these guidelines is to streamline maintenance through standardization and to prevent misunderstandings or disagreements stemming from divergent design philosophies. By implementing a unified set of rules, we not only facilitate easier maintenance but also mitigate potential disputes during the database schema design process.

We understand that these guidelines may differ from your personal design philosophy. However, if you are involved in project design and development for our organization, it's crucial that you adhere to these standards to ensure consistency across our database schemas.

If you believe these rules should be modified, we welcome your suggestions. You may discuss your proposal with our CTO and other senior members. If a consensus deems the proposed change to be beneficial, we will adjust the rules accordingly.

## Database System

Our primary database system utilizes the most recent version of PostgreSQL. Thus, the ensuing standards are predicated on PostgreSQL's structure and functionality.

## Naming Conventions for Tables

Table names should employ the plural form of the noun that the resource represents. For instance, we prefer 'users', 'organizations', and 'wallets' over their singular counterparts such as 'user' and 'organization'.

### Primary Key

The primary key should be denoted simply as id. While some might favor appending the singular form of the table name, like user_id, our convention is to stick with id.

In terms of the primary key's format, we utilize UUID v4 or BigInteger. Consistency in the primary key format is paramount across the entire project. The choice between UUID or a numeric sequence hinges on the project's characteristics. If you have tables that require sorting by ID in their generation order, opt for BigInt; in all other cases, use UUID.

When employing numeric sequences, always choose BigInt (64 bit) over Int (32 bit). This precaution minimizes the risk of numeric overflow in the future.

## Column Naming Conventions

Aim to keep column names concise yet descriptive. Single-word names are preferred, but when multiple words are necessary, use the snake_case format, such as user_id or access_token.

The column name should inherently hint at the kind of data it houses. Therefore, it's recommended to use commonly accepted names and maintain consistency for columns that convey the same meaning within the project.

## Date and Time Columns

Date and time-oriented columns should include the _at suffix, like `created_at` or `registered_at`.

Adopt Int as the data type and manage values with a UNIX timestamp. This approach simplifies parsing, is unaffected by time zones, and is compatible with most standard time libraries. While RDBMSs have specific types to handle DateTime, they vary in time zone handling, and the time zone value relies on the DB or OS configuration, potentially compromising portability.

However, using the Date type is acceptable for "date" data that doesn't involve time zones. But consider if storing only the date would suffice for future information requirements. For instance, a registration date might better be stored as a UNIX timestamp, anticipating the potential need for the exact time in the future.

## `created_at` and `updated_at` Columns

Each table must include `created_at` to timestamp record creation and `updated_at` to timestamp the latest record update. These timestamps should auto-populate upon record creation or update.

For these two columns, we use the TIMESTAMP type instead of Integer.

These columns serve strictly for logging and troubleshooting purposes and shouldn't influence business logic decisions in the service or system.

For example, do not use the created_at timestamp of users to determine a user's registration date and time. If you need to record a user's registration date and time, create a separate column (BigInteger type), such as `registered_at` or `posted_at`.

This approach circumvents potential unintended alterations to `created_at` and `updated_at` columns, like during data migration.

## Flag Columns

Flag columns should be prefixed with identifiers like `is_` or `has_`, making it clear that they represent a boolean value.

## Magic Numbers

Avoid using magic numbers as data stored in columns.

For instance, consider a table named `orders` with a `status` column that represents the order status. Do not use integers as the data type for this column, assigning meanings such as 1 for "order completed" and 2 for "delivery completed".

This practice is discouraged because it's impossible to understand the meaning without knowing what each number signifies, contradicting the principle that one should be able to glean the basic meaning from the table alone.

As such, the `status` column should store strings like `ordered` or `delivered`, using a string data type.

## Relationships

To denote relations between tables, use a foreign key. The name of this key should be the singular form of the table name concatenated with the column name. For example, use `user_id` to reference the `id` column of the `users` table from another table.

For many-to-many relationships, concatenate the singular form of one table name with the plural form of the other, like `user_roles`. This table would include two columns: `user_id` and `role_id`. To decide which table name to use in the singular form, consider the relationship between the tables and prioritize the more important data.

## Enums

Avoid using ENUM as it lacks extendability. Instead, employ string(varchar) and manage the contents within the code.

## Blobs

Refrain from storing binary data, such as images, directly within the table. Leverage Cloud Storage instead and only store the corresponding URLs in the table.

## Numeric Postfixes

Never resort to numerical postfixes like _1, _2. If you need to store up to three similar types of data within a single table, normalization is required. Create another table to store this data, ensuring it's capable of accommodating an increase in maximum size to four or more.

## Indexing

Be sure to create indices on columns that are frequently used in WHERE, JOIN, and ORDER BY clauses. This can significantly speed up database performance. However, don't overuse them as they can slow down the performance of data insertion and update operations.

## Empty values and Null values

Empty values ( such as empty string ) and null value should have different. Empty values should be treated as a valid value. Null values should be treated as a non-existent value.


