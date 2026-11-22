# Invoice Automation & SAP Integration Pipeline

An end-to-end document processing and workflow automation pipeline that extracts structured invoice fields into validated JSON, cross-checks them against relational purchase order records, logs execution audit trails, and syncs verified invoices to an **SAP Integration Suite / OData** accounting schema.

## Architecture
1. **Document Extractor (`src/extractor.py`)**: Extracts vendor, invoice number, PO number, subtotal, tax, and total into Pydantic-validated JSON.
2. **Workflow Validator (`src/validator.py`)**: Cross-checks invoice values against approved Purchase Orders in SQL and flags amount/vendor discrepancies.
3. **SAP Integration Client (`src/sap_integration.py`)**: Transforms validated REST JSON into an SAP S/4HANA Supplier Invoice OData payload with retry logic.
4. **Audit Database (`src/audit_db.py`)**: Records every ingestion, validation decision, and posting status in SQLite/PostgreSQL.
5. **Integration Suite Artifacts (`integration_suite/`)**: Documents the iFlow architecture and REST-to-OData mapping schema.

## Quick Start
```bash
python -m venv venv
source venv/bin/activate  # Windows: venv\Scripts\activate
pip install -r requirements.txt
python -m src.pipeline
```

## Run Tests
```bash
pytest -v
```
