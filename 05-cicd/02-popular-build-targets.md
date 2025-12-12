# 🚀 1. MAVEN (Java ecosystems)

Maven is the legacy-aligned, enterprise-friendly build orchestrator.

Targets / Lifecycle Phases
Build Target	      Maven Command	                        What It Actually Does
Build	                mvn compile	                Compiles Java sources → .class files.
Test	                mvn test	                Runs unit tests (Surefire).
Package	                mvn package	                Builds JAR/WAR artifacts.
Deploy	                mvn deploy	                Pushes artifact to Maven repo (Nexus/Artifactory).
Clean	                mvn clean	                Removes target/ directory.

# 🚀 2. GRADLE (Modern Java/Kotlin)

Gradle = performance optimization meets flexibility.

Targets / Tasks
Build Target	Gradle Command	                        Value Prop
Build	        gradle build	                    Full build pipeline: compile + test + package.
Test	        gradle test	                        Runs test suites.
Package	        gradle assemble	                    Generates JAR/WAR without running tests.
Deploy	        gradle publish	                    Publishes artifacts to repo.
Clean	        gradle clean	                    Cleans build/ directory.

# 🚀 3. ANT (Legacy enterprises still love this)

Ant gives full control with XML-based build logic.

Build Target	Ant Command (build.xml target)	            Description
Build	        ant compile	                            Compiles source.
Test	        ant test	                            Executes JUnit tests.
Package	        ant jar or ant war	                    Creates packaged artifacts.
Deploy	        ant deploy	                            Custom deployment logic (SSH copy, JBoss deploy, etc).
Clean	        ant clean	                            Removes build outputs.

# 🚀 4. NODE / NPM / YARN (Frontend & JS apps)

JS stacks move fast but structure stays consistent.

Targets via Scripts
Build Target	NPM Script	                                Meaning
Build	        npm run build	                        Create production bundle (dist/, build/).
Test	        npm test	                            Jest/Mocha tests.
Package	        npm pack	                            Produce .tgz artifact.
Deploy	        npm run deploy	                        Publish to CDN, S3, Vercel, or custom task.
Clean	        rm -rf node_modules / custom script	    Reset environment.

# 🚀 5. PYTHON (setuptools / Poetry)

Python packaging is ecosystem-driven.

Targets
Build Target	Command	                                        Details
Build	        python setup.py build or poetry build	        Builds distributables.
Test	        pytest	                                        Test execution.
Package	        python setup.py sdist bdist_wheel	            Wheel + source dist.
Deploy	        twine upload dist/*	                            Publish to PyPI.
Clean	        rm -rf build dist *.egg-info	                Clean workspace.

# 🚀 6. DOCKER (Containerized build pipeline)

Infra-aligned engineering staple.

Targets
Build Target	    Command	                                    Outcome
Build	           docker build -t app:v1 .	                Container image build.
Test	           Use Test Containers / separate stage	    Externalized test suite.
Package	           Docker image is the package	            N/A.
Deploy	           docker push	                            Ship to ACR/ECR/DockerHub.
Clean	           docker system prune	                    Remove unused artifacts.