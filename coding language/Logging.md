

## logging standard
### Unstructured log
Example with iso-8601 standard
|Date & Timestamp|Logging level|Message|
|-|-|-|
|2021-07-29 14:54:55.1623|INFO|New report created by user 4253|

### Structured log
```json
{ 
	"TimeStamp": "2021-07-29 14:52:55.1623", 
	"Level": "Info", 
	"Message": "New report created", 
	"UserId": "4253", 
	"ReportId": "4567", 
	"Action": "Report_Creation" 
}
```
## Python logger
info won't be printed to the console
```python

import logging
logging.basicConfig(format='%(asctime)s %(message)s', datefmt='%m/%d/%Y %I:%M:%S %p')
logging.warning('Look before you {}!'.format('leap'))  # will print to the console
logging.info('I told you so')  # will not print anything
```
### simple logging config
```python
import logging

# create logger
logger = logging.getLogger('simple_example')
logger.setLevel(logging.DEBUG)

# create console handler and set level to debug
ch = logging.StreamHandler()
ch.setLevel(logging.DEBUG)

# create formatter
formatter = logging.Formatter('%(asctime)s - %(name)s - %(levelname)s - %(message)s')

# add formatter to ch
ch.setFormatter(formatter)

# add ch to logger
logger.addHandler(ch)

# 'application' code
logger.debug('debug message')
logger.info('info message')
logger.warning('warn message')
logger.error('error message')
logger.critical('critical message')
```
### file config
.conf file
```conf
[loggers]
keys=root,simpleExample

[handlers]
keys=consoleHandler

[formatters]
keys=simpleFormatter

[logger_root]
level=DEBUG
handlers=consoleHandler

[logger_simpleExample]
level=DEBUG
handlers=consoleHandler
qualname=simpleExample
propagate=0

[handler_consoleHandler]
class=StreamHandler
level=DEBUG
formatter=simpleFormatter
args=(sys.stdout,)

[formatter_simpleFormatter]
format=%(asctime)s - %(name)s - %(levelname)s - %(message)s
```
con
```config
[logger_<loggers>]
level = DEBUG, WARNING,...
handlers = <handlers>
formatter = <formatters>

[handler_<handlers>]
class = StreamHandler,FileHandler,...
level = DEBUG, WARNING,...
formatter = <formatters>
args=(sys.stdout,)

[formatter_<formatters>]
format=%(asctime)s - %(name)s - %(levelname)s - %(message)s
```
python module
```python
import logging
import logging.config

logging.config.fileConfig('logging.conf')

# create logger
logger = logging.getLogger('simpleExample')

# 'application' code
logger.debug('debug message')
logger.info('info message')
logger.warning('warn message')
logger.error('error message')
logger.critical('critical message')
```
## yaml config
```yaml
formatters:
  brief:
    format: '%(message)s'
  default:
    format: '%(asctime)s %(levelname)-8s %(name)-15s %(message)s'
    datefmt: '%Y-%m-%d %H:%M:%S'
  custom:
      (): my.package.customFormatterFactory
      bar: baz
      spam: 99.9
      answer: 42
```
# Link
[Basic Logging Tutorial](https://docs.python.org/3/howto/logging.html)
[Handler Configuration Order](https://docs.python.org/3/library/logging.config.html#handler-configuration-order)