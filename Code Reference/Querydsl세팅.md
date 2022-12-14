# build.gradle
```java
buildscript {
 ext {
 queryDslVersion = "5.0.0"
 }
}

plugins {
 //querydsl 추가
 id "com.ewerk.gradle.plugins.querydsl" version "1.0.10"
}

dependencies {
 //querydsl 추가
 implementation "com.querydsl:querydsl-jpa:${queryDslVersion}"
 annotationProcessor "com.querydsl:querydsl-apt:${queryDslVersion}"

 //테스트에서 lombok 사용
 testCompileOnly 'org.projectlombok:lombok'
 testAnnotationProcessor 'org.projectlombok:lombok'
 testImplementation('org.springframework.boot:spring-boot-starter-test') {
 }
}

test {
 useJUnitPlatform()
}

//querydsl 추가 시작
def querydslDir = "$buildDir/generated/querydsl"
querydsl {
 jpa = true
 querydslSourcesDir = querydslDir
}
sourceSets {
 main.java.srcDir querydslDir
}
configurations {
 querydsl.extendsFrom compileClasspath
}
compileQuerydsl {
 options.annotationProcessorPath = configurations.querydsl
}
//querydsl 추가 끝
```
- querydsl-jpa , querydsl-apt 를 추가하고 버전을 명시해야 한다

### querydsl 강의때 사용한 build.gradle
```java
plugins {  
   id 'org.springframework.boot' version '2.7.3'  
   id 'io.spring.dependency-management' version '1.0.13.RELEASE'  
   id 'java'  
  
   /* querydsl 추가 */   id "com.ewerk.gradle.plugins.querydsl" version "1.0.10"  
}  
  
group = 'com.study'  
version = '0.0.1-SNAPSHOT'  
sourceCompatibility = '11'  
  
configurations {  
   compileOnly {  
      extendsFrom annotationProcessor  
   }  
}  
  
repositories {  
   mavenCentral()  
}  
  
dependencies {  
   implementation 'org.springframework.boot:spring-boot-starter-data-jpa'  
   implementation 'org.springframework.boot:spring-boot-starter-web'  
  
   /* querydsl 추가 */   implementation 'com.querydsl:querydsl-jpa'  
   annotationProcessor "com.querydsl:querydsl-apt:5.0.0:jpa"  
   annotationProcessor "jakarta.annotation:jakarta.annotation-api"  
   annotationProcessor "jakarta.persistence:jakarta.persistence-api"  
  
   /* 쿼리 로그 상세 보기 */   implementation 'com.github.gavlyukovskiy:p6spy-spring-boot-starter:1.8.0'  
  
   compileOnly 'org.projectlombok:lombok'  
   runtimeOnly 'com.h2database:h2'  
   annotationProcessor 'org.projectlombok:lombok'  
   testImplementation 'org.springframework.boot:spring-boot-starter-test'  
  
}  
  
tasks.named('test') {  
   useJUnitPlatform()  
}  
  
/* querydsl 추가 시작 */def querydslDir = "$buildDir/generated/querydsl"  
querydsl {  
   jpa = true  
   querydslSourcesDir = querydslDir  
}  
sourceSets {  
   main.java.srcDir querydslDir  
}  
configurations {  
   querydsl.extendsFrom compileClasspath  
}  
compileQuerydsl {  
   options.annotationProcessorPath = configurations.querydsl  
}  
/* querydsl 추가 끝 */
```