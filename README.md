# CFB-FL
Call Frequency-Based Fault Localization


1. Start Docker:
	- [clone this repository]
	- docker build -t d4j --build-arg AGENT_VERSION=0.0.4 .

2. Create UDCS's:
	- [docker is running]
	- defects4j checkout -p [project] -v [bug][version] -w [output folder]
  
		e.g: defects4j checkout -p Lang -v 1b -w ./Lang_1b
	- cd [output folder]
  
		e.g: cd ./Lang_1b
	- defects4j compile
	- defects4j test
	- chmod -R 777 ./coverage
	([output folder]/coverage will contain the .trc files])

3. Calculate the FL-scores/ranks:
	- [docker is running]
	- cd /python_scripts
	- python3 -W ignore main.py --cov-folder=[output folder]/coverage/ --nameMapping=[output folder]/coverage/trace.trc.names --change=./changed_methods/Lang-changes.csv --bugID=[bug]
  
		e.g: python3 -W ignore main.py --cov-folder=/defects4j/Lang_1b/coverage/ --nameMapping=/defects4j/Lang_1b/coverage/trace.trc.names --change=./changed_methods/Lang-changes.csv --bugID=1
