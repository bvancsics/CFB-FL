1. Start Docker:
	- [clone this repository]
	- docker build -t d4j --build-arg AGENT_VERSION=0.0.4 .

2. Create UDCS's:
	- Start docker:
		- docker run -i -t [IMAGE ID] /bin/bash
			(image-id: docker image ls)
			e.g: docker run -i -t 25a0b0ce79a0 /bin/bash  --> docker is running
	- Download a Defects4J-bug
		- defects4j checkout -p [project] -v [bug][version] -w [output folder]
			e.g: defects4j checkout -p Lang -v 1b -w ./Lang_1b --> 1th bug of Lang has been downloaded into /defects4j/Lang_1b folder
	- Enter bug's directory:
		- cd [output folder]
			e.g: cd ./Lang_1b --> current workdir is /defects4j/Lang_1b
	- Compile project:
		- defects4j compile --> the source code has been compiled
	- Run tests:
		- defects4j test --> [output folder]/coverage will contain the .trc files
	- Set permissions:
		- chmod -R 777 ./coverage
	

3. Calculate the FL-scores/ranks:
	- [docker is running]
	- cd /python_scripts  --> current workdir is /python_scripts
	- python3 -W ignore main.py --cov-folder=[output folder]/coverage/ --nameMapping=[output folder]/coverage/trace.trc.names --change=./changed_methods/Lang-changes.csv --bugID=[bug]
		e.g: python3 -W ignore main.py --cov-folder=/defects4j/Lang_1b/coverage/ --nameMapping=/defects4j/Lang_1b/coverage/trace.trc.names --change=./changed_methods/Lang-changes.csv --bugID=1 --> rank of the bug has been calculated