```xml
<profile id="aws.small" pluginId="aws">
  <property>
    <key>instance-type</key>
    <value>m1.small</value>
  </property>
</profile>
...
<job name="unit-tests"
     elasticProfileId="aws.small">
</job>
```
