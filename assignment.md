# Assignment outline

For the given application description, please create a sample document for the API using the following
background data:
The application allows to facilitate execution, management, and monitoring of ad creatives via a
configurable API Gateway. The following operations (endpoints) are included:

1. Create Ad Creative - Endpoint accepts the following parameters: id, name, type, content,
   additional_data (array of key => value elements). 200 - response with success status, 400 - error
   status with error messages.
2. Bulk Creation - Accepts the array of ad creative objects (see previous endpoint). Returns success
   status 200 if all ad creatives were created, error status 400 with array of error message per
   entity.
3. View Ad Creative List – the endpoint returns the list of ad creative objects based on the IDs
   provided as request parameters.
4. Edit Ad Creative – Endpoint accepts the same parameters as create endpoint. Additional error
   404 if ad creative ID does not exist. All input parameters except of ID are optional
5. Status Report Generation – Status report provides information on the ad creatives that were
   "created" or "updated" on a specific date. Input parameters: start_date and end_date. Report
   contains ad creative IDs as arrays for each day included in report and the number of ad creative
   IDs with respective statuses (the number of created and updated ad creatives for period). Error
   messages are returned when start date and end date have no valid date format or start date is
   later than end date.

Each endpoint requires X_TOKEN as a header to ensure security.
Expected Output:

- The document should contain an application overview, security section, and endpoints
  description with **sample requests and responses**.
- If some information is missing, please use assumptions and list them in the document as a
  separate section.
- Please suggest and use (if possible) the most suitable documenting tool for this artifact.
