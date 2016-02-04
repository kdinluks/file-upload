# file-upload

UI Elements for uploading CSV files and sending them to the time series ingestion service. https://github.com/kdinluks/timeseries-ingestion-service

## Overview

### file-upload

```
<file-upload id="" max-size="" concat="" packet-size="" initial-configuration="{"valueindex": "", "tagindex": "", "dateindex": "", "delimiter": "", "mask": "", "metername": "", "meterindex": "", "equipmentindex": ""}"></file-upload>
```

#### Attributes

    id : the identifier for the uploader.
  
    max-size : the maximum file size allowed for upload, in bytes. Default is 10485760 Bytes.
  
    concat : the char used in the concatenation of the tag name and equipment name to create the meter name. Default is "_".
  
    packet-size : the packet size to be used for the ingestion service when sending the data to Predix Timeseries. Default and max value is 5000.
  
    initial-configuration : object with the initial configuration for the parameters sent to the ingestion service. This configuration is overwritten by the User values set in the configuration fields.
  
      valueindex : the row index of the value field in the csv file
    
      tagindex : the row index of the tag name in the csv file
    
      dateindex : the row index of the timestamp in the csv file
    
      mask : the timestamp mask used in the csv file. Please follow the standards from here https://docs.python.org/2/library/datetime.html#strftime-and-strptime-behavior
    
      metername : the meter name to be used in Predix Timeseries to store the data
    
      meterindex : the row index of the meter name in the csv file, to be used in Predix Timeseries to store the data
    
      equipmentindex : the row index of the meter name in the csv file

#### Notes

The packet size is the amount of information sent per request to Predix Timeseries, and it relates straight to the number of points sent per request. Predix timeseries has a maximum size for the request and therefore the 5000 limit was put in place. You shouldn't need to change this value.

You don't need to use the property initial-configuration, as it has default values and it's values are going to be changed when the user changes the values using the configuration fields. For future releases we may add options to disable some fields so you can set the properties using the initial-configuration and have them sent without the user interference.

All the parameters in the initial-configuration are required, but you can use the meterindex and metername interchangeably. If meterindex is used, it's going to be used for the Predix Timeseries meter name, even if metername is defined.

If meterindex or metername is defined, you don't need to use tagindex or equipmentindex.

If neither meterindex nor metername are defined, you must use tagindex and equipmentindex. They will be used in conjunction with concat to create the meter name.

### file-upload-header

```
<file-upload-header id="" title=""></file-upload-header>
```

#### Attributes

    id : the identifier for the header
  
    title : the title to be displayed in the header

#### Notes

For now this is a place holder for future functionalities like: adding multiple uploader modules; global upload start; global upload cancel; global queue; ...
