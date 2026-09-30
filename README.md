# Vivian Cao

I am a backend cloud integration engineer focusing on serverless pipeline architecture, data extraction, and payload normalization on AWS. Most of my work involves taking messy and nonstandard inputs such as multipage PDF invoices, multitab Excel workbooks, CSVs, XMLs, MHTMLs, and REST API payloads and turning them into clean, standardized records for downstream platforms.

In production, getting data out of a file is only half the work. The harder part is making sure the data is accurate. Vendor layouts can change without notice, text extraction can fail without being obvious, and downstream procurement portals have strict validation rules. AI and standard scripts do not always handle these cases well. Much of my day to day work involves writing arithmetic checks, handling edge cases, debugging pipeline issues, and looking for ways to improve accuracy and processing speed. I also look for unnecessary AWS usage and other costs that can be reduced without affecting the result.

Because I work on a small team, I handle these pipelines across their full lifecycle. I design the architecture, build the extraction services, configure AWS infrastructure such as IAM roles, VPC networking, Docker containers, and CloudFormation or SAM stacks, deploy to production, and investigate support issues when upstream files change. I also make ongoing changes to improve how the pipelines work and keep them practical for the needs and budget of a small team.

> ***Note on repositories:** The enterprise projects below are production systems built for client integrations. The source code is restricted, but each repository includes architectural documentation, data flow diagrams, and engineering notes.*

## Skills

* **Languages:** Python, SQL, JavaScript (Node.js)
* **Also worked with:** PHP, Angular, React
* **AWS:** Lambda, Step Functions, S3, SQS, SNS, EventBridge, API Gateway, RDS, DynamoDB, Glue, Athena, QuickSight, Bedrock, CloudWatch, SES, IAM, Secrets Manager, SSM Parameter Store
* **Infrastructure:** AWS SAM, CloudFormation, Docker, VPC (NAT Gateway, static Elastic IPs), Linux or WSL, Git, GitHub, GitLab
* **Data:** PostgreSQL, MySQL, DuckDB, Pandas, SQLAlchemy, PyArrow, Parquet, PDFPlumber, openpyxl, BeautifulSoup
* **Integration and security:** REST APIs, mTLS client certificates, OAuth 2.0 (client credentials), bearer token auth
* **AI:** Amazon Bedrock, OpenAI API (vision and structured extraction)

## Certifications

* **AWS Certified Solutions Architect: Associate** (Currently studying)

## Enterprise Projects

### Document Processing and Extraction

