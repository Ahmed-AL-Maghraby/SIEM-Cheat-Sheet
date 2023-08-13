Certainly, here is a comprehensive list of 100 famous Splunk SPL commands, divided into categories, along with explanations and examples for each category:

| Command | Description | Example |
| ------- | ----------- | ------- |
| ------- | ----------- | ------- |
| ------- | ----------- | ------- |

# Table of contents 
   
|Table of contents|
| -- |
|[   ]()|
|[   ]()|
|[   ]()|
|[   ]()|
|[   ]()|
|[   ]()|
|[   ]()|
|[   ]()|
|[   ]()|


-------------------------------

## Basic Commands:

| Command | Description | Example |
| ------- | ----------- | ------- |
| search | Initiates a search for events based on specified criteria | ``index=web_logs status=200`` |
| index | Specifies the index to search within | ``index=web_logs`` |
| sourcetype | Filters events based on the specified sourcetype | ``sourcetype=apache_access`` |

<br/>

## Filtering and Extraction

| Command | Description | Example |
| ------- | ----------- | ------- |
| where |  Filters events based on conditions | ``index=logs \| where status="error"`` |
| eval | Creates new fields or modifies existing ones | ``index=logs \| eval latency_ms=response_time/1000 \| table latency_ms`` |
| rex | Performs regular expression extraction on fields | index=logs | rex field=message "Error: (?<error_message>.*)" |
| erex | Enhanced regular expression extraction with named capture groups | index=logs | erex "Error: (?<error_message>.*)" |


<br/>

### **Aggregation and Statistics:**

8. **stats**
   - Description: Generates statistics and calculations on fields.
   - Example: `index=sales | stats sum(price) as total_sales by product`

9. **timechart**
   - Description: Creates time-based charts and aggregates data over time.
   - Example: `index=web_logs | timechart count by status`

10. **chart**
    - Description: Generates charts and graphs based on specified fields.
    - Example: `index=web_logs | chart avg(response_time) by uri`

11. **eventstats**
    - Description: Performs statistics calculations on events and adds results as new fields.
    - Example: `index=transactions | eventstats avg(amount) as avg_amount by user`

---

### **Grouping and Transactional Analysis:**

12. **transaction**
    - Description: Groups related events into transactions based on conditions.
    - Example: `index=transactions | transaction user startswith="login" endswith="logout"`

13. **stats count by**
    - Description: Counts occurrences of unique values in a field.
    - Example: `index=web_logs | stats count by status`

14. **stats earliest, latest by**
    - Description: Retrieves the earliest and latest events for each value in a field.
    - Example: `index=logs | stats earliest(_time) as first_event latest(_time) as last_event by user`

---

### **Field Manipulation:**

15. **fields**
    - Description: Specifies fields to be included in the search results.
    - Example: `index=logs | fields timestamp, source, message`

16. **rename**
    - Description: Renames fields in the search results.
    - Example: `index=logs | rename old_field as new_field`

17. **fieldformat**
    - Description: Applies formatting to field values in search results.
    - Example: `index=metrics | eval formatted_latency = fieldformat(response_time, "duration")`

18. **addcoltotals**
    - Description: Adds row and column totals to tabular search results.
    - Example: `index=sales | addcoltotals useother=f sum(price) as total_price`

---

### **Data Transformation:**

19. **rex mode=sed**
    - Description: Applies sed-like replacements using regular expressions.
    - Example: `index=logs | rex mode=sed field=description "s/error/warning/g"`

20. **spath**
    - Description: Extracts structured data from fields containing JSON or XML.
    - Example: `index=logs | spath input=raw output=uri path=uri`

21. **spath output path**
    - Description: Extracts specific paths from structured data as separate fields.
    - Example: `index=logs | spath input=raw output=page path=uri`

22. **spath input path output path default**
    - Description: Extracts structured data with default values if path is not found.
    - Example: `index=logs | spath input=raw output=page path=uri default="Unknown"`

---

### **Lookup and Enrichment:**

23. **lookup**
    - Description: Enhances data with additional information from lookup tables.
    - Example: `index=logs | lookup user_info.csv username as user`

24. **inputlookup**
    - Description: Loads lookup data into a search.
    - Example: `| inputlookup user_info.csv`

25. **outputlookup**
    - Description: Saves search results into a lookup file.
    - Example: `index=logs | stats count by user | outputlookup user_counts.csv`

