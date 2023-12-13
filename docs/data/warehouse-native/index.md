---
title: Warehouse-native Amplitude
---
!!! beta
    Warehouse-native Amplitude is a beta feature, and not generally available.

Warehouse-native Amplitude (WNA) is a version of Amplitude that enables you to create custom analyses with data models based on data already in your data warehouse. Like standard Amplitude, Warehouse-native Amplitude helps you gain insight into user behavior, identify trends, and make data-driven decisions to improve your business with data you already have.

## Create a Warehouse-native project

To get started with Warehouse-native Amplitude, an Administrator in your organization must create a Warehouse-native Project.

1. In the Amplitude app, navigate to **Data**.
2. Click the project selector dropdown, and click **Create new Warehouse Native Project**.
3. In the modal that appears, provide a descriptive name for the project.
4. Click **Finish**. Amplitude creates the project.
5. Update the project's permissions to allow access to other members of your organization.

## Connect to Snowflake

When the Warehouse-native project is ready, connect Amplitude to your Snowflake data warehouse.

Select the method to provide Amplitude with access to your data. Amplitude recommends **Data Share**. For more information, see [Connection types](#connection-types) below. This option impacts the way you configure Warehouse-native Amplitude, and associated costs.

Warehouse-native Amplitude supports one Snowflake connection per project.

### Snowflake data share

With Snowflake data share, you can share databases, schemas, tables, and views with Amplitude.

#### Amplitude configuration

1. TBD

#### Snowflake configuration

1. TBD

### Snowflake (direct connection)

In a direct connection, Snowflake requires that Amplitude use a service account to access the data in your Snowflake instance.

## Query performance and optimization

Amplitude recommends the following to improve performance and reduce latency.

- Use clustering keys in Snowflake. For more information, see Snowflake's documentation [Clustering Keys & Clustered Tables](https://docs.snowflake.com/en/user-guide/tables-clustering-keys)
- Use the `event time` column as a part of the clustering key, since most queries use this field.

## Create your first data model

In Amplitude, data models are the building blocks of analyses. An Amplitude data model is a table or view in your Snowflake instance that you can use to create queries and reports. Amplitude supports analyses that reference more than one data model.

Amplitude supports the following data model types:

| Type                          | Mandatory fields                           | Description                                                                                                                                                                                                   |
| ----------------------------- | ------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Events                        | Unique ID <br /> Timestamp (TIMESTAMP_NTZ) | A specific action or interaction that's associated with a timestamp. Amplitude uses this value to understand the project and organization's MTU count, and informs how Amplitude counts uniques in Analytics. |
| User Properties (Current)     | Unique ID                                  | Traits and attributes associated with an individual user at present. For example, current preferences or recent interactions.                                                                                 |
| User Properties (Historical)  | Unique ID <br />Start Time <br /> End Time | Traits and attributes associated with a user over time. For example, historical preferences or past interactions.                                                                                            |
| Group Properties (Current)    | Unique ID                                  | Characteristics and attributes of a group at present. For example, name, description, or membership composition.                                                                                              |
| Group Properties (Historical) | Unique ID <br />Start Time <br /> End Time | Characteristics and attributes of a group over time. For example, previous name, description, or past membership composition.                                                                                 |
| Event Properties              | Event ID                                   | Traits and attributes associated with a specific recorded action or interaction.                                                                                                                              |

To create a data model:

1. Navigate to the **Data** tab of your Warehouse-native project.
2. Click **Add Models**.
3. Select the table to connect. Select either **Table Selection** or **SQL Query**.
   
      - For **Table Selection**, choose the table or view from the respective dropdowns to populate the content. Values in the dropdowns reflect the access you provide to the service account or credentials in use for Warehouse-native Amplitude.
      - For **SQL Query**, provide your own query to join tables, filter rows, or incorporate more advanced SQL to create the base table.

4. Select the data type of the model.
5. Depending on the data type you select, map any mandatory fields in the table above to matching fields in Amplitude.
6. Select or deselect columns in the rest of the table. Columns you deselect aren't shared with Amplitude. Update your column selection at any time, or use [Snowflake Functions](https://docs.snowflake.com/en/sql-reference-functions).
7. Click **Save**. Confirm or update the Amplitude-generated model name.

## Create an analysis

When your data model is complete, you can create a Warehouse-native analysis. Warehouse-native Amplitude supports a version of Event Segmentation, Funnels, Retention, Cohorts, and Journeys.