* [**Serverless Invoice Pipeline Optimization**](https://github.com/Vivianwcao/OLAP-Invoice-Processor-Bedrock-Pipeline)  
  Traced a $500 per month AWS bill to Textract scanning 100 page PDFs for three fields, plus invisible retries repeating the charge. Built a page slicer, replaced most OCR with targeted PDFPlumber parsing, and rebuilt nine external workflow scenarios as one Step Functions state machine. Monthly cost down to $3 to $5; processing time from five minutes to ten seconds.

* [**Modular Hybrid PDF Parsing and Routing Pipeline**](https://github.com/Vivianwcao/Serverless-Invoice-Processing-Pipeline)  
  Step Functions state machine that extracts text directly from PDF text layers, validates the results, and only sends files to manual OCR when needed. This reduced OCR usage and costs while allowing more than 90% of PDFs to be processed without a human. Supplier specific stages such as AFE validation and pricebook mapping are handled within the same workflow.

* [**Serverless Vision AI Document Pipeline**](https://github.com/Vivianwcao/Aimsio-Invoice-Processing-Pipeline)  
  Multimodal extraction using PyMuPDF and GPT 4o Vision to identify supplier department logos, with an in memory DuckDB engine inside Lambda for subsecond pricebook matching against CSV rate tables.

* [**Field Ticket Workbook Pipeline**](https://github.com/Vivianwcao/Serverless-Excel-ERP-microservice)  
  Parses eight tab Excel workbooks, joins job metadata to line items across six cost categories by ticket number, and emits both a 52 column CSV for accounting import and individual ticket JSON files for platform submission.

* [**Serverless Field Invoice XLSX Parser**](https://github.com/Vivianwcao/Field-Invoice-XLSX-Parser)  
  Python microservice streaming unstructured `.xlsx` billing sheets from S3 into memory, dynamically mapping variable table headers and line items with Pandas and openpyxl.

### Data Engineering and Analytics

* [**E Procurement Submission Analytics Pipeline**](https://github.com/Vivianwcao/B2B-Invoice-Submission-Analytics-Pipelines)  
  Combines two sources with no shared access method: an mTLS API returning full receipt history, and Excel snapshots landing in S3. SQS fanout gives each supplier its own execution window; timestamp checked upserts prevent stale payloads overwriting fresh data; per worker staging tables avoid deadlocks. Migrated storage from Parquet or Athena to RDS MySQL when schema changes became the bottleneck. Feeds a five page QuickSight dashboard.

* [**Serverless Data Lakehouse for Field Operations**](https://github.com/Vivianwcao/Serverless-Excel-to-Lakehouse-OLAP-pipeline)  
  Medallion architecture (Bronze, Silver, Gold) on S3 ingesting 750+ multitab operational workbooks, using Bedrock to extract structured fields from free text engineering notes, surfaced through Athena and QuickSight.

* [**TrueContext Invoice Data Pipeline**](https://github.com/Vivianwcao/TrueContext-Invoice-Data-Pipeline)  
  Event driven ingestion using a native IAM push destination instead of custom polling code. Glue Crawlers infer schema across 2200+ deeply nested JSON payloads for Athena querying and QuickSight reporting.

### B2B Platform Integrations

* [**SAP Ariba PO Line Enrichment Engine**](https://github.com/Vivianwcao/SAP-Ariba-Purchase-Order-Sync-Engine)  
  Two step OAuth 2.0 to fetch PO line structures, reordering invoice JSON in S3 to satisfy strict line sequence validation. Handles 24 minute token expiry against warm Lambda containers and falls back to explicit date range queries for POs older than 31 days.

* [**Invoice Flipper**](https://github.com/Vivianwcao/Serverless-Invoice-Flipper)  
  Mutual TLS authentication from Python inside a VPC, routed through a NAT Gateway with a static Elastic IP to satisfy platform IP whitelisting.

* [**Sage 50 CSV to IMP Ingestion Engine**](https://github.com/Vivianwcao/Sage-50-CSV-to-IMP-Conversion-Microservice)  
  Node.js service converting field ticket CSVs into Sage 50 `.IMP` sales invoice files, aggregating line items by PO and applying tax rules to the target schema.

## Personal Projects

* [**Stock Portfolio Analytics Engine**](https://github.com/Vivianwcao/Personal-Stock-Trading-Ledger-with-Analytics)  
  Built for an active trader tracking five accounts across 80+ Excel tabs. Rolling cost basis computed with SQL window functions partitioned by account, symbol, and trade cycle to match the broker's own calculation. Went through three database iterations; the write up covers why each one failed.

* [**StatCan Data Lakehouse and ELT Pipelines**](https://github.com/Vivianwcao/StatCanada-ELT-pipeline)  
  Two pipeline patterns over Statistics Canada census data: API streaming into a PostgreSQL snowflake schema, and direct CSV parsing with DuckDB into partitioned Bronze, Silver, Gold Parquet layers.

## Education

* **British Columbia Institute of Technology:** Diploma, Computer Systems Technology (Cloud Computing option), 2022. Graduated with Distinction.
* **BrainStation:** Software Engineering Diploma, 2025. 96%
  
## Contact

* **LinkedIn:** [linkedin.com/in/vivianwcao](https://linkedin.com/in/vivianwcao)
* **Email:** vivian.w.cao@gmail.com