---

### **Advanced Analysis:**

26. **eval case()**
    - Description: Performs conditional evaluation.
    - Example: `index=logs | eval priority = case(severity=="High", "Urgent", severity=="Medium", "Normal", true(), "Low")`

27. **eval coalesce()**
    - Description: Returns the first non-null value among arguments.
    - Example: `index=logs | eval important_info = coalesce(critical_message, warning_message, info_message)`

28. **eval round()**
    - Description: Rounds a numeric field to a specified number of decimal places.
    - Example: `index=metrics | eval rounded_value = round(value, 2)`

29. **eval mvjoin()**
    - Description: Joins multivalue fields into a single value using a separator.
    - Example: `index=events | eval combined_tags = mvjoin(tags, ", ")`

30. **eval strftime()**
    - Description: Converts a Unix timestamp to a human-readable date and time format.
    - Example: `index=logs | eval formatted_time = strftime(_time, "%Y-%m-%d %H:%M:%S")`

---

### **Subsearch and Correlation:**

31. **subsearch**
    - Description: Embeds a subsearch within the main search to correlate events.
    - Example: `index=access_logs [ search index=error_logs | stats count ]`

32. **tstats**
    - Description: Accelerated statistics command for summarizing indexed data.
    - Example: `| tstats count where index=web_logs by sourcetype`

---

### **Visualization and Reporting:**

33. **timechart span**
    - Description: Creates time-based charts with specified time spans.
    - Example: `index=web_logs | timechart span=1h sum(response_time)`

34. **geostats**
    - Description: Generates geospatial statistics and visualizations.
    - Example: `index=locations | geostats count by city`

35. **chart usenull**
    - Description: Includes NULL values in chart visualizations.
    - Example: `index=logs | chart count by user usenull=f`

36. **rangemap**
    - Description: Maps field values to ranges for reporting.
    - Example: `index=sales | rangemap price output_field=price_range`



37. **xyseries**
    - Description: Generates XY chart visualizations from multivalue fields.
    - Example: `index=metrics | xyseries x=time y=values`

---

### **Alerting and Monitoring:**

38. **alert**
    - Description: Sets up alerts based on specified conditions.
    - Example: `index=errors | stats count as error_count | alert threshold=100 "High Error Count"`

39. **collect**
    - Description: Aggregates and stores events for future analysis.
    - Example: `index=access_logs | collect index=access_history`

40. **track_alert**
    - Description: Tracks alert activity and results.
    - Example: `index=_audit action="alert_fired" | stats count by alert`

---

### **Batch Mode and Lookup:**

41. **multisearch**
    - Description: Runs multiple searches in parallel.
    - Example: `| multisearch [ search index=logs ] [ search index=metrics ]`

42. **multisearch SID**
    - Description: Searches in parallel with session ID.
    - Example: `| multisearch SID=search1 [ search index=logs ] [ search index=metrics ]`

43. **inputcsv**
    - Description: Loads data from a CSV file into the search.
    - Example: `| inputcsv data.csv`

44. **inputlookup append=t**
    - Description: Appends data from a lookup table to the search results.
    - Example: `index=logs | inputlookup append=t lookup_table.csv`

---

### **Working with Time:**

45. **strptime**
    - Description: Converts a string to a timestamp format.
    - Example: `index=logs | eval event_time = strptime(timestamp, "%Y-%m-%d %H:%M:%S")`

46. **earliest latest**
    - Description: Specifies time ranges for the search.
    - Example: `index=logs earliest=-7d latest=now`

47. **bucket**
    - Description: Groups events into time buckets.
    - Example: `index=logs | bucket span=1h _time`

---

### **String Functions:**

48. **substr**
    - Description: Extracts a substring from a field's value.
    - Example: `index=logs | eval short_message = substr(message, 1, 50)`

49. **len**
    - Description: Returns the length of a string field.
    - Example: `index=logs | eval message_length = len(message)`

50. **toupper tolower**
    - Description: Converts string values to uppercase or lowercase.
    - Example: `index=logs | eval uppercase_message = toupper(message)`

---

### **Math Functions:**

51. **round**
    - Description: Rounds numeric values to the nearest whole number.
    - Example: `index=metrics | eval rounded_value = round(value)`

52. **abs**
    - Description: Returns the absolute value of a number.
    - Example: `index=metrics | eval absolute_value = abs(change)`

