Sample repository to demonstrate differences in checkstyle import order checks
between version 6.x and 8.9. In the old version, there was no error for import
separation, while in the new version this is flagged as a violation.

To see the original behaviour, run
```
mvn checkstyle:checkstyle -Dcheckstyle.consoleOutput=true
```

To see the new violations, run
```
mvn checkstyle:checkstyle -Dcheckstyle.consoleOutput=true -Pcheckstyle8
```

The errors reported will be like these (local file paths may differ):
```
[INFO] --- maven-checkstyle-plugin:3.0.0:checkstyle (default-cli) @ checkstyle-poc ---
[WARNING] File encoding has not been set, using platform encoding UTF-8, i.e. build is platform dependent!
[INFO] Starting audit...
[ERROR] /Users/mdrob/IdeaProjects/checkstylepoc/src/main/java/Main.java:5: Extra separation in import group before 'com.foo.Foo' [ImportOrder]
[ERROR] /Users/mdrob/IdeaProjects/checkstylepoc/src/main/java/Main.java:7: Extra separation in import group before 'org.bar.Bar' [ImportOrder]
Audit done.
[INFO] There are 2 errors reported by Checkstyle 8.9 with src/main/resources/checkstyle.xml ruleset.
```

A `checkstyle.xml` file with `<property name="separated" value="true"/>` is also available, and 
can be used with the `separated` maven profile.
```
mvn checkstyle:checkstyle -Dcheckstyle.consoleOutput=true -Pcheckstyle8,separated
```

This version still flags a violation inside of the group:
```
[INFO] --- maven-checkstyle-plugin:3.0.0:checkstyle (default-cli) @ checkstyle-poc ---
[WARNING] File encoding has not been set, using platform encoding UTF-8, i.e. build is platform dependent!
[INFO] Starting audit...
[ERROR] /Users/mdrob/IdeaProjects/checkstylepoc/src/main/java/Main.java:7: Extra separation in import group before 'org.bar.Bar' [ImportOrder]
Audit done.
[INFO] There is 1 error reported by Checkstyle 8.9 with src/main/resources/checkstyle-separated.xml ruleset.
```
