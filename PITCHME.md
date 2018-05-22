## Project CI Anywhere
*A universal CI abstraction layer*

![Image](./assets/BcCube128.png)

---
### Bincrafters OSS Team

Find us online...
* https://bincrafters.github.io
* https://twitter.com/bincrafters
* https://github.com/bincrafters
* https://opencollective.com/bincrafters

---
### Universal CI Specifications
* Generalize common CI features 
* Decouple selected logic from CI implementation
* Inspired by OpenAPI, OpenSAM, specs 
* Do in Python

---
### CI Anywhere - Prior Art
* github.com/solvingj/go-github-release-test
* Conan Package Tools
	* Run python build.py anywhere,  CI or Local
	* Incubating and Evolving for 2+ years
	* Features for both enterprise and OSS CI's
	* Primitive yet brilliant and invaluable
	
---
### CI Anywhere - Motivation 1/2
* Any non-trivial scripting with YML is aweful
* OS-Specific scripting languages have issues
* CI's have 90% similar features
	* Proprietary Pmplementations
* Reproducing a CI job locally is invaluable
	* Usually not possible
* Lots of redundant hand-rolled boilerplate
* Typically no "unit-testing" for scripts

---
### CI Anywhere - Motivation 2/2
* Choosing and configuring a new CI is extremely painful
* Modern CI's are all good at some things, bad at others
* Most CI services struggle to support new technology
* Proprietary plugins needed for seemingly basic things
* Adding/changing CI services becoming more common

---
### CI Anywhere - Conan Package Tools 1/3
* Great as a reference for a generalized implementation
* Standardizes universal boilerplate tasks:
* Docker:
	* Optionally update container with pull 
	* Optionally update code in container before run
	* Mounting current working directory
	* sudo both inside and outside docker commands
	* Docker entry script lets user do anything pre-build

---
### CI Anywhere - Conan Package Tools 2/3
* Itelligently layers defaults, env vars, script params
* Artifact publishing and credential pre-verification
* Git branch detection and commit parsing
* Shows importance of language-specific customizability

---
### CI Anywhere - Conan Package Tools 3/3
* More accessible extensibility model (code sharing)
* Simply create and share python modules via pypi repo
* Bincrafters package tools good example
* Compare with creating a custom plugin for CI XYZ
* Jenkins just added "Shared Libraries" feature: 
	* Nice but proprietary

---
### Travis example
```yml
before_install: python ci/travis_pipeline.py -step_name before_install
install: python ci/travis_pipeline.py -step_name install
script: python ci/travis_pipeline.py -step_name script
after_success: python ci/travis_pipeline.py -step_name after_success
```
---
### Appveyor example
```yml
install: python ci/appveyor_pipeline.py -step_name install
build_script: python ci/appveyor_pipeline.py -step_name build_script
after_build: python ci/appveyor_pipeline.py -step_name after_build
deploy_script: python ci/appveyor_pipeline.py -step_name deploy_script
```
---
### Phase 1 - OSS
* Start by borrowing lots of logic from CPT
* Add more general commit parsing ("[skip travis]", etc)
* Add more "publish" helpers (bintray, packagecloud, etc)


---
### Phase 2 - Enterprise
* CPT does bypass some novel visibility features of CI 
	* Test coverage  
* Explore making use of some native features of each CI
* Potentially create CI Anywhere plugins for Jenkins/Etc.