53. **sqrt**
    - Description: Calculates the square root of a number.
    - Example: `index=metrics | eval square_root = sqrt(number)`

54. **power**
    - Description: Raises a number to a specified power.
    - Example: `index=metrics | eval squared_value = power(value, 2)`

55. **log log10**
    - Description: Computes the natural logarithm or base-10 logarithm.
    - Example: `index=metrics | eval ln_value = log(value)`

---

### **Conditional Functions:**

56. **if()**
    - Description: Returns different values based on a condition.
    - Example: `index=logs | eval status_type = if(status>=400, "Error", "Success")`

57. **case()**
    - Description: Evaluates a series of conditions and returns values accordingly.
    - Example: `index=logs | eval severity_level = case(severity=="High", 3, severity=="Medium", 2, severity=="Low", 1)`

58. **coalesce()**
    - Description: Returns the first non-null value among arguments.
    - Example: `index=logs | eval important_info = coalesce(critical_message, warning_message, info_message)`

---

### **Logical Functions:**

59. **and or not**
    - Description: Performs logical AND, OR, and NOT operations.
    - Example: `index=logs | eval is_error = (severity=="High" OR status>=500)`

60. **eval like**
    - Description: Matches field values with wildcard patterns.
    - Example: `index=logs | eval is_error = like(message, "*error*")`

61. **mvfilter**
    - Description: Filters multivalue fields based on conditions.
    - Example: `index=events | eval tags = mvfilter(tag, like(tag, "*critical*"))`

---

### **Working with Multivalue Fields:**

62. **mvexpand**
    - Description: Expands multivalue fields into separate events.
    - Example: `index=events | mvexpand tags`

63. **mvzip mvappend mvcombine**
    - Description: Manipulates multivalue fields.
    - Example: `index=events | eval combined_fields = mvzip(field1, field2, ", ")`

64. **mvcount**
    - Description: Counts the number of values in a multivalue field.
    - Example: `index=events | eval tag_count = mvcount(tags)`

65. **mvfind**
    - Description: Searches for values in a multivalue field.
    - Example: `index=events | eval has_error = mvfind(tags, "error")`

---

### **Numeric Functions:**

66. **isnull isnotnull**
    - Description: Checks if a field value is null or not null.
    - Example: `index=metrics | eval missing_value = isnull(response_time)`

67. **isnum**
    - Description: Checks if a field value is a number.
    - Example: `index=metrics | eval is_number = isnum(value)`

68. **isbool**
    - Description: Checks if a field value is a boolean.
    - Example: `index=events | eval is_boolean = isbool(flag)`

69. **mvjoin**
   

 - Description: Joins multivalue fields into a single value using a separator.
    - Example: `index=events | eval combined_tags = mvjoin(tags, ", ")`

---

### **Time and Date Functions:**

70. **now**
    - Description: Returns the current date and time.
    - Example: `index=logs | eval current_time = now()`

71. **strptime strftime**
    - Description: Converts between Unix timestamps and human-readable dates.
    - Example: `index=logs | eval formatted_time = strftime(_time, "%Y-%m-%d %H:%M:%S")`

72. **relative_time**
    - Description: Calculates a relative time based on a unit and offset.
    - Example: `index=logs earliest=relative_time(now(), "-1d@d")`

73. **date_month date_wday**
    - Description: Extracts month or day of the week from timestamps.
    - Example: `index=logs | eval month = date_month(_time)`

74. **now offset**
    - Description: Returns the current time with an offset.
    - Example: `index=logs | eval future_time = now() + 3600`

75. **time**
    - Description: Converts a string representation of time to a Unix timestamp.
    - Example: `index=logs | eval event_time = time("2023-01-15 10:30:00")`

76. **date_part**
    - Description: Extracts specific components (year, month, day, etc.) from a timestamp.
    - Example: `index=logs | eval year = date_part(_time, "year")`

---

### **IP and Geolocation Functions:**

77. **iplocation**
    - Description: Retrieves geolocation information for IP addresses.
    - Example: `index=logs | iplocation clientip`

78. **cidrmatch**
    - Description: Matches IP addresses against CIDR ranges.
    - Example: `index=network_traffic | cidrmatch(ip, "192.168.0.0/24")`

79. **isipv4 isipv6**
    - Description: Checks if a field value is an IPv4 or IPv6 address.
    - Example: `index=logs | eval is_ipv4 = isipv4(ip_address)`

