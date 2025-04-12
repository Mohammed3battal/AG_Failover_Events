## Script: Read AG Failover Events from Always On Extended Events Log

**Description**:
This script reads the Extended Events log files related to Always On (`AlwaysOn*.xel`) and extracts **failover events (error 1480)** using the `sys.fn_xe_file_target_read_file()` function. It helps DBAs track failover activity and understand when and why failovers occurred.

**Key Features**:
- Reads `error_reported` events from the XE log
- Filters for error number `1480` (failover detection)
- Extracts timestamp, error number, and message
- Adjusts timestamp for local timezone (+3 by default)

**Use Case**:
- Investigate **when** failovers occurred
- Capture **messages associated with failover events**
- Perform **historical analysis** of AG health and stability

**Requirements**:
- SQL Server 2012 or later (Extended Events must be enabled)
- Access to the default `AlwaysOn_health` XE session (enabled by default)
- `VIEW SERVER STATE` permission

**Notes**:
- You can modify the `error_number` filter to retrieve other errors
- Be sure to adjust the timezone offset (`DATEADD(HOUR, 3, ...)`) if needed
- This script reads from the `.xel` files stored on disk by default at:
  `C:\Program Files\Microsoft SQL Server\MSSQLXX.<InstanceName>\MSSQL\Log`
