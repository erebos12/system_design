# Assemblage - a microservice architecture definition process

## 1. Define system operations

- NR001: Upload files incl. validation
  - asset file, journal file, account file 
- NR002: Create client
- NR003: Create public facility for one client
- NR004: Create years for one public facility
- NR005: Create configurations for one year (complex config)
  - config A - account ranges
  - config B
  - config C
  - ... more will come up in future
- NR006: Calculate reports
  - report A, report B, report C
  - more will come up in future
- NR007: Download reports via Excel
- NR008: Dashboard for reports
- NR009: statistics 
  - based on file data from clients
  - based on reports
  - based on configurations

## 2. Define subdomains based on operations

- client
- public facility
- year
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


## 3. For each operation, define group of domains

1. Operation: NR002: Create client
   - required-domains:
      - client (ONLY CLIENT)

2. Operation: NR003: Create public facility for one client
   - required-domains:
      - client & public facility

3. Operation: NR004: Create years for one public facility
   - required-domains:
      - client & public facility & years

4. Operation: - NR001: Upload files incl. validation
   - required-domains:
     - client & public facility & year & files

... continue for other operations !!

## 4. Microservices based on group of domains

- Client Service
  - maybe client, Public facility & year in one single service
- Public facility Service
- Year Service
- File Service
- Report Service
  - maybe for each report a single service
- Configuration Service
  - maybe for each configuration a single service

## 5. Evaluate & Refactor - go back to step 1.