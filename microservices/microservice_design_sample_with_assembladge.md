# Assemblage - a microservice architecture definition process

## 1. Define system operations

- SO001: Upload files incl. validation
  - asset file, journal file, account file 
  - ... more will come up in future
- SO002: Create client
- SO003: Create public facility for one client
- SO004: Create fee-calculation for one year & one public facility
- SO005: Create configurations for one fee-calculation/year (complex config)
  - sub-config A - account ranges
  - sub-config B - interest rates
  - ... more will come up in future
- SO006: Calculate reports
  - report A, report B, report C
  - ... more will come up in future
- SO007: Dashboard for reports

## 2. Define subdomains based on operations

- client
- public facility
- calculation-year
- files
  - assets
  - journal
  - etc.
- configuration
  - config A
  - config B
  - etc.
- reports
  - report A
  - report B
  - etc.
- dashboards
  - for report A, B, C ...

## 3. For each operation, define group of domains

1. Operation: - SO001: Upload files incl. validation
   - required-domains:
     - client & public facility & calculation-year & files
     
2. Operation: SO002: Create client
   - required-domains:
      - client (ONLY CLIENT)

3. Operation: SO003: Create public facility for one client
   - required-domains:
      - client & public facility

4. Operation: SO004: Create fee-calculation for one year & one public facility
   - required-domains:
      - client & public facility & calculation-year

5. Operation: SO006: Calculate reports
   - required-domains:
      - client & public facility & calculation-year & configuration & files
     
... continue for other operations !!

## 4. Microservices based on domains 

- Client Service
  - maybe client, Public facility & year in one single service
- Public facility Service
- Calculation-Year Service
- File Service
- Report Service
  - maybe for each report a single service
- Configuration Service
  - maybe for each configuration a single service
- Dashboard Service
  - maybe for each dashboard a single service

## 5. Microservices communication based on system operations & required subdomains

- TBC 

## 6. Evaluate & Refactor - go back to step 1.