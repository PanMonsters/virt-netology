# Домашнее задание к занятию "09.05 Teamcity"

---
## Подготовка к выполнению
1. В Ya.Cloud создайте новый инстанс (4CPU4RAM) на основе образа `jetbrains/teamcity-server`
2. Дождитесь запуска teamcity, выполните первоначальную настройку
3. Создайте ещё один инстанс(2CPU4RAM) на основе образа `jetbrains/teamcity-agent`. Пропишите к нему переменную окружения `SERVER_URL: "http://<teamcity_url>:8111"`
4. Авторизуйте агент
5. Сделайте fork [репозитория](https://github.com/aragastmatb/example-teamcity)
6. Создать VM (2CPU4RAM) и запустить [playbook](./infrastructure)

## Основная часть

1. Создайте новый проект в teamcity на основе fork

2. Сделайте autodetect конфигурации

![image](https://github.com/PanMonsters/virt-netology/blob/3487ac808404f4fe730947472a81185521818bbf/image/9.5_1.png)

3. Сохраните необходимые шаги, запустите первую сборку master'a

![image](https://github.com/PanMonsters/virt-netology/blob/3487ac808404f4fe730947472a81185521818bbf/image/9.5_2.png)

<details><summary>Logs</summary>

```
[10:39:13]The build is removed from the queue to be prepared for the start
[10:39:13]Collecting changes in 1 VCS root (1s)
[10:39:13][Collecting changes in 1 VCS root] VCS Root details
[10:39:13][VCS Root details] "git@github.com:PanMonsters/example-teamcity.git#refs/heads/master" {instance id=1, parent internal id=1, parent id=Netology_GitGithubComPanMonstersExampleTeamcityGitRefsHeadsMaster, description: "git@github.com:PanMonsters/example-teamcity.git#refs/heads/master"}
[10:39:15][Collecting changes in 1 VCS root] Compute revision for 'git@github.com:PanMonsters/example-teamcity.git#refs/heads/master'
[10:39:15][Compute revision for 'git@github.com:PanMonsters/example-teamcity.git#refs/heads/master'] Upper limit revision: bd3bcfbfa25c0076df0a9a35343b865dc77ebfc2
[10:39:15][Compute revision for 'git@github.com:PanMonsters/example-teamcity.git#refs/heads/master'] The first revision that was detected in the branch refs/heads/master: bd3bcfbfa25c0076df0a9a35343b865dc77ebfc2
[10:39:15][Compute revision for 'git@github.com:PanMonsters/example-teamcity.git#refs/heads/master'] Cannot find modification in TeamCity database with revision bd3bcfbfa25c0076df0a9a35343b865dc77ebfc2
[10:39:15][Compute revision for 'git@github.com:PanMonsters/example-teamcity.git#refs/heads/master'] Computed revision: bd3bcfbfa25c0076df0a9a35343b865dc77ebfc2
[10:39:15]Starting the build on the agent "teamcity-agent"
[10:39:16]Updating tools for build
[10:39:16][Updating tools for build] Found 1 tool used by the build: maven3_6
[10:39:16][Updating tools for build] Tool maven3_6 updated successfully
[10:39:16]Clearing temporary directory: /opt/buildagent/temp/buildTmp
[10:39:17]Publishing internal artifacts
[10:39:17][Publishing internal artifacts] Publishing 1 file using [WebPublisher]
[10:39:17][Publishing internal artifacts] Publishing 1 file using [ArtifactsCachePublisherImpl]
[10:39:17]Full checkout enforced. Reason: [Checkout directory is empty or doesn't exist]
[10:39:17]Will perform clean checkout. Reason: Checkout directory is empty or doesn't exist
[10:39:17]Checkout directory: /opt/buildagent/work/4dad5dc52ced311f
[10:39:17]Updating sources: auto checkout (on agent) (9s)
[10:39:17][Updating sources] Will use agent side checkout
[10:39:17][Updating sources] VCS Root: git@github.com:PanMonsters/example-teamcity.git#refs/heads/master (9s)
[10:39:17][VCS Root: git@github.com:PanMonsters/example-teamcity.git#refs/heads/master] revision: bd3bcfbfa25c0076df0a9a35343b865dc77ebfc2
[10:39:17][VCS Root: git@github.com:PanMonsters/example-teamcity.git#refs/heads/master] Git version: 2.36.1.0
[10:39:17][VCS Root: git@github.com:PanMonsters/example-teamcity.git#refs/heads/master] Update git mirror (/opt/buildagent/system/git/git-463B453E.git) (6s)
[10:39:23][VCS Root: git@github.com:PanMonsters/example-teamcity.git#refs/heads/master] Update checkout directory (/opt/buildagent/work/4dad5dc52ced311f) (2s)
[10:39:26]Step 1/1: Maven (27s)
[10:39:26][Step 1/1] Initial M2_HOME not set
[10:39:26][Step 1/1] Current M2_HOME = /opt/buildagent/tools/maven3_6
[10:39:26][Step 1/1] PATH = /opt/buildagent/tools/maven3_6/bin:/opt/java/openjdk/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
[10:39:26][Step 1/1] Using watcher: /opt/buildagent/plugins/mavenPlugin/maven-watcher-jdk17/maven-watcher-agent.jar
[10:39:26][Step 1/1] Using agent local repository at /opt/buildagent/system/jetbrains.maven.runner/maven.repo.local
[10:39:26][Step 1/1] *** Start reading the project structure ***
[10:39:30][Step 1/1] Initial MAVEN_OPTS not set
[10:39:30][Step 1/1] Current MAVEN_OPTS not set
[10:39:30][Step 1/1] Starting: /opt/java/openjdk/bin/java -Dagent.home.dir=/opt/buildagent -Dagent.name=teamcity-agent -Dagent.ownPort=9090 -Dagent.work.dir=/opt/buildagent/work -Dbuild.number=1 -Dbuild.vcs.number=bd3bcfbfa25c0076df0a9a35343b865dc77ebfc2 -Dbuild.vcs.number.1=bd3bcfbfa25c0076df0a9a35343b865dc77ebfc2 -Dbuild.vcs.number.Netology_GitGithubComPanMonstersExampleTeamcityGitRefsHeadsMaster=bd3bcfbfa25c0076df0a9a35343b865dc77ebfc2 -Dclassworlds.conf=/opt/buildagent/temp/buildTmp/teamcity.m2.conf -Dcom.jetbrains.maven.watcher.report.file=/opt/buildagent/temp/buildTmp/maven-build-info.xml -Dec2.instance-id=epdnr2ph4agcjm1rshbo -Dec2.local-hostname=teamcity-agent.ru-central1.internal -Dec2.local-ipv4=172.16.0.17 -Dec2.public-hostname=130.193.43.16 -Dec2.public-ipv4=130.193.43.16 -Djava.io.tmpdir=/opt/buildagent/temp/buildTmp -Dmaven.home=/opt/buildagent/tools/maven3_6 -Dmaven.multiModuleProjectDirectory=/opt/buildagent/work/4dad5dc52ced311f -Dteamcity.agent.cpuBenchmark=445 -Dteamcity.agent.dotnet.agent_url=http://localhost:9090/RPC2 -Dteamcity.agent.dotnet.build_id=1 -Dteamcity.auth.password=******* -Dteamcity.auth.userId=TeamCityBuildId=1 -Dteamcity.build.changedFiles.file=/opt/buildagent/temp/buildTmp/changedFiles18380407497919013739.txt -Dteamcity.build.checkoutDir=/opt/buildagent/work/4dad5dc52ced311f -Dteamcity.build.id=1 -Dteamcity.build.properties.file=/opt/buildagent/temp/buildTmp/teamcity.build15754385149996164060.properties -Dteamcity.build.tempDir=/opt/buildagent/temp/buildTmp -Dteamcity.build.workingDir=/opt/buildagent/work/4dad5dc52ced311f -Dteamcity.buildConfName=Build -Dteamcity.buildType.id=Netology_Build -Dteamcity.configuration.properties.file=/opt/buildagent/temp/buildTmp/teamcity.config11754278782065081027.properties -Dteamcity.maven.watcher.home=/opt/buildagent/plugins/mavenPlugin/maven-watcher-jdk17 -Dteamcity.projectName=netology -Dteamcity.runner.properties.file=/opt/buildagent/temp/buildTmp/teamcity.runner2507692390646276429.properties -Dteamcity.tests.recentlyFailedTests.file=/opt/buildagent/temp/buildTmp/testsToRunFirst4578355233386267214.txt "-Dteamcity.version=2022.04.1 (build 108575)" -Dmaven.repo.local=/opt/buildagent/system/jetbrains.maven.runner/maven.repo.local -classpath /opt/buildagent/tools/maven3_6/boot/plexus-classworlds-2.6.0.jar: org.codehaus.plexus.classworlds.launcher.Launcher -f /opt/buildagent/work/4dad5dc52ced311f/pom.xml -B -Dmaven.test.failure.ignore=true clean test
[10:39:30][Step 1/1] in directory: /opt/buildagent/work/4dad5dc52ced311f
[10:39:32][Step 1/1] [INFO] Scanning for projects...
[10:39:32][Step 1/1] [INFO] 
[10:39:32][Step 1/1] [INFO] -----------------------< org.netology:plaindoll >-----------------------
[10:39:32][Step 1/1] [INFO] Building plaindoll 0.0.1
[10:39:32][Step 1/1] [INFO] --------------------------------[ jar ]---------------------------------
[10:39:32][Step 1/1] org.netology:plaindoll (21s)
[10:39:32][Step 1/1] Importing data from '/opt/buildagent/work/4dad5dc52ced311f/target/surefire-reports/TEST-*.xml' (not existing file) with 'surefire' processor
[10:39:32][Step 1/1] Importing data from '/opt/buildagent/work/4dad5dc52ced311f/target/failsafe-reports/TEST-*.xml' (not existing file) with 'surefire' processor
[10:39:32][Step 1/1] Surefire report watcher
[10:39:32][Surefire report watcher] Watching paths:
[10:39:32][Surefire report watcher] /opt/buildagent/work/4dad5dc52ced311f/target/surefire-reports/TEST-*.xml
[10:39:32][Step 1/1] Surefire report watcher
[10:39:32][Surefire report watcher] Watching paths:
[10:39:32][Surefire report watcher] /opt/buildagent/work/4dad5dc52ced311f/target/failsafe-reports/TEST-*.xml
[10:39:32][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/plugins/maven-clean-plugin/2.5/maven-clean-plugin-2.5.pom
[10:39:33][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/plugins/maven-clean-plugin/2.5/maven-clean-plugin-2.5.pom (3.9 kB at 6.4 kB/s)
[10:39:33][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/plugins/maven-plugins/22/maven-plugins-22.pom
[10:39:33][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/plugins/maven-plugins/22/maven-plugins-22.pom (13 kB at 115 kB/s)
[10:39:33][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-parent/21/maven-parent-21.pom
[10:39:33][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-parent/21/maven-parent-21.pom (26 kB at 198 kB/s)
[10:39:33][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/apache/10/apache-10.pom
[10:39:33][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/apache/10/apache-10.pom (15 kB at 145 kB/s)
[10:39:33][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/plugins/maven-clean-plugin/2.5/maven-clean-plugin-2.5.jar
[10:39:34][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/plugins/maven-clean-plugin/2.5/maven-clean-plugin-2.5.jar (25 kB at 197 kB/s)
[10:39:34][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/plugins/maven-resources-plugin/2.6/maven-resources-plugin-2.6.pom
[10:39:34][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/plugins/maven-resources-plugin/2.6/maven-resources-plugin-2.6.pom (8.1 kB at 80 kB/s)
[10:39:34][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/plugins/maven-plugins/23/maven-plugins-23.pom
[10:39:34][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/plugins/maven-plugins/23/maven-plugins-23.pom (9.2 kB at 96 kB/s)
[10:39:34][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-parent/22/maven-parent-22.pom
[10:39:34][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-parent/22/maven-parent-22.pom (30 kB at 266 kB/s)
[10:39:34][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/apache/11/apache-11.pom
[10:39:34][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/apache/11/apache-11.pom (15 kB at 144 kB/s)
[10:39:34][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/plugins/maven-resources-plugin/2.6/maven-resources-plugin-2.6.jar
[10:39:34][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/plugins/maven-resources-plugin/2.6/maven-resources-plugin-2.6.jar (30 kB at 246 kB/s)
[10:39:34][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/plugins/maven-compiler-plugin/3.1/maven-compiler-plugin-3.1.pom
[10:39:34][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/plugins/maven-compiler-plugin/3.1/maven-compiler-plugin-3.1.pom (10 kB at 93 kB/s)
[10:39:34][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/plugins/maven-plugins/24/maven-plugins-24.pom
[10:39:34][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/plugins/maven-plugins/24/maven-plugins-24.pom (11 kB at 115 kB/s)
[10:39:34][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-parent/23/maven-parent-23.pom
[10:39:35][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-parent/23/maven-parent-23.pom (33 kB at 296 kB/s)
[10:39:35][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/apache/13/apache-13.pom
[10:39:35][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/apache/13/apache-13.pom (14 kB at 133 kB/s)
[10:39:35][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/plugins/maven-compiler-plugin/3.1/maven-compiler-plugin-3.1.jar
[10:39:35][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/plugins/maven-compiler-plugin/3.1/maven-compiler-plugin-3.1.jar (43 kB at 338 kB/s)
[10:39:35][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/plugins/maven-surefire-plugin/2.12.4/maven-surefire-plugin-2.12.4.pom
[10:39:35][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/plugins/maven-surefire-plugin/2.12.4/maven-surefire-plugin-2.12.4.pom (10 kB at 105 kB/s)
[10:39:35][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/surefire/surefire/2.12.4/surefire-2.12.4.pom
[10:39:35][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/surefire/surefire/2.12.4/surefire-2.12.4.pom (14 kB at 145 kB/s)
[10:39:35][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/plugins/maven-surefire-plugin/2.12.4/maven-surefire-plugin-2.12.4.jar
[10:39:35][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/plugins/maven-surefire-plugin/2.12.4/maven-surefire-plugin-2.12.4.jar (30 kB at 293 kB/s)
[10:39:35][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/junit/junit/4.12/junit-4.12.pom
[10:39:35][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/junit/junit/4.12/junit-4.12.pom (24 kB at 237 kB/s)
[10:39:35][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/hamcrest/hamcrest-core/1.3/hamcrest-core-1.3.pom
[10:39:35][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/hamcrest/hamcrest-core/1.3/hamcrest-core-1.3.pom (766 B at 8.5 kB/s)
[10:39:35][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/hamcrest/hamcrest-parent/1.3/hamcrest-parent-1.3.pom
[10:39:35][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/hamcrest/hamcrest-parent/1.3/hamcrest-parent-1.3.pom (2.0 kB at 22 kB/s)
[10:39:35][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/junit/junit/4.12/junit-4.12.jar
[10:39:35][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/hamcrest/hamcrest-core/1.3/hamcrest-core-1.3.jar
[10:39:36][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/junit/junit/4.12/junit-4.12.jar (315 kB at 1.4 MB/s)
[10:39:36][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/hamcrest/hamcrest-core/1.3/hamcrest-core-1.3.jar (45 kB at 162 kB/s)
[10:39:36][Step 1/1] [INFO] 
[10:39:36][Step 1/1] [INFO] --- maven-clean-plugin:2.5:clean (default-clean) @ plaindoll ---
[10:39:36][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-plugin-api/2.0.6/maven-plugin-api-2.0.6.pom
[10:39:36][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-plugin-api/2.0.6/maven-plugin-api-2.0.6.pom (1.5 kB at 14 kB/s)
[10:39:36][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven/2.0.6/maven-2.0.6.pom
[10:39:36][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven/2.0.6/maven-2.0.6.pom (9.0 kB at 93 kB/s)
[10:39:36][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-parent/5/maven-parent-5.pom
[10:39:36][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-parent/5/maven-parent-5.pom (15 kB at 151 kB/s)
[10:39:36][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/apache/3/apache-3.pom
[10:39:36][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/apache/3/apache-3.pom (3.4 kB at 35 kB/s)
[10:39:36][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus-utils/3.0/plexus-utils-3.0.pom
[10:39:36][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus-utils/3.0/plexus-utils-3.0.pom (4.1 kB at 41 kB/s)
[10:39:36][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/sonatype/spice/spice-parent/16/spice-parent-16.pom
[10:39:36][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/sonatype/spice/spice-parent/16/spice-parent-16.pom (8.4 kB at 84 kB/s)
[10:39:36][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/sonatype/forge/forge-parent/5/forge-parent-5.pom
[10:39:36][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/sonatype/forge/forge-parent/5/forge-parent-5.pom (8.4 kB at 87 kB/s)
[10:39:36][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-plugin-api/2.0.6/maven-plugin-api-2.0.6.jar
[10:39:36][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus-utils/3.0/plexus-utils-3.0.jar
[10:39:37][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-plugin-api/2.0.6/maven-plugin-api-2.0.6.jar (13 kB at 110 kB/s)
[10:39:37][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus-utils/3.0/plexus-utils-3.0.jar (226 kB at 1.8 MB/s)
[10:39:37][Step 1/1] [INFO] 
[10:39:37][Step 1/1] [INFO] --- maven-resources-plugin:2.6:resources (default-resources) @ plaindoll ---
[10:39:37][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-project/2.0.6/maven-project-2.0.6.pom
[10:39:37][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-project/2.0.6/maven-project-2.0.6.pom (2.6 kB at 28 kB/s)
[10:39:37][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-settings/2.0.6/maven-settings-2.0.6.pom
[10:39:37][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-settings/2.0.6/maven-settings-2.0.6.pom (2.0 kB at 22 kB/s)
[10:39:37][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-model/2.0.6/maven-model-2.0.6.pom
[10:39:37][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-model/2.0.6/maven-model-2.0.6.pom (3.0 kB at 33 kB/s)
[10:39:37][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus-utils/1.4.1/plexus-utils-1.4.1.pom
[10:39:37][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus-utils/1.4.1/plexus-utils-1.4.1.pom (1.9 kB at 21 kB/s)
[10:39:37][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus/1.0.11/plexus-1.0.11.pom
[10:39:37][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus/1.0.11/plexus-1.0.11.pom (9.0 kB at 99 kB/s)
[10:39:37][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus-container-default/1.0-alpha-9-stable-1/plexus-container-default-1.0-alpha-9-stable-1.pom
[10:39:37][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus-container-default/1.0-alpha-9-stable-1/plexus-container-default-1.0-alpha-9-stable-1.pom (3.9 kB at 43 kB/s)
[10:39:37][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus-containers/1.0.3/plexus-containers-1.0.3.pom
[10:39:37][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus-containers/1.0.3/plexus-containers-1.0.3.pom (492 B at 4.3 kB/s)
[10:39:37][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus/1.0.4/plexus-1.0.4.pom
[10:39:37][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus/1.0.4/plexus-1.0.4.pom (5.7 kB at 63 kB/s)
[10:39:37][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/junit/junit/3.8.1/junit-3.8.1.pom
[10:39:38][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/junit/junit/3.8.1/junit-3.8.1.pom (998 B at 11 kB/s)
[10:39:38][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus-utils/1.0.4/plexus-utils-1.0.4.pom
[10:39:38][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus-utils/1.0.4/plexus-utils-1.0.4.pom (6.9 kB at 75 kB/s)
[10:39:38][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/classworlds/classworlds/1.1-alpha-2/classworlds-1.1-alpha-2.pom
[10:39:38][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/classworlds/classworlds/1.1-alpha-2/classworlds-1.1-alpha-2.pom (3.1 kB at 36 kB/s)
[10:39:38][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-profile/2.0.6/maven-profile-2.0.6.pom
[10:39:38][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-profile/2.0.6/maven-profile-2.0.6.pom (2.0 kB at 22 kB/s)
[10:39:38][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-artifact-manager/2.0.6/maven-artifact-manager-2.0.6.pom
[10:39:38][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-artifact-manager/2.0.6/maven-artifact-manager-2.0.6.pom (2.6 kB at 30 kB/s)
[10:39:38][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-repository-metadata/2.0.6/maven-repository-metadata-2.0.6.pom
[10:39:38][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-repository-metadata/2.0.6/maven-repository-metadata-2.0.6.pom (1.9 kB at 21 kB/s)
[10:39:38][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-artifact/2.0.6/maven-artifact-2.0.6.pom
[10:39:38][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-artifact/2.0.6/maven-artifact-2.0.6.pom (1.6 kB at 18 kB/s)
[10:39:38][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-plugin-registry/2.0.6/maven-plugin-registry-2.0.6.pom
[10:39:38][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-plugin-registry/2.0.6/maven-plugin-registry-2.0.6.pom (1.9 kB at 21 kB/s)
[10:39:38][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-core/2.0.6/maven-core-2.0.6.pom
[10:39:38][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-core/2.0.6/maven-core-2.0.6.pom (6.7 kB at 76 kB/s)
[10:39:38][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-plugin-parameter-documenter/2.0.6/maven-plugin-parameter-documenter-2.0.6.pom
[10:39:38][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-plugin-parameter-documenter/2.0.6/maven-plugin-parameter-documenter-2.0.6.pom (1.9 kB at 21 kB/s)
[10:39:38][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/reporting/maven-reporting-api/2.0.6/maven-reporting-api-2.0.6.pom
[10:39:39][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/reporting/maven-reporting-api/2.0.6/maven-reporting-api-2.0.6.pom (1.8 kB at 16 kB/s)
[10:39:39][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/reporting/maven-reporting/2.0.6/maven-reporting-2.0.6.pom
[10:39:39][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/reporting/maven-reporting/2.0.6/maven-reporting-2.0.6.pom (1.4 kB at 15 kB/s)
[10:39:39][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/doxia/doxia-sink-api/1.0-alpha-7/doxia-sink-api-1.0-alpha-7.pom
[10:39:39][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/doxia/doxia-sink-api/1.0-alpha-7/doxia-sink-api-1.0-alpha-7.pom (424 B at 4.8 kB/s)
[10:39:39][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/doxia/doxia/1.0-alpha-7/doxia-1.0-alpha-7.pom
[10:39:39][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/doxia/doxia/1.0-alpha-7/doxia-1.0-alpha-7.pom (3.9 kB at 42 kB/s)
[10:39:39][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-error-diagnostics/2.0.6/maven-error-diagnostics-2.0.6.pom
[10:39:39][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-error-diagnostics/2.0.6/maven-error-diagnostics-2.0.6.pom (1.7 kB at 17 kB/s)
[10:39:39][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/commons-cli/commons-cli/1.0/commons-cli-1.0.pom
[10:39:39][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/commons-cli/commons-cli/1.0/commons-cli-1.0.pom (2.1 kB at 22 kB/s)
[10:39:39][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-plugin-descriptor/2.0.6/maven-plugin-descriptor-2.0.6.pom
[10:39:39][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-plugin-descriptor/2.0.6/maven-plugin-descriptor-2.0.6.pom (2.0 kB at 22 kB/s)
[10:39:39][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus-interactivity-api/1.0-alpha-4/plexus-interactivity-api-1.0-alpha-4.pom
[10:39:39][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus-interactivity-api/1.0-alpha-4/plexus-interactivity-api-1.0-alpha-4.pom (7.1 kB at 76 kB/s)
[10:39:39][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-monitor/2.0.6/maven-monitor-2.0.6.pom
[10:39:39][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-monitor/2.0.6/maven-monitor-2.0.6.pom (1.3 kB at 14 kB/s)
[10:39:39][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/classworlds/classworlds/1.1/classworlds-1.1.pom
[10:39:39][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/classworlds/classworlds/1.1/classworlds-1.1.pom (3.3 kB at 39 kB/s)
[10:39:39][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus-utils/2.0.5/plexus-utils-2.0.5.pom
[10:39:39][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus-utils/2.0.5/plexus-utils-2.0.5.pom (3.3 kB at 38 kB/s)
[10:39:39][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus/2.0.6/plexus-2.0.6.pom
[10:39:40][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus/2.0.6/plexus-2.0.6.pom (17 kB at 188 kB/s)
[10:39:40][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/shared/maven-filtering/1.1/maven-filtering-1.1.pom
[10:39:40][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/shared/maven-filtering/1.1/maven-filtering-1.1.pom (5.8 kB at 63 kB/s)
[10:39:40][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/shared/maven-shared-components/17/maven-shared-components-17.pom
[10:39:40][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/shared/maven-shared-components/17/maven-shared-components-17.pom (8.7 kB at 95 kB/s)
[10:39:40][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus-utils/1.5.15/plexus-utils-1.5.15.pom
[10:39:40][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus-utils/1.5.15/plexus-utils-1.5.15.pom (6.8 kB at 68 kB/s)
[10:39:40][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus/2.0.2/plexus-2.0.2.pom
[10:39:40][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus/2.0.2/plexus-2.0.2.pom (12 kB at 133 kB/s)
[10:39:40][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus-interpolation/1.12/plexus-interpolation-1.12.pom
[10:39:40][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus-interpolation/1.12/plexus-interpolation-1.12.pom (889 B at 9.9 kB/s)
[10:39:40][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus-components/1.1.14/plexus-components-1.1.14.pom
[10:39:40][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus-components/1.1.14/plexus-components-1.1.14.pom (5.8 kB at 62 kB/s)
[10:39:40][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/sonatype/plexus/plexus-build-api/0.0.4/plexus-build-api-0.0.4.pom
[10:39:40][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/sonatype/plexus/plexus-build-api/0.0.4/plexus-build-api-0.0.4.pom (2.9 kB at 33 kB/s)
[10:39:40][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/sonatype/spice/spice-parent/10/spice-parent-10.pom
[10:39:40][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/sonatype/spice/spice-parent/10/spice-parent-10.pom (3.0 kB at 33 kB/s)
[10:39:40][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/sonatype/forge/forge-parent/3/forge-parent-3.pom
[10:39:40][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/sonatype/forge/forge-parent/3/forge-parent-3.pom (5.0 kB at 59 kB/s)
[10:39:40][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus-utils/1.5.8/plexus-utils-1.5.8.pom
[10:39:41][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus-utils/1.5.8/plexus-utils-1.5.8.pom (8.1 kB at 94 kB/s)
[10:39:41][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus-interpolation/1.13/plexus-interpolation-1.13.pom
[10:39:41][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus-interpolation/1.13/plexus-interpolation-1.13.pom (890 B at 10 kB/s)
[10:39:41][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus-components/1.1.15/plexus-components-1.1.15.pom
[10:39:41][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus-components/1.1.15/plexus-components-1.1.15.pom (2.8 kB at 33 kB/s)
[10:39:41][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus/2.0.3/plexus-2.0.3.pom
[10:39:41][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus/2.0.3/plexus-2.0.3.pom (15 kB at 176 kB/s)
[10:39:41][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-project/2.0.6/maven-project-2.0.6.jar
[10:39:41][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-profile/2.0.6/maven-profile-2.0.6.jar
[10:39:41][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-artifact-manager/2.0.6/maven-artifact-manager-2.0.6.jar
[10:39:41][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-plugin-registry/2.0.6/maven-plugin-registry-2.0.6.jar
[10:39:41][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-core/2.0.6/maven-core-2.0.6.jar
[10:39:41][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-project/2.0.6/maven-project-2.0.6.jar (116 kB at 1.0 MB/s)
[10:39:41][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-plugin-parameter-documenter/2.0.6/maven-plugin-parameter-documenter-2.0.6.jar
[10:39:41][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-profile/2.0.6/maven-profile-2.0.6.jar (35 kB at 289 kB/s)
[10:39:41][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/reporting/maven-reporting-api/2.0.6/maven-reporting-api-2.0.6.jar
[10:39:41][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-plugin-parameter-documenter/2.0.6/maven-plugin-parameter-documenter-2.0.6.jar (21 kB at 109 kB/s)
[10:39:41][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/doxia/doxia-sink-api/1.0-alpha-7/doxia-sink-api-1.0-alpha-7.jar
[10:39:41][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/reporting/maven-reporting-api/2.0.6/maven-reporting-api-2.0.6.jar (9.9 kB at 46 kB/s)
[10:39:41][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-repository-metadata/2.0.6/maven-repository-metadata-2.0.6.jar
[10:39:41][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-plugin-registry/2.0.6/maven-plugin-registry-2.0.6.jar (29 kB at 125 kB/s)
[10:39:41][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-error-diagnostics/2.0.6/maven-error-diagnostics-2.0.6.jar
[10:39:41][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-artifact-manager/2.0.6/maven-artifact-manager-2.0.6.jar (57 kB at 206 kB/s)
[10:39:41][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/commons-cli/commons-cli/1.0/commons-cli-1.0.jar
[10:39:41][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/doxia/doxia-sink-api/1.0-alpha-7/doxia-sink-api-1.0-alpha-7.jar (5.9 kB at 21 kB/s)
[10:39:41][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-plugin-descriptor/2.0.6/maven-plugin-descriptor-2.0.6.jar
[10:39:41][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-repository-metadata/2.0.6/maven-repository-metadata-2.0.6.jar (24 kB at 78 kB/s)
[10:39:41][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus-interactivity-api/1.0-alpha-4/plexus-interactivity-api-1.0-alpha-4.jar
[10:39:41][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-core/2.0.6/maven-core-2.0.6.jar (152 kB at 472 kB/s)
[10:39:41][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/classworlds/classworlds/1.1/classworlds-1.1.jar
[10:39:41][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-error-diagnostics/2.0.6/maven-error-diagnostics-2.0.6.jar (14 kB at 41 kB/s)
[10:39:41][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-artifact/2.0.6/maven-artifact-2.0.6.jar
[10:39:41][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/commons-cli/commons-cli/1.0/commons-cli-1.0.jar (30 kB at 81 kB/s)
[10:39:41][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-settings/2.0.6/maven-settings-2.0.6.jar
[10:39:41][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-plugin-descriptor/2.0.6/maven-plugin-descriptor-2.0.6.jar (37 kB at 98 kB/s)
[10:39:41][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-model/2.0.6/maven-model-2.0.6.jar
[10:39:41][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus-interactivity-api/1.0-alpha-4/plexus-interactivity-api-1.0-alpha-4.jar (13 kB at 33 kB/s)
[10:39:41][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-monitor/2.0.6/maven-monitor-2.0.6.jar
[10:39:41][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/classworlds/classworlds/1.1/classworlds-1.1.jar (38 kB at 90 kB/s)
[10:39:41][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus-container-default/1.0-alpha-9-stable-1/plexus-container-default-1.0-alpha-9-stable-1.jar
[10:39:41][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-settings/2.0.6/maven-settings-2.0.6.jar (49 kB at 104 kB/s)
[10:39:41][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/junit/junit/3.8.1/junit-3.8.1.jar
[10:39:41][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-artifact/2.0.6/maven-artifact-2.0.6.jar (87 kB at 178 kB/s)
[10:39:41][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus-utils/2.0.5/plexus-utils-2.0.5.jar
[10:39:41][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-model/2.0.6/maven-model-2.0.6.jar (86 kB at 175 kB/s)
[10:39:41][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/shared/maven-filtering/1.1/maven-filtering-1.1.jar
[10:39:41][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-monitor/2.0.6/maven-monitor-2.0.6.jar (10 kB at 20 kB/s)
[10:39:41][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/sonatype/plexus/plexus-build-api/0.0.4/plexus-build-api-0.0.4.jar
[10:39:41][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus-container-default/1.0-alpha-9-stable-1/plexus-container-default-1.0-alpha-9-stable-1.jar (194 kB at 342 kB/s)
[10:39:41][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus-interpolation/1.13/plexus-interpolation-1.13.jar
[10:39:41][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/junit/junit/3.8.1/junit-3.8.1.jar (121 kB at 212 kB/s)
[10:39:41][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/shared/maven-filtering/1.1/maven-filtering-1.1.jar (43 kB at 73 kB/s)
[10:39:41][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/sonatype/plexus/plexus-build-api/0.0.4/plexus-build-api-0.0.4.jar (6.8 kB at 11 kB/s)
[10:39:41][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus-interpolation/1.13/plexus-interpolation-1.13.jar (61 kB at 91 kB/s)
[10:39:41][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus-utils/2.0.5/plexus-utils-2.0.5.jar (223 kB at 328 kB/s)
[10:39:42][Step 1/1] [WARNING] Using platform encoding (UTF-8 actually) to copy filtered resources, i.e. build is platform dependent!
[10:39:42][Step 1/1] [INFO] skip non existing resourceDirectory /opt/buildagent/work/4dad5dc52ced311f/src/main/resources
[10:39:42][Step 1/1] [INFO] 
[10:39:42][Step 1/1] [INFO] --- maven-compiler-plugin:3.1:compile (default-compile) @ plaindoll ---
[10:39:42][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-plugin-api/2.0.9/maven-plugin-api-2.0.9.pom
[10:39:42][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-plugin-api/2.0.9/maven-plugin-api-2.0.9.pom (1.5 kB at 13 kB/s)
[10:39:42][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven/2.0.9/maven-2.0.9.pom
[10:39:42][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven/2.0.9/maven-2.0.9.pom (19 kB at 191 kB/s)
[10:39:42][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-parent/8/maven-parent-8.pom
[10:39:42][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-parent/8/maven-parent-8.pom (24 kB at 249 kB/s)
[10:39:42][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/apache/4/apache-4.pom
[10:39:42][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/apache/4/apache-4.pom (4.5 kB at 45 kB/s)
[10:39:42][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-artifact/2.0.9/maven-artifact-2.0.9.pom
[10:39:42][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-artifact/2.0.9/maven-artifact-2.0.9.pom (1.6 kB at 14 kB/s)
[10:39:42][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus-utils/1.5.1/plexus-utils-1.5.1.pom
[10:39:42][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus-utils/1.5.1/plexus-utils-1.5.1.pom (2.3 kB at 24 kB/s)
[10:39:42][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-core/2.0.9/maven-core-2.0.9.pom
[10:39:42][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-core/2.0.9/maven-core-2.0.9.pom (7.8 kB at 82 kB/s)
[10:39:42][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-settings/2.0.9/maven-settings-2.0.9.pom
[10:39:42][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-settings/2.0.9/maven-settings-2.0.9.pom (2.1 kB at 16 kB/s)
[10:39:42][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-model/2.0.9/maven-model-2.0.9.pom
[10:39:43][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-model/2.0.9/maven-model-2.0.9.pom (3.1 kB at 34 kB/s)
[10:39:43][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-plugin-parameter-documenter/2.0.9/maven-plugin-parameter-documenter-2.0.9.pom
[10:39:43][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-plugin-parameter-documenter/2.0.9/maven-plugin-parameter-documenter-2.0.9.pom (2.0 kB at 18 kB/s)
[10:39:43][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-profile/2.0.9/maven-profile-2.0.9.pom
[10:39:43][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-profile/2.0.9/maven-profile-2.0.9.pom (2.0 kB at 22 kB/s)
[10:39:43][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-repository-metadata/2.0.9/maven-repository-metadata-2.0.9.pom
[10:39:43][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-repository-metadata/2.0.9/maven-repository-metadata-2.0.9.pom (1.9 kB at 21 kB/s)
[10:39:43][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-error-diagnostics/2.0.9/maven-error-diagnostics-2.0.9.pom
[10:39:43][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-error-diagnostics/2.0.9/maven-error-diagnostics-2.0.9.pom (1.7 kB at 19 kB/s)
[10:39:43][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-project/2.0.9/maven-project-2.0.9.pom
[10:39:43][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-project/2.0.9/maven-project-2.0.9.pom (2.7 kB at 29 kB/s)
[10:39:43][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-artifact-manager/2.0.9/maven-artifact-manager-2.0.9.pom
[10:39:43][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-artifact-manager/2.0.9/maven-artifact-manager-2.0.9.pom (2.7 kB at 29 kB/s)
[10:39:43][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-plugin-registry/2.0.9/maven-plugin-registry-2.0.9.pom
[10:39:43][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-plugin-registry/2.0.9/maven-plugin-registry-2.0.9.pom (2.0 kB at 20 kB/s)
[10:39:43][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-plugin-descriptor/2.0.9/maven-plugin-descriptor-2.0.9.pom
[10:39:43][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-plugin-descriptor/2.0.9/maven-plugin-descriptor-2.0.9.pom (2.1 kB at 23 kB/s)
[10:39:43][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-monitor/2.0.9/maven-monitor-2.0.9.pom
[10:39:43][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-monitor/2.0.9/maven-monitor-2.0.9.pom (1.3 kB at 14 kB/s)
[10:39:43][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-toolchain/1.0/maven-toolchain-1.0.pom
[10:39:44][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-toolchain/1.0/maven-toolchain-1.0.pom (3.4 kB at 36 kB/s)
[10:39:44][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/shared/maven-shared-utils/0.1/maven-shared-utils-0.1.pom
[10:39:44][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/shared/maven-shared-utils/0.1/maven-shared-utils-0.1.pom (4.0 kB at 37 kB/s)
[10:39:44][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/shared/maven-shared-components/18/maven-shared-components-18.pom
[10:39:44][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/shared/maven-shared-components/18/maven-shared-components-18.pom (4.9 kB at 52 kB/s)
[10:39:44][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/com/google/code/findbugs/jsr305/2.0.1/jsr305-2.0.1.pom
[10:39:44][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/com/google/code/findbugs/jsr305/2.0.1/jsr305-2.0.1.pom (965 B at 9.7 kB/s)
[10:39:44][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/shared/maven-shared-incremental/1.1/maven-shared-incremental-1.1.pom
[10:39:44][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/shared/maven-shared-incremental/1.1/maven-shared-incremental-1.1.pom (4.7 kB at 44 kB/s)
[10:39:44][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/shared/maven-shared-components/19/maven-shared-components-19.pom
[10:39:44][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/shared/maven-shared-components/19/maven-shared-components-19.pom (6.4 kB at 66 kB/s)
[10:39:44][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-plugin-api/2.2.1/maven-plugin-api-2.2.1.pom
[10:39:44][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-plugin-api/2.2.1/maven-plugin-api-2.2.1.pom (1.5 kB at 16 kB/s)
[10:39:44][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven/2.2.1/maven-2.2.1.pom
[10:39:44][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven/2.2.1/maven-2.2.1.pom (22 kB at 238 kB/s)
[10:39:44][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-parent/11/maven-parent-11.pom
[10:39:44][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-parent/11/maven-parent-11.pom (32 kB at 338 kB/s)
[10:39:44][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/apache/5/apache-5.pom
[10:39:45][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/apache/5/apache-5.pom (4.1 kB at 41 kB/s)
[10:39:45][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-core/2.2.1/maven-core-2.2.1.pom
[10:39:45][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-core/2.2.1/maven-core-2.2.1.pom (12 kB at 119 kB/s)
[10:39:45][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-settings/2.2.1/maven-settings-2.2.1.pom
[10:39:45][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-settings/2.2.1/maven-settings-2.2.1.pom (2.2 kB at 22 kB/s)
[10:39:45][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-model/2.2.1/maven-model-2.2.1.pom
[10:39:45][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-model/2.2.1/maven-model-2.2.1.pom (3.2 kB at 30 kB/s)
[10:39:45][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus-interpolation/1.11/plexus-interpolation-1.11.pom
[10:39:45][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus-interpolation/1.11/plexus-interpolation-1.11.pom (889 B at 8.6 kB/s)
[10:39:45][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-plugin-parameter-documenter/2.2.1/maven-plugin-parameter-documenter-2.2.1.pom
[10:39:45][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-plugin-parameter-documenter/2.2.1/maven-plugin-parameter-documenter-2.2.1.pom (2.0 kB at 22 kB/s)
[10:39:45][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/slf4j/slf4j-jdk14/1.5.6/slf4j-jdk14-1.5.6.pom
[10:39:45][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/slf4j/slf4j-jdk14/1.5.6/slf4j-jdk14-1.5.6.pom (1.9 kB at 21 kB/s)
[10:39:45][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/slf4j/slf4j-parent/1.5.6/slf4j-parent-1.5.6.pom
[10:39:45][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/slf4j/slf4j-parent/1.5.6/slf4j-parent-1.5.6.pom (7.9 kB at 86 kB/s)
[10:39:45][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/slf4j/slf4j-api/1.5.6/slf4j-api-1.5.6.pom
[10:39:45][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/slf4j/slf4j-api/1.5.6/slf4j-api-1.5.6.pom (3.0 kB at 30 kB/s)
[10:39:45][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/slf4j/jcl-over-slf4j/1.5.6/jcl-over-slf4j-1.5.6.pom
[10:39:45][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/slf4j/jcl-over-slf4j/1.5.6/jcl-over-slf4j-1.5.6.pom (2.2 kB at 24 kB/s)
[10:39:45][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-profile/2.2.1/maven-profile-2.2.1.pom
[10:39:46][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-profile/2.2.1/maven-profile-2.2.1.pom (2.2 kB at 23 kB/s)
[10:39:46][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-artifact/2.2.1/maven-artifact-2.2.1.pom
[10:39:46][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-artifact/2.2.1/maven-artifact-2.2.1.pom (1.6 kB at 17 kB/s)
[10:39:46][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-repository-metadata/2.2.1/maven-repository-metadata-2.2.1.pom
[10:39:46][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-repository-metadata/2.2.1/maven-repository-metadata-2.2.1.pom (1.9 kB at 20 kB/s)
[10:39:46][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-error-diagnostics/2.2.1/maven-error-diagnostics-2.2.1.pom
[10:39:46][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-error-diagnostics/2.2.1/maven-error-diagnostics-2.2.1.pom (1.7 kB at 19 kB/s)
[10:39:46][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-project/2.2.1/maven-project-2.2.1.pom
[10:39:46][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-project/2.2.1/maven-project-2.2.1.pom (2.8 kB at 30 kB/s)
[10:39:46][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-artifact-manager/2.2.1/maven-artifact-manager-2.2.1.pom
[10:39:46][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-artifact-manager/2.2.1/maven-artifact-manager-2.2.1.pom (3.1 kB at 33 kB/s)
[10:39:46][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/backport-util-concurrent/backport-util-concurrent/3.1/backport-util-concurrent-3.1.pom
[10:39:46][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/backport-util-concurrent/backport-util-concurrent/3.1/backport-util-concurrent-3.1.pom (880 B at 9.6 kB/s)
[10:39:46][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-plugin-registry/2.2.1/maven-plugin-registry-2.2.1.pom
[10:39:46][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-plugin-registry/2.2.1/maven-plugin-registry-2.2.1.pom (1.9 kB at 21 kB/s)
[10:39:46][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-plugin-descriptor/2.2.1/maven-plugin-descriptor-2.2.1.pom
[10:39:46][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-plugin-descriptor/2.2.1/maven-plugin-descriptor-2.2.1.pom (2.1 kB at 19 kB/s)
[10:39:46][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-monitor/2.2.1/maven-monitor-2.2.1.pom
[10:39:46][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-monitor/2.2.1/maven-monitor-2.2.1.pom (1.3 kB at 14 kB/s)
[10:39:46][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/sonatype/plexus/plexus-sec-dispatcher/1.3/plexus-sec-dispatcher-1.3.pom
[10:39:47][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/sonatype/plexus/plexus-sec-dispatcher/1.3/plexus-sec-dispatcher-1.3.pom (3.0 kB at 32 kB/s)
[10:39:47][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/sonatype/spice/spice-parent/12/spice-parent-12.pom
[10:39:47][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/sonatype/spice/spice-parent/12/spice-parent-12.pom (6.8 kB at 74 kB/s)
[10:39:47][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/sonatype/forge/forge-parent/4/forge-parent-4.pom
[10:39:47][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/sonatype/forge/forge-parent/4/forge-parent-4.pom (8.4 kB at 90 kB/s)
[10:39:47][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus-utils/1.5.5/plexus-utils-1.5.5.pom
[10:39:47][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus-utils/1.5.5/plexus-utils-1.5.5.pom (5.1 kB at 46 kB/s)
[10:39:47][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/sonatype/plexus/plexus-cipher/1.4/plexus-cipher-1.4.pom
[10:39:47][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/sonatype/plexus/plexus-cipher/1.4/plexus-cipher-1.4.pom (2.1 kB at 22 kB/s)
[10:39:47][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus-component-annotations/1.5.5/plexus-component-annotations-1.5.5.pom
[10:39:47][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus-component-annotations/1.5.5/plexus-component-annotations-1.5.5.pom (815 B at 8.9 kB/s)
[10:39:47][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus-containers/1.5.5/plexus-containers-1.5.5.pom
[10:39:47][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus-containers/1.5.5/plexus-containers-1.5.5.pom (4.2 kB at 46 kB/s)
[10:39:47][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus/2.0.7/plexus-2.0.7.pom
[10:39:47][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus/2.0.7/plexus-2.0.7.pom (17 kB at 188 kB/s)
[10:39:47][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus-compiler-api/2.2/plexus-compiler-api-2.2.pom
[10:39:47][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus-compiler-api/2.2/plexus-compiler-api-2.2.pom (865 B at 7.6 kB/s)
[10:39:47][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus-compiler/2.2/plexus-compiler-2.2.pom
[10:39:47][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus-compiler/2.2/plexus-compiler-2.2.pom (3.6 kB at 36 kB/s)
[10:39:47][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus-components/1.3.1/plexus-components-1.3.1.pom
[10:39:48][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus-components/1.3.1/plexus-components-1.3.1.pom (3.1 kB at 33 kB/s)
[10:39:48][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus/3.3.1/plexus-3.3.1.pom
[10:39:48][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus/3.3.1/plexus-3.3.1.pom (20 kB at 207 kB/s)
[10:39:48][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/sonatype/spice/spice-parent/17/spice-parent-17.pom
[10:39:48][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/sonatype/spice/spice-parent/17/spice-parent-17.pom (6.8 kB at 73 kB/s)
[10:39:48][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/sonatype/forge/forge-parent/10/forge-parent-10.pom
[10:39:48][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/sonatype/forge/forge-parent/10/forge-parent-10.pom (14 kB at 141 kB/s)
[10:39:48][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus-utils/3.0.8/plexus-utils-3.0.8.pom
[10:39:48][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus-utils/3.0.8/plexus-utils-3.0.8.pom (3.1 kB at 34 kB/s)
[10:39:48][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus/3.2/plexus-3.2.pom
[10:39:48][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus/3.2/plexus-3.2.pom (19 kB at 204 kB/s)
[10:39:48][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus-compiler-manager/2.2/plexus-compiler-manager-2.2.pom
[10:39:48][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus-compiler-manager/2.2/plexus-compiler-manager-2.2.pom (690 B at 7.5 kB/s)
[10:39:48][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus-compiler-javac/2.2/plexus-compiler-javac-2.2.pom
[10:39:48][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus-compiler-javac/2.2/plexus-compiler-javac-2.2.pom (769 B at 8.4 kB/s)
[10:39:48][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus-compilers/2.2/plexus-compilers-2.2.pom
[10:39:48][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus-compilers/2.2/plexus-compilers-2.2.pom (1.2 kB at 14 kB/s)
[10:39:48][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus-container-default/1.5.5/plexus-container-default-1.5.5.pom
[10:39:48][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus-container-default/1.5.5/plexus-container-default-1.5.5.pom (2.8 kB at 30 kB/s)
[10:39:48][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus-utils/1.4.5/plexus-utils-1.4.5.pom
[10:39:49][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus-utils/1.4.5/plexus-utils-1.4.5.pom (2.3 kB at 25 kB/s)
[10:39:49][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus-classworlds/2.2.2/plexus-classworlds-2.2.2.pom
[10:39:49][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus-classworlds/2.2.2/plexus-classworlds-2.2.2.pom (4.0 kB at 43 kB/s)
[10:39:49][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/xbean/xbean-reflect/3.4/xbean-reflect-3.4.pom
[10:39:49][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/xbean/xbean-reflect/3.4/xbean-reflect-3.4.pom (2.8 kB at 27 kB/s)
[10:39:49][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/xbean/xbean/3.4/xbean-3.4.pom
[10:39:49][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/xbean/xbean/3.4/xbean-3.4.pom (19 kB at 197 kB/s)
[10:39:49][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/log4j/log4j/1.2.12/log4j-1.2.12.pom
[10:39:49][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/log4j/log4j/1.2.12/log4j-1.2.12.pom (145 B at 1.4 kB/s)
[10:39:49][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/commons-logging/commons-logging-api/1.1/commons-logging-api-1.1.pom
[10:39:49][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/commons-logging/commons-logging-api/1.1/commons-logging-api-1.1.pom (5.3 kB at 58 kB/s)
[10:39:49][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/com/google/collections/google-collections/1.0/google-collections-1.0.pom
[10:39:49][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/com/google/collections/google-collections/1.0/google-collections-1.0.pom (2.5 kB at 27 kB/s)
[10:39:49][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/com/google/google/1/google-1.pom
[10:39:49][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/com/google/google/1/google-1.pom (1.6 kB at 17 kB/s)
[10:39:49][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/junit/junit/3.8.2/junit-3.8.2.pom
[10:39:49][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/junit/junit/3.8.2/junit-3.8.2.pom (747 B at 7.5 kB/s)
[10:39:49][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-plugin-api/2.0.9/maven-plugin-api-2.0.9.jar
[10:39:49][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-artifact/2.0.9/maven-artifact-2.0.9.jar
[10:39:49][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-core/2.0.9/maven-core-2.0.9.jar
[10:39:49][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus-utils/1.5.1/plexus-utils-1.5.1.jar
[10:39:49][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-settings/2.0.9/maven-settings-2.0.9.jar
[10:39:49][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-artifact/2.0.9/maven-artifact-2.0.9.jar (89 kB at 794 kB/s)
[10:39:49][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-plugin-api/2.0.9/maven-plugin-api-2.0.9.jar (13 kB at 113 kB/s)
[10:39:49][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-plugin-parameter-documenter/2.0.9/maven-plugin-parameter-documenter-2.0.9.jar
[10:39:49][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-profile/2.0.9/maven-profile-2.0.9.jar
[10:39:49][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-settings/2.0.9/maven-settings-2.0.9.jar (49 kB at 455 kB/s)
[10:39:49][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-model/2.0.9/maven-model-2.0.9.jar
[10:39:49][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus-utils/1.5.1/plexus-utils-1.5.1.jar (211 kB at 1.3 MB/s)
[10:39:49][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-repository-metadata/2.0.9/maven-repository-metadata-2.0.9.jar
[10:39:50][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-core/2.0.9/maven-core-2.0.9.jar (160 kB at 956 kB/s)
[10:39:50][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-error-diagnostics/2.0.9/maven-error-diagnostics-2.0.9.jar
[10:39:50][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-plugin-parameter-documenter/2.0.9/maven-plugin-parameter-documenter-2.0.9.jar (21 kB at 109 kB/s)
[10:39:50][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-project/2.0.9/maven-project-2.0.9.jar
[10:39:50][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-profile/2.0.9/maven-profile-2.0.9.jar (35 kB at 179 kB/s)
[10:39:50][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-plugin-registry/2.0.9/maven-plugin-registry-2.0.9.jar
[10:39:50][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-model/2.0.9/maven-model-2.0.9.jar (87 kB at 414 kB/s)
[10:39:50][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-plugin-descriptor/2.0.9/maven-plugin-descriptor-2.0.9.jar
[10:39:50][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-repository-metadata/2.0.9/maven-repository-metadata-2.0.9.jar (25 kB at 96 kB/s)
[10:39:50][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-artifact-manager/2.0.9/maven-artifact-manager-2.0.9.jar
[10:39:50][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-error-diagnostics/2.0.9/maven-error-diagnostics-2.0.9.jar (14 kB at 54 kB/s)
[10:39:50][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-monitor/2.0.9/maven-monitor-2.0.9.jar
[10:39:50][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-project/2.0.9/maven-project-2.0.9.jar (122 kB at 424 kB/s)
[10:39:50][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-toolchain/1.0/maven-toolchain-1.0.jar
[10:39:50][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-plugin-registry/2.0.9/maven-plugin-registry-2.0.9.jar (29 kB at 100 kB/s)
[10:39:50][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/shared/maven-shared-utils/0.1/maven-shared-utils-0.1.jar
[10:39:50][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-plugin-descriptor/2.0.9/maven-plugin-descriptor-2.0.9.jar (37 kB at 121 kB/s)
[10:39:50][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/com/google/code/findbugs/jsr305/2.0.1/jsr305-2.0.1.jar
[10:39:50][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-monitor/2.0.9/maven-monitor-2.0.9.jar (10 kB at 29 kB/s)
[10:39:50][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/shared/maven-shared-incremental/1.1/maven-shared-incremental-1.1.jar
[10:39:50][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-artifact-manager/2.0.9/maven-artifact-manager-2.0.9.jar (58 kB at 163 kB/s)
[10:39:50][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus-component-annotations/1.5.5/plexus-component-annotations-1.5.5.jar
[10:39:50][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-toolchain/1.0/maven-toolchain-1.0.jar (33 kB at 88 kB/s)
[10:39:50][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus-compiler-api/2.2/plexus-compiler-api-2.2.jar
[10:39:50][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/shared/maven-shared-utils/0.1/maven-shared-utils-0.1.jar (155 kB at 391 kB/s)
[10:39:50][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus-compiler-manager/2.2/plexus-compiler-manager-2.2.jar
[10:39:50][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/com/google/code/findbugs/jsr305/2.0.1/jsr305-2.0.1.jar (32 kB at 78 kB/s)
[10:39:50][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus-compiler-javac/2.2/plexus-compiler-javac-2.2.jar
[10:39:50][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/shared/maven-shared-incremental/1.1/maven-shared-incremental-1.1.jar (14 kB at 29 kB/s)
[10:39:50][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus-container-default/1.5.5/plexus-container-default-1.5.5.jar
[10:39:50][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus-compiler-api/2.2/plexus-compiler-api-2.2.jar (25 kB at 53 kB/s)
[10:39:50][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus-classworlds/2.2.2/plexus-classworlds-2.2.2.jar
[10:39:50][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus-component-annotations/1.5.5/plexus-component-annotations-1.5.5.jar (4.2 kB at 8.9 kB/s)
[10:39:50][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/xbean/xbean-reflect/3.4/xbean-reflect-3.4.jar
[10:39:50][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus-compiler-manager/2.2/plexus-compiler-manager-2.2.jar (4.6 kB at 9.2 kB/s)
[10:39:50][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/log4j/log4j/1.2.12/log4j-1.2.12.jar
[10:39:50][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus-compiler-javac/2.2/plexus-compiler-javac-2.2.jar (19 kB at 36 kB/s)
[10:39:50][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/commons-logging/commons-logging-api/1.1/commons-logging-api-1.1.jar
[10:39:50][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus-classworlds/2.2.2/plexus-classworlds-2.2.2.jar (46 kB at 80 kB/s)
[10:39:50][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/com/google/collections/google-collections/1.0/google-collections-1.0.jar
[10:39:50][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/xbean/xbean-reflect/3.4/xbean-reflect-3.4.jar (134 kB at 230 kB/s)
[10:39:50][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/junit/junit/3.8.2/junit-3.8.2.jar
[10:39:50][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus-container-default/1.5.5/plexus-container-default-1.5.5.jar (217 kB at 355 kB/s)
[10:39:50][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/commons-logging/commons-logging-api/1.1/commons-logging-api-1.1.jar (45 kB at 73 kB/s)
[10:39:50][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/log4j/log4j/1.2.12/log4j-1.2.12.jar (358 kB at 565 kB/s)
[10:39:50][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/junit/junit/3.8.2/junit-3.8.2.jar (121 kB at 175 kB/s)
[10:39:50][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/com/google/collections/google-collections/1.0/google-collections-1.0.jar (640 kB at 879 kB/s)
[10:39:50][Step 1/1] [INFO] Changes detected - recompiling the module!
[10:39:50][Step 1/1] [WARNING] File encoding has not been set, using platform encoding UTF-8, i.e. build is platform dependent!
[10:39:50][Step 1/1] [INFO] Compiling 2 source files to /opt/buildagent/work/4dad5dc52ced311f/target/classes
[10:39:51][Step 1/1] [INFO] 
[10:39:51][Step 1/1] [INFO] --- maven-resources-plugin:2.6:testResources (default-testResources) @ plaindoll ---
[10:39:51][Step 1/1] [WARNING] Using platform encoding (UTF-8 actually) to copy filtered resources, i.e. build is platform dependent!
[10:39:51][Step 1/1] [INFO] skip non existing resourceDirectory /opt/buildagent/work/4dad5dc52ced311f/src/test/resources
[10:39:51][Step 1/1] [INFO] 
[10:39:51][Step 1/1] [INFO] --- maven-compiler-plugin:3.1:testCompile (default-testCompile) @ plaindoll ---
[10:39:51][Step 1/1] [INFO] Changes detected - recompiling the module!
[10:39:51][Step 1/1] [WARNING] File encoding has not been set, using platform encoding UTF-8, i.e. build is platform dependent!
[10:39:51][Step 1/1] [INFO] Compiling 1 source file to /opt/buildagent/work/4dad5dc52ced311f/target/test-classes
[10:39:51][Step 1/1] [INFO] 
[10:39:51][Step 1/1] [INFO] --- maven-surefire-plugin:2.12.4:test (default-test) @ plaindoll ---
[10:39:51][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/surefire/surefire-booter/2.12.4/surefire-booter-2.12.4.pom
[10:39:51][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/surefire/surefire-booter/2.12.4/surefire-booter-2.12.4.pom (3.0 kB at 32 kB/s)
[10:39:51][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/surefire/surefire-api/2.12.4/surefire-api-2.12.4.pom
[10:39:51][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/surefire/surefire-api/2.12.4/surefire-api-2.12.4.pom (2.5 kB at 26 kB/s)
[10:39:51][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/surefire/maven-surefire-common/2.12.4/maven-surefire-common-2.12.4.pom
[10:39:51][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/surefire/maven-surefire-common/2.12.4/maven-surefire-common-2.12.4.pom (5.5 kB at 57 kB/s)
[10:39:51][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/plugin-tools/maven-plugin-annotations/3.1/maven-plugin-annotations-3.1.pom
[10:39:51][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/plugin-tools/maven-plugin-annotations/3.1/maven-plugin-annotations-3.1.pom (1.6 kB at 14 kB/s)
[10:39:51][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/plugin-tools/maven-plugin-tools/3.1/maven-plugin-tools-3.1.pom
[10:39:51][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/plugin-tools/maven-plugin-tools/3.1/maven-plugin-tools-3.1.pom (16 kB at 167 kB/s)
[10:39:51][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/reporting/maven-reporting-api/2.0.9/maven-reporting-api-2.0.9.pom
[10:39:52][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/reporting/maven-reporting-api/2.0.9/maven-reporting-api-2.0.9.pom (1.8 kB at 19 kB/s)
[10:39:52][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/reporting/maven-reporting/2.0.9/maven-reporting-2.0.9.pom
[10:39:52][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/reporting/maven-reporting/2.0.9/maven-reporting-2.0.9.pom (1.5 kB at 16 kB/s)
[10:39:52][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-toolchain/2.0.9/maven-toolchain-2.0.9.pom
[10:39:52][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-toolchain/2.0.9/maven-toolchain-2.0.9.pom (3.5 kB at 32 kB/s)
[10:39:52][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/commons/commons-lang3/3.1/commons-lang3-3.1.pom
[10:39:52][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/commons/commons-lang3/3.1/commons-lang3-3.1.pom (17 kB at 172 kB/s)
[10:39:52][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/commons/commons-parent/22/commons-parent-22.pom
[10:39:52][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/commons/commons-parent/22/commons-parent-22.pom (42 kB at 446 kB/s)
[10:39:52][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/apache/9/apache-9.pom
[10:39:52][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/apache/9/apache-9.pom (15 kB at 140 kB/s)
[10:39:52][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/shared/maven-common-artifact-filters/1.3/maven-common-artifact-filters-1.3.pom
[10:39:52][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/shared/maven-common-artifact-filters/1.3/maven-common-artifact-filters-1.3.pom (3.7 kB at 39 kB/s)
[10:39:52][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/shared/maven-shared-components/12/maven-shared-components-12.pom
[10:39:52][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/shared/maven-shared-components/12/maven-shared-components-12.pom (9.3 kB at 99 kB/s)
[10:39:52][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-parent/13/maven-parent-13.pom
[10:39:52][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-parent/13/maven-parent-13.pom (23 kB at 236 kB/s)
[10:39:52][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/apache/6/apache-6.pom
[10:39:52][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/apache/6/apache-6.pom (13 kB at 138 kB/s)
[10:39:52][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus-container-default/1.0-alpha-9/plexus-container-default-1.0-alpha-9.pom
[10:39:53][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus-container-default/1.0-alpha-9/plexus-container-default-1.0-alpha-9.pom (1.2 kB at 13 kB/s)
[10:39:53][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/surefire/surefire-booter/2.12.4/surefire-booter-2.12.4.jar
[10:39:53][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/surefire/surefire-api/2.12.4/surefire-api-2.12.4.jar
[10:39:53][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/surefire/maven-surefire-common/2.12.4/maven-surefire-common-2.12.4.jar
[10:39:53][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/commons/commons-lang3/3.1/commons-lang3-3.1.jar
[10:39:53][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/shared/maven-common-artifact-filters/1.3/maven-common-artifact-filters-1.3.jar
[10:39:53][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/surefire/surefire-booter/2.12.4/surefire-booter-2.12.4.jar (35 kB at 340 kB/s)
[10:39:53][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus-utils/3.0.8/plexus-utils-3.0.8.jar
[10:39:53][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/shared/maven-common-artifact-filters/1.3/maven-common-artifact-filters-1.3.jar (31 kB at 314 kB/s)
[10:39:53][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/reporting/maven-reporting-api/2.0.9/maven-reporting-api-2.0.9.jar
[10:39:53][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/surefire/surefire-api/2.12.4/surefire-api-2.12.4.jar (118 kB at 1.0 MB/s)
[10:39:53][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-toolchain/2.0.9/maven-toolchain-2.0.9.jar
[10:39:53][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/surefire/maven-surefire-common/2.12.4/maven-surefire-common-2.12.4.jar (263 kB at 2.1 MB/s)
[10:39:53][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/plugin-tools/maven-plugin-annotations/3.1/maven-plugin-annotations-3.1.jar
[10:39:53][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/commons/commons-lang3/3.1/commons-lang3-3.1.jar (316 kB at 2.3 MB/s)
[10:39:53][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/reporting/maven-reporting-api/2.0.9/maven-reporting-api-2.0.9.jar (10 kB at 54 kB/s)
[10:39:53][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus-utils/3.0.8/plexus-utils-3.0.8.jar (232 kB at 1.2 MB/s)
[10:39:53][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-toolchain/2.0.9/maven-toolchain-2.0.9.jar (38 kB at 192 kB/s)
[10:39:53][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/plugin-tools/maven-plugin-annotations/3.1/maven-plugin-annotations-3.1.jar (14 kB at 70 kB/s)
[10:39:53][Step 1/1] [INFO] Surefire report directory: /opt/buildagent/work/4dad5dc52ced311f/target/surefire-reports
[10:39:53][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/surefire/surefire-junit4/2.12.4/surefire-junit4-2.12.4.pom
[10:39:53][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/surefire/surefire-junit4/2.12.4/surefire-junit4-2.12.4.pom (2.4 kB at 28 kB/s)
[10:39:53][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/surefire/surefire-providers/2.12.4/surefire-providers-2.12.4.pom
[10:39:53][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/surefire/surefire-providers/2.12.4/surefire-providers-2.12.4.pom (2.3 kB at 27 kB/s)
[10:39:53][Step 1/1] [INFO] Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/surefire/surefire-junit4/2.12.4/surefire-junit4-2.12.4.jar
[10:39:53][Step 1/1] [INFO] Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/surefire/surefire-junit4/2.12.4/surefire-junit4-2.12.4.jar (37 kB at 415 kB/s)
[10:39:53][Step 1/1] 
[10:39:53][Step 1/1] -------------------------------------------------------
[10:39:53][Step 1/1]  T E S T S
[10:39:53][Step 1/1] -------------------------------------------------------
[10:39:53][Step 1/1] Running plaindoll.WelcomerTest
[10:39:54][Step 1/1] Tests run: 4, Failures: 0, Errors: 0, Skipped: 0, Time elapsed: 0.098 sec
[10:39:54][Step 1/1] 
[10:39:54][Step 1/1] Results :
[10:39:54][Step 1/1] 
[10:39:54][Step 1/1] Tests run: 4, Failures: 0, Errors: 0, Skipped: 0
[10:39:54][Step 1/1] 
[10:39:54][Step 1/1] [INFO] ------------------------------------------------------------------------
[10:39:54][Step 1/1] [INFO] BUILD SUCCESS
[10:39:54][Step 1/1] [INFO] ------------------------------------------------------------------------
[10:39:54][Step 1/1] [INFO] Total time:  21.806 s
[10:39:54][Step 1/1] [INFO] Finished at: 2022-06-09T11:39:54+01:00
[10:39:54][Step 1/1] [INFO] ------------------------------------------------------------------------
[10:39:54][Step 1/1] Process exited with code 0
[10:39:54][Step 1/1] Publishing artifacts
[10:39:54][Publishing artifacts] Collecting files to publish: [/opt/buildagent/temp/buildTmp/.tc-maven-bi/maven-build-info.xml.gz => .teamcity]
[10:39:54][Publishing artifacts] Publishing 1 file using [WebPublisher]: /opt/buildagent/temp/buildTmp/.tc-maven-bi/maven-build-info.xml.gz => .teamcity
[10:39:54][Publishing artifacts] Publishing 1 file using [ArtifactsCachePublisherImpl]: /opt/buildagent/temp/buildTmp/.tc-maven-bi/maven-build-info.xml.gz => .teamcity
[10:39:54][Step 1/1] Waiting for 2 service processes to complete
[10:39:54][Step 1/1] Surefire report watcher
[10:39:54][Surefire report watcher] 1 report found for paths:
[10:39:54][Surefire report watcher] /opt/buildagent/work/4dad5dc52ced311f/target/surefire-reports/TEST-*.xml
[10:39:54][Surefire report watcher] Successfully parsed
[10:39:54]Publishing internal artifacts
[10:39:54][Publishing internal artifacts] Publishing 1 file using [WebPublisher]
[10:39:54][Publishing internal artifacts] Publishing 1 file using [ArtifactsCachePublisherImpl]
[10:39:54]Build finished
```

</details>

4. Поменяйте условия сборки: если сборка по ветке `master`, то должен происходит `mvn clean deploy`, иначе `mvn clean test`

![image](https://github.com/PanMonsters/virt-netology/blob/3487ac808404f4fe730947472a81185521818bbf/image/9.5_3.png)

5. Для deploy будет необходимо загрузить [settings.xml](./teamcity/settings.xml) в набор конфигураций maven у teamcity, предварительно записав туда креды для подключения к nexus

![image](https://github.com/PanMonsters/virt-netology/blob/3487ac808404f4fe730947472a81185521818bbf/image/9.5_4.png)

6. В pom.xml необходимо поменять ссылки на репозиторий и nexus

7. Запустите сборку по master, убедитесь что всё прошло успешно, артефакт появился в nexus

![image](https://github.com/PanMonsters/virt-netology/blob/3487ac808404f4fe730947472a81185521818bbf/image/9.5_5.png)

<details><summary>Logs</summary>

```
[13:14:01]The build is removed from the queue to be prepared for the start
[13:14:01]Collecting changes in 1 VCS root (1s)
[13:14:01][Collecting changes in 1 VCS root] VCS Root details
[13:14:01][VCS Root details] "git@github.com:PanMonsters/example-teamcity.git#refs/heads/master" {instance id=1, parent internal id=1, parent id=Netology_GitGithubComPanMonstersExampleTeamcityGitRefsHeadsMaster, description: "git@github.com:PanMonsters/example-teamcity.git#refs/heads/master"}
[13:14:02][Collecting changes in 1 VCS root] Compute revision for 'git@github.com:PanMonsters/example-teamcity.git#refs/heads/master'
[13:14:02][Compute revision for 'git@github.com:PanMonsters/example-teamcity.git#refs/heads/master'] Upper limit revision: a3278dd574f720d3ea7c93dfd48e895a3f0de083
[13:14:02][Compute revision for 'git@github.com:PanMonsters/example-teamcity.git#refs/heads/master'] The first revision that was detected in the branch refs/heads/master: bd3bcfbfa25c0076df0a9a35343b865dc77ebfc2
[13:14:02][Compute revision for 'git@github.com:PanMonsters/example-teamcity.git#refs/heads/master'] The first revision that was detected in the branch refs/heads/master after the last change of the VCS root or checkout rules: bd3bcfbfa25c0076df0a9a35343b865dc77ebfc2
[13:14:02][Compute revision for 'git@github.com:PanMonsters/example-teamcity.git#refs/heads/master'] Latest commit attached to build configuration (with id <= 4): a3278dd574f720d3ea7c93dfd48e895a3f0de083
[13:14:02][Compute revision for 'git@github.com:PanMonsters/example-teamcity.git#refs/heads/master'] Computed revision: a3278dd574f720d3ea7c93dfd48e895a3f0de083
[13:14:02]Starting the build on the agent "teamcity-agent"
[13:14:02]Updating tools for build
[13:14:02][Updating tools for build] Found 1 tool used by the build: maven3_6
[13:14:02][Updating tools for build] All used tools are up-to-date
[13:14:03]Clearing temporary directory: /opt/buildagent/temp/buildTmp
[13:14:03]Publishing internal artifacts
[13:14:03][Publishing internal artifacts] Publishing 1 file using [WebPublisher]
[13:14:03][Publishing internal artifacts] Publishing 1 file using [ArtifactsCachePublisherImpl]
[13:14:03]Using vcs information from agent file: 4dad5dc52ced311f.xml
[13:14:03]Checkout directory: /opt/buildagent/work/4dad5dc52ced311f
[13:14:03]Updating sources: auto checkout (on agent) (6s)
[13:14:03][Updating sources] Will use agent side checkout
[13:14:03][Updating sources] VCS Root: git@github.com:PanMonsters/example-teamcity.git#refs/heads/master (6s)
[13:14:09]Step 1/2: Master (mvn clean deploy) (Maven) (8s)
[13:14:09][Step 1/2] Using predefined Maven user settings: settings.xml
[13:14:09][Step 1/2] Using predefined Maven user settings: settings.xml
[13:14:09][Step 1/2] Initial M2_HOME not set
[13:14:09][Step 1/2] Current M2_HOME = /opt/buildagent/tools/maven3_6
[13:14:09][Step 1/2] PATH = /opt/buildagent/tools/maven3_6/bin:/opt/java/openjdk/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
[13:14:09][Step 1/2] Using watcher: /opt/buildagent/plugins/mavenPlugin/maven-watcher-jdk17/maven-watcher-agent.jar
[13:14:09][Step 1/2] Using agent local repository at /opt/buildagent/system/jetbrains.maven.runner/maven.repo.local
[13:14:09][Step 1/2] *** Start reading the project structure ***
[13:14:11][Step 1/2] Initial MAVEN_OPTS not set
[13:14:11][Step 1/2] Current MAVEN_OPTS not set
[13:14:11][Step 1/2] Starting: /opt/java/openjdk/bin/java -Dagent.home.dir=/opt/buildagent -Dagent.name=teamcity-agent -Dagent.ownPort=9090 -Dagent.work.dir=/opt/buildagent/work -Dbuild.number=20 -Dbuild.vcs.number=a3278dd574f720d3ea7c93dfd48e895a3f0de083 -Dbuild.vcs.number.1=a3278dd574f720d3ea7c93dfd48e895a3f0de083 -Dbuild.vcs.number.Netology_GitGithubComPanMonstersExampleTeamcityGitRefsHeadsMaster=a3278dd574f720d3ea7c93dfd48e895a3f0de083 -Dclassworlds.conf=/opt/buildagent/temp/buildTmp/teamcity.m2.conf -Dcom.jetbrains.maven.watcher.report.file=/opt/buildagent/temp/buildTmp/maven-build-info.xml -Dec2.instance-id=epdnr2ph4agcjm1rshbo -Dec2.local-hostname=teamcity-agent.ru-central1.internal -Dec2.local-ipv4=172.16.0.17 -Dec2.public-hostname=130.193.43.16 -Dec2.public-ipv4=130.193.43.16 -Djava.io.tmpdir=/opt/buildagent/temp/buildTmp -Dmaven.home=/opt/buildagent/tools/maven3_6 -Dmaven.multiModuleProjectDirectory=/opt/buildagent/work/4dad5dc52ced311f -Dteamcity.agent.cpuBenchmark=418 -Dteamcity.agent.dotnet.agent_url=http://localhost:9090/RPC2 -Dteamcity.agent.dotnet.build_id=106 -Dteamcity.auth.password=******* -Dteamcity.auth.userId=TeamCityBuildId=106 -Dteamcity.build.changedFiles.file=/opt/buildagent/temp/buildTmp/changedFiles5236233261843781621.txt -Dteamcity.build.checkoutDir=/opt/buildagent/work/4dad5dc52ced311f -Dteamcity.build.id=106 -Dteamcity.build.properties.file=/opt/buildagent/temp/buildTmp/teamcity.build17403652667293193851.properties -Dteamcity.build.tempDir=/opt/buildagent/temp/buildTmp -Dteamcity.build.workingDir=/opt/buildagent/work/4dad5dc52ced311f -Dteamcity.buildConfName=Build -Dteamcity.buildType.id=Netology_Build -Dteamcity.configuration.properties.file=/opt/buildagent/temp/buildTmp/teamcity.config12589760277175121985.properties -Dteamcity.maven.userSettings.path=/opt/buildagent/temp/buildTmp/maven_settings_12117859169925349347.xml -Dteamcity.maven.watcher.home=/opt/buildagent/plugins/mavenPlugin/maven-watcher-jdk17 -Dteamcity.projectName=netology -Dteamcity.runner.properties.file=/opt/buildagent/temp/buildTmp/teamcity.runner249450325026128735.properties -Dteamcity.tests.recentlyFailedTests.file=/opt/buildagent/temp/buildTmp/testsToRunFirst15721401209808646952.txt "-Dteamcity.version=2022.04.1 (build 108575)" -Dmaven.repo.local=/opt/buildagent/system/jetbrains.maven.runner/maven.repo.local -classpath /opt/buildagent/tools/maven3_6/boot/plexus-classworlds-2.6.0.jar: org.codehaus.plexus.classworlds.launcher.Launcher -f /opt/buildagent/work/4dad5dc52ced311f/pom.xml -B -s /opt/buildagent/temp/buildTmp/maven_settings_12117859169925349347.xml -Dmaven.test.failure.ignore=true clean deploy
[13:14:11][Step 1/2] in directory: /opt/buildagent/work/4dad5dc52ced311f
[13:14:13][Step 1/2] [INFO] Scanning for projects...
[13:14:13][Step 1/2] [INFO] 
[13:14:13][Step 1/2] [INFO] -----------------------< org.netology:plaindoll >-----------------------
[13:14:13][Step 1/2] [INFO] Building plaindoll 0.0.2
[13:14:13][Step 1/2] [INFO] --------------------------------[ jar ]---------------------------------
[13:14:13][Step 1/2] org.netology:plaindoll (4s)
[13:14:13][Step 1/2] Importing data from '/opt/buildagent/work/4dad5dc52ced311f/target/surefire-reports/TEST-*.xml' (not existing file) with 'surefire' processor
[13:14:13][Step 1/2] Importing data from '/opt/buildagent/work/4dad5dc52ced311f/target/failsafe-reports/TEST-*.xml' (not existing file) with 'surefire' processor
[13:14:13][Step 1/2] Surefire report watcher
[13:14:13][Surefire report watcher] Watching paths:
[13:14:13][Surefire report watcher] /opt/buildagent/work/4dad5dc52ced311f/target/surefire-reports/TEST-*.xml
[13:14:13][Step 1/2] Surefire report watcher
[13:14:13][Surefire report watcher] Watching paths:
[13:14:13][Surefire report watcher] /opt/buildagent/work/4dad5dc52ced311f/target/failsafe-reports/TEST-*.xml
[13:14:13][Step 1/2] [INFO] 
[13:14:13][Step 1/2] [INFO] --- maven-clean-plugin:2.5:clean (default-clean) @ plaindoll ---
[13:14:14][Step 1/2] [INFO] Deleting /opt/buildagent/work/4dad5dc52ced311f/target
[13:14:14][Step 1/2] [INFO] 
[13:14:14][Step 1/2] [INFO] --- maven-resources-plugin:2.6:resources (default-resources) @ plaindoll ---
[13:14:14][Step 1/2] [WARNING] Using platform encoding (UTF-8 actually) to copy filtered resources, i.e. build is platform dependent!
[13:14:14][Step 1/2] [INFO] skip non existing resourceDirectory /opt/buildagent/work/4dad5dc52ced311f/src/main/resources
[13:14:14][Step 1/2] [INFO] 
[13:14:14][Step 1/2] [INFO] --- maven-compiler-plugin:3.1:compile (default-compile) @ plaindoll ---
[13:14:14][Step 1/2] [INFO] Changes detected - recompiling the module!
[13:14:14][Step 1/2] [WARNING] File encoding has not been set, using platform encoding UTF-8, i.e. build is platform dependent!
[13:14:14][Step 1/2] [INFO] Compiling 2 source files to /opt/buildagent/work/4dad5dc52ced311f/target/classes
[13:14:15][Step 1/2] [INFO] 
[13:14:15][Step 1/2] [INFO] --- maven-resources-plugin:2.6:testResources (default-testResources) @ plaindoll ---
[13:14:15][Step 1/2] [WARNING] Using platform encoding (UTF-8 actually) to copy filtered resources, i.e. build is platform dependent!
[13:14:15][Step 1/2] [INFO] skip non existing resourceDirectory /opt/buildagent/work/4dad5dc52ced311f/src/test/resources
[13:14:15][Step 1/2] [INFO] 
[13:14:15][Step 1/2] [INFO] --- maven-compiler-plugin:3.1:testCompile (default-testCompile) @ plaindoll ---
[13:14:15][Step 1/2] [INFO] Changes detected - recompiling the module!
[13:14:15][Step 1/2] [WARNING] File encoding has not been set, using platform encoding UTF-8, i.e. build is platform dependent!
[13:14:15][Step 1/2] [INFO] Compiling 1 source file to /opt/buildagent/work/4dad5dc52ced311f/target/test-classes
[13:14:15][Step 1/2] [INFO] 
[13:14:15][Step 1/2] [INFO] --- maven-surefire-plugin:2.12.4:test (default-test) @ plaindoll ---
[13:14:15][Step 1/2] [INFO] Surefire report directory: /opt/buildagent/work/4dad5dc52ced311f/target/surefire-reports
[13:14:15][Step 1/2] 
[13:14:15][Step 1/2] -------------------------------------------------------
[13:14:15][Step 1/2]  T E S T S
[13:14:15][Step 1/2] -------------------------------------------------------
[13:14:16][Step 1/2] Running plaindoll.WelcomerTest
[13:14:16][Step 1/2] Tests run: 4, Failures: 0, Errors: 0, Skipped: 0, Time elapsed: 0.122 sec
[13:14:16][Step 1/2] 
[13:14:16][Step 1/2] Results :
[13:14:16][Step 1/2] 
[13:14:16][Step 1/2] Tests run: 4, Failures: 0, Errors: 0, Skipped: 0
[13:14:16][Step 1/2] 
[13:14:16][Step 1/2] [INFO] 
[13:14:16][Step 1/2] [INFO] --- maven-jar-plugin:2.4:jar (default-jar) @ plaindoll ---
[13:14:16][Step 1/2] [INFO] Building jar: /opt/buildagent/work/4dad5dc52ced311f/target/plaindoll-0.0.2.jar
[13:14:16][Step 1/2] [INFO] 
[13:14:16][Step 1/2] [INFO] --- maven-shade-plugin:3.2.4:shade (default) @ plaindoll ---
[13:14:16][Step 1/2] [INFO] Replacing original artifact with shaded artifact.
[13:14:16][Step 1/2] [INFO] Replacing /opt/buildagent/work/4dad5dc52ced311f/target/plaindoll-0.0.2.jar with /opt/buildagent/work/4dad5dc52ced311f/target/plaindoll-0.0.2-shaded.jar
[13:14:16][Step 1/2] [INFO] 
[13:14:16][Step 1/2] [INFO] --- maven-install-plugin:2.4:install (default-install) @ plaindoll ---
[13:14:16][Step 1/2] [INFO] Installing /opt/buildagent/work/4dad5dc52ced311f/target/plaindoll-0.0.2.jar to /opt/buildagent/system/jetbrains.maven.runner/maven.repo.local/org/netology/plaindoll/0.0.2/plaindoll-0.0.2.jar
[13:14:17][Step 1/2] [INFO] Installing /opt/buildagent/work/4dad5dc52ced311f/pom.xml to /opt/buildagent/system/jetbrains.maven.runner/maven.repo.local/org/netology/plaindoll/0.0.2/plaindoll-0.0.2.pom
[13:14:17][Step 1/2] [INFO] 
[13:14:17][Step 1/2] [INFO] --- maven-deploy-plugin:2.7:deploy (default-deploy) @ plaindoll ---
[13:14:17][Step 1/2] [INFO] Uploading to nexus: http://84.201.160.130:8081/repository/maven-releases/org/netology/plaindoll/0.0.2/plaindoll-0.0.2.jar
[13:14:17][Step 1/2] [INFO] Uploaded to nexus: http://84.201.160.130:8081/repository/maven-releases/org/netology/plaindoll/0.0.2/plaindoll-0.0.2.jar (3.1 kB at 11 kB/s)
[13:14:17][Step 1/2] [INFO] Uploading to nexus: http://84.201.160.130:8081/repository/maven-releases/org/netology/plaindoll/0.0.2/plaindoll-0.0.2.pom
[13:14:17][Step 1/2] [INFO] Uploaded to nexus: http://84.201.160.130:8081/repository/maven-releases/org/netology/plaindoll/0.0.2/plaindoll-0.0.2.pom (1.5 kB at 12 kB/s)
[13:14:17][Step 1/2] [INFO] Downloading from nexus: http://84.201.160.130:8081/repository/maven-releases/org/netology/plaindoll/maven-metadata.xml
[13:14:17][Step 1/2] [INFO] Downloaded from nexus: http://84.201.160.130:8081/repository/maven-releases/org/netology/plaindoll/maven-metadata.xml (301 B at 6.0 kB/s)
[13:14:17][Step 1/2] [INFO] Uploading to nexus: http://84.201.160.130:8081/repository/maven-releases/org/netology/plaindoll/maven-metadata.xml
[13:14:17][Step 1/2] [INFO] Uploaded to nexus: http://84.201.160.130:8081/repository/maven-releases/org/netology/plaindoll/maven-metadata.xml (332 B at 3.5 kB/s)
[13:14:17][Step 1/2] [INFO] ------------------------------------------------------------------------
[13:14:17][Step 1/2] [INFO] BUILD SUCCESS
[13:14:17][Step 1/2] [INFO] ------------------------------------------------------------------------
[13:14:17][Step 1/2] [INFO] Total time:  4.435 s
[13:14:17][Step 1/2] [INFO] Finished at: 2022-06-09T14:14:17+01:00
[13:14:17][Step 1/2] [INFO] ------------------------------------------------------------------------
[13:14:18][Step 1/2] Process exited with code 0
[13:14:18][Step 1/2] Publishing artifacts
[13:14:18][Step 1/2] Waiting for 2 service processes to complete
[13:14:18][Step 1/2] Surefire report watcher
[13:14:18]Step 2/2: Master (mvn clean test) (Maven)
[13:14:18][Step 2/2] Build step Master (mvn clean test) (Maven) is skipped because of unfulfilled condition: "teamcity.build.branch does not equal master"
[13:14:18]Publishing internal artifacts
[13:14:18][Publishing internal artifacts] Publishing 1 file using [WebPublisher]
[13:14:18][Publishing internal artifacts] Publishing 1 file using [ArtifactsCachePublisherImpl]
[13:14:18]Build finished
```

</details>

8. Мигрируйте `build configuration` в репозиторий

![image](https://github.com/PanMonsters/virt-netology/blob/3487ac808404f4fe730947472a81185521818bbf/image/9.5_6.png)

[Ссылка на .teamcity](https://github.com/PanMonsters/example-teamcity/tree/master/.teamcity)

9. Создайте отдельную ветку `feature/add_reply` в репозитории

10. Напишите новый метод для класса Welcomer: метод должен возвращать произвольную реплику, содержащую слово `hunter`

Welcomer.java  

```
    public String sayHunter() {
            return "When the first hunter succumbed to the curse of blood, nightmare filled the streets of Yarnam.";
    }
```

11. Дополните тест для нового метода на поиск слова `hunter` в новой реплике

WelcomerTest.java  

```
	@Test
	public void netologySaysHunter() {
		assertThat(welcomer.sayHunter(), containsString("hunter"));
	}
```

12. Сделайте push всех изменений в новую ветку в репозиторий

13. Убедитесь что сборка самостоятельно запустилась, тесты прошли успешно

![image](https://github.com/PanMonsters/virt-netology/blob/3487ac808404f4fe730947472a81185521818bbf/image/9.5_7.png)

![image](https://github.com/PanMonsters/virt-netology/blob/3487ac808404f4fe730947472a81185521818bbf/image/9.5_8.png)

<details><summary>Master logs</summary>

```
[13:19:01]The build is removed from the queue to be prepared for the start
[13:19:01]Collecting changes in 1 VCS root (1s)
[13:19:01][Collecting changes in 1 VCS root] VCS Root details
[13:19:01][VCS Root details] "git@github.com:PanMonsters/example-teamcity.git#refs/heads/master" {instance id=1, parent internal id=1, parent id=Netology_GitGithubComPanMonstersExampleTeamcityGitRefsHeadsMaster, description: "git@github.com:PanMonsters/example-teamcity.git#refs/heads/master"}
[13:19:03][Collecting changes in 1 VCS root] Compute revision for 'git@github.com:PanMonsters/example-teamcity.git#refs/heads/master'
[13:19:03][Compute revision for 'git@github.com:PanMonsters/example-teamcity.git#refs/heads/master'] Upper limit revision: 3b59c2089f0158f610451848beb9c9da96ff0365
[13:19:03][Compute revision for 'git@github.com:PanMonsters/example-teamcity.git#refs/heads/master'] The first revision that was detected in the branch refs/heads/master: bd3bcfbfa25c0076df0a9a35343b865dc77ebfc2
[13:19:03][Compute revision for 'git@github.com:PanMonsters/example-teamcity.git#refs/heads/master'] The first revision that was detected in the branch refs/heads/master after the last change of the VCS root or checkout rules: bd3bcfbfa25c0076df0a9a35343b865dc77ebfc2
[13:19:03][Compute revision for 'git@github.com:PanMonsters/example-teamcity.git#refs/heads/master'] Latest commit attached to build configuration (with id <= 5): 3b59c2089f0158f610451848beb9c9da96ff0365
[13:19:03][Compute revision for 'git@github.com:PanMonsters/example-teamcity.git#refs/heads/master'] Computed revision: 3b59c2089f0158f610451848beb9c9da96ff0365
[13:19:03]Starting the build on the agent "teamcity-agent"
[13:19:03]Updating tools for build
[13:19:03][Updating tools for build] Found 1 tool used by the build: maven3_6
[13:19:03][Updating tools for build] All used tools are up-to-date
[13:19:03]Clearing temporary directory: /opt/buildagent/temp/buildTmp
[13:19:03]Publishing internal artifacts
[13:19:03][Publishing internal artifacts] Publishing 1 file using [WebPublisher]
[13:19:03][Publishing internal artifacts] Publishing 1 file using [ArtifactsCachePublisherImpl]
[13:19:03]Using vcs information from agent file: 4dad5dc52ced311f.xml
[13:19:03]Checkout directory: /opt/buildagent/work/4dad5dc52ced311f
[13:19:03]Updating sources: auto checkout (on agent) (5s)
[13:19:03][Updating sources] Will use agent side checkout
[13:19:03][Updating sources] VCS Root: git@github.com:PanMonsters/example-teamcity.git#refs/heads/master (5s)
[13:19:03][VCS Root: git@github.com:PanMonsters/example-teamcity.git#refs/heads/master] revision: 3b59c2089f0158f610451848beb9c9da96ff0365
[13:19:03][VCS Root: git@github.com:PanMonsters/example-teamcity.git#refs/heads/master] Git version: 2.36.1.0
[13:19:03][VCS Root: git@github.com:PanMonsters/example-teamcity.git#refs/heads/master] Update git mirror (/opt/buildagent/system/git/git-463B453E.git) (5s)
[13:19:09][VCS Root: git@github.com:PanMonsters/example-teamcity.git#refs/heads/master] Update checkout directory (/opt/buildagent/work/4dad5dc52ced311f)
[13:19:09]Step 1/2: Master (mvn clean deploy) (Maven) (9s)
[13:19:09][Step 1/2] Using predefined Maven user settings: settings.xml
[13:19:09][Step 1/2] Using predefined Maven user settings: settings.xml
[13:19:09][Step 1/2] Initial M2_HOME not set
[13:19:09][Step 1/2] Current M2_HOME = /opt/buildagent/tools/maven3_6
[13:19:09][Step 1/2] PATH = /opt/buildagent/tools/maven3_6/bin:/opt/java/openjdk/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
[13:19:09][Step 1/2] Using watcher: /opt/buildagent/plugins/mavenPlugin/maven-watcher-jdk17/maven-watcher-agent.jar
[13:19:09][Step 1/2] Using agent local repository at /opt/buildagent/system/jetbrains.maven.runner/maven.repo.local
[13:19:09][Step 1/2] *** Start reading the project structure ***
[13:19:11][Step 1/2] Initial MAVEN_OPTS not set
[13:19:11][Step 1/2] Current MAVEN_OPTS not set
[13:19:11][Step 1/2] Starting: /opt/java/openjdk/bin/java -Dagent.home.dir=/opt/buildagent -Dagent.name=teamcity-agent -Dagent.ownPort=9090 -Dagent.work.dir=/opt/buildagent/work -Dbuild.number=21 -Dbuild.vcs.number=3b59c2089f0158f610451848beb9c9da96ff0365 -Dbuild.vcs.number.1=3b59c2089f0158f610451848beb9c9da96ff0365 -Dbuild.vcs.number.Netology_GitGithubComPanMonstersExampleTeamcityGitRefsHeadsMaster=3b59c2089f0158f610451848beb9c9da96ff0365 -Dclassworlds.conf=/opt/buildagent/temp/buildTmp/teamcity.m2.conf -Dcom.jetbrains.maven.watcher.report.file=/opt/buildagent/temp/buildTmp/maven-build-info.xml -Dec2.instance-id=epdnr2ph4agcjm1rshbo -Dec2.local-hostname=teamcity-agent.ru-central1.internal -Dec2.local-ipv4=172.16.0.17 -Dec2.public-hostname=130.193.43.16 -Dec2.public-ipv4=130.193.43.16 -Djava.io.tmpdir=/opt/buildagent/temp/buildTmp -Dmaven.home=/opt/buildagent/tools/maven3_6 -Dmaven.multiModuleProjectDirectory=/opt/buildagent/work/4dad5dc52ced311f -Dteamcity.agent.cpuBenchmark=418 -Dteamcity.agent.dotnet.agent_url=http://localhost:9090/RPC2 -Dteamcity.agent.dotnet.build_id=107 -Dteamcity.auth.password=******* -Dteamcity.auth.userId=TeamCityBuildId=107 -Dteamcity.build.changedFiles.file=/opt/buildagent/temp/buildTmp/changedFiles17318294929848464102.txt -Dteamcity.build.checkoutDir=/opt/buildagent/work/4dad5dc52ced311f -Dteamcity.build.id=107 -Dteamcity.build.properties.file=/opt/buildagent/temp/buildTmp/teamcity.build5470787546927236860.properties -Dteamcity.build.tempDir=/opt/buildagent/temp/buildTmp -Dteamcity.build.workingDir=/opt/buildagent/work/4dad5dc52ced311f -Dteamcity.buildConfName=Build -Dteamcity.buildType.id=Netology_Build -Dteamcity.configuration.properties.file=/opt/buildagent/temp/buildTmp/teamcity.config13412251945824822569.properties -Dteamcity.maven.userSettings.path=/opt/buildagent/temp/buildTmp/maven_settings_10415481173199249270.xml -Dteamcity.maven.watcher.home=/opt/buildagent/plugins/mavenPlugin/maven-watcher-jdk17 -Dteamcity.projectName=netology -Dteamcity.runner.properties.file=/opt/buildagent/temp/buildTmp/teamcity.runner17549192796101879030.properties -Dteamcity.tests.recentlyFailedTests.file=/opt/buildagent/temp/buildTmp/testsToRunFirst17002302387863729791.txt "-Dteamcity.version=2022.04.1 (build 108575)" -Dmaven.repo.local=/opt/buildagent/system/jetbrains.maven.runner/maven.repo.local -classpath /opt/buildagent/tools/maven3_6/boot/plexus-classworlds-2.6.0.jar: org.codehaus.plexus.classworlds.launcher.Launcher -f /opt/buildagent/work/4dad5dc52ced311f/pom.xml -B -s /opt/buildagent/temp/buildTmp/maven_settings_10415481173199249270.xml -Dmaven.test.failure.ignore=true clean deploy
[13:19:11][Step 1/2] in directory: /opt/buildagent/work/4dad5dc52ced311f
[13:19:13][Step 1/2] [INFO] Scanning for projects...
[13:19:13][Step 1/2] [INFO] 
[13:19:13][Step 1/2] [INFO] -----------------------< org.netology:plaindoll >-----------------------
[13:19:13][Step 1/2] [INFO] Building plaindoll 0.0.2
[13:19:13][Step 1/2] [INFO] --------------------------------[ jar ]---------------------------------
[13:19:13][Step 1/2] org.netology:plaindoll (4s)
[13:19:13][Step 1/2] Importing data from '/opt/buildagent/work/4dad5dc52ced311f/target/surefire-reports/TEST-*.xml' (not existing file) with 'surefire' processor
[13:19:13][Step 1/2] Importing data from '/opt/buildagent/work/4dad5dc52ced311f/target/failsafe-reports/TEST-*.xml' (not existing file) with 'surefire' processor
[13:19:13][Step 1/2] Surefire report watcher
[13:19:13][Surefire report watcher] Watching paths:
[13:19:13][Surefire report watcher] /opt/buildagent/work/4dad5dc52ced311f/target/surefire-reports/TEST-*.xml
[13:19:13][Step 1/2] Surefire report watcher
[13:19:13][Surefire report watcher] Watching paths:
[13:19:13][Surefire report watcher] /opt/buildagent/work/4dad5dc52ced311f/target/failsafe-reports/TEST-*.xml
[13:19:13][Step 1/2] [INFO] 
[13:19:13][Step 1/2] [INFO] --- maven-clean-plugin:2.5:clean (default-clean) @ plaindoll ---
[13:19:13][Step 1/2] [INFO] Deleting /opt/buildagent/work/4dad5dc52ced311f/target
[13:19:13][Step 1/2] [INFO] 
[13:19:13][Step 1/2] [INFO] --- maven-resources-plugin:2.6:resources (default-resources) @ plaindoll ---
[13:19:14][Step 1/2] [WARNING] Using platform encoding (UTF-8 actually) to copy filtered resources, i.e. build is platform dependent!
[13:19:14][Step 1/2] [INFO] skip non existing resourceDirectory /opt/buildagent/work/4dad5dc52ced311f/src/main/resources
[13:19:14][Step 1/2] [INFO] 
[13:19:14][Step 1/2] [INFO] --- maven-compiler-plugin:3.1:compile (default-compile) @ plaindoll ---
[13:19:14][Step 1/2] [INFO] Changes detected - recompiling the module!
[13:19:14][Step 1/2] [WARNING] File encoding has not been set, using platform encoding UTF-8, i.e. build is platform dependent!
[13:19:14][Step 1/2] [INFO] Compiling 2 source files to /opt/buildagent/work/4dad5dc52ced311f/target/classes
[13:19:14][Step 1/2] [INFO] 
[13:19:14][Step 1/2] [INFO] --- maven-resources-plugin:2.6:testResources (default-testResources) @ plaindoll ---
[13:19:14][Step 1/2] [WARNING] Using platform encoding (UTF-8 actually) to copy filtered resources, i.e. build is platform dependent!
[13:19:14][Step 1/2] [INFO] skip non existing resourceDirectory /opt/buildagent/work/4dad5dc52ced311f/src/test/resources
[13:19:14][Step 1/2] [INFO] 
[13:19:14][Step 1/2] [INFO] --- maven-compiler-plugin:3.1:testCompile (default-testCompile) @ plaindoll ---
[13:19:14][Step 1/2] [INFO] Changes detected - recompiling the module!
[13:19:14][Step 1/2] [WARNING] File encoding has not been set, using platform encoding UTF-8, i.e. build is platform dependent!
[13:19:14][Step 1/2] [INFO] Compiling 1 source file to /opt/buildagent/work/4dad5dc52ced311f/target/test-classes
[13:19:15][Step 1/2] [INFO] 
[13:19:15][Step 1/2] [INFO] --- maven-surefire-plugin:2.12.4:test (default-test) @ plaindoll ---
[13:19:15][Step 1/2] [INFO] Surefire report directory: /opt/buildagent/work/4dad5dc52ced311f/target/surefire-reports
[13:19:15][Step 1/2] 
[13:19:15][Step 1/2] -------------------------------------------------------
[13:19:15][Step 1/2]  T E S T S
[13:19:15][Step 1/2] -------------------------------------------------------
[13:19:15][Step 1/2] Running plaindoll.WelcomerTest
[13:19:16][Step 1/2] Tests run: 4, Failures: 0, Errors: 0, Skipped: 0, Time elapsed: 0.111 sec
[13:19:16][Step 1/2] 
[13:19:16][Step 1/2] Results :
[13:19:16][Step 1/2] 
[13:19:16][Step 1/2] Tests run: 4, Failures: 0, Errors: 0, Skipped: 0
[13:19:16][Step 1/2] 
[13:19:16][Step 1/2] [INFO] 
[13:19:16][Step 1/2] [INFO] --- maven-jar-plugin:2.4:jar (default-jar) @ plaindoll ---
[13:19:16][Step 1/2] [INFO] Building jar: /opt/buildagent/work/4dad5dc52ced311f/target/plaindoll-0.0.2.jar
[13:19:16][Step 1/2] [INFO] 
[13:19:16][Step 1/2] [INFO] --- maven-shade-plugin:3.2.4:shade (default) @ plaindoll ---
[13:19:16][Step 1/2] [INFO] Replacing original artifact with shaded artifact.
[13:19:16][Step 1/2] [INFO] Replacing /opt/buildagent/work/4dad5dc52ced311f/target/plaindoll-0.0.2.jar with /opt/buildagent/work/4dad5dc52ced311f/target/plaindoll-0.0.2-shaded.jar
[13:19:16][Step 1/2] [INFO] 
[13:19:16][Step 1/2] [INFO] --- maven-install-plugin:2.4:install (default-install) @ plaindoll ---
[13:19:16][Step 1/2] [INFO] Installing /opt/buildagent/work/4dad5dc52ced311f/target/plaindoll-0.0.2.jar to /opt/buildagent/system/jetbrains.maven.runner/maven.repo.local/org/netology/plaindoll/0.0.2/plaindoll-0.0.2.jar
[13:19:16][Step 1/2] [INFO] Installing /opt/buildagent/work/4dad5dc52ced311f/pom.xml to /opt/buildagent/system/jetbrains.maven.runner/maven.repo.local/org/netology/plaindoll/0.0.2/plaindoll-0.0.2.pom
[13:19:16][Step 1/2] [INFO] 
[13:19:16][Step 1/2] [INFO] --- maven-deploy-plugin:2.7:deploy (default-deploy) @ plaindoll ---
[13:19:17][Step 1/2] [INFO] Uploading to nexus: http://84.201.160.130:8081/repository/maven-releases/org/netology/plaindoll/0.0.2/plaindoll-0.0.2.jar
[13:19:17][Step 1/2] [INFO] Uploaded to nexus: http://84.201.160.130:8081/repository/maven-releases/org/netology/plaindoll/0.0.2/plaindoll-0.0.2.jar (3.1 kB at 12 kB/s)
[13:19:17][Step 1/2] [INFO] Uploading to nexus: http://84.201.160.130:8081/repository/maven-releases/org/netology/plaindoll/0.0.2/plaindoll-0.0.2.pom
[13:19:17][Step 1/2] [INFO] Uploaded to nexus: http://84.201.160.130:8081/repository/maven-releases/org/netology/plaindoll/0.0.2/plaindoll-0.0.2.pom (1.5 kB at 25 kB/s)
[13:19:17][Step 1/2] [INFO] Downloading from nexus: http://84.201.160.130:8081/repository/maven-releases/org/netology/plaindoll/maven-metadata.xml
[13:19:17][Step 1/2] [INFO] Downloaded from nexus: http://84.201.160.130:8081/repository/maven-releases/org/netology/plaindoll/maven-metadata.xml (332 B at 12 kB/s)
[13:19:17][Step 1/2] [INFO] Uploading to nexus: http://84.201.160.130:8081/repository/maven-releases/org/netology/plaindoll/maven-metadata.xml
[13:19:17][Step 1/2] [INFO] Uploaded to nexus: http://84.201.160.130:8081/repository/maven-releases/org/netology/plaindoll/maven-metadata.xml (332 B at 3.6 kB/s)
[13:19:17][Step 1/2] [INFO] ------------------------------------------------------------------------
[13:19:17][Step 1/2] [INFO] BUILD SUCCESS
[13:19:17][Step 1/2] [INFO] ------------------------------------------------------------------------
[13:19:17][Step 1/2] [INFO] Total time:  4.574 s
[13:19:17][Step 1/2] [INFO] Finished at: 2022-06-09T14:19:17+01:00
[13:19:17][Step 1/2] [INFO] ------------------------------------------------------------------------
[13:19:17][Step 1/2] Process exited with code 0
[13:19:17][Step 1/2] Publishing artifacts
[13:19:17][Publishing artifacts] Collecting files to publish: [/opt/buildagent/temp/buildTmp/.tc-maven-bi/maven-build-info.xml.gz => .teamcity]
[13:19:17][Publishing artifacts] Publishing 1 file using [WebPublisher]: /opt/buildagent/temp/buildTmp/.tc-maven-bi/maven-build-info.xml.gz => .teamcity
[13:19:17][Publishing artifacts] Publishing 1 file using [ArtifactsCachePublisherImpl]: /opt/buildagent/temp/buildTmp/.tc-maven-bi/maven-build-info.xml.gz => .teamcity
[13:19:17][Step 1/2] Waiting for 2 service processes to complete
[13:19:18][Step 1/2] Surefire report watcher
[13:19:18][Surefire report watcher] 1 report found for paths:
[13:19:18][Surefire report watcher] /opt/buildagent/work/4dad5dc52ced311f/target/surefire-reports/TEST-*.xml
[13:19:18][Surefire report watcher] Successfully parsed
[13:19:18]Step 2/2: Master (mvn clean test) (Maven)
[13:19:18][Step 2/2] Build step Master (mvn clean test) (Maven) is skipped because of unfulfilled condition: "teamcity.build.branch does not equal master"
[13:19:18]Publishing internal artifacts
[13:19:18][Publishing internal artifacts] Publishing 1 file using [WebPublisher]
[13:19:18][Publishing internal artifacts] Publishing 1 file using [ArtifactsCachePublisherImpl]
[13:19:18]Build finished
```

</details>

<details><summary>Feature/add_reply logs</summary>

```
[14:03:44]The build is removed from the queue to be prepared for the start
[14:03:44]Collecting changes in 1 VCS root (1s)
[14:03:44][Collecting changes in 1 VCS root] VCS Root details
[14:03:44][VCS Root details] "git@github.com:PanMonsters/example-teamcity.git#refs/heads/master" {instance id=1, parent internal id=1, parent id=Netology_GitGithubComPanMonstersExampleTeamcityGitRefsHeadsMaster, description: "git@github.com:PanMonsters/example-teamcity.git#refs/heads/master"}
[14:03:45][Collecting changes in 1 VCS root] Compute revision for 'git@github.com:PanMonsters/example-teamcity.git#refs/heads/master'
[14:03:45][Compute revision for 'git@github.com:PanMonsters/example-teamcity.git#refs/heads/master'] Upper limit revision: febaf00d6c3efbc43bcc88deeb1f68488b233335
[14:03:45][Compute revision for 'git@github.com:PanMonsters/example-teamcity.git#refs/heads/master'] The first revision that was detected in the branch refs/heads/feature/add_reply: febaf00d6c3efbc43bcc88deeb1f68488b233335
[14:03:45][Compute revision for 'git@github.com:PanMonsters/example-teamcity.git#refs/heads/master'] Latest commit attached to build configuration (with id <= 6): febaf00d6c3efbc43bcc88deeb1f68488b233335
[14:03:45][Compute revision for 'git@github.com:PanMonsters/example-teamcity.git#refs/heads/master'] Computed revision: febaf00d6c3efbc43bcc88deeb1f68488b233335
[14:03:45]Starting the build on the agent "teamcity-agent"
[14:03:45]Updating tools for build
[14:03:45][Updating tools for build] Found 1 tool used by the build: maven3_6
[14:03:45][Updating tools for build] All used tools are up-to-date
[14:03:45]Clearing temporary directory: /opt/buildagent/temp/buildTmp
[14:03:45]Publishing internal artifacts
[14:03:45][Publishing internal artifacts] Publishing 1 file using [WebPublisher]
[14:03:45][Publishing internal artifacts] Publishing 1 file using [ArtifactsCachePublisherImpl]
[14:03:45]Using vcs information from agent file: 4dad5dc52ced311f.xml
[14:03:45]Checkout directory: /opt/buildagent/work/4dad5dc52ced311f
[14:03:45]Updating sources: auto checkout (on agent) (5s)
[14:03:45][Updating sources] Will use agent side checkout
[14:03:45][Updating sources] VCS Root: git@github.com:PanMonsters/example-teamcity.git#refs/heads/master (5s)
[14:03:45][VCS Root: git@github.com:PanMonsters/example-teamcity.git#refs/heads/master] revision: febaf00d6c3efbc43bcc88deeb1f68488b233335
[14:03:46][VCS Root: git@github.com:PanMonsters/example-teamcity.git#refs/heads/master] Git version: 2.36.1.0
[14:03:46][VCS Root: git@github.com:PanMonsters/example-teamcity.git#refs/heads/master] Update git mirror (/opt/buildagent/system/git/git-463B453E.git) (5s)
[14:03:51][VCS Root: git@github.com:PanMonsters/example-teamcity.git#refs/heads/master] Update checkout directory (/opt/buildagent/work/4dad5dc52ced311f)
[14:03:51]Step 1/2: Master (mvn clean deploy) (Maven)
[14:03:51][Step 1/2] Build step Master (mvn clean deploy) (Maven) is skipped because of unfulfilled condition: "teamcity.build.branch equals master"
[14:03:51]Step 2/2: Master (mvn clean test) (Maven) (6s)
[14:03:51][Step 2/2] Initial M2_HOME not set
[14:03:51][Step 2/2] Current M2_HOME = /opt/buildagent/tools/maven3_6
[14:03:51][Step 2/2] PATH = /opt/buildagent/tools/maven3_6/bin:/opt/java/openjdk/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
[14:03:51][Step 2/2] Using watcher: /opt/buildagent/plugins/mavenPlugin/maven-watcher-jdk17/maven-watcher-agent.jar
[14:03:51][Step 2/2] Using agent local repository at /opt/buildagent/system/jetbrains.maven.runner/maven.repo.local
[14:03:51][Step 2/2] *** Start reading the project structure ***
[14:03:53][Step 2/2] Initial MAVEN_OPTS not set
[14:03:53][Step 2/2] Current MAVEN_OPTS not set
[14:03:53][Step 2/2] Starting: /opt/java/openjdk/bin/java -Dagent.home.dir=/opt/buildagent -Dagent.name=teamcity-agent -Dagent.ownPort=9090 -Dagent.work.dir=/opt/buildagent/work -Dbuild.number=22 -Dbuild.vcs.number=febaf00d6c3efbc43bcc88deeb1f68488b233335 -Dbuild.vcs.number.1=febaf00d6c3efbc43bcc88deeb1f68488b233335 -Dbuild.vcs.number.Netology_GitGithubComPanMonstersExampleTeamcityGitRefsHeadsMaster=febaf00d6c3efbc43bcc88deeb1f68488b233335 -Dclassworlds.conf=/opt/buildagent/temp/buildTmp/teamcity.m2.conf -Dcom.jetbrains.maven.watcher.report.file=/opt/buildagent/temp/buildTmp/maven-build-info.xml -Dec2.instance-id=epdnr2ph4agcjm1rshbo -Dec2.local-hostname=teamcity-agent.ru-central1.internal -Dec2.local-ipv4=172.16.0.17 -Dec2.public-hostname=130.193.43.16 -Dec2.public-ipv4=130.193.43.16 -Djava.io.tmpdir=/opt/buildagent/temp/buildTmp -Dmaven.home=/opt/buildagent/tools/maven3_6 -Dmaven.multiModuleProjectDirectory=/opt/buildagent/work/4dad5dc52ced311f -Dteamcity.agent.cpuBenchmark=418 -Dteamcity.agent.dotnet.agent_url=http://localhost:9090/RPC2 -Dteamcity.agent.dotnet.build_id=108 -Dteamcity.auth.password=******* -Dteamcity.auth.userId=TeamCityBuildId=108 -Dteamcity.build.changedFiles.file=/opt/buildagent/temp/buildTmp/changedFiles7128500707067147307.txt -Dteamcity.build.checkoutDir=/opt/buildagent/work/4dad5dc52ced311f -Dteamcity.build.id=108 -Dteamcity.build.properties.file=/opt/buildagent/temp/buildTmp/teamcity.build11921833310124394558.properties -Dteamcity.build.tempDir=/opt/buildagent/temp/buildTmp -Dteamcity.build.workingDir=/opt/buildagent/work/4dad5dc52ced311f -Dteamcity.buildConfName=Build -Dteamcity.buildType.id=Netology_Build -Dteamcity.configuration.properties.file=/opt/buildagent/temp/buildTmp/teamcity.config14165752639207701495.properties -Dteamcity.maven.watcher.home=/opt/buildagent/plugins/mavenPlugin/maven-watcher-jdk17 -Dteamcity.projectName=netology -Dteamcity.runner.properties.file=/opt/buildagent/temp/buildTmp/teamcity.runner9607984964773062617.properties -Dteamcity.tests.recentlyFailedTests.file=/opt/buildagent/temp/buildTmp/testsToRunFirst4303271254413957311.txt "-Dteamcity.version=2022.04.1 (build 108575)" -Dmaven.repo.local=/opt/buildagent/system/jetbrains.maven.runner/maven.repo.local -classpath /opt/buildagent/tools/maven3_6/boot/plexus-classworlds-2.6.0.jar: org.codehaus.plexus.classworlds.launcher.Launcher -f /opt/buildagent/work/4dad5dc52ced311f/pom.xml -B clean test
[14:03:53][Step 2/2] in directory: /opt/buildagent/work/4dad5dc52ced311f
[14:03:55][Step 2/2] [INFO] Scanning for projects...
[14:03:55][Step 2/2] [INFO] 
[14:03:55][Step 2/2] [INFO] -----------------------< org.netology:plaindoll >-----------------------
[14:03:55][Step 2/2] [INFO] Building plaindoll 0.1.2
[14:03:55][Step 2/2] [INFO] --------------------------------[ jar ]---------------------------------
[14:03:55][Step 2/2] org.netology:plaindoll (2s)
[14:03:55][Step 2/2] Importing data from '/opt/buildagent/work/4dad5dc52ced311f/target/surefire-reports/TEST-*.xml' (not existing file) with 'surefire' processor
[14:03:55][Step 2/2] Surefire report watcher
[14:03:55][Surefire report watcher] Watching paths:
[14:03:55][Surefire report watcher] /opt/buildagent/work/4dad5dc52ced311f/target/surefire-reports/TEST-*.xml
[14:03:55][Step 2/2] Importing data from '/opt/buildagent/work/4dad5dc52ced311f/target/failsafe-reports/TEST-*.xml' (not existing file) with 'surefire' processor
[14:03:55][Step 2/2] [INFO] 
[14:03:55][Step 2/2] [INFO] --- maven-clean-plugin:2.5:clean (default-clean) @ plaindoll ---
[14:03:56][Step 2/2] [INFO] 
[14:03:56][Step 2/2] [INFO] --- maven-resources-plugin:2.6:resources (default-resources) @ plaindoll ---
[14:03:56][Step 2/2] Surefire report watcher
[14:03:56][Surefire report watcher] Watching paths:
[14:03:56][Surefire report watcher] /opt/buildagent/work/4dad5dc52ced311f/target/failsafe-reports/TEST-*.xml
[14:03:56][Step 2/2] [WARNING] Using platform encoding (UTF-8 actually) to copy filtered resources, i.e. build is platform dependent!
[14:03:56][Step 2/2] [INFO] skip non existing resourceDirectory /opt/buildagent/work/4dad5dc52ced311f/src/main/resources
[14:03:56][Step 2/2] [INFO] 
[14:03:56][Step 2/2] [INFO] --- maven-compiler-plugin:3.1:compile (default-compile) @ plaindoll ---
[14:03:56][Step 2/2] [INFO] Changes detected - recompiling the module!
[14:03:56][Step 2/2] [WARNING] File encoding has not been set, using platform encoding UTF-8, i.e. build is platform dependent!
[14:03:56][Step 2/2] [INFO] Compiling 2 source files to /opt/buildagent/work/4dad5dc52ced311f/target/classes
[14:03:57][Step 2/2] [INFO] 
[14:03:57][Step 2/2] [INFO] --- maven-resources-plugin:2.6:testResources (default-testResources) @ plaindoll ---
[14:03:57][Step 2/2] [WARNING] Using platform encoding (UTF-8 actually) to copy filtered resources, i.e. build is platform dependent!
[14:03:57][Step 2/2] [INFO] skip non existing resourceDirectory /opt/buildagent/work/4dad5dc52ced311f/src/test/resources
[14:03:57][Step 2/2] [INFO] 
[14:03:57][Step 2/2] [INFO] --- maven-compiler-plugin:3.1:testCompile (default-testCompile) @ plaindoll ---
[14:03:57][Step 2/2] [INFO] Changes detected - recompiling the module!
[14:03:57][Step 2/2] [WARNING] File encoding has not been set, using platform encoding UTF-8, i.e. build is platform dependent!
[14:03:57][Step 2/2] [INFO] Compiling 1 source file to /opt/buildagent/work/4dad5dc52ced311f/target/test-classes
[14:03:57][Step 2/2] [INFO] 
[14:03:57][Step 2/2] [INFO] --- maven-surefire-plugin:2.12.4:test (default-test) @ plaindoll ---
[14:03:57][Step 2/2] [INFO] Surefire report directory: /opt/buildagent/work/4dad5dc52ced311f/target/surefire-reports
[14:03:57][Step 2/2] 
[14:03:57][Step 2/2] -------------------------------------------------------
[14:03:57][Step 2/2]  T E S T S
[14:03:57][Step 2/2] -------------------------------------------------------
[14:03:57][Step 2/2] Running plaindoll.WelcomerTest
[14:03:58][Step 2/2] Tests run: 5, Failures: 0, Errors: 0, Skipped: 0, Time elapsed: 0.123 sec
[14:03:58][Step 2/2] 
[14:03:58][Step 2/2] Results :
[14:03:58][Step 2/2] 
[14:03:58][Step 2/2] Tests run: 5, Failures: 0, Errors: 0, Skipped: 0
[14:03:58][Step 2/2] 
[14:03:58][Step 2/2] [INFO] ------------------------------------------------------------------------
[14:03:58][Step 2/2] [INFO] BUILD SUCCESS
[14:03:58][Step 2/2] [INFO] ------------------------------------------------------------------------
[14:03:58][Step 2/2] [INFO] Total time:  2.485 s
[14:03:58][Step 2/2] [INFO] Finished at: 2022-06-09T15:03:58+01:00
[14:03:58][Step 2/2] [INFO] ------------------------------------------------------------------------
[14:03:58][Step 2/2] Process exited with code 0
[14:03:58][Step 2/2] Publishing artifacts
[14:03:58][Publishing artifacts] Collecting files to publish: [/opt/buildagent/temp/buildTmp/.tc-maven-bi/maven-build-info.xml.gz => .teamcity]
[14:03:58][Publishing artifacts] Publishing 1 file using [WebPublisher]: /opt/buildagent/temp/buildTmp/.tc-maven-bi/maven-build-info.xml.gz => .teamcity
[14:03:58][Publishing artifacts] Publishing 1 file using [ArtifactsCachePublisherImpl]: /opt/buildagent/temp/buildTmp/.tc-maven-bi/maven-build-info.xml.gz => .teamcity
[14:03:58][Step 2/2] Waiting for 2 service processes to complete
[14:03:58][Step 2/2] Surefire report watcher
[14:03:58][Surefire report watcher] 1 report found for paths:
[14:03:58][Surefire report watcher] /opt/buildagent/work/4dad5dc52ced311f/target/surefire-reports/TEST-*.xml
[14:03:58][Surefire report watcher] Successfully parsed
[14:03:58]Publishing internal artifacts
[14:03:58][Publishing internal artifacts] Publishing 1 file using [WebPublisher]
[14:03:58][Publishing internal artifacts] Publishing 1 file using [ArtifactsCachePublisherImpl]
[14:03:58]Build finished
```

</details>


14. Внесите изменения из произвольной ветки `feature/add_reply` в `master` через `Merge`

[Ссылка на Merge](https://github.com/PanMonsters/example-teamcity/commit/d49785028351d63d486b22f1977535a258571d79)

15. Убедитесь, что нет собранного артефакта в сборке по ветке `master`

16. Настройте конфигурацию так, чтобы она собирала `.jar` в артефакты сборки

![image](https://github.com/PanMonsters/virt-netology/blob/3487ac808404f4fe730947472a81185521818bbf/image/9.5_9.png)

17. Проведите повторную сборку мастера, убедитесь, что сбора прошла успешно и артефакты собраны

![image](https://github.com/PanMonsters/virt-netology/blob/3487ac808404f4fe730947472a81185521818bbf/image/9.5_10.png)

18. Проверьте, что конфигурация в репозитории содержит все настройки конфигурации из teamcity

![image](https://github.com/PanMonsters/virt-netology/blob/3487ac808404f4fe730947472a81185521818bbf/image/9.5_11.png)

19. В ответ предоставьте ссылку на репозиторий

[Ссылка на репозиторий](https://github.com/PanMonsters/example-teamcity/tree/master)