80. **maxmindisplocation**
    - Description: Retrieves geolocation information from MaxMind databases.
    - Example: `index=logs | maxmindisplocation ipfield=client_ip`

81. **iptoname**
    - Description: Maps IP addresses to domain names.
    - Example: `index=network_traffic | eval hostname = iptoname(destination_ip)`

---

### **Geospatial Functions:**

82. **geostats**
    - Description: Generates geospatial statistics and visualizations.
    - Example: `index=locations | geostats count by city`

83. **geodistance**
    - Description: Calculates the distance between two sets of geographic coordinates.
    - Example: `index=locations | eval distance_km = geodistance(lat1, lon1, lat2, lon2, "km")`

84. **geobounds**
    - Description: Calculates the bounding box of a set of geographic coordinates.
    - Example: `index=locations | geobounds latfield=latitude lonfield=longitude`

85. **geopoint**
    - Description: Converts latitude and longitude to a geopoint field.
    - Example: `index=locations | eval geopoint = geopoint(latitude, longitude)`

86. **geom distance**
    - Description: Calculates the distance between two geopoint fields.
    - Example: `index=locations | eval distance_km = geom_distance(geopoint1, geopoint2, "km")`

---

### **Advanced Transformations:**

87. **spath**
    - Description: Extracts structured data from fields containing JSON or XML.
    - Example: `index=logs | spath input=raw output=uri path=uri`

88. **spath output path**
    - Description: Extracts specific paths from structured data as separate fields.
    - Example: `index=logs | spath input=raw output=page path=uri`

89. **spath output default**
    - Description: Extracts structured data with default values if path is not found.
    - Example: `index=logs | spath input=raw output=page path=uri default="Unknown"`

90. **spath input path output path default**
    - Description: Extracts structured data with specific paths and default values.
    - Example: `index=logs | spath input=raw output=status_code path=code default="N/A"`

---

### **Conditional Transformations:**

91. **case()**
    - Description: Performs conditional evaluations and returns values.
    - Example: `index=logs | eval priority = case(severity=="High", "Urgent", severity=="Medium", "Normal", true(), "Low")`

92. **if()**
    - Description: Returns different values based on a condition.
    - Example: `index=logs | eval alert_level = if(severity=="High", "Critical", "Normal")`

93. **eval coalesce()**
    - Description: Returns the first non-null value among arguments.
    - Example: `index=logs | eval important_info =

 coalesce(critical_message, warning_message, info_message)`

---

### **Timechart and Chart Functions:**

94. **timechart span**
    - Description: Creates time-based charts with specified time spans.
    - Example: `index=web_logs | timechart span=1h sum(response_time)`

95. **chart usenull**
    - Description: Includes NULL values in chart visualizations.
    - Example: `index=logs | chart count by user usenull=f`

96. **chart overlay**
    - Description: Generates overlay charts based on fields.
    - Example: `index=web_logs | chart count over status by host`

97. **chart span**
    - Description: Creates span charts with time and non-time fields.
    - Example: `index=events | chart count by user span=1d`

98. **chart stack**
    - Description: Generates stacked charts based on fields.
    - Example: `index=web_logs | chart count stack by status`

99. **chart bins**
    - Description: Creates histogram-style charts with specified bin sizes.
    - Example: `index=metrics | chart count bins=10 by value`

---

### **Advanced Analysis and Correlation:**

100. **stats first last**
    - Description: Retrieves the first and last values of fields.
    - Example: `index=events | stats first(_time) as first_event last(_time) as last_event by user`

101. **eventstats**
    - Description: Performs statistics calculations on events and adds results as new fields.
    - Example: `index=transactions | eventstats avg(amount) as avg_amount by user`

102. **rare**
    - Description: Identifies rare values in a field.
    - Example: `index=errors | rare error_code`

103. **dedup**
    - Description: Removes duplicate events based on specified fields.
    - Example: `index=logs | dedup user, ip_address`

104. **multikv**
    - Description: Extracts key-value pairs from fields.
    - Example: `index=logs | multikv fields key1, key2`

---

Please note that these examples are simplified for demonstration purposes. Actual use cases might require more complex combinations of commands, functions, and field names. Replace `index`, `sourcetype`, field names, and values with your actual data and requirements. Splunk's real power comes from creatively combining these commands and functions to analyze and visualize data according to your specific use case.
