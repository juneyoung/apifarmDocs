### API 운영반영 절차

#### 목차 
0. Project Settings
  - Maven Profiles
  - Profile location
  
1. Server Basic Settings
  - JDK
  - Apache-tomcat
  
2. File & UI Settings
  - File. `.config` files
  - UI. Server configurations
  - UI. Cache Server configurations
  - UI. Functional Configurations
  
3. Device Settings
  - Auto start with device booting
  
#### 개요
 본 문서는 MariaDB 와 CentOS7 기반으로 작성되었으며, JDK 등의 설치는 클라이언트의 요청에 따라 바이너리가 아닌 `yum` 명령으로 설치되었음. 

#### 0. Project Settings
 본 항에서는 ApiFarm 소스 단에서 배포를 위해 준비해야 될 부분들을 기술함. 
##### 0-1. Maven Profiles

프로젝트 내부의 `pom.xml` 의 `<profiles>` 에 아래와 같은 형식으로 현재 프로젝트를 설정한다.
```
<profile>
    <id>tory-api1</id>
    <activation>
        <activeByDefault>false</activeByDefault>
    </activation>
    <properties>
        <resource-path>tory-api1</resource-path>
        <tomcat-url>http://139.162.24.153:8201/manager/text</tomcat-url>
        <tomcat-user>sdp</tomcat-user>
        <tomcat-pwd>sdp</tomcat-pwd>
        <cxf-scope>compile</cxf-scope>
    </properties>
</profile>
```
- `id` :  프로젝트 아이디 기술 `default.properties` 의 `project` 항목과 일치할 것.
- `resource-path` : 프로젝트에서 참조할 설정 경로. 해당 이름으로 `/src/main/resources/` 아래에 폴더를 만들어야 하며, 하위에 `config`, `web` 이라는 하위 폴더도 만들어야 함.(후술)
- `tomcat-url` : 해당 프로젝트가 배포될 tomcat 의 매니저 경로. 
- `tomcat-user`/`tomcat-pwd` : 배포될 서버의 tomcat 매니저의 `id`/`pw` 로 일반적으로 tomcat 경로 내에 `/conf/tomcat-user.xml` 에 기술되어 있음. 위 예시와 같은 경우에는 배포될 서버의 `tomcat-user.xml` 에 `<user username="sdp" password="sdp" roles="admin,manager,manager-gui,manager-script"/>` 라는 내용이 있어야 함.

#### 99. History
- 07.MAR.17 : 최초 작성 
- 09.MAR.17 : maven profile 항목 추가 
