### Lesson 5: Data Transformation using Data Flows + Triggering Pipeline

---

#### 🔁 Previous Logic Recap
**Pipeline Flow:**
- Get Metadata → ForEach → If Condition → Copy only files starting with `Fact`

---

#### 🧠 Objective:
1)Apply transformations on the copied files inside reporting folder using **Data Flows** and trigger the pipeline automatically using **Triggers**.
![alt text](image-58.png)
2)Stream Processing & Conditional Splits: Creating multiple data streams using conditional splits (e.g., separating data by payment methods like MasterCard, American Express) within data transformation pipelines )
![alt text](image-63.png)
3)Write the output of 1 particular data stream to the sink : */reporting/dataflowOutput*

---

#### 🔧 Data Flow Setup

| Property                 | Value / Choice                                 |
|--------------------------|------------------------------------------------|
| **Data Flow Name**       | `Data_Transformation`                      |
| **Source Dataset**       | Point to copied CSV file in secure container   |
| **Transformations**      | - Select 6 Columns<br> - Filter<br> - Conditional split <br> - Derive new column <br> - Aggregate| 
| **Sink**                 | [`dataflow_sink`] A dataflow folder within the reporting container(to store the transformed data) |
| **Data Flow Debug**      | Enabled                                        |

---

#### ⚙️ Trigger Configuration

| Property             | Value                              |
|----------------------|-------------------------------------|
| **Trigger Type**     | Scheduled                           |
| **Trigger Name**     | `selectedFilesTrigger`            |
| **Start Time**       | `6/8/2025, 1:35:46 AM`               |
| **Recurrence**       | e.g., every 1 hour (if scheduled)   |
| **Associated Pipeline** | Connect this to main pipeline     |

---

## 🔁 Workflow Screenshot

- In the dataflow canvas -> Settings -> Create a new dataset for this data flow ->File path = reporting/csvfiles
![alt text](image-44.png)

- Turn on the cluster
![alt text](image-45.png)

- Import Project -> To import the schema
![alt text](image-46.png)

- Data Preview
![alt text](image-47.png)

- The list of transformation functions
![alt text](image-48.png)

- Select 6 cols
![alt text](image-49.png)

- Filter data : discard cusid = 12
![alt text](image-50.png)
![alt text](image-51.png)

- Split data based on  Payment type (visa , mastercard , amex)
![alt text](image-52.png)
![alt text](image-53.png)

- Apply `Derived Column` [to transform a col or add a new col] to remove null values in amex category
![alt text](image-54.png)

- Apply groupBy(`Aggregate`)
 
    - GroupyBy Customer id
    ![alt text](image-55.png)

    - Max of prod id
    ![alt text](image-56.png)

    - Data preview [The max prod it based on each customer id]
    ![alt text](image-57.png)

 - Use AlterRows b4 Sink (allows to perform insert , update, upsert. esp delaimg with dbs and data warehouses)
 [*Insert all records*]
 ![alt text](image-61.png)
 [*esp useful if we only want to insert data for prod_id == 1, etc]

- Select sink after aggregation to write the transformed data

![alt text](image-59.png)
![alt text](image-60.png)

- Here we ignored writing data pf mastercard and amex stream to a sink. Only the o/p of visa is written to a sink.
![alt text](image-62.png)

- Add a trigger
![alt text](image-65.png)

- Trigger Activated
![alt text](image-66.png)

- Pipeline executed successfully
![alt text](image-67.png)

- Output
![alt text](image-68.png)
---  

### 📌 Step-by-Step Workflow

#### 1. 🛠️ Data Flow Setup
- Open the **Data Flow canvas** in ADF.
- Create a new dataset → Set file path: `reporting/csvfiles`.
- **Turn on debug cluster** to allow data preview.

#### 2. 📥 Schema Import & Preview
- Use **Import Projection** to load schema structure.
- Enable **Data Preview** to validate incoming data.

---

### 🔄 Transformations Performed

#### ✅ Column Selection
- Selected only **6 relevant columns**.

#### ✅ Filter
- Applied **Filter**: Removed records where `cusid = 12`.

#### ✅ Conditional Split
- Split data into 3 streams based on **Payment Type**:
  - `Visa`
  - `Mastercard`
  - `Amex`

#### ✅ Derived Column
- In the **Amex stream**, applied `Derived Column` to remove null values.

#### ✅ Aggregation
- Used **GroupBy** on `cusid`.
- Aggregated **max of `prod_id`** per customer.

#### ✅ Alter Row
- Applied **Alter Row** transformation to mark all rows for **Insert**.
  - Useful when targeting databases or performing conditional upserts.

#### ✅ Sink (Write Output)
- Wrote only the **Visa stream** to the final sink.
- Skipped `Mastercard` and `Amex` outputs for privacy/security.

### 🔔 Trigger Configuration

- Added a trigger to the pipeline.
- Activated it to automate execution (manual or scheduled).

---


#### 📈 Outcome
- Pipeline executed successfully via trigger.
- Only `Fact_*.csv` Visa records were transformed and saved.
- Output verified in sink and data preview.

---

#### 📂 JSON File Reference:
- [lesson6_dataflow_transform_fact.json](./lesson6_dataflow_transform_fact.json)

