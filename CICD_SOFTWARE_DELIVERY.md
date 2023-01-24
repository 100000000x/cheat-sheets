# CI/CD, Proactive, Preemptive Software Delivery

_Isolation, Reproducability, Declarativity_  
_Granularity, Version Control, Source Control, Resource Control_  

Virtualization Advantages:
- Security (higher isolation)
- Development (lower cost)
- Resource management (higher flexibility, vertical and horizontal)  

Containerization Advantages:
- PID, Process Isolation
- NET, Network Isolation
- IPC, Inter Process Communication Isolation
- MNT, Mount Isolation
- UTS, Isolation Kernel Resources and Version Identifiers
- USR, User Isolation

Orchestration Advantages:
- Leveraging all above by horizontal scaling through automation

_Bare Metal > Host OS ( > Hypervisor > Guest OS (TCP/IP - )) ( > Container Orchestration ( - TCP/IP - )) > Container Runtime (/run, /exec) > Docker Daemon (/build, /push) > ( - UNIX DOMAIN SOCKETS - ) > Docker CLI >  Container Build (chroot+) ( > Image Registry) > Image (Artefact) (tar.gz) > extra Dockerfiles ( = Makefiles)_

# Integrated Software Quality Mechanisms

_LINT, COMPILE, TYPE, DOCUMENT, HANDLE, LOG, TEST, CI/CD & DEBUG LIKE A PRO_  
_Proactive: Make easy debugging likely_  
_Preemptive: Make user churn due to bugs unlikely_  
_Semantic Versioning: MAJOR(not backwards compatible).MINOR(backwards compatible refactoring).PATCH(bugfixes)_
_Implementation Testing, Unit Test, Integration Test, System Test, In Service Test, In Service Bug Hunts / In Service Penetration Tests_

_Division of Origin and Usage_
_Shift Left Thinking_
_Dev Sec Ops_

_CI/CD_
_Continuous: Triggers and Runner_
_Delivery: Human Inspected Staging Layer_
_Deployment: Automated Shipping_
_Development Environment: Git, Gitlab, Gitlab Actions: Container Image Registry: Image Staging: Image Deployment_

## Lint, Compile, Type
```
Typescript
Babel
black
flake8
autopep8
yapf
Pylint
PyFlakes
mypy
Static Code Analysis
```
## Documentation best practices, Git best practices, Documentation generators
```
Sphinx
```
## Exception error handling, Exception error printing
list of all built in exceptions
```
Exception
StopIteration
SystemExit
StandardError
ArithmeticError
OverflowError
FloatingPointError
ZeroDivisionError
AssertionError
AttributeError
EOFError
ImportError
KeyboardInterrupt
LookupError
IndexError
KeyError
NameError
UnboundLocalError
EnvironmentError
IOError
OSError
SyntaxError
IndentationError
SystemError
SystemExit
TypeError
ValueError
RuntimeError
NotImplementedError
```
use exception filter like
```
try:
    print("string")

except Exception as e:
    print(traceback.format_exc())
    print(str(e))

except TimeoutException as te:
    print(te)
finally:
    return "string"
```
## Extensive Logging, Monitoring
```
Graylog
Grafana
```
## Testing
Business Logic Testing  
Arrange, Act, Assert  
Optimize for: Quality, Speed, Cost, Security  
```
TDD
Development in Container
CI/CD Triggers (Source Code, Libraries Changes)
Jenkins
Selenium
Testing in Container
Testing as Container Orchestra
```
## Debugging
_use prints to divide and conquer, zoom in on the troublemaker in locality (where in the code) and concept (where in the processing of the code). make it transparent_
```
print(f"before function xyz - {dict}")
print(f"after function xyz - {dict}")
find / -name '*.py' -exec grep -l "keyword" {} \;
grep -iaR
history | grep
du
find
dir()
data()
type()
